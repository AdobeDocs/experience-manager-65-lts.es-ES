---
title: Crear temáticas de formularios adaptables personalizadas
description: Una temática de formulario adaptable es una biblioteca de cliente de Adobe Experience Manager que se utiliza para definir los estilos (aspecto y presentación) de un formulario adaptable. Aprenda a crear temáticas de formularios adaptables personalizadas.
content-type: reference
topic-tags: customization
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 56%

---

# Crear temáticas de formularios adaptables personalizadas {#creating-custom-adaptive-form-themes}

>[!CAUTION]
>
>Adobe Experience Manager (AEM) Forms proporciona la capacidad [Editor de temáticas](/help/forms/using/themes.md) para crear y modificar [temáticas](/help/forms/using/themes.md) de formularios adaptables. Realice los pasos enumerados en este artículo solo si ha actualizado desde una versión que no tiene [Editor de temáticas](/help/forms/using/themes.md) y ya tiene creada una inversión en temáticas con menos archivos CSS (método editor pre-tema).

## Requisitos previos {#prerequisites}

* Conocimiento del marco de trabajo LESS (CSS más inteligente)
* Crear una biblioteca de cliente en Adobe Experience Manager
* [Crear una plantilla de formulario adaptable](/help/forms/using/custom-adaptive-forms-templates.md) para utilizar la temática que cree

## Temática del formulario adaptable {#adaptive-form-theme}

Una **temática de formulario adaptable** es una biblioteca de cliente de AEM que se utiliza para definir los estilos (aspecto y presentación) de un formulario adaptable.

Puede crear una **plantilla adaptable** y aplicar la temática a la plantilla. Puede usar esta plantilla personalizada para crear un **formulario adaptable**.

![Formulario adaptable y biblioteca de cliente](assets/hierarchy.png)

## Crear una temática de formulario adaptable {#to-create-an-adaptive-form-theme}

>[!NOTE]
>
>El siguiente procedimiento se describe con nombres de ejemplo para objetos de AEM como nodos, propiedades y carpetas.
>
>Si sigue estos pasos y usa los nombres, la plantilla resultante debería aparecer de forma similar a la siguiente captura de pantalla:

![Captura de pantalla del formulario adaptable con la temática Forest](assets/thumbnail.png)
**Figura:** *Ejemplo de la temática Forest*

1. Crear un nodo de tipo `cq:ClientLibraryFolder` en el nodo `/apps`.

   Por ejemplo, cree el siguiente nodo:

   `/apps/myAfThemes/forestTheme`

1. Agregue una propiedad `categories` de cadena de varios valores al nodo y establezca su valor apropiadamente.

   Por ejemplo, establezca la propiedad en: `af.theme.forest`.

   ![Captura de pantalla del repositorio CRX](assets/3-2.png)

1. Agregue dos carpetas, `less` y `css` y un archivo `css.txt` al nodo creado en el paso 1:

   * `less` carpeta: Contiene los archivos de la variable `less` en los que define las variables `less` y `less mixins` que se utilizan para administrar los estilos .css.

     Esta carpeta consta de `less` archivos de variables, `less` archivos de mezcla, `less` archivos que definen estilos mediante mezclas y variables. Y todos estos `less` archivos se importan en styles.less.

   * `css` carpeta: Contiene los archivos .css en los que se definen los estilos estáticos que se utilizarán en la temática.

   **Archivos de variables Less**: estos son los archivos donde define o anula las variables que se usan para definir estilos CSS.

   Los formularios adaptables proporcionan variables predeterminadas definidas en los siguientes `.less` archivos:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less`
   * `/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   Los formularios adaptables también proporcionan variables de terceros definidas en:

   `/apps/clientlibs/fd/af/third-party/less/variables.less`

   Puede utilizar las variables `less` que se proporcionan con los formularios adaptables, puede anular estas variables o crear nuevas variables `less`.

   >[!NOTE]
   >
   >Al importar los archivos del preprocesador Less, en la instrucción import, especifique la ruta relativa de los archivos.

   Variables de anulación de ejemplo:

   ```css
   @button-background-color: rgb(19, 102, 44);
   @button-border-color: rgb(19, 102, 44);
   @button-border-size: 0px;
   @button-padding: 10px 15px;
   @button-font-color: #ffffff;
   ```

   Para anular la variable `less`:

   1. Importe variables de formulario adaptable predeterminadas:

      `/apps/clientlibs/fd/af/guidetheme/common/less/globalvariables.less/apps/clientlibs/fd/af/guidetheme/common/less/layoutvariables.less`

   1. A continuación, importe el archivo Less que incluya variables anuladas.

   Ejemplo de nuevas definiciones de variables:

   ```css
   @button-focus-bg-color: rgb(40, 208, 90);
   @button-hover-bg-color: rgb(30, 156, 67);
   ```

   **Archivos de mezcla Less:** puede definir las funciones que aceptan variables como argumentos. El resultado de estas funciones son los estilos resultantes. Utilice estas mezclas en diferentes estilos para evitar la repetición de estilos CSS.

   Los formularios adaptables proporcionan mezclas integradas definidas en lo siguiente:

   * `/apps/clientlibs/fd/af/guidetheme/common/less/adaptiveforms-mixins.less`

   Los formularios adaptables también proporcionan mezclas de terceros definidas en:

   * `/apps/clientlibs/fd/af/third-party/less/mixins.less`

   Definición de mezcla de muestra:

   ```css
   .rounded-corners (@radius) {
     -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
     -ms-border-radius: @radius;
     -o-border-radius: @radius;
     border-radius: @radius;
   }
   
   .border(@color, @type, @size) {
      border: @color @size @type;
   }
   ```

   **Archivo Styles.less:** Use este archivo para incluir todos los archivos `less` (variables, mezclas, estilos) que debe usar en la biblioteca de cliente.

   En el siguiente archivo de ejemplo `styles.less`, la instrucción import se puede colocar en cualquier orden.

   Las instrucciones para importar los siguientes `.less` archivos son obligatorias:

   * `globalvariables.less`
   * `layoutvariables.less`
   * `components.less`
   * `layouts.less`

   ```css
   @import "../../../clientlibs/fd/af/guidetheme/common/less/globalvariables.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layoutvariables.less";
   @import "forestTheme-variables";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/components.less";
   @import "../../../clientlibs/fd/af/guidetheme/common/less/layouts.less";
   
   /* custom styles */
   
   .guidetoolbar {
     input[type="button"], button, .button {
       .rounded-corners (@button-radius);
       &:hover {
         background-color: @button-hover-bg-color;
       }
       &:focus {
         background-color: @button-focus-bg-color;
       }
     }
   }
   
   form {
       background-image: url(../images/forest.png);
    background-repeat: no-repeat;
    background-size: 100%;
   }
   ```

   El `css.txt` contiene las rutas de los archivos .css que se van a descargar para la biblioteca.

   Por ejemplo:

   ```javascript
   #base=/apps/clientlibs/fd/af/third-party/css
   bootstrap.css
   
   #base=less
   styles.less
   
   #base=/apps/clientlibs/fd/xfaforms/xfalib/css
   datepicker.css
   listboxwidget.css
   scribble.css
   dialog.css
   ```

   >[!NOTE]
   >
   >El archivo style.less no es obligatorio. Esto significa que no es necesario crear este archivo si no se ha definido ningún estilo, variable o mezcla personalizado.
   >
   >Sin embargo, si no crea un archivo style.less, en el archivo css.txt debe quitar la siguiente línea:
   >
   >**`#base=less`**
   >
   >E incluir la siguiente línea:
   >
   >**`styles.less`**

## Usar una temática en un formulario adaptable {#to-use-a-theme-in-an-adaptive-form}

Después de crear una temática de formulario adaptable, realice los siguientes pasos para utilizarlo de forma adaptativa:

1. Para incluir la temática creada en [para crear una temática de formulario adaptable](/help/forms/using/creating-custom-adaptive-form-themes.md#p-to-create-an-adaptive-form-theme-p), cree una página personalizada de tipo `cq:Component`.

   Por ejemplo, `/apps/myAfCustomizations/myAfPages/forestPage`. 

   1. Agregue una propiedad `sling:resourceSuperType` y establezca su valor como `fd/af/components/page/base`.

      ![Captura de pantalla del repositorio CRX](assets/1-2.png)

   1. Para utilizar una temática en la página, debe agregar un archivo de anulación library.jsp al nodo.

      A continuación, puede importar la temática creada en la sección Crear una temática de formulario adaptable de este artículo.

      El siguiente fragmento de código de ejemplo importa la temática `af.theme.forest`.

      ```jsp
      <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
      <cq:includeClientLib categories="af.theme.forest"/>
      ```

   1. **Opcional**: en la página personalizada, reemplace header.jsp, footer.jsp y body.jsp, según sea necesario.

1. Cree una plantilla personalizada (por ejemplo: `/apps/myAfCustomizations/myAfTemplates/forestTemplate`) cuyo jcr:content apunta a la página personalizada creada en el paso anterior (por ejemplo: `myAfCustomizations/myAfPages/forestPage)`.

   ![Captura de pantalla del repositorio CRX](assets/2-1.png)

1. Crear un formulario adaptable mediante la plantilla creada en el paso anterior. El aspecto del formulario adaptable se define mediante la temática creada en la sección Crear una temática del formulario adaptable de este artículo.
