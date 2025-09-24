---
title: ¿Qué son los fragmentos de formulario adaptable?
description: Los formularios adaptables proporcionan un mecanismo para crear un segmento de formulario, como un panel o un grupo de campos, para utilizarlo en cualquier formulario adaptable. También puede guardar un panel existente como fragmento.
topic-tags: author
keywords: Agregar fragmentos de formulario adaptable, fragmentos de formulario adaptable, Crear un fragmento de formulario, Agregar un fragmento a un formulario adaptable, Administrar fragmentos
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
role: Admin, Developer
exl-id: 708a4ab2-ca66-445d-8d69-bcf12fd5158a
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 95%

---

# Crear y utilizar fragmentos de Formularios adaptables en un formulario adaptable basado en componentes principales {#adaptive-form-fragments}

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/adaptive-form-fragments-core-components.html?lang=es).

Aunque cada formulario está diseñado para un propósito específico, hay algunos segmentos comunes en la mayoría de los formularios, como para proporcionar detalles personales como nombre y dirección, detalles familiares, detalles de ingresos, etc. Los desarrolladores de formularios deben crear estos segmentos comunes cada vez que se crea un nuevo formulario.

Los formularios adaptables proporcionan un mecanismo cómodo para crear segmentos de formulario como un panel o un grupo de campos solo una vez y reutilizarlos. Estos segmentos reutilizables e independientes se denominan fragmentos de formulario adaptables.

Los fragmentos de formulario se integran perfectamente en varios formularios, lo que optimiza la creación de formularios coherentes y de aspecto profesional. Los fragmentos de formulario garantizan la reutilización, la estandarización y la coherencia de la marca mediante la funcionalidad “cambiar una vez y reflejar en todas partes”. Experimente una mayor capacidad de mantenimiento y eficacia, ya que las actualizaciones realizadas en un solo lugar se propagan automáticamente a todos los formularios que utilizan estos fragmentos.

Puede agregar un fragmento varias veces a un documento y utilizar las propiedades de enlace de datos de sus componentes para vincularlo a diferentes fuentes de datos o esquemas. Por ejemplo, puede utilizar el mismo fragmento de dirección para la dirección permanente, de comunicación y de facturación y conectarlo a diferentes campos de un origen de datos o esquema.

>[!NOTE]
>
> Puede personalizar fácilmente la experiencia del fragmento para los usuarios con el cuadro de diálogo [Configurar y el cuadro de diálogo Diseño del componente Fragmento de formulario](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment).


## Creación de un fragmento de formulario {#create-a-fragment}

Puede crear un fragmento de formulario adaptable desde cero o guardar un panel en un formulario adaptable existente como fragmento. Para crear un fragmento de formulario:

1. Inicie sesión en una instancia de AEM Forms en https://[*hostname*]:[*port*]/aem/forms.html.
1. Haga clic en **Crear > fragmento de formulario adaptable**.
1. Especifique el título, el nombre, la descripción y las etiquetas del fragmento. Asegúrese de especificar un nombre único para el fragmento. Si ya existe otro fragmento con el mismo nombre, el fragmento no se creará.
1. Seleccione una plantilla de formulario. Puede crear un fragmento de formulario para componentes principales basados en Formularios adaptables o en componentes de base basados en Formularios adaptables.
   * Para crear un fragmento de formulario para formularios basados en componentes principales, seleccione una plantilla basada en componentes principales.
   * Para crear un fragmento de formulario para formularios basados en componentes de base, seleccione una plantilla Componentes de base. Por ejemplo, /libs/fd/af/templateForFragment/defaultFragmentTemplate.

   Cuando cree un fragmento de formulario para formularios basados en componentes principales, utilice la opción Seleccionar tema de formulario para seleccionar un tema basado en componentes principales.

1. Haga clic para abrir el **modelo de formulario** y desde el menú desplegable **Seleccionar desde**, seleccione uno de los siguientes modelos para el fragmento:

   ![Muestra el tipo de modelo en la pestaña Modelo de formulario](assets/create-af-1-1.png)

   * **Ninguno**: especifica que se cree el fragmento desde cero sin usar ningún modelo de formulario.

     >[!NOTE]
     >
     > En Formularios adaptables, puede utilizar un solo fragmento de formulario (basado en componentes principales) varias veces. Admite fragmentos de formulario basados en ninguno y en esquema.

   * **Esquema**: especifica que se crea el fragmento con un esquema XML o JSON cargado en AEM Forms. Puede cargar o seleccionar entre los esquemas XML disponibles como modelo de formulario para el fragmento. Al seleccionar un esquema XML, también puede crear un fragmento de formulario adaptable seleccionando un complexType presente en el esquema seleccionado del cuadro desplegable **[!UICONTROL Tipo complejo de esquema XML]**. Al seleccionar un esquema JSON, también puede crear un fragmento de formulario adaptable seleccionando una definición de esquema presente en el esquema seleccionado del cuadro desplegable **[!UICONTROL Definiciones de esquema JSON]**.
   * **Modelo de datos de formulario**: especifica la creación del fragmento mediante un modelo de datos de formulario. Puede crear un fragmento de formulario adaptable basado en un único objeto de modelo de datos en un modelo de datos de formulario. Expanda la lista desplegable Definiciones del modelo de datos de formulario. Esta lista enumera todos los objetos de modelo de datos del modelo de datos de formulario especificado. Seleccione un objeto de modelo de datos de la lista.

   ![Modelo de datos de formulario](assets/create-af-3.png)



1. Haga clic en **Crear** y luego haga clic en **Abrir** para abrir el fragmento, con una plantilla predeterminada, en el modo de edición. En el modo de edición, puede agregar cualquier componente del formulario adaptable al fragmento.

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> Además, si ha seleccionado un esquema XML o una plantilla de formulario XDP como modelo de formulario para el fragmento, aparecerá una nueva pestaña que mostrará la jerarquía del modelo de formulario en el buscador de contenido. Permite arrastrar y soltar los elementos del modelo de formulario en el fragmento. Los elementos del modelo de formulario agregados se convierten en componentes de formulario, al tiempo que se conservan las propiedades originales del XDP o XSD asociado.

Una vez creado el fragmento de formulario adaptable basado en un esquema o modelo de datos de formulario, los objetos de esquema o modelo de datos de formulario aparecen en la pestaña Fuentes de datos del Explorador de contenido en el Editor de formularios adaptables. Puede arrastrar y soltar elementos del modelo de formulario en el fragmento. Los elementos del modelo de formulario agregados se convierten en componentes de formulario, al tiempo que se conservan las propiedades originales del esquema asociado.


## Añadir un fragmento a un formulario adaptable {#insert-a-fragment-in-an-adaptive-form}

Para agregar un fragmento de formulario adaptable en un formulario adaptable, haga lo siguiente:

1. Abra el formulario adaptable en modo de edición.
1. Añada el componente **Fragmento de formulario adaptable** al formulario.
1. Haga clic en el explorador de contenido de **Recursos** en la barra lateral. En el explorador de recursos, en las rutas, seleccione la opción **Fragmentos de formulario adaptable**. Aparecerán todos los fragmentos de Formularios adaptables disponibles para el formulario, según el modelo del formulario.

   ![seleccione la opción Fragmentos de formulario adaptable](assets/adaptive-forms-fragments.png)

1. Arrastre y suelte un fragmento de formulario adaptable en el componente **Fragmento de formulario adaptable** en el formulario adaptable.

   >[!NOTE]
   >
   >El fragmento de formulario adaptable no está habilitado para la creación desde el formulario adaptable. Además, no puede utilizar un fragmento basado en XSD en un formulario adaptable basado en JSON y viceversa.

El fragmento de formulario adaptable se inserta por referencia en el formulario adaptable y se sincroniza con el fragmento de formulario adaptable independiente. Esto implica que cualquier modificación realizada en el fragmento de formulario adaptable se reflejará en todas las instancias en las que el fragmento se incorpore a Formularios adaptables.

### Incrustar un fragmento en el formulario adaptable {#embed-a-fragment-in-adaptive-form}

Puede incrustar un fragmento de formulario adaptable en un formulario adaptable si hace clic en el icono ![Incrustar](assets/Smock_Import_18_N.svg) de la barra de herramientas del panel del fragmento añadido

El fragmento incrustado ya no estará vinculado al fragmento independiente. Puede editar los componentes del fragmento incrustado desde el formulario adaptable.

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### Uso de fragmentos dentro de fragmentos {#using-fragments-within-fragments}

Puede crear fragmentos de formulario adaptable anidados, lo que significa que puede arrastrar y soltar un fragmento en otro fragmento y tener una estructura anidada.

### Uso de un fragmento de formulario varias veces en un formulario adaptable {#using-form-fragment-mutiple-times-in-af}

Puede utilizar un fragmento de formulario basado en esquemas y no basado en esquema varias veces en un formulario adaptable para guardar datos de forma única para cada campo de fragmento de formulario.  Por ejemplo, puede utilizar un fragmento de formulario de dirección para recopilar detalles de dirección para direcciones permanentes, de comunicación y actuales en un formulario de solicitud de préstamo.

![usar varios fragmentos en formularios adaptables](assets/using-multiple-fragment-af.gif)

## Asignar automáticamente fragmentos para enlazar datos {#auto-mapping-of-fragments-for-data-binding}

Cuando crea un fragmento de formulario adaptable mediante una plantilla de formulario XFA o un tipo complejo XSD y arrastra y suelta el fragmento en un formulario adaptable, el fragmento XFA o el tipo complejo XSD se reemplazará automáticamente por el fragmento de formulario adaptable correspondiente, cuya raíz del modelo de fragmento estará asignada al fragmento XFA o al tipo complejo XSD.

Puede cambiar el recurso del fragmento y sus enlaces desde el cuadro de diálogo Editar componente.

También puede arrastrar y soltar un fragmento de formulario adaptable enlazado desde la biblioteca de fragmentos de formularios adaptables en el buscador de contenido de AEM y proporcionar la referencia de enlace correcta desde el diálogo Editar componente del panel de fragmentos de formulario adaptable.

## Administrar fragmentos {#manage-fragments}

Puede realizar varias operaciones en los fragmentos de formularios adaptables mediante la interfaz de usuario de AEM Forms.

1. Vaya a `https://[hostname]/aem/forms.html`.

1. Haga clic en **Seleccionar** en la barra de herramientas de la IU de AEM Forms y seleccione un fragmento de formulario adaptable. La barra de herramientas muestra las siguientes operaciones que puede realizar en el fragmento de formulario adaptable seleccionado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operación</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
  </tr>
  <tr>
   <td><p>Editar</p> </td>
   <td><p>Abre el fragmento de formulario adaptable seleccionado en el modo de edición.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Propiedades</p> </td>
   <td><p>Abre el panel Propiedades. Desde el panel Propiedades, puede ver y editar propiedades, generar una vista previa y cargar una imagen en miniatura del fragmento seleccionado. Para obtener más información, consulte <a>Administrar metadatos</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copiar</p> </td>
   <td><p>Copia el fragmento seleccionado. El botón Pegar aparece en la barra de herramientas.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Descargar</p> </td>
   <td><p>Descarga el fragmento seleccionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Vista previa</p> </td>
   <td><p>Proporciona opciones para obtener una vista previa del fragmento como HTML o una vista previa personalizada mediante la combinación de datos de un archivo XML con el fragmento. Para obtener más información, consulte <a>Previsualizar un formulario</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Iniciar revisión/Administrar revisión</p> </td>
   <td><p>Permite iniciar y administrar una revisión del fragmento seleccionado. Para obtener más información, consulte <a>Crear y administrar revisiones</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Agregar diccionario</p> </td>
   <td><p>Genera un diccionario para localizar el fragmento seleccionado. Para obtener más información, consulte <a>Localizar formularios adaptables</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publicar o cancelar la publicación</p> </td>
   <td><p>Publica/cancela la publicación del fragmento seleccionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Eliminar</p> </td>
   <td><p>Elimina el fragmento seleccionado.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Puntos clave que se deben recordar al trabajar con fragmentos {#key-points-to-remember-when-working-with-fragments}

* Asegúrese de que el nombre del fragmento sea único. El fragmento no se creará si hay un fragmento existente con el mismo nombre.
* En un formulario adaptable basado en XDP, si guarda un panel como fragmento que incluye otro fragmento XDP, el fragmento resultante se enlaza automáticamente al fragmento XDP secundario. Si es un formulario adaptable basado en XSD, el fragmento resultante está enlazado a la raíz del esquema.
* Cuando cree un fragmento de formulario adaptable, se creará un nodo de fragmento en CRXDe Lite, similar al nodo guideContainer para un formulario adaptable.
* No se admite un fragmento de un formulario adaptable que utilice un modelo de datos de formulario diferente. Por ejemplo, un fragmento basado en XDP no es compatible con un formulario adaptable basado en XSD y viceversa.
* Los fragmentos de formularios adaptables están disponibles para utilizarlos a través de la pestaña Fragmentos de formularios adaptables en el buscador de contenido de AEM.
* Cualquier expresión, script o estilo de un fragmento de formulario adaptable independiente se conservará cuando se inserte por referencia o se incruste en un formulario adaptable.
* No puede editar un fragmento de formulario adaptable, que se inserte por referencia, desde un formulario adaptable. Para editarlo, edite el fragmento de formulario adaptable independiente o incruste el fragmento en el formulario adaptable.
* Cuando publique un formulario adaptable, deberá publicar los fragmentos de formulario adaptable independientes insertados por referencia en el formulario adaptable.
* Cuando vuelva a publicar un fragmento de formulario adaptable actualizado, los cambios se reflejarán en las instancias publicadas del formulario adaptable en el que se utilice el fragmento.
* El formulario adaptable que contenga el componente Verificar no admitirá usuarios anónimos. Además, no se recomienda utilizar el componente Verificar en un fragmento de formulario adaptable.
* (**Solo Mac**) Para asegurarse de que la funcionalidad de los fragmentos del formulario funciona perfectamente en todas las situaciones, agregue la siguiente entrada al archivo /private/etc/hosts:
  `127.0.0.1 <Host machine>` **Equipo host**: el equipo Mac de Apple en el que está implementado AEM Forms.

## Fragmentos de referencia {#reference-fragments}

Fragmentos de formulario adaptable de referencia que puede utilizar para crear el formulario.
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->

## Ver también {#see-also}

* [Crear un formulario adaptable basado en componentes principales](create-an-adaptive-form-core-components.md)
* [Utilice el editor de reglas para agregar un comportamiento dinámico al formulario](rule-editor.md)
* [Crear o personalizar temáticas para componentes principales basados en Forms adaptable](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Crear una plantilla para componentes principales basados en Forms adaptable](template-editor.md)
* [Crear o agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Plantillas temáticas y modelos de datos de formulario de ejemplo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=es)
