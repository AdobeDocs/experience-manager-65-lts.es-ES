---
title: Oriente su Adobe Campaign
description: Puede crear experiencias segmentadas para Adobe Campaign después de configurar la segmentación.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 0%

---

# Segmentación de Adobe Campaign{#targeting-your-adobe-campaign}

Para dirigirse al boletín informativo de Adobe Campaign, primero debe configurar la segmentación, que solo está disponible en la IU clásica (para el contexto de cliente). Después, puede crear experiencias segmentadas para Adobe Campaign. Ambos se describen en esta sección.

## Configuración de la segmentación en AEM {#setting-up-segmentation-in-aem}

Para configurar la segmentación, debe utilizar la IU clásica para configurar los segmentos. Los pasos restantes se pueden realizar en la interfaz de usuario estándar.

La configuración de la segmentación incluye la creación de segmentos, una marca, una campaña y experiencias.

>[!NOTE]
>
>El ID del segmento debe asignarse al del lado de Adobe Campaign.

### Creación de segmentos {#creating-segments}

Para crear segmentos:

1. Abra la [consola de segmentación](http://localhost:4502/miscadmin#/etc/segmentation) en **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Cree una página, escriba un título (por ejemplo, **Segmentos de CA**) y seleccione la plantilla **Segmento (Adobe Campaign)**.
1. Seleccione la página creada en la vista de árbol de la izquierda.
1. Cree un segmento, por ejemplo, dirigido a usuarios hombres, creando una página en el segmento que ha creado llamada Hombre y seleccione la plantilla **Segmento (Adobe Campaign)**.
1. Abra la página de segmentos creada y arrastre y suelte un **ID de segmento** de la barra de tareas en la página.
1. Haga doble clic en el rasgo, introduzca el ID que representa, en este caso, el segmento masculino definido en Adobe Campaign (por ejemplo, **MALE**) y haga clic en **Aceptar**. El siguiente mensaje debería aparecer: *`targetData.segmentCode == "MALE"`*
1. Repita los pasos para otro segmento, por ejemplo, un segmento dirigido a mujeres.

### Creación de una marca {#creating-a-brand}

Para crear una marca:

1. En **Sites**, vaya a la carpeta **Campaigns** (por ejemplo, en We.Retail).
1. Haga clic en **Crear página** e introduzca un título para la página como, por ejemplo, Marca We.Retail y seleccione la plantilla **Marca**.

### Creación de una campaña {#creating-a-campaign}

Para crear una campaña:

1. Abra la página **Marca** que creó.
1. Haga clic en **Crear página** e introduzca un título para su página como, por ejemplo, We.Retail Campaign, seleccione la plantilla **Campaign** y haga clic en **Crear**.

### Creación de experiencias {#creating-experiences}

Para crear experiencias para segmentos:

1. Abra la página **Campaign** que creó.
1. Cree experiencias para sus segmentos haciendo clic en **Crear página** e introduciendo un título para su página como, por ejemplo, Hombre mientras crea una experiencia para el segmento Hombre y seleccione la plantilla **Experiencia**.
1. Abra la página de experiencia creada.
1. Haz clic en **Editar** y luego, debajo de Segmentos, haz clic en **Agregar elemento**.
1. Introduzca la ruta al segmento masculino, por ejemplo, **/etc/segmentation/ac-segments/male**, y haga clic en **Aceptar**. Debería aparecer el siguiente mensaje: *La experiencia está dirigida a: Hombre*
1. Repita los pasos anteriores para crear una experiencia para todos los segmentos, por ejemplo, el segmento femenino.

## Creación de una newsletter con contenido de destino {#creating-a-newsletter-with-targeted-content}

Después de crear segmentos, una marca, una campaña y una experiencia, puede crear una newsletter con contenido de destino. Después de crear la experiencia, las vincula a sus segmentos.

>[!NOTE]
>
>[Las muestras de correo electrónico solo están disponibles en Geometrixx](/help/sites-developing/we-retail.md). Descargue contenido de Geometrixx de muestra desde Package Share.

Para crear una newsletter con contenido de destino:

1. Cree una newsletter con contenido de destino: debajo de Campañas de correo electrónico en Geometrixx Outdoors, haga clic en **Crear** > **Página** y seleccione una de las plantillas de correo de Adobe Campaign.

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. En la newsletter, añada un componente Texto y Personalization.
1. Agregue texto al componente Texto y Personalization, como &quot;Este es el valor predeterminado&quot;.
1. Haga clic en la flecha junto a **Editar** y seleccione **Segmentación**.
1. Seleccione la marca en el menú desplegable Marca y seleccione la Campaña. (Esta es la marca y la campaña que creó anteriormente).
1. Haga clic en **Iniciar segmentación**. Verá sus segmentos aparecer en el área Audiencias. La experiencia predeterminada se utiliza si ninguno de los segmentos definidos coincide.

   >[!NOTE]
   >
   >De forma predeterminada, los ejemplos de correo electrónico incluidos con AEM utilizan Adobe Campaign como motor de segmentación. Para los boletines personalizados, es posible que tenga que seleccionar Adobe Campaign como motor de segmentación. Cuando establezca como objetivo, haga clic en + en la barra de herramientas, escriba un título para la nueva actividad y seleccione **Adobe Campaign** como motor de orientación.

1. Haga clic en **Predeterminado** y, a continuación, en el componente Texto y Personalization que agregó y verá la diana con una flecha. Haga clic en el icono para orientar este componente.

   ![chlimage_1-189](assets/chlimage_1-189.png)

1. Vaya a otro segmento (Masculino), haga clic en **Agregar oferta** y luego haga clic en el icono de signo más +. A continuación, edite la oferta.
1. Vaya a otro segmento (Femenino) y haga clic en **Agregar oferta** y luego en el icono de signo +. Luego edite esta oferta.
1. Haga clic en **Siguiente** para ver la asignación y, a continuación, haga clic en **Siguiente** para ver la configuración, que no se aplica a Adobe Campaign, y haga clic en **Guardar**.

   AEM genera automáticamente el código de objetivo correcto para Adobe Campaign cuando el contenido se utiliza en una entrega dentro de Adobe Campaign

1. En Adobe Campaign, cree su envío: seleccione **Envío de correo electrónico con contenido de AEM** y seleccione la cuenta local de AEM, según corresponda, y confirme los cambios.

   En la vista de HTML, las diferentes experiencias de los componentes segmentados se incluyen en el código de segmentación de Adobe Campaign.

   ![chlimage_1-190](assets/chlimage_1-190.png)

   >[!NOTE]
   >
   >Si también configuras los segmentos en Adobe Campaign, al hacer clic en **Vista previa** te mostrarán las experiencias de cada segmento.
