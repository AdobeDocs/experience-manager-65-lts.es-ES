---
title: Desarrollo de Forms (IU clásica)
description: Aprenda a desarrollar formularios para la IU clásica de Adobe Experience Manager
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 0%

---

# Desarrollo de Forms (IU clásica){#developing-forms-classic-ui}

La estructura básica de un formulario es:

* Inicio de formulario
* Elementos de formulario
* Fin de formulario

Todos estos elementos se realizan con una serie de [componentes de formulario](/help/sites-authoring/default-components.md#form) predeterminados, disponibles en una instalación estándar de AEM.

Además de [desarrollar nuevos componentes](/help/sites-developing/developing-components-samples.md) para usarlos en sus formularios, también puede:

* [Precargar el formulario con valores](#preloading-form-values)
* [Precargar (ciertos) campos con varios valores](#preloading-form-fields-with-multiple-values)
* [Desarrollar nuevas acciones](#developing-your-own-form-actions)
* [Desarrollar nuevas restricciones](#developing-your-own-form-constraints)
* [Mostrar u ocultar campos de formulario específicos](#showing-and-hiding-form-components)

[Usar scripts](#developing-scripts-for-use-with-forms) para ampliar la funcionalidad donde sea necesario.

>[!NOTE]
>
>Este documento se centra en el desarrollo de formularios utilizando [componentes de base](/help/sites-authoring/default-components-foundation.md) en la IU clásica. Adobe recomienda usar los nuevos [componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y [Ocultar condiciones](/help/sites-developing/hide-conditions.md) para el desarrollo de formularios en la interfaz de usuario táctil.

## Precarga de valores de formulario {#preloading-form-values}

El componente de inicio de formulario proporciona un campo para **Ruta de carga**, una ruta opcional que apunta a un nodo del repositorio.

La ruta de carga es la ruta a las propiedades del nodo que se utiliza para cargar valores predefinidos en varios campos del formulario.

Es un campo opcional que especifica la ruta a un nodo del repositorio. Cuando este nodo tiene propiedades que coinciden con los nombres de campo, los campos adecuados del formulario se precargan con el valor de esas propiedades. Si no existe ninguna coincidencia, el campo contiene el valor predeterminado.

>[!NOTE]
>
>Una [acción de formulario](#developing-your-own-form-actions) también puede establecer el recurso desde el cual cargar los valores iniciales. Esto se completó con `FormsHelper#setFormLoadResource` dentro de `init.jsp`.
>
>El autor solo rellenará el formulario desde la ruta establecida en el componente del formulario de inicio si no se ha establecido.

### Precarga de campos de formulario con varios valores {#preloading-form-fields-with-multiple-values}

Varios campos de formulario también tienen la ruta de carga **Items**, de nuevo una ruta opcional que apunta a un nodo del repositorio.

La ruta de carga de **elementos** es la ruta a las propiedades del nodo que se usa para cargar valores predefinidos en ese campo específico del formulario, por ejemplo, una [lista desplegable](/help/sites-authoring/default-components-foundation.md#dropdown-list), [grupo de casillas de verificación](/help/sites-authoring/default-components-foundation.md#checkbox-group) o [grupo de radio](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Ejemplo: Precarga de una lista desplegable con varios valores {#example-preloading-a-dropdown-list-with-multiple-values}

Se puede configurar una lista desplegable con el rango de valores para la selección.

La **Ruta de carga de elementos** se puede usar para obtener acceso a una lista de una carpeta en el repositorio y precargarla en el campo:

1. Crear una carpeta de sling (`sling:Folder`)
por ejemplo, `/etc/designs/<myDesign>/formlistvalues`

1. Agregue una nueva propiedad (por ejemplo, `myList`) de tipo cadena de varios valores ( `String[]`) para contener la lista de elementos desplegables. El contenido también se puede importar mediante una secuencia de comandos, como con una secuencia de comandos JSP o cURL en una secuencia de comandos shell.

1. Utilice la ruta completa en el campo **Ruta de carga de elementos**:
por ejemplo, `/etc/designs/geometrixx/formlistvalues/myList`

Tenga en cuenta que si los valores de `String[]` son del con el formato siguiente:

* `AL=Alabama`
* `AK=Alaska`

y así sucesivamente, AEM genera la lista como:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Esta función, por ejemplo, se puede utilizar correctamente en un entorno de varios idiomas.

### Desarrollo de sus propias acciones de formulario {#developing-your-own-form-actions}

Un formulario necesita una acción. Una acción define la operación que se ejecuta cuando se envía el formulario con los datos del usuario.

Con una instalación estándar de AEM se proporcionan una serie de acciones que se pueden ver en:

`/libs/foundation/components/form/actions`

y en la lista **Tipo de acción** del componente **Formulario**:

![chlimage_1-8](assets/chlimage_1-8.png)

Esta sección explica cómo puede desarrollar su propia acción de formulario para incluirla en esta lista.

Puede agregar su propia acción en `/apps` de la siguiente manera:

1. Cree un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la acción que desea implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormAction`

1. En este nodo, defina las siguientes propiedades y haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - establecido como `foundation/components/form/action`

   * `componentGroup` - definir como `.hidden`

   * Opcionalmente:

      * `jcr:title` - especifique un título de su elección, esto se mostrará en la lista desplegable de selección. Si no se define, se mostrará el nombre del nodo

      * `jcr:description` - escriba una descripción de su elección

1. En la carpeta, cree un nodo de diálogo:

   1. Agregue campos para que el autor pueda editar el cuadro de diálogo de formularios una vez elegida la acción.

1. En la carpeta, cree lo siguiente:

   1. Un guion post.
El nombre del script es `post.POST.<extension>`, por ejemplo, `post.POST.jsp`
El script posterior se invoca cuando se envía un formulario para procesarlo y contiene el código que administra los datos que llegan desde el formulario `POST`.

   1. Agregue un script de reenvío que se invoque cuando se envíe el formulario.
El nombre del script es `forward.<extension`>, por ejemplo, `forward.jsp`
Esta secuencia de comandos puede definir una ruta. La solicitud actual se reenvía a la ruta especificada.

   La llamada necesaria es `FormsHelper#setForwardPath` (2 variantes). Un caso típico es realizar alguna validación, o lógica, para encontrar la ruta de destino y luego reenviar a esa ruta, dejando que el servlet Sling POST predeterminado realice el almacenamiento real en JCR.

   También podría haber otro servlet que realice el procesamiento real, en tal caso la acción de formulario y `forward.jsp` solo actuarían como código de &quot;pegado&quot;. Un ejemplo de esto es la acción de correo en `/libs/foundation/components/form/actions/mail`, que reenvía detalles a `<currentpath>.mail.html`donde se encuentra un servlet de correo.

   Así que:

   * un(a) `post.POST.jsp` es útil para operaciones pequeñas que la propia acción realiza por completo
   * mientras que `forward.jsp` resulta útil cuando solo se requiere delegación.

   El orden de ejecución de los scripts es el siguiente:

   * Al procesar el formulario ( `GET`):

      1. `init.jsp`
      1. para todas las restricciones del campo: `clientvalidation.jsp`
      1. elemento validationRT del formulario: `clientvalidation.jsp`
      1. el formulario se carga mediante el recurso de carga si está configurado
      1. `addfields.jsp` mientras se encontraba dentro del procesamiento `<form></form>`

   * al administrar un formulario `POST`:

      1. `init.jsp`
      1. para todas las restricciones del campo: `servervalidation.jsp`
      1. elemento validationRT del formulario: `servervalidation.jsp`
      1. `forward.jsp`
      1. si se estableció una ruta de reenvío (`FormsHelper.setForwardPath`), reenvíe la solicitud y llame a `cleanup.jsp`

      1. si no se estableció ninguna ruta de reenvío, llame a `post.POST.jsp` (termina aquí, no se llamó a `cleanup.jsp`)

1. De nuevo en la carpeta, agregue lo siguiente de forma opcional:

   1. Script para agregar campos.
El nombre del script es `addfields.<extension>`, por ejemplo, `addfields.jsp`
Se invoca un script `addfields` inmediatamente después de escribir HTML para el inicio del formulario. Esto permite a la acción agregar campos de entrada personalizados u otros HTML dentro del formulario.

   1. Un script de inicialización.
El nombre del script es `init.<extension>`, por ejemplo, `init.jsp`
Este script se invoca cuando se procesa el formulario. Se puede utilizar para inicializar acciones específicas.

   1. Un script de limpieza.
El nombre del script es `cleanup.<extension>`, por ejemplo, `cleanup.jsp`
Esta secuencia de comandos se puede utilizar para realizar la limpieza.

1. Use el componente **Forms** en un parsys. La lista desplegable **Tipo de acción** ahora incluirá su nueva acción.

   >[!NOTE]
   >
   >Para ver las acciones predeterminadas que forman parte del producto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Desarrollo de sus propias restricciones de formulario {#developing-your-own-form-constraints}

Las restricciones se pueden imponer en dos niveles:

* Para [campos individuales (consulte el siguiente procedimiento)](#constraints-for-individual-fields)
* Como [validación de formulario global](#form-global-constraints)

#### Restricciones para campos individuales {#constraints-for-individual-fields}

Puede agregar sus propias restricciones para un campo individual (en `/apps`) de la siguiente manera:

1. Cree un nodo de tipo `sling:Folder`. Especifique un nombre que refleje la restricción que se va a implementar.

   Por ejemplo:

   `/apps/myProject/components/customFormConstraint`

1. En este nodo, defina las siguientes propiedades y haga clic en **Guardar todo** para mantener los cambios:

   * `sling:resourceType` - se estableció en `foundation/components/form/constraint`

   * `constraintMessage`: un mensaje personalizado que se muestra si el campo no es válido, según la restricción, cuando se envía el formulario

   * Opcionalmente:

      * `jcr:title` - especifique un título de su elección, esto se mostrará en la lista de selección. Si no se define, se mostrará el nombre del nodo
      * `hint`: información adicional, para el usuario, sobre cómo utilizar el campo

1. Dentro de esta carpeta, puede necesitar los siguientes scripts:

   * Un script de validación de cliente:
El nombre del script es `clientvalidation.<extension>`, por ejemplo, `clientvalidation.jsp`
Se invocará cuando se represente el campo de formulario. Se puede utilizar para crear el javascript del cliente para validar el campo en el cliente.

   * Un script de validación de servidor:
El nombre del script es `servervalidation.<extension>`, por ejemplo, `servervalidation.jsp`
Se invocará cuando se envíe el formulario. Se puede utilizar para validar el campo en el servidor después de enviarlo.

>[!NOTE]
>
>Las restricciones de muestra se pueden ver en:
>
>`/libs/foundation/components/form/constraints`

#### Restricciones globales de formulario {#form-global-constraints}

La validación global del formulario se especifica configurando un tipo de recurso en el componente del formulario de inicio ( `validationRT`). Por ejemplo:

`apps/myProject/components/form/validation`

A continuación, puede definir:

* a `clientvalidation.jsp` - insertado después de los scripts de validación de cliente del campo
* y un `servervalidation.jsp`, también llamado después de las validaciones individuales del servidor de campo en un `POST`.

### Mostrar y ocultar componentes de formulario {#showing-and-hiding-form-components}

Puede configurar el formulario para mostrar u ocultar componentes de formulario según el valor de otros campos del formulario.

Cambiar la visibilidad de un campo de formulario resulta útil cuando el campo solo es necesario en condiciones específicas. Por ejemplo, en un formulario de comentarios, una pregunta pregunta a los clientes si desean que se les envíe información de productos por correo electrónico. Al seleccionar sí, aparece un campo de texto para permitir que el cliente escriba su dirección de correo electrónico.

Utilice el cuadro de diálogo **Editar reglas para mostrar u ocultar** para especificar las condiciones en las que se muestra o se oculta un componente de formulario.

![showhideeditor](assets/showhideeditor.png)

Utilice los campos de la parte superior del cuadro de diálogo para especificar la siguiente información:

* Si está especificando condiciones para ocultar o mostrar el componente.
* Si alguna o todas las condiciones deben ser verdaderas para mostrar u ocultar el componente.

Debajo de estos campos aparecen una o más condiciones. Una condición compara el valor de otro componente del formulario (en el mismo formulario) con un valor. Si el valor real del campo cumple la condición, la condición se evalúa como true. Las condiciones incluyen la siguiente información:

* Título del campo de formulario que se prueba.
* Un operador.
* Se compara un valor con el valor del campo.

Por ejemplo, un componente de grupo de radio con el título `Receive email notifications?`* * contiene `Yes` y `No` botones de opción. Un componente de campo de texto con el título `Email Address` utiliza la siguiente condición para que sea visible si se selecciona `Yes`:

![showhidecondition](assets/showhidecondition.png)

En JavaScript, las condiciones utilizan el valor de la propiedad Nombre del elemento para hacer referencia a los campos. En el ejemplo anterior, la propiedad Nombre del elemento del componente Grupo de radio es `contact`. El siguiente código es el código JavaScript equivalente para ese ejemplo:

`((contact == "Yes"))`

**Para mostrar u ocultar un componente de formulario:**

1. Edite el componente de formulario específico.

1. Seleccione **Mostrar / Ocultar** para abrir el diálogo **Editar reglas para mostrar / ocultar**:

   * En la primera lista desplegable, seleccione **Mostrar** o **Ocultar** para especificar si las condiciones determinan si se debe mostrar u ocultar el componente.

   * En la lista desplegable al final de la línea superior, seleccione:

      * **all** - si todas las condiciones deben ser verdaderas para mostrar u ocultar el componente
      * **any** - si solo una o más condiciones deben ser verdaderas para mostrar u ocultar el componente

   * En la línea de condición (se presenta una como predeterminada), seleccione un componente, un operador y, a continuación, especifique un valor.
   * Agregue más condiciones si es necesario haciendo clic en **Agregar condición**.

   Por ejemplo:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Haga clic en **Aceptar** para guardar la definición.

1. Después de guardar la definición, aparece un vínculo **Editar reglas** junto a la opción **Mostrar / Ocultar** en las propiedades del componente del formulario. Haga clic en este vínculo para abrir el cuadro de diálogo **Editar mostrar / ocultar reglas** para realizar cambios.

   Haga clic en **Aceptar** para guardar todos los cambios.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Los efectos de las definiciones Mostrar / Ocultar se pueden ver y probar:
   >
   >* en modo **Vista previa** en el entorno de creación (necesita una recarga de página la primera vez que se cambia a vista previa)
   >
   >* en el entorno de publicación

#### Gestión de referencias de componentes rotos {#handling-broken-component-references}

Las condiciones Show/hide utilizan el valor de la propiedad Element Name para hacer referencia a otros componentes del formulario. La configuración Mostrar/Ocultar no es válida cuando cualquiera de las condiciones hace referencia a un componente que se elimina o cuya propiedad Nombre del elemento se ha cambiado. Cuando esto sucede, es necesario actualizar manualmente las condiciones o se produce un error cuando se carga el formulario.

Cuando la configuración Mostrar/Ocultar no es válida, la configuración solo se proporciona como código JavaScript. Edite el código para corregir los problemas. El código utiliza la propiedad Nombre del elemento (Element Name) que se utilizó originalmente para hacer referencia a los componentes.

### Desarrollo de scripts para su uso con Forms {#developing-scripts-for-use-with-forms}

Para obtener más información sobre los elementos de API que se pueden usar al escribir scripts, consulte los [javadocs relacionados con formularios](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

Puede utilizarlo para acciones como llamar a un servicio antes de enviar el formulario y cancelar el servicio si falla:

* Definir el tipo de recurso de validación
* Incluya un script para la validación:

   * En el JSP, llame al servicio web y cree un objeto `com.day.cq.wcm.foundation.forms.ValidationInfo` que contenga los mensajes de error. Si hay errores, no se publicarán los datos del formulario.
