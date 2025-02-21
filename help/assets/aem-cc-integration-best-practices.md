---
title: Integración con las prácticas recomendadas de Adobe Creative Cloud
description: Prácticas recomendadas para integrar [!DNL Adobe Experience Manager] con [!DNL Adobe Creative Cloud] para optimizar los flujos de trabajo de transferencia de recursos y lograr una alta velocidad de contenido.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3173'
ht-degree: 11%

---

# Prácticas recomendadas de integración de [!DNL Adobe Experience Manager] y [!DNL Creative Cloud] {#aem-and-creative-cloud-integration-best-practices}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Experience Manager Assets] es una solución de administración de recursos digitales (DAM) que se puede integrar con [!DNL Adobe Creative Cloud] para ayudar a los usuarios de DAM a trabajar junto con los equipos creativos, lo que optimiza la colaboración en el proceso de creación de contenido.

[!DNL Adobe Creative Cloud] proporciona a los equipos creativos un ecosistema de soluciones y servicios para ayudarles a crear recursos digitales. Incluye aplicaciones de escritorio y móviles, servicios en la nube como almacenamiento con sincronización de escritorio o experiencia web, y mercados como [!DNL Adobe Stock].

Continúe leyendo para saber qué integraciones elegir entre el escritorio y el DAM de nivel empresarial en función de su caso de uso y cuáles son las prácticas recomendadas asociadas para los flujos de trabajo de conexión.

>[!NOTE]
>
>El uso compartido de carpetas de [!DNL Experience Manager] a [!DNL Creative Cloud] está obsoleto y ya no se trata en esta guía. Adobe recomienda usar funcionalidades más recientes, como [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) o [Experience Manager desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html), para proporcionar al usuario creativo acceso a los recursos administrados en [!DNL Experience Manager].

## Necesidades de Collaboration de creativos, especialistas en marketing y usuarios de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos  | Caso de uso | Superficies afectadas |
|---|---|---|
| Simplifique la experiencia para creativos en equipos de escritorio | Optimice el acceso al recurso desde un DAM ([!DNL Experience Manager Assets]) para los profesionales creativos o, más en general, para los usuarios de escritorio que trabajan en aplicaciones nativas de creación de recursos. Necesitan una forma fácil y directa de descubrir, usar (abrir), editar y guardar cambios en [!DNL Experience Manager] y cargar nuevos archivos. | Escritorio Win o Mac; [!DNL Creative Cloud] aplicaciones |
| Proporcionar recursos de alta calidad listos para usar de [!DNL Adobe Stock] | Los especialistas en marketing ayudan a acelerar el proceso de creación de contenido al ayudar con la obtención y el descubrimiento de recursos. Los profesionales creativos utilizan los recursos aprobados desde sus herramientas creativas. | [!DNL Experience Manager Assets]; mercado [!DNL Adobe Stock]; campos de metadatos |
| Distribuir y compartir recursos por organizaciones | Los departamentos internos/sucursales locales y los socios externos, distribuidores y agencias utilizan los activos aprobados compartidos por la organización matriz. La organización desea compartir de forma segura y sin problemas los recursos creados para una reutilización más amplia. | Brand Portal, uso compartido de recursos Commons |

## Ofertas de Adobe para satisfacer las necesidades de colaboración {#adobe-offerings-to-support-the-collaboration-need}

| Propuesta de valor para las personas involucradas | oferta de Adobe | Superficies afectadas |
|---|---|---|
| Los usuarios creativos pueden descubrir recursos de [!DNL Experience Manager], abrirlos y utilizarlos, editar y cargar cambios en [!DNL Experience Manager] y cargar nuevos archivos en [!DNL Experience Manager], sin salir de las aplicaciones de [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) | .[!DNL Adobe Photoshop], [!DNL Adobe Illustrator], y [!DNL Adobe InDesign]. |
| Los usuarios empresariales simplifican la apertura y el uso de los recursos, la edición y carga de cambios en [!DNL Experience Manager] y la carga de nuevos archivos en [!DNL Experience Manager] desde el entorno de escritorio. Utilizan una integración genérica para abrir cualquier tipo de recurso en la aplicación de escritorio nativa, incluidos los que no son de Adobe. | [aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] aplicación de escritorio en Windows y Mac Desktop |
| Los especialistas en marketing y los usuarios empresariales pueden descubrir, obtener una vista previa, obtener una licencia y guardar y administrar los recursos de [!DNL Adobe Stock] desde [!DNL Experience Manager]. Los recursos con licencia y guardados proporcionan metadatos de [!DNL Adobe Stock] seleccionados para mejorar el control. | [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md) | Interfaz web de [!DNL Experience Manager] |

Este artículo se centra principalmente en los dos primeros aspectos de las necesidades de colaboración. La distribución y el abastecimiento de activos a escala se mencionan brevemente como un caso de uso. Para estas necesidades, considere Adobe Brand Portal o Asset Share Commons. Las soluciones alternativas como [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), las soluciones que se pueden crear en función de los componentes de [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](/help/assets/link-sharing.md), con [Experience Manager Assets](/help/assets/manage-assets.md) deben revisarse según los requisitos específicos.

![Conexiones Creative Cloud para Experience Manager, decida qué capacidad utilizar](assets/creative-connections-aem.png)

### Asignación de casos de uso y soluciones de Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso práctico | [!DNL Adobe Asset Link] | Aplicación de escritorio de [!DNL Experience Manager] | Observaciones / Otras soluciones |
|---|---|---|---|
| Discover: examinar carpetas DAM | Sí | [!DNL Experience Manager] acciones de escritorio e interfaz web | |
| Discover: acceso a colecciones DAM | Sí | [!DNL Experience Manager] acciones de escritorio e interfaz web | |
| Discover: buscar recursos de DAM | Sí | [!DNL Experience Manager] acciones de escritorio e interfaz web | |
| Uso: Abrir recurso | Sí | Sí | [Abrir desde la interfaz web](manage-assets.md#previewing-assets) o desde el Finder |
| Uso: colocar un recurso de DAM en un documento | Sí: incrustación | Sí: vinculación o incrustación | La aplicación de escritorio [!DNL Experience Manager] proporciona acceso a los recursos como archivos en el sistema de archivos local. Estos vínculos en las aplicaciones nativas se representan mediante rutas locales. |
| Editar: abrir para editar | Sí: acción de salida | Sí: Abrir acción (en el recurso compartido de red) | [Al desprotegerlo en AAL](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html), se guarda el recurso en la cuenta de almacenamiento de Creative Cloud del usuario (sincronizada por la aplicación de Creative Cloud) de forma predeterminada. |
| Editar: trabajo en curso fuera de DAM | Sí, el recurso está disponible en la cuenta de almacenamiento de Creative Cloud del usuario sincronizada con el equipo de escritorio. | Sí | |
| Editar: cambios de carga | Sí: [acción de protección](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html) con comentario opcional | Sí | |
| Cargar: un solo archivo | Sí: carga el documento activo actual | Sí | [Cargar mediante interfaz web](manage-assets.md#uploading-assets) |
| Cargar: varios archivos/estructuras de carpetas jerárquicas | No | Sí | [Cargar a través de la interfaz web](manage-assets.md#uploading-assets) o a través de scripts personalizados o herramientas. |
| Varios: usuario e inicio de sesión | Se reconoce el inicio de sesión único (SSO) de un usuario de Creative Cloud que haya iniciado sesión en la aplicación de escritorio de Creative Cloud | Usuario y credenciales de [!DNL Experience Manager] | Los usuarios de ambas soluciones se contabilizan en la cuota de usuarios de [!DNL Experience Manager]. |
| Varios: red y acceso | Requiere acceso desde el escritorio del usuario a la implementación de [!DNL Experience Manager] en la red | Requiere acceso desde el escritorio del usuario a la implementación de [!DNL Experience Manager] en la red | [!DNL Adobe Asset Link] no comparte el entorno de proxy de red. |
| Varios: migrar un gran número de recursos | No | No | [Guía de migración de Assets](assets-migration-guide.md) |

Para admitir casos de uso de distribución de recursos, se deben considerar otras soluciones:

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para un complemento de SaaS configurable de [!DNL Experience Manager Assets] para publicar recursos.
* Se crean soluciones personalizadas basadas en el código base [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager] [vínculo compartido](/help/assets/link-sharing.md) para compartir recursos bajo demanda mediante vínculos.
* [Interfaz web de Experience Manager Assets](/help/assets/manage-assets.md) con áreas para partes externas protegidas por la configuración de control de acceso de [!DNL Experience Manager] y con los ajustes de configuración de red/TI necesarios, lo que proporciona a estos usuarios externos acceso a [!DNL Experience Manager].

## Conceptos clave y casos de uso {#key-concepts-and-use-cases}

### Glosario de términos comunes {#glossary-of-common-terms}

* **Trabajo en curso o trabajo en curso creativo (WIP):** Fase del ciclo vital de los recursos en la que sufren varios cambios y, por lo general, no están listos para compartirse con equipos más amplios.
* **Recursos listos para el proceso creativo:** [!DNL Assets] que están listos para compartirse con un equipo más amplio, o que han sido seleccionados o aprobados por el equipo creativo para compartirlos con equipos de marketing o de LOB.
* **Aprobaciones de recursos:** Proceso de aprobación que se ejecuta para los recursos ya cargados en DAM, que generalmente incluye aprobaciones de marca, aprobaciones legales, etc.
* **Recurso final:** Recurso que ha pasado por todas las aprobaciones/etiquetado de metadatos y está listo para que lo utilice el equipo superior. Este recurso se almacena en DAM y se pone a disposición de todos los usuarios (o de todos los interesados). Se puede utilizar en canales de marketing o en equipos creativos para crear diseños.
* **Cambio o actualización menor de recursos :** Un cambio rápido y pequeño en un recurso digital. A menudo se realiza como respuesta a una solicitud de edición, revisión o aprobación de recursos (por ejemplo, cambiar la posición, el tamaño del texto, ajustar la saturación/brillo, el color, etc.).
* **Cambio o actualización de recursos principales:** Un cambio en un recurso digital que requiere un trabajo considerable y que a veces debe realizarse durante un período de tiempo más largo. Generalmente incluye varios cambios. El recurso debe guardarse varias veces mientras se actualiza. Las principales actualizaciones de recursos suelen hacer que el recurso entre en una etapa de trabajo en curso.
* **DAM**: Administración de recursos digitales. En este documento, es sinónimo de [!DNL Experience Manager Assets], a menos que se indique específicamente lo contrario.
* **Usuario creativo:** Un profesional creativo que crea recursos digitales mediante las aplicaciones y los servicios de Creative Cloud. En algunos casos, un usuario creativo puede ser miembro de un equipo creativo que puede utilizar Creative Cloud, pero no crea recursos digitales (como un director creativo o un administrador de equipo creativo).
* **Usuario de DAM:** Usuario típico de un sistema DAM. Según la organización, un usuario de DAM puede ser un usuario de marketing o no de marketing, por ejemplo, un usuario de línea de negocios (LOB), bibliotecario, vendedor, etc.

### Consideraciones al usar la integración de [!DNL Experience Manager] y [!DNL Creative Cloud] {#considerations-when-using-aem-and-creative-cloud-integration}

* Ver [prácticas recomendadas de aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Ver [integración de Adobe Stock](aem-assets-adobe-stock.md)
* Ver [vínculo de recurso de Adobe](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)

Este es un breve resumen de las prácticas recomendadas para la integración de [!DNL Experience Manager] y [!DNL Creative Cloud]. Lea el resto de este documento para comprender en detalle estos aspectos.

* **Para usuarios creativos que trabajan en Photoshop, InDesign o Illustrator:** Adobe Asset Link ofrece la mejor experiencia de usuario, incluida la administración del trabajo en curso en los recursos desprotegidos de [!DNL Experience Manager].
* **Para simplificar el acceso a los recursos desde el escritorio para cualquier aplicación o formato de archivo genérico:** use la aplicación de escritorio [!DNL Experience Manager].
* **Comprenda por qué y cuándo almacenar recursos en DAM:** Actualizaciones que se pondrán a disposición del equipo de la organización al completo.
* **Tenga en cuenta el volumen de recursos compartidos:** Si el caso de uso es la distribución de recursos, la administración y la seguridad podrían ser los aspectos más importantes. Considere utilizar herramientas creadas para hacerlo a escala, como Brand Portal.
* **Comprenda el ciclo vital de los recursos:** Conozca cómo los distintos equipos administran los recursos en su organización
* **Gestione los ahorros frecuentes de los recursos con cuidado:** Adobe Asset Link se encarga de ello con PS, AI e ID. Para otras aplicaciones, no realice tareas de trabajo en curso en carpetas asignadas o compartidas a menos que necesite todos los cambios en DAM

### Acceso a [!DNL Adobe Stock] recursos desde [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[La integración de Experience Manager y Adobe Stock](/help/assets/aem-assets-adobe-stock.md) permite a los usuarios de [!DNL Experience Manager] buscar, obtener una vista previa, obtener una licencia y guardar los recursos de [!DNL Adobe Stock] en [!DNL Experience Manager]. Los recursos con licencia y guardados [!DNL Stock] han seleccionado [!DNL Stock] metadatos, que se pueden usar para buscarlos con filtros adicionales.

Algunos puntos importantes sobre esta integración:

* Cuando los recursos de Adobe Stock se guardan en [!DNL Experience Manager], pasan a ser un [!DNL Assets] normal, con el binario guardado en el repositorio [!DNL Experience Manager]. Algunos metadatos relacionados con [!DNL Adobe Stock] se guardan para el recurso en [!DNL Experience Manager]; de lo contrario, el proceso de ingesta tendrá el mismo aspecto que para cualquier otro archivo. Por ejemplo, si las etiquetas inteligentes están activas, estas se añaden a estos recursos al guardarlas.
* El recurso guardado en [!DNL Experience Manager] es una copia, no un vínculo a [!DNL Adobe Stock].

**Trabajando con recursos guardados de [!DNL Adobe Stock] a [!DNL Experience Manager] en[!DNL Creative Cloud]**. Esta integración es independiente de [!DNL Adobe Asset Link], pero [!DNL Adobe Asset Link] reconoce estos recursos guardados de [!DNL Stock] de esa manera y muestra metadatos adicionales y un logotipo de [!DNL Adobe Stock] en estos recursos en la interfaz de usuario de la extensión [!DNL Adobe Asset Link] en [!DNL Photoshop], [!DNL Illustrator] o [!DNL InDesign]. Los archivos están disponibles para explorarlos, abrirlos, etc., porque son recursos normales cuando se guardan en [!DNL Experience Manager].
Los usuarios creativos que trabajen en aplicaciones de [!DNL Creative Cloud] con la extensión [!DNL Adobe Asset Link] presente, además de tener acceso a recursos con licencia de [!DNL Adobe Stock] en [!DNL Experience Manager], también pueden usar el panel Bibliotecas de [!DNL Creative Cloud] para buscar, obtener una vista previa y obtener una licencia de recursos de [!DNL Adobe Stock].
[!DNL Assets] de [!DNL Adobe Stock] con licencia y guardado en [!DNL Experience Manager] pasan a estar disponibles para los equipos más amplios que acceden a la implementación de [!DNL Experience Manager Assets], mientras que los creativos que otorgan licencias a recursos de [!DNL Adobe Stock] mediante el panel Bibliotecas de [!DNL Creative Cloud] los ponen a su disposición solo de forma predeterminada en su cuenta de [!DNL Creative Cloud].

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Acerca del almacenamiento de recursos en un DAM {#about-storing-assets-in-a-dam}

Para diseñar un flujo de trabajo eficiente entre los equipos creativos y de marketing/línea de negocios (LOB) y elegir las mejores capacidades de soporte, es importante comprender cuándo y por qué los recursos se almacenan en DAM.

### Por qué se almacenan los recursos en DAM {#why-assets-are-stored-in-dam}

El almacenamiento de recursos en DAM los hace fácilmente accesibles y localizables. Garantiza que numerosos usuarios de toda la organización o el ecosistema puedan utilizar los recursos, lo que incluye socios, clientes, etc.

La mayoría de las organizaciones eligen almacenar únicamente los recursos relevantes para los procesos de marketing descendente/LOB (publicación en canales como el canal web a través de [!DNL Experience Manager Sites] u otros canales ofrecidos por Adobe Experience Cloud: Marketing Cloud, Advertising Cloud y medidos por Analytics Cloud, que proporciona a usuarios/socios, etc.). Además, las organizaciones almacenan recursos que pueden estar sujetos a un proceso de revisión/aprobación en DAM. De este modo, DAM almacena principalmente recursos que tienen altas probabilidades de utilizarse y evita almacenar recursos inactivos.

El almacenamiento de recursos también está sujeto a consideraciones técnicas y de utilización de recursos. DAM proporciona servicios adicionales relacionados con los recursos almacenados, como la extracción de metadatos, el control de versiones, la generación de previsualizaciones/transcodificación, la administración de referencias y la adición de información de control de acceso. Estos servicios consumen tiempo y recursos de infraestructura adicionales.

A menudo, no es deseable almacenar todos los recursos y las actualizaciones. Por ejemplo, si las actualizaciones de recursos específicos son de mala calidad y consumen recursos excesivos, es posible que los recursos no se almacenen en DAM.

#### Cuando los recursos se almacenan en DAM {#when-assets-are-stored-in-dam}

Los equipos creativos (y las organizaciones) generalmente no están interesados en almacenar recursos en cada fase del ciclo de vida del recurso. Por ejemplo, evitan almacenar recursos en los siguientes casos:

* Assets que aún no se han finalizado o que están sujetos a experimentación.
* Assets que no superan el ciclo de revisión del equipo creativo/interno.
* En comparación con el recurso en cuestión, el equipo tiene mejores candidatos para representar su trabajo ante equipos externos.

Normalmente, los siguientes recursos de clases se almacenan en DAM:

* Assets que ha alcanzado un cierto grado de madurez y que se considera que está listo para compartirse.
* Assets que fueron preseleccionados por el equipo creativo.
* Formatos de recurso específicos que el marketing puede utilizar o solicitar, según un contrato o acuerdo específico (por ejemplo, archivos JPG convertidos de archivos RAW, TIFF/imágenes de PSD originales).

#### Cuando se almacenan actualizaciones de recursos en DAM {#when-updates-to-assets-are-stored-in-dam}

Como regla general, solo las actualizaciones de los recursos relevantes para el conjunto más amplio de usuarios de DAM deben almacenarse en DAM. Garantiza que los usuarios (funciones de marketing y similares) solo vean versiones relevantes en la cronología de recursos de DAM.

Normalmente, los cambios están relacionados con los hitos principales del ciclo vital del recurso. Por ejemplo, el recurso inicial listo para el marketing o una actualización oficial basada en la solicitud/revisión proporcionada por el equipo creativo debe almacenarse y tener versiones en DAM.

La actualización del equipo creativo para que la revise el equipo de marketing después de una solicitud de cambio en el recurso existente en DAM es un ejemplo de actualización relevante. Se debe almacenar y crear versiones en DAM para obtener más información o para volver a la versión anterior.

Los siguientes son ejemplos de actualizaciones que generalmente no son relevantes:

* Versiones tempranas de los recursos cargados antes de que estén listos para la revisión de marketing
* Realice cambios creativos frecuentes en el recurso en la fase de trabajo en curso antes de que los equipos creativos y de marketing decidan que el recurso está listo

### Acceso del usuario a DAM {#user-access-to-dam}

[!DNL Assets] admite dos tipos de usuarios según su acceso a la implementación [!DNL Assets]. Normalmente, los usuarios dentro de la red empresarial (cortafuegos) tienen acceso directo a DAM. Otros usuarios fuera de la red empresarial no tendrían acceso directo. El tipo de usuario determina qué integraciones se pueden utilizar desde el punto de vista técnico.

#### Usuarios creativos con acceso directo a DAM {#creative-users-with-direct-access-to-dam}

Normalmente, los equipos creativos internos, las agencias o los profesionales creativos incorporados a la red interna tienen acceso a la implementación de DAM, incluido el inicio de sesión de [!DNL Experience Manager]. [!DNL Experience Manager] y la infraestructura de red se pueden configurar para permitir el acceso directo a terceros externos (por lo general, organizaciones de confianza como agencias que trabajan para un cliente) para tener acceso a [!DNL Experience Manager] a través de la red, por ejemplo, mediante una lista de permitidos VPN o IP.

En estos casos, Adobe Asset Link o la aplicación de escritorio [!DNL Experience Manager] ayudan a proporcionar un acceso fácil a los recursos finales/aprobados y le permiten guardar recursos listos para la creatividad en DAM.

#### Usuarios creativos sin acceso a DAM {#creative-users-without-access-to-dam}

Las agencias externas y los autónomos sin acceso directo a la implementación de DAM pueden requerir acceso a recursos aprobados o querer agregar sus nuevos diseños a DAM.

Utilice las siguientes estrategias para proporcionar acceso a los recursos finales/aprobados:

* Utilice la aplicación de escritorio si Asset Link no funciona.
* Use [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) para distribuir recursos de forma segura a socios externos
* Use una implementación personalizada de un portal de distribución y abastecimiento basado en [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Use el control de acceso configurado en [!DNL Experience Manager] y la infraestructura de red necesaria (por ejemplo, lista de permitidos IP y VPN) para que los terceros externos tengan acceso a un área de contenido específica en DAM. Pueden usar la interfaz de usuario web [!DNL Experience Manager] para obtener recursos y cargar contenido nuevo en DAM.

#### Trabajo en curso en los recursos de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Como se explica en este documento, se recomienda realizar actualizaciones importantes en los recursos, a veces denominadas trabajo en curso, sin que todas las ediciones guardadas en el archivo local también se carguen en [!DNL Experience Manager] como cambios. Esto acelera el trabajo de un usuario de escritorio, limita el ancho de banda de la red utilizado y mantiene la cronología de los recursos limpia y centrada en actualizaciones importantes y controladas.

Adobe Asset Link ofrece una buena compatibilidad con este caso de uso:

* Cuando los usuarios de [!DNL Photoshop], [!DNL InDesign] o [!DNL Illustrator] intentan editar un archivo, ejecutan una operación de desprotección en el recurso dado
* El recurso se descarga en segundo plano, se coloca en la cuenta de Creative Cloud de los usuarios sincronizada con el disco mediante la aplicación de escritorio de Creative Cloud y el indicador de desprotección se activa en [!DNL Experience Manager] en el recurso para minimizar los conflictos de edición
* A partir de ahí, el usuario trabaja en un archivo almacenado localmente en la ubicación sincronizada y puede seguir trabajando y guardando los cambios necesarios en cualquier frecuencia requerida
* Además, como el recurso se encuentra en la cuenta de Creative Cloud, también está disponible en otros dispositivos que el usuario pueda tener (por ejemplo, se puede abrir o editar en una aplicación móvil de Creative Cloud dedicada) y se puede compartir con otros usuarios de Creative Cloud para colaborar.
* Cuando el usuario creativo haya terminado con los cambios, puede ejecutar una operación de protección en ese archivo en su aplicación de Creative Cloud, con un comentario opcional. El recurso correspondiente de [!DNL Experience Manager] tiene una versión y se ha actualizado a con el nuevo binario. [!DNL Experience Manager] usuarios como especialistas en marketing o usuarios de LOB tienen acceso a cambios de recursos importantes o hitos a través de la interfaz de usuario de la cronología de recursos [!DNL Experience Manager].

La aplicación de escritorio [!DNL Experience Manager] proporciona un recurso compartido de red para los recursos abiertos en la aplicación nativa. De manera predeterminada, todos los cambios realizados localmente se cargan automáticamente en [!DNL Experience Manager] después de un breve tiempo. Con una configuración de este tipo, los ahorros frecuentes durante la fase de trabajo en curso se cargarían en [!DNL Experience Manager] y se versionarían, lo que crearía numerosos desafíos de tráfico de red y escalabilidad potenciales, sin mencionar las versiones innecesarias en [!DNL Experience Manager].

El método recomendado aquí es usar una opción en la aplicación de escritorio [!DNL Experience Manager] para desactivar las actualizaciones automatizadas y cargar manualmente los cambios en los recursos a [!DNL Experience Manager] mediante la acción de cargar cambios en la interfaz de usuario de estado de los recursos de la aplicación.

#### Carga masiva en DAM {#bulk-upload-to-dam}

Es posible que deba cargar simultáneamente un número mayor de archivos en DAM en algunos casos, por ejemplo:

* Carga de resultados de sesiones fotográficas o proyectos más grandes
* Carga de recursos proporcionados por agencias creativas
* Cargar los recursos seleccionados de un conjunto mayor si la selección se realiza fuera de DAM

La descripción hace referencia a la carga de archivos de forma operativa (por ejemplo, cada semana o con cada sesión fotográfica), como parte normal del flujo de trabajo del usuario de escritorio. Las migraciones de recursos grandes no están cubiertas aquí.

Puede utilizar las siguientes capacidades de carga:

* Para cargar carpetas grandes y jerárquicas de forma masiva, usa la aplicación de escritorio [!DNL Experience Manager] que proporciona la funcionalidad [cargar carpetas](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#upload-and-add-new-assets-to-aem). También puede cargar estructuras de carpetas jerárquicas. [!DNL Assets] se han subido al segundo plano y, por lo tanto, no está enlazado a una sesión de explorador web
* Para cargar algunos archivos desde una sola carpeta, arrástrelos directamente a la interfaz web o utilice la opción Crear en la interfaz web [!DNL Assets].
* Según sus necesidades comerciales, también puede utilizar un cargador personalizado.

#### Administre recursos digitales directamente desde el escritorio {#managing-digital-assets-directly-from-desktop}

Si usa Recursos compartidos de archivos de red para administrar recursos digitales, el simple uso del recurso compartido de red asignado por la aplicación de escritorio [!DNL Experience Manager] podría considerarse un sustituto conveniente. Al realizar la transición desde recursos compartidos de archivos de red, la interfaz web de [!DNL Experience Manager] proporciona un completo conjunto de funcionalidades de administración de recursos digitales que van mucho más allá de lo que es posible en un recurso compartido de red (búsqueda, colecciones, metadatos, colaboración, vistas previas, etc.), y la aplicación de escritorio de [!DNL Experience Manager] proporciona un vínculo útil para conectar el repositorio DAM del lado del servidor con el trabajo en el escritorio.

Evite usar la aplicación de escritorio [!DNL Experience Manager] para administrar recursos directamente en el recurso compartido de red de [!DNL Assets]. Por ejemplo, evite usar la aplicación de escritorio [!DNL Experience Manager] para mover o copiar varios archivos. En su lugar, use la interfaz [!DNL Assets] para arrastrar carpetas desde Finder/Explorer al recurso compartido de red o use la característica de carga de carpetas [!DNL Assets].

#### Migración de recursos {#asset-migration}

Para planear y ejecutar migraciones de recursos de un sistema existente a otro o la migración de un gran volumen de recursos almacenados en servidores, consulte la [Guía de migración](/help/assets/assets-migration-guide.md). La aplicación de escritorio [!DNL Experience Manager] y las integraciones de [!DNL Experience Manager] a [!DNL Creative Cloud] no admiten estas migraciones. Debido a los grandes volúmenes de recursos que se van a ingerir y a los requisitos adicionales relacionados con la asignación, transformación e ingesta de metadatos, las migraciones deben gestionarse con diferentes herramientas y enfoques.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)
>* [Prácticas recomendadas de la aplicación de escritorio de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integración de Experience Manager y Adobe Stock](aem-assets-adobe-stock.md)
