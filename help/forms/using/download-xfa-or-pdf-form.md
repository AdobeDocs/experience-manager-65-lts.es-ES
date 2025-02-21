---
title: Descargar una plantilla de formulario XFA o un PDF
description: Puede exportar formularios del repositorio al sistema local y migrar los formularios descargados al nuevo repositorio.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%

---

# Descargar una plantilla de formulario XFA o un PDF {#download-an-xfa-or-a-pdf-form-template}

La operación de descarga, como su nombre indica, permite exportar formularios desde el repositorio al sistema local. Junto con la operación de carga, esta operación le ayuda a migrar los formularios de un repositorio a otro.

En AEM Forms, la operación de descarga es compatible con los siguientes tipos de recursos:

* Plantillas de formulario (formularios XFA)
* Formularios PDF
* Documentos (archivos PDF aplanados)

AEM Forms admite la descarga de estos tipos de formulario de forma individual o en una carpeta que contenga uno o varios formularios admitidos.

Además de estos recursos, puede descargar el tipo de recurso `Resource` si está presente en una carpeta. Esta funcionalidad se proporciona para permitirle descargar el recurso al que hace referencia un formulario XFA junto con el formulario.

## Descargar uno o varios formularios {#download-one-or-more-forms}

1. Inicie sesión en la interfaz de usuario de AEM Forms en `https://<server>:<port>/aem/forms.html`.

1. Navegue hasta la ubicación del recurso que desee descargar.

1. Seleccione el recurso. Haga clic en el icono **[!UICONTROL Descargar]** ![aem6forms_download](assets/aem6forms_download.png) de la barra de herramientas.

   >[!NOTE]
   >
   >Solo puede seleccionar un formulario para descargarlo. Si desea descargar varios formularios, deberá descargarlos como una carpeta.

1. En el cuadro de diálogo que aparece, haga clic en **[!UICONTROL Descargar]**.

   AEM Forms generará un archivo ZIP que contendrá el archivo o la carpeta seleccionada.

   Si descarga una carpeta, los recursos admitidos dentro de la misma se descargarán en su jerarquía existente.

   El archivo ZIP se guardará en la carpeta `Downloads` en su sistema.

## Consideraciones relacionadas con la operación de carga {#related-considerations-for-the-upload-operation}

* Puede cargar el archivo ZIP en cualquier otra ubicación del mismo u otro repositorio
* La jerarquía de los recursos de una carpeta se conservará durante la operación de carga
* Cualquier cambio de metadatos realizado en los recursos descargados antes de la descarga se reflejará en la carga
