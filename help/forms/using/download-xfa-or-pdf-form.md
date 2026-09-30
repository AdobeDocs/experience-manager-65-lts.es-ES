---
title: Descargar una plantilla de formulario XFA o un PDF
description: Puede exportar formularios del repositorio al sistema local y migrar los formularios descargados al nuevo repositorio.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
exl-id: eafb1a93-8ee5-4420-830b-aee234988393
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: aa28c6c8-3ede-445b-a351-eeb0c9f9aec4
    internal-label: Interactive Communication
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
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
