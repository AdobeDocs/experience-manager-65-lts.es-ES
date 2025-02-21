---
title: Configurar formularios de búsqueda
description: Aprenda a utilizar Search Forms para personalizar la selección de predicados de búsqueda utilizados en los paneles de búsqueda disponibles en las consolas y paneles de AEM del entorno de creación.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 7%

---


# Configurar formularios de búsqueda{#configuring-search-forms}

Use **Buscar en Forms** para personalizar la selección de predicados de búsqueda utilizados en los paneles de búsqueda disponibles en varias consolas o paneles de AEM del entorno de creación. La personalización de estos paneles hace que la funcionalidad de búsqueda sea versátil según sus necesidades específicas.

Hay un [rango de predicados](#predicates-and-their-settings)s disponibles de forma predeterminada. Puede agregar varios predicados, incluido (entre otros) el predicado Propiedad, para buscar recursos que coincidan con una sola propiedad especificada por usted. O bien, el predicado Opciones para buscar recursos que coincidan con uno o varios valores especificados para una propiedad en particular.

Puede [configurar los formularios de búsqueda](#configuring-your-search-forms) que se usan en varias consolas y en el explorador de recursos (al editar páginas). Se puede acceder a los [cuadros de diálogo para configurar estos formularios](#configuring-your-search-forms) a través de:

* **Herramientas**

   * **General**

      * **Buscar en Forms**

Cuando acceda por primera vez a esta consola, verá que todas las configuraciones tienen un símbolo de candado. Esto indica que la configuración adecuada es la predeterminada (predeterminada) y no se puede eliminar. Después de haber personalizado la configuración, el bloqueo desaparece a menos que [elimine su configuración personalizada](#deleting-a-configuration-to-reinstate-the-default). En tal caso, se restablece el valor predeterminado (y el indicador de candado).

![Ventana de formularios de búsqueda](assets/chlimage_1-374.png)

## Configuraciones {#configurations}

Las configuraciones predeterminadas disponibles son las siguientes:

* **Editor de páginas (búsqueda de documentos):**

  Esta configuración define las opciones disponibles al buscar documentos en el explorador de recursos (al editar una página).

* **Editor de páginas (búsqueda de imágenes):**

  Esta configuración define las opciones disponibles al buscar imágenes en el explorador de recursos (al editar una página).

* **Editor de páginas (búsqueda de manuscritos):**

  Esta configuración define las opciones disponibles al buscar manuscritos en el explorador de recursos (al editar una página).

* **Editor de páginas (búsqueda de páginas):**

  Esta configuración define las opciones disponibles al buscar páginas en el explorador de recursos (al editar una página).

* **Editor de páginas (búsqueda de párrafos):**

  Esta configuración define las opciones disponibles al buscar párrafos en el explorador de recursos (al editar una página).

* **Editor de páginas (búsqueda de productos):**

  Esta configuración define las opciones disponibles al buscar productos en el explorador de recursos (al editar una página).

* **Editor de páginas (Dynamic Media Classic [anteriormente búsqueda de Scene7])**:

  Esta configuración define las opciones disponibles al buscar recursos de Scene7 en el explorador de recursos (al editar una página).

* **Carril de búsqueda de administración de sitios**:

  Esta configuración define las opciones de búsqueda disponibles para el usuario al utilizar el carril de búsqueda de la consola Sitios.

* **Editor de páginas (búsqueda de vídeos):**

  Esta configuración define las opciones disponibles al buscar vídeos en el explorador de recursos (al editar una página).

* **Carril de búsqueda de administración de Assets:**

  Esta configuración define las opciones de búsqueda disponibles para el usuario al utilizar la consola de Assets.

* **Carril de búsqueda de administración de catálogos:**

  Esta configuración define las opciones de búsqueda disponibles para el usuario al buscar en un catálogo comercial.

* **Carril de búsqueda de administración de pedidos:**

  Esta configuración define las opciones de búsqueda disponibles para el usuario al buscar pedidos comerciales.

* Carril de búsqueda de administración de **colecciones de productos:**

  Esta configuración define las opciones de búsqueda disponibles para el usuario al buscar colecciones de productos de comercio.

* Carril de búsqueda de administración de **productos:**

  Esta configuración define las opciones de búsqueda disponibles para el usuario al buscar productos de comercio.

* **Carril de búsqueda del administrador del proyecto:**

  Esta configuración define las opciones de búsqueda disponibles para el usuario al buscar proyectos.

## Predicados y su configuración {#predicates-and-their-settings}

### Predicados {#predicates}

Los siguientes predicados están disponibles, según la configuración:

<table>
 <tbody>
  <tr>
   <th>Predicado</th>
   <th>Función</th>
   <th>Configuración</th>
  </tr>
  <tr>
   <td>Análisis </td>
   <td>Funciones de búsqueda y filtrado en el explorador de sitios al mostrar datos con análisis. Los filtros de búsqueda de Analytics se cargan para coincidir con las columnas de Analytics personalizadas asignadas.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Última modificación del recurso </td>
   <td>Fecha de la última modificación del recurso.<br /> </td>
   <td>Un predicado personalizado, basado en el predicado de fecha.</td>
  </tr>
  <tr>
   <td>Componentes </td>
   <td>Permite a un autor buscar/filtrar páginas que tienen un componente específico en él. Por ejemplo, una galería de imágenes.<br /> </td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Profundidad de la propiedad</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Fecha </td>
   <td>Búsqueda basada en el deslizador de recursos basada en una propiedad de fecha.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo de fechas </td>
   <td>Busque recursos creados dentro de un intervalo especificado para una propiedad de fecha. En el panel Buscar, puede especificar las fechas de inicio y finalización.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Texto de intervalo (desde)*</li>
     <li>Texto de intervalo (hasta)*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado de caducidad </td>
   <td>Buscar recursos en función del estado de caducidad.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Tamaño del archivo </td>
   <td>Busque recursos en función de su tamaño.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta de opción</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Filtro oculto</td>
   <td>Un filtro de propiedad y valor, no visible para el usuario.</td>
   <td>
    <ul>
     <li>Nombre de la propiedad</li>
     <li>Valor de propiedad</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opciones </td>
   <td><p>Las opciones son nodos de contenido creados por el usuario.</p> <p>Consulte <a href="#addinganoptionspredicate">Agregar un predicado de opciones</a> para obtener más información.</p> </td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Ruta de JSON</li>
     <li>Nombre de propiedad*</li>
     <li>Selección única</li>
     <li>Ruta de opción</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propiedad Options </td>
   <td>Busque en una propiedad de la opción.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta del nodo de opciones <br /> </li>
     <li>Selección única</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Estado de la página </td>
   <td>Buscar páginas según su estado.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de la propiedad de publicación</li>
     <li>Nombre de la propiedad de LiveCopy</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ruta </td>
   <td>Busque recursos ubicados en una ruta específica.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Añadir ruta de búsqueda</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Propiedad </td>
   <td>Busque en una propiedad especificada.</td>
   <td>ninguno</td>
  </tr>
  <tr>
   <td>Estado de publicación </td>
   <td>Buscar recursos en función de su estado de publicación</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo </td>
   <td>Busque recursos que se encuentren dentro de un rango especificado. En el panel Buscar, puede especificar los valores mínimo y máximo del rango.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de la propiedad</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Opciones del intervalo </td>
   <td>Un predicado de búsqueda específico para Assets y el mismo que el predicado de regulador común. Sigue disponible debido a problemas de compatibilidad con versiones anteriores.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta de opción</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Clasificación </td>
   <td>Buscar recursos según su clasificación.<br /> </td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta de opción</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Fecha relativa </td>
   <td>Buscar recursos en función de la fecha relativa de su creación <br /> </td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Fecha relativa</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Intervalo del regulador </td>
   <td>Un predicado de búsqueda común que amplía el predicado de intervalo con la capacidad del control deslizante. El valor de la propiedad buscada debe estar entre los límites del control deslizante.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Etiqueta </td>
   <td>Busque recursos en función de etiquetas. Puede configurar la propiedad Ruta para rellenar varias etiquetas en la lista Etiquetas.</td>
   <td>
    <ul>
     <li>Etiqueta de campo</li>
     <li>Nombre de propiedad*</li>
     <li>Ruta de opción</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Etiquetas </td>
   <td>Busque en función de las etiquetas.</td>
   <td>
    <ul>
     <li>Marcador de posición</li>
     <li>Nombre de propiedad*</li>
     <li>Descripción</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Los predicados de búsqueda comunes se definen en:
>  `/libs/cq/gui/components/common/admin/customsearch/searchpredicates`
>
>* Los predicados de búsqueda relacionados únicamente con siteadmin (IU clásica) se encuentran en:
>  `/libs/cq/gui/components/siteadmin/admin/searchpanel/searchpredicates`
>   * Están en desuso y solo están disponibles para la compatibilidad con versiones anteriores.
>
>Esta información es solo de referencia. No cambie `/libs`.

### Configuración de predicado {#predicate-settings}

En función del predicado, hay una selección de opciones disponibles para la configuración:

* **Etiqueta de campo**

  La etiqueta que aparece como encabezado contraíble o como etiqueta de campo del predicado.

* **Descripción**

  Detalles descriptivos del usuario.

* **Marcador de posición**

  Texto vacío o el marcador de posición del predicado en caso de que no se introduzca ningún texto de filtrado.

* **Nombre de propiedad**

  Propiedad en la que se va a buscar. Utiliza una ruta relativa y los caracteres comodín `*/*/*` especifican la profundidad de la propiedad en relación con el nodo `jcr:content` (cada asterisco representa un nivel de nodo).

  Si desea buscar únicamente en un nodo secundario de primer nivel del recurso que tiene la propiedad `x` en el nodo `jcr:content`, utilice `*/jcr:content/x`

* **Profundidad de propiedad**

  Profundidad máxima para buscar esa propiedad dentro de los recursos. Por lo tanto, se puede realizar una búsqueda de esa propiedad en un recurso y en elementos secundarios recursivos hasta que el nivel de los elementos secundarios sea igual a la profundidad especificada.

* **Valor de propiedad**

  El valor de la propiedad como cadena absoluta o como lenguaje de expresión; por ejemplo, `cq:Page` o

  `${empty requestPathInfo.suffix ? "/content" : requestPathInfo.suffix}`.

* **Texto de intervalo**

  La etiqueta del campo de intervalo en el predicado **Date Range**.

* **Ruta de opción**

  El usuario puede seleccionar la ruta mediante el Explorador de rutas en la pestaña de configuración de predicado. Después de seleccionar **+**, se usa el icono para agregar la selección a la lista de opciones válidas (a continuación, se usa el icono **-** para quitar, si es necesario).

  Las opciones son nodos de contenido creados por el usuario que tienen la siguiente estructura:

  `(jcr:primaryType = nt:unstructured, value (String), jcr:title (String))`

* **Ruta del nodo de opciones**
Igual que en la práctica **Ruta de opciones**, solo que esto se encuentra en el campo de predicado común y el otro es específico para los recursos.

* **Selección única**
Si se selecciona, las opciones se representan como casillas de verificación que permiten solo una selección. Si se selecciona por error, se puede anular la selección de una casilla de verificación.

* **Nombres de propiedades de publicación y Live Copy**
Las etiquetas de las casillas de verificación de publicación y Live Copy para el predicado específico de Sites.

* La &amp;ast; de las etiquetas de campo de la ficha **Configuración** indica que los campos son obligatorios y, si se deja en blanco, aparece un mensaje de error.

## Configuración de Search Forms {#configuring-your-search-forms}

### Creación/apertura de una configuración personalizada {#creating-opening-a-customized-configuration}

1. Vaya a **Herramientas** >> **General** >> **Buscar en Forms**.

1. Seleccione la configuración que desee personalizar.
1. Use el icono **Editar** para abrir la configuración y actualizarla.
1. Si hay una nueva personalización, es probable que desee [agregar nuevos campos de predicado y definir la configuración](#add-edit-a-predicate-field-and-define-field-settings) según sea necesario. Si hay una personalización existente, puede seleccionar un campo existente y [actualizar la configuración](#add-edit-a-predicate-field-and-define-field-settings).
1. Seleccione **Listo** para guardar la configuración.

   >[!NOTE]
   >
   >Las configuraciones personalizadas se almacenan (según corresponda) en:
   >
   >* `/apps/cq/gui/content/facets/<option>`
   >* `/apps/commerce/gui/content/facets/<option>`

### Adición o edición de un campo de predicado y definición de la configuración del campo {#add-edit-a-predicate-field-and-define-field-settings}

Puede añadir o editar campos y definir o actualizar su configuración:

1. [Abra la configuración personalizada](#creating-opening-a-customized-configuration) para actualizarla.
1. Si desea agregar un campo, abra la ficha **Seleccionar predicado** y arrastre el predicado requerido a la ubicación requerida. Por ejemplo, el **Predicado de intervalo de fechas**:

   ![Editando un formulario de búsqueda](assets/chlimage_1-375.png)

1. En función de si:

   * Va a añadir un campo:

     Después de agregar el predicado, se abre la ficha **Configuración** y se muestran las propiedades que se pueden definir.

   * Desea actualizar un predicado existente:

     Seleccione el campo de predicado (a la derecha) y, a continuación, abra la ficha **Configuración**.

   Por ejemplo, la configuración del **Predicado de intervalo de fechas**:

   ![Propiedades del predicado de intervalo de fechas](assets/chlimage_1-376.png)

1. Realice los cambios según sea necesario y confirme con **Listo**.

### Previsualización de la configuración de búsqueda {#previewing-the-search-configuration}

1. Seleccione el icono Vista previa:

   ![Vista previa de formularios de búsqueda](do-not-localize/chlimage_1-31.png)

1. Esto muestra los formularios de búsqueda tal como se muestran (totalmente expandidos) en la columna Buscar de la consola adecuada.

   ![Vista previa del formulario de búsqueda](assets/chlimage_1-377.png)

1. **Cerrar** la vista previa para que puedas regresar y finalizar la configuración.

### Eliminación de un campo de predicado {#deleting-a-predicate-field}

1. [Abra la configuración personalizada](#creating-opening-a-customized-configuration) para actualizarla.
1. Seleccione el campo de predicado (a la derecha), abra la ficha **Configuración** y, a continuación, seleccione el icono **Eliminar** (abajo a la izquierda).

   ![Icono Eliminar](do-not-localize/chlimage_1-32.png)

1. Un cuadro de diálogo solicita confirmación de la acción de eliminación.

1. Confirme este y cualquier otro cambio con **Listo**.

### Eliminación de una configuración (para restablecer los valores predeterminados) {#deleting-a-configuration-to-reinstate-the-default}

Después de personalizar una configuración, se anulan los valores predeterminados. Puede restablecer la configuración predeterminada eliminando la configuración personalizada.

>[!NOTE]
>
>No puede eliminar ninguna de las configuraciones predeterminadas.

La eliminación de una configuración personalizada se realiza desde la consola:

1. Seleccione la configuración necesaria (por ejemplo, **Editor de páginas (búsqueda de párrafos)**) y, a continuación, el icono **Eliminar** de la barra de herramientas:

   ![Eliminando un formulario](assets/chlimage_1-378.png)

1. La configuración personalizada se elimina y se restaura el valor predeterminado (esto se indica con la reaparición del símbolo de candado en la consola).

### Adición de predicados de opciones {#adding-options-predicates}

Los predicados de opciones (Options, Options, Property) permiten configurar un elemento para buscarlo. Se utilizan para buscar algo directamente debajo de la página; por ejemplo, una propiedad en el nodo de la página.

El siguiente ejemplo (para buscar según la plantilla utilizada para crear una página), ilustra los pasos involucrados:

1. Cree el nodo que define la propiedad en la que se va a buscar.

   Necesita un nodo raíz que contenga definiciones de las opciones individuales que deben estar disponibles para el usuario.

   Los nodos de las opciones individuales necesitan las propiedades:

   * `jcr:title`: etiqueta de campo que se mostrará en el carril de búsqueda
   * `value`: el valor de propiedad en el que se va a buscar

   ![Agregando opciones en CRXDE](assets/chlimage_1-379.png)

   >[!NOTE]
   >
   >***no*** cambia nada en la ruta de acceso `/libs`.
   >
   >Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
   >
   >El método recomendado para la configuración y otros cambios es:
   >
   >1. Vuelva a crear el elemento requerido, tal como existe en `/libs`, en `/apps`. En este caso de:
   >1. `/libs/cq/gui/content/common/options/predicates`
   >1. Realizar cambios en `/apps.`

1. Abra la consola **Buscar en Forms** y seleccione la configuración que desee actualizar. Por ejemplo, **Carril de búsqueda de administración de sitios**.

   Luego haga clic en el icono **Editar formularios de búsqueda**.

1. Según la configuración, agregue una **Options** u **Options Property** a la configuración.
1. Actualice los campos, en particular:

   * **Nombre de propiedad**

     Especifica la propiedad del nodo que se va a buscar en los nodos de destino. Por ejemplo:

     `jcr:content/cq:template`

   * **Ruta del nodo de opción**

     Seleccione la ruta donde se guardan las opciones. Por ejemplo:

     `/apps/cq/gui/content/common/options/predicates/templatetype`

   ![Agregando ruta de acceso de propiedad](assets/chlimage_1-380.png)

1. Seleccione **Listo** para guardar la configuración.
1. Vaya a la consola adecuada (en este ejemplo, **Sitios**) y abra el carril **Buscar**. Los formularios de búsqueda recién definidos, junto con las distintas opciones, están visibles. Seleccione la opción necesaria para poder ver los resultados de búsqueda:

   ![Los resultados finales](assets/chlimage_1-381.png)

## Permisos de usuario {#user-permissions}

En la tabla siguiente se enumeran los permisos necesarios para realizar acciones de edición, eliminación y vista previa en formularios de búsqueda.

<table>
 <tbody>
  <tr>
   <td><strong>Acción</strong></td>
   <td><strong>Permisos</strong></td>
  </tr>
  <tr>
   <td>Editar </td>
   <td>Permisos de lectura y escritura en el nodo <code>/apps </code>.</td>
  </tr>
  <tr>
   <td>Eliminar</td>
   <td>Permisos de lectura, escritura y eliminación en el nodo <code>/apps</code></td>
  </tr>
  <tr>
   <td>Vista previa</td>
   <td>Permisos de lectura, escritura y eliminación en el nodo <code>/var/dam/content</code>.<br /> Permisos de lectura y escritura en el nodo <code>/apps</code>.</td>
  </tr>
 </tbody>
</table>
