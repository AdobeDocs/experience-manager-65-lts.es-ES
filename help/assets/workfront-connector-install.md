---
title: Instalar [!DNL Workfront for Experience Manager enhanced connector]
description: Instalar [!DNL Workfront for Experience Manager enhanced connector]
role: Admin
feature: Workfront Integrations and Apps
hide: true
solution: Experience Manager, Workfront
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 3%

---

# Instalar [!DNL Workfront for Experience Manager enhanced connector] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-connector-install.html?lang=en) |
| AEM 6.5 | Este artículo |

Un usuario con acceso de administrador en [!DNL Adobe Experience Manager] instala el conector mejorado. Antes de instalar, revise la compatibilidad con la plataforma y otros [requisitos previos para el conector](https://one.workfront.com/s/csh?context=2467&amp;pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe requiere la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>* Adobe puede publicar actualizaciones para [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hagan redundante este conector; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, vaya al grupo `digital.hoodoo` disponible en el panel izquierdo de [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html?lang=en).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información sobre el examen, consulte [Guía para exámenes](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

Para instalar el conector, siga estos pasos:

1. Descargue el conector desde [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. [Configurar el firewall](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FAdministration_and_Setup%2FGet_started-WF_administration%2Fconfigure-your-firewall.html).
1. En Dispatcher, permita los encabezados HTTP llamados `authorization`, `username` y `apikey`. Permitir solicitudes de `GET`, `POST` y `PUT` a `/bin/workfront-tools`.
1. Asegúrese de que las siguientes rutas no existan en el repositorio [!DNL Experience Manager]:

   * `/apps/dam/gui/coral/components/admin/schemaforms/formbuilder`
   * `/apps/dam/gui/coral/components/admin/folderschemaforms/formbuilder`
   * `/apps/dam/gui/content/foldermetadataschemaeditor`
   * `/apps/dam/cfm/models/editor/components/datatypeproperties`
   * `/apps/settings/dam/cfm/models/formbuilderconfig`

1. Instale el paquete mediante [!UICONTROL Administrador de paquetes]. Para saber cómo instalar paquetes, consulte [Documentación del Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Cree `wf-workfront-users` en el grupo de usuarios [!DNL Experience Manager] y asigne el permiso `jcr:all` a `/content/dam`.
1. Agregue una propiedad personalizada a la definición de índice predeterminada de **`ntFolderDamLucene(/oak:index/ntFolderDamLucene)`**. Siga estos pasos:
   * Agregar una propiedad de **`nt:unstructured`** denominada **`wfReferenceNumber`** a:

     `/oak:index/ntFolderDamLucene/indexRules/nt:folder/properties/wfReferenceNumber`.
   * Reindexe `index /oak:index/ntFolderDamLucene` cambiando el indicador de reindexación a `true`.

Se crea automáticamente un usuario del sistema `workfront-tools` y los permisos necesarios se administran automáticamente. Todos los usuarios de [!DNL Workfront] que utilizan el conector se agregan automáticamente como parte de este grupo.

## Configurar la conexión entre [!DNL Experience Manager] y [!DNL Workfront] {#configure-connection}

Para crear una conexión con Workfront, siga estos pasos:

1. En [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de herramientas de Workfront]**.

1. Seleccione `workfront-tools` en el panel izquierdo y seleccione la opción **[!UICONTROL Crear]** en el área superior derecha de la página.

1. En el cuadro de diálogo **[!UICONTROL Conexión de Workfront]**, proporcione los detalles necesarios de su implementación de [!DNL Workfront] y seleccione la opción **[!UICONTROL Conectarse a Workfront]**. Una vez que se haya conectado correctamente, la integración personalizada del documento [!DNL Workfront] se creará automáticamente en el entorno [!DNL Workfront].

   ![Conectar [!DNL Experience Manager] y [!DNL Workfront]](/help/assets/assets/wf-connection-config.png)

1. Para comprobar la conexión, obtenga acceso a ella en [!DNL Workfront] y compruebe que la clave de API sea la misma y que la conexión esté **[!UICONTROL habilitada]**. Para ello, seleccione **[!UICONTROL Configuración]** > **[!UICONTROL Documentos]** > **[!UICONTROL Integraciones personalizadas]** en [!DNL Workfront].

## Actualización [!DNL Workfront for Experience Manager enhanced connector] {#update-enhanced-connector-for-workfront}

Experience Manager Assets le permite actualizar [!DNL Workfront for Experience Manager enhanced connector] de una versión anterior a la versión más reciente.

Para actualizar [!DNL Workfront for Experience Manager enhanced connector] a la última versión:

1. Descargue la última versión del conector mejorado de [[!DNL Software Distribution] link](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/workfront-tools.ui.apps.zip).
1. Instale el paquete mediante [!UICONTROL Administrador de paquetes]. Para saber cómo instalar paquetes, consulte [Documentación del Administrador de paquetes](/help/sites-administering/package-manager.md).
