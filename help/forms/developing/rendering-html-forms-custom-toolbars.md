---
title: Procesar formularios HTML con barras de herramientas personalizadas
description: Utilice el servicio Forms para personalizar una barra de herramientas que se procesa con un formulario de HTML. Puede procesar un formulario HTML Forms con una barra de herramientas personalizada mediante la API de Java y una API de servicio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: e4b02c17-dcd1-424b-9aee-579a8346b4d7
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2328'
ht-degree: 1%

---

# Procesar formularios HTML con barras de herramientas personalizadas {#rendering-html-forms-with-customtoolbars}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

## Procesar HTML Forms con barras de herramientas personalizadas {#rendering-html-forms-with-custom-toolbars}

El servicio Forms permite personalizar una barra de herramientas que se procesa con un formulario de HTML. Se puede personalizar una barra de herramientas para modificar su aspecto al anular los estilos CSS predeterminados y agregar un comportamiento dinámico al anular los scripts de Java. Una barra de herramientas se personaliza mediante un archivo XML denominado fscmenu.xml. De forma predeterminada, el servicio Forms recupera este archivo desde una ubicación URI especificada internamente.

>[!NOTE]
>
>Esta ubicación de URI se encuentra en el archivo adobe-forms-core.jar, que se encuentra en el archivo adobe-forms-dsc.jar. El archivo adobe-forms-dsc.jar se encuentra en la carpeta C:\Adobe\Adobe_Experience_Manager_forms\ (C:\ es el directorio de instalación). Puede utilizar una herramienta de extracción de archivos, como Win RAR, para abrir Adobe.

Puede copiar el archivo fscmenu.xml desde esta ubicación, modificarlo para que se ajuste a sus necesidades y, a continuación, colocarlo en una ubicación URI personalizada. A continuación, mediante la API del servicio de Forms, establezca las opciones en tiempo de ejecución que resultan en el servicio de Forms mediante el archivo fscmenu.xml desde la ubicación especificada. Estas acciones hacen que el servicio Forms procese un formulario de HTML que tiene una barra de herramientas personalizada.

Además del archivo fscmenu.xml, también necesita obtener los siguientes archivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS es la secuencia de comandos Java asociada a cada nodo. Es necesario proporcionar uno para el nodo `div#fscmenu` y, opcionalmente, para `ul#fscmenuItem` nodos. Los archivos JS implementan la funcionalidad principal de la barra de herramientas y funcionan los archivos predeterminados.

fscCSS es una hoja de estilos asociada a un nodo concreto. Los estilos de los archivos CSS especifican el aspecto de la barra de herramientas. *fscVCSS* es una hoja de estilo para una barra de herramientas vertical que se muestra a la izquierda del formulario de HTML procesado. *fscIECS* es una hoja de estilos que se usa para los formularios de HTML que se representan en Internet Explorer.

Asegúrese de que se hace referencia a todos los archivos anteriores en el archivo fscmenu.xml. Es decir, en el archivo fscmenu.xml, especifique las ubicaciones de los URI que apuntarán a estos archivos para que el servicio de Forms pueda localizarlos. De forma predeterminada, estos archivos están disponibles en ubicaciones de URI que comienzan con palabras clave internas `FSWebRoot` o `ApplicationWebRoot`.

Para personalizar la barra de herramientas, reemplace las palabras clave por la palabra clave externa `FSToolBarURI`. Esta palabra clave representa el URI que se pasa al servicio Forms en tiempo de ejecución (este método se muestra más adelante en esta sección).

También puede especificar las ubicaciones absolutas de estos archivos JS y CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. En este caso, no necesita usar la palabra clave `FSToolBarURI`.

>[!NOTE]
>
>No se recomienda mezclar las formas en que se hace referencia a estos archivos. Es decir, se debe hacer referencia a todos los URI mediante la palabra clave `FSToolBarURI` o una ubicación absoluta.

Puede obtener los archivos JS y CSS abriendo el archivo adobe-forms-&lt;appserver>.ear. Dentro de este archivo, abra adobe-forms-res.war. Todos estos archivos se encuentran en el archivo WAR. El archivo adobe-forms-&lt;appserver>.ear se encuentra en la carpeta de instalación de AEM forms (C:\ es el directorio de instalación). Puede abrir adobe-forms-&lt;appserver>.ear con una herramienta de extracción de archivos como WinRAR.

La siguiente sintaxis XML muestra un archivo fscmenu.xml de ejemplo.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>El texto en negrita representa los URI de los archivos CSS y JS a los que se debe hacer referencia.

Los siguientes elementos describen cómo se puede personalizar una barra de herramientas:

* Cambie los valores de los atributos `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (en el archivo fscmenu.xml) para reflejar las ubicaciones personalizadas de los archivos a los que se hace referencia mediante uno de los métodos descritos en esta sección (por ejemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Se deben especificar todos los archivos CSS y JS. Si no se modifica ninguno de los archivos, proporcione el predeterminado en la ubicación personalizada. Puede obtener los archivos predeterminados abriendo varios archivos como se describe en esta sección.
* Se permite proporcionar una referencia absoluta (por ejemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para cualquier archivo.
* Los archivos JS y CSS que requiere el nodo `div#fscmenu` son esenciales para la funcionalidad de la barra de herramientas. Los nodos individuales `ul#fscmenuItem` pueden tener o no archivos JS o CSS compatibles.

**Cambiando el valor local**

Al personalizar una barra de herramientas, puede cambiar su valor de configuración regional. Es decir, puede mostrarlo en otro idioma. La siguiente ilustración muestra una barra de herramientas personalizada que se muestra en francés.

>[!NOTE]
>
>No es posible crear una barra de herramientas personalizada en más de un idioma. Las barras de herramientas no pueden utilizar archivos XML diferentes basados en la configuración regional.

Para cambiar el valor de configuración regional de una barra de herramientas, asegúrese de que el archivo fscmenu.xml contiene el idioma que desea mostrar. La siguiente sintaxis XML muestra el archivo fscmenu.xml que se utiliza para mostrar una barra de herramientas en francés.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Los tutoriales rápidos asociados a esta sección utilizan este archivo XML para mostrar una barra de herramientas personalizada en francés, como se muestra en la ilustración anterior.

Especifique también un valor de configuración regional válido invocando el método `setLocale` del objeto `HTMLRenderSpec` y pasando un valor de cadena que especifique el valor de configuración regional. Por ejemplo, pase `fr_FR` para especificar francés. El servicio Forms está empaquetado con barras de herramientas localizadas.

>[!NOTE]
>
>Antes de procesar un formulario de HTML que utilice una barra de herramientas personalizada, debe saber cómo se procesan los formularios de HTML. (Consulte [Procesar Forms como HTML](/help/forms/developing/rendering-forms-html.md)).

Para obtener más información acerca del servicio Forms, consulte [Referencia de servicios para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumen de los pasos {#summary-of-steps}

Para procesar un formulario de HTML que contenga una barra de herramientas personalizada, realice estas tareas:

1. Incluir archivos de proyecto.
1. Cree un objeto de API de Java de Forms.
1. Hacer referencia a un archivo XML fscmenu personalizado.
1. Procesar un formulario de HTML.
1. Escriba el flujo de datos del formulario en el explorador web del cliente.

**Incluir archivos de proyecto**

Incluya los archivos necesarios en el proyecto de desarrollo. Si está creando una aplicación cliente con Java, incluya los archivos JAR necesarios. Si utiliza servicios web, incluya los archivos proxy.

**Crear un objeto de API Java de Forms**

Para poder realizar mediante programación una operación compatible con el servicio Forms, debe crear un objeto de cliente de Forms.

**Hacer referencia a un archivo XML fscmenu personalizado**

Para procesar un formulario de HTML que contenga una barra de herramientas personalizada, haga referencia a un archivo XML fscmenu que describa la barra de herramientas. (Esta sección proporciona dos ejemplos de un archivo XML fscmenu.) Asegúrese también de que el archivo fscmenu.xml especifica correctamente las ubicaciones de todos los archivos a los que se hace referencia. Como se mencionó anteriormente en esta sección, asegúrese de que la palabra clave `FSToolBarURI` o sus ubicaciones absolutas hacen referencia a todos los archivos.

**Procesar un formulario de HTML**

Para procesar un formulario de HTML, especifique un diseño de formulario que se haya creado en Designer y guardado como archivo XDP. Seleccione también un tipo de transformación de HTML. Por ejemplo, puede especificar el tipo de transformación de HTML que procesa un HTML dinámico para Internet Explorer 5.0 o posterior.

El procesamiento de un formulario de HTML también requiere valores, como valores URI para el procesamiento de otros tipos de formulario.

**Escriba el flujo de datos del formulario en el explorador web del cliente**

Cuando el servicio Forms procesa un formulario de HTML, devuelve un flujo de datos de formulario que debe escribir en el explorador web del cliente para que los usuarios puedan ver el formulario de HTML.

**Consulte también**

[Procesar un formulario HTML con una barra de herramientas personalizada mediante la API de Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Representar un formulario HTML con una barra de herramientas personalizada mediante la API de servicio web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Inicio rápido de la API del servicio de Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Procesar formularios PDF interactivos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Procesar formularios como HTML](/help/forms/developing/rendering-forms-html.md)

[Crear aplicaciones web que procesen Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Procesar un formulario HTML con una barra de herramientas personalizada mediante la API de Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Procese un formulario HTML que contenga una barra de herramientas personalizada mediante la API de servicio de Forms (Java):

1. Incluir archivos de proyecto

   Incluya archivos JAR de cliente, como adobe-forms-client.jar, en la ruta de clase del proyecto Java.

1. Creación de un objeto de API de Java de Forms

   * Cree un objeto `ServiceClientFactory` que contenga propiedades de conexión.
   * Cree un objeto `FormsServiceClient` utilizando su constructor y pasando el objeto `ServiceClientFactory`.

1. Hacer referencia a un archivo XML fscmenu personalizado

   * Crear un objeto `HTMLRenderSpec` mediante su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque el método `setHTMLToolbar` del objeto `HTMLRenderSpec` y pase un valor de enumeración `HTMLToolbar`. Por ejemplo, para mostrar una barra de herramientas vertical de HTML, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando el método `setToolbarURI` del objeto `HTMLRenderSpec` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando el método `setLocale` del objeto `HTMLRenderSpec` y pasando un valor de cadena que especifique el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >Los inicios rápidos asociados con esta sección establecen este valor en `fr_FR`*.*

1. Procesar un formulario de HTML

   Invoque el método `renderHTMLForm` del objeto `FormsServiceClient` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valor de enumeración `TransformTo` que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con Dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Objeto `com.adobe.idp.Document` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase un objeto `com.adobe.idp.Document` vacío.
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un objeto `URLSpec` que almacena valores de URI necesarios para procesar un formulario de HTML.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este es un parámetro opcional y puede especificar `null` si no desea adjuntar archivos al formulario.

   El método `renderHTMLForm` devuelve un objeto `FormsResult` que contiene una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `com.adobe.idp.Document` invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `com.adobe.idp.Document` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `com.adobe.idp.Document`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se use para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree un objeto `java.io.InputStream` invocando el método `getInputStream` del objeto `com.adobe.idp.Document`.
   * Cree una matriz de bytes y rellénela con la secuencia de datos de formulario invocando el método `read` del objeto `InputStream` y pasando la matriz de bytes como argumento.
   * Invoque el método `write` del objeto `javax.servlet.ServletOutputStream` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Inicio rápido (modo SOAP): Procesar un formulario HTML con una barra de herramientas personalizada mediante la API de Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Incluir archivos de biblioteca Java de AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Estableciendo propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Representar un formulario HTML con una barra de herramientas personalizada mediante la API de servicio web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Procese un formulario de HTML que contenga una barra de herramientas personalizada mediante la API del servicio web de Forms:

1. Incluir archivos de proyecto

   * Cree clases de proxy Java que consuman el WSDL del servicio Forms.
   * Incluya las clases de proxy Java en la ruta de clase.

1. Creación de un objeto de API de Java de Forms

   Cree un objeto `FormsService` y establezca los valores de autenticación.

1. Hacer referencia a un archivo XML fscmenu personalizado

   * Crear un objeto `HTMLRenderSpec` mediante su constructor.
   * Para procesar un formulario de HTML con una barra de herramientas, invoque el método `setHTMLToolbar` del objeto `HTMLRenderSpec` y pase un valor de enumeración `HTMLToolbar`. Por ejemplo, para mostrar una barra de herramientas vertical de HTML, pase `HTMLToolbar.Vertical`.
   * Especifique la ubicación del archivo XML fscmenu invocando el método `setToolbarURI` del objeto `HTMLRenderSpec` y pasando un valor de cadena que especifica la ubicación URI del archivo XML.
   * Si corresponde, establezca el valor de configuración regional invocando el método `setLocale` del objeto `HTMLRenderSpec` y pasando un valor de cadena que especifique el valor de configuración regional. El valor predeterminado es inglés.

   >[!NOTE]
   >
   >Los inicios rápidos asociados con esta sección establecen este valor en `fr_FR`*.*

1. Procesar un formulario de HTML

   Invoque el método `renderHTMLForm` del objeto `FormsService` y pase los siguientes valores:

   * Un valor de cadena que especifica el nombre del diseño del formulario, incluida la extensión del nombre de archivo. Si hace referencia a un diseño de formulario que forma parte de una aplicación de Forms, asegúrese de especificar la ruta de acceso completa, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valor de enumeración `TransformTo` que especifica el tipo de preferencia de HTML. Por ejemplo, para procesar un formulario de HTML compatible con Dynamic HTML para Internet Explorer 5.0 o posterior, especifique `TransformTo.MSDHTML`.
   * Objeto `BLOB` que contiene datos para combinar con el formulario. Si no desea combinar datos, pase `null`.
   * El objeto `HTMLRenderSpec` que almacena las opciones de tiempo de ejecución de HTML.
   * Un valor de cadena que especifica el valor del encabezado `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Puede pasar una cadena vacía si no desea establecer este valor.
   * Un objeto `URLSpec` que almacena valores de URI necesarios para procesar un formulario de HTML.
   * Objeto `java.util.HashMap` que almacena datos adjuntos de archivos. Este parámetro es opcional y puede especificar `null` si no desea adjuntar archivos al formulario.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método `renderHTMLForm`. Este valor de parámetro almacena el formulario procesado.
   * Un objeto `com.adobe.idp.services.holders.BLOBHolder` vacío que se rellena con el método `renderHTMLForm`. Este parámetro almacena los datos XML de salida.
   * Un objeto `javax.xml.rpc.holders.LongHolder` vacío que se rellena con el método `renderHTMLForm`. Este argumento almacena el número de páginas del formulario.
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método `renderHTMLForm`. Este argumento almacena el valor de configuración regional.
   * Un objeto `javax.xml.rpc.holders.StringHolder` vacío que se rellena con el método `renderHTMLForm`. Este argumento almacena el valor de procesamiento de HTML que se utiliza.
   * Un objeto `com.adobe.idp.services.holders.FormsResultHolder` vacío que contendrá los resultados de esta operación.

   El método `renderHTMLForm` rellena el objeto `com.adobe.idp.services.holders.FormsResultHolder` que se pasa como el último valor de argumento con una secuencia de datos de formulario que debe escribirse en el explorador web del cliente.

1. Escribir el flujo de datos del formulario en el explorador web del cliente

   * Cree un objeto `FormResult` obteniendo el valor del miembro de datos `value` del objeto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Cree un objeto `BLOB` que contenga datos de formulario invocando el método `getOutputContent` del objeto `FormsResult`.
   * Obtenga el tipo de contenido del objeto `BLOB` invocando su método `getContentType`.
   * Establezca el tipo de contenido del objeto `javax.servlet.http.HttpServletResponse` invocando su método `setContentType` y pasando el tipo de contenido del objeto `BLOB`.
   * Cree un objeto `javax.servlet.ServletOutputStream` que se use para escribir el flujo de datos de formulario en el explorador web del cliente invocando el método `getOutputStream` del objeto `javax.servlet.http.HttpServletResponse`.
   * Cree una matriz de bytes y rellénela invocando el método `getBinaryData` del objeto `BLOB`. Esta tarea asigna el contenido del objeto `FormsResult` a la matriz de bytes.
   * Invoque el método `write` del objeto `javax.servlet.http.HttpServletResponse` para enviar el flujo de datos de formulario al explorador web del cliente. Pase la matriz de bytes al método `write`.

**Consulte también**

[Invocar AEM Forms con codificación Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
