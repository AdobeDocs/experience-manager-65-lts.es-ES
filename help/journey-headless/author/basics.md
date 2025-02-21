---
title: Información sobre conceptos básicos de creación
description: Obtenga información sobre los conceptos y la mecánica de creación de contenido para su CMS sin encabezado mediante Fragmentos de contenido.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 75%

---

# Conceptos básicos de creación para usuarios sin encabezado con AEM {#author-headless-basics}

## La historia hasta ahora {#story-so-far}

Al principio del [recorrido del autor de contenido de AEM sin encabezado](overview.md), en la [introducción](introduction.md) se han abordado los conceptos básicos y la terminología relevante para la creación sin encabezado.

Este artículo se basa en estos elementos para que pueda comprender cómo crear su propio contenido para su proyecto de AEM sin encabezado.

## Objetivo {#objective}

* **Audiencia**: principiante
* **Objetivo**: presentar los conceptos básicos de la creación de CMS sin encabezado.
   * Introducción a la creación con AEMaaCS.
   * Introducción a los fragmentos de contenido.

## Gestión básica {#basic-handling}

Antes de comprender los fragmentos de contenido, aquí tiene una muy rápida introducción al uso de AEM.Aunque nada sustituye realmente la experiencia de iniciar sesión e intentar utilizar el sistema.

### Autor y publicación {#author-preview-publish}

Una instalación de AEM generalmente consta de al menos dos entornos:

* Autor
* Publicación

Inicie sesión y utilice el entorno de creación para generar su contenido. Cuando esté listo, publíquelo para que esté disponible para el público en general. Para el contenido sin encabezado, esto sería para otras aplicaciones, para páginas web sería para los lectores de la web.

Para obtener más información, consulte Conceptos de creación.

### Inicio de sesión {#signing-in}

Al igual que con la mayoría de los sistemas, debe iniciar sesión. Como autor, se le proporcionará lo siguiente:

* Un nombre de usuario o de cuenta
* Una contraseña
* Un vínculo para acceder a la pantalla de inicio de sesión

Su cuenta se habrá configurado con los privilegios que necesite. Si tiene algún problema, recomendamos que se ponga en contacto con su equipo de soporte interno del proyecto.

### Navegación {#navigation}

La primera vez que inicie sesión, un breve tutorial en línea resalta algunas de las funciones principales de la interfaz de usuario.

A continuación, puede utilizar el panel de navegación para acceder a las áreas clave de AEM. Para los fragmentos de contenido usará la **consola de Assets**.

El panel de navegación se puede abrir seleccionando el icono Adobe en la parte superior izquierda, seguido del icono de una pequeña brújula:

![Panel de navegación](/help/journey-headless/author/assets/headless-journey-author-navigation-01.png)

>[!NOTE]
>Aunque los fragmentos de contenido son una característica de AEM **Sites**, se encuentran en la consola **Assets**. Se trata de un detalle técnico que no debería afectarle, pero que es útil conocer.

En la consola, puede seleccionar carpetas para desplazarse hasta el fragmento de contenido o las rutas de exploración (en el encabezado) para desplazarse hacia atrás en el árbol.

![Rutas de exploración](/help/journey-headless/author/assets/headless-journey-author-navigation-02.png)

### Acciones: selección y visualización {#actions-selecting-viewing}

La consola **Assets** tiene **barras de herramientas de acción** y **acciones rápidas** dedicadas que puede usar después de seleccionar un recurso (por ejemplo, una carpeta o un fragmento de contenido).

Las Acciones rápidas están disponibles para un único recurso, consulte **Basilea** en el ejemplo siguiente:

![Acciones rápidas](/help/journey-headless/author/assets/headless-journey-author-navigation-05.png)

La barra de herramientas de acciones proporciona acceso a toda la gama de acciones, aplicables al escenario actual. Las acciones disponibles pueden cambiar, por ejemplo, en función de su ubicación o de si ha seleccionado varios recursos:

![Barra de herramientas de acciones](/help/journey-headless/author/assets/headless-journey-author-navigation-06.png)

Puede seleccionar el formato para ver los recursos con el Selector de vista:

![Selector de vista](/help/journey-headless/author/assets/headless-journey-author-navigation-03.png)

Puede ver información adicional sobre los elementos mediante el Selector de carril. Esto también proporciona acceso a acciones adicionales.

![Carril Izquierdo](/help/journey-headless/author/assets/headless-journey-author-navigation-04.png)

## Creación de fragmentos de contenido {#authoring-content-fragments}

Esta ha sido una introducción muy rápida a la interfaz de usuario (IU) de AEM, esperamos que haya tenido la oportunidad de probarla. Ahora llegamos a lo que realmente le interesa: los fragmentos de contenido sin encabezado.

Tendremos que revisar las cosas de principio a fin, pero es posible que su instancia ya tenga carpetas o fragmentos creados, y que estos se encuentren en diferentes ubicaciones. Los principios son los mismos.

### Organización y navegación {#organizing-and-navigating}

A menos que tenga muy pocos fragmentos de contenido, querrá organizarlos para que usted (y otros) puedan volver a encontrarlos.

#### Creación de una carpeta {#creating-folder}

Puede hacerlo creando una serie de carpetas en la sección **Files** de la consola de Assets. Seleccione la opción **Crear** (parte superior derecha), seguido de **Carpeta**:

![Opción Crear carpeta](/help/journey-headless/author/assets/headless-journey-author-folder-01.png)

Se abre un cuadro de diálogo en el que puede escribir los detalles y confirmarlos con **Crear**:

![Cuadro de diálogo Crear carpeta](/help/journey-headless/author/assets/headless-journey-author-folder-02.png)

#### Uso de rutas y etiquetas para limitar los modelos de fragmento de contenido disponibles en la carpeta {#tags-paths-for-models-in-folder}

Esta sección es un poco más avanzada. Realmente no lo necesita si acaba de empezar y probar cosas, pero es más útil cuando tiene muchos fragmentos. Así que es bueno conocerla, aunque todavía no la utilice.

El arquitecto de contenido habrá creado todos los modelos de fragmento de contenido necesarios para el proyecto actual y tal vez también otros proyectos. Para simplificarle las cosas a usted y a otros autores, puede limitar la lista de modelos disponibles para una carpeta específica.

Tras crear la carpeta, puede abrir la carpeta **Propiedades**. Aquí hay varias pestañas con información y detalles de configuración sobre la carpeta. En concreto, para los fragmentos de contenido, puede usar la pestaña **Políticas** para definir rutas y etiquetas específicas para esta carpeta. Esto limita los modelos de fragmento de contenido disponibles para su uso en la carpeta, ya que significa que los modelos de fragmento de contenido deben cumplir estos requisitos antes de poder utilizarse para generar fragmentos en esta carpeta.

![Crear propiedades de carpeta: políticas](/help/journey-headless/author/assets/headless-journey-author-folder-04.png)

>[!NOTE]
>
>Puede leer más detalles en Modelos de fragmento de contenido: permitir modelos de fragmento de contenido en la carpeta Recursos.

A continuación, desplácese por estas carpetas para crear y editar los fragmentos de contenido.

#### Por si acaso: configuración de la carpeta de Cloud Services {#cloud-services-folder}

Por si acaso...

Probablemente, se le dará una carpeta inicial donde podrá crear sus carpetas. Así es como deben aplicarse algunos detalles de configuración (normalmente por un desarrollador o administrador del sistema) a la carpeta raíz. Probablemente no le interese, pero si es necesario, puede comprobar la **configuración** en **Cloud Services** de la carpeta **Properties**:

![Propiedades de Crear carpeta: configuración](/help/journey-headless/author/assets/headless-journey-author-folder-03.png)

>[!NOTE]
>
>Puede obtener más información en Aplicar la configuración a la carpeta Recursos.

### Creación de un fragmento de contenido {#creating-fragment}

La creación de un fragmento de contenido es muy similar: solo tiene que usar la opción **Fragmento de contenido**:

![Opción Crear fragmento de contenido](/help/journey-headless/author/assets/headless-journey-author-content-fragment-01.png)

Esta vez se abre un asistente. El primer paso es seleccionar el Modelo de fragmento de contenido en el que se basará el fragmento:

![Crear fragmento de contenido - seleccionar modelo](/help/journey-headless/author/assets/headless-journey-author-content-fragment-02.png)

Después de continuar con **Siguiente**, puedes proporcionar los detalles (**Básico** y **Avanzado**) para tu fragmento:

![Crear fragmento de contenido: proporcionar nombre](/help/journey-headless/author/assets/headless-journey-author-content-fragment-03.png)

Confirma con **Crear** y podrás **abrir** tu fragmento en el editor.

### Edición de un fragmento {#editing-fragment}

Puede abrir un fragmento inmediatamente después de crearlo o seleccionarlo en la consola de Assets.

Cuando se abra el editor por primera vez, verá lo siguiente:

* Una lista de iconos en el lado izquierdo: esto le permite acceder a varias áreas de funcionalidad. El editor se abre en la pestaña **Variaciones**, que es donde se produce la mayor parte de la edición. También puede estar interesado en las pestañas **Anotaciones** y **Metadatos**.

* Un encabezado con información sobre el fragmento con acceso a varias acciones.

* El área de edición principal: esto depende del modelo utilizado para crear el fragmento.

Ejemplos:

* Un fragmento que solo requiere múltiples informaciones, algunas con un tipo específico. Para el contenido sin encabezado, las referencias son clave; más adelante, en el recorrido, aprenderá sobre ellas.

  ![Editor de fragmentos de contenido: mi fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-04.png)

* Un fragmento que le permite escribir una sección larga de texto. Aquí hay opciones adicionales para administrar y dar formato al texto. Incluso puede abrir los campos de texto individuales en un editor de pantalla completa (con el icono en forma de pantalla pequeña de la derecha)

  ![Editor de fragmentos de contenido: Alaska Spirits](/help/journey-headless/author/assets/headless-journey-author-content-fragment-05.png)

>[!NOTE]
>
>Es posible que se requiera documentación específica del proyecto para ayudar a los autores con detalles sobre cómo completar correctamente algunos campos.
>
>Consulte Modelos de fragmentos de contenido: tipos de datos y propiedades para obtener detalles genéricos.

Confirme las actualizaciones con: **Guardar** o **Guardar y cerrar**.

>[!NOTE]
>
>Para obtener más información, puede leer Variaciones: creación de fragmentos de contenido.

#### Lo que (probablemente) no debe preocuparle {#what-you-probably-do-not-need-to-worry-about}

De acuerdo. Esta sección puede parecer un poco extraña, pero cuando abra el Editor de fragmentos de contenido y empiece a explorar, aparecerán varias opciones que no se aplican a su recorrido sin encabezado (probablemente) como Autor de contenido. Así que esto es tan solo un rápido avance de lo que debe ignorar en un contexto sin encabezado.

* **Modelos de fragmentos de contenido**

  Aparecerá el nombre del modelo de fragmento de contenido en la parte superior del editor, directamente debajo del nombre del fragmento. También se trata de un vínculo que conduce al editor de modelos.
Los modelos de fragmento de contenido son vitales para los fragmentos de contenido, ya que definen la estructura que se utiliza. Sin embargo, crearlos y editarlos es, normalmente, responsabilidad de otra persona, el arquitecto de contenido.

  >[!NOTE]
  >
  >Para obtener más información, puede leer el Recorrido para arquitectos de contenido sin encabezado de AEM.

* **Contenido asociado**

  Este es bastante obvio, ya que es una pestaña en el editor.

  Los fragmentos de contenido han estado disponibles en AEM desde hace ya varias versiones. En un principio, se pusieron a disposición para el uso “tradicional” cuando se creaban páginas.Se siguen utilizando en este contexto. Esto puede implicar la asociación de recursos (por ejemplo, imágenes) que, aunque no estén incrustados en el fragmento, deben estar disponibles para el autor al crear una página.

* **Vista previa**

  Esta es otra pestaña del editor y proporciona una vista técnica, destinada principalmente a los desarrolladores.

* **Actualizar referencias de página**

  Esta acción está disponible en el menú desplegable **...** (puntos suspensivos). No tiene interés para los autores sin encabezado, ya que está relacionado con la creación de páginas.

### Publicación {#publishing}

<!-- needs more details -->

Una vez completado el fragmento, puede **Publicarlo** para que esté disponible para las aplicaciones sin encabezado.

Las acciones de publicación están disponibles en el editor (o en la barra de herramientas de la consola **Assets**):

![Editor de fragmentos de contenido: mi fragmento](/help/journey-headless/author/assets/headless-journey-author-content-fragment-06.png)

## Siguientes pasos {#whats-next}

Ahora que ha aprendido lo básico, el siguiente paso es [Obtener información sobre las referencias](references.md). Se presentarán y explicarán las distintas referencias disponibles, y cómo crear niveles de estructura con las referencias de fragmento, una parte clave de la creación sin encabezado.

## Recursos adicionales {#additional-resources}

* [Conceptos de creación](/help/sites-authoring/author.md)

* [Gestión básica](/help/sites-authoring/basic-handling.md): esta página se basa principalmente en la consola **Sites**, pero la mayoría de funciones también son relevantes para la creación de los **Fragmentos de contenido** debajo de la consola **Recursos**.

   * [Panel de navegación](/help/sites-authoring/basic-handling.md#navigation-panel)

   * [Encabezado](/help/sites-authoring/basic-handling.md#the-header)

   * [Barra de herramientas de acciones](/help/sites-authoring/basic-handling.md#actions-toolbar)

   * [Acciones rápidas](/help/sites-authoring/basic-handling.md#quick-actions)

   * [Visualización y selección de los recursos](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)

   * [Selector de carril](/help/sites-authoring/basic-handling.md#rail-selector)

* [Trabajar con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)

   * [Administración de los fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md)

      * [Aplicación de la configuración a la carpeta Recursos](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Creación de un fragmento de contenido](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Variaciones: creación de fragmentos de contenido](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)

      * [Modelos de fragmento de contenido: tipos de datos](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modelos de fragmento de contenido: propiedades](/help/assets/content-fragments/content-fragments-models.md#properties)

      * [Modelos de fragmento de contenido: permitir modelos de fragmento de contenido en la carpeta de recursos](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

* Guías de introducción
   * [Guía de inicio rápido Creación de una carpeta de Assets sin encabezado](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [Recorrido para arquitectos de contenido sin encabezado de AEM](/help/journey-headless/architect/overview.md)

* [Recorrido de traducción de AEM sin encabezado](/help/journey-headless/translation/overview.md)
