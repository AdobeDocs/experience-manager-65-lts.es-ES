---
title: Cómo modelar el contenido
description: En esta parte del Recorrido para desarrolladores de contenido sin encabezado de AEM, aprenderá a modelar el contenido para la entrega de contenido sin encabezado de AEM utilizando el Modelado de contenido con modelos de fragmentos de contenido y fragmentos de contenido.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 79%

---

# Cómo modelar el contenido {#model-your-content}

En esta parte del [Recorrido para desarrolladores de contenido sin encabezado de AEM](overview.md), puede aprender a modelar la estructura de contenido. A continuación, tenga en cuenta que la estructura de Adobe Experience Manager (AEM) utiliza modelos de fragmentos de contenido y fragmentos de contenido para su reutilización en todos los canales.

## Lo que hemos visto hasta ahora {#story-so-far}

Al principio, [Obtenga información acerca del desarrollo sin encabezado de CMS](learn-about.md) abarcó la entrega de contenido sin encabezado y por qué debería usarse. A continuación, [Introducción a AEM Headless](getting-started.md) describió AEM Headless en el contexto de su propio proyecto.

En el documento anterior del recorrido del contenido sin encabezado de AEM, [Ruta hacia la primera experiencia al usar contenido sin encabezado de AEM](path-to-first-experience.md), aprendió los pasos necesarios para implementar su primer proyecto. Después de leerlo, debería:

* Comprender las consideraciones de planificación importantes para diseñar el contenido
* Comprender los pasos para implementar sin encabezado según los requisitos de nivel de integración.
* Configurar las herramientas y configuraciones de AEM necesarias.
* Conocer las prácticas recomendadas para que su recorrido sin encabezado sea fluido, mantenga la eficiencia de la generación de contenido y asegurarse de que el contenido se entregue rápidamente.

Este artículo se basa en estos fundamentos para que entienda cómo preparar su propio proyecto de AEM sin encabezado.

## Objetivo {#objective}

* **Audiencia**: principiante
* **Objetivo**: aprenda a modelar la estructura de contenido y, a continuación, a llevar a cabo esa estructura utilizando modelos de fragmentos de contenido y fragmentos de contenido de AEM.
   * Introduzca conceptos y terminología relacionados con el modelado de datos/contenido.
   * Descubra por qué se necesita el modelado de contenido para la entrega de contenido sin encabezado.
   * Aprenda a llevar a cabo esta estructura utilizando modelos de fragmento de contenido de AEM (y a crear contenido con fragmentos de contenido).
   * Aprenda a modelar el contenido y los principios con muestras básicas.

>[!NOTE]
>
>El modelado de datos es un campo muy grande, ya que se utiliza para desarrollar bases de datos relacionales. Hay muchos libros y fuentes de información en línea disponibles.
>
>Solo se tienen en cuenta los aspectos que son de interés al modelar datos para utilizarlos con AEM Headless.

## Modelado de contenido {#content-modeling}

*Es un mundo grande y peligroso*.

Quizás sí, pero quizás no. Sin duda es un mundo ***complicado*** de manera abrumadora. El modelado de datos se utiliza para definir una representación simplificada de una subsección muy (muy) pequeña, utilizando la información específica que se necesita para un propósito determinado.

>[!NOTE]
>
>Dado que AEM se ocupa del contenido, el modelado de datos se denomina modelado de contenido.

Por ejemplo:

Hay muchas escuelas, pero todas tienen varias cosas en común.

* Una ubicación,
* un director
* muchos profesores,
* muchos miembros del personal no docente,
* muchos alumnos,
* muchos exprofesores,
* muchos exalumnos,
* muchos salones,
* muchos libros,
* mucho equipamiento,
* muchas actividades extraescolares,
* etc...

Incluso en un ejemplo tan pequeño, la lista puede parecer interminable. Pero si simplemente desea que la aplicación realice una tarea sencilla, puede limitar la información a lo esencial.

Por ejemplo, anunciar eventos especiales para todas las escuelas de la zona:

* Nombre del colegio
* Ubicación
* Director
* Tipo de evento
* Fecha del evento
* Profesor que organiza el evento

### Conceptos  {#concepts}

Lo que desea describir se denomina **Entidades**; básicamente, las &quot;cosas&quot; sobre las que desea almacenar información.

La información que deseamos almacenar son los **Atributos** (propiedades), como el Nombre y las Cualificaciones del profesorado.

A continuación, hay varias **Relaciones** entre las entidades. Por ejemplo, normalmente una escuela tiene un director y varios profesores (normalmente, el director también suele ser un profesor).

El proceso de análisis y definición de esta información, junto con las relaciones entre ellos se denomina **Modelado de contenido**.

### Datos básicos {#basics}

A menudo, puede empezar por dibujar un **Esquema conceptual** que describe las entidades y sus relaciones. Normalmente es de alto nivel conceptual.

Cuando haya terminado, puede convertir los modelos en un **Esquema lógico** que describe las entidades, junto con los atributos y las relaciones. En este nivel, debe examinar detenidamente las definiciones para eliminar la duplicación y optimizar el diseño.

>[!NOTE]
>
>A veces, estos dos pasos se combinan; a menudo, esto depende de la complejidad del escenario.

Por ejemplo, ¿necesita entidades independientes para `Head Teacher` y `Teacher`, o simplemente un atributo adicional en el modelo `Teacher`?

### Garantía de integridad de los datos {#data-integrity}

La integridad de los datos es necesaria para garantizar la precisión y coherencia del contenido durante todo su ciclo de vida. Esto incluye garantizar que los autores de contenido puedan comprender fácilmente qué almacenar y dónde, por lo que los elementos siguientes son vitales:

* una estructura clara,
* una estructura lo más concisa posible (sin sacrificar la precisión),
* validación de campos individuales,
* cuando proceda, restringir el contenido de campos específicos a lo que sea significativo.

### Eliminación de la redundancia de datos {#data-redundancy}

La redundancia de datos se produce cuando la misma información se almacena dos veces dentro de la estructura de contenido. Esto debe evitarse, ya que puede provocar confusión al crear el contenido y errores en la consulta; sin mencionar el uso indebido del espacio de almacenamiento.

### Optimización y rendimiento {#optimization-and-performance}

Al optimizar su estructura, puede mejorar el rendimiento, tanto para la creación de contenido como para realizar consultas.

Todo es un acto de equilibrio, pero crear una estructura que sea demasiado compleja o con demasiados niveles puede:

* Resultar confuso para los autores que generan el contenido.

* Afectar gravemente al rendimiento si la consulta tiene que acceder a varios fragmentos de contenido anidados (referenciados) para recuperar el contenido necesario.

## Modelado de contenido sin encabezado de AEM {#content-modeling-for-aem-headless}

El modelado de datos es un conjunto de técnicas establecidas, que a menudo se utilizan cuando se han desarrollado bases de datos de relaciones; por consiguiente, ¿qué significa el modelado de contenido sin encabezado de AEM?

### ¿Por qué? {#why}

Para garantizar que su aplicación pueda solicitar y recibir de forma consistente y eficiente el contenido necesario de AEM, debe estar estructurado.

Esto significa que la aplicación conoce de antemano la forma de respuesta y, por lo tanto, cómo procesarla. Esto es mucho más fácil que recibir contenido de forma libre, que debe analizarse para determinar qué contiene y, por lo tanto, cómo puede utilizarse.

### Introducción a ¿Cómo hacerlo? {#how}

AEM utiliza fragmentos de contenido para proporcionar las estructuras necesarias para la entrega sin encabezado del contenido en las aplicaciones.

La estructura del modelo de contenido:

* Se consigue mediante la definición del modelo de fragmento de contenido.
* Se utiliza como base de los fragmentos de contenido utilizados para la generación de contenido.

>[!NOTE]
>
>Los modelos de fragmento de contenido también se utilizan como base de los esquemas AEM GraphQL, que se utilizan para recuperar el contenido; más información al respecto en una sesión posterior.

Las solicitudes de contenido se realizan mediante la API de AEM, GraphQL, una implementación personalizada de la API de GraphQL estándar. La API de AEM GraphQL permite realizar consultas (complejas) en los fragmentos de contenido, y cada consulta se realiza de acuerdo con un tipo de modelo específico.

Las aplicaciones pueden utilizar el contenido devuelto.

## Creación de la estructura con modelos de fragmento de contenido {#create-structure-content-fragment-models}

Los modelos de fragmentos de contenido proporcionan varios mecanismos que le permiten definir la estructura del contenido.

Un modelo de fragmento de contenido describe una entidad.

>[!NOTE]
>Habilite la funcionalidad Fragmento de contenido en el Explorador de configuración para poder crear modelos.

>[!TIP]
>
>Se debe asignar un nombre al modelo para que el autor del contenido sepa qué modelo seleccionar al crear un fragmento de contenido.

Dentro de un modelo:

1. **Tipos de datos** le permiten definir los atributos individuales.
Por ejemplo, defina el campo que contiene el nombre de un profesor como **Texto** y sus años de servicio como un **Número**.
1. Los tipos de datos **Referencia de contenido** y **Referencia de fragmento** le permiten crear relaciones con otro contenido dentro de AEM.
1. El tipo de datos **referencia de fragmento** le permite obtener varios niveles de estructura anidando los fragmentos de contenido (según el tipo de modelo). Esto es importante para el modelado de contenido.

Por ejemplo:
![Modelado de contenido con fragmentos de contenido](assets/headless-modeling-01.png "Modelado de contenido con fragmentos de contenido")

### Tipos de datos {#data-types}

AEM proporciona los siguientes tipos de datos para modelar el contenido:

* Texto de una sola línea
* Texto de varias líneas
* Número
* Booleano
* Fecha y hora
* Lista desglosada
* Etiquetas
* Referencia de contenido
* Referencia al fragmento
* Objeto JSON

### Referencias y contenido anidado {#references-nested-content}

Dos tipos de datos proporcionan referencias al contenido fuera de un fragmento específico:

* **Referencia de contenido**
Proporciona una sencilla referencia a otro contenido de cualquier tipo.
Por ejemplo, puede hacer referencia a una imagen en una ubicación específica.

* **Referencia de fragmento**
Proporciona referencias a otros fragmentos de contenido.
Este tipo de referencia se utiliza para crear contenido anidado e introduce las relaciones necesarias para modelar el contenido.
El tipo de datos se puede configurar para que los autores de fragmentos puedan hacer lo siguiente:
   * Editar directamente el fragmento al que se hace referencia.
   * Cree un fragmento de contenido basado en el modelo adecuado.

### Creación de modelos de fragmento de contenido {#creating-content-fragment-models}

Al principio, debe habilitar Modelos de fragmento de contenido para el sitio. Esta activación se realiza en el Explorador de configuración, en Herramientas > General > Explorador de configuración. Puede seleccionar la configuración de la entrada global o crear una configuración. Por ejemplo:

![Definir configuración](assets/cfm-configuration.png)

>[!NOTE]
>
>Consulte Recursos adicionales: Fragmentos de contenido en el explorador de configuración

A continuación, se pueden crear los modelos de fragmento de contenido y definir la estructura. Esto se puede hacer en Herramientas > Assets > Modelos de fragmentos de contenido. Por ejemplo:

![Modelo de fragmento de contenido](assets/cfm-model.png)

>[!NOTE]
>
>Consulte Recursos adicionales: Modelos de fragmento de contenido.

## Uso del modelo para crear contenido con fragmentos de contenido {#use-content-to-author-content}

Los fragmentos de contenido se basan siempre en un modelo de fragmento de contenido. El modelo proporciona la estructura, el fragmento incluye el contenido.

### Selección del modelo apropiado {#select-model}

El primer paso para crear el contenido es crear un fragmento de contenido. Esto se realiza mediante Crear > Fragmento de contenido en la carpeta necesaria en Recursos > Archivos. El asistente le guiará a través de los pasos.

Un fragmento de contenido se basa en un modelo de fragmento de contenido específico que se selecciona como primer paso del proceso de creación.

### Creación y edición de contenido estructurado {#create-edit-structured-content}

Una vez creado el fragmento, puede abrirlo en el Editor de fragmentos de contenido. Aquí puede hacer lo siguiente:

* Editar el contenido en modo normal o pantalla completa.
* Dar formato al contenido como Texto completo, Texto sin formato o Markdown.
* Crear y administrar Variaciones del contenido.
* Asociar contenido.
* Editar los metadatos.
* Mostrar la estructura de árbol.
* Previsualizar la representación JSON.

### Creación de fragmentos de contenido {#creating-content-fragments}

Después de seleccionar el modelo adecuado, se abre un fragmento de contenido para editarlo en el Editor de fragmentos de contenido:

![Editor de fragmentos de contenido](assets/cfm-editor.png)

>[!NOTE]
>
>Consulte Recursos adicionales: trabajar con fragmentos de contenido.

## Introducción a algunos ejemplos {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

Para obtener una estructura básica como ejemplo, consulte La estructura del fragmento de contenido de muestra.

## Siguientes pasos {#whats-next}

Ahora que ha aprendido a modelar su estructura y a crear contenido en función de ella, el siguiente paso es [Aprender a utilizar las consultas de GraphQL para acceder al contenido de los fragmentos de contenido y recuperarlo](access-your-content.md). En esta sección se presenta y se analiza GraphQL y, a continuación, se examinan algunas consultas de ejemplo para ver cómo funcionan las cosas en la práctica.

## Recursos adicionales {#additional-resources}

* [Trabajo con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md): la página de inicio para los fragmentos de contenido.
   * [Fragmentos de contenido en el Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md): habilite la funcionalidad de fragmentos de contenido en el Explorador de configuración.
   * [Modelos de fragmentos de contenido](/help/assets/content-fragments/content-fragments-models.md): creando y editando modelos de fragmentos de contenido.
   * [Administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md): creación y creación de fragmentos de contenido; esta página le lleva a otras secciones detalladas.
* [Esquemas de AEM GraphQL](access-your-content.md): Cómo GraphQL realiza los modelos.
* [La estructura de fragmento de contenido de muestra](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Introducción a AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=es): una breve serie de tutoriales de vídeo que ofrecen información general sobre el uso de las funciones de AEM sin encabezado, incluidos el modelado de contenido y GraphQL.
   * [Conceptos básicos de modelado de GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html?lang=es): aprenda a definir y utilizar fragmentos de contenido en Adobe Experience Manager (AEM) para su uso con GraphQL.
