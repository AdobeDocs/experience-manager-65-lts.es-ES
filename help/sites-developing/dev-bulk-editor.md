---
title: Desarrollo del editor en bloque
description: El etiquetado permite clasificar y organizar el contenido
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 1%

---

# Desarrollo del editor en bloque{#developing-the-bulk-editor}

En esta sección se describe cómo desarrollar la herramienta Editor por lotes y cómo ampliar el componente Lista de productos, que se basa en el Editor por lotes.

## Parámetros de consulta del editor en lotes {#bulk-editor-query-parameters}

Al trabajar con el Editor por lotes, puede añadir varios parámetros de consulta a la URL para llamar al Editor por lotes con una configuración específica. Si desea que el editor en lotes siempre se utilice con una configuración determinada, por ejemplo, como en el componente Lista de productos, debe editar `bulkeditor.jsp` (en /libs/wcm/core/components/bulkeditor) o crear un componente con la configuración específica. Los cambios realizados con los parámetros de consulta no son permanentes.

Por ejemplo, si escribe lo siguiente en la dirección URL del explorador:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

El editor en lotes se muestra sin el campo **Ruta raíz**, ya que hrp=true oculta el campo. Con el parámetro hrp=false, se muestra el campo (el valor predeterminado).

A continuación se muestra una lista de los parámetros de consulta del Editor por lotes:

>[!NOTE]
>
>Cada parámetro puede tener un nombre largo y uno corto. Por ejemplo, el nombre largo de la ruta de acceso raíz de búsqueda es `rootPath`, el corto es `rp`. Si no se define el nombre largo, se lee el corto de la solicitud.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> Parámetro</p> <p>(nombre largo/nombre corto)<br /> </p> </td>
   <td> Tipo <br /> </td>
   <td> Descripción <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> Cadena </td>
   <td> ruta raíz de búsqueda</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> Cadena</td>
   <td> consulta de búsqueda</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> Booleano</td>
   <td> cuando es true, el modo de contenido está habilitado <br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> String[]</td>
   <td> propiedades buscadas (valores seleccionados de colsSelection mostrados como casillas de verificación)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> String[]</td>
   <td> propiedades buscadas adicionales (mostradas en un campo de texto separado por comas)</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> Booleano</td>
   <td> cuando es true, la consulta se realiza al cargar la página <br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> String[]</td>
   <td> selección de propiedades buscadas (mostradas como casillas de verificación)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> Booleano</td>
   <td> cuando es true, muestra únicamente la cuadrícula y no el panel de búsqueda <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed/spc</td>
   <td> Booleano</td>
   <td> cuando es true, el panel de búsqueda se contrae al cargar</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de ruta raíz</td>
  </tr>
  <tr>
   <td> hideQueryParams/hqp</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de consulta</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo content mode</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo de selección columnas</td>
  </tr>
  <tr>
   <td> hideExtraCols/hec</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el campo columnas adicionales</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón buscar</td>
  </tr>
  <tr>
   <td> hideSaveButton/hsavep</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón guardar</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón exportar</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón importar</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el texto del número de resultados de búsqueda de cuadrícula</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón de inserción de cuadrícula</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> Booleano</td>
   <td> cuando es true, oculta el botón eliminar de cuadrícula</td>
  </tr>
  <tr>
   <td> hidePathCol/hpc</td>
   <td> Booleano</td>
   <td> cuando es true, oculta la columna "ruta" de la cuadrícula</td>
  </tr>
 </tbody>
</table>

### Desarrollo de un componente basado en el editor por lotes: el componente Lista de productos {#developing-a-bulk-editor-based-component-the-product-list-component}

En esta sección se proporciona información general sobre cómo utilizar el Editor por lotes y una descripción del componente de Geometrixx existente basado en el Editor por lotes: el componente Lista de productos.

El componente Lista de productos permite a los usuarios mostrar y editar una tabla de datos. Por ejemplo, puede utilizar el componente Lista de productos para representar los productos en un catálogo. La información se presenta en una tabla estándar de HTML y cualquier edición se realiza en el cuadro de diálogo **Editar**, que contiene un widget BulkEditor. (Este editor en bloque es el mismo al que se puede acceder en /etc/importers/bulkeditor.html o a través del menú Herramientas). El componente Lista de productos se ha configurado para funciones específicas y limitadas del Editor por lotes. Se pueden configurar todas las partes del editor en bloque (o los componentes derivados del editor en bloque).

Con el editor en bloque, puede añadir, modificar, eliminar, filtrar y exportar las filas, guardar modificaciones e importar un conjunto de filas. Cada fila se almacena como un nodo en la propia instancia del componente Lista de productos. Cada celda es una propiedad de cada nodo. Esta es una opción de diseño y se puede cambiar fácilmente, por ejemplo, puede almacenar nodos en otro lugar del repositorio. La función del servlet de consulta es devolver la lista de los nodos que se van a mostrar; la ruta de búsqueda se define como una instancia de lista de productos.

El código fuente del componente Lista de productos está disponible en el repositorio en /apps/geometrixx/components/productlist y se compone de varias partes, como todos los componentes de Adobe Experience Manager (AEM):

* Renderización HTML: la renderización se realiza en un archivo JSP (/apps/geometrixx/components/productlist/productlist.jsp). El JSP lee los subnodos del componente de lista de productos actual y muestra cada uno de ellos como una fila de una tabla de HTML.
* Cuadro de diálogo Editar, que es donde se define la configuración del Editor por lotes. Configure el cuadro de diálogo para que coincida con las necesidades del componente: columnas disponibles y posibles acciones realizadas en la cuadrícula o en la búsqueda. Consulte [Propiedades de configuración del editor en lotes](#bulk-editor-configuration-properties) para obtener información sobre todas las propiedades de configuración.

Esta es una representación XML de los subnodos del cuadro de diálogo:

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### Propiedades de configuración del editor en lotes {#bulk-editor-configuration-properties}

Se pueden configurar todas las partes del editor en bloque. En la tabla siguiente se enumeran todas las propiedades de configuración del Editor por lotes.

<table>
 <tbody>
  <tr>
   <td>Nombre de la propiedad</td>
   <td>Definición</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Ruta raíz de búsqueda</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Consulta de búsqueda</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>True para habilitar el modo de contenido: las propiedades se leen en el nodo jcr:content y no en el nodo de resultados de búsqueda</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>Propiedades buscadas (valores seleccionados de colsSelection mostrados como casillas de verificación)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>Propiedades buscadas adicionales (mostradas en un campo de texto separadas por comas)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>True para realizar la consulta al cargar la página</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>Selección de propiedades buscadas (mostradas como casillas de verificación)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True para mostrar únicamente la cuadrícula y no el panel de búsqueda (no olvide establecer initialSearch en true)</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>True para contraer el panel de búsqueda de forma predeterminada</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>Ocultar campo de ruta raíz</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>Ocultar campo de consulta</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>Ocultar campo de modo de contenido</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>Ocultar campo de selección de columnas</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>Ocultar campo de columnas adicionales</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>Ocultar botón de búsqueda</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>Ocultar botón de guardar</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>Ocultar botón de exportación</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Ocultar botón de importación</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Ocultar texto de número de resultado de búsqueda de cuadrícula</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Ocultar botón de inserción de cuadrícula</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Ocultar botón de eliminación de cuadrícula</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Ocultar columna de "ruta" de cuadrícula</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>Ruta al servlet de consulta</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>Ruta para exportar el servlet</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>Ruta para importar servlet</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>Tipo de recurso agregado al nodo cuando se inserta una fila</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>Guardar configuración del widget de botón</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>Configuración del widget del botón de búsqueda</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>Configuración del widget del botón Exportar</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>Configuración del widget del botón Importar</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>Configuración del widget del panel de búsqueda</td>
  </tr>
  <tr>
   <td>rejilla</td>
   <td>Configuración del widget de cuadrícula</td>
  </tr>
  <tr>
   <td>almacenar</td>
   <td>Configuración de tienda</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>Configuración del modelo de columna de cuadrícula</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>Configuración del widget rootPath</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>Configuración del widget queryParams</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>configuración del widget contentMode</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>configuración del widget colsSelection</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>configuración del widget extraCols</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>Configuración de metadatos de columna. Las propiedades posibles son (aplicadas a todas las celdas de la columna): <br />
    <ul>
     <li>cellStyle: estilo html </li>
     <li>cellCls: clase css </li>
     <li>readOnly: true para no poder cambiar el valor </li>
     <li>casilla de verificación: true para definir todas las celdas de la columna como casillas de verificación (valores true/false) </li>
     <li>forcedPosition: valor entero para especificar dónde se debe colocar la columna en la cuadrícula (entre 0 y 1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configuración de metadatos de columnas {#columns-metadata-configuration}

Puede configurar para cada columna:

* propiedades de visualización: estilo html, clase CSS y solo lectura

* una casilla
* una posición forzada

Columnas CSS y de solo lectura

El editor en bloque tiene tres configuraciones de columna:

* Cell CSS class name (cellCls): un nombre de clase CSS que se agrega a cada celda de la columna configurada.
* Cell style (cellStyle): un estilo de HTML que se añade a cada celda de la columna configurada.
* Solo lectura (readOnly): solo lectura se establece para cada celda de la columna configurada.

La configuración debe definirse como la siguiente:

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

El siguiente ejemplo se encuentra en el componente productlist (/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata):

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**Casilla de verificación**

Si la propiedad checkbox configuration se establece en true, todas las celdas de la columna se representan como casillas de verificación. Una casilla marcada envía **true** al servidor Guardar servlet, **false** en caso contrario. En el menú del encabezado, también puede **seleccionar todo** o **seleccionar ninguno**. Estas opciones se activan si el encabezado seleccionado es el encabezado de una columna de casilla de verificación.

En el ejemplo anterior, la columna de selección contiene solo casillas de verificación como checkbox=&quot;true&quot;.

**Posición forzada**

Los metadatos de posición forzada forcedPosition le permiten especificar dónde se coloca la columna dentro de la cuadrícula: 0 es el primer lugar y &lt;número de columnas>-1 es la última posición. Se ignora cualquier otro valor.

En el ejemplo anterior, la columna de selección es la primera columna como forcedPosition=&quot;0&quot;.

### Servlet de consulta {#query-servlet}

De manera predeterminada, el servlet de consulta se encuentra en `/libs/wcm/core/components/bulkeditor/json.java`. Puede configurar otra ruta para recuperar los datos.

El servlet de consulta funciona de la siguiente manera: recibe una consulta GQL y las columnas que se van a devolver, calcula los resultados y devuelve los resultados al Editor por lotes como un flujo JSON.

En el caso del componente Lista de productos, los dos parámetros enviados al servlet de Consulta son los siguientes:

* query: &quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
* cols: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

Y la secuencia JSON se devuelve de la siguiente manera:

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

Cada visita individual corresponde a un nodo y a sus propiedades, y se muestra como una fila en la cuadrícula.

Puede ampliar el servlet de consulta para devolver un modelo de herencia complejo o nodos devueltos almacenados en un lugar lógico específico. El servlet de consulta se puede utilizar para realizar cualquier tipo de cálculo complejo. La cuadrícula puede mostrar filas que son un agregado de varios nodos en el repositorio. La modificación y el guardado de estas filas deben ser administrados en ese caso por Save Servlet.

### Guardar servlet {#save-servlet}

En la configuración predeterminada del Editor por lotes, cada fila es un nodo y la ruta de este nodo se almacena en el registro de fila. El Editor por lotes mantiene el vínculo entre la fila y el nodo a través de la ruta jcr. Cuando un usuario edita la cuadrícula, se crea una lista de todas las modificaciones. Cuando un usuario hace clic en **Guardar**, se envía una consulta POST a cada ruta con los valores de propiedades actualizados. Esta es la base del concepto de Sling y funciona bien si cada celda es una propiedad del nodo. Sin embargo, si el servlet de consulta está implementado para realizar el cálculo de herencia, este modelo no puede funcionar porque una propiedad devuelta por el servlet de consulta se puede heredar de otro nodo.

El concepto Guardar servlet implica que las modificaciones no se publican directamente en cada nodo, sino que se publican en un servlet que realiza el trabajo de guardado. Esto ofrece a este servlet la posibilidad de analizar las modificaciones y guardar las propiedades en el nodo derecho.

Cada propiedad actualizada se envía al servlet en el siguiente formato:

* Nombre del parámetro: &lt;jcr path>/&lt;property name>

  Ejemplo: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valor: &lt;value>

  Ejemplo: 12123

El servlet debe saber dónde se almacena la propiedad catalogCode.

Una implementación predeterminada del servlet Guardar está disponible en /libs/wcm/bulkeditor/save/POST.jsp y se utiliza en el componente Lista de productos. Toma todos los parámetros de la solicitud (con un formato &lt;jcr path>/&lt;property name>) y escribe propiedades en los nodos mediante la API de JCR. También crea un nodo si no existen (filas insertadas en la cuadrícula).

No utilice el código predeterminado tal cual, ya que reimplementa lo que hace el servidor de forma nativa (una POST en &lt;jcr path>/&lt;property name>) y, por lo tanto, solo es un buen punto de partida para crear un servlet de guardado que pueda administrar un modelo de herencia de propiedades.
