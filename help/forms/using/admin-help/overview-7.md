---
title: Aspectos básicos de la configuración de formularios
description: Obtenga información sobre los distintos servicios de Forms que le ayudan a crear aplicaciones de captura de datos interactivas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 68e43842-cba9-47b8-b7a3-6f625dbfca08
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 4%

---

# Aspectos básicos de la configuración de formularios {#basics-of-configuring-forms}

El servicio Forms permite crear aplicaciones cliente de captura de datos interactivas que validan, procesan, transforman y envían formularios creados normalmente en Designer. Los autores de formularios desarrollan un único diseño de formulario que el servicio Forms procesa en varios formatos:

* como PDF en Adobe Reader o en un explorador
* como HTML en varios entornos de explorador, incluido un procesamiento XHTML 1.0 compatible
* como guías de formulario en varios entornos de explorador compatibles con Adobe Flash Player.

Para obtener información adicional acerca del servicio Forms, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

Con la página Forms de la consola de administración, puede configurar el comportamiento del servicio de Forms. Esta configuración se aplica a todas las invocaciones del servicio. Cualquier parámetro enviado a través de AEM Forms SDK anula la configuración establecida en la consola de administración; sin embargo, solo afecta a esa invocación en particular.

Después de cambiar la configuración de Forms en la consola de administración, haga clic en Guardar. No es necesario reiniciar el servidor para que los cambios surtan efecto. Sin embargo, es posible que tenga que detener y reiniciar el servicio de Forms al configurar el modo de caché. (Consulte [Iniciar y detener servicios](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services).)
