---
title: Biblioteca de transcodificación de imágenes
description: Aprenda a configurar y utilizar la biblioteca de transcodificación de imágenes de Adobe, una solución de procesamiento de imágenes que puede realizar funciones principales de administración de imágenes, como codificación, transcodificación, remuestreo de imágenes y cambio de tamaño de imágenes.
contentOwner: AG
role: Admin
feature: Renditions,Developer Tools,Asset Processing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---

# Biblioteca de transcodificación de imágenes {#imaging-transcoding-library}

La biblioteca de transcodificación de imágenes de Adobe es una solución de procesamiento de imágenes propietaria que puede realizar funciones principales de administración de imágenes, como las siguientes:

* Codificación
* Transcodificación (conversión de formatos compatibles)
* Remuestreo de imágenes, con algoritmos de PS e Intel IPP
* Profundidad de bits y preservación del perfil de color
* Compresión de calidad JPEG
* Cambio de tamaño de imagen

La biblioteca de transcodificación de imágenes proporciona compatibilidad con CMYK y con alfa completo, excepto CMYK -Alpha.

Además de admitir una amplia gama de formatos y perfiles de archivo, la biblioteca de transcodificación de imágenes tiene ventajas significativas respecto a otras soluciones de terceros en cuanto a rendimiento, escalabilidad y calidad. Estas son algunas de las ventajas clave de utilizar la biblioteca de transcodificación de imágenes:

* **Escalas con mayor tamaño o resolución de archivo**: La escala se logra principalmente gracias a la capacidad patentada de la biblioteca de transcodificación de imágenes para cambiar el tamaño al descodificar archivos. Esta capacidad garantiza que el uso de la memoria en tiempo de ejecución siempre sea óptimo y no sea una función cuadrática de aumento del tamaño del archivo o de megapíxeles de resolución. La biblioteca de transcodificación de imágenes puede procesar archivos más grandes y de alta resolución (que contienen megapíxeles más altos). Las herramientas de terceros, como ImageMagick, no pueden gestionar archivos grandes ni bloqueos durante el procesamiento de dichos archivos.
* **Algoritmos de compresión y cambio de tamaño con calidad Photoshop**: Coherencia con el estándar de la industria en términos de calidad de muestreo descendente (bicúbico suave, nítido y automático) y calidad de compresión. La biblioteca de transcodificación de imágenes evalúa aún más el factor de calidad de la imagen de entrada y utiliza de forma inteligente tablas y ajustes de calidad óptimos para la imagen de salida. Esta capacidad produce archivos de tamaño óptimo sin poner en riesgo la calidad visual.
* **Alto rendimiento:** El tiempo de respuesta es menor y el rendimiento es consistentemente mayor que ImageMagick. Por lo tanto, la biblioteca de transcodificación de imágenes debe reducir el tiempo de espera de los usuarios y el coste del alojamiento.
* **Escalar mejor con carga simultánea:** La biblioteca de transcodificación de imágenes funciona de manera óptima en condiciones de carga simultánea. Proporciona un alto rendimiento con un rendimiento de CPU óptimo, uso de memoria y bajo tiempo de respuesta, lo que ayuda a reducir el coste del alojamiento.

## Plataformas compatibles {#supported-platforms}

La biblioteca de transcodificación de imágenes solo está disponible para distribuciones RHEL 8, RHEL 7 y CentOS 7.

>[!NOTE]
>
>Mac OS y otras distribuciones *nix (por ejemplo, Debian y Ubuntu) no son compatibles.

## Uso {#usage}

Los argumentos de la línea de comandos para la biblioteca de transcodificación de imágenes pueden incluir los siguientes:

```shell
 -destMime PNG/JPEG: Mime type of output rendition
 -BitDepth 8/16: Preserves Bit Depth. Bitdepth '4' is automatically converted to '8'
 -preserveBitDepth: Downscales Bit Depth (No upscaling)
 -preserveCMYK: Preserves CMYK color space
 -jpegQuality: Provides jpeg quality parameter (0-12 , corresponding to Photoshop qualities)
 -ResamplingMethod BiCubic/Lanczos/PSBicubic: Provides resampling methods. PSBicubic is a Photoshop quality resampling method.
 -resize
```

Puede configurar las siguientes opciones para el parámetro `-resize`:

* `X`: funciona de forma similar a [!DNL Experience Manager]. Por ejemplo, -resize 319.
* `WxH`: la proporción de aspecto no se mantiene, por ejemplo, `-resize 319x319`.
* `Wx`: corrige la anchura y calcula la altura manteniendo la relación de aspecto. Por ejemplo, `-resize 319x`.
* `xH`: corrige la altura y calcula la anchura manteniendo la relación de aspecto. Por ejemplo, `-resize x319`.

```shell
 -AllowUpsampling (Resizes smaller images)
 -input <fileName>
 -output <fileName>
```

## Configurar biblioteca de transcodificación de imágenes {#configuring-imaging-transcoding-library}

Para configurar el procesamiento de ITL, cree un archivo de configuración y actualice el flujo de trabajo para ejecutarlo.

### Crear archivo de configuración para el paquete extraído {#create-conf-file}

Para configurar la biblioteca, cree un archivo CONF para indicar las bibliotecas siguiendo los pasos siguientes. Necesita permisos de administrador o de raíz.

1. Descargue el paquete de la biblioteca de transcodificación de imágenes [de Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/aem630/product/assets/aem-assets-imaging-transcoding-library-pkg) e instálelo mediante el Administrador de paquetes. El paquete es compatible con [!DNL Experience Manager] 6.5.

1. Para conocer un identificador de paquete para `com.day.cq.dam.cq-dam-switchengine`, inicia sesión en la consola web y haz clic en **[!UICONTROL OSGi]** > **[!UICONTROL Paquetes]**. Como alternativa, para abrir la consola de paquetes, acceda a la URL `https://[aem_server:[port]/system/console/bundles/`. Busque el paquete `com.day.cq.dam.cq-dam-switchengine` y su ID.

1. Asegúrese de que se extraen todas las bibliotecas necesarias comprobando la carpeta con el comando `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/`, donde el nombre de la carpeta se construye con el ID de paquete. Por ejemplo, el comando es `ls -la /aem65/author/crx-quickstart/launchpad/felix/bundle588/data/binaries/` si el identificador del paquete es `588`.

1. Crear `SWitchEngineLibs.conf` archivo para vincular a la biblioteca.

   ```shell
   cd `/etc/ld.so.conf.d`
   touch SWitchEngineLibs.conf
   vi SWitchEngineLibs.conf
   ```

1. Agregar la ruta de acceso `/aem65/author/crx-quickstart/launchpad/felix/bundle<id>/data/binaries/` al archivo conf mediante el comando `cat SWitchEngineLibs.conf`.

1. Ejecute el comando `ldconfig` para crear los vínculos y la caché necesarios.

1. En la cuenta que se usa para iniciar [!DNL Experience Manager], edite el archivo `.bash_profile`. Agregue `LD_LIBRARY_PATH` agregando lo siguiente.

   ```shell
   LD_LIBRARY_PATH=.
   export LD_LIBRARY_PATH
   ```

1. Para asegurarse de que el valor de la ruta de acceso está establecido en `.`, utilice el comando `echo $LD_LIBRARY_PATH`. El resultado debe ser `.`. Si el valor no está establecido en `.`, reinicie la sesión.

### Configurar flujo de trabajo de [!UICONTROL DAM Update Asset] {#configure-dam-asset-update-workflow}

Actualice el flujo de trabajo [!UICONTROL DAM Update Asset] para usar la biblioteca para procesar imágenes.

1. En la interfaz de usuario de [!DNL Experience Manager], seleccione **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.

1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, abra el modelo de flujo de trabajo **[!UICONTROL Recurso de actualización DAM]** en modo de edición.

1. Abra el paso de proceso de **[!UICONTROL Procesar miniaturas]**. En la ficha **[!UICONTROL Miniaturas]**, agregue los tipos MIME para los que desea omitir el proceso predeterminado de generación de miniaturas en la lista **[!UICONTROL Omitir tipos MIME]**.
Por ejemplo, si desea crear miniaturas para una imagen de TIFF mediante la biblioteca de transcodificación de imágenes, especifique `image/tiff` en el campo **[!UICONTROL Omitir tipos MIME]**.

1. En la ficha **[!UICONTROL Imagen Web habilitada]**, agregue los tipos MIME para los que desea omitir el proceso predeterminado de generación de representación web en **[!UICONTROL Lista para omitir]**. Por ejemplo, si omitió el tipo MIME `image/tiff` en el paso anterior, agregue `image/tiff` a la lista de omisión.

1. Abra las miniaturas de **[!UICONTROL EPS (con tecnología de ImageMagick)]** paso y vaya a la pestaña **[!UICONTROL Argumentos]**. En la lista **[!UICONTROL Tipos MIME]**, agregue los tipos MIME que desea que procese la biblioteca de transcodificación de imágenes. Por ejemplo, si omitió el tipo MIME `image/tiff` en el paso anterior, agregue `image/jpeg` a la lista **[!UICONTROL Tipos MIME]**.

1. Quite los comandos predeterminados, si los hay.

1. Alternar panel lateral y, en la lista de pasos, agregar **[!UICONTROL Controlador SWitchEngine]**.

1. Agregue comandos al controlador [!UICONTROL SwitchEngine] en función de sus requisitos personalizados. Ajuste los parámetros de los comandos que especifique para satisfacer sus necesidades. Por ejemplo, si desea conservar el perfil de color de la imagen de JPEG, agregue los siguientes comandos a la lista **[!UICONTROL Comandos]**:

   * `SWitchEngine -input ${file} -destMime PNG -resize 48 -output ${directory}cq5dam.thumbnail.48.48.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 140x100 -output ${directory}cq5dam.thumbnail.140.100.png`
   * `SWitchEngine -input ${file} -destMime PNG -resize 319 -output ${directory}cq5dam.thumbnail.319.319.png`
   * `SWitchEngine -input ${file} -destMime JPEG -resize 1280 -preserveCMYK -output ${directory}cq5dam.web.1280.1280.jpeg`

   ![chlimage](assets/chlimage_1-199.png)

1. (Opcional) Genere miniaturas de una representación intermedia con un solo comando. La representación intermedia actúa como fuente para generar representaciones estáticas y web. Este método es más rápido que el anterior. Sin embargo, no puede aplicar parámetros personalizados a las miniaturas mediante este método.

   ![chlimage](assets/chlimage_1-200.png)

1. Para generar representaciones web, configure los parámetros en la ficha **[!UICONTROL Imagen habilitada para web]**.

1. Sincronizar el modelo de flujo de trabajo [!UICONTROL DAM Update Asset] actualizado. Guarde el flujo de trabajo.

Para comprobar la configuración, cargue una imagen de TIFF y supervise el archivo error.log. Observará `INFO` mensajes con menciones de `SwitchEngineHandlingProcess execute: executing command line`. Los registros mencionan las representaciones generadas. Una vez completado el flujo de trabajo, puede ver las nuevas representaciones en [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Artículo de tipos MIME admitidos](assets-formats.md#supported-image-transcoding-library)
