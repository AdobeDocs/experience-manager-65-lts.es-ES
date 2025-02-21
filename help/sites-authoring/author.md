---
title: Creación
description: Conceptos sobre creación y publicación en Adobe Experience Manager 6.5.
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: d1297182b801ff4db163b8ae91332f5aebb94b9b
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 32%

---

# Creación{#authoring}

## Concepto de creación (y publicación) {#concept-of-authoring-and-publishing}

AEM le proporciona dos entornos:

* Autor
* Publicación

Interactúan para permitirle ofrecer contenido en su sitio web, de modo que los visitantes puedan leerlo.

El entorno de creación ofrece mecanismos para crear, actualizar y revisar el contenido antes de publicarlo:

* Un autor crea y revisa el contenido (que puede ser de varios tipos; por ejemplo, páginas, recursos, publicaciones, etc.)
* que, en algún momento, se publicará en su sitio web.

![Información general de entornos](assets/chlimage_1-132.png)

En el entorno de creación, la funcionalidad de AEM está disponible a través de dos interfaces de usuario. Desde el entorno de publicación se diseña todo el aspecto y funcionamiento de la interfaz de usuario.

### Entorno de creación {#author-environment}

El autor trabaja en lo que se conoce como **entorno de creación**. Esto proporciona una interfaz fácil de usar (interfaz gráfica de usuario (GUI o IU)) para crear el contenido. Se encuentra detrás del cortafuegos de una empresa que proporciona protección total y requiere que el autor inicie sesión con una cuenta a la que se le hayan asignado los derechos de acceso correspondientes.

>[!NOTE]
>
>Su cuenta necesita los derechos de acceso adecuados para crear, editar o publicar contenido.

Según la configuración de su instancia y sus derechos de acceso personales, puede realizar muchas tareas con el contenido, incluidas (entre otras):

* generar contenido nuevo o editar contenido existente en una página
* usar plantillas predefinidas para crear páginas de contenido nuevo
* crear, editar y administrar sus recursos y colecciones
* crear, editar y administrar sus publicaciones
* desarrolle sus campañas y los recursos relacionados
* mover, copiar o eliminar páginas de contenido, recursos, etc
* publicar (o cancelar la publicación) de páginas, recursos, etc

Además, hay tareas administrativas que le ayudan a administrar su contenido:

* flujos de trabajo que controlan cómo se administran los cambios; por ejemplo, aplicar una revisión antes de la publicación
* proyectos que coordinan tareas individuales

>[!NOTE]
>
>AEM también está [administrado](/help/sites-administering/home.md) (para la mayoría de las tareas) desde el entorno de creación.

#### Entorno de publicación {#publish-environment}

Cuando esté listo, el contenido del sitio de AEM se publicará en el **entorno de publicación**. Aquí las páginas del sitio web se ponen a disposición de la audiencia objetivo de acuerdo con la apariencia de la interfaz diseñada.

Por lo general, el entorno de publicación se encuentra dentro de la zona desmilitarizada; es decir, disponible para Internet, pero ya no bajo la plena protección de la red interna.

>[!NOTE]
>
>Lamentablemente, a veces se produce una superposición en la terminología utilizada. Esto puede ocurrir con:
>
>* **Publicar o cancelar la publicación**
>  Estos son los términos principales de las acciones que harán que el contenido esté disponible o no para los visitantes en su entorno de publicación.
>
>* **Activar o desactivar**
>  Estos términos son sinónimos de publicar y cancelar la publicación.
>
>* **Replicar o replicación**
>  Son los términos técnicos utilizados para indicar el movimiento de datos (por ejemplo, contenido de página, archivos, código, comentarios del usuario) de un entorno a otro; es decir, al publicar o replicar de forma inversa los comentarios del usuario.
>

#### Dispatcher {#dispatcher}

Para optimizar el rendimiento de los visitantes de tu sitio web, **[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es)** implementa almacenamiento en caché y equilibrio de carga.
