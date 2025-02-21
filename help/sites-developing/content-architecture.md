---
title: Arquitectura de contenido
description: 'Sugerencias para crear el contenido (sugerencia: todo es contenido)'
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Arquitectura de contenido{#content-architecture}

## Seguir el modelo de David {#follow-david-s-model}

El Modelo de David fue escrito por David Nuescheler hace años, pero las ideas son ciertas hoy en día. Los principios principales del Modelo de David son los siguientes:

* Los datos van primero, la estructura después. Tal vez.
* Impulse la jerarquía de contenido, no permita que ocurra.
* Los espacios de trabajo son para `clone()`, `merge()` y `update()`.
* Tenga cuidado con los hermanos del mismo nombre.
* Las referencias se consideran perjudiciales.
* Los archivos son archivos.
* Los identificadores son malvados.

El modelo de David se encuentra en la wiki de Jackrabbit en [https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel).

### Todo está contenido {#everything-is-content}

Todo debe almacenarse en el repositorio, en lugar de depender de fuentes de datos de terceros independientes, como bases de datos. Esto se aplica al contenido creado, a los datos binarios como imágenes, códigos y configuraciones. Esto nos permite utilizar un conjunto de API para administrar todo el contenido y para administrar la promoción de este contenido a través de la replicación. También obtiene una única fuente de copia de seguridad, registro, etc.

### Utilice el principio de diseño &quot;el modelo de contenido primero&quot; {#use-the-content-model-first-design-principle}

Al crear una nueva función, comience siempre por diseñar primero la estructura de contenido JCR y, a continuación, busque leer y escribir el contenido utilizando los servlets predeterminados de Sling. Esto le permite asegurarse de que la implementación funciona correctamente con los mecanismos de control de acceso predeterminados y evitar generar servlets innecesarios de estilo CRUD.

### Ser RESTful {#be-restful}

Los servlets deben definirse en función de resourceTypes en lugar de rutas. Esto permite utilizar controles de acceso JCR, adherirse a los principios de REST y utilizar el solucionador de recursos y recursos que se nos proporciona en la solicitud. Esto también nos permite cambiar las secuencias de comandos que representan las direcciones URL en el servidor sin necesidad de cambiar ninguna dirección URL del lado del cliente, mientras ocultamos los detalles de implementación del lado del servidor del cliente para mayor seguridad.

### Evite definir nuevos tipos de nodo {#avoid-defining-new-node-types}

Los tipos de nodo funcionan en un nivel bajo en la capa de infraestructura y la mayoría de los requisitos se pueden cumplir mediante un tipo de nodo sling:resourceType asignado a un tipo de nodo nt:unstructured, oak:Unstructured, sling:Folder o cq:Page. Los tipos de nodo equivalen al esquema en el repositorio y cambiar los tipos de nodo puede resultar caro en el futuro.

### Respetar las convenciones de nomenclatura en JCR. {#adhere-to-naming-conventions-in-the-jcr}

El cumplimiento de las convenciones de nomenclatura agrega coherencia a la base de código, reduciendo la tasa de incidencia de defectos y aumentando la velocidad de los desarrolladores que trabajan en el sistema. Adobe utiliza las siguientes convenciones para desarrollar AEM:

* Nombres de nodo

   * Todas las minúsculas
   * Separación de palabras mediante guiones

* Nombres de propiedades

   * Mayúsculas y minúsculas, a partir de una letra minúscula

* Componentes (JSP/HTML)

   * Todas las minúsculas
   * Separación de palabras mediante guiones
