---
title: Andamiaje
description: A veces, es posible que tenga que crear un gran conjunto de páginas que compartan estructura pero que tengan contenido diferente. Con el andamiaje, puede crear un formulario (un andamio) con campos que reflejen la estructura que desee para sus páginas y, a continuación, utilizar este formulario para crear fácilmente páginas basadas en esta estructura.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# Andamiaje{#scaffolding}

A veces, es posible que tenga que crear un gran conjunto de páginas que compartan estructura pero que tengan contenido diferente. A través de la interfaz estándar de Adobe Experience Manager (AEM), debe crear cada página, arrastrar los componentes adecuados a la página y rellenarlos individualmente.

Con el andamiaje, puede crear un formulario (un andamio) con campos que reflejen la estructura que desee para sus páginas y, a continuación, utilizar este formulario para crear fácilmente páginas basadas en esta estructura.

>[!NOTE]
>
>El andamiaje (en la IU clásica) [respeta la herencia de MSM](#scaffolding-with-msm-inheritance).

## Cómo funciona el andamiaje {#how-scaffolding-works}

Los andamios se almacenan en la consola **Tools** del administrador del sitio.

* Abra la consola **Herramientas** y haga clic en **Andamiaje de página predeterminado**.
* En esta sección, haz clic en **Geometrixx**.
* En **Geometrixx**, encontrará una *página de andamio* llamada **Noticias**. Haga doble clic para abrir esta página.

![howscaffolds_work](assets/howscaffolds_work.png)

El andamio consiste en un formulario con un campo para cada parte de contenido que conformará la página que se va a crear y cuatro parámetros importantes a los que se accede a través de las **Propiedades de página** de la página del andamio.

![props de página](assets/pageprops.png)

Las propiedades de la página de andamiaje son:

* **Texto de título**: Este es el nombre de la página de andamiaje. En este ejemplo, se llama &quot;News&quot;.
* **Descripción**: esto aparece debajo del título en la página de andamiaje.
* **Plantilla de destino**: Esta es la plantilla que este andamio usará cuando cree una página. En este ejemplo, se trata de una plantilla *Geometrixx Content Page*.
* **Ruta de destino**: Esta es la ruta de la página principal por debajo de la cual este andamio creará páginas. En este ejemplo, la ruta es */content/geometrixx/en/news*.

El cuerpo del andamio es la forma. Cuando un usuario desea crear una página con el andamio, rellena el formulario y hace clic en *Crear*, en la parte inferior. En el ejemplo **Noticias** anterior, el formulario tiene los campos siguientes:

* **Título**: Este es el nombre de la página que se va a crear. Este campo siempre está presente en cada andamio.
* **Texto**: Este campo corresponde a un componente Texto en la página resultante.
* **Imagen**: este campo corresponde a un Componente de imagen en la página resultante.
* **Imagen/Avanzado**: **Título**: El título de la imagen.
* **Imagen/Avanzado**: **Texto alternativo**: Texto alternativo de la imagen.
* **Imagen/Avanzado**: **Descripción**: La descripción de la imagen.
* **Imagen/Avanzado**: **Tamaño**: El tamaño de la imagen.
* **Etiquetas/palabras clave**: metadatos que se asignarán a esta página. Este campo siempre está presente en cada andamio.

### Creación de un andamio {#creating-a-scaffold}

Para crear un andamio, ve a la consola **Herramientas**, luego a **Andamiaje de página predeterminado** y crea una página. Hay disponible un solo tipo de plantilla de página, *Plantilla de andamiaje.*

Vaya a **Propiedades de página** de la nueva página y establezca el *Texto de título*, la *Descripción*, la *Plantilla de destino* y la *Ruta de destino*, tal como se ha descrito anteriormente.

A continuación, debe definir la estructura de la página que creará este andamio. Para ello, vaya a **[modo de diseño](/help/sites-authoring/page-authoring.md#sidekick)** en la página del andamio. Aparece un vínculo que le permite editar el andamio en el **editor de diálogos**.

![cq5_dialog_editor](assets/cq5_dialog_editor.png)

Con el editor de diálogos, se especifican las propiedades que se crearán cada vez que se cree una nueva página con este andamio.

La definición del cuadro de diálogo de un andamio funciona de manera similar a la de un componente (consulte [Componentes](/help/sites-developing/components.md)). Sin embargo, se aplican algunas diferencias importantes:

* Las definiciones de cuadros de diálogo de componentes se representan como cuadros de diálogo normales (como se muestra en el panel central del editor de diálogos), mientras que las definiciones de cuadros de diálogo de andamios, aunque aparecen como cuadros de diálogo normales en el editor de diálogos, se representan en la página de andamio como un formulario de andamio (como se muestra en el andamio **News** anterior).
* Los cuadros de diálogo de componentes proporcionan campos solo para aquellos valores necesarios para definir el contenido de un componente específico único. Un cuadro de diálogo de andamiaje debe proporcionar campos para cada propiedad en cada párrafo de la página que se va a crear.
* Si hay cuadros de diálogo de componentes, el componente utilizado para procesar el contenido especificado está implícito y, por lo tanto, la propiedad `sling:resourceType` del párrafo se rellena automáticamente cuando se crea el párrafo. Con un andamiaje, toda la información que defina el contenido y el componente asignado para un párrafo determinado debe proporcionarla el propio cuadro de diálogo. En los cuadros de diálogo de andamiaje, esta información debe proporcionarse usando los campos *Oculto* para enviar esta información al crear la página.

Un vistazo al diálogo de andamiaje de ejemplo **News** en el editor de diálogos ayuda a explicar cómo funciona esto. Vaya al modo de diseño en la página del andamio y haga clic en el vínculo del editor de diálogos.

Ahora, haga clic en el campo de diálogo **Cuadro de diálogo > Panel de fichas > Texto > Texto**, de esta manera:

![textedit](assets/textedit.png)

La lista de propiedades de este campo aparece a la derecha del editor de diálogos, de esta manera:

![lista_de_propiedades](assets/list_of_properties.png)

Observe la propiedad name de este campo. Tiene el valor

`./jcr:content/par/text/text`

Es el nombre de la propiedad en la que se escribirá el contenido de este campo cuando se utilice el andamio para crear una página. La propiedad se indica como una ruta relativa desde el nodo que representa la página que se va a crear. Especifica el texto de la propiedad, debajo del texto del nodo, que está debajo de la parte del nodo, que es a su vez un elemento secundario del nodo jcr:content debajo del nodo de la página.

Define la ubicación del almacenamiento de contenido para el texto que se introduce en este campo. Sin embargo, también es necesario especificar dos características más para este contenido:

* El hecho de que la cadena que se está almacenando aquí debe interpretarse como *texto enriquecido*, y
* qué componente debe utilizarse para procesar este contenido en la página resultante.

En un cuadro de diálogo de componente normal no tendría que especificar esta información porque está implícita en el hecho de que el cuadro de diálogo ya está enlazado a un componente específico.

Para especificar estos dos fragmentos de información, se utilizan campos ocultos. Haga clic en el primer campo oculto **Cuadro de diálogo > Panel de fichas > Texto > Oculto**, de esta manera:

![oculto](assets/hidden.png)

Las propiedades de este campo oculto son las siguientes:

![props_lista_oculta](assets/hidden_list_props.png)

La propiedad name de este campo oculto es

`./jcr:content/par/text/textIsRich`

Esta es una propiedad booleana que se usa para interpretar la cadena de texto almacenada en `./jcr:content/par/text/text`.

Como sabemos que el texto debe interpretarse como texto enriquecido, vamos a especificar la propiedad `value` de este campo como `true`.

>[!CAUTION]
>
>El editor de diálogos permite al usuario cambiar los valores de *propiedades existentes* en la definición del diálogo. Para agregar una nueva propiedad, el usuario debe usar [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md). Por ejemplo, cuando se agrega un nuevo campo oculto a una definición de diálogo con el editor de diálogos, no tiene una propiedad *value* (es decir, una propiedad con el nombre &quot;value&quot;). Si el campo oculto en cuestión requiere que se establezca una propiedad de valor predeterminada, esta propiedad debe agregarse manualmente con una de las herramientas de CRX. El valor no se puede agregar con el propio editor de diálogos. Sin embargo, una vez que la propiedad está presente, su valor se puede editar con el editor de diálogos.

El segundo campo oculto se puede ver haciendo clic en él de esta manera:

![oculto2](assets/hidden2.png)

Las propiedades de este campo oculto son las siguientes:

![hidden_list_props2](assets/hidden_list_props2.png)

La propiedad name de este campo oculto es

`./jcr:content/par/text/sling:resourceType`

Y el valor fijo especificado para esta propiedad es

`foundation/components/textimage`

Esto especifica que el componente que se utilizará para procesar el contenido de texto de este párrafo es el componente *Imagen de texto*. Usando con el booleano `isRichText` especificado en el otro campo oculto, el componente puede procesar la cadena de texto real almacenada en `./jcr:content/par/text/text` de la manera deseada.

### Andamiaje con herencia MSM {#scaffolding-with-msm-inheritance}

En la IU clásica, el andamiaje está totalmente integrado con la herencia de MSM (cuando corresponda).

Al abrir una página en modo **Andamiaje** (con el icono de la parte inferior de la barra de tareas), los componentes sujetos a herencia se indicarán de la siguiente manera:

* un símbolo de bloqueo (para la mayoría de los componentes; por ejemplo, Texto y Título)
* una máscara con el texto **Haga clic para cancelar la herencia** (para componentes de imagen)

Estos muestran que el componente no se puede editar hasta que se cancele la herencia.

![chlimage_1](assets/chlimage_1.jpeg)

>[!NOTE]
>
>Esto es comparable a [componentes heredados al editar contenido de página](/help/sites-authoring/editing-content.md#inheritedcomponentsclassicui).

Al hacer clic en el símbolo de bloqueo o en el icono de imagen, puede interrumpir la herencia:

* el símbolo cambia a un candado abierto.
* una vez desbloqueado, puede editar el contenido.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

Después de desbloquear, puede restaurar la herencia haciendo clic en el símbolo de candado desbloqueado: esto perderá las ediciones que haya realizado.

>[!NOTE]
>
>Si la herencia se cancela en el nivel de página (desde la pestaña Livecopy de Propiedades de página), todos los componentes se pueden editar en el modo **Andamiaje** (se muestran en estado desbloqueado).
