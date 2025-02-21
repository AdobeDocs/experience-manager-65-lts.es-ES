---
title: Procesamiento posterior de cartas y comunicaciones interactivas
description: El procesamiento posterior de cartas en Administración de correspondencia le permite crear procesos posteriores de AEM y Forms, como imprimir y enviar por correo electrónico, e integrarlos en sus cartas.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 99%

---

# Procesamiento posterior de cartas y comunicaciones interactivas{#post-processing-of-letters-and-interactive-communications}

## Procesamiento posterior {#post-processing}

Los agentes pueden asociar y ejecutar flujos de trabajo posteriores al procesamiento en cartas y comunicaciones interactivas. El proceso posterior que se va a ejecutar se puede seleccionar en la vista Propiedades de la plantilla Carta. Puede configurar los procesos de publicación para enviar por correo electrónico, imprimir, fax o archivar las cartas finales.

![Procesamiento posterior](assets/ppoverview.png)

Para asociar procesos de publicación con cartas o comunicaciones interactivas, primero debe configurar los procesos de publicación. Se pueden ejecutar dos tipos de flujos de trabajo en las cartas enviadas:

1. **Flujo de trabajo de formularios:** estos son los flujos de trabajo de administración de procesos de AEM Forms en JEE. Instrucciones para configurar el [flujo de trabajo de formularios](#formsworkflow).

1. **Flujo de trabajo de AEM:** los flujos de trabajo de AEM también se pueden utilizar como procesos posteriores para las cartas enviadas. Instrucciones para configurar el [flujo de trabajo de AEM](../../forms/using/aem-forms-workflow.md).

## Flujo de trabajo de formularios {#formsworkflow}

1. En AEM, abra Configuración de la consola web de Adobe Experience Manager para su servidor mediante la siguiente URL: `https://<server>:<port>/<contextpath>/system/console/configMgr`

   ![Administrador de configuración](assets/2configmanager-1.png)

1. En esta página, busque Configuración del AEM Forms Client SDK y expanda la aplicación al hacer clic en ella.
1. En la URL del servidor, escriba el nombre de AEM Forms en el servidor JEE, detalles de inicio de sesión y, a continuación, haga clic en **Guardar**.

   ![Escriba el nombre del servidor de LiveCycle](assets/1cofigmanager.png)

1. Escriba el nombre de usuario y la contraseña.
1. Asegúrese de que sun.util.calendar se agrega a la configuración del firewall de deserialización

   Vaya a la configuración del firewall de deserialización y en Clases incluidas en la lista de permitidos de prefijos de paquete, agregue sun.util.calendar.

1. Ahora, los servidores están asignados y los procesos de publicación de AEM Forms en JEE están disponibles en la interfaz de usuario de AEM al crear cartas.

   ![Crear pantalla de carta con procesos de publicación enumerados](assets/0configmanager.png)

1. Para autenticar un proceso/servicio, copie el nombre de un proceso y vuelva a la página Configuración de la consola web de Adobe Experience Manager > Configuración del AEM Forms Client SDK y agregue el proceso como un nuevo servicio.

   Por ejemplo, si la lista desplegable de la página de cartas Propiedades muestra el nombre del proceso como Flujo de trabajo de formularios -> ValidCCPostProcess/SaveXML, agregue un Nnmbre de servicio como `ValidCCPostProcess/SaveXML`.

1. Para utilizar AEM Forms en flujos de trabajo de JEE para el procesamiento posterior, configure los parámetros y resultados necesarios. A continuación se indican los valores predeterminados de los parámetros.

   Vaya a la página Configuraciones de la consola web de Adobe Experience Manager > **[!UICONTROL Configuraciones de Administración de correspondencia]** y configure los siguientes parámetros:

   1. **inPDFDoc (parámetro de documento PDF):** un documento PDF como entrada. Esta entrada contiene la carta procesada como entrada. Los nombres de parámetro indicados son configurables. Se pueden configurar desde las configuraciones de Administración de correspondencia.
   1. **inXMLDoc (parámetro de datos XML):** un documento XML como entrada. Esta entrada contiene datos introducidos por el usuario en forma de XML.
   1. **inXDPDoc (parámetro de documento XDP):** un documento XML como entrada. Esta entrada contiene el diseño subyacente (XDP).
   1. **inAttachmentDocs (parámetro de documentos adjuntos):** un parámetro de entrada de lista. Esta entrada contiene todos los archivos adjuntos como entrada.
   1. **redirectURL (salida de URL de redireccionamiento):** tipo de salida que indica la dirección URL a la que se redirige.

   El flujo de trabajo de formularios debe tener como entrada un parámetro de documento PDF o un parámetro de datos XML con el mismo nombre especificado en **[!UICONTROL Configuraciones de Administración de correspondencia]**. Esto es necesario para que el proceso aparezca en la lista desplegable Procesamiento posterior.

## Configurar la instancia de publicación {#settings-on-the-publish-instance}

1. Inicie sesión en `https://localhost:publishport/aem/forms`.
1. Navegue hasta **[!UICONTROL Cartas]** para ver la carta publicada que está disponible en la instancia de publicación.
1. Configure AEM DS. Consulte [Configurar AEM DS](../../forms/using/configuring-the-processing-server-url.md).

>[!NOTE]
>
>Al utilizar Forms o flujos de trabajo de AEM, antes de realizar cualquier envío desde el servidor de publicación, es necesario configurar el servicio de configuración de DS. De lo contrario, el envío del formulario fallará.

## Recuperar instancias de carta {#letter-instances-retrieval}

Las instancias de carta guardadas se pueden manipular aún más, como la recuperación de instancias de carta y la eliminación de instancias de carta, mediante las siguientes API definidas en LetterInstanceService.

<table>
 <tbody>
  <tr>
   <td><strong>API del lado del servidor</strong></td>
   <td><strong>Nombre de la operación</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><p>LetterInstanceVO pública</p> <p>getLetterInstance(String letterInstanceId)</p> <p>Throws ICCException; </p> </td>
   <td>getLetterInstance</td>
   <td>Recuperar la instancia de carta especificada </td>
  </tr>
  <tr>
   <td>Public void deleteLetterInstance(String letterInstanceId) devuelve ICCException. </td>
   <td>deleteLetterInstance </td>
   <td>Se eliminó la instancia de letra especificada </td>
  </tr>
  <tr>
   <td>List getAllLetterInstances(Query) devuelve ICCException. </td>
   <td>getAllLetterInstances </td>
   <td>Esta API recupera instancias de cartas en función del parámetro de consulta de entrada. Para recuperar todas las instancias de cartas, el parámetro de consulta se puede pasar como nulo.<br /> </td>
  </tr>
  <tr>
   <td>Public Boolean letterInstanceExists(String letterInstanceName) devuelve ICCException. </td>
   <td>letterInstanceExists </td>
   <td>Comprobar si existe una LetterInstance con el nombre dado </td>
  </tr>
 </tbody>
</table>

## Asociar un proceso de publicación a una carta {#associating-a-post-process-with-a-letter}

En la interfaz de usuario de CCR, complete los siguientes pasos para asociar un proceso de publicación con una carta:

1. Pase el ratón sobre una carta y seleccione **Ver propiedades**.
1. Seleccione **Editar**.
1. En Propiedades básicas, mediante la lista desplegable Procesamiento posterior, seleccione el procesamiento posterior que quiera asociar con la carta. En la lista desplegable se enumeran los procesamientos posteriores de publicación relacionados con AEM y Forms.
1. Seleccione **Guardar**.
1. Después de configurar la carta con el procesamiento posterior, publique la carta y, opcionalmente, en la instancia de publicación, especifique la URL del procesamiento en el servicio de configuración de AEM DS. Esto garantiza que el procesamiento posterior se ejecute en la instancia de procesamiento.

## Volver a cargar una instancia de borrador de carta  {#reloaddraft}

Se puede volver a cargar una instancia de borrador de carta en la interfaz de usuario mediante la siguiente URL:

`https://<server>:<port>/aem/forms/`

`createcorrespondence.html?/random=$&cmLetterInstanceId=$<LetterInstanceId>`

LetterInstaceID: ID exclusivo de la instancia de carta enviada.

Para obtener más información sobre cómo guardar un borrador de carta, consulte [Guardar borradores y envíos de instancias de carta](../../forms/using/create-correspondence.md#savingdrafts).
