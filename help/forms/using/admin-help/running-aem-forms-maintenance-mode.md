---
title: Ejecutar AEM Forms en modo de mantenimiento
description: El modo de mantenimiento es útil cuando se realizan tareas como aplicar parches a un DSC, actualizar formularios AEM o aplicar un service pack. Obtenga más información sobre la ejecución de formularios AEM en modo de mantenimiento.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: d4cfe1c1-8b44-4bd5-b6ec-29e5f70f0674
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
source-wordcount: '259'
ht-degree: 4%
---
# Ejecutar AEM Forms en modo de mantenimiento {#running-aem-forms-in-maintenance-mode}

El modo de mantenimiento es útil cuando se realizan tareas como aplicar parches a un DSC, actualizar formularios AEM o aplicar un service pack.

Evite invocar procesos mientras el servidor se encuentra en modo de mantenimiento. Esto es lo que sucede si se invoca un proceso mientras el servidor está en modo de mantenimiento:

* Si el proceso es de larga duración, se añade a la base de datos de trabajos, pero no se inicia. Al salir del modo de mantenimiento, los formularios AEM Forms procesan los trabajos de larga duración en su cola, incluso si el servidor se reinició mientras estaba en modo de mantenimiento.
* Si el proceso es de corta duración, se procesa de inmediato.

**Poner formularios AEM en modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   Se muestra el mensaje &quot;ahora en pausa&quot; en la ventana del explorador.

   >[!NOTE]
   >
   >Si apaga el servidor mientras está en modo de mantenimiento, cuando se reinicia aún estará en modo de mantenimiento. Desactive el modo de mantenimiento cuando haya terminado sus tareas de mantenimiento.

**Compruebe si AEM Forms se está ejecutando en modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   El estado se muestra en la ventana del explorador. El estado &quot;true&quot; indica que el servidor se está ejecutando en modo de mantenimiento y &quot;false&quot; indica que el servidor no está en modo de mantenimiento.

**Desactivar el modo de mantenimiento**

1. En un explorador web, introduzca:

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   Se muestra el mensaje &quot;now running&quot; en la ventana del explorador.
