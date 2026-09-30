---
title: Reconocer certificados válidos y caducados en documentos PDF
description: Obtenga información sobre cómo reconocer certificados válidos y caducados en documentos de PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: f7402f0d-7c19-4a56-8630-208faa197f94
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 8%
---
# Reconocer certificados válidos y caducados en documentos PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Cuando se abre en Adobe Reader un documento de PDF con derechos de uso aplicados por las extensiones de Reader, aparece una barra de estado que describe los derechos de uso específicos habilitados en el documento de PDF.

Cuando caduca el certificado digital que especifica los derechos de uso de un documento de PDF y el documento de PDF se abre en Adobe Reader, un cuadro de diálogo informa al usuario de que el documento de PDF tiene derechos de uso, pero estos derechos están desactivados. Aunque el mensaje indica que el documento de PDF se alteró o alteró, no es necesariamente el caso. Adobe Reader muestra este mensaje cuando caduca un certificado o se modifica un documento. En Adobe Reader 7.0.x o posterior, no puede determinar qué caso es el problema actualmente.

Después de cerrar el cuadro de diálogo, Adobe Reader abre el documento de PDF. Los derechos de uso aplicados con las extensiones de Acrobat Reader DC no están disponibles, según lo esperado. Si el documento de PDF es un formulario interactivo, los campos del formulario se bloquean y el usuario no puede cambiar los datos del formulario.
