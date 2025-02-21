---
title: Depurar datos de procesos
description: Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que da como resultado un menor rendimiento de los formularios AEM Forms y el uso de espacio en disco innecesario. Consulte cómo puede depurar datos de proceso.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 3%

---

# Depurar datos de procesos {#purging-process-data}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Los datos de proceso que se generan cuando se invoca un proceso de larga duración pueden llegar a ser demasiado grandes, lo que da como resultado un menor rendimiento de los formularios AEM Forms y el uso de espacio en disco innecesario. Se recomienda depurar los datos de proceso cuando ya no son necesarios los registros. Los formularios AEM Forms proporcionan varios medios para depurar datos de proceso:

* Puede utilizar la consola de administración para realizar una depuración única de registros obsoletos relacionados con procesos de larga duración o para programar depuraciones automáticas regulares. (Consulte [Purgar registros de la base de datos de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Puede utilizar la API de Java y la API del servicio web de AEM Forms para depurar mediante programación los datos de proceso relacionados con procesos de larga duración. (Consulte &quot;Purgar datos de proceso&quot; en [Programar con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63)).
* Utilice la herramienta de depuración de procesos para depurar procesos en función del nombre del proceso y otros parámetros. Para obtener más información, consulte el archivo léame de la herramienta de depuración de procesos, en *[raíz de aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
