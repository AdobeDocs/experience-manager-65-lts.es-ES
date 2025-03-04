---
title: Cambiar el logotipo de la organización para la promoción de la marca
description: Para personalizar la marca de AEM Forms Workspace, proporcione el logotipo de su organización al personalizar el logotipo predeterminado.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 91%

---

# Cambiar el logotipo de la organización para la promoción de la marca {#changing-the-organization-logo-for-branding}

El logotipo de la organización se muestra en la esquina superior izquierda de AEM Forms Workspace. Para actualizar el logotipo, siga los [Pasos genéricos de la personalización de AEM Forms Workspace](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization) y luego los siguientes pasos.

1. Cree un logotipo y asigne un nombre al archivo como `NewWorkspace.png`. Coloque el archivo de imagen en la carpeta /apps/ws/images mediante un cliente WebDAV.

   >[!NOTE]
   >
   >El tamaño recomendado para la imagen del logotipo es de 218 px × 20 px.

   >[!NOTE]
   >
   >Para obtener más información, consulte [Acceso a WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/webdav-access.html?lang=en).

   [Acceso a WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/webdav-access.html?lang=en)

1. Haga referencia a la nueva imagen del logotipo en la hoja de estilo en /apps/ws/css/newStyle.css al agregar el siguiente estilo.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
