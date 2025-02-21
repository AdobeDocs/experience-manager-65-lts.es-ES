---
title: Uso de Translator para administrar diccionarios
description: AEM proporciona una consola para administrar las distintas traducciones de textos utilizados en la interfaz de usuario del componente
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a8f03f31dd636ee239cfc6f2b67a7573216cf0fe
workflow-type: tm+mt
source-wordcount: '2312'
ht-degree: 1%

---

# Uso de Translator para administrar diccionarios{#using-translator-to-manage-dictionaries}

AEM proporciona una consola para administrar las distintas traducciones de textos utilizados en la interfaz de usuario del componente. Esta consola está disponible en

`https://<hostname>:<port-number>/libs/cq/i18n/translator.html`

Utilice la herramienta de traducción para gestionar cadenas en inglés y sus traducciones. Los diccionarios se crean en el repositorio, por ejemplo, /apps/myproject/i18n.

La herramienta de traducción y los diccionarios que administra se utilizan para presentar la interfaz de usuario de los componentes en diferentes idiomas. Si desea traducir contenido generado por la página o el usuario, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md).

>[!CAUTION]
>
>Solo edite los diccionarios creados para su proyecto y que residan en `/apps`.
>
>Los diccionarios del sistema de AEM también están disponibles en esta herramienta. No cambie los diccionarios del sistema de AEM, ya que esto puede causar problemas con la interfaz de usuario de AEM. Además, los cambios se pueden perder tras la actualización. Los diccionarios del sistema de AEM se encuentran en `/libs`.

>[!NOTE]
>
>Aunque la herramienta de traducción tiene una interfaz de usuario clásica, se utiliza para la traducción de frases independientemente de la interfaz en la que se encuentren.

El traductor enumera los textos utilizados en AEM con las distintas traducciones lingüísticas:

![chlimage_1-205](assets/chlimage_1-205.png)

Puede buscar, filtrar y editar el inglés y los textos traducidos. También puede exportar diccionarios al formato XLIFF para traducirlos y, a continuación, importar las traducciones de nuevo en los diccionarios.

También es posible añadir diccionarios i18n a un proyecto de traducción desde esta consola. Puede crear uno o agregar uno a un proyecto existente.

1. Haga clic en **Traducir diccionario**.

   ![chlimage_1-206](assets/chlimage_1-206.png)

1. Seleccione las opciones Crear o Añadir según sus necesidades. Se abre un cuadro de diálogo.

   ![chlimage_1-207](assets/chlimage_1-207.png)

1. Rellene los campos según sea necesario y haga clic en Aceptar. ![chlimage_1-208](assets/chlimage_1-208.png)

1. Ahora puede hacer clic en **Aceptar** o ver el diccionario de Target.

   >[!NOTE]
   >
   >Para obtener más información sobre los proyectos de traducción, lea [Administración de proyectos de traducción](/help/sites-administering/tc-manage.md).

## Crear un diccionario {#creating-a-dictionary}

Cree un diccionario para administrar las cadenas de IU localizadas. Después de crear un diccionario, puede utilizar la herramienta de traducción para administrarlo.

1. Con CRXDE Lite, agregue el nodo raíz ( `sling:Folder`) del nuevo diccionario como la estructura que contendrá las definiciones de idioma:

   ` /apps/<projectName>/i18n`

   Por ejemplo, `/apps/myProject/i18n`

1. Añada la estructura de idioma necesaria debajo de esta raíz. Por ejemplo:

   ```shell
   /apps/myProject/i18n [sling:Folder]
       - de.json [nt:file] [mix:language]
           + jcr:language = de
       - fr.json [nt:file] [mix:language]
           + jcr:language = fr
   ```

   >[!NOTE]
   >
   >Esta es la estructura del [módulo i18n de Sling](https://sling.apache.org/site/internationalization-support.html).

1. Volver a cargar el traductor y la ruta del diccionario (por ejemplo, `/apps/myProject/i18n`) estarán disponibles en el selector desplegable de la barra de herramientas. Seleccione esta opción para empezar a añadir cadenas y sus traducciones.

   >[!NOTE]
   >
   >El traductor solo guardará las traducciones de los idiomas que estén realmente presentes debajo de la ruta (por ejemplo, `/apps/myProject/i18n`).
   >
   >Asegúrese de que se corresponden con los idiomas mostrados en la cuadrícula.

## Administrar cadenas de diccionario {#managing-dictionary-strings}

Utilice la herramienta de traducción para administrar las cadenas de los diccionarios. Puede añadir, modificar y eliminar cadenas en inglés, y también proporcionar cadenas traducidas.

>[!CAUTION]
>
>Solo edite los diccionarios creados para su proyecto y que residan en `/apps`.
>
>No cambie los diccionarios del sistema de AEM, ya que esto puede causar problemas con la interfaz de usuario de AEM. Además, los cambios se pueden perder tras la actualización. Los diccionarios del sistema de AEM se encuentran en `/libs`.

### Adición, cambio y eliminación de cadenas {#adding-changing-and-removing-strings}

Agregue cadenas en inglés a un diccionario que el componente haya internacionalizado. Agregue únicamente cadenas que estén internacionalizadas para que no desperdicie recursos traduciendo cadenas que no se utilicen.

Las cadenas que agregue a un diccionario deben coincidir exactamente con la cadena especificada en el código. Si la cadena en inglés predeterminada que se utiliza en el código no coincide con la cadena en inglés de un diccionario, la cadena traducida no aparece en la interfaz de usuario cuando es necesario. Las cadenas distinguen entre mayúsculas y minúsculas.

**Proporcionando sugerencias de traducción**

Utilice la propiedad Comment de la cadena del diccionario para proporcionar información al traductor y aclarar el significado de la cadena. Normalmente, la interfaz de usuario ayuda a los usuarios a determinar el significado de las palabras ambiguas. Sin embargo, el traductor no ve la cadena en el contexto de la interfaz de usuario. La sugerencia de traducción elimina la ambigüedad. Por ejemplo, un comentario ayuda al traductor a comprender que la palabra en inglés Request se utiliza como sustantivo en lugar de como verbo.

Las sugerencias de traducción también distinguen cadenas que son idénticas y tienen significados diferentes. Por ejemplo, la palabra Buscar puede ser un sustantivo o un verbo, que requiere dos entradas &quot;Buscar&quot; en el diccionario con dos sugerencias de traducción diferentes. El código que solicita la cadena también incluye la sugerencia de traducción para que se utilice la cadena correcta en la interfaz de usuario.

**Incluyendo variables indizadas**

Incluya variables en la cadena localizada para crear significado contextual en una frase. Por ejemplo, después de iniciar sesión en una aplicación web, la página de inicio muestra el mensaje &quot;Bienvenido de nuevo, administrador&quot;. Tiene dos mensajes en la bandeja de entrada&quot;. El contexto de página determina el nombre de usuario y el número de mensajes.

Para incluir variables en la cadena localizada, coloque índices entre corchetes en la ubicación de las variables en el primer argumento del método get. Utilice la sugerencia de localización para describir los valores. El traductor debe comprender el significado de las variables porque los distintos idiomas utilizan diferentes estructuras de oración.

Tenga en cuenta que [el código que solicita la cadena traducida](/help/sites-developing/i18n-dev.md#including-variables-in-localized-sentences) proporciona valores para las variables indizadas según el contexto.

Por ejemplo, la siguiente cadena aparece cuando un usuario inicia sesión en un sitio web y se incluye en el diccionario:

`Welcome back {0}. You have {1} messages.`

En el siguiente comentario se describen las variables:

`{0} = the user name, {1} = the number of items in the user's inbox`

**Modificar cadenas**

Cambie o quite cadenas en inglés a medida que se cambian o se eliminan en el código. Al cambiar una cadena, la cadena original se mantiene y se crea una nueva cadena que refleja el cambio. Antes de quitar una cadena, asegúrese de que ningún código la utiliza.

Utilice el siguiente procedimiento para añadir una cadena.

1. En el menú desplegable Diccionarios, seleccione el diccionario al que desea agregar una cadena. En el menú desplegable, los diccionarios se representan mediante su ruta en el repositorio.
1. Sobre la tabla Cadenas y traducciones, haga clic en Añadir.

   ![chlimage_1-209](assets/chlimage_1-209.png)

1. En el cuadro Cadena del cuadro de diálogo Agregar cadena, escriba la cadena en inglés. En el cuadro Comentario, escriba una sugerencia de traducción para el traductor si es necesario.
1. Haga clic en Aceptar.
1. Haga clic en Guardar.

   ![chlimage_1-210](assets/chlimage_1-210.png)

Utilice el siguiente procedimiento para cambiar una cadena en un diccionario.

1. En el menú desplegable Diccionarios, seleccione el diccionario que contiene la cadena que desea cambiar.
1. Haga doble clic en la cadena para cambiarla.
1. En el cuadro de diálogo Editar cadena, seleccione Modificar cadena o Comentario (Crea una copia).

   ![chlimage_1-211](assets/chlimage_1-211.png)

1. Modifique la cadena o el comentario y haga clic en Aceptar.
1. Haga clic en Guardar.

   ![chlimage_1-212](assets/chlimage_1-212.png)

Utilice el siguiente procedimiento para quitar una cadena de un diccionario.

1. En el menú desplegable Diccionarios, seleccione el diccionario del que desea quitar una cadena.
1. Haga clic en Quitar.

   ![chlimage_1-213](assets/chlimage_1-213.png)

1. Haga clic en Guardar.

   ![chlimage_1-214](assets/chlimage_1-214.png)

### Búsqueda de cadenas {#searching-for-strings}

La barra de búsqueda situada en la parte inferior de la herramienta Traductor proporciona opciones de selección de cadenas:

* **Filtrar por texto:** Un patrón que coincida con la cadena, comentario o traducciones en inglés. En la tabla solo aparecen los elementos que coinciden con todo o parte del patrón.
* **Cambios: Cualquiera, Modificado, Nuevo, Eliminado:** Mostrar elementos que se han cambiado y no se han guardado.

   * Cualquiera: muestra los elementos que se han modificado, añadido o eliminado.
   * Modificado: mostrar los elementos modificados.
   * Nuevo: mostrar los elementos añadidos.
   * Eliminados: muestra los elementos que se van a eliminar.
   * Varias selecciones: muestra los elementos que tienen todas las propiedades seleccionadas.

* **Tiene comentario**: mostrar elementos que tienen comentarios para los traductores.
* **Faltan traducciones:** Mostrar elementos en los que al menos un idioma no tiene traducción.

![chlimage_1-215](assets/chlimage_1-215.png)

1. En la barra de búsqueda, seleccione las opciones de filtrado.
1. Para filtrar con las opciones, haga clic en Filtrar.
1. Para quitar los filtros y ver todos los elementos del diccionario, haga clic en Borrar.

### Edición de cadenas traducidas {#editing-translated-strings}

Después de agregar la cadena en inglés a un diccionario, puede agregar traducciones de la cadena. También puede [exportar el diccionario](/help/sites-developing/i18n-translator.md#exporting-a-dictionary) para que lo traduzca un tercero.

1. Seleccione [el diccionario específico del proyecto](#creating-a-dictionary), ya que especifica la ruta de acceso en el repositorio que contiene las traducciones. Por ejemplo, seleccione **Diccionarios** como:

   `/apps/myProject/i18n`

   >[!CAUTION]
   >
   >Solo edite los diccionarios creados para su proyecto y que residan en `/apps`.
   >
   >Los diccionarios del sistema de AEM también están disponibles en esta herramienta. No cambie los diccionarios del sistema de AEM, ya que esto puede causar problemas con la interfaz de usuario de AEM. Además, los cambios se pueden perder tras la actualización. Los diccionarios del sistema de AEM se encuentran en `/libs`.

1. Para editar los textos traducidos para una de las cadenas, puede hacer lo siguiente:

   * Haga doble clic en el idioma apropiado para la cadena requerida para editar ese solo texto:

   ![chlimage_1-216](assets/chlimage_1-216.png)

   * Haga doble clic en los campos **Cadena** o **Comentario** de la cadena necesaria para abrir el cuadro de diálogo **Editar cadena**, edite las traducciones según sea necesario y, a continuación, haga clic en **Aceptar** para cerrar el cuadro de diálogo:

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. Haga clic en **Guardar** en la barra de herramientas para confirmar los cambios.

   >[!NOTE]
   >
   >Al hacer clic en **Restablecer y actualizar** (en lugar de **Guardar**), se revertirán los cambios realizados en los textos anteriores.

## Uso de traductores de terceros {#using-third-party-translators}

Para admitir el uso de servicios de traducción de terceros, la herramienta de traducción le permite exportar e importar diccionarios.

### Exportación de un diccionario {#exporting-a-dictionary}

Exporte un diccionario a un archivo XLIFF para que un servicio de terceros pueda traducir las cadenas de diccionario.

* Exporte un diccionario e incluya el inglés y los términos traducidos para un idioma.
* Exporte algunas o todas solo las cadenas en inglés.

Al exportar un archivo XLIFF e incluir un idioma, la estructura de nodos del diccionario del repositorio debe incluir ese idioma. Si no se incluye el idioma, se producen errores. Por ejemplo, para exportar el archivo XLIFF francés, la carpeta del diccionario debe incluir el nodo secundario `mix:language` denominado `fr`. (Consulte [Crear un diccionario](/help/sites-developing/i18n-translator.md#creating-a-dictionary).)

Utilice el siguiente procedimiento para exportar un archivo XLIFF para un idioma específico.

1. Abrir la herramienta de traducción `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Utilice el menú desplegable Diccionarios para seleccionar el diccionario que desea exportar.
1. Haga clic en Exportar > Exportar *XX* opciones Xliff completas, donde *XX* es el código de idioma de dos letras, como DE o FR.

   El archivo XLIFF se abre en una nueva pestaña o ventana.

1. Utilice los comandos del explorador web para guardar la página como un archivo en el sistema de archivos, como Archivo > Guardar página como.

Utilice el siguiente procedimiento para exportar todas o algunas de las cadenas sólo en inglés.

1. Abra la herramienta de traducción. `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Utilice el menú desplegable Diccionarios para seleccionar el diccionario que desea exportar.
1. Si va a exportar un subconjunto de las cadenas, seleccione los elementos del diccionario que desea exportar. Al seleccionar ningún elemento, se exportan todos los elementos.
1. Haga clic en Exportar > Exportar selección como Xliff (solo cadenas).
1. En el cuadro de diálogo que aparece, copie el texto y péguelo en un archivo de texto.

### Importación de un diccionario {#importing-a-dictionary}

Importe un archivo XLIFF en un diccionario para rellenar el diccionario. Cuando el diccionario incluye una traducción para una cadena en inglés y el archivo XLIFF contiene una traducción diferente para la misma cadena, se reemplaza la traducción del diccionario.

1. Abrir la herramienta de traducción `http://<host>:<port>/libs/cq/i18n/translator.html`
1. Haga clic en Importar > Traducciones XLIFF.
1. Seleccione el archivo que desea importar y haga clic en Aceptar.

## Administración de idiomas admitidos {#managing-supported-lanuages}

Agregar o quitar idiomas compatibles con la herramienta de traducción y que se proporcionan a los usuarios de las páginas web.

### Cambio de los idiomas enumerados en la tabla de diccionario {#changing-languages-listed-in-the-dictionary-table}

La herramienta Traductor incluye los siguientes idiomas en la tabla del diccionario:

* de - Alemán
* fr - francés
* it - Italiano
* es - Español
* ja: japonés
* pt-br - Portugués de Brasil
* zh-cn: chino simplificado
* zh-tw: chino tradicional (compatibilidad limitada)
* ko-kr - Coreano

Utilice el siguiente procedimiento para añadir o quitar idiomas.

1. Con CRXDE Lite, cree un nodo:

   `/etc/languages`

1. En este nodo, cree una propiedad:

   * **Nombre**: `languages`
   * **Tipo**: `Multi-String`
   * **Valor**: la lista de idiomas que desea mostrar. Por ejemplo:

      * fr
      * es

   >[!NOTE]
   >
   >Los códigos de idioma deben escribirse en minúsculas.

1. Haga clic en **Guardar todo** en CRXDE Lite y vuelva a cargar el traductor. La cuadrícula se actualizará para mostrar los idiomas definidos.

   >[!NOTE]
   >
   >El traductor solamente guardará las traducciones para los idiomas que están realmente [presentes en el diccionario](#creating-a-dictionary) (es decir, debajo de la ruta de acceso del diccionario como `/apps/myProject/i18n`).
   >
   >Asegúrese de que se corresponden con los idiomas mostrados en la cuadrícula.

### Disponibilidad de idiomas para los autores {#making-languages-available-to-authors}

Después de definir un diccionario para un idioma nuevo en su instancia de AEM, debe hacer que este esté disponible para que lo seleccionen los autores (por ejemplo, para usarlo en **Preferencias**):

1. Para cambiar la lista de idiomas disponibles en **Preferencias** de la consola **Seguridad**:

   1. Cree una superposición en el código de la aplicación para lo siguiente:

      ```
              /libs/cq/security/widgets/source/widgets/security/Preferences.js
       and update as required.
      ```

1. Para que el idioma esté disponible en **Preferencias** desde la consola de **Sitios web**, debe realizar los siguientes cambios en la aplicación:

   1. Cree una superposición para la estructura en:

      `/libs/cq/security/content/tools/userProperties`

   1. Dentro de la superposición, actualice la lista de idiomas en:

      `items/common/items /lang/options`

1. Guarde todo y vuelva a cargar la consola adecuada.

### Cambio de nombres de idiomas y países predeterminados {#changing-language-names-and-default-countries}

Varios países utilizan el mismo idioma, por ejemplo, Estados Unidos, el Reino Unido y Australia utilizan el inglés. Esto se indica mediante un código que indica idioma y país como `en_US`, `en_GB` y `en_AU`.

Los países predeterminados se utilizan al mostrar los indicadores (por ejemplo, en el cuadro de diálogo de copia de idioma), y se utilizan para resolver el país de un código de idioma.

>[!NOTE]
>
>Para las localizaciones administradas por el traductor anterior, solo funciona el idioma exacto. Si la lista desplegable de preferencia de idioma usa `en_uk`, debe haber un diccionario `en_uk` en el repositorio.

Para cambiar las definiciones predeterminadas:

1. La lista de idiomas se almacena en:

   `/libs/wcm/core/resources/languages`

   Superponga esto copiándolo en:

   `/apps/wcm/core/resources/languages`

   A continuación, cambie o amplíe la lista allí. La propiedad `defaultCountry` de un nodo de idioma (por ejemplo, `ja`) debe contener el código completo, como `ja_jp`, que definiría `jp` como el país predeterminado para el idioma `ja`.

1. Actualice el **Administrador de idioma CQ WCM**.

   * **Lista de idiomas**:

     La ruta a la lista de idiomas en el repositorio. Configure esto en la ubicación utilizada para la superposición:

     ```
            /apps/wcm/core/resources/languages
     ```

   Puede hacerlo mediante la consola web de OSGi:

   ```shell
   https://<hostname>:<port-number>/system/console/configMgr/com.day.cq.wcm.core.impl.LanguageManagerImpl
   ```

## Publicar diccionarios {#publishing-dictionaries}

Incorpore sus diccionarios al proceso de administración de versiones de sus aplicaciones de AEM. Por ejemplo, incluya el diccionario en el paquete de contenido de la aplicación para su implementación en la instancia de publicación. Esta estrategia ofrece las siguientes ventajas:

* Los diccionarios están disponibles para los componentes en su entorno de publicación.
* Los cambios en las cadenas de la interfaz de usuario de los componentes se implementan junto con las traducciones actualizadas.

Del mismo modo, la prueba de las cadenas de diccionario debe realizarse como parte del ciclo de vida normal del desarrollo de software.

>[!NOTE]
>
>No utilice la funcionalidad de publicación normal o la replicación para los diccionarios. En su lugar, los diccionarios deben tratarse del mismo modo que el código y la configuración. Esto incluye el uso del control de código fuente para realizar un seguimiento de los cambios y el uso de paquetes de contenido para aplicar los cambios a autor y publicación.

>[!NOTE]
>
>Al usar Dispatcher, debe [invalidar las páginas en caché](https://helpx.adobe.com/experience-manager/dispatcher/using/page-invalidate.html) para incluir nuevas cadenas de diccionario en las cadenas de componentes procesadas.
