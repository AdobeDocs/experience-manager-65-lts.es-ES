---
title: 'Desarrollo de AEM: directrices y prácticas recomendadas'
description: Directrices y prácticas recomendadas para el desarrollo en AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 1%

---

# Desarrollo de AEM: directrices y prácticas recomendadas{#aem-development-guidelines-and-best-practices}

## Directrices para el uso de plantillas y componentes {#guidelines-for-using-templates-and-components}

Los componentes y las plantillas de Adobe Experience Manager (AEM) conforman un potente conjunto de herramientas. Los desarrolladores pueden utilizarlas para proporcionar a los usuarios, editores y administradores de sitios web la funcionalidad de adaptar sus sitios web a las cambiantes necesidades comerciales (agilidad de contenido). Todo esto manteniendo el diseño uniforme de los sitios (protección de marca).

Un desafío típico para una persona responsable de un sitio web o un conjunto de sitios web (por ejemplo, en una sucursal de una empresa global) es introducir un nuevo tipo de presentación de contenido en sus sitios web.

Supongamos que es necesario agregar una página de lista de noticias a los sitios web, que enumera extractos de otros artículos ya publicados. La página debe tener el mismo diseño y estructura que el resto del sitio web.

La manera recomendada de abordar ese problema sería la siguiente:

* Reutilice una plantilla existente para poder crear un tipo de página. La plantilla define aproximadamente la estructura de la página (elementos de navegación, paneles, etc.), que se ajusta aún más por su diseño (CSS, gráficos).
* Utilice el sistema de párrafos (parsys/iparsys) en las páginas nuevas.
* Defina el derecho de acceso al modo Diseño de los sistemas de párrafos, de modo que solo las personas autorizadas (normalmente el administrador) puedan cambiarlas.
* Defina los componentes permitidos en el sistema de párrafos determinado para que los editores puedan colocar los componentes necesarios en la página. En este caso, podría ser un componente de lista, que puede atravesar un subárbol de páginas y extraer la información según reglas predefinidas.
* Los editores agregan y configuran los componentes permitidos en las páginas de las que son responsables para entregar la funcionalidad solicitada (información) a la empresa.

Esto ilustra cómo este enfoque permite a los usuarios y administradores colaboradores del sitio web responder a las necesidades comerciales rápidamente, sin requerir la participación de equipos de desarrollo. Los métodos alternativos, como la creación de una plantilla, suelen ser un ejercicio costoso, que requiere un proceso de gestión del cambio y la participación del equipo de desarrollo. Esto hace que todo el proceso sea más largo y costoso.

Por lo tanto, los desarrolladores de sistemas basados en AEM deben utilizar:

* plantillas y control de acceso al diseño del sistema de párrafos para la uniformidad y la protección de la marca
* sistema de párrafos, incluidas sus opciones de configuración para una mayor flexibilidad.

Las siguientes reglas generales para desarrolladores tienen sentido en la mayoría de los proyectos habituales:

* Mantenga el número de plantillas bajo, tan bajo como el número de estructuras de página fundamentalmente diferentes en los sitios web.
* Proporcione la flexibilidad y las capacidades de configuración necesarias a los componentes personalizados.
* Maximice el uso de la potencia y la flexibilidad del sistema de párrafos de AEM: los componentes parsys e iparsys.

### Personalizar componentes y otros elementos {#customizing-components-and-other-elements}

Al crear sus propios componentes o personalizar un componente existente, a menudo es más fácil (y seguro) reutilizar las definiciones existentes. Los mismos principios se aplican también a otros elementos de AEM, por ejemplo, el gestor de errores.

Esto se puede hacer copiando y superponiendo la definición existente. En otras palabras, copiando la definición de `/libs` a `/apps/<your-project>`. Esta nueva definición, en `/apps`, se puede actualizar según sus necesidades.

>[!NOTE]
>
>Consulte [Uso de superposiciones](/help/sites-developing/overlays.md) para obtener más información.

Por ejemplo:

* [Personalizar un componente](/help/sites-developing/components.md)

  Esto implicaba superponer una definición de componente:

   * Cree una carpeta de componentes en `/apps/<website-name>/components/<MyComponent>` copiando un componente existente:

      * Por ejemplo, para personalizar la copia del componente Texto:

         * de `/libs/foundation/components/text`
         * hasta `/apps/myProject/components/text`

* [Personalizar páginas mostradas por el Controlador de errores](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Este caso implica la superposición de un servlet:

   * En el repositorio, copie uno o más scripts predeterminados:

      * de `/libs/sling/servlet/errorhandler/`
      * hasta `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**No** cambie nada en la ruta de acceso `/libs`.
>
>El motivo es que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
>
>Para cambios de configuración y de otro tipo:
>
>1. copiar el elemento de `/libs` en `/apps`
>1. realice cualquier cambio dentro de `/apps`

## Cuándo utilizar Consultas JCR y cuándo no utilizarlas {#when-to-use-jcr-queries-and-when-not-to-use-them}

Las consultas JCR son una herramienta potente cuando se utilizan correctamente. Son adecuados para:

* consultas reales del usuario final, como búsquedas de texto completo en el contenido.
* ocasiones en las que el contenido estructurado debe encontrarse en todo el repositorio.

  En estos casos, asegúrese de que las consultas solo se ejecuten cuando sea necesario. Por ejemplo, en la activación de componentes o la invalidación de caché (a diferencia de, por ejemplo, Pasos de flujos de trabajo, Controladores de eventos que almacenan en déclencheur las modificaciones de contenido y Filtros).

Nunca utilice Consultas JCR para solicitudes de procesamiento puras. Por ejemplo, las consultas JCR no son adecuadas para lo siguiente:

* navegación de procesamiento
* información general sobre la creación de las 10 noticias más recientes
* mostrar recuentos de elementos de contenido

Para procesar contenido, utilice el acceso de navegación al árbol de contenido en lugar de realizar una consulta JCR.

>[!NOTE]
>
>Si usa el [Generador de consultas](/help/sites-developing/querybuilder-api.md), usará Consultas JCR, ya que el Generador de consultas genera Consultas JCR bajo el capó.
>

## Consideraciones de seguridad {#security-considerations}

>[!NOTE]
>
>También vale la pena hacer referencia a la [lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

### Sesiones JCR (repositorio) {#jcr-repository-sessions}

Utilice la sesión del usuario, no la sesión administrativa. Esto significa que debe utilizar:

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Proteger contra scripts en sitios múltiples (XSS) {#protect-against-cross-site-scripting-xss}

El proceso de ejecución de scripts en sitios múltiples (XSS) permite a los atacantes insertar código en páginas web que han visto otros usuarios. Los usuarios web malintencionados pueden aprovechar esta vulnerabilidad de seguridad para evitar los controles de acceso.

AEM aplica el principio de filtrar todo el contenido proporcionado por el usuario al generar la salida. La prevención de XSS tiene la máxima prioridad tanto durante el desarrollo como durante las pruebas.

Además, un firewall de aplicaciones web, como [mod_security para Apache](https://modsecurity.org), puede proporcionar un control central y confiable sobre la seguridad del entorno de implementación y protegerlo contra ataques de scripts entre sitios que no se habían detectado anteriormente.

>[!CAUTION]
>
>El código de ejemplo proporcionado con AEM puede no protegerse contra estos ataques y generalmente depende del filtrado de solicitudes por un cortafuegos de aplicaciones web.

La hoja de trucos de la API XSS contiene información que debe saber para utilizar la API XSS y hacer que una aplicación de AEM sea más segura. Puede descargarlo aquí:

La hoja de trucos de XSSAPI.

[Obtener archivo](assets/xss_cheat_sheet_2016.pdf)

### Proteger la comunicación de información confidencial {#securing-communication-for-confidential-information}

Como para cualquier aplicación de Internet, asegúrese de que al transportar información confidencial

* el tráfico está protegido mediante SSL
* HTTP POST se utiliza si corresponde

Esto se aplica a la información que es confidencial para el sistema (como la configuración o el acceso administrativo) y a la información confidencial para sus usuarios (como sus datos personales)

## Tareas de desarrollo distintas {#distinct-development-tasks}

### Personalización de páginas de error {#customizing-error-pages}

Las páginas de error se pueden personalizar para AEM. Esto es aconsejable para que la instancia no muestre los seguimientos de sling en los errores internos del servidor.

Consulte [Personalización de páginas de error mostradas por el controlador de error](/help/sites-developing/customizing-errorhandler-pages.md) para obtener información detallada.

### Abrir archivos en el proceso de Java™ {#open-files-in-the-java-process}

Dado que AEM puede acceder a muchos archivos, se recomienda que el número de [archivos abiertos para un proceso Java™](/help/sites-deploying/configuring.md#open-files-in-the-java-process) se configure explícitamente para AEM.

Para minimizar este problema, el desarrollo debe garantizar que cualquier archivo abierto se cierre correctamente cuando (de forma significativa) sea posible.
