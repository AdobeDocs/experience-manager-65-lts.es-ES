---
title: Prácticas recomendadas de MSM
description: Descubra las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha el Administrador de varios sitios AEM.
topic-tags: site-features, best-practices
feature: Multi Site Manager
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 34%

---

# Prácticas recomendadas de MSM{#msm-best-practices}

## General {#general}

MSM es un marco de trabajo configurable para automatizar la implementación de contenido. Las implementaciones suelen incluir partes importantes de un sitio web y abarcan organizaciones y áreas geográficas. Por lo tanto, es muy recomendable planificar las implementaciones de MSM con el cuidado con que planifica el sitio web:

* Planifique con cuidado la **estructura y los flujos de contenido** antes de iniciar la implementación.
* **Mantenga al mínimo la cantidad de Live Copies.** El procesamiento de Live Copies es una tarea que requiere muchos recursos. Cuantas más Live Copies haya en el sistema, más rendimiento se verá afectado: desde el procesamiento de índices internos de Live Copy, pasando por operaciones de Live Copy como despliegues, hasta operaciones de interfaz de usuario como mostrar relaciones de Live Copy en el carril Referencias de administración de sitios. La práctica recomendada es crear Live Copies de sitios o ramas de un sitio, donde las relaciones de Live Copy se heredan en las páginas del sitio o rama. Evite crear Live Copies individuales para páginas de un sitio o rama cuando toda la estructura se pueda convertir en una Live Copy.
* **Personalice tanto como sea necesario, pero tan poco como sea posible.** Aunque MSM admite un alto grado de personalización (por ejemplo, configuraciones de despliegue), la práctica recomendada normalmente para el rendimiento, la fiabilidad y la actualización del sitio web es minimizar la personalización.
* Establezca un modelo de **gobernanza** desde el principio, y capacite a los usuarios debidamente para garantizar el éxito. Una práctica recomendada desde el punto de vista de la gobernanza es **minimizar la autoridad que tienen los productores de contenido local** para asignar o conectar contenido a otros usuarios locales y a sus respectivas Live Copies. Esto se debe a que las herencias encadenadas no gobernadas pueden aumentar significativamente la complejidad de una estructura de MSM y comprometer su rendimiento y fiabilidad.

* Una vez que exista un plan para la estructura, los flujos de contenido, la automatización y el control: **haga un prototipo y pruebe exhaustivamente su sistema** antes de iniciar la implementación activa.
* Tenga en cuenta que la **consultoría de Adobe y los integradores de sistemas líderes** tienen una amplia experiencia en la planificación e implementación de la automatización de contenido con MSM, por lo que pueden ayudarle a empezar su proyecto MSM y a lo largo de toda su implementación.

>[!NOTE]
>
>Encontrará más información sobre cómo trabajar con MSM en los artículos de la Base de conocimiento:
>
>* [Resolución de problemas de MSM y preguntas frecuentes](troubleshoot-msm.md)
>

>[!NOTE]
>
>También puede usar el [componente de referencia](/help/sites-authoring/default-components-foundation.md#reference) para reutilizar una sola página o párrafo. Sin embargo, tenga en cuenta:
>
>* MSM es más flexible y permite un control preciso sobre qué contenido se sincroniza y cuándo.
>* Ahora se recomiendan [componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) sobre los componentes de base.
>

## Fuentes de Live Copy y configuraciones de modelo {#live-copy-sources-and-blueprint-configurations}

Tenga en cuenta que se puede crear una Live Copy mediante [páginas regulares](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) o una [configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos son casos de uso válidos.

Los beneficios adicionales de utilizar una configuración de modelo son que:

* Permiten que el autor use la opción **Despliegue** en un modelo para insertar (explícitamente) modificaciones en Live Copies que hereden de este modelo.
* Permitir que el autor use **Crear sitio**; esto permite al usuario seleccionar idiomas fácilmente y configurar la estructura de la Live Copy.
* Defina una configuración de despliegue predeterminada para Live Copies que tengan una relación con el modelo.

En caso de que no se haga referencia a una configuración de modelo, los despliegues solo se pueden iniciar desde las propias Live Copies, lo que básicamente extrae contenido del origen.

Al crear un sitio con Live Copy, resulta ventajoso crear configuraciones de modelo para garantizar la disponibilidad del conjunto completo de funciones MSM.

>[!NOTE]
>
>Tenga en cuenta que los CUG de la pestaña Permisos no se pueden desplegar en Live Copies desde modelos. Tenga en cuenta esto al configurar Live Copy.

## Sincronización de componentes y contenedores {#components-and-container-synchronization}

En general, la regla de despliegue en MSM con respecto a la sincronización de componentes es:

* Los componentes se despliegan sincronizando cualquier recurso contenido en el modelo.
* Los contenedores solo sincronizan el recurso actual.

Esto significa que los componentes se tratan como un acumulado y, en un despliegue, el componente en sí y todos sus elementos secundarios se sustituyen por los de los modelos. Esto significa que si se agrega un recurso a un componente de este tipo localmente, se reemplazará por el contenido del modelo al desplegarse.

Para admitir el anidado de componentes de modo que los componentes añadidos localmente se mantengan en un despliegue, el componente debe declararse como contenedor. Por ejemplo, el parsys predeterminado se declara como contenedor para que pueda admitir contenido añadido localmente.

>[!NOTE]
>
>Añada la propiedad `cq:isContainer` al componente para designarlo como contenedor.

## Crear sitio {#create-site}

Tenga en cuenta que AEM tiene dos enfoques principales para crear Live Copies:

* Al [crear una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

  Este enfoque puede considerarse más genérico y le permite crear Live Copies desde cualquier página. La estructura de contenido de una Live Copy coincide exactamente con el origen.

* Al [crear un sitio](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

  Se trata de un enfoque más especializado, principalmente para crear sitios web con una estructura multilingüe.

A continuación se indican algunas consideraciones que se deben tener en cuenta al crear un sitio:

* Para crear un sitio, necesita una [configuración de modelo](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Para permitir la selección de rutas de idioma a crear en un sitio nuevo, las raíces de idioma correspondientes deben existir en el modelo (fuente).
* Una vez que se ha creado un [nuevo sitio como Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (con **Crear**, luego **Sitio**), los dos primeros niveles de esta Live Copy son *superficiales*. Los elementos secundarios de la página no pertenecen a la relación dinámica, pero se desplegará si se encuentra una relación dinámica que coincida con el activador.

  Ayuda a evitar:

   * adición manual de idiomas en el modelo (por debajo del primer nivel)
   * añadir contenido manualmente directamente debajo de la raíz del idioma,
   * no provoca que se transfiera automáticamente este nuevo contenido a live copy durante el despliegue.

## MSM y sitios web multilingües {#msm-and-multilingual-websites}

MSM puede ayudar en la creación de sitios web multilingües de dos maneras:

* Al crear formatos de idiomas.

   * Mientras que MSM en sí **no proporciona traducción de contenido**, se puede integrar con conectores de traducción de terceros que sí lo hagan. Tenga en cuenta que:

      * MSM le permite cancelar la herencia en el nivel de página o componente. Esto ayuda a evitar sobrescribir el contenido traducido (de una Live Copy, con contenido aún no traducido de un modelo) en el siguiente despliegue.
      * Algunos conectores de traducción de terceros automatizan esta administración de las herencias de MSM.

        Consulte a su proveedor de servicios de traducción para obtener más información.

      * Un enfoque alternativo para crear y traducir maestros de idiomas es usar copias de idiomas junto con el marco de trabajo de integración de traducción listo para usar de AEM.

* Al desplegar contenido desde maestros de idiomas.

   * Por ejemplo, desde el francés, que es el idioma principal, a sitios específicos de países como Francia/Francia, Canadá/Francia, Suiza/Francia.

Para obtener más información, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) y [Prácticas recomendadas de traducción](/help/sites-administering/tc-bp.md).

## Cambios y despliegues de la estructura {#structure-changes-and-rollouts}

Las modificaciones en la estructura de contenido de un modelo o árbol de fuentes se reflejan de forma diferente en una Live Copy. Esto depende del tipo de modificación:

* **Al crear** páginas nuevas en un modelo, se crearán las páginas correspondientes en Live Copies después del despliegue con la configuración de despliegue estándar.

* **Al eliminar** páginas en un modelo, las páginas correspondientes se eliminarán de las Live Copies después del despliegue con la configuración de despliegue estándar.

* **Mover** páginas a un modelo **no** hará que las páginas correspondientes se muevan a Live Copies después del despliegue con la configuración de despliegue estándar:

   * El motivo de este comportamiento es que mover una página incluye implícitamente eliminar una página. Esto podría provocar un comportamiento inesperado al publicar, ya que al eliminar páginas en el autor se desactiva automáticamente el contenido correspondiente al publicar. Esto también puede tener un efecto colateral en elementos relacionados, como vínculos, marcadores, etc.
   * La herencia de contenido en las respectivas páginas de Live Copy se actualiza para reflejar la nueva ubicación de sus fuentes en el modelo.
   * Para mover completamente una página de un modelo a Live Copies, tenga en cuenta las siguientes prácticas recomendadas:

>[!NOTE]
>
>Esto solo funcionará con el [déclencheur de despliegue](/help/sites-administering/msm-sync.md#rollout-triggers).

* Cree una configuración de despliegue personalizada:

   * Esta nueva configuración debe incluir la acción:

     `PageMoveAction`

     No agregue otras acciones a esta configuración.

* Coloque la nueva configuración:

   * Para desplegar completamente la página, mueva mientras elimina las páginas respectivas en su antigua ubicación en Live Copy:

      * Coloque la configuración recién creada antes de la configuración de despliegue estándar.

        La configuración de despliegue estándar se encarga de eliminar las páginas en su ubicación antigua.

   * Para desplegar la página, mueva las páginas mientras mantiene las respectivas en su antigua ubicación en las Live Copies (básicamente duplicando el contenido):

      * Coloque la configuración recién creada después de la configuración de despliegue estándar.

        Esto garantizará que no se elimine contenido en la Live Copy ni se desactive de la publicación.

## Personalización de despliegues {#customizing-rollouts}

Las configuraciones de despliegue de MSM son altamente personalizables. La automatización de los despliegues puede tener consecuencias de gran alcance. Como práctica recomendada, debe planificar *very* con cuidado antes, por ejemplo:

* automatizando despliegues; por ejemplo, con [déclencheur onModify](#onmodify),
* personalizando [tipos de nodo/propiedades](#node-types-properties),
* inicio de flujos de trabajo subsiguientes,
* y/o activando contenido como parte de los despliegues.

### onModify {#onmodify}

Al usar el [activador de despliegue](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify` debe tener en cuenta lo siguiente:

* La automatización de despliegues con `onModify` déclencheur puede tener un impacto negativo en el rendimiento de la creación, ya que almacenan en déclencheur los despliegues después de *cada* modificación de página.

* El resultado del despliegue puede diferir del esperado, ya que:

   * No se puede especificar el orden de los eventos de modificación resultantes.
   * La arquitectura basada en eventos no puede garantizar la secuencia de eventos transferidos al administrador de despliegue.

* El uso de una configuración de despliegue de este tipo podría provocar conflictos de confirmación si se producen actualizaciones simultáneas del mismo recurso.

Por lo tanto, se recomienda que *solo* use `onModify` déclencheur si los beneficios del inicio del despliegue automático superan cualquier problema de rendimiento potencial.

### Tipos de nodo/Propiedades {#node-types-properties}

Recuerde lo siguiente:

* Además de personalizar las acciones de despliegue, MSM también le permite personalizar las propiedades de los nodos que se están desplegando. La configuración OSGi de [MSM le permite excluir tipos de nodo](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de copiarse del origen a Live Copy.

## Información adicional {#further-information}

Esta y las siguientes páginas tratan sobre los problemas relacionados:

* [Creación y sincronización de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuración de la sincronización de Live Copy](/help/sites-administering/msm-sync.md)
* [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md)
