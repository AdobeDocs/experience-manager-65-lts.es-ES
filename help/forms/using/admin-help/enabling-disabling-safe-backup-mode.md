---
title: Habilitar y deshabilitar el modo de copia de seguridad
description: En la página Configuración de copia de seguridad, puede utilizar los formularios de AEM en el modo de copia de seguridad segura para poder realizar copias de seguridad fiables de la base de datos y del directorio de almacenamiento global de documentos (GDS) (GDS). Obtenga información sobre cómo habilitar y deshabilitar el modo de copia de seguridad segura.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 34381caa-154e-479c-b475-7b3549909e9a
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
source-wordcount: '208'
ht-degree: 5%
---
# Habilitar y deshabilitar el modo de copia de seguridad {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

En la página Configuración de copia de seguridad, puede utilizar los formularios de AEM en el modo de copia de seguridad segura para poder realizar copias de seguridad fiables de la base de datos y del directorio de almacenamiento global de documentos (GDS) (GDS).

Mientras los formularios AEM Forms están en modo de copia de seguridad segura, funcionan normalmente, excepto que no quitan activamente los archivos del directorio GDS.

>[!NOTE]
>
>La configuración de esta opción no realiza una copia de seguridad del sistema, sino que lo prepara para realizar una copia de seguridad.

## Habilitar modo de copia de seguridad {#enable-safe-backup-mode}

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuración de copia de seguridad.
1. En la página Configuración de copia de seguridad, seleccione Operar en modo de copia de seguridad segura y haga clic en Aceptar.

>[!NOTE]
>
>Si el sistema ya se está ejecutando en modo de copia de seguridad, no se creará una nueva reserva al hacer clic en Aceptar.

## Desactivar el modo de copia de seguridad {#disable-safe-backup-mode}

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuración de copia de seguridad.
1. En la página Configuración de copia de seguridad, anule la selección de Operar en modo de copia de seguridad segura y haga clic en Aceptar.
