---
title: Comprobaciones de coherencia y recorrido
description: Aprenda a realizar comprobaciones de coherencia y transversales.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 6ed130d5-30b5-4864-8bea-dfe41bed5422
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Comprobaciones de coherencia y recorrido{#consistency-and-traversal-checks}

Al actualizar, puede haber problemas debido a incoherencias en el espacio de trabajo. Puede ejecutar una actualización de prueba para ver si se trata de un problema o ejecutar las comprobaciones de coherencia como acción preventiva.

Si ejecuta una actualización de prueba que falla debido a incoherencias en el espacio de trabajo, verá entradas similares a las siguientes en crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Realizar una comprobación de coherencia {#perform-a-consistency-check}

Para realizar una comprobación de coherencia, vaya a la página de administración del Mbean JMX **com.adobe.granite (Repository)**. En la pantalla principal de AEM, vaya a:

**Herramientas > Consola web > Principal (en la barra de menús) > JMX > com.adobe.granite (Repositorio)**

En una instalación predeterminada, se encuentra aquí: **[|Mostrar|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

En la sección **Operaciones** de la página, se encuentran dos métodos: **`traversalCheck`** y **`consistencyCheck`**. Para ejecutar una comprobación, haga clic en la operación e introduzca los parámetros deseados.

![chlimage_1-117](assets/chlimage_1-117.png)
