---
title: Volver a conectar con Microsoft Translator
description: Obtenga información sobre cómo conectar AEM a Microsoft Translator de forma predeterminada para automatizar el flujo de trabajo de traducción.
feature: Language Copy
role: Admin
solution: Experience Manager, Experience Manager Sites
exl-id: e4beda86-2d74-44b9-a5f4-e3671ba9a2da
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: d9d38edd-df1b-480c-8f5e-72b62576f390
    internal-label: Site and page features
subfeature_v2:
  - id: e15a4109-ae5d-497d-b301-31149e35aed4
    internal-label: Language Copy Wizard
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 64%
---
# Volver a conectar con Microsoft Translator {#connecting-to-microsoft-translator}

AEM proporciona un conector integrado para [Microsoft Translator](https://www.microsoft.com/es-es/translator/business/) para traducir contenido o recursos de la página. Después de obtener una licencia de Microsoft para utilizar Microsoft Translator, configure el conector siguiendo las instrucciones de esta página.

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | El nombre para mostrar del servicio de traducción |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo, `Translations by Microsoft` |
| ID del espacio de trabajo | (Opcional) El ID del motor personalizado de Microsoft Translator que debe utilizar |
| Clave de suscripción | La clave de suscripción de Microsoft para Microsoft Translator |

El siguiente procedimiento crea una configuración de Microsoft Translator.

1. En el panel de navegación [haga clic](/help/sites-authoring/basic-handling.md#first-steps) en **Herramientas** > **Cloud Services** > **Cloud Services de traducción**.
1. Vaya a donde desea crear la configuración. Normalmente, se encuentra en la raíz del sitio o puede ser una configuración global predeterminada.
1. Haga clic en el botón **Crear**.
1. Defina la configuración.
   1. Seleccione **Microsoft Translator** en la lista desplegable.
   1. Escriba un título para la configuración. El título identifica la configuración en la consola Cloud Services y en las listas desplegables de propiedades de página.
   1. De forma opcional, escriba un nombre para usar para el nodo del repositorio que almacena la configuración.

   ![Creación de configuración de traducción](assets/create-translation-config.png)

1. Haga clic en **Crear**.
1. En la ventana **Editar configuración**, proporcione los valores para el servicio de traducción descrito en la tabla anterior.

   ![Edición de la configuración de traducción](assets/msft-config-ui.png)

1. Haga clic en **Conectar** para verificar la conexión.
1. Haga clic en **Guardar y cerrar**.

## Publicación de las configuraciones del servicio de traducción {#publishing-the-translator-service-configurations}

Como último paso, publique las configuraciones de Microsoft Translator para que admitan el contenido traducido publicado, mediante la acción [publicar un árbol](/help/sites-authoring/publishing-pages.md#publishing-and-unpublishing-a-tree).
