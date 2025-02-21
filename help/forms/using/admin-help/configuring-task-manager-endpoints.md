---
title: Configurar los extremos del Administrador de tareas
description: Obtenga información sobre cómo configurar los extremos del Administrador de tareas para invocar el servicio. Se requieren diferentes configuraciones para configurar los extremos del Administrador de tareas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 3%

---

# Configurar los extremos del Administrador de tareas {#configuring-task-manager-endpoints}

Los extremos del Administrador de tareas permiten a los usuarios de Workspace invocar el servicio.

**Configuración del extremo del Administrador de tareas**

Use la siguiente configuración para configurar un extremo del Administrador de tareas.

**Nombre:** (obligatorio) identifica el extremo. El nombre se muestra en la vista de tarjeta de Workspace. No incluya un carácter &lt; porque truncará el nombre mostrado en Workspace. Si introduce una dirección URL como nombre del extremo, asegúrese de que se ajuste a las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Una descripción del extremo. No incluya un carácter &lt; porque truncará la descripción mostrada en Workspace.

**Instrucciones de tarea:** instrucciones para el usuario que inicia este flujo de trabajo.

**Propietario del proceso:** Nombre de la persona responsable del proceso.

**El usuario puede reenviar la tarea:** Permite al usuario reenviar la tarea inicial.

**Mostrar ventana de datos adjuntos:** Permite que el usuario vea la ventana de datos adjuntos.

**Permitir adición de datos adjuntos:** Permite al usuario agregar datos adjuntos y notas.

**Tarea bloqueada inicialmente:** bloquea la tarea inicial.

**Agregar ACL para colas compartidas:** La tarea inicial se crea con ACL para los usuarios de colas compartidas.

**Categorización:** (obligatoria) categoría en la que el usuario verá el formulario en Workspace. Seleccione una categoría de la lista o seleccione Nueva categoría para añadir una categoría.

**Nombre de operación:** (obligatorio) Una lista de operaciones que se pueden asignar al extremo.
