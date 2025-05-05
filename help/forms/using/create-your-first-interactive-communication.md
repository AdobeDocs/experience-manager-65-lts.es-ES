---
title: 'Tutorial: Cree su primera comunicación interactiva'
description: Aprenda a crear su primera comunicación interactiva.
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 98%

---

# Tutorial: Crear la primera comunicación interactiva {#tutorial-create-your-first-interactive-communication}

Aprenda a crear su primera comunicación interactiva.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Las comunicaciones interactivas centralizan y administran la creación, la combinación y la entrega de correspondencia segura, personalizada e interactiva, como correspondencia comercial, documentos, declaraciones, correos de marketing, facturas y kits de bienvenida. Las comunicaciones interactivas pueden entregarse mediante dos canales: Imprimir y Web. El canal Imprimir se utiliza para crear PDF y comunicaciones en papel, mientras que el canal Web se utiliza para ofrecer experiencias en línea.

Este tutorial proporciona un marco de trabajo completo para crear una comunicación interactiva. El tutorial está organizado en un caso de uso y en varias guías. Cada guía le ayudará a crear características que se utilizan como componentes básicos para crear una comunicación interactiva.

La siguiente imagen ilustra los componentes básicos necesarios para crear una comunicación interactiva.

![flujo de trabajo](assets/workflow.gif)

Al final de este tutorial, podrá:

* Crear bloques de creación (modelo de datos de formulario, fragmentos de documento y plantillas)
* Crear una comunicación interactiva
* Probar y publicar una comunicación interactiva

## Caso de uso {#use-case}

El recorrido comienza con el aprendizaje del caso de uso:

Un operador de telecomunicaciones envía facturas mensuales a los clientes por correo electrónico. La factura es una comunicación interactiva. El correo electrónico incluye lo siguiente:

* Un PDF protegido mediante contraseña, denominado Canal Imprimir en este tutorial. Incluye detalles de clientes y de facturas, resumen de gastos, modos prácticos de pagar las facturas y detalles de uso.
* Un vínculo a la versión web de la lista, denominado Canal Web en este tutorial. La versión web de la factura, además de los detalles cubiertos en la versión PDF, proporciona una representación gráfica de los detalles de uso y las ofertas personalizadas basadas en Adobe Target. La versión web también contiene un formulario de pago en línea. Ayuda a realizar pagos en línea sin salir del IC.
* Un vínculo a servicios de valor agregado, como almacenamiento en línea, suscripciones de música y de vídeo bajo demanda.

## Requisitos previos {#prerequisites}

* Configure una instancia de autor de AEM.
* Instale el [Complemento de AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) en la instancia de autor
* Configure la base de datos MYSQL
* Obtenga el controlador de base de datos JDBC (archivo JAR) del proveedor de la base de datos. Los ejemplos del tutorial se basan en la base de datos MySQL y utilizan el [Controlador de la base de datos JDBC de MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html) de Oracle.

## Paso 1: Planificar la comunicación interactiva {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

El primer paso de la planificación de una comunicación interactiva es finalizar el contenido de la comunicación. Una vez finalizado, debe analizarlo para identificar los distintos tipos de recursos necesarios para crear la comunicación interactiva.

**Objetivos:**

Crear una anatomía para la comunicación interactiva con los siguientes modos de entrada de datos:

* Texto estático
* Modelo de datos de formulario
* IU del Agente
* Datos condicionales
* Imágenes

[&#128279;](/help/forms/using/planning-interactive-communications.md)

## Paso 2: Crear un modelo de datos de formulario {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Un modelo de datos de formulario permite conectar una comunicación interactiva a distintas fuentes de datos. Por ejemplo, un perfil de usuario de AEM, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Un modelo de datos de formulario es un esquema de representación de datos unificado de entidades y servicios empresariales disponibles en fuentes de datos conectadas. Puede utilizar el modelo de datos de formulario con una comunicación interactiva para recuperar datos de fuentes de datos conectadas. Para obtener información sobre el modelo de datos de formulario, consulte [Integración de datos de AEM Forms](/help/forms/using/data-integration.md).

**Objetivos:**

* Configurar la instancia de la base de datos (base de datos MySQL) como fuente de datos
* Crear el modelo de datos de formulario con la base de datos MySQL como fuente de datos
* Agregar objetos del modelo de datos al modelo de datos de formulario
* Configurar servicios de lectura y escritura para el modelo de datos de formulario
* Crear asociaciones entre los objetos del modelo de datos
* Ver datos de ejemplo generados automáticamente
* Editar datos de muestra
* Probar el modelo de datos de formulario y los servicios configurados con datos de prueba

[&#128279;](/help/forms/using/create-form-data-model0.md)

## Paso 3: Crear fragmentos de documento {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Los fragmentos de documento son componentes reutilizables de una correspondencia que se utilizan para componer una comunicación interactiva. Los fragmentos de documento son de tipo: Texto, Lista y Condición.

**Objetivos:**

* Crear fragmentos de documento
* Crear variables
* Crear y aplicar reglas

[&#128279;](/help/forms/using/create-document-fragments.md)

## Paso 4: Crear plantillas {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Para crear una comunicación interactiva, debe tener plantillas disponibles en el servidor de AEM para los canales Imprimir y Web.

Las plantillas del canal Imprimir se crean en Adobe Forms Designer y se cargan en el servidor de AEM. Estas plantillas están disponibles para su uso durante la creación de una comunicación interactiva.

Las plantillas del canal Web se crean en AEM. Los autores y administradores de plantillas pueden crear, editar y habilitar plantillas web. Una vez creadas y habilitadas, estas plantillas están disponibles para usarlas durante la creación de una comunicación interactiva.

**Objetivos:**

* Crear plantillas XDP para el canal Imprimir mediante Adobe Forms Designer
* Cargar las plantillas XDP al servidor de AEM Forms
* Crear y habilitar plantillas para el canal Web

[&#128279;](/help/forms/using/create-templates-print-web.md)

## Paso 5: Crear una comunicación interactiva {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Una vez creados todos los componentes básicos, como el modelo de datos de formulario, los fragmentos de documento y las plantillas para la versión web, puede empezar a crear una comunicación interactiva.

Las comunicaciones interactivas se pueden entregar a través de dos canales: Imprimir y Web. También puede crear una comunicación interactiva con el canal Imprimir como principal. La opción Imprimir como principal del canal Web garantiza que el contenido, la herencia y el enlace de datos del canal Web se deriven del canal Imprimir.

**Objetivos:**

* Crear una comunicación interactiva para el canal Imprimir
* Crear una comunicación interactiva para el canal Web
* Crear comunicaciones interactivas Imprimir y Web con Imprimir como principal
* Crear una tabla dinámica en la versión web de la comunicación interactiva
* Crear un gráfico en la versión web de la comunicación interactiva
* Crear hipervínculos en la versión web de la comunicación interactiva

[&#128279;](/help/forms/using/create-interactive-communication0.md)

## Paso 6: Publicar la comunicación interactiva {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Una vez que haya creado y probado las comunicaciones interactivas mediante los canales Imprimir y Web, podrá publicar estos recursos. El caso de uso descrito en este tutorial se centra en la integración de estos recursos con un cliente de correo electrónico. El cliente de correo electrónico sirve como puente para enviar las comunicaciones interactivas a varias direcciones de correo electrónico.

**Objetivos:**

* Integrar las comunicaciones interactivas con un cliente de correo electrónico para poder enviar una comunicación a los clientes
* Incluir un documento PDF como adjunto (comunicación interactiva creada en el canal Imprimir)
* Incluir un vínculo a la versión web de la comunicación interactiva
