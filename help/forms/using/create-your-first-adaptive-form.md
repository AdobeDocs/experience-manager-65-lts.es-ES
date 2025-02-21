---
title: 'Tutorial: Crear el primer formulario adaptable'
description: Aprenda a crear formularios interactivos, adaptables y de clase empresarial.
feature: Adaptive Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 9bb44a58e919fd038c83cab89620256501137bef
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 71%

---

# Tutorial: Crear el primer formulario adaptable {#tutorial-create-your-first-adaptive-form}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html?lang=es) |
| AEM 6.5 | Este artículo |


![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Introducción {#introduction}

¿Está buscando una experiencia de **formularios** compatible con dispositivos móviles que simplifique la inscripción, aumente la participación y reduzca el tiempo de respuesta? **los formularios adaptables** son perfectos para usted. Los formularios adaptables proporcionan una experiencia adaptada para móviles, automatizada y analítica. Puede crear fácilmente formularios que sean interactivos y adaptables, utilizar procesos automatizados para reducir las tareas administrativas y repetitivas y utilizar análisis de datos para mejorar y personalizar la experiencia que los clientes tienen con sus formularios.

Este tutorial proporciona un marco de trabajo completo para crear un formulario adaptable. El tutorial está organizado en un caso de uso y en varias guías. Cada guía le ayuda a aprender y agregar nuevas características al formulario adaptable que cree en este tutorial. Después de cada guía, tendrá un formulario adaptable operativo. La guía para crear un formulario adaptable está disponible. Próximamente habrá más guías. Al final de este tutorial, debería poder hacer lo siguiente:

* Crear un formulario adaptable y un modelo de datos de formulario.
* Establecer el estilo de su formulario adaptable.
* Utilizar el editor de reglas de formulario adaptable para crear reglas empresariales.
* Probar y publicar un formulario adaptable.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

El recorrido comienza con el aprendizaje del caso de uso:

Un sitio web ofrece una amplia gama de productos para diversos clientes. Los clientes examinan el portal, seleccionan y solicitan los productos. Cada cliente crea una cuenta y proporciona direcciones de envío y de facturación. Una cliente, Sara Rose, quiere agregar su dirección de envío al sitio web. El sitio web proporciona un formulario en línea para agregar y actualizar las direcciones de envío.

El sitio web se ejecuta en Adobe Experience Manager (AEM) y utiliza AEM [!DNL Forms] para recoger y procesar los datos. El formulario de adición y actualización de direcciones es un formulario adaptable. El sitio web almacena los detalles del cliente en una base de datos. Se utiliza el formulario de adición y actualización de direcciones para recuperar y mostrar las direcciones disponibles. También se utiliza el formulario adaptable para aceptar direcciones nuevas y actualizadas.

### Requisitos previos {#prerequisite}

* Configurar una [instancia de autor de AEM](https://experienceleague.adobe.com/docs/experience-manager-65-2025/content/implementing/deploying/deploying/deploy.html#author-and-publish-installs)
* Instalar el [Complemento de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) en la instancia de autor.
* Obtener el controlador de base de datos JDBC (archivo JAR) del proveedor de la base de datos. Los ejemplos del tutorial se basan en la base de datos [!DNL MySQL] y utiliza el [!DNL Oracle's] [Controlador de base de datos JDBC de MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Configure una base de datos que contenga datos de clientes con los campos que se muestran a continuación. Una base de datos no es esencial para crear un formulario adaptable. Este tutorial utiliza una base de datos para mostrar el modelo de datos de formulario y las capacidades de persistencia de AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Paso 1: Crear un formulario adaptable {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Los formularios adaptables son de nueva generación, atractivos, interactivos, dinámicos y adaptables. Gracias a los formularios adaptables, puede ofrecer experiencias personalizadas y segmentadas. AEM [!DNL Forms] proporciona un editor WYSIWYG de arrastrar y soltar para crear formularios adaptables. Para obtener más información sobre los formularios adaptables, consulte [Introducción a la creación de formularios adaptables](../../forms/using/introduction-forms-authoring.md).

Objetivos:

* Crear un formulario adaptable que permita a un cliente agregar una dirección de envío.
* Diseñar campos de un formulario adaptable para mostrar y aceptar información de un cliente.
* Cree una acción de envío para enviar un correo electrónico que contenga contenido de formulario.
* Previsualizar y enviar un formulario adaptable.

[![Consulte la guía](assets/see-the-guide-sm.png)](create-adaptive-form.md)

## Paso 2: Crear un modelo de datos de formulario {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Un modelo de datos de formulario permite conectar un formulario adaptable a distintas fuentes de datos. Por ejemplo, un perfil de usuario de AEM, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Un modelo de datos de formulario es un esquema de representación de datos unificado de entidades y servicios empresariales disponibles en fuentes de datos conectadas. Puede utilizar el modelo de datos de formulario con un formulario adaptable para recuperar, actualizar, eliminar y agregar datos a fuentes de datos conectadas.

Objetivos:

* Configure la instancia de base de datos del sitio web (base de datos [!DNL MySQL]) como origen de datos.
* Cree el modelo de datos de formulario con la base de datos [!DNL MySQL] como origen de datos.
* Agregar objetos del modelo de datos para poder formar el modelo de datos.
* Configure los servicios de lectura y escritura para el modelo de datos de formulario.
* Probar el modelo de datos de formulario y los servicios configurados con datos de prueba.

[![Consulte la guía](assets/see-the-guide-sm.png)](create-form-data-model.md)

## Paso 3: Aplicar reglas a campos de formulario adaptables {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Los formularios adaptables proporcionan un editor para escribir reglas sobre objetos de formulario adaptables. Estas reglas definen las acciones que se deben habilitar en los objetos del formulario en función de los ajustes preestablecidos, las entradas del usuario y las acciones del usuario en el formulario. Ayuda a garantizar la precisión y acelera la experiencia de cumplimentación de formularios.

Objetivos:

* Cree y aplique reglas en los campos de formulario adaptables.
* Utilice reglas para almacenar en déclencheur los servicios del modelo de datos de formulario para actualizar los datos a la base de datos.

[![Consulte la guía](assets/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Paso 4: Estilo del formulario adaptable {#step-style-your-adaptive-form}

![estilo-formulario-adaptable](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

Los formularios adaptables proporcionan temáticas y un [editor](../../forms/using/themes.md) para crear temáticas para los formularios adaptables. Una temática contiene detalles de estilo para componentes y paneles y se puede reutilizar el mismo en distintos formularios. Los estilos incluyen propiedades como colores de fondo, colores de estado, transparencia, alineación y tamaño. Al aplicar la temática al formulario, el estilo especificado se reflejará en los componentes correspondientes del formulario. Los formularios adaptables también admiten el estilo en línea para estilos específicos de un formulario.

Objetivos:

* Aplicar una temática predeterminada a un formulario adaptable.
* Cree una temática para el formulario adaptable mediante el editor de temáticas.
* Usar Web Fonts en una temática personalizada.

[![Consulte la guía](assets/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Paso 5: Publicar el formulario adaptable {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Puede publicar formularios adaptables como un formulario independiente (aplicación de una sola página), incluido en la [página de AEM Sites](/help/forms/using/embed-adaptive-form-aem-sites.md)o una lista en un [!DNL Site] de AEM mediante el [portal de formularios](../../forms/using/introduction-publishing-forms.md).

Objetivos:

* Publique el formulario adaptable como una página de AEM.
* Incruste el formulario adaptable en una página de AEM [!DNL Sites].
* Incruste el formulario adaptable en una página web externa (una página web que no sea de AEM y esté alojada fuera de AEM).

[![Consulte la guía](assets/see-the-guide-sm.png)](publish-your-adaptive-form.md)
