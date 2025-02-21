---
title: Selector de recursos
description: Aprenda a utilizar el selector de recursos para buscar, filtrar, examinar y recuperar metadatos de recursos en Adobe Experience Manager Assets. También aprenderá a personalizar la interfaz del selector de recursos.
contentOwner: Adobe
feature: Asset Management,Metadata,Search
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# Selector de recursos {#asset-selector}

>[!NOTE]
>
>El [selector de recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=en) se llamaba [selector de recursos](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) en versiones anteriores de [!DNL Experience Manager].

El selector de recursos le permite examinar, buscar y filtrar recursos en [!DNL Adobe Experience Manager] Assets. También puede recuperar los metadatos de los recursos seleccionados mediante el selector de recursos. Para personalizar la interfaz del selector de recursos, puede iniciarla con parámetros de solicitud compatibles. Estos parámetros establecen el contexto del selector de recursos para un escenario en particular.

Actualmente, puede pasar los parámetros de solicitud `assettype` (*Imagen/Vídeo/Texto*) y la selección `mode` (*Único/Múltiple*) como información contextual para el selector de recursos, que permanece intacto durante toda la selección.

El selector de recursos usa el mensaje HTML5 **Window.postMessage** para enviar datos del recurso seleccionado al destinatario.

El selector de recursos se basa en el vocabulario del selector de base de Granite. De forma predeterminada, el selector de recursos funciona en el modo Examinar. Sin embargo, puede aplicar filtros utilizando la experiencia Omnisearch para restringir la búsqueda de recursos concretos.

Puede integrar cualquier página web (independientemente de si forma parte del contenedor CQ) con el selector de recursos (`https://[AEM_server]:[port]/aem/assetpicker.html`).

## Parámetros contextuales {#contextual-parameters}

Puede pasar los siguientes parámetros de solicitud en una URL para iniciar el selector de recursos en un contexto concreto:

| Nombre | Valores | Ejemplos | Función |
|---|---|---|---|
| sufijo de recurso (B) | Ruta de la carpeta como sufijo de recurso en la dirección URL:`http://localhost:4502/aem/`<br>`assetpicker.html/<folder_path>` | Para iniciar el selector de recursos con una carpeta particular seleccionada, por ejemplo, con la carpeta `/content/dam/we-retail/en/activities` seleccionada, la dirección URL debe tener el formato: `http://localhost:4502/aem/assetpicker.html`<br>`/content/dam/we-retail/en/activities?assettype=images` | Si necesita que se seleccione una carpeta concreta al iniciar el selector de recursos, pásela como sufijo de recurso. |
| modo | individual, múltiple | `http://localhost:4502/aem/assetpicker.html`<br>`?mode=multiple` <br> `http://localhost:4502/aem/assetpicker.html`<br>`?mode=single` | En el modo múltiple, puede seleccionar varios recursos simultáneamente mediante el selector de recursos. |
| cuadro de diálogo | true, false | `http://localhost:4502/aem/assetpicker.html`<br>`?dialog=true` | Utilice estos parámetros para abrir el selector de recursos como cuadro de diálogo de Granite. Esta opción solo es aplicable cuando se inicia el selector de recursos a través del campo Granite Path y se configura como URL de pickerSrc. |
| raíz | `<folder_path>` | `http://localhost:4502/aem/`<br>`assetpicker.html?assettype=images`<br>`&root=/content/dam/we-retail/en/activities` | Utilice esta opción para especificar la carpeta raíz del selector de recursos. En este caso, el selector de recursos le permite seleccionar solo recursos secundarios (directos/indirectos) en la carpeta raíz. |
| viewmode | buscar |  | Para iniciar el selector de recursos en modo de búsqueda, con los parámetros assettype y mimetype. |
| tipo de recurso (S) | imágenes, documentos, multimedia, archivos | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia`</li> <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives`</li> | Utilice esta opción para filtrar los tipos de recursos en función del valor pasado. |
| tipo MIME | tipos MIME (`/jcr:content/metadata/dc:format`) de un recurso (también se admiten caracteres comodín) | <ul><li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=image/png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&?mimetype=*png`</li>  <li>`http://localhost:4502/aem/assetpicker.html?viewmode=search&mimetype=*presentation`</li>  <li>`http://localhost:4502/aem/assetpicker?viewmode=search&mimetype=*presentation&mimetype=*png`</li></ul> | Utilícelo para filtrar recursos en función de los tipos MIME |

## Uso del selector de recursos {#using-the-asset-selector}

1. Para acceder a la interfaz del selector de recursos, vaya a `https://[AEM_server]:[port]/aem/assetpicker`.
1. Vaya a la carpeta deseada y seleccione uno o varios recursos.

   ![chlimage_1-441](assets/chlimage_1-441.png)

   También puede buscar el recurso deseado en el cuadro OmniSearch y, a continuación, seleccionarlo.

   ![chlimage_1-442](assets/chlimage_1-442.png)

   Si busca recursos mediante el cuadro OmniSearch, puede seleccionar varios filtros en el panel **[!UICONTROL Filtros]** para restringir la búsqueda.

   ![chlimage_1-443](assets/chlimage_1-443.png)

1. Haga clic en **[!UICONTROL Seleccionar]** en la barra de herramientas.

>[!MORELIKETHIS]
>
>* [Selector de recursos de Micro-Frontend en AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/asset-selector.html?lang=en)
