---
title: Configurar extensiones de Acrobat Reader DC para capturar datos
description: Obtenga información sobre cómo configurar extensiones de Acrobat Reader DC para capturar datos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services,Reader Extensions
hide: true
hidefromtoc: true
exl-id: f9b01de7-1de5-43aa-bcc3-b15719bfa5c0
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Configurar extensiones de Acrobat Reader DC para capturar datos {#configuring-acrobat-reader-dc-extensions-for-data-capture}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Si los usuarios de la instalación de formularios AEM Forms utilizan la funcionalidad de captura de datos de Content Services (Obsoleto), se recomienda crear una función con acceso de solo lectura para estos usuarios.

***Nota **: Adobe® LiveCycle® Content Services ES (Obsoleto) es un sistema de administración de contenido instalado con LiveCycle. Permite a los usuarios diseñar, administrar, supervisar y optimizar procesos centrados en las personas. La compatibilidad con los servicios de contenido (obsoleto) finaliza el 31/12/2014. Ver [documento del ciclo de vida del producto Adobe](https://helpx.adobe.com/es/support/programs/eol-matrix.html).*

La captura de datos requiere que asigne una función de usuario para acceder a SampleReaderExtensionsCredential. Puede asignar la función estándar Administrador de confianza. Sin embargo, tenga en cuenta que esta función proporciona a los usuarios no administradores privilegios generales de administrador que controlan la configuración de confianza de PKI y administran las credenciales de PKI, lo que podría poner en peligro la seguridad de la instalación de los formularios AEM Forms en un entorno de producción. Se recomienda que el administrador del sistema de AEM Forms cree una función que conceda acceso de solo lectura al Almacén de confianza y asigne esta nueva función a usuarios que no sean administradores y que utilicen la captura de datos.

## Cree una función para los usuarios de captura de datos {#create-a-role-for-data-capture-users}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Nueva función.
1. Introduzca el nombre de la función (por ejemplo, Usuario de captura de datos) y la descripción en los campos correspondientes y, a continuación, haga clic en Siguiente.
1. En la pantalla Permisos de funciones, haga clic en Buscar permisos y, a continuación, seleccione Lectura de credencial en la lista de permisos disponibles.
1. Haga clic en Aceptar y luego en Finalizar.

## Asignar la función de captura de datos {#assign-the-data-capture-role}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de funciones y, a continuación, haga clic en Buscar.
1. Haga clic en la función de usuario de captura de datos que ha creado.
1. En la ficha Usuarios/grupos de roles, haga clic en Buscar usuarios/grupos.
1. En la pantalla Buscar usuarios y grupos, haga clic en Buscar, seleccione los usuarios que necesitan la función de usuario de captura de datos y, a continuación, haga clic en Aceptar.
1. En la pantalla Editar rol, haga clic en Guardar.
