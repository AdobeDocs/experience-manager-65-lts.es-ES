---
title: Escribir una acción de envío personalizada para formularios adaptables
description: AEM Forms permite crear acciones de envío personalizadas para formularios adaptables. En este artículo se describe el procedimiento para agregar una acción de envío personalizada para formularios adaptables.
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components,Form Data Model
exl-id: dc3bd697-5b1a-4efe-9554-c6aa1575c1c0
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 84%

---

# Escribir una acción de envío personalizada para formularios adaptables{#writing-custom-submit-action-for-adaptive-forms}

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/custom-submit-action-form.html?lang=es).

Los formularios adaptables requieren enviar acciones para procesar los datos especificados por el usuario. Una acción de envío determina la tarea realizada en los datos enviados mediante un formulario adaptable. Adobe Experience Manager (AEM) incluye [acciones de envío listas para usar](../../forms/using/configuring-submit-actions.md) que muestran tareas personalizadas que puede realizar con los datos enviados por el usuario. Por ejemplo, puede realizar tareas como enviar correos electrónicos o almacenar los datos.

## Flujo de trabajo para una acción de envío {#workflow-for-a-submit-action}

El diagrama de flujo muestra el flujo de trabajo de una acción de envío que se activa al hacer clic en el botón **[!UICONTROL Enviar]** de un formulario adaptable. Los archivos del componente Archivo adjunto se cargan en el servidor y los datos del formulario se actualizan con las direcciones URL de los archivos cargados. Dentro del cliente, los datos se almacenan en formato JSON. El cliente envía una solicitud Ajax a un servlet interno que analiza los datos especificados y los devuelve en formato XML. El cliente recopila estos datos con campos de acción. Envía los datos al servlet final (servlet de envío de guía) mediante la acción de envío formulario. A continuación, el servlet reenvía el control a la acción de envío. La acción de envío puede reenviar la solicitud a otro recurso de sling o redirigir el explorador a otra dirección URL.

![Diagrama de flujo que muestra el flujo de trabajo para la acción de envío](assets/diagram1.png)

### Formato de datos XML {#xml-data-format}

Los datos XML se envían al servlet utilizando el parámetro de solicitud **`jcr:data`**. Las acciones Enviar pueden acceder al parámetro para procesar los datos. El siguiente código describe el formato de los datos XML. Los campos vinculados al modelo de formulario aparecen en la sección **`afBoundData`**. Los campos no vinculados aparecen en la sección `afUnoundData`. Para obtener más información sobre el formato del archivo `data.xml`, consulte [Introducción al rellenado previo de campos de formularios adaptables](../../forms/using/prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### Campos de acción {#action-fields}

Una acción de envío puede agregar campos de entrada ocultos (mediante la etiqueta de [entrada HTML ](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input)) al HTML de formulario procesado. Estos campos ocultos pueden contener los valores que necesita al procesar el envío del formulario. Al enviar el formulario, estos valores de campo se vuelven a registrar como parámetros de solicitud que la acción de envío puede utilizar durante el envío. Los campos de entrada se denominan campos de acción.

Por ejemplo, una acción de envío que también capture el tiempo necesario para rellenar un formulario, puede agregar los campos de entrada ocultos `startTime` y `endTime`.

Un script puede aportar los valores de los campos `startTime` y `endTime` cuando el formulario se procesa y antes de enviarlo, respectivamente. El ActionScript de envío `post.jsp` puede acceder a estos campos mediante parámetros de solicitud y calcular el tiempo total necesario para rellenar el formulario.

### Archivos adjuntos {#file-attachments}

Las acciones de envío también pueden utilizar los archivos adjuntos que se cargan mediante el componente Archivo adjunto. Los scripts de acción de envío pueden acceder a estos archivos mediante la [API RequestParameter](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html) de Sling. El método [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) de la API ayuda a identificar si el parámetro de solicitud es un archivo o un campo de formulario. Puede iterar los parámetros de solicitud en una acción de envío para identificar los parámetros del archivo adjunto.

El siguiente código de ejemplo identifica los archivos adjuntos en la solicitud. A continuación, lee los datos en el archivo utilizando [Obtener API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Finalmente, crea un objeto Documento utilizando los datos y lo anexa a una lista.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Ruta de reenvío y URL de redireccionamiento {#forward-path-and-redirect-url}

Después de realizar la acción necesaria, el servlet de envío reenvía la solicitud a la ruta de reenvío. Una acción utiliza la API setForwardPath para establecer la ruta de reenvío en el servlet de envío de la guía.

Si la acción no ofrece una ruta de reenvío, el servlet de envío redirecciona el explorador mediante la URL de redireccionamiento. El autor configura la URL de redireccionamiento utilizando la configuración de la página de agradecimiento del cuadro de diálogo Editar formulario adaptable. También puede configurar la URL de redireccionamiento mediante la acción de envío o la API setRedirectUrl en el servlet de envío de la guía. También puede configurar los parámetros de solicitud enviados a la URL de redireccionamiento utilizando la API setRedirectParameters en el servlet de envío de la guía.

>[!NOTE]
>
>Un autor aporta la URL de redireccionamiento (mediante la configuración de la página de agradecimiento). [Acciones de envío listas para usar](../../forms/using/configuring-submit-actions.md) usan la URL de redireccionamiento para redirigir el explorador desde el recurso al que hace referencia la ruta de reenvío.
>
>Puede escribir una acción de envío personalizada que reenvíe una solicitud a un recurso o servlet. Adobe recomienda que el script que administra los recursos de la ruta de reenvío redirija la solicitud a la URL de redireccionamiento cuando termine el procesamiento.

## Acción de envío {#submit-action}

Una acción de envío es un sling:Folder que incluye lo siguiente:

* **addfields.jsp**: Este script aporta los campos de acción que se añaden al archivo HTML durante la representación. Utilice este script para agregar los parámetros de entrada ocultos necesarios durante el envío en el script post.POST.jsp.
* **dialog.xml**: Este script es similar al cuadro de diálogo Componente CQ. Aporta información de configuración que el autor personaliza. Los campos se muestran en la pestaña Acciones de envío, del cuadro de diálogo Editar formulario adaptable, al seleccionar la acción de envío.
* **post.POST.jsp**: El servlet de envío utiliza este script con los datos que envía y los datos adicionales de las secciones anteriores. Cualquier mención de la ejecución de una acción en esta página implica la ejecución del script post.POST.jsp. Para registrar la acción de envío con los formularios adaptables para que se muestre en el cuadro de diálogo Editar formulario adaptable, agregue estas propiedades a `sling:Folder`:

   * **guideComponentType** de tipo cadena y valor **fd/af/components/guidesubmittype**
   * **guideDataModel** de tipo cadena que especifica el tipo de formulario adaptable para el que se aplica la acción de envío. **xfa** es compatible con formularios adaptables basados en XFA, mientras **xsd** es compatible con formularios adaptables basados en XSD. **basic** es compatible con formularios adaptables que no utilizan XDP o XSD. Para mostrar la acción en varios tipos de formularios adaptables, agregue las cadenas correspondientes. Separe cada cadena con una coma. Por ejemplo, para que una acción sea visible en formularios adaptables basados en XFA y XSD, especifique los valores **xfa** y **xsd** respectivamente.

   * **jcr:description** de tipo cadena. El valor de esta propiedad se muestra en la lista Enviar acción de la pestaña Acciones de envío del cuadro de diálogo Editar formulario adaptable. Las acciones listas para usar están presentes en el repositorio de CRX en la ubicación **/libs/fd/af/components/guidesubmittype**.

## Crear una acción de envío personalizada {#creating-a-custom-submit-action}

Realice los siguientes pasos para crear una acción de envío personalizada que guarde los datos en el repositorio CRX y luego le envíe un correo electrónico. El formulario adaptable contiene el contenido del almacén de acciones de envío predeterminado (obsoleto) que guarda los datos en el repositorio de CRX. Además, CQ facilitará una API de [Correo electrónico](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es) que se puede utilizar para enviar correos electrónicos. Antes de usar la API de correo electrónico, [configure](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es&wcmmode=disabled) el servicio Day CQ Mail a través de la consola del sistema. Puede reutilizar la acción Almacenar contenido (obsoleta) para almacenar los datos en el repositorio. La acción Almacenar contenido (obsoleta) está disponible en la ubicación /libs/fd/af/components/guidesubmittype/store en el repositorio CRX.

1. Inicie sesión en CRXDE Lite en la URL https://&lt;server>:&lt;port>/crx/de/index.jsp. Cree un nodo con la propiedad sling::Folder y el nombre store_and_mail en la carpeta /apps/custom_submit_action. Cree la carpeta custom_submit_action si todavía no existe.

   ![Captura de pantalla que representa la creación de un nodo con la propiedad sling::Folder](assets/step1.png)

1. **Facilite los campos de configuración obligatorios.**

   Añada la configuración que requiere la acción Almacenar. Copie el nodo **cq:dialog** de la acción Almacenar de /libs/fd/af/components/guidesubmittype/store a la carpeta de acciones en /apps/custom_submit_action/store_and_email.

   ![Captura de pantalla que muestra la copia del nodo de diálogo a la carpeta de acciones](assets/step2.png)

1. **Facilite campos de configuración para solicitar al autor que configure el correo electrónico.**

   El formulario adaptable también ofrece una acción de correo electrónico que envía correos electrónicos a los usuarios. Personalice esta acción según sus necesidades. Vaya a /libs/fd/af/components/guidesubmittype/email/dialog. Copie los nodos dentro del nodo cq:dialog al nodo cq:dialog de su acción de envío (/apps/custom_submit_action/store_and_email/dialog).

   ![Personalizar la acción de correo electrónico](assets/step3.png)

1. **Haga que la acción esté disponible en el cuadro de diálogo Editar el formulario adaptable.**

   Añada las siguientes propiedades en el nodo store_and_email:

   * **guideComponentType** de tipo **Cadena** y valor **fd/af/components/guidesubmittype**

   * **guideDataModel** de tipo **Cadena** y valor **xfa, xsd, basic**

   * **jcr:description** de tipo **String** y valor **Acción de almacenamiento y correo electrónico**

1. Abra cualquier formulario adaptable. Haga clic en el botón **Editar** junto a **Inicio** para abrir el cuadro de diálogo **Editar** del contenedor del formulario adaptable. La nueva acción se muestra en la pestaña **Acciones de envío**. Al seleccionar **Acción de almacenamiento y correo electrónico**, muestra la configuración añadida en el nodo de diálogo.

   ![Cuadro de diálogo Configuración de la acción de envío](assets/store_and_email_submit_action_dialog.jpg)

1. **Utilice la acción para completar una tarea.**

   Añada el script post.POST.jsp a su acción. (/apps/custom_submit_action/store_and_mail/).

   Ejecute la acción predeterminada Almacenar (script post.POST.jsp). Utilice la API [FormsHelper.runAction](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String,java.lang.String,org.apache.sling.api.resource.Resource,org.apache.sling.api.SlingHttpServletRequest,org.apache.sling.api.SlingHttpServletResponse))&#x200B;(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) que CQ proporciona en su código para ejecutar la acción de almacenamiento. Añada el siguiente código en su archivo JSP:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   Para enviar el correo electrónico, el código lee la dirección de correo electrónico del destinatario de la configuración. Para recuperar el valor de configuración en el script de la acción, lea las propiedades del recurso actual utilizando el siguiente código. Del mismo modo, puede leer los demás archivos de configuración.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Finalmente, utilice la API CQ Mail para enviar el correo electrónico. Utilice la clase [SimpleEmail](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/commons/mail/SimpleEmail.html) para crear el objeto de correo electrónico como se muestra a continuación:

   >[!NOTE]
   >
   >Asegúrese de que el archivo JSP tiene el nombre post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Seleccione la acción en el formulario adaptable. La acción envía un correo electrónico y almacena los datos.
