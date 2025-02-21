---
title: Administrar audiencias
description: La consola Audiencias permite crear, organizar y administrar las audiencias de la cuenta de Adobe Target o administrar segmentos de ContextHub o Client Context
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 63%

---

# Administrar audiencias{#managing-audiences}

La consola Audiencias permite crear, organizar y administrar las audiencias de la cuenta de Adobe Target o administrar segmentos de ContextHub o Client Context:

* Añadir públicos: de Adobe Target o segmentos de ContextHub.
* Administrar públicos.

Una audiencia denominada *segment* en ContextHub y Client Context es una clase de visitantes definidos por criterios específicos y que, a su vez, determina quién ve una actividad de destino. Al segmentar una actividad, puede seleccionar audiencias directamente en el proceso de segmentación o crear más en la consola Audiencias.

En la consola de públicos, estos se organizan por marca.

Las audiencias están disponibles en el modo Segmentación de [contenido de destino de creación](/help/sites-authoring/content-targeting-touch.md), donde también puede crear audiencias (pero debe crear audiencias de Adobe Target en la consola Audiencias). Los públicos que crea en el modo Segmentación aparecen en la consola de públicos.

Los públicos se muestran con una etiqueta que describe el tipo de público que se define:

* CH: segmento de ContextHub
* CC: segmento de Client Context
* AT: público destinatario de Adobe

## Para crear un segmento de ContextHub en la consola de públicos {#creating-a-contexthub-segment-in-the-audiences-console}

Puede crear un segmento de ContextHub en la consola de públicos o durante el proceso de segmentación.

Para crear un segmento de ContextHub en la consola de audiencias:

1. En la consola de navegación, haga clic en **Personalization**. Haga clic en **Audiencias**.
1. Haga clic en **Crear segmento de ContextHub**.

   ![captura de pantalla_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. En cuadro de diálogo **Nuevo segmento de ContextHub**, introduzca un título, ajuste el aumento y haga clic en **Crear**. El nuevo segmento de ContextHub aparece en la lista de audiencias.

   >[!NOTE]
   >
   >Puede ordenar la lista modificada pulsando o haciendo clic en **Modificado** para clasificar en orden descendente y ver las audiencias recién creadas.

Para obtener más información sobre cómo crear segmentos con ContextHub, consulte la documentación de [Configuración de la segmentación con ContextHub](/help/sites-administering/segmentation.md).

## Creación de un público de Adobe Target mediante la consola de públicos {#creating-an-adobe-target-audience-using-the-audience-console}

Puede crear públicos de Adobe Target directamente en AEM mediante la consola de públicos.

Los públicos se definen mediante reglas que determinan quién se incluye en una actividad de público destinatario. Una definición de público puede incluir varias reglas, y cada una puede incluir varios parámetros.

Al utilizar más de una regla, estas reglas se combinan según el operador boolean AND, lo que significa que cualquier posible miembro de la audiencia debe cumplir todas las condiciones que se detallaron para ser incluido en la actividad. Por ejemplo, si define una regla de sistema operativo AND una regla de explorador, solo se incluyen en la actividad los visitantes que usan el sistema operativo definido y el explorador definido.

>[!NOTE]
>
>Si no ve **Crear audiencia de Target **en el menú **Crear**, no tiene los permisos necesarios para crear una audiencia. Necesita permisos de escritura en **/etc/segmentation** para poder crear audiencias. Los autores de contenido del grupo tienen permisos de escritura de forma predeterminada.

Para crear una audiencia de Adobe Target:

1. En la consola de navegación, haga clic en **Personalization**. Haga clic en **Audiencias**.

   ![captura de pantalla_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. En la consola Audiencias, haga clic en **Crear** y, a continuación** Crear audiencia de destino**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. En el cuadro de diálogo **Configuración de Adobe Target**, seleccione la configuración de destino y haga clic en **Aceptar**.
1. En el área Rule#1, haga clic en el tipo de atributo e introduzca la información de atributo en los campos disponibles. Cuando termine, seleccione la marca de verificación a la derecha del atributo para guardarlo. Consulte [Atributos y sus opciones](#attributes-and-their-options) para obtener información sobre todos los atributos.
1. Haga clic en **Agregar regla** para añadir otra regla. Escriba tantas reglas como sea necesario. Las reglas se combinan con el operador boolean AND, lo que significa que la audiencia debe cumplir todos los requisitos de cada regla para poder optar a una actividad.
1. Haga clic en **Siguiente**.
1. Escriba un nombre para la audiencia y haga clic en **Guardar**.
1. Haga clic en **Guardar**. El público se enumera en la lista de públicos.

### Atributos y sus opciones {#attributes-and-their-options}

Puede crear reglas de segmentación para cada uno de los atributos siguientes:

| **Atributo** | **Descripción** | **Para obtener más información** |
|---|---|---|
| **Móvil** | Dirija la segmentación a dispositivos móviles en función de parámetros como dispositivo móvil, tipo de dispositivo, proveedor de dispositivo, dimensiones de pantalla (en píxeles) y más. | Consulte [Documentación móvil](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=es) en Adobe Target. |
| **Personalizado** | Los parámetros personalizados son parámetros de mbox. Si pasa algún parámetro mbox a mboxes, o usa la función targetPageParams, ese parámetro aparece aquí para su uso en audiencias. | Consulte [Documentación de parámetros personalizados](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=es) en Adobe Target. |
| **SO** | Puede segmentar visitantes que usen un sistema operativo determinado. | Usuarios de Target que usen Linux®, Macintosh o Windows. |
| **Páginas del sitio** | Segmente a los visitantes que estén en una página específica o que tengan un parámetro de mbox específico. | Consulte [Documentación de páginas del sitio](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=es) en Adobe Target. |
| **Explorador** | Puede segmentar usuarios que usen un explorador específico u opciones específicas del explorador cuando visiten la página. | Consulte la [documentación sobre las opciones del explorador](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=es) en Adobe Target. |
| **Perfil del visitante** | Segmente a los visitantes que cumplan parámetros de perfil específicos. | Consulte [Documentación del perfil del visitante](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile.html?lang=es) en Adobe Target. |
| **Fuentes de tráfico** | Segmente a los visitantes en función del motor de búsqueda o de la página de aterrizaje que les lleve a su sitio. | Consulte [Documentación de fuentes de tráfico](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=es) en Adobe Target. |

## Modificación de un público en la consola Audiencies {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Solo puede editar los públicos de Adobe Target que se hayan creado en la misma instancia de AEM en la que está editando. Los públicos destinatarios creados en distintos entornos de AEM no se pueden editar.

Puede editar cualquier audiencia de ContextHub o Client Context desde la consola Audiencias. También puede editar audiencias de Adobe Target, pero solo las que se hayan creado en AEM:

1. En la consola de navegación, haga clic en **Personalization**. Haga clic en **Audiencias**.
1. Haga clic en el icono situado junto al segmento de ContextHub o Client Context que desee editar y, a continuación, haga clic en **Editar**.
1. Haga los cambios necesarios en el editor de segmentos. Consulte la documentación de [Client Context](/help/sites-administering/campaign-segmentation.md) o [ContextHub](/help/sites-developing/ch-configuring.md).
