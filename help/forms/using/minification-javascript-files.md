---
title: Minificación de los archivos JavaScript
description: Instrucciones para generar código minificado después de las personalizaciones de AEM Forms Workspace para optimizar los archivos JS para la web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 56%

---

# Minificación de los archivos JavaScript {#minification-of-the-javascript-files}

La minificación elimina del código fuente los caracteres redundantes, como los espacios en blanco, las líneas nuevas y los comentarios. Esto mejora el rendimiento al reducir el tamaño del código. Aunque la minificación no afecta a la funcionalidad, reduce la legibilidad del código.

Para generar código minificado para cambios semánticos, siga estos pasos.

1. Copie `client-html/src/main/webapp/js` desde src-package en el sistema de archivos.

   >[!NOTE]
   >
   >Consulte [Introducción a la personalización de AEM Forms Workspace](/help/forms/using/introduction-customizing-html-workspace.md) para obtener más información sobre los paquetes.

1. Actualice las rutas de `main.js`, ubicado en client-html/src/main/webapp/js, para obtener modelos o vistas agregados o actualizados.

   Por ejemplo, si se agrega un nuevo modelo de Sharequeue, por ejemplo, mySharequeue, cambie lo siguiente:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   A

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Actualice `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` en el caso de que haya algún cambio o adición de alias en `main.js`.

   Por ejemplo, si se agrega un nuevo modelo de Sharequeue, por ejemplo, mySharequeue, cambie lo siguiente:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   A

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. Ejecute el siguiente comando en client-html/src/main/webapp/js/minifier:

   ```shell
   mvn clean install
   ```

   Genera una carpeta de archivos minificados en client-html/src/main/webapp/js en la que main.js y register.js están minificados.

>[!NOTE]
>
>La minificación solo funciona en JVM de 64 bits.

>[!NOTE]
>
>Si utiliza la minificación, la actualización se verá afectada.
