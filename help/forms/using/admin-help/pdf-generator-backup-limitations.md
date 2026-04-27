---
title: Limitaciones de copia de seguridad del generador de PDF
description: Obtenga información acerca de las limitaciones de copia de seguridad de PDF Generator. No se puede realizar una copia de seguridad del directorio temporal que utiliza PDF Generator, ya que borra el contenido a intervalos establecidos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: f76ce3be-6d50-4531-a982-2e902f866208
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 10%

---

# Limitaciones de copia de seguridad del generador de PDF {#pdf-generator-backup-limitations}

No se puede realizar una copia de seguridad del directorio temporal que utiliza PDF Generator para convertir archivos. Aunque el servicio se restaure correctamente, los datos pueden perderse porque PDF Generator revisa y borra el contenido del directorio temporal a intervalos establecidos.
