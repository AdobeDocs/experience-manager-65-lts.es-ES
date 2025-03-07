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
hidefromtoc: true
exl-id: 34381caa-154e-479c-b475-7b3549909e9a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
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
