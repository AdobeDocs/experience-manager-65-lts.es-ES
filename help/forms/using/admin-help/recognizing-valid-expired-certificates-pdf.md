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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 8%

---

# Reconocer certificados válidos y caducados en documentos PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Cuando se abre en Adobe Reader un documento de PDF con derechos de uso aplicados por las extensiones de Reader, aparece una barra de estado que describe los derechos de uso específicos habilitados en el documento de PDF.

Cuando caduca el certificado digital que especifica los derechos de uso de un documento de PDF y el documento de PDF se abre en Adobe Reader, un cuadro de diálogo informa al usuario de que el documento de PDF tiene derechos de uso, pero estos derechos están desactivados. Aunque el mensaje indica que el documento de PDF se alteró o alteró, no es necesariamente el caso. Adobe Reader muestra este mensaje cuando caduca un certificado o se modifica un documento. En Adobe Reader 7.0.x o posterior, no puede determinar qué caso es el problema actualmente.

Después de cerrar el cuadro de diálogo, Adobe Reader abre el documento de PDF. Los derechos de uso aplicados con las extensiones de Acrobat Reader DC no están disponibles, según lo esperado. Si el documento de PDF es un formulario interactivo, los campos del formulario se bloquean y el usuario no puede cambiar los datos del formulario.
