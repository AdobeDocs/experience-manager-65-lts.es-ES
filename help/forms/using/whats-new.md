---
title: Resumen de las nuevas funciones | AEM 6.5 Forms
description: Últimas funciones y mejoras en formularios y documentos de AEM, la solución de administración de experiencias digitales más avanzada del mundo.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Release Information
role: Admin, User, Developer
hide: true
hidefromtoc: true
exl-id: 4db457d2-fefb-410d-8e74-58147f52bbd3
source-git-commit: 4ce7de628810e13f96361c0b253ef12850985ade
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 3%

---

# Resumen de las nuevas funciones | AEM 6.5 Forms{#new-features-summary-aem-forms}

| Producto | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Versión | 6.5.19.0 |
| Tipo | Versión del paquete de servicio |
| Fecha | sábado, 08 de diciembre de 2023 |

## Qué se incluye en el paquete de servicio 19 de Adobe Experience Manager 6.5 Forms (6.5.19.0)

Experience Manager 6.5.19.0 incluye nuevas funciones, mejoras clave solicitadas por el cliente, correcciones de errores y mejoras de rendimiento, estabilidad y seguridad que se han publicado desde la publicación inicial de la versión 6.5 en abril de 2019.

### Nuevas funciones

#### Nuevos componentes principales de formulario adaptable

Se agregan pestañas verticales, Términos y condiciones y Casilla de verificación para mejorar la escalabilidad de los formularios.

* **[Componente de casilla de verificación](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=es)**: los Forms adaptables basados en componentes principales ahora pueden incluir un componente de casilla de verificación. Permite a los usuarios realizar elecciones binarias, seleccionando o anulando la selección de una opción en particular. Normalmente aparece como un pequeño cuadro en el que se puede hacer clic o pulsar para alternar entre dos estados: activado y desactivado. La casilla de verificación es un elemento de formulario común que se utiliza para presentar una opción sí/no o verdadero/falso.

* **[Componente Términos y condiciones](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=es)**: el Forms adaptable basado en componentes principales ahora puede incluir un componente Términos y condiciones. Permite a los autores de formularios introducir una sección específica dentro del formulario en la que se presentan a los usuarios los términos, condiciones o acuerdos legales asociados al uso de un servicio, producto o plataforma. Este componente está diseñado para informar a los usuarios sobre las reglas, regulaciones y obligaciones que aceptan enviando el formulario.

  ![Fichas verticales, términos y condiciones y componentes de casilla de verificación](/help/forms/using/assets/forms-components.png)

* **[Componente de pestañas verticales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=es)**: los Forms adaptables basados en componentes principales ahora pueden organizar el contenido del formulario en una lista vertical de pestañas, lo que proporciona un diseño estructurado y navegable. El uso de pestañas verticales en un formulario puede mejorar la experiencia general del usuario al simplificar la navegación y mejorar la organización del contenido del formulario, especialmente en situaciones en que un formulario contiene varias secciones o información compleja.

#### Versión de 64 bits de AEM Forms Designer

La [versión de 64 bits de AEM Forms Designer](/help/forms/using/installing-configuring-designer.md) ofrece un rendimiento, una escalabilidad y una administración de memoria mejorados para potenciar su experiencia de creación de formularios. Con la arquitectura de 64 bits, puede abordar proyectos aún más grandes y complejos con facilidad, lo que garantiza flujos de trabajo de diseño sin problemas y eficiencia optimizada. Aumente sus capacidades de diseño de formularios y disfrute del futuro de AEM Forms Designer con esta versión de vanguardia.

#### Conectar un Forms adaptable con Microsoft® SharePoint List

AEM Forms proporciona una integración predeterminada para [enviar datos de formularios directamente a la SharePoint List](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list)), lo que le permite utilizar las capacidades de Listas de SharePoint. Puede configurar la lista de Microsoft® SharePoint como fuente de datos para un modelo de datos de formulario y utilizar la acción de envío Enviar mediante el modelo de datos de formulario para conectar un formulario adaptable con una lista de SharePoint.

#### Compatibilidad para configurar las propiedades del documento de registro para los fragmentos de formulario adaptable

Ahora puede [personalizar fácilmente sus fragmentos de formulario adaptable y sus campos en el editor de formularios adaptables](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

#### Incluye la versión de 64 bits de XMLFM

La iteración de 64 bits de XMLFM presenta un rendimiento, escalabilidad y administración de memoria mejorados. Es el primer servicio nativo de 64 bits implementado en el lado del servidor. Al aprovechar su capacidad inherente para acceder a recursos de memoria significativamente mayores en comparación con su homólogo de 32 bits, XMLFM de 64 bits permite la gestión perfecta de cargas de trabajo de procesamiento más grandes. Este hito no solo representa un salto en el rendimiento, sino que también introduce mejoras clave en el marco de servicio nativo dentro del servidor de AEM Forms. Esta actualización equipa al servidor de AEM Forms para admitir sin problemas cualquier servicio nativo de 64 bits.


## Correcciones de errores

La versión también incluye correcciones para más de 20 problemas notificados por los clientes. Para obtener una lista detallada de las correcciones incluidas en el Service Pack, consulte [notas de la versión](/help/release-notes/release-notes.md)


## Instalación del Service Pack

El Service Pack ofrece nuevas funciones y correcciones de errores tanto para AEM Forms en JEE como para AEM Forms en OSGi. Las instrucciones de instalación tienen cambios en comparación con los Service Packs anteriores. Para obtener instrucciones de instalación, consulte [Instrucciones de instalación del Service Pack de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-65-lts/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=en).




<!-- 
## Transaction Reports {#transaction-reports}



Transaction reports lets you capture and track the number of submitted forms, processed documents, and rendered documents. The objective behind tracking these transactions is to make an informed decision about the product usage and rebalancing investments in hardware and software. Some examples of transactions include:

* Submission of an Adaptive Form, an HTML5 Form, or a Form Set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For information about configuring and using transaction reports, see [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md).

![A sample transaction report](assets/surface_transaction_reporting.png)

## Interactive Communications {#interactive-communications}

**Define data display patterns**

Interactive Communication authors can now define [data display patterns](create-interactive-communication.md#datadisplaypatterns) for fields, variables, and form data model elements. For example, date, currency, or phone formats.

**Use new types of charts**

You can now add [Quadrant charts and charts with multiple series](../../forms/using/chart-component-interactive-communications.md) to Interactive Communications.

**Sort columns in a table**

You can now [sort columns of a table](../../forms/using/create-interactive-communication.md#sortcolumns) in the Interactive Communication. You can bind and sort table columns with static text or data model objects.

**Use new components in a web channel**

You can now add Button and Separator components to the web channel. For more information, see [Add Button component to the web channel](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) and [Separator component in web channel](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Layout mode to resize components**

You can now switch to [Layout mode](../../forms/using/resize-using-layout-mode.md) to resize components in the Web channel using a WYSIWYG interface.

**Usability improvements**

Interactive Communication authors can now utilize various easy-to-use operations while creating correspondences. The list of operations includes:

* [Perform undo-redo actions in print and web channels](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Add variables in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Add data model elements in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Delete or add a web channel to an existing Interactive Communication](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Bind data source elements with fields and variables using drag-and-drop actions](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Highlight unbound fields and variables while authoring Interactive Communication](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Perform additional actions such as copy, group, or more on inherited components in a web channel](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Improvements in sync process**

There are several improvements in the Web channel layout auto-generated using the Print channel.

![Interactive Communications Charts](assets/interactive-communication-charts.png)

## Adaptive Forms {#adaptive-forms}

### Use Adobe Sign's cloud-based digital signatures in Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Cloud-based digital signatures](https://helpx.adobe.com/es/sign/kb/digital-certificate-providers.html) or remote signatures are a new generation of digital signatures that work across desktop, mobile, and the web — and meet the highest levels of compliance and assurance for signer authentication. You can now [sign an Adaptive Form](../../forms/using/working-with-adobe-sign.md) with Cloud-based digital signatures.

#### Embed an Adaptive Form or Interactive Communication in AEM Sites Single Page Applications {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms lets you [seamlessly embed an Adaptive Form](../../forms/using/embed-adaptive-form-aem-sites-spa.md) or Interactive Communication in an AEM Sites single page application (SPA). The embedded Adaptive Form and Interactive Communication is fully functional and users can fill and submit the form without leaving the page. It helps user remain in context of other elements on the web page and simultaneously interact with the adaptive form or Interactive Communication.

#### Sort columns of Adaptive Form tables {#sort-columns-of-adaptive-form-tables}

You can [sort any column of an Adaptive Form table](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) in an ascending or descending order. You can apply sorting to table columns with static text, data model object properties, or a combination of static text and data model object properties.

#### Restrict the availability of Adaptive Forms templates to specific paths {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Adaptive forms has added support for the cq:allowedPaths property. The property [restricts availability of Adaptive Forms templates to specific paths](creating-adaptive-form.md#adaptive-form-templates).

#### Add check boxes to the Adaptive Form dynamically {#add-check-boxes-to-the-adaptive-form-dynamically}

You can now define rules to [add checkboxes to the Adaptive Form dynamically](../../forms/using/rule-editor.md#setpropertyrule) based on custom function, a form object, or an object property.

## AEM Workflows {#aem-workflows}

### Use variables in AEM Workflows {#use-variables-in-aem-workflows}

Variables enable workflow steps to hold and pass metadata across workflow steps at runtime. You can create different types of variables for storing different types of data. For example, integers, strings, documents, or form data model instances. Typically, you use a variable or a collection of variables when you need to make a decision based on the value that it holds or to store information that you need later in a process.

Variables are an extension of [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interface available in the previous version. It helps save time spent in developing custom ECMAScript code used to retrieve and update metadata values. You continue using MetaDataMap interface and ECMAScript code to manipulate metadata. Some benefits of using variables over MetaDataMap and ECMAScript are:

* Dynamically store, update, and use values stored in a variable across the workflow without relying on custom code
* Retrieve and update values directly to a form data model and data file (XML/JSON ) of a submitted form
* Store complete documents in a variable to perform document processing

The Go To step, OR Split step, and all AEM Forms workflow steps support variables. You can use MetaDataMap interface to access variables in workflow steps that do not have a native support for variables. For more information, see [Variables in AEM Workflows](../../forms/using/variable-in-aem-workflows.md).

![Setting a variable for in a workflow](assets/variable.png)

#### Use a workflow with different Adaptive Forms  {#use-a-workflow-with-different-adaptive-forms}

You can [specify an Adaptive Form for the assign task](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) and document of record step of form-centric workflows on the runtime. It allows a workflow to work with different Adaptive Forms. You can decide the method to select an Adaptive Form while designing the workflow. The Adaptive Form can be located at an absolute path, submitted as payload to the workflow, or available at a path calculated using a variable.

#### Use enhanced logging capabilities of forms-centric workflow steps {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Logging capabilities of forms-centric workflow steps are standardized. Now, all form-centric workflow steps produce similarly standardized logs. It helps improve debugging speed.

## Data Integration {#data-integration}

You can now:

* [Validate input data](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) based on a list of constraints. It helps ensure that only valid data is submitted to data source.
* [Override default endpoint](../../forms/using/configure-data-sources.md#configure-soap-web-services) defined in a WSDL (Web Services Description Language) file.

* [Override default](../../forms/using/configure-data-sources.md#configure-restful-web-services) [scheme, host, and base path](../../forms/using/configure-data-sources.md#configure-restful-web-services) defined in Swagger definition file.

## Platform and Security updates {#platform-and-security-updates}

### Major platform updates {#major-platform-updates}

AEM Forms can be set up using any combination of supported operating systems, application servers, databases, database drivers, JDK, LDAP servers, and email servers. The following are the major changes in [supported platforms](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Component</td>
   <td>Support Removed</td>
  </tr>
  <tr>
   <td>Operating systems</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Application servers<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty profile</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Databases</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP servers</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Email servers</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Connectors</td>
   <td>
    <ul>
     <li>Connector for Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1 support</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; Contact Adobe Support for information on migrating to a different platform

#### New HTML5-based UIs {#new-html-based-uis}

In line with planned EOL of Adobe Flash Player and overall direction of migrating Flash-based content to open standards, AEM 6.5 Forms has replaced Flash-based UI of Health Monitor, Process Management, Reader Extension, and Category Management UI of AEM Forms on JEE Administration Console with HTML5-based UI.

#### Security improvements {#security-improvements}

* AEM 6.5 Forms on JEE administration console UI is now based on Apache Struts 2.5.
* AEM 6.5 Forms now uses jQuery to 3.2.1 and jQuery UI 1.12.1. See, [upgrade documentation](/help/forms/using/introduction-aem-forms.md) for the impact of the change.

#### Accessibility improvements {#accessibility-improvements}

AEM 6.5 Forms has improved accessibility of AEM Forms Workspace. 
!-->
