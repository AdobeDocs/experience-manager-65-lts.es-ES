---
title: Envío asincrónico de formularios adaptables
description: Aprenda a configurar el envío asincrónico en formularios adaptables.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: df2621db-59a1-4031-8856-7c2de766c099
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 78%

---

# Envío asincrónico de formularios adaptables{#asynchronous-submission-of-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/asynchronous-submissions-adaptive-forms.html).

Tradicionalmente, los formularios web se configuran para enviarse sincrónicamente. En el envío sincrónico, cuando los usuarios envían un formulario, se les redirige a una página de reconocimiento, de agradecimiento o, si hay un error en el envío, a una página de error. Sin embargo, las experiencias web modernas, como las aplicaciones de una sola página, están ganando popularidad en los casos en los que la página web permanece estática mientras la interacción cliente-servidor se produce en segundo plano. Ahora puede proporcionar esta experiencia con formularios adaptables mediante la configuración del envío asincrónico.

En el caso del envío asincrónico, cuando un usuario envía un formulario, el desarrollador del formulario agrega una experiencia independiente, como redirigir a otro formulario o a una sección independiente del sitio web. El autor también puede añadir servicios independientes, como enviar datos a un almacén de datos diferente o añadir un motor de análisis personalizado. Si hay envío asincrónico, un formulario adaptable se comporta como una aplicación de una sola página, ya que el formulario no se vuelve a cargar o su URL no cambia cuando los datos del formulario enviados se validan en el servidor.

Siga leyendo para obtener más información sobre el envío asincrónico en formularios adaptables.

## Configuración del envío asincrónico {#configure}

Para configurar el envío asincrónico en un formulario adaptable haga lo siguiente:

1. En el modo Autor del formulario adaptable, seleccione el objeto Contenedor de formulario y seleccione ![cmppr1](assets/cmppr1.png) para abrir sus propiedades.
1. En la sección de propiedades de **[!UICONTROL Envío]**, habilite **[!UICONTROL Usar envío asincrónico]**.
1. En la sección **[!UICONTROL Al enviar]**, seleccione una de las siguientes opciones para realizarla cuando se envíe correctamente del formulario.

   * **[!UICONTROL Redirigir a URL]**: redirige a la URL o página especificada después de enviar el formulario. Puede especificar una URL o examinar y elegir la ruta a una página en el campo **[!UICONTROL URL/ruta de redireccionamiento]**.
   * **[!UICONTROL Mostrar mensaje]**: muestra un mensaje sobre el envío del formulario. Puede escribir un mensaje en el campo de texto debajo de la opción Mostrar mensaje. El campo de texto admite el formato de texto enriquecido.

1. Seleccione ![check-button1](assets/check-button1.png) para guardar las propiedades.

## Funcionamiento del envío asincrónico {#how-asynchronous-submission-works}

AEM Forms proporciona controladores de éxito y de error predeterminados para los envíos de formularios. Los controladores son funciones del lado del cliente que se ejecutan en función de la respuesta del servidor. Cuando se envía un formulario, los datos se transmiten al servidor para su validación, lo que devuelve una respuesta al cliente con información sobre el evento de éxito o error del envío. La información se pasa en forma de parámetros al controlador correspondiente para ejecutar la función.

Además, los autores y desarrolladores de formularios pueden escribir reglas a nivel de formulario para invalidar los controladores predeterminados. Para obtener más información, consulte [Invalidar los controladores predeterminados mediante reglas](#custom).

Primero vamos a revisar la respuesta del servidor para los eventos de éxito y de error.

### Respuesta del servidor para el evento de éxito del envío {#server-response-for-submission-success-event}

La estructura de la respuesta del servidor para el evento de éxito del envío es la siguiente:

```json
{
  contentType : "<xmlschema or jsonschema>",
  data : "<dataXML or dataJson>" ,
  thankYouOption : <page/message>,
  thankYouContent : "<thank you page url/thank you message>"
}
```

La respuesta del servidor si el envío de formularios se realiza correctamente incluye lo siguiente:

* el tipo de formato de datos del formulario: XML o JSON;
* los datos del formulario en formato XML o JSON;
* la opción seleccionada para redireccionar a una página o mostrar un mensaje como se ha configurado en el formulario;
* la URL de la página o contenido del mensaje, según la configuración del formulario.

El controlador de éxito lee la respuesta del servidor y, en consecuencia, redirige a la URL de la página configurada o muestra un mensaje.

### Respuesta del servidor para el evento de error del envío {#server-response-for-submission-error-event}

La estructura de la respuesta del servidor para el evento de error del envío es la siguiente:

```json
{
   errorCausedBy : "<CAPTCHA_VALIDATION or SERVER_SIDE_VALIDATION>",

   errors : [
               { "somExpression" : "<SOM Expression>",
                 "errorMessage"  : "<Error Message>"
               },
               ...
             ]
 }
```

La respuesta del servidor si hay un error en el envío del formulario incluye:

* el motivo del error, el error de CAPTCHA o la validación del lado del servidor;
* la lista de objetos de error, que incluye la expresión SOM del campo en el que se ha producido un error al efectuar la validación y el mensaje de error correspondiente.

El controlador de error lee la respuesta del servidor y, en consecuencia, muestra el mensaje de error en el formulario.

## Invalidar los controladores predeterminados mediante reglas {#custom}

Los desarrolladores y autores de formularios pueden escribir reglas a nivel de formulario en el editor de código para invalidar los controladores predeterminados. La respuesta del servidor para eventos de éxito y error se expone a nivel de formulario, al cual los desarrolladores pueden acceder usando `$event.data` en las reglas.

Realice los siguientes pasos para escribir reglas en el editor de código para controlar los eventos de éxito y error.

1. Abra el formulario adaptable en el modo Autor, seleccione cualquier objeto de formulario y seleccione ![edit-rules1](assets/edit-rules1.png) para abrir el editor de reglas.
1. Seleccione **[!UICONTROL Formulario]** en el árbol Objetos de formulario y seleccione **[!UICONTROL Crear]**.
1. Seleccione **[!UICONTROL Editor de código]** de la lista desplegable de modo de selección.
1. En el editor de código, seleccione **[!UICONTROL Editar código]**. Seleccione **[!UICONTROL Editar]** en el cuadro de diálogo de confirmación.
1. Elija **[!UICONTROL Envío correcto]** o **[!UICONTROL Error en el envío]** de la lista desplegable **[!UICONTROL Evento]**.
1. Escriba una regla para el evento seleccionado y seleccione **[!UICONTROL Listo]** para guardar la regla.
