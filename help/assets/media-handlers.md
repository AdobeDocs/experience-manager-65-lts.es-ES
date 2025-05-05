---
title: Procesar recursos mediante controladores de medios y flujos de trabajo
description: Obtenga información acerca de los controladores de medios y cómo utilizar flujos de trabajo para realizar tareas en los recursos digitales.
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2113'
ht-degree: 3%

---

# Procesar recursos mediante controladores de medios y flujos de trabajo {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] incluye un conjunto de flujos de trabajo y controladores de medios predeterminados para procesar los recursos. Un flujo de trabajo define las tareas que se ejecutan en los recursos y, a continuación, delega las tareas específicas en los controladores de medios como, por ejemplo, la generación de miniaturas o la extracción de metadatos.

Se puede configurar un flujo de trabajo para que se ejecute automáticamente cuando se cargue un recurso de un tipo MIME concreto. Los pasos de procesamiento se definen en términos de una serie de controladores de medios [!DNL Assets]. [!DNL Experience Manager] proporciona algunos [controladores integrados](#default-media-handlers), y los adicionales pueden ser [desarrollados a medida](#creating-a-new-media-handler) o definidos delegando el proceso a una [herramienta de línea de comandos](#command-line-based-media-handler).

Los controladores de medios son servicios de [!DNL Assets] que realizan acciones específicas en los recursos. Por ejemplo, cuando se carga un archivo de audio MP3 en [!DNL Experience Manager], un flujo de trabajo déclencheur un controlador MP3 que extrae los metadatos y genera una miniatura. Los controladores de medios se utilizan con flujos de trabajo. Los tipos MIME más comunes son compatibles con [!DNL Experience Manager]. Se pueden realizar tareas específicas en los recursos ampliando o creando flujos de trabajo, ampliando o creando controladores de medios, o deshabilitando y habilitando controladores de medios.

>[!NOTE]
>
>Consulte la página [Formatos de recurso compatibles](assets-formats.md) para obtener una descripción de todos los formatos compatibles con [!DNL Assets] y las características compatibles con cada formato.

## Controladores de medios predeterminados {#default-media-handlers}

Los siguientes controladores de medios están disponibles en [!DNL Assets] y administran los tipos MIME más comunes:

<!-- TBD: Java versions should not be set to 1.5. Must be updated.
-->

| Nombre del controlador | Nombre del servicio (en la consola del sistema) | Tipos MIME admitidos |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL ControladorDeTexto] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL ControladorPdf] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL ControladorJpeg] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>Importante</b>: Un archivo MP3 cargado se [procesa mediante una biblioteca de terceros](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). La biblioteca calcula una longitud aproximada no precisa si el MP3 tiene una velocidad de bits variable (VBR). |
| [!UICONTROL ControladorZip] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL ControladorImagenEstándar] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL ControladorRecursosGenérico] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | reserva en caso de que no se encuentre ningún otro controlador para extraer datos de un recurso |

{style="table-layout:auto"}

Todos los controladores realizan las siguientes tareas:

* extraer todos los metadatos disponibles del recurso.
* crear una imagen en miniatura de un recurso.

Para ver los controladores de medios activos:

1. En su explorador, vaya a `https://localhost:4502/system/console/components`.
1. Haga clic en `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Se muestra una lista con todos los controladores de medios activos. Por ejemplo:

![chlimage_1-437](assets/chlimage_1-437.png)

## Uso de controladores de medios en flujos de trabajo para realizar tareas en recursos {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

Los controladores de medios son servicios que se utilizan con flujos de trabajo.

[!DNL Experience Manager] tiene algunos flujos de trabajo predeterminados para procesar los recursos. Para verlos, abra la consola Flujo de trabajo y haga clic en la ficha **[!UICONTROL Modelos]**: los títulos de flujo de trabajo que comienzan con [!DNL Assets] son los específicos de los recursos.

Los flujos de trabajo existentes se pueden ampliar y se pueden crear otros nuevos para procesar recursos según requisitos específicos.

En el siguiente ejemplo se muestra cómo mejorar el flujo de trabajo de **[!UICONTROL sincronización de AEM Assets]** para que se generen subrecursos para todos los recursos, excepto para los documentos PDF.

### Deshabilitar o habilitar un controlador de medios {#disabling-enabling-a-media-handler}

Los controladores de medios se pueden deshabilitar o habilitar a través de la consola de administración web de Apache Felix. Cuando el controlador de medios está deshabilitado, sus tareas no se realizan en los recursos.

Para habilitar o deshabilitar un controlador de medios:

1. En su explorador, vaya a `https://<host>:<port>/system/console/components`.
1. Haga clic en **[!UICONTROL Deshabilitar]** junto al nombre del controlador de medios. Por ejemplo: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Actualice la página: aparece un icono junto al controlador de medios que indica que está desactivado.
1. Para habilitar el controlador de medios, haga clic en **[!UICONTROL Habilitar]** junto al nombre del controlador de medios.

### Crear un controlador de medios {#creating-a-new-media-handler}

Para admitir un nuevo tipo de medios o ejecutar tareas específicas en un recurso, es necesario crear un controlador de medios. En esta sección se describe cómo proceder.

#### Clases e interfaces importantes {#important-classes-and-interfaces}

La mejor manera de iniciar una implementación es heredar de una implementación abstracta proporcionada que se ocupe de la mayoría de las cosas y proporcione un comportamiento predeterminado razonable: la clase `com.day.cq.dam.core.AbstractAssetHandler`.

Esta clase ya proporciona un descriptor de servicio abstracto. Por lo tanto, si ha heredado de esta clase y utiliza el complemento maven-sling, asegúrese de establecer el indicador de herencia en `true`.

Implemente los siguientes métodos:

* `extractMetadata()`: extrae todos los metadatos disponibles.
* `getThumbnailImage()`: crea una imagen en miniatura a partir del recurso pasado.
* `getMimeTypes()`: devuelve los tipos MIME del recurso.

Esta es una plantilla de ejemplo:

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

La interfaz y las clases incluyen:

* Interfaz `com.day.cq.dam.api.handler.AssetHandler`: esta interfaz describe el servicio que agrega compatibilidad con tipos MIME específicos. Añadir un tipo MIME requiere implementar esta interfaz. La interfaz contiene métodos para importar y exportar documentos específicos, para crear miniaturas y extraer metadatos.
* Clase `com.day.cq.dam.core.AbstractAssetHandler`: esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona funcionalidad utilizada comúnmente.
* Clase `com.day.cq.dam.core.AbstractSubAssetHandler`:
   * Esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona la funcionalidad utilizada comúnmente, además de la funcionalidad utilizada comúnmente para la extracción de subrecursos.
   * La mejor manera de iniciar una implementación es heredar de una implementación abstracta proporcionada que se ocupe de la mayoría de las cosas y proporcione un comportamiento predeterminado razonable: la clase com.day.cq.dam.core.AbstractAssetHandler.
   * Esta clase ya proporciona un descriptor de servicio abstracto. Por lo tanto, si ha heredado de esta clase y utiliza el complemento maven-sling, asegúrese de establecer el indicador de herencia en true.

Se deben implementar los siguientes métodos:

* `extractMetadata()`: este método extrae todos los metadatos disponibles.
* `getThumbnailImage()`: este método crea una imagen en miniatura a partir del recurso pasado.
* `getMimeTypes()`: este método devuelve los tipos MIME del recurso.

Esta es una plantilla de ejemplo:

package my.own.stuff; /&ast;&ast; &ast; @scr.component inherit=&quot;true&quot; &ast; @scr.service &ast;/ la clase pública MyMediaHandler amplía com.day.cq.dam.core.AbstractAssetHandler { // implementa las partes relevantes }

La interfaz y las clases incluyen:

* Interfaz `com.day.cq.dam.api.handler.AssetHandler`: esta interfaz describe el servicio que agrega compatibilidad con tipos MIME específicos. Añadir un tipo MIME requiere implementar esta interfaz. La interfaz contiene métodos para importar y exportar documentos específicos, para crear miniaturas y extraer metadatos.
* Clase `com.day.cq.dam.core.AbstractAssetHandler`: esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona funcionalidad utilizada comúnmente.
* Clase `com.day.cq.dam.core.AbstractSubAssetHandler`: esta clase sirve de base para todas las demás implementaciones de controladores de recursos y proporciona una funcionalidad utilizada comúnmente, además de otra funcionalidad utilizada comúnmente para la extracción de subrecursos.

#### Ejemplo: Creación de un controlador de texto específico {#example-create-a-specific-text-handler}

En esta sección, se crea un controlador de texto específico que genera miniaturas con una marca de agua.

Proceda como se indica a continuación:

Consulte [Herramientas de desarrollo](../sites-developing/dev-tools.md) para instalar y configurar Eclipse con un complemento de [!DNL Maven] y para configurar las dependencias necesarias para el proyecto [!DNL Maven].

Después de realizar el siguiente procedimiento, al cargar un archivo TXT en [!DNL Experience Manager], se extraen los metadatos del archivo y se generan dos miniaturas con una marca de agua.

1. En Eclipse, cree `myBundle` [!DNL Maven] proyecto:

   1. En la barra de menús, haga clic en **[!UICONTROL Archivo]** > **[!UICONTROL Nuevo]** > **[!UICONTROL Otro]**.
   1. En el cuadro de diálogo, expanda la carpeta [!DNL Maven], seleccione el proyecto [!DNL Maven] y, a continuación, haga clic en **[!UICONTROL Siguiente]**.
   1. Marque la casilla Crear un proyecto simple y el cuadro Usar ubicación predeterminada de Workspace y luego haga clic en **[!UICONTROL Siguiente]**.
   1. Definir un proyecto [!DNL Maven]:

      * Id. de grupo: `com.day.cq5.myhandler`.
      * ID del artefacto: myBundle.
      * Nombre: Mi paquete [!DNL Experience Manager].
      * Descripción: Este es mi paquete [!DNL Experience Manager].

   1. Haga clic en **[!UICONTROL Finalizar]**.

1. Establezca el compilador [!DNL Java™] en la versión 1.5:

   1. Haga clic con el botón derecho en el proyecto `myBundle` y seleccione [!UICONTROL Propiedades].
   1. Seleccione [!UICONTROL Compilador Java™] y establezca las siguientes propiedades en 1.5:

      * Nivel de cumplimiento del compilador
      * Compatibilidad de archivos .class generada
      * Compatibilidad con Source

   1. Haga clic en **[!UICONTROL Aceptar]**. En la ventana de diálogo, haga clic en **[!UICONTROL Sí]**.

1. Reemplace el código del archivo `pom.xml` por el siguiente código:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. Cree el paquete `com.day.cq5.myhandler` que contiene las clases [!DNL Java™] en `myBundle/src/main/java`:

   1. En myBundle, haga clic con el botón derecho en `src/main/java`, seleccione Nuevo y luego Empaquetar.
   1. Asígnele el nombre `com.day.cq5.myhandler` y haga clic en Finalizar.

1. Crear la clase [!DNL Java™] `MyHandler`:

   1. En [!DNL Eclipse], en `myBundle/src/main/java`, haga clic con el botón secundario en el paquete `com.day.cq5.myhandler`. Seleccione [!UICONTROL Nuevo] y después [!UICONTROL Clase].
   1. En la ventana de diálogo, asigne un nombre a la clase [!DNL Java™] `MyHandler` y haga clic en [!UICONTROL Finalizar]. [!DNL Eclipse] crea y abre el archivo `MyHandler.java`.
   1. En `MyHandler.java`, reemplace el código existente por el siguiente y, a continuación, guarde los cambios:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we do not want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile la clase [!DNL Java™] y cree el paquete:

   1. Haga clic con el botón derecho en el proyecto `myBundle`, seleccione **[!UICONTROL Ejecutar como]** y, a continuación, **[!UICONTROL Instalar Maven]**.
   1. El paquete `myBundle-0.0.1-SNAPSHOT.jar` (que contiene la clase compilada) se crea en `myBundle/target`.

1. En el explorador de CRX, cree un nodo en `/apps/myApp`. Nombre = `install`, Tipo = `nt:folder`.
1. Copie el paquete `myBundle-0.0.1-SNAPSHOT.jar` y guárdelo en `/apps/myApp/install` (por ejemplo, con WebDAV). El nuevo controlador de texto ahora está activo en [!DNL Experience Manager].
1. En su explorador, abra la [!UICONTROL Consola de administración web Apache Felix]. Seleccione la ficha [!UICONTROL Componentes] y deshabilite el controlador de texto predeterminado `com.day.cq.dam.core.impl.handler.TextHandler`.

## Controlador de medios basado en la línea de comandos {#command-line-based-media-handler}

[!DNL Experience Manager] le permite ejecutar cualquier herramienta de línea de comandos dentro de un flujo de trabajo para convertir recursos (como [!DNL ImageMagick]) y agregar la nueva representación al recurso. Instale únicamente la herramienta de línea de comandos en el disco que hospeda el servidor [!DNL Experience Manager] y agregue y configure un paso de proceso en el flujo de trabajo. El proceso invocado, denominado `CommandLineProcess`, también filtra según tipos MIME específicos y para crear varias miniaturas basadas en la nueva representación.

Las siguientes conversiones se pueden ejecutar y almacenar automáticamente en [!DNL Assets]:

* Transformación de EPS e IA usando [ImageMagick](https://www.imagemagick.org/script/index.php) y [Ghostscript](https://www.ghostscript.com/).
* Transcodificación de vídeo FLV con [FFmpeg](https://ffmpeg.org/).
* Codificación MP3 con [LAME](https://lame.sourceforge.io/).
* Procesamiento de audio mediante [SOX](https://sourceforge.net/projects/sox/).

>[!NOTE]
>
>En sistemas que no son Windows, la herramienta FFmpeg devuelve un error al generar representaciones para un recurso de vídeo que tiene una comilla simple (&#39;) en su nombre de archivo. Si el nombre del archivo de vídeo incluye una comilla simple, elimínelo antes de cargarlo en [!DNL Experience Manager].

El proceso `CommandLineProcess` realiza las siguientes operaciones en el orden indicado:

* Filtra el archivo según tipos MIME específicos, si se especifican.
* Crea un directorio temporal en el disco que hospeda el servidor [!DNL Experience Manager].
* Transmite el archivo original al directorio temporal.
* Ejecuta el comando definido por los argumentos del paso. El comando se está ejecutando en el directorio temporal con los permisos del usuario que ejecuta [!DNL Experience Manager].
* Transmite el resultado de nuevo a la carpeta de representación del servidor [!DNL Experience Manager].
* Elimina el directorio temporal.
* Crea miniaturas basadas en esas representaciones, si se especifican. El número y las dimensiones de las miniaturas se definen mediante los argumentos del paso.

### Ejemplo con [!DNL ImageMagick] {#an-example-using-imagemagick}

El siguiente ejemplo muestra cómo configurar el paso de proceso de la línea de comandos para que cada vez que se agregue un recurso con el tipo de correo electrónico miMIME GIF o TIFF a `/content/dam` en el servidor [!DNL Experience Manager], se cree una imagen volteada del original. También se crean tres miniaturas más de 140 x 100, 48 x 48 y 10 x 250.

Para ello, use [!DNL ImageMagick]. [!DNL ImageMagick] es un software gratuito de línea de comandos que se utiliza para crear, editar y componer imágenes de mapa de bits.

Instale [!DNL ImageMagick] en el disco que hospeda el servidor [!DNL Experience Manager]:

1. Instalar [!DNL ImageMagick]: consulte [Documentación de ImageMagick](https://www.imagemagick.org/script/download.php).
1. Configure la herramienta para que en la línea de comandos pueda ejecutar `convert`.
1. Para ver si la herramienta está instalada correctamente, ejecute el siguiente comando `convert -h` en la línea de comandos.

   Muestra una pantalla de ayuda con todas las opciones posibles de la herramienta de conversión.

   >[!NOTE]
   >
   >En algunas versiones de Windows, el comando convert puede no ejecutarse porque está en conflicto con la utilidad de conversión nativa que forma parte de la instalación de [!DNL Windows]. En este caso, mencione la ruta completa del software [!DNL ImageMagick] utilizado para convertir archivos de imagen en miniaturas. Por ejemplo, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. Para ver si la herramienta se ejecuta correctamente, agregue una imagen de JPG al directorio de trabajo y ejecute el comando convert `<image-name>.jpg -flip <image-name>-flipped.jpg` en la línea de comandos. Se añade una imagen volteada al directorio. A continuación, agregue el paso del proceso de la línea de comandos al flujo de trabajo **[!UICONTROL DAM Update Asset]**.
1. Vaya a la consola **[!UICONTROL Workflow]**.
1. En la ficha **[!UICONTROL Modelos]**, edite el modelo **[!UICONTROL Recurso de actualización DAM]**.
1. Cambie los [!UICONTROL argumentos] del paso **[!UICONTROL Representación habilitada para web]** a: `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. Guarde el flujo de trabajo.

Para probar el flujo de trabajo modificado, agregue un recurso a `/content/dam`.

1. En el sistema de archivos, obtenga una imagen de TIFF de su elección. Cambie el nombre a `myImage.tiff` y cópielo en `/content/dam`, por ejemplo, utilizando WebDAV.
1. Vaya a la consola **[!UICONTROL CQ5 DAM]**, por ejemplo, `https://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Abra el recurso **[!UICONTROL myImage.tiff]** y compruebe que se hayan creado la imagen volteada y las tres miniaturas.

#### Configurar el paso del proceso CommandLineProcess {#configuring-the-commandlineprocess-process-step}

En esta sección se describe cómo establecer los [!UICONTROL argumentos de proceso] de [!UICONTROL CommandLineProcess].

Separe los valores de [!UICONTROL Argumentos del proceso] con una coma y no lo inicie con un espacio en blanco.

| Argument-Format | Descripción |
|---|---|
| mime:&lt;tipo MIME> | Argumento opcional. El proceso se aplica si el recurso tiene el mismo tipo MIME que el del argumento. <br>Se pueden definir varios tipos MIME. |
| tn:&lt;width>:&lt;height> | Argumento opcional. El proceso crea una miniatura con las dimensiones definidas en el argumento. <br>Se pueden definir varias miniaturas. |
| cmd: &lt;comando> | Define el comando que se ejecuta. La sintaxis depende de la herramienta de línea de comandos. Solo se puede definir un comando. <br>Se pueden usar las siguientes variables para crear el comando:<br>`${filename}`: nombre del archivo de entrada, por ejemplo, original.jpg <br> `${file}`: nombre de ruta de acceso completo del archivo de entrada, por ejemplo, `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`: directorio del archivo de entrada, por ejemplo, `/tmp/cqdam0816.tmp` <br>`${basename}`: nombre del archivo de entrada sin su extensión, por ejemplo, original <br>`${extension}`: extensión del archivo de entrada, por ejemplo, JPG. |

Por ejemplo, si [!DNL ImageMagick] está instalado en el disco que hospeda el servidor [!DNL Experience Manager] y crea un paso de proceso utilizando [!UICONTROL CommandLineProcess] como implementación y los siguientes valores como [!UICONTROL Argumentos de proceso]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

A continuación, cuando se ejecute el flujo de trabajo, el paso solo se aplicará a los recursos que tienen `image/gif` o `mime:image/tiff` como `mime-types`. Crea una imagen volteada del original, la convierte en JPG y crea tres miniaturas con las dimensiones 140x100, 48x48 y 10x250.

Use los siguientes [!UICONTROL argumentos de proceso] para crear las tres miniaturas estándar con [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Use los siguientes [!UICONTROL argumentos de proceso] para crear la representación habilitada para web con [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>El paso [!UICONTROL CommandLineProcess] solo se aplica a los recursos (nodos de tipo `dam:Asset`) o a los descendientes de un recurso.

>[!MORELIKETHIS]
>
>* [Procesar recursos](assets-workflow.md)
