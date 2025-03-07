---
title: Agregar, activar, modificar o eliminar puntos finales
description: Obtenga información sobre cómo agregar, habilitar, modificar y quitar extremos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 14264788-a05a-4a8d-b485-33ae1caac094
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 4%

---

# Agregar, activar, modificar o eliminar puntos finales {#adding-enabling-modifying-or-removing-endpoints}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

## Agregar un extremo a un servicio {#add-an-endpoint-to-a-service}

Los extremos solo se pueden agregar a los servicios. Un extremo no puede existir solo; debe estar asociado a un servicio.

>[!NOTE]
>
>Se recomienda utilizar nombres únicos al agregar puntos finales.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio que desea configurar.
1. En la lista de la pestaña Puntos finales, seleccione el tipo de punto de conexión que desea agregar y haga clic en Agregar.
1. Según el tipo de extremo, configure opciones de extremo adicionales.

[Configuración del extremo de carpeta inspeccionada](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Configuración de extremo de correo electrónico](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configurar los extremos del Administrador de tareas](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Configuración del extremo remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Haga clic en Agregar.

## Habilitar o deshabilitar un extremo {#enable-or-disable-an-endpoint}

De forma predeterminada, los nuevos extremos se habilitan automáticamente. Pero si ha deshabilitado un punto final, debe habilitarlo para que esté operativo.

Si tiene problemas con los servicios de, deshabilite los extremos asociados de para solucionar mejor el problema. También es posible que desee deshabilitar los extremos durante el mantenimiento regular del sistema o al actualizar un servicio.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Endpoint Management.
1. En la página Administración de extremos, active la casilla de verificación del extremo que desea habilitar o deshabilitar y haga clic en Habilitar o Deshabilitar.

## Modificar un extremo {#modify-an-endpoint}

>[!NOTE]
>
>Los cambios realizados en una configuración de extremo mediante la consola de administración no se reflejan en las copias en tiempo de diseño de las aplicaciones. Si vuelve a implementar una aplicación, se perderá cualquier cambio que haya realizado en sus extremos mediante la consola de administración.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Endpoint Management.
1. En la página Endpoint Management, haga clic en el extremo que desea modificar.
1. En la página Actualizar extremo, modifique el nombre, la descripción y la configuración del extremo.

   >[!NOTE]
   >
   >No incluya un carácter &lt; en el nombre o la descripción, ya que truncará el nombre o la descripción mostrados en Workspace.

1. Para guardar los cambios, haga clic en Actualizar.

También puede realizar esta tarea desde la página Administración de servicios seleccionando un servicio y haciendo clic en la pestaña Puntos finales.

## Quitar un extremo {#remove-an-endpoint}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Endpoint Management.
1. En la página Administración de extremos, active la casilla de verificación del extremo que desea quitar y haga clic en Quitar. El extremo ya no se muestra.
