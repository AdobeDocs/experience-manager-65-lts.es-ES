---
title: Crear experiencias segmentadas en AEM Forms
description: Use Target en AEM Forms para crear experiencias personalizadas para clientes segmentados.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 76%

---

# Crear experiencias segmentadas en AEM Forms {#create-targeted-experiences-in-aem-forms}

## Integrar Adobe Target con AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target integrado con AEM permite crear experiencias personalizadas para una audiencia segmentada. Con Adobe Target, puede crear pruebas A/B, medir la respuesta del usuario y generar contenido web personalizado para usuarios segmentados. Puede integrar Adobe Target con AEM Forms para dirigirse a los componentes de imagen de los formularios adaptables y las comunicaciones interactivas.

Configure Adobe Target en AEM para utilizarlo con formularios adaptables y comunicaciones interactivas, consulte [Crear una configuración de destino en AEM](/help/sites-administering/target.md) y [Agregar un marco de trabajo](/help/sites-administering/target.md).

>[!NOTE]
>
>La segmentación funciona cuando el formulario adaptable o la comunicación interactiva se procesan con un nombre de host o una dirección IP. Se producirá un error si el formulario adaptable o la comunicación interactiva se procesan mediante localhost.

## Crear una actividad de Target {#creating-a-target-activity}

1. Seleccione **Adobe Experience Manager > Personalization > Actividades**.

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. En la página Actividades, seleccione **Crear > Crear marca**.
1. Se le pide que elija una plantilla e introduzca las propiedades.

   Seleccione una plantilla, seleccione **Siguiente.** Escriba el título de su marca en la sección Propiedades y seleccione **Crear.**
La marca ahora aparecerá en la página Actividades.

1. Seleccione la marca en la página Actividades.
1. En el área principal de su marca, seleccione **Crear** > **Crear actividad**.

   Cuando cree una actividad, especifique sus detalles, destinatario y configuración.

   La sección Detalles incluye nombre, motor de segmentación y objetivo. Al seleccionar Adobe Target como motor de segmentación, se habilita la opción de configuración de la nube de Target. Elija la configuración de nube de Target, elija Tipo de actividad, proporcione el objetivo de la actividad y seleccione **Siguiente**. La comunicación interactiva solo admite el tipo de actividad Segmentación de experiencias.

   La sección Target le permite agregar una experiencia de audiencia y ponerle un nombre. Haga clic en **Agregar experiencia** para habilitar las opciones **Seleccionar audiencia** y **Nombrar experiencia**. Seleccione **Seleccionar audiencia** para ver una lista de audiencias y su origen. Seleccione una audiencia en la lista Nombre de audiencia. Seleccione **Agregar experiencia** para asignar un nombre a la experiencia y seleccione **Siguiente**.

   La sección Objetivos y configuración le permite programar y dar prioridad a su actividad. Establezca la fecha de inicio, la fecha de finalización y la prioridad de la actividad, la métrica del objetivo, la métrica adicional y seleccione **Guardar**.

   La actividad aparece ahora en la página de marca.

   >[!NOTE]
   >
   >Puede ignorar el error &quot;Su actividad se ha guardado, pero no se ha sincronizado con Target. Motivo: La siguiente experiencia no tiene ofertas”, si aparece al guardar la actividad.

1. Para habilitar la segmentación, edite el archivo .jsp para incluir las bibliotecas de cliente que utiliza la plantilla de formularios adaptables.

   Por ejemplo, en la implementación predeterminada, haga clic en **Herramientas** > **CRXDE Lite**.

   En la barra de direcciones de CRXDE Lite, escriba /libs/fd/af/components/page/base/head.jsp para editar el archivo head.jsp.

   Esta implementación utiliza la plantilla simpleEnrollment. En esta implementación, modifique el archivo head.jsp para incluir las siguientes bibliotecas de cliente:

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. Para habilitar el marco de trabajo de segmentación para formularios adaptables, navegue hasta el formulario o a la comunicación interactiva y ábralo en modo de edición.

   Para abrir un formulario o una comunicación interactiva en modo de edición, selecciona **Seleccionar** y, a continuación, selecciona **Abrir**.

   Alternativamente, aparecerán cuatro botones al mover el puntero sobre icono del formulario o de la comunicación interactiva sin seleccionarlo. Puede seleccionar el botón **Editar** que aparece para abrir el formulario en modo de edición.

1. En la barra de herramientas de la página, seleccione **Información de la página** ![theme-options](assets/theme-options.png) > **Abrir propiedades**.
1. En la pestaña General, elija una configuración para el campo **Adobe Target**. Seleccione **Guardar y cerrar**.

## Aplicar la actividad creada a una imagen de formulario adaptable o de comunicación interactiva {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. Abra el formulario adaptable y la comunicación interactiva para editarlos. Si abre una comunicación interactiva, abra el canal Web.

1. En el modo de creación de la comunicación interactiva o del formulario adaptable, agregue una imagen para segmentar.

   >[!NOTE]
   >
   >AEM Forms solo admite segmentar componentes de imagen. Asegúrese de que el panel que aloja el componente de imagen no contenga ningún otro componente y que el número de columnas esté establecido en 1.

1. Cambie de **Editar** a **Segmentar** en el menú contextual. La opción para cambiar de modo está cerca de la esquina superior derecha.
1. Seleccione una **MARCA**, seleccione **ACTIVIDAD** y seleccione **Iniciar segmentación**. El menú **Audiencias** aparecerá en la parte derecha del editor.

   ![targeting-menu](assets/targeting-menu.png)

1. Seleccione una audiencia del menú **Audiencias** y seleccione la imagen de destino. Aparecerá un menú. En el menú, seleccione **Destino**. Seleccione la imagen y seleccione **Configurar**. En la ventana de propiedades, seleccione la imagen que desea mostrar para la audiencia seleccionada. Repita el paso para todas las audiencias. La segmentación de experiencias está habilitada para imágenes en la comunicación interactiva o en el formulario adaptable.

## Compruebe si la actividad creada se sincroniza con el servidor de Target {#check-if-the-created-activity-syncs-with-the-target-server}

Una actividad utilizada para segmentar se sincroniza con el servidor de Target. Para comprobar si la actividad está sincronizada con el servidor de Target, compruebe el estado de la actividad en la página de la marca.

Asegúrese de que el estado de la actividad sea Sincronizado.

## Validar comportamiento de Target {#validate-target-behavior}

Para validar el comportamiento de Target, haga lo siguiente:

* Use segmentar con `wcmmode preview` en el modo de creación
* Usar segmentar con `wcmmode preview` y `wcmmode disabled` en el modo de publicación

## Segmentar el monitor para el componente de imagen {#monitor-targeting-for-the-image-component}

Para supervisar la segmentación de los componentes de imagen en el formulario, publique sus imágenes, actividades y formularios adaptables.

## Problemas abiertos {#open-issues}

Expresión de visibilidad, error al definir el enfoque de las imágenes segmentadas en los formularios adaptables.
