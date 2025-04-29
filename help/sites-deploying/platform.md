---
title: Introducción a la plataforma de AEM
description: Obtenga información sobre la plataforma AEM y sus componentes más importantes, incluida la instalación e implementación de Adobe Experience Manager 6.5 LTS, y sobre su arquitectura, incluida la implementación en la nube de Adobe Managed Services.
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Architect
exl-id: c9ea613d-f1d1-49be-bd52-95d489442f46
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 4%

---

# Introducción a la plataforma de AEM{#introduction-to-the-aem-platform}

La plataforma AEM de AEM 6 se basa en Apache Jackrabbit Oak.

Apache Jackrabbit Oak es un esfuerzo por implementar un repositorio de contenido jerárquico escalable y de rendimiento para utilizarlo como la base de sitios web modernos de primera clase y otras aplicaciones de contenido exigentes.

Es el sucesor de Jackrabbit 2 y AEM 6 lo utiliza como backend predeterminado para su repositorio de contenido, CRX.

## Diseñar principios y objetivos {#design-principles-and-goals}

Oak implementa la especificación [JSR-283](https://jcp.org/en/jsr/detail?id=283) (JCR 2.0). Sus principales objetivos de diseño son:

* Mejor compatibilidad con repositorios grandes
* Varios nodos de clúster distribuido para alta disponibilidad
* Mejor rendimiento
* Compatibilidad con muchos nodos secundarios y niveles de control de acceso

## Concepto de arquitectura {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Almacenamiento {#storage}

El propósito de la capa de almacenamiento es:

* Implementación de un modelo de árbol
* Hacer el almacenamiento conectable
* Proporcionar un mecanismo de agrupación en clústeres

### Oak Core {#oak-core}

Oak Core agrega varias capas a la capa de almacenamiento:

* Controles de nivel de acceso
* Búsqueda e indexación
* Observación

### OAK JCR {#oak-jcr}

El objetivo principal del JCR de Oak es transformar la semántica de JCR en operaciones de árbol. También es responsable de:

* Implementación de la API JCR
* Que contengan vínculos de compromiso que implementen restricciones JCR.

Además, ahora es posible realizar implementaciones que no sean de Java y forman parte del concepto JCR de Oak.

## Resumen de almacenamiento {#storage-overview}

La capa de almacenamiento de Oak proporciona una capa de abstracción para el almacenamiento real del contenido.

Actualmente, hay dos implementaciones de almacenamiento disponibles en AEM6: **Almacenamiento Tar** y **Almacenamiento MongoDB**.

### Almacenamiento de tar {#tar-storage}

El almacenamiento Tar utiliza archivos tar. Almacena el contenido como varios tipos de registros en segmentos más grandes. Los diarios se utilizan para realizar un seguimiento del estado más reciente del repositorio.

Existen varios principios clave de diseño en torno a los cuales se construyó:

* **Segmentos inmutables**

El contenido se almacena en segmentos que pueden tener hasta 256 KB. Son inmutables, lo que facilita la caché de los segmentos a los que se accede con frecuencia y la reducción de los errores del sistema que pueden dañar el repositorio.

Cada segmento se identifica con un identificador único (UUID) y contiene un subconjunto continuo del árbol de contenido. Además, los segmentos pueden hacer referencia a otro contenido. Cada segmento mantiene una lista de UUID de otros segmentos a los que se hace referencia.

* **Localidad**

Los registros relacionados, como un nodo y sus tareas secundarias inmediatas, se almacenan en el mismo segmento. Al hacerlo, la búsqueda en el repositorio se realiza rápidamente y se evitan la mayoría de los errores de caché para los clientes habituales que acceden a más de un nodo relacionado por sesión.

* **Compacidad**

El formato de los registros está optimizado para su tamaño, a fin de reducir los costes de E/S y ajustar el mayor contenido posible en las cachés.

### Almacenamiento de Mongo {#mongo-storage}

El almacenamiento de MongoDB utiliza MongoDB para el uso compartido y la agrupación en clústeres. El árbol del repositorio se mantiene en una base de datos MongoDB, donde cada nodo es un documento independiente.

Tiene varias particularidades:

* Revisiones

Para cada actualización (confirmación) del contenido, se crea una nueva revisión. Una revisión es básicamente una cadena que consta de tres elementos:

1. Una marca de tiempo derivada de la hora del sistema de la máquina en la que se generó
1. Un contador para distinguir las revisiones creadas con la misma marca de tiempo
1. Id. del nodo de clúster donde se creó la revisión

* Ramas

Se admiten ramas, lo que permite al cliente almacenar en zona intermedia varios cambios y hacerlos visibles con una sola llamada de combinación.

* Documentos anteriores

El almacenamiento MongoDB agrega datos a un documento con cada modificación. Sin embargo, solo elimina datos si se activa explícitamente una limpieza. Los datos antiguos se mueven cuando se alcanza un umbral determinado. Los documentos anteriores solo contienen datos inmutables, lo que significa que solo contienen revisiones confirmadas y combinadas.

* Metadatos del nodo de clúster

Los datos sobre los nodos de clúster activos e inactivos se guardan en la base de datos para facilitar las operaciones de clúster.

Una configuración de clúster típica de AEM con almacenamiento MongoDB:

![chlimage_1-85](assets/chlimage_1-85.png)

## ¿En qué se diferencia de Jackrabbit 2? {#what-is-different-from-jackrabbit}

Como Oak es compatible con la versión anterior del estándar JCR 1.0, casi no hay cambios en el nivel de usuario. Sin embargo, existen algunas diferencias importantes que debe tener en cuenta al configurar una instalación de AEM basada en Oak:

* Oak no crea índices automáticamente. Como tal, se deben crear índices personalizados cuando sea necesario.
* A diferencia de Jackrabbit 2, donde las sesiones siempre reflejan el estado más reciente del repositorio, con Oak una sesión refleja una vista estable del repositorio desde el momento en que se adquirió la sesión. El motivo se debe al modelo MVCC en el que se basa Oak.
* Los hermanos del mismo nombre (SNS) no son compatibles con Oak.

## Documentación relacionada con otras plataformas {#other-platform-related-documentation}

Para obtener más información sobre la plataforma AEM, consulte también los artículos siguientes:

* [Configuración de los almacenes de nodos y los almacenes de datos en AEM 6](/help/sites-deploying/data-store-config.md)
* [Consultas e indexación de Oak](/help/sites-deploying/queries-and-indexing.md)
* [Elementos de almacenamiento en AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM con MongoDB](/help/sites-deploying/aem-with-mongodb.md)
