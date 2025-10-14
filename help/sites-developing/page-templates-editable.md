---
title: 'Plantillas de página: editables'
description: Se han introducido plantillas editables que permiten a los usuarios que no son desarrolladores crear y editar plantillas, proporcionar plantillas que mantengan una conexión dinámica con cualquier página creada a partir de ellas y hacer que el componente de página sea más genérico
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: cfa055e7f7e51133129f918f31b48f246927cfcf
workflow-type: tm+mt
source-wordcount: '2981'
ht-degree: 5%

---

# Plantillas de página: editables {#page-templates-editable}

Las plantillas editables se han introducido en:

* Permitir que los autores especializados [creen y editen plantillas](/help/sites-authoring/templates.md).

   * Estos autores especializados se denominan **autores de plantillas**
   * Los autores de plantillas deben ser miembros del grupo `template-authors`.

* Proporcione plantillas que mantengan una conexión dinámica con cualquier página creada a partir de ellas. Al hacerlo, se asegura de que los cambios realizados en la plantilla se reflejen en las propias páginas.
* Hacer que el componente de página sea más genérico para que el componente de página principal se pueda utilizar sin personalización.

Con las plantillas editables, las partes que componen una página están aisladas dentro de los componentes. Puede configurar las combinaciones necesarias de componentes en una interfaz de usuario para que no sea necesario desarrollar un nuevo componente de página para cada variación de página.

Este documento:

* Ofrece información general sobre la creación de plantillas editables

   * Para obtener más información, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md)

* Describe las tareas de administrador/desarrollador necesarias para crear plantillas editables
* Describe los fundamentos técnicos de las plantillas editables

Este documento supone que ya está familiarizado con la creación y edición de plantillas. Consulte el documento de creación [Creación de plantillas de página](/help/sites-authoring/templates.md), que detalla las capacidades de las plantillas editables tal como se exponen al autor de la plantilla.

>[!NOTE]
>
>El siguiente tutorial también puede ser de interés para configurar una plantilla de página editable en un nuevo proyecto:
>[Introducción a AEM Sites, parte 2: Creación de una página base y una plantilla](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/project-archetype/pages-templates.html?lang=es)

## Creación de una nueva plantilla {#creating-a-new-template}

La creación de plantillas editables se realiza principalmente con la [consola y el editor de plantillas](/help/sites-authoring/templates.md) por un autor de plantillas. En esta sección se ofrece una descripción general de este proceso y se incluye una descripción de lo que sucede a nivel técnico.

Para obtener información sobre cómo usar plantillas editables en un proyecto de AEM, consulte [Creación de un proyecto de AEM con Lazybones](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/create-aem-project-structure-using-lazybones/m-p/186478?profile.language=es).

Al crear una plantilla editable, debe hacer lo siguiente:

1. Crear una [carpeta para las plantillas](#template-folders). Esta carpeta no es obligatoria, pero se recomienda como práctica recomendada.
1. Seleccione un [tipo de plantilla](#template-type). Este tipo se copia para crear la [definición de plantilla](#template-definitions).

   >[!NOTE]
   >
   >Se proporciona una selección de tipos de plantillas listas para usarse. También puede [crear sus propios tipos de plantilla específicos del sitio](/help/sites-developing/page-templates-editable.md#creating-template-types), si es necesario.

1. Configure la estructura, las políticas de contenido, el contenido inicial y el diseño de la nueva plantilla.

   **Estructura**

   * La estructura permite definir los componentes y el contenido de la plantilla.
   * Los componentes definidos en la estructura de la plantilla no se pueden mover a una página resultante ni eliminar de ninguna página resultante.

      * Si está creando una plantilla en una carpeta personalizada fuera del contenido de muestra de `We.Retail`, puede elegir Componentes básicos o utilizar [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=es).

   * Si desea que los autores de páginas puedan añadir y quitar componentes, agregue un sistema de párrafos a la plantilla.
   * Los componentes se pueden volver a desbloquear y bloquear para que pueda definir el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de la estructura, consulte [Estructura](/help/sites-developing/page-templates-editable.md#structure) en este documento.

   **Políticas**

   * Las políticas de contenido definen las propiedades de diseño de un componente.

      * Por ejemplo, los componentes disponibles o las dimensiones mínimas/máximas.

   * Estas políticas se aplican a la plantilla (y a las páginas creadas con la plantilla).

   Para obtener más información sobre cómo define las directivas un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

   Para obtener detalles técnicos de las directivas, consulte [Políticas de contenido](/help/sites-developing/page-templates-editable.md#content-policies) en este documento.

   **Contenido inicial**

   * Contenido inicial define el contenido que aparece cuando se crea una página por primera vez en función de la plantilla.
   * Los autores de la página pueden editar el contenido inicial.

   Para obtener más información sobre cómo define la estructura un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-initial-content-author).

   Para obtener detalles técnicos sobre el contenido inicial, consulte [Contenido inicial](/help/sites-developing/page-templates-editable.md#initial-content) en este documento.

   **Diseño**

   * Puede definir el diseño de la plantilla para una amplia gama de dispositivos.
   * El diseño interactivo para las plantillas funciona igual que para la creación de páginas.

   Para obtener más información sobre cómo define el diseño de la plantilla un autor de plantillas, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#editing-a-template-layout-template-author).

   Para obtener detalles técnicos sobre el diseño de la plantilla, consulte [Diseño](/help/sites-developing/page-templates-editable.md#layout) en este documento.

1. Habilite la plantilla y déjela para árboles de contenido específicos.

   * Una plantilla se puede habilitar o deshabilitar para que esté disponible o no disponible para los autores de páginas.
   * Una plantilla puede estar disponible o no disponible para determinadas ramas de la página.

   Para obtener más información sobre cómo un autor de plantillas habilita una plantilla, consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#enabling-and-allowing-a-template-template-author).

   Para obtener detalles técnicos sobre cómo habilitar una plantilla, consulte [Habilitar y permitir una plantilla](/help/sites-developing/page-templates-editable.md#enabling-and-allowing-a-template-for-use)e en este documento

1. Úselo para crear páginas de contenido.

   * Cuando se utiliza una plantilla para crear una página, no hay ninguna diferencia visible ni indicación entre las plantillas estáticas y editables.
   * Para el autor de la página, el proceso es transparente.

   Para obtener más información sobre cómo un autor de páginas usa plantillas para crear una página, consulte [Creación y organización de páginas](/help/sites-authoring/managing-pages.md#templates).

   Para obtener detalles técnicos sobre la creación de páginas con plantillas editables, consulte [Páginas de contenido resultante](/help/sites-developing/page-templates-editable.md#resultant-content-pages) en este documento.

>[!TIP]
>
>Nunca introduzca en una plantilla información que deba internacionalizarse. Para fines de internalización, se recomienda la característica de localización [de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html?lang=es).

>[!NOTE]
>
>Las plantillas son herramientas útiles para optimizar el flujo de trabajo de creación de páginas. Sin embargo, demasiadas plantillas pueden saturar a los autores y hacer que la creación de páginas sea confusa. Una buena regla general es mantener el número de plantillas por debajo de 100.
>
>Adobe no recomienda tener más de 1000 plantillas debido a posibles impactos en el rendimiento.

>[!NOTE]
>
>La biblioteca de cliente del editor supone la presencia del área de nombres `cq.shared` en las páginas de contenido. Si está ausente, se produce el error de JavaScript `Uncaught TypeError: Cannot read property 'shared' of undefined`.
>
>Todas las páginas de contenido de muestra contienen `cq.shared`, por lo que cualquier contenido basado en ellas incluye automáticamente `cq.shared`. Sin embargo, si decide crear sus propias páginas de contenido desde cero sin basarlas en contenido de ejemplo, debe asegurarse de incluir el área de nombres `cq.shared`.
>
>Consulte [Uso de bibliotecas del lado del cliente](/help/sites-developing/clientlibs.md) para obtener más información.

## Carpetas de plantilla {#template-folders}

Para organizar las plantillas, puede utilizar las siguientes carpetas:

* **global**
* Específico del sitio
Las carpetas específicas del sitio que cree para organizar las plantillas se crean con una cuenta que contiene privilegios de administrador.

>[!NOTE]
>
>Aunque puede anidar las carpetas, cuando el usuario las vea en la consola **Templates**, se presentarán como una estructura plana.

En una instancia estándar de AEM, la carpeta **global** existe en la consola de plantillas. Esta carpeta contiene plantillas predeterminadas y actúa como alternativa si no se encuentran directivas ni tipos de plantilla en la carpeta actual. Puede agregar las plantillas predeterminadas a esta carpeta o crear una carpeta (recomendado).

>[!NOTE]
>
>Se recomienda crear una carpeta que contenga las plantillas personalizadas y no utilizar la carpeta global.

>[!CAUTION]
>
>Las carpetas debe crearlas un usuario con `admin` derechos.

Los tipos de plantilla y las directivas se heredan en todas las carpetas según el siguiente orden de prioridad:

1. La carpeta actual.
1. Principal o principal de la carpeta actual.
1. `/conf/global`
1. `/apps`
1. `/libs`

Se crea una lista de todas las entradas permitidas. Si alguna configuración se superpone ( `path`/ `label`), solo se presenta al usuario la instancia más cercana a la carpeta actual.

Para crear una carpeta, haga lo siguiente:

* Mediante programación o con CRXDE Lite
* Uso del explorador de configuración

## Uso del CRXDE Lite {#using-crxde-lite}

1. Se puede crear una nueva carpeta (en /conf) para su instancia mediante programación o con CRXDE Lite.

   Se debe utilizar la siguiente estructura:

   ```xml
   /conf
       <your-folder-name> [sling:Folder]
           settings [sling:Folder]
               wcm [cq:Page]
                   templates [cq:Page]
                   policies [cq:Page]
   ```

1. A continuación, puede definir las siguientes propiedades en el nodo raíz de la carpeta:

   `<your-folder-name> [sling:Folder]`

   Nombre: `jcr:title`

   * Tipo: `String`

   * Valor: título (de la carpeta) que desea que aparezca en la consola **Plantillas**.

1. En *adición* a los permisos y privilegios de creación estándar (por ejemplo, `content-authors`), asigne grupos y defina los derechos de acceso (ACL) requeridos para que sus autores puedan crear plantillas en la nueva carpeta.

   El grupo `template-authors` es el grupo predeterminado que se debe asignar. Consulte la siguiente sección [ACL y grupos](/help/sites-developing/page-templates-editable.md#acls-and-groups) para obtener más información.

   Consulte [Administración de derechos de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management) para obtener información detallada sobre cómo administrar y asignar derechos de acceso.

### Uso del explorador de configuración {#using-the-configuration-browser}

1. Vaya a **Navegación global** > **Herramientas** > **Explorador de configuración**.

   Las carpetas existentes se muestran a la izquierda, incluida la carpeta **global**.

1. Haga clic en **Crear**.
1. En el cuadro de diálogo **Crear configuración**, se deben configurar los siguientes campos:

   * **Título**: proporcione un título para la carpeta de configuración
   * **Plantillas editables**: seleccione esta opción para permitir plantillas editables dentro de esta carpeta

1. Haga clic en **Crear**

>[!NOTE]
>
>En el Explorador de configuración, puede editar la carpeta global y activar la opción **Plantillas editables** si desea crear plantillas dentro de esta carpeta. Sin embargo, esta práctica no es una práctica recomendada.
>
>Consulte la documentación del [Explorador de configuración](/help/sites-administering/configurations.md) para obtener más información.

### ACL y grupos {#acls-and-groups}

Una vez creadas las carpetas de plantilla (ya sea mediante CRXDE o con el Explorador de configuración), se deben definir ACL para los grupos adecuados para las carpetas de plantilla para garantizar la seguridad adecuada.

Las carpetas de plantillas para la implementación de referencia [`We.Retail` &#x200B;](/help/sites-developing/we-retail.md) se pueden usar como ejemplo.

#### El grupo de autores de plantillas {#the-template-authors-group}

El grupo `template-authors` es el grupo que se usa para administrar el acceso a las plantillas y viene de serie con AEM, pero está vacío. Los usuarios deben agregarse al grupo para el proyecto o sitio.

>[!CAUTION]
>
>El grupo `template-authors` es *solamente* para los usuarios que deben poder crear plantillas.
>
>La edición de plantillas es eficaz y, si no se realiza correctamente, las plantillas existentes pueden romperse. Por lo tanto, esta función debe centrarse y solo incluir usuarios cualificados.

La siguiente tabla detalla los permisos necesarios para editar plantillas.

<table>
 <tbody>
  <tr>
   <th>Ruta</th>
   <th>Rol/grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/templates</code></td>
   <td>Autores de plantillas<br /> </td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en el espacio <code>/conf</code> específico del sitio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
   <td>El usuario web anónimo debe leer las plantillas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>replicateLos autores de contenido deben activar las plantillas de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/&lt;<i>your-folder</i>&gt;/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en el espacio <code>/conf</code> específico del sitio</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
   <td>El usuario web anónimo debe leer las directivas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los autores de contenido deben activar las políticas de una plantilla de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/&lt;site&gt;/settings/template-types</code></td>
   <td>Autor de plantillas</td>
   <td>leer</td>
   <td>El autor de la plantilla crea una plantilla basada en uno de los tipos de plantilla predefinidos.</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

Este grupo predeterminado de `template-authors` solo cubre las configuraciones de proyecto, en las que se permite a todos los miembros de `template-authors` acceder a todas las plantillas y crearlas. Para configuraciones más complejas, donde es necesario que varios grupos de autores de plantillas separen el acceso a las plantillas, se deben crear grupos de autores de plantillas más personalizados. Sin embargo, los permisos para los grupos de autores de plantillas seguirían siendo los mismos.

#### Plantillas heredadas en /conf/global {#legacy-templates-under-conf-global}

No almacene plantillas en `/conf/global`. Sin embargo, para algunas instalaciones heredadas, puede que aún haya plantillas en esta ubicación. *Solo* en estas situaciones heredadas deben configurarse explícitamente las siguientes `/conf/global` rutas.

<table>
 <tbody>
  <tr>
   <th>Ruta</th>
   <th>Rol/grupo</th>
   <th>Permisos<br /> </th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/templates</code></td>
   <td>Autores de plantillas</td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
   <td>El usuario web anónimo debe leer las plantillas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los autores de contenido deben activar las plantillas de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="3"><code>/conf/global/settings/wcm/policies</code></td>
   <td><code>Template Author</code></td>
   <td>leer, escribir, replicar</td>
   <td>Autores de plantillas que crean, leen, actualizan, eliminan y replican plantillas en <code>/conf/global</code></td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>leer</td>
   <td>El usuario web anónimo debe leer las directivas mientras procesa una página</td>
  </tr>
  <tr>
   <td>Autores de contenido</td>
   <td>replicar</td>
   <td>Los autores de contenido deben activar las políticas de una plantilla de una página al activar una página</td>
  </tr>
  <tr>
   <td rowspan="2"><code>/conf/global/settings/wcm/template-types</code></td>
   <td>Autor de plantillas</td>
   <td>leer</td>
   <td>El autor de la plantilla crea una plantilla basada en uno de los tipos de plantilla predefinidos</td>
  </tr>
  <tr>
   <td>Usuario web anónimo</td>
   <td>ninguno</td>
   <td>El usuario web anónimo no debe acceder a los tipos de plantilla</td>
  </tr>
 </tbody>
</table>

## Tipo de plantilla {#template-type}

Al crear una plantilla, especifique un tipo de plantilla:

* Los tipos de plantilla proporcionan plantillas para una plantilla de forma eficaz. Al crear una plantilla, se utiliza la estructura y el contenido inicial del tipo de plantilla seleccionado para crearla.

   * El tipo de plantilla se copia para crearla.
   * Una vez realizada la copia, la única conexión entre la plantilla y el tipo de plantilla es una referencia estática con fines informativos.

* Los tipos de plantilla permiten definir lo siguiente:

   * El tipo de recurso del componente de página.
   * La directiva del nodo raíz, que define los componentes permitidos en el editor de plantillas.

* AEM proporciona una pequeña selección de tipos de plantillas listas para usar, como Página de HTML5 y Página de formulario adaptable.

   * Se proporcionan ejemplos adicionales como parte del contenido de muestra [`We.Retail`](/help/sites-developing/we-retail.md).

* Los desarrolladores suelen definir los tipos de plantillas.

Los tipos de plantilla predeterminados se almacenan en:

* `/libs/settings/wcm/template-types`

>[!CAUTION]
>
>No cambie nada en la ruta de acceso `/libs`. El motivo es que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y se sobrescribirá al aplicar una revisión o un paquete de características).

Los tipos de plantilla específicos del sitio deben almacenarse en la ubicación comparable de:

* `/apps/settings/wcm/template-types`

Las definiciones de los tipos de plantillas personalizadas deben almacenarse en carpetas definidas por el usuario (recomendado) o, alternativamente, en `global`. Por ejemplo:

* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/template-types`
* `/conf/<my-folder>/settings/wcm/template-types`
* `/conf/global/settings/wcm/template-types`

>[!CAUTION]
>
>Los tipos de plantilla deben respetar la estructura de carpetas correcta (es decir, `/settings/wcm/...`); de lo contrario, no se encontrarán los tipos de plantilla.

### Creación de tipos de plantilla {#creating-template-types}

Si ha creado una plantilla que puede servir de base a otras plantillas, puede copiar esta plantilla como un tipo de plantilla.

1. Cree una plantilla como lo haría con cualquier plantilla editable. Consulte [Creación de plantillas de página](/help/sites-authoring/templates.md#creating-a-new-template-template-author). Esto puede servir de base para el tipo de plantilla.
1. Con CRXDE Lite, copie la plantilla recién creada del nodo `templates` al nodo `template-types` en la [carpeta de plantillas](/help/sites-developing/page-templates-editable.md#template-folders).
1. Elimine la plantilla del nodo `templates` en la [carpeta de plantillas](/help/sites-developing/page-templates-editable.md#template-folders).
1. En la copia de la plantilla que se encuentra bajo el nodo `template-types`, elimine todas las propiedades `cq:template` y `cq:templateType` de todos los nodos `jcr:content`.

También puede desarrollar su propio tipo de plantilla con una plantilla editable de ejemplo como base, disponible en GitHub.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto aem-sites-example-custom-template-type en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type)
* Descargar el proyecto como [archivo ZIP](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sites-example-custom-template-type/zip/refs/heads/master)

## Definiciones de plantilla {#template-definitions}

Las definiciones para plantillas editables se almacenan en [carpetas definidas por el usuario](/help/sites-developing/page-templates-editable.md#template-folders) (recomendado) o, alternativamente, en `global`. Por ejemplo:

* `/conf/<my-folder>/settings/wcm/templates`
* `/conf/<my-folder-01>/<my-folder-02>/settings/wcm/templates`
* `/conf/global/settings/wcm/templates`

El nodo raíz de la plantilla es del tipo `cq:Template` con una estructura básica de:

```xml
<template-name>
  initial
    jcr:content
      root
        <component>
        ...
        <component>
  jcr:content
    @property status
  policies
    jcr:content
      root
        @property cq:policy
        <component>
          @property cq:policy
        ...
        <component>
          @property cq:policy
  structure
    jcr:content
      root
        <component>
        ...
        <component>
      cq:responsive
        breakpoints
  thumbnail.png
```

Los elementos principales son:

* `<template-name>`

   * ` [initial](#initial-content)`
   * `jcr:content`
   * ` [structure](#structure)`
   * ` [policies](#policies)`
   * `thumbnail.png`

### jcr:contenido {#jcr-content}

Este nodo contiene propiedades para la plantilla:

* **Nombre**: `jcr:title`

* **Nombre**: `status`

   * **Tipo**: `String`

   * **Valor**: `draft`, `enabled` o `disabled`

### Estructura {#structure}

Define la estructura de la página resultante:

* Se combina con el contenido inicial (`/initial`) al crear una página.
* Los cambios realizados en la estructura se reflejan en cualquier página creada con la plantilla.
* El nodo `root` ( `structure/jcr:content/root`) define la lista de componentes disponibles en la página resultante.

   * Los componentes definidos en la estructura de la plantilla no se pueden mover ni eliminar de ninguna página resultante.
   * Una vez desbloqueado un componente, la propiedad `editable` se establece en `true`.

   * Después de desbloquear un componente que ya contiene contenido, este contenido se mueve a la rama `initial`.

* El nodo `cq:responsive` contiene definiciones para el diseño interactivo.

### Contenido inicial {#initial-content}

Define el contenido inicial que tiene una nueva página al crearla:

* Contiene un nodo `jcr:content` que se copia en las páginas nuevas.
* Se combina con la estructura (`/structure`) al crear una página.
* Todas las páginas existentes se actualizan si el contenido inicial cambia después de la creación.
* El nodo `root` contiene una lista de componentes para definir los que están disponibles en la página resultante.
* Si el contenido se añade a un componente en modo de estructura y ese componente se desbloquea posteriormente (o a la inversa), este contenido se utiliza como contenido inicial.

### Diseño {#layout}

Al [editar una plantilla, puede definir el diseño](/help/sites-authoring/templates.md), esta práctica usa [diseño interactivo estándar](/help/sites-authoring/responsive-layout.md) que también se puede [configurar](/help/sites-administering/configuring-responsive-layout.md).

### Políticas de contenido {#content-policies}

Las políticas de contenido (o diseño) definen las propiedades de diseño de un componente, como su disponibilidad o las dimensiones mínimas/máximas. Estas políticas se aplican a la plantilla (y a las páginas creadas con la plantilla). Las políticas de contenido se pueden crear y seleccionar en el editor de plantillas.

* La propiedad `cq:policy`, en el nodo `root`
  `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/root`
Proporciona una referencia relativa a la directiva de contenido para el sistema de párrafos de la página.

* La propiedad `cq:policy`, en los nodos explícitos de componente en `root`, proporciona vínculos a las directivas de los componentes individuales.

* Las definiciones de directivas reales se almacenan en:
  `/conf/<your-folder>/settings/wcm/policies/wcm/foundation/components`

>[!NOTE]
>
>Las rutas de las definiciones de directivas dependen de la ruta del componente. `cq:policy` contiene una referencia relativa a la propia configuración.

>[!NOTE]
>
>Las páginas creadas a partir de plantillas editables no ofrecen el modo Diseño en el editor de páginas.
>
>El árbol `policies` de una plantilla editable tiene la misma jerarquía que la configuración de modo de diseño de una plantilla estática en:
>
>`/etc/designs/<my-site>/jcr:content/<component-name>`
>
>Se definió la configuración de modo de diseño de una plantilla estática por componente de página.

### Políticas de la página {#page-policies}

Las directivas de página permiten definir la [directiva de contenido](#content-policies) para la página (parsys principal), en la plantilla o en las páginas resultantes.

### Habilitar y permitir el uso de una plantilla {#enabling-and-allowing-a-template-for-use}

1. **Habilitar la plantilla**

   Para poder utilizar una plantilla, debe habilitarse mediante lo siguiente:

   * [Habilitando la plantilla](/help/sites-authoring/templates.md#enablingatemplateauthor) desde la consola **Plantillas**.

   * Estableciendo la propiedad status en el nodo `jcr:content`.

      * Por ejemplo, en:

        `/conf/<your-folder>/settings/wcm/templates/<your-template>/jcr:content`

      * Defina la propiedad:

         * Nombre: estado
         * Tipo: cadena
         * Valor: `enabled`

1. **Plantillas permitidas**

   * [Defina las rutas de plantilla permitidas en **Propiedades de página**](/help/sites-authoring/templates.md#allowing-a-template-author) de la página o página raíz apropiada de una subrama.
   * Establezca la propiedad:

     `cq:allowedTemplates`
En el nodo `jcr:content` de la rama requerida.

   Por ejemplo, con un valor de:

   `/conf/<your-folder>/settings/wcm/templates/.*`

## Páginas de contenido resultantes {#resultant-content-pages}

Páginas creadas a partir de plantillas editables:

* Se crean con un subárbol que se combina de `structure` y `initial` en la plantilla

* Tener referencias a información contenida en la plantilla y el tipo de plantilla. Puede lograr esta funcionalidad con un nodo `jcr:content` con las propiedades:

   * `cq:template`
Proporciona la referencia dinámica a la plantilla real; permite que los cambios realizados en la plantilla se reflejen en las páginas reales.

   * `cq:templateType`
Proporciona una referencia al tipo de plantilla.

![chlimage_1-71](assets/chlimage_1-71.png)

El diagrama anterior muestra cómo se interrelacionan las plantillas, el contenido y los componentes:

* Controlador - `/content/<my-site>/<my-page>`
La página resultante que hace referencia a la plantilla. El contenido controla todo el proceso. Según las definiciones, accede a la plantilla y a los componentes adecuados.

* Configuración - `/conf/<my-folder>/settings/wcm/templates/<my-template>`
La [plantilla y las políticas de contenido relacionadas](#template-definitions) definen la configuración de la página.

* Modelo: paquetes OSGi
Los [paquetes OSGI](/help/sites-deploying/osgi-configuration-settings.md) implementan la funcionalidad.

* Vista: `/apps/<my-site>/components`
Tanto en el entorno de creación como en el de publicación, [components](/help/sites-developing/components.md) procesan el contenido.

Al procesar una página:

* **Plantillas**:

   * Se hace referencia a la propiedad `cq:template` de su nodo `jcr:content` para obtener acceso a la plantilla que corresponde a esa página.

* **Componentes**:

   * El componente de página combina el árbol `structure/jcr:content` de la plantilla con el árbol `jcr:content` de la página.

   * El componente Página solo permite al autor editar los nodos de la estructura de la plantilla que se han marcado como editables (y los secundarios).
   * Al procesar un componente en una página, la ruta relativa de ese componente se toma del nodo `jcr:content`; a continuación, se busca en la misma ruta bajo el nodo `policies/jcr:content` de la plantilla.

      * La propiedad `cq:policy` de este nodo señala a la directiva de contenido real (es decir, contiene la configuración de diseño para ese componente).

      * Esta funcionalidad permite tener varias plantillas que reutilizan las mismas configuraciones de directiva de contenido.
