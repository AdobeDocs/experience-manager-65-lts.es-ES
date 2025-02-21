---
title: Error al realizar la copia de seguridad de la base de datos durante la actualización a 6.5.12.0 para MySQL.
description: Cuando un usuario actualiza a Experience Manager 6.5.12.0 y hace clic en "Actualizar MySQL", el administrador de configuración no realiza una copia de seguridad de la base de datos de Experience Manager Forms anterior.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 6%

---

# Error al realizar la copia de seguridad de la base de datos durante la actualización a 6.5.12.0 para MySQL {#issue}

Cuando un usuario actualiza a Experience Manager 6.5.12.0 y hace clic en &quot;Actualizar MySQL&quot;, el administrador de configuración no realiza una copia de seguridad de la base de datos de Experience Manager Forms anterior. Muestra el error:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Aplicable a {#applies-to}

* Experience Manager 6.5 Forms

## Solución {#solution}

Para resolver el problema, aumente el max_packet_size de la base de datos a 100 M o según sea necesario en el archivo my.ini ubicado en {AEM_HOME}/mysql.
