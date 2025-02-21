---
title: Fragmentos de experiencias
description: Fragmentos de experiencias en la creación de Adobe Experience Manager Sites.
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Experience Fragments
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 71%

---

# Fragmentos de experiencias{#experience-fragments}

En Adobe Experience Manager (AEM), un fragmento de experiencia es un grupo de uno o más componentes, incluido el contenido y el diseño, a los que se puede hacer referencia dentro de las páginas. Pueden contener cualquier componente.

Un fragmento de experiencia:

* Forma parte de una experiencia (página).
* Se puede usar en varias páginas (que se basan en plantillas editables).
* Se basa en una plantilla (solo editable) para definir la estructura y los componentes.
* Esta plantilla se utiliza para crear la *página raíz* del Fragmento de experiencia.
* Está formado por uno o más componentes, con diseño, en un sistema de párrafos.
* Puede contener otros fragmentos de experiencias.
* Se puede combinar con otros componentes (incluidos otros fragmentos de experiencias) para formar una página completa (experiencia).
* Se pueden crear una o más variaciones basadas en la página raíz.
* Estas pueden compartir contenido o componentes.
* Se puede desglosar en bloques de construcción que se pueden utilizar en varias variaciones del fragmento.

Puede utilizar los fragmentos de experiencias:

* Si un autor desea reutilizar partes de una página (un fragmento de una experiencia), debe copiar y pegar ese fragmento. Crear y mantener estas experiencias de copia y pegado es un proceso laborioso y es posible que el usuario cometa errores. Los fragmentos de experiencias eliminan la necesidad de copiar y pegar.
* Para admitir el caso práctico de CMS sin encabezado. Los autores quieren utilizar AEM solo para la creación, pero no para la entrega al cliente. Un punto de contacto o sistema de terceros consumiría esa experiencia y luego la entregaría al usuario final.
* Con [Multi Site Management (MSM)](/help/sites-administering/msm.md); como fragmento de experiencia forma parte de una página. Esto se aplica tanto a los fragmentos individuales como a las carpetas en las que residen.

>[!NOTE]
>
>La escritura de acceso para fragmentos de experiencias requiere que la cuenta de usuario se registre en el grupo:
>
>    `experience-fragments-editors`
>
>Si tiene algún problema, póngase en contacto con el administrador del sistema.

## ¿Cuándo se deben utilizar los fragmentos de experiencias?   {#when-should-you-use-experience-fragments}

Los fragmentos de experiencias deben usarse en las siguientes situaciones:

* Siempre que quiera reutilizar experiencias.

   * Experiencias que se reutilizarán con contenido igual o similar

* Cuando se utiliza AEM como plataforma de envío de contenido para terceros.

   * Cualquier solución que desee utilizar AEM como plataforma de entrega de contenido
   * Incrustación de contenido en puntos de contacto de terceros

* Si tiene una experiencia con diferentes variaciones o representaciones.

   * Variaciones específicas de canal o contexto
   * Experiencias que tiene sentido agrupar (por ejemplo, una campaña con diferentes experiencias en diferentes canales)

* Al utilizar el comercio omnicanal.

   * Compartir contenido relacionado con el comercio en [medios sociales](/help/sites-developing/experience-fragments.md#social-variations) canales a escala
   * Hacer transaccionales los puntos de contacto

## Organización de los fragmentos de experiencias {#organizing-your-experience-fragments}

Se recomienda:
* usar carpetas para organizar los fragmentos de experiencias,

* [configurar las plantillas permitidas en estas carpetas](#configure-allowed-templates-folder).

La creación de carpetas permite:

* crear una estructura significativa para los fragmentos de experiencias; por ejemplo, según la clasificación.

  >[!NOTE]
  >
  >No es necesario alinear la estructura de los fragmentos de experiencias con la estructura de página del sitio.

* [asignar las plantillas permitidas en el nivel de carpeta](#configure-allowed-templates-folder)

  >[!NOTE]
  >
  >Puede utilizar el [editor de plantillas](/help/sites-authoring/templates.md) para crear su propia plantilla.

El proyecto WKND estructura algunos fragmentos de experiencias según `Contributors`. La estructura utilizada también ilustra cómo se pueden utilizar otras funciones, como la Administración de varios sitios (incluidas las copias de idiomas).

Consulte:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Carpetas para fragmentos de experiencias](/help/sites-authoring/assets/xf-folders.png)

## Creación y configuración de una carpeta para los fragmentos de experiencias {#creating-and-configuring-a-folder-for-your-experience-fragments}

Para crear y configurar una carpeta para los fragmentos de experiencias, se recomienda:

1. [Crear una carpeta](/help/sites-authoring/managing-pages.md#creating-a-new-folder).

1. [Configurar las plantillas de fragmento de experiencia permitidas para esa carpeta](#configure-allowed-templates-folder).

>[!NOTE]
>
>También es posible configurar las plantillas [permitidas para su instancia](#configure-allowed-templates-instance), pero este método **no se recomienda**, ya que los valores se pueden sobrescribir tras la actualización.

### Configurar las plantillas permitidas para la carpeta {#configure-allowed-templates-folder}

>[!NOTE]
>
>Este es el método recomendado para especificar las **plantillas permitidas**, ya que los valores no se sobrescriben tras la actualización.

1. Vaya a la carpeta de **fragmentos de experiencias** necesaria.

1. Seleccione la carpeta y, a continuación, vaya a **Propiedades**.

1. Especifique la expresión regular para recuperar las plantillas necesarias en el campo **Plantillas permitidas**.

   Por ejemplo:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Consulte:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Propiedades de fragmentos de experiencias: plantillas permitidas](/help/sites-authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Para obtener más información, consulte [Plantillas para fragmentos de experiencias](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments).

1. Seleccione **Guardar y cerrar**.

### Configure las plantillas permitidas para la instancia {#configure-allowed-templates-instance}

>[!CAUTION]
>
>No se recomienda cambiar las **plantillas permitidas** por este método, ya que las plantillas especificadas se pueden sobrescribir tras la actualización.
>
>Utilice este cuadro de diálogo únicamente con fines informativos.

1. Vaya a la consola de **fragmentos de experiencias** indicada.

1. Seleccione las **opciones de configuración**:

   ![Botón Configuración](assets/ef-02.png)

1. Especifique las plantillas necesarias en el cuadro de diálogo **Configurar fragmentos de experiencias**:

   ![Configurar Fragmentos de experiencias](assets/ef-01.png)

   >[!NOTE]
   >
   >Para obtener más información, consulte [Plantillas para fragmentos de experiencias](/help/sites-developing/experience-fragments.md#templates-for-experience-fragments).

1. Seleccione **Guardar**.

## Creación de un fragmento de experiencia {#creating-an-experience-fragment}

Para crear un fragmento de experiencia:

1. Seleccione Fragmentos de experiencias desde la navegación global.

   ![xf-01](assets/xf-01.png)

1. Vaya a la carpeta requerida y seleccione **Crear**.

   ![xf-02](assets/xf-02.png)

1. Seleccione **Fragmento de experiencia** para abrir el asistente **Crear fragmento de experiencia**.

   Seleccione la **plantilla** adecuada y, a continuación, **Siguiente**:

   ![xf-03](assets/xf-03.png)

1. Introduzca las **propiedades** del **fragmento de experiencia**.

   Es obligatorio escribir un **título**. Si se deja **Name** en blanco, se derivará del **Title**.

   ![xf-04](assets/xf-04.png)

   >[!NOTE]
   >
   >Las etiquetas de la plantilla de Fragmento de experiencia no se combinarán con etiquetas en esta página raíz del Fragmento de experiencia.
   >
   >Son totalmente independientes.

1. Haga clic en **Crear**.

   Se mostrará un mensaje. Seleccione lo siguiente:

   * **Listo** para volver a la consola

   * **Abrir** para abrir el editor de fragmentos

## Edición del fragmento de experiencia {#editing-your-experience-fragment}

El editor de fragmentos de experiencias ofrece funcionalidades similares a las del editor de páginas.

>[!NOTE]
>
>Consulte [Edición del contenido de página](/help/sites-authoring/editing-content.md) para obtener más información sobre cómo utilizar el editor de páginas.

El siguiente procedimiento de ejemplo ilustra cómo crear un teaser para un producto:

1. Arrastre y suelte un **Teaser** desde el [Explorador de componentes](/help/sites-authoring/author-environment-tools.md#components-browser).

   ![xf-05](assets/xf-05.png)

1. Seleccione **[Configurar](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)** en la barra de herramientas de componentes.
1. Agregue el **recurso** y defina las **propiedades** según sea necesario.
1. Confirme las definiciones con **Listo** (icono del tic).
1. Agregue más componentes según sea necesario.

## Creación de una variación de fragmento de experiencia {#creating-an-experience-fragment-variation}

Puede crear varias variaciones para este fragmento de experiencia en función de sus necesidades:

1. Abra el fragmento a [editar](/help/sites-authoring/experience-fragments.md#editing-your-experience-fragment).
1. Abra la pestaña **Variaciones**.

   ![xf-authoring-06](assets/xf-authoring-06.png)

1. **Crear** le permite crear:

   * **Variación**
   * **Variación como [Live Copy](/help/sites-administering/msm.md#live-copies)**.

     >[!NOTE]
     >
     >Al crear una variación inicial como Live Copy, se heredará el título mediante Live Copy Source como variación principal.

1. Defina las propiedades necesarias:

   * **Plantilla**
   * **Título**
   * **Nombre**; si se deja en blanco, se derivará del Título
   * **Descripción**
   * **Etiquetas de variación**

   ![xf-06](assets/xf-06.png)

1. Confirme con **Listo** (icono del tic), la nueva variación se mostrará en el panel:

   ![xf-07](assets/xf-07.png)

## Uso de los fragmentos de experiencias {#using-your-experience-fragment}

Ahora puede utilizar el fragmento de experiencia para crear páginas:

1. Abra la página para editarla.

   >[!NOTE]
   >
   >La página debe basarse en una plantilla editable.

   Por ejemplo: [https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html](https://localhost:4502/editor.html/content/we-retail/language-masters/en/products/men.html)

1. Cree una instancia del componente Fragmento de experiencia arrastrando el componente desde el Explorador de componentes al sistema de párrafos de página:

   ![xf-08](assets/xf-08.png)

1. Agregue el fragmento de experiencia real a la instancia de componente; o bien:

   * Arrastre el fragmento necesario desde el explorador Assets y suéltelo en el componente
   * Seleccione **Configurar** en la barra de herramientas de componentes y especifique el fragmento que desea utilizar. Confirme con **Listo** (marca)

   ![xf-09](assets/xf-09.png)

   >[!NOTE]
   >
   >La opción Editar, en la barra de herramientas del componente, funciona como un método abreviado para abrir el fragmento en el editor de fragmentos.

## Componentes {#building-blocks}

Puede seleccionar uno o varios componentes para crear un bloque de creación y así reciclarlo en el fragmento:

### Crear un bloque de creación {#creating-a-building-block}

Para crear un bloque de creación:

1. En el editor de Fragmento de experiencia, seleccione los componentes que desea reutilizar:

   ![xf-10](assets/xf-10.png)

1. En la barra de herramientas de componentes, seleccione **Convertir en bloque de creación**:

   ![xf-authoring-13-icon](assets/xf-authoring-13-icon.png)

1. Escriba el nombre del **bloque de creación** y confirme con **Convertir**:

   ![xf-11](assets/xf-11.png)

1. El **bloque de creación** se muestra en la pestaña y se puede seleccionar en el sistema de párrafos:

   ![xf-12](assets/xf-12.png)

#### Administración de un bloque de creación {#managing-a-building-block}

El bloque de creación se puede ver en la pestaña **Bloques de creación**. Para cada bloque, están disponibles las siguientes acciones:

* Ir a la variación principal: abrir la variación de la página raíz en una nueva pestaña
* Cambiar nombre
* Eliminar

![xf-13](assets/xf-13.png)

#### Uso de un bloque de creación {#using-a-building-block}

Puede arrastrar el bloque de creación al sistema de párrafos de cualquier fragmento, como con cualquier componente.

## Detalles del fragmento de experiencia {#details-of-your-experience-fragment}

Se pueden ver los detalles del fragmento:

1. Los detalles se muestran en todas las vistas de la consola de **Fragmentos de experiencias**, con una **vista de lista** que incluye los detalles de una [exportación a destino](/help/sites-administering/experience-fragments-target.md):

   ![ef-03](assets/ef-03.png)

1. Al abrir las **propiedades** del fragmento de experiencia:

   ![ef-04](assets/ef-04.png)

   Las propiedades están disponibles en varias pestañas:

   >[!CAUTION]
   >
   >Estas pestañas se muestran al abrir **Propiedades** desde la consola fragmentos de experiencias.
   >
   >
   >Si se selecciona **Abrir propiedades** al editar un fragmento de experiencia, se muestran las [propiedades de página](/help/sites-authoring/editing-page-properties.md) correspondientes.

   ![ef-05](assets/ef-05.png)

   * **Básico**

      * **Título**: obligatorio

      * **Descripción**
      * **Etiquetas**
      * **Número total de variantes**: solo información

      * **Número de variantes web**: solo información
      * **Número de variantes que no son de web** - solo inf **formación**

      * **Número de páginas que utilizan este fragmento**: solo información

   * **Cloud Services**

      * **Configuración de la nube**
      * **Configuraciones de Cloud Service**
      * **ID de página de Facebook**
      * **Tablero de Pinterest**

   * **Referencias**

      * Una lista de referencias.

   * **Estado de medios sociales**

      * Detalles de las variaciones de las redes sociales.

## Representación HTML sin formato {#the-plain-html-rendition}

Uso del selector de `.plain.` en la URL; puede acceder a la representación HTML sin formato desde el explorador.

>[!NOTE]
>
>Aunque esta opción está disponible directamente desde el explorador, [el objetivo principal es permitir a otras aplicaciones (por ejemplo, aplicaciones web de terceros o implementaciones móviles personalizadas) acceder al contenido del fragmento de experiencia directamente, únicamente mediante la URL](/help/sites-developing/experience-fragments.md#the-plain-html-rendition).

## Exportación de fragmentos de experiencias   {#exporting-experience-fragments}

De forma predeterminada, los fragmentos de experiencias se envían en formato HTML. Esto se puede utilizar tanto en AEM como en canales de terceros por igual.

Para la exportación a Adobe Target, también se puede utilizar JSON. Consulte [Integración de Target con fragmentos de experiencias](/help/sites-administering/experience-fragments-target.md) para obtener información completa.
