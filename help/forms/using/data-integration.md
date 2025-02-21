---
title: Integración de datos de AEM Forms
description: La integración de datos permite integrar AEM Forms con fuentes de datos dispares y crear un modelo de datos de formulario para crear y trabajar con formularios adaptables y comunicaciones interactivas.
contentOwner: vishgupt
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
docset: aem65
feature: Form Data Model
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 87%

---

# Integración de datos de [!DNL AEM Forms] {#aem-forms-data-integration}

![imagen a pantalla completa](do-not-localize/data-integration.png)

Las infraestructuras empresariales incluyen diferentes sistemas back-end o fuentes de datos, como bases de datos, servicios web, servicios REST, servicios OData y soluciones CRM. En conjunto, crean un sistema de información que sirve datos a las aplicaciones empresariales para realizar el trabajo diario. Por otro lado, las aplicaciones capturan datos y los envían de vuelta para actualizar las fuentes de datos.

Las aplicaciones de [!DNL AEM Forms], como los formularios adaptables y las comunicaciones interactivas, requieren la integración con fuentes de datos para recuperar los datos de los clientes mientras representan los formularios y crean las comunicaciones interactivas. Hay casos de uso en los que se recuperan datos de fuentes de datos basadas en entradas de usuarios de formularios adaptables. Además, los datos de los formularios adaptables enviados se pueden escribir de forma diferida para actualizar las fuentes de datos correspondientes.

Si bien un sistema modular y distribuido tiene sus propias ventajas, el desafío consiste en integrar y crear asociaciones de datos entre fuentes de datos. La integración de datos es la clave de una infraestructura empresarial funcional y eficiente con diferentes fuentes de datos conectadas a aplicaciones para intercambiar datos del negocio.

## Información general sobre la integración de datos {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

La integración de datos de [!DNL AEM Forms] permite configurar y conectar diferentes fuentes de datos con [!DNL AEM Forms]. Proporciona una interfaz de usuario intuitiva para crear un esquema de representación de datos unificado de entidades y servicios empresariales a través de fuentes de datos conectadas. La representación unificada se conoce como modelo de datos de formulario, una extensión del esquema JSON. Las entidades de un modelo de datos de formulario se denominan objetos de modelo de datos. Un modelo de datos de formulario le permite:

* acceder a los objetos, las propiedades y los servicios de modelo de datos desde las fuentes de datos conectadas;
* crear objetos y propiedades personalizadas para el modelo de datos;
* crear asociaciones entre objetos de modelo de datos dentro de las fuentes de datos y entre ellas;
* invocar los servicios de los objetos de modelo de datos para consultar o escribir datos desde y hacia fuentes de datos.

Una vez haya creado un modelo de datos de formulario, podrá utilizarlo en varios flujos de trabajo de formularios adaptables y comunicaciones interactivas, como:

* Crear formularios adaptables y comunicaciones interactivas basadas en el modelo de datos de formulario.
* Prerrellenar formularios adaptables y comunicaciones interactivas desde las fuentes de datos configuradas.
* Invocar servicios u operaciones de fuentes de datos mediante las reglas de los formularios adaptables.
* Escribir los datos de los formularios adaptables enviados en fuentes de datos.

## Introducción a la integración de datos {#get-started-with-data-integration}

El primer paso para implementar la integración de datos es identificar y configurar las fuentes de datos que almacenan la información que desea utilizar en los casos de uso de las comunicaciones interactivas y los formularios adaptables. A continuación, se crea un modelo de datos de formulario que utiliza los objetos, las propiedades y los servicios de modelo de datos de una o varias fuentes de datos. Puede crear formularios adaptables y comunicaciones interactivas basadas en un modelo de datos de formulario en el que los campos de los formularios adaptables o los marcadores de posición de las comunicaciones interactivas estén enlazados a las propiedades de sus respectivas fuentes de datos.

[!DNL AEM Forms] también permite crear un modelo de datos de formulario independiente de las fuentes de datos y asociar o enlazar objetos y propiedades de modelo de datos en el modelo de datos de formulario con la fuente de datos más adelante. Esto elimina la dependencia de las fuentes de datos mientras trabaja en un modelo de datos de formulario.

Revise la siguiente información para iniciar, entender e implementar la integración de datos.

* [Configurar fuentes de datos](../../forms/using/configure-data-sources.md)
* [Crear un modelo de datos de formulario](../../forms/using/create-form-data-models.md)
* [Trabajar con el modelo de datos de formulario](../../forms/using/work-with-form-data-model.md)
* [Usar el modelo de datos de formulario](../../forms/using/using-form-data-model.md)
