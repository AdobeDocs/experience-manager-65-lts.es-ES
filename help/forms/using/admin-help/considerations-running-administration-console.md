---
title: Consideraciones al ejecutar la consola de administración
description: Este documento enumera algunos puntos a tener en cuenta al ejecutar la consola de administración.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: bdd884c4-ae12-4827-8251-01033cbc0185
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
source-wordcount: '147'
ht-degree: 0%
---
# Consideraciones al ejecutar la consola de administración {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Estas son algunas cuestiones que se deben tener en cuenta al ejecutar la consola de administración:

* Si accede a la consola de administración mediante la dirección URL `https://[hostname]:'port'/adminui`, el nombre de host especificado no puede contener caracteres de guion bajo. De lo contrario, es posible que los vínculos a algunas áreas de la consola de administración no funcionen correctamente.
* Si ejecuta una consola de administración en el Explorador de Windows en un sistema operativo japonés, puede encontrar estos problemas:

  * Al hacer clic en un vínculo, vuelve a la página de inicio de sesión en lugar de al vínculo esperado.
  * Al hacer clic en un vínculo, se muestra un error de permiso.

  Se recomienda ejecutar la consola de administración desde otro explorador, como Mozilla Firefox, para garantizar que no se produzcan errores en los vínculos.

* No utilice caracteres de barra invertida () al realizar búsquedas en la consola de administración.
