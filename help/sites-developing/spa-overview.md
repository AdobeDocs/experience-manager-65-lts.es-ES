---
title: Información general del editor de SPA
description: Este artículo ofrece una información general completa del Editor de SPA y cómo funciona, e incluye flujos de trabajo detallados de interacción del Editor de SPA dentro de AEM.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: b179ca99-c9c6-435a-b000-c7f3fd15cd53
index: false
source-git-commit: f6a3d16c55a6b62aea9a374904339e16d30f0a75
workflow-type: tm+mt
source-wordcount: '1626'
ht-degree: 85%

---


# Información general del editor de SPA{#spa-editor-overview}

Las aplicaciones de una sola página (SPA) pueden ofrecer experiencias atractivas para los usuarios de sitios web. Los desarrolladores quieren poder generar sitios usando marcos de SPA y los autores quieren editar contenido dentro de AEM para un sitio generado usando dichos marcos.

El Editor de SPA ofrece una solución completa para admitir las SPA dentro de AEM. Esta página proporciona información general sobre cómo se estructura el soporte de las SPA en AEM, cómo funciona el Editor de SPA y cómo el marco de trabajo de las SPA y AEM se mantiene sincronizado.

{{ue-over-spa}}

## Introducción {#introduction}

Los sitios creados con marcos de trabajo de las SPA comunes, como React y Angular, cargan su contenido a través de JSON dinámico y no proporcionan la estructura de HTML necesaria para que el Editor de páginas de AEM pueda colocar controles de edición.

Para permitir la edición de las SPA dentro de AEM, se necesita una asignación entre la salida JSON de las SPA y el modelo de contenido en el repositorio AEM para guardar los cambios en el contenido.

El soporte de las SPA en AEM introduce una capa delgada de JS que interactúa con el código JS de las SPA cuando se carga en el Editor de páginas con el que se pueden enviar eventos y activar la ubicación de los controles de edición para permitir la edición en contexto. Esta función se basa en el concepto de punto final de la API de Servicios de contenido, ya que el contenido de las SPA debe cargarse a través de los Servicios de contenido.

Para obtener más información sobre las SPA en AEM, consulte los siguientes documentos:

* [Modelo de SPA](/help/sites-developing/spa-blueprint.md) para los requisitos técnicos de una SPA
* [Introducción a las SPA en AEM](/help/sites-developing/spa-getting-started-react.md) para ver un recorrido rápido por una SPA sencilla

## Diseño {#design}

El componente de página de una SPA no proporciona los elementos HTML de sus componentes secundarios a través del archivo JSP o HTL. Esta operación se delega al marco de trabajo de las SPA. La representación de componentes o modelos secundarios se obtiene como una estructura de datos JSON del JCR. A continuación, se añaden los componentes de las SPA a la página según esa estructura. Este comportamiento diferencia la composición inicial del cuerpo del componente de página de las contrapartes que no son de las SPA.

### Administración de modelos de página {#page-model-management}

La resolución y la gestión del modelo de página se delegan a la biblioteca `PageModel`. La SPA debe utilizar la biblioteca de modelo de página para que se inicialice y sea creada por el Editor de SPA. La biblioteca Modelo de página se proporciona indirectamente al componente de Página de AEM a través del npm `aem-react-editable-components`. El Modelo de página es un intérprete entre el AEM y las SPA y, por lo tanto, siempre debe estar presente. Cuando se crea la página, se debe agregar una biblioteca adicional `cq.authoring.pagemodel.messaging` para habilitar la comunicación con el editor de páginas.

Si el componente de página de las SPA hereda del componente principal de página, hay dos opciones para hacer que la categoría de la biblioteca de cliente `cq.authoring.pagemodel.messaging` esté disponible:

* Si la plantilla es editable, agréguela a la política de la página.
* O agregue las categorías utilizando `customfooterlibs.html`.

Para cada recurso del modelo exportado, las SPA se asignarán a un componente real que realizará la 
renderización. El modelo, representado como JSON, se procesa a continuación utilizando las asignaciones de componentes dentro de un contenedor.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>La inclusión de la categoría `cq.authoring.pagemodel.messaging` debe limitarse al contexto del Editor de SPA.

### Tipo de datos de comunicación {#communication-data-type}

Cuando la categoría `cq.authoring.pagemodel.messaging` se añade a la página, envía un mensaje al Editor de páginas para establecer el tipo de datos de comunicación JSON. Cuando el tipo de datos de comunicación se establece en JSON, las solicitudes de GET se comunican con los puntos finales del modelo Sling de un componente. Una vez que se produce una actualización de estado en el editor de páginas, la representación JSON del componente actualizado se envía a la biblioteca del Modelo de página. A continuación, la biblioteca del Modelo de página informa a las SPA de las actualizaciones.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Flujo de trabajo {#workflow}

Puede comprender el flujo de la interacción entre las SPA y el AEM pensando en el Editor de SPA como un mediador entre ambos.

* La comunicación entre el editor de páginas y las SPA se realiza mediante JSON en lugar de HTML.
* El editor de páginas proporciona la versión más reciente del modelo de página a las SPA mediante el iframe y la API de mensajería.
* El administrador de modelos de página notifica al editor que está listo para la edición y pasa el modelo de página como una estructura JSON.
* El editor no modifica ni accede a la estructura DOM de la página que se está creando, sino que proporciona el último modelo de página.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Flujo de trabajo del Editor de SPA básico {#basic-spa-editor-workflow}

Teniendo en cuenta los elementos clave del Editor de SPA, el flujo de trabajo de alto nivel de edición de una SPA dentro de AEM aparece para el autor de la siguiente manera.

![sin título1](assets/untitled1.gif)

1. Se carga el Editor de SPA.
1. La SPA se carga en un fotograma independiente.
1. La SPA solicita contenido JSON y procesa componentes en el lado del cliente.
1. El Editor de SPA detecta los componentes procesados y genera superposiciones.
1. El autor hace clic en la superposición y muestra la barra de herramientas de edición del componente.
1. El Editor de SPA mantiene las ediciones con una petición POST al servidor.
1. El Editor de SPA solicita JSON actualizado al Editor de SPA, que se envía a la SPA con un evento DOM.
1. SPA vuelve a procesar el componente correspondiente, actualizando su DOM.

>[!NOTE]
>
>Tenga en cuenta lo siguiente:
>
>* La SPA siempre está a cargo de su visualización.
>* El editor de SPA está aislado de la propia SPA.
>* En producción (publicación), el editor de SPA nunca se carga.
>

### Flujo de trabajo de edición de páginas cliente-servidor {#client-server-page-editing-workflow}

Esta es una descripción más detallada de la interacción cliente-servidor al editar una SPA.

![page_editor_spa_authingmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. La SPA se inicializa y solicita el modelo de página desde Sling Model Exporter.
1. Sling Model Exporter solicita al repositorio los recursos que componen la página.
1. El repositorio devuelve los recursos.
1. Sling Model Exporter devuelve el modelo de la página.
1. La SPA crea una instancia de sus componentes basada en el modelo de página.
1. **6a** El contenido informa al editor de que está listo para la creación.

   **6b** El editor de páginas solicita las configuraciones de creación de componentes.

   **6c** El editor de páginas recibe las configuraciones de componentes.
1. Cuando el autor edita un componente, el editor de páginas publica una solicitud de modificación en el servlet de POST predeterminado.
1. El recurso se actualiza en el repositorio.
1. El recurso actualizado se proporciona al servlet de POST.
1. El servlet de POST predeterminado informa al editor de páginas de que el recurso se ha actualizado.
1. El editor de páginas solicita el nuevo modelo de página.
1. Los recursos que componen la página se solicitan al repositorio.
1. El repositorio proporciona los recursos que componen la página a Sling Model Exporter.
1. El modelo de página actualizado se devuelve al editor.
1. El editor de páginas actualiza la referencia del modelo de página de la SPA.
1. La SPA actualiza sus componentes en función de la nueva referencia del modelo de página.
1. Se actualizan las configuraciones de componentes de los editores de páginas.

   **17a** La SPA indica al editor de páginas que el contenido está listo.

   **17b** El editor de páginas proporciona a la SPA configuraciones de componentes.

   **17c** La SPA proporciona configuraciones de componentes actualizadas.

### Flujo de trabajo de creación {#authoring-workflow}

Esta es una descripción más detallada que se centra en la experiencia de creación.

![modelo spa_content_authingmodel](assets/spa_content_authoringmodel.png)

1. La SPA toma el modelo de página.
1. **2a** El modelo de página proporciona al editor los datos necesarios para la creación.

   **2b** Cuando se le notifica, el orquestador de componentes actualiza la estructura de contenido de la página.
1. El orquestador de componentes consulta la asignación entre un tipo de recurso AEM y un componente SPA.
1. El orquestador de componentes crea una instancia dinámica del componente SPA en función del modelo de página y de la asignación de componentes.
1. El editor de páginas actualiza el modelo de página.
1. **6a** El modelo de página proporciona datos de creación actualizados al editor de páginas.

   **6b** El modelo de página envía cambios al orquestador de componentes.
1. El orquestador de componentes recupera la asignación de componentes.
1. El orquestador de componentes actualiza el contenido de la página.
1. Cuando la SPA termina de actualizar el contenido de la página, el editor de páginas carga el entorno de creación.

## Requisitos y limitaciones {#requirements-limitations}

Para permitir que el autor utilice el editor de páginas para editar el contenido de una SPA, la aplicación de SPA debe implementarse para interactuar con el SDK del editor de SPA de AEM. Consulte [Introducción a las SPA en AEM](/help/sites-developing/spa-getting-started-react.md) para saber lo mínimo que necesita saber para poner en marcha el suyo.

### Marcos de trabajo compatibles {#supported-frameworks}

El SDK del editor de SPA admite las versiones mínimas siguientes:

* React 16.x y posteriores
* Angular 6.x y superior

Las versiones anteriores de estos marcos de trabajo pueden funcionar con el Editor de SDK de SPA de AEM, pero no son compatibles.

### Marcos de trabajo adicionales {#additional-frameworks}

Se pueden implementar marcos de SPA adicionales para trabajar con el Editor de SDK de SPA de AEM. Consulte el [modelo de SPA](/help/sites-developing/spa-blueprint.md) para conocer los requisitos que debe cumplir un marco de trabajo para crear una capa específica de marco de trabajo compuesta de módulos, componentes y servicios para trabajar con el Editor de SPA de AEM.

### Uso de varios selectores {#multiple-selectors}

Se pueden definir y utilizar selectores personalizados adicionales como parte de un SPA desarrollado para el SDK de SPA de AEM. Sin embargo, esta compatibilidad requiere que el selector `model` sea el primer selector y que la extensión sea `.json`, ya que [el exportador JSON lo requiere.](json-exporter-components.md#multiple-selectors)

### Requisitos del editor de texto {#text-editor-requirements}

Si desea utilizar el editor in situ de un componente de texto creado en la SPA, se requiere una configuración adicional.

1. Establezca un atributo (puede ser cualquiera) en el elemento contenedor que encierra el texto HTML. Si hay contenido de muestra de WKND Journal, es un elemento `<div>` y el selector que se ha utilizado es `data-rte-editelement`.
1. Establezca la configuración `editElementQuery` en el componente de texto de AEM correspondiente `cq:InplaceEditingConfig` que apunte a ese selector, por ejemplo, `data-rte-editelement`. Esto permite al editor saber qué elemento de HTML ajusta el texto HTML.

Para ver un ejemplo de cómo se hace, vea el contenido de muestra de [WKND Journal.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

Para obtener información adicional acerca de la propiedad `editElementQuery` y la configuración del editor de texto enriquecido, consulte [Configuración del Editor de texto enriquecido.](/help/sites-administering/rich-text-editor.md)

### Restricciones {#limitations}

AEM SPA Editor SDK se introdujo con AEM 6.4 Service Pack 2. Es totalmente compatible con Adobe y se sigue mejorando y ampliando. El Editor de SPA aún no admite las siguientes funciones de AEM:

* Modo de destinatario
* ContextHub
* Edición de imágenes en línea
* Editar configuraciones (p. ej., oyentes)
* Deshacer, Rehacer
* Diferencias de página y Deformación de tiempo
* Funciones que realizan la reescritura de HTML en el lado del servidor, como Verificador de vínculos, Servicio de reescritura de CDN, Acortamiento de URL, etc.
* Modo de desarrollador
* Lanzamientos de AEM
