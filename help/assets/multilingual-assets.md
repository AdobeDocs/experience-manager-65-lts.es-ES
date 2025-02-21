---
title: Recurso multilingüe
description: Obtenga información sobre cómo automatizar flujos de trabajo para traducir recursos, incluidos binarios, metadatos y etiquetas, a varios idiomas.
contentOwner: AG
feature: Asset Management
role: Admin
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 7%

---

# Recursos multilingües {#multilingual-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Experience Manager Assets] le permite automatizar los flujos de trabajo de traducción de los recursos (incluidos binarios, metadatos y etiquetas) para generar recursos en otros idiomas y utilizarlos en proyectos multilingües.

Para automatizar los flujos de trabajo de traducción, se integran los proveedores de servicios de traducción con [!DNL Experience Manager] y se crean proyectos para traducir recursos a varios idiomas. [!DNL Experience Manager] admite flujos de trabajo de traducción automática y humana.

Traducción humana: los recursos traducidos se devuelven y se importan en [!DNL Experience Manager]. Cuando el proveedor de traducción está integrado con [!DNL Experience Manager], los recursos se envían automáticamente entre [!DNL Experience Manager] y el proveedor de traducción.

Traducción automática: el servicio de traducción automática traduce inmediatamente los metadatos y las etiquetas de los recursos.

La traducción de recursos incluye lo siguiente:

1. [Conexión de Experience Manager con el proveedor de servicios de traducción](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Crear configuraciones del marco de trabajo de integración de traducciones](/help/sites-administering/tc-tic.md)
1. [Preparación de recursos para su traducción](preparing-assets-for-translation.md)
1. [Aplicación de servicios de nube de traducción a carpetas](transition-cloud-services.md)
1. [Creación de proyectos de traducción](translation-projects.md)

Si el proveedor de servicios de traducción no proporciona un conector para integrar con [!DNL Experience Manager], use un [proceso alternativo](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Vea también [Crear proyectos de traducción para fragmentos de contenido](creating-translation-projects-for-content-fragments.md).
