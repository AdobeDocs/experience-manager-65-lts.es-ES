---
title: Crear una plantilla de formulario adaptable personalizada
description: Este artículo describe cómo crear plantillas de formulario adaptables personalizadas.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 98%

---

# Crear una plantilla de formulario adaptable personalizada{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>AEM Forms ha introducido plantillas dinámicas. Puede utilizar el editor de plantillas de AEM Sites para [crear o editar plantillas dinámicas](../../forms/using/template-editor.md). Las plantillas mencionadas en el siguiente artículo son plantillas estáticas. No están disponibles en una instalación predeterminada. [Instale el paquete de compatibilidad](../../forms/using/compatibility-package.md) para obtener estas plantillas en su entorno.

## Requisitos previos {#prerequisites}

* Comprender la [Plantilla de la página de AEM](/help/sites-authoring/templates.md) y [la creación de formularios adaptables](https://helpx.adobe.com/es/aem-forms/6-1/introduction-forms-authoring.html)

* Comprender las [Bibliotecas de cliente de AEM](/help/sites-developing/clientlibs.md)

## Plantillas de formularios adaptables {#adaptive-form-template}

Una plantilla de formulario adaptable es una plantilla de la página de AEM especializada, con determinadas propiedades y estructura de contenido que se utiliza para crear el formulario adaptable. La plantilla tiene diseños, estilos y estructuras de contenido inicial básicas preconfigurados.

Una vez creado un formulario, los cambios realizados en la estructura de contenido de la plantilla original no se reflejarán en el formulario.

## Plantillas de formulario adaptables predeterminadas {#default-adaptive-form-templates}

AEM QuickStart proporciona las siguientes plantillas de formulario adaptables:

* Plantilla de encuesta: permite crear un formulario adaptable de una sola página con el diseño adaptable que tiene varias columnas configuradas. La presentación se ajusta automáticamente en función de las dimensiones de las distintas pantallas en las que desea mostrar el formulario.
* Plantilla de inscripción simple: permite crear un formulario adaptable de varios pasos con una presentación de asistente. En este diseño, se puede especificar una expresión de finalización de paso para cada paso, que se validará antes de que el asistente continúe con el siguiente paso.
* Plantilla de inscripción tabulada: permite crear un formulario adaptable con varias pestañas mediante una presentación de pestañas a la izquierda, donde puede visitar las pestañas en cualquier orden aleatorio.
* Plantilla de inscripción avanzada: permite crear un formulario con varias pestañas y un asistente. Utiliza un diseño de pestañas a la izquierda que permite visitar las pestañas en cualquier orden. Utiliza los servicios de Adobe Document Cloud Design para la firma y verificación.
* Plantilla en blanco: permite crear un formulario sin encabezado, pie de página ni contenido inicial. Puede agregar componentes, como cuadros de texto, botones e imágenes. La plantilla en blanco permite crear un formulario que puede [incrustar en páginas de AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md).

Estas plantillas tienen la propiedad `sling:resourceType` establecida en el componente de página correspondiente. El componente de página procesa la página de CQ, que contiene el contenedor de formulario adaptable, que a su vez procesa el formulario adaptable.

La siguiente tabla enumera la asociación entre las plantillas y el componente de página:

<table>
 <tbody>
  <tr>
   <td><p><strong>Plantilla</strong></p> </td>
   <td><p><strong>Componente Página </strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## Crear una plantilla de formulario adaptable mediante el editor de plantillas {#creating-an-adaptive-form-template-using-template-editor}

Puede especificar la estructura y el contenido inicial de un formulario adaptable mediante el Editor de plantillas. Por ejemplo, si quiere que todos los autores de formularios tengan ciertos cuadros de texto, botones de navegación y un botón de envío en un formulario de registro. Puede crear una plantilla que los autores puedan utilizar para crear un formulario coherente con otros formularios de registro. El Editor de plantillas de AEM le permite lo siguiente:

* Agregar componentes de encabezado y pie de página de un formulario en la capa de estructura
* Proporcionar el contenido inicial para el formulario.
* Especificar una temática.
* Especificar acciones como enviar, restablecer y navegar.

Para obtener más información, consulte [Editor de plantillas](../../forms/using/template-editor.md).

## Crear una plantilla de formulario adaptable a partir de CRXDE {#creating-an-adaptive-form-template-from-crxde}

En lugar de utilizar las plantillas disponibles, puede crear una y utilizarla para crear formularios adaptables. Las plantillas personalizadas se basan en varios componentes de página que hacen referencia a contenedores de formularios adaptables y elementos de página, como el encabezado y el pie de página.

Puede crear estos componentes mediante el componente de página base para el sitio web. También puede ampliar el componente de página del formulario adaptable que utilizan las plantillas listas para usar.

Realice los siguientes pasos para crear una plantilla personalizada, como simpleEnrollmentTemplate.

1. Navegue hasta CRXDE Lite de la instancia de autor.

1. En el directorio /apps, cree la estructura de carpetas para la aplicación. Por ejemplo, si el nombre de la aplicación es mycompany, cree una carpeta con este nombre. Normalmente, la carpeta de la aplicación contendrá componentes, configuración, plantillas, src y directorios de instalación. Para este ejemplo, cree las carpetas de componentes, configuración y plantillas.

1. Navegue hasta la carpeta /libs/fd/af/templates.
1. Copie el nodo `simpleEnrollmentTemplate`.
1. Navegue hasta la carpeta /apps/mycompany/templates. Haga clic con el botón derecho y seleccione **[!UICONTROL Pegar]**.
1. Si es necesario, cambie el nombre del nodo de plantilla que ha copiado. Por ejemplo, cambie el nombre a enrollment-template.

1. Navegue hasta la ubicación /apps/mycompany/templates/enrollment-template.

1. Modifique las propiedades `jcr:title` y `jcr:description` del nodo `jcr:content` para distinguir la plantilla de la plantilla copiada.

1. El nodo `jcr:content` de la plantilla modificada contiene los componentes `guideContainer` y `guideformtitle`. `guideContainer` es el contenedor que contiene el formulario adaptable. El componente `guideformtitle` muestra el nombre de la aplicación, la descripción, etc.

   En lugar de `guideformtitle`, puede incluir un componente personalizado o el componente`parsys`. Por ejemplo, quite `guideformtitle` y agregue un componente personalizado o el nodo de componente `parsys`. Asegúrese de que la propiedad `sling:resourceType` del componente hace referencia al componente y se define lo mismo en el archivo de la página `component.jsp`.

1. Navegue hasta la ubicación /apps/mycompany/templates/enrollment-template/jcr:content.

1. Abra la pestaña **[!UICONTROL Propiedades]** y cambie el valor de la propiedad `cq:designPath` a /etc/designs/mycompany.

1. Ahora cree un nodo /etc/designs/mycompany para el tipo `cq:Page`.

## Crear un componente de página de formulario adaptable {#create-an-adaptive-form-page-component}

La plantilla personalizada tiene el mismo estilo que la plantilla predeterminada porque hace referencia al componente de página /libs/fd/af/components/page/base. Puede encontrar la referencia del componente como la propiedad `sling:resourceType` definida en el nodo /apps/mycompany/templates/enrollment-template/jcr:content. Como base es un componente de producto principal, no modifique este componente.

1. Navegue hasta el nodo /apps/mycompany/templates/enrollment-template/jcr:content y modifique el valor de la propiedad `sling:resourceType` a /apps/mycompany/components/page/enrollmentpage
1. Copie el nodo /libs/fd/af/components/page/base en la carpeta /apps/mycompany/components/page.

1. Cambie el nombre del componente copiado a `enrollmentpage`.

1. **(Solo si ya tiene una página de contenido)** Realice los siguientes pasos (a-d), si ya tiene un componente `contentpage` para su sitio web. Si no tiene un componente `contentpage` existente para su sitio web, puede dejar la propiedad `resourceSuperType`para que apunte a la página base predeterminada.

   1. Para el nodo `enrollmentpage`, establezca el valor de la propiedad `sling:resourceSuperType` a mycompany/components/page/contentpage. El componente `contentpage` es el componente de la página base del sitio. Otros componentes de página pueden ampliarlo. Quite los archivos del script en `enrollmentpage`, excepto `head.jsp`, `content.jsp` y `library.jsp`. El componente `sling:resourceSuperType`, que es `contentpage` en este caso, incluye todos esos scripts. Los encabezados, incluidas la barra de navegación y el pie de página, se heredan del componente `contentpage`.

   1. Abra el archivo `head.jsp`.

      El archivo JSP contiene la línea `<cq.include script="library.jsp"/>`.

      El archivo `library.jsp` contiene la biblioteca de cliente`guide.theme.simpleEnrollment`, que contiene el estilo del formulario adaptable.

      El componente de página `enrollmentpage` tiene un archivo exclusivo `head.jsp` que anula el archivo `head.jsp` del componente`contentpage`.

   1. Incluya todos los scripts en el archivo `head.jsp` para el componente `contentpage`al archivo `head.jsp` para el componente`enrollmentpage`.
   1. En el script `content.jsp`, puede agregar contenido de página adicional o referencias a otros componentes que se incluyen cuando se procesa una página. Por ejemplo, si agrega el componente personalizado `applicationformheader`, asegúrese de agregar la siguiente referencia al componente en el archivo JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Del mismo modo, si agrega un componente `parsys` en la estructura del nodo de la plantilla, incluya también el componente personalizado.

## Crear una biblioteca de cliente de formulario adaptable {#creating-an-adaptive-form-client-library}

El archivo `head.jsp` del componente `enrollmentpage` para la nueva plantilla incluye una biblioteca de cliente `guide.theme.simpleEnrollment`. La plantilla predeterminada también utiliza esta biblioteca de cliente. Cambie el estilo en la plantilla nueva mediante uno de estos métodos:

* Definir una temática personalizada y reemplazar la predeterminada `guide.theme.simpleEnrollment` con la personalizada.
* Definir una nueva biblioteca de cliente en /etc/designs/mycompany. Incluir la biblioteca de cliente después de la entrada de la temática predeterminada en la página jsp. Incluir todos los estilos anulados y archivos JavaScript adicionales en esta biblioteca de cliente.

>[!NOTE]
>
>La temática hace referencia a una biblioteca de cliente que se incluye en el componente de página que se utiliza para procesar un formulario adaptable. La biblioteca de cliente rige principalmente el aspecto de un formulario adaptable.
