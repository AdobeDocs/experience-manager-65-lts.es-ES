---
title: Estructura de la IU táctil de Adobe Experience Manager
description: La IU táctil optimizada, tal como se implementa en Adobe Experience Manager, tiene varios principios subyacentes y se compone de varios elementos clave
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---

# Estructura de la IU táctil de Adobe Experience Manager{#structure-of-the-aem-touch-enabled-ui}

La IU táctil de Adobe Experience Manager (AEM) tiene varios principios subyacentes y consta de varios elementos clave:

## Consolas {#consoles}

### Diseño básico y cambio de tamaño {#basic-layout-and-resizing}

La interfaz de usuario se adapta tanto a dispositivos móviles como de escritorio, aunque en lugar de crear dos estilos, Adobe ha decidido utilizar un estilo que funcione para todas las pantallas y dispositivos.

Todos los módulos utilizan el mismo diseño básico. En AEM, esto puede considerarse como:

![chlimage_1-142](assets/chlimage_1-142.png)

El diseño se adhiere a un estilo de diseño interactivo y se adaptará al tamaño del dispositivo o la ventana que utilice.

Por ejemplo, cuando la resolución es inferior a 1024 píxeles (como en un dispositivo móvil), la pantalla se ajusta en consecuencia:

![chlimage_1-143](assets/chlimage_1-143.png)

### Barra de encabezado {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

La barra de encabezado muestra elementos globales como:

* el logotipo y el producto/solución específico que esté utilizando; para AEM, esto también forma un vínculo a la navegación global
* Búsqueda
* icono para acceder a los recursos de ayuda
* para acceder a otras soluciones
* un indicador de (y acceso a) cualquier alerta o elemento de la Bandeja de entrada que le esté esperando
* el icono de usuario, junto con un vínculo a la administración de perfiles

### Barra de herramientas {#toolbar}

Esto es contextual para la ubicación y las herramientas de superficie relevantes para controlar la vista o los recursos en la página siguiente. La barra de herramientas es específica del producto, pero los elementos tienen algunas características comunes.

En cualquier ubicación, la barra de herramientas muestra las acciones disponibles actualmente:

![chlimage_1-145](assets/chlimage_1-145.png)

También depende de si se selecciona un recurso:

![chlimage_1-146](assets/chlimage_1-146.png)

### Carril izquierdo {#left-rail}

El carril izquierdo se puede abrir u ocultar según sea necesario para mostrar:

* **Cronología**
* **Referencias**
* **Filtro**

El valor predeterminado es **Solo contenido** (carril oculto).

![chlimage_1-147](assets/chlimage_1-147.png)

## Creación de páginas {#page-authoring}

Al crear páginas, las áreas estructurales son las siguientes.

### Marco de contenido {#content-frame}

El contenido de la página se representa en el marco de contenido. El marco de contenido es independiente del editor para garantizar que no haya conflictos debido a CSS o JavaScript.

El marco de contenido se encuentra en la sección derecha de la ventana, debajo de la barra de herramientas.

![chlimage_1-148](assets/chlimage_1-148.png)

### Marco del editor {#editor-frame}

El marco del editor realiza las funciones de edición.

El marco del editor es un contenedor (abstracto) para todos los *elementos de creación de páginas*. Se encuentra sobre el marco de contenido e incluye:

* la barra de herramientas superior
* el panel lateral
* todas las superposiciones
* cualquier otro elemento de creación de página; por ejemplo, la barra de herramientas de componentes

![chlimage_1-149](assets/chlimage_1-149.png)

### Panel lateral {#side-panel}

Contiene dos pestañas predeterminadas que permiten seleccionar recursos y componentes. Se pueden arrastrar desde aquí y soltar en la página.

El panel lateral está oculto de forma predeterminada. Cuando se selecciona, se muestra en el lado izquierdo o se desliza para cubrir toda la ventana (cuando el tamaño de la ventana es inferior a una anchura de 1024 píxeles; como, por ejemplo, en un dispositivo móvil).

![chlimage_1-150](assets/chlimage_1-150.png)

### Panel lateral: Assets {#side-panel-assets}

En la pestaña Assets puede seleccionar entre los distintos recursos. También puede filtrar por un término específico o seleccionar un grupo.

![chlimage_1-151](assets/chlimage_1-151.png)

### Panel lateral: Grupos de recursos {#side-panel-asset-groups}

En la pestaña Recurso, hay una lista desplegable que puede utilizar para seleccionar los grupos de recursos específicos.

![chlimage_1-152](assets/chlimage_1-152.png)

### Panel lateral: Componentes {#side-panel-components}

En la pestaña Componentes, puede seleccionar entre el rango de componentes. También puede filtrar por un término específico o seleccionar un grupo.

![chlimage_1-153](assets/chlimage_1-153.png)

### Superposiciones {#overlays}

Se superponen en el marco de contenido y las [capas](#layer) las utilizan para comprender la mecánica de cómo puede interactuar (de forma transparente) con los componentes y su contenido.

Las superposiciones se encuentran en el marco del editor (con todos los demás elementos de creación de páginas), aunque en realidad se superponen a los componentes adecuados en el marco de contenido.

![chlimage_1-154](assets/chlimage_1-154.png)

### Capa {#layer}

Una capa es un paquete independiente de funciones que se puede activar para:

* proporcionar una vista diferente de la página
* le permite manipular o interactuar con una página

Las capas proporcionan una funcionalidad sofisticada para toda la página, en lugar de acciones específicas en un componente individual.

AEM incluye varias capas ya implementadas para la creación de páginas; por ejemplo, editar, previsualizar y anotar.

>[!NOTE]
>
>Las capas son un concepto potente que afecta a la vista del usuario y a la interacción con el contenido de la página. Al desarrollar sus propias capas, debe asegurarse de que la capa se limpia cuando se sale de ella.

### Conmutador de capas {#layer-switcher}

El selector de capas le permite elegir la capa que desea utilizar. Cuando se cierra, indica la capa que se está utilizando en ese momento.

El selector de capas está disponible como una lista desplegable en la barra de herramientas (en la parte superior de la ventana, dentro del marco del editor).

![chlimage_1-155](assets/chlimage_1-155.png)

### Barra de herramientas del componente {#component-toolbar}

Cada instancia de un componente muestra su barra de herramientas cuando se hace clic (una vez o con un doble clic lento). La barra de herramientas contiene las acciones específicas (por ejemplo, copiar, pegar, abrir editor) disponibles para la instancia de componente (Editable) en la página.

Según el espacio disponible, las barras de herramientas de los componentes se colocan en la esquina superior o inferior derecha del componente correspondiente.

![chlimage_1-156](assets/chlimage_1-156.png)

## Información adicional {#further-information}

Para obtener más información sobre los conceptos relacionados con la IU táctil, lee [Conceptos de la IU táctil de AEM](/help/sites-developing/touch-ui-concepts.md).

Para obtener más información técnica, consulte [Conjunto de documentación de JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html) para el editor de páginas táctil.
