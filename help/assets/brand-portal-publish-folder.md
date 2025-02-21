---
title: Publicar carpetas en Brand Portal
description: Obtenga información sobre cómo publicar y cancelar la publicación de carpetas en Brand Portal.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 34%

---

# Publicar carpetas en Brand Portal{#publish-folders-to-brand-portal}

Como administrador de Assets de Adobe Experience Manager (AEM), puede publicar recursos y carpetas en la instancia de AEM Assets Brand Portal (o programar el flujo de trabajo de publicación para una fecha u hora posterior) para su organización. Sin embargo, primero debe integrar AEM Assets con Brand Portal. Para obtener más información, consulte [Configurar AEM Assets con Brand Portal](/help/assets/configure-aem-assets-with-brand-portal.md).

Después de publicar un recurso o una carpeta, estará disponible para los usuarios en Brand Portal.

Si realiza las modificaciones posteriores al recurso o la carpeta originales en AEM Assets, los cambios no se reflejarán en Brand Portal hasta que vuelva a publicar el recurso o la carpeta. Esta función garantiza que los cambios en curso no estén disponibles en Brand Portal. Solo los cambios aprobados publicados por un administrador están disponibles en Brand Portal.

## Publicar carpetas en Brand Portal {#publish-folders-to-brand-portal-1}

1. En la interfaz de AEM Assets, pase el ratón sobre la carpeta que quiera y seleccione la opción **Publicar** en las acciones rápidas.

   También puede seleccionar la carpeta que desee y seguir los pasos adicionales.

   ![publish2bp](assets/publish2bp.png)

1. **Publicar carpetas ahora**

   Para publicar las carpetas seleccionadas en Brand Portal, haga una de las acciones siguientes:

   * En la barra de herramientas, seleccione **Publicación rápida**. A continuación, en el menú, seleccione **Publicar en Brand Portal**.

   * En la barra de herramientas, seleccione **Administrar publicación**.

   1. En **Acción**, seleccione **Publicar en Brand Portal**, en **Programación**, seleccione **Ahora** y haga clic en **Siguiente.**
   1. Confirme su selección en **Ámbito** y haga clic en **Publicar en Brand Portal**.

   Aparece un mensaje que indica que la carpeta se ha puesto en cola para su publicación en Brand Portal. Inicie sesión en la interfaz de Brand Portal para ver la carpeta publicada.

   **Publicar carpetas más tarde**

   Para programar el flujo de trabajo de publicación en Brand Portal de las carpetas de recursos para una fecha u hora posterior:

   1. Una vez que haya seleccionado los recursos o las carpetas que desea publicar, seleccione **Administrar publicación** en la barra de herramientas de la parte superior.
   1. En **Acción**, seleccione **Publicar en Brand Portal**, en **Programación**, seleccione **Más tarde**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Seleccione una **Fecha de activación** y especifique la hora. Haga clic en **Siguiente**. 
   1. Confirme la selección en **Ámbito**. Haga clic en **Siguiente**. 
   1. Especifique un título de flujo de trabajo en **Flujos de trabajo**. Haga clic en **Publicar más tarde**.

      ![manageschedulepub](assets/manageschedulepub.png)

## Cancelar la publicación de carpetas desde Brand Portal {#unpublish-folders-from-brand-portal}

Puede eliminar cualquier carpeta de recursos publicada en Brand Portal cancelando la publicación de la instancia de autor de AEM. Después de cancelar la publicación de la carpeta original, su copia ya no estará disponible para los usuarios de Brand Portal.

Tiene la opción de cancelar la publicación de carpetas desde Brand Portal rápidamente o programarlas para una fecha y hora posteriores. Para cancelar la publicación de carpetas de recursos desde Brand Portal:

1. En la interfaz de AEM Assets de la instancia de autor de AEM, seleccione la carpeta cuya publicación desea cancelar.

   ![publish2bp-1](assets/publish2bp.png)

1. En la barra de herramientas, haga clic en **Administrar publicación**.

1. **Cancelar publicación de Brand Portal ahora**

   Para cancelar la publicación de la carpeta deseada de Brand Portal rápidamente:

   1. En la barra de herramientas, seleccione **Administrar publicación**.
   1. En **Acción**, seleccione **Cancelar publicación en Brand Portal**, en **Programación**, seleccione **Ahora** y haga clic en **Siguiente.**
   1. Confirme su selección en **Ámbito** y haga clic en **Cancelar publicación desde Brand Portal**.

   ![confirmar-cancelar publicación](assets/confirm-unpublish.png)

   **Cancelar publicación de Brand Portal más tarde**

   Para programar la publicación de una carpeta desde Brand Portal a una fecha y hora posteriores:

   1. En la barra de herramientas, seleccione **Administrar publicación**.
   1. En **Acción**, seleccione **Cancelar la publicación de Brand Portal** y en **Programación**, seleccione **Más tarde**.
   1. Seleccione una **Fecha de activación** y especifique la hora. Haga clic en **Siguiente**. 
   1. Confirme la selección en **Ámbito** y haga clic en **Siguiente**.
   1. Especifique un **título de flujo de trabajo** en **Flujos de trabajo**. Haga clic en **Cancelar publicación más tarde.**

      ![flujos de trabajo sin publicar](assets/unpublishworkflows.png)

>[!NOTE]
>
>El procedimiento para publicar/cancelar la publicación de un recurso desde/hacia Brand Portal es similar al procedimiento correspondiente para una carpeta.
