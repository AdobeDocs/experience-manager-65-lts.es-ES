---
title: Procedimiento de actualización
description: Obtenga información acerca del procedimiento para actualizar Adobe Experience Manager (AEM).
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: ae78421de75518894f3996829e554acd9003a6d1
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Procedimiento de actualización {#upgrade-procedure}

>[!NOTE]
>
>La actualización requiere tiempo de inactividad para el nivel de Author, ya que la mayoría de las actualizaciones de Adobe Experience Manager (AEM) se realizan in situ. Si sigue estas prácticas recomendadas, puede minimizar o eliminar el tiempo de inactividad del nivel de publicación.

Al actualizar los entornos de AEM, debe tener en cuenta las diferencias de enfoque entre actualizar los entornos de creación o los entornos de publicación para minimizar el tiempo de inactividad tanto para los autores como para los usuarios finales. Esta página describe el procedimiento de alto nivel para actualizar una topología de AEM que se esté ejecutando en una versión de AEM 6.x. Dado que el proceso difiere entre los niveles de creación y publicación y las implementaciones basadas en Mongo y TarMK, cada nivel y micronúcleo se han enumerado en una sección independiente. Al ejecutar la implementación, Adobe recomienda actualizar primero el entorno de creación, determinar el éxito y, a continuación, continuar con los entornos de publicación.

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## Nivel de TarMK Author {#tarmk-author-tier}

### Iniciando topología {#starting-topology}

La topología supuesta para esta sección consiste en un servidor de creación que se ejecuta en TarMK con una espera fría. La replicación se produce desde el servidor de creación a la granja de servidores de publicación TarMK. Aunque no se ilustra aquí, este enfoque también se puede utilizar para implementaciones que utilizan descarga. Asegúrese de actualizar o volver a generar la instancia de descarga en la nueva versión después de deshabilitar los agentes de replicación en la instancia de autor y antes de volver a habilitarlos.

![tarmk_start_topology](assets/tarmk_starting_topology.jpg)

### Preparación de actualización {#upgrade-preparation}

![autor-preparación-actualización](assets/upgrade-preparation-author.png)

1. Detener la creación de contenido.

1. Detenga la instancia de espera.

1. Deshabilite los agentes de replicación en el autor.

1. Ejecute las [tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### Ejecución de actualización {#upgrade-execution}

![ejecutar_actualización](assets/execute_upgrade.jpg)

1. Ejecute la [actualización local](/help/sites-deploying/in-place-upgrade.md).
1. Actualice el módulo de Dispatcher *si es necesario*.

1. QA valida la actualización.

1. Cierre la instancia de autor.

### Si se realiza correctamente {#if-successful}

![si_tiene éxito](assets/if_successful.jpg)

1. Copie la instancia actualizada para crear una espera en frío.

1. Inicie la instancia de autor.

1. Inicie la instancia de espera.

### Si no lo consigue (reversión) {#if-unsuccessful-rollback}

![reversión](assets/rollback.jpg)

1. Inicie la instancia de espera en frío como la nueva instancia principal.

1. Reconstruir el entorno de creación desde el modo de espera en frío.

## Clúster de autor de MongoMK {#mongomk-author-cluster}

### Iniciando topología {#starting-topology-1}

La topología supuesta para esta sección consiste en un clúster de creación de MongoMK con al menos dos instancias de autor de AEM, respaldadas por al menos dos bases de datos MongoMK. Todas las instancias de autor comparten un almacén de datos. Estos pasos deben aplicarse tanto a los almacenes de datos S3 como a los de archivos. La replicación se produce desde los servidores de creación a la granja de servidores de publicación TarMK.

![topología mongo](assets/mongo-topology.jpg)

### Preparación de actualización {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. Detener la creación de contenido.
1. Clone el almacén de datos para la copia de seguridad.
1. Detenga todas las instancias de autor de AEM, excepto una, y su autor principal.
1. Elimine todos los nodos MongoDB excepto uno del conjunto de réplicas, su instancia principal de Mongo.
1. Actualice el archivo `DocumentNodeStoreService.cfg` en el autor principal para reflejar el conjunto de réplicas de un solo miembro.
1. Reinicie el autor principal para asegurarse de que se reinicia correctamente.
1. Deshabilite los agentes de replicación en el autor principal.
1. Ejecute [tareas de mantenimiento previas a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) en la instancia de autor principal.

### Ejecución de actualización {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. Ejecute una [actualización local](/help/sites-deploying/in-place-upgrade.md) en el autor principal.
1. Actualice el Dispatcher o el módulo web *si es necesario*.
1. QA valida la actualización.

### Si se realiza correctamente {#if-successful-1}

![mongo-secondary](assets/mongo-secondaries.jpg)

1. Cree nuevas instancias de autor de AEM 6.5 LTS, conectadas a la instancia actualizada de Mongo.

1. Vuelva a generar los nodos MongoDB que se quitaron del clúster.

1. Actualice los `DocumentNodeStoreService.cfg` archivos para reflejar el conjunto de réplicas completo.

1. Reinicie las instancias de autor de a una por vez.

1. Elimine el almacén de datos clonado.

### Si no lo consigue (reversión)  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. Vuelva a configurar las instancias de autor secundarias para conectarse al almacén de datos clonado.

1. Cierre la instancia principal de Author actualizada.

1. Cierre la instancia principal de Mongo actualizada.

1. Inicie las instancias secundarias de Mongo con una de ellas como la nueva principal.

1. Configure los archivos `DocumentNodeStoreService.cfg` en las instancias de autor secundarias para que apunten al conjunto de réplicas de instancias Mongo aún no actualizadas.

1. Inicie las instancias de autor secundarias.

1. Limpie las instancias de autor actualizadas, el nodo Mongo y el almacén de datos.

## Granja de publicación TarMK {#tarmk-publish-farm}

### Granja de publicación TarMK {#tarmk-publish-farm-1}

La topología supuesta para esta sección consiste en dos instancias de publicación de TarMK, delante de Dispatcher y, a su vez, delante de un equilibrador de carga. La replicación se produce desde el servidor de creación a la granja de servidores de publicación TarMK.

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### Ejecución de actualización {#upgrade-execution-2}

![actualizar-publicar2](assets/upgrade-publish2.png)

1. Detenga el tráfico a la instancia de Publish 2 en el equilibrador de carga.
1. Ejecutar [mantenimiento previo a la actualización](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) en Publish 2.
1. Ejecute una [actualización local](/help/sites-deploying/in-place-upgrade.md) en Publish 2.
1. Actualice el Dispatcher o el módulo web *si es necesario*.
1. Vacíe la caché de Dispatcher.
1. QA valida Publish 2 a través de Dispatcher, detrás del cortafuegos.
1. Cerrar publicación 2.
1. Copie la instancia de Publish 2.
1. Iniciar publicación 2.

### Si se realiza correctamente {#if-successful-2}

![actualización-publicación1](assets/upgrade-publish1.png)

1. Habilitar tráfico en Publish 2.
1. Detener el tráfico en Publish 1.
1. Detenga la instancia Publish 1.
1. Reemplace la instancia Publish 1 por una copia de Publish 2.
1. Actualice el Dispatcher o el módulo web *si es necesario*.
1. Vaciar la memoria caché de Dispatcher para Publish 1.
1. Iniciar publicación 1.
1. QA valida Publish 1 a través de Dispatcher, detrás del cortafuegos.

### Si no lo consigue (reversión) {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. Cree una copia de Publish 1.
1. Reemplace la instancia de Publish 2 por una copia de Publish 1.
1. Vaciar la memoria caché de Dispatcher para Publish 2.
1. Iniciar publicación 2.
1. QA valida Publish 2 a través de Dispatcher, detrás del cortafuegos.
1. Habilitar tráfico en Publish 2.

## Pasos finales de la actualización {#final-upgrade-steps}

1. Habilitar el tráfico en Publicar 1.
1. QA realiza la validación final desde una dirección URL pública.
1. Habilite los agentes de replicación desde el entorno de creación.
1. Reanudar creación de contenido.
1. Realizar [comprobaciones posteriores a la actualización](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![final](assets/final.jpg)
