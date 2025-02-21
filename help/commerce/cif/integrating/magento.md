---
title: Integración de AEM y Adobe Commerce con Commerce integration framework
description: AEM y Adobe Commerce se integran perfectamente con Commerce integration framework (CIF). CIF permite a AEM acceder a una instancia de Adobe Commerce y comunicarse con Adobe Commerce a través de GraphQL. También permite a los autores de AEM utilizar los seleccionadores de productos y categorías, así como la consola de productos para examinar los datos de productos y categorías que se obtienen a petición de Adobe Commerce Además, CIF ofrece una tienda predeterminada que puede acelerar los proyectos de comercio.
thumbnail: aem-magento-architecture.jpg
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 23%

---

# Integración de AEM y Adobe Commerce (Magento) con Commerce integration framework {#aem-commerce-framework}

Experience Manager y Adobe Commerce se integran perfectamente con Commerce integration framework (CIF). CIF permite que AEM acceda directamente a la instancia de Commerce y se comunique con ella mediante las [API de GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) de Adobe Commerce.

>[!NOTE]
>
>La versión mínima de la API de GraphQL admitida es 2.3.5. Algunas funciones solo son compatibles con las versiones más recientes o solo con la edición de Adobe Commerce.

## Información general sobre la arquitectura {#overview}

La arquitectura general es la siguiente:

![Información general sobre la arquitectura del CIF](../assets/AEM_Magento_Architecture.png)

Dentro de CIF, hay compatibilidad con patrones de comunicación del lado del servidor y del lado del cliente.
Las llamadas de API del lado del servidor se implementan mediante el [cliente GraphQL](https://github.com/adobe/commerce-cif-graphql-client) genérico integrado en combinación con un [conjunto de modelos de datos generados](https://github.com/adobe/commerce-cif-magento-graphql) para el esquema de Commerce GraphQL. Además, se puede utilizar cualquier consulta o mutación de GraphQL en formato GQL.

Para los componentes del lado del cliente, que se generan mediante [React](https://reactjs.org/), se utiliza el cliente [Apollo](https://www.apollographql.com/docs/react/).

## Arquitectura de componentes principales de AEM CIF {#cif-core-components}

![Arquitectura de los componentes principales del CIF de AEM](../assets/cif-component-architecture.jpg)

[Los componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components) siguen patrones de diseño y prácticas recomendadas muy similares a los de los [componentes principales de AEM WCM](https://github.com/adobe/aem-core-wcm-components).

La lógica empresarial y la comunicación back-end con Adobe Commerce para los componentes principales de AEM CIF se implementan en los modelos Sling. En caso de que sea necesario personalizar esta lógica para cumplir los requisitos específicos del proyecto, se puede utilizar el patrón de delegación para modelos Sling.

>[!TIP]
>
>La página [Personalización de los componentes principales del CIF de AEM](../customizing/customize-cif-components.md) tiene un ejemplo detallado y una práctica recomendada sobre cómo personalizar los componentes principales del CIF.

Dentro de los proyectos, los componentes principales de AEM CIF y los componentes de proyecto personalizados pueden recuperar fácilmente el cliente configurado para una tienda de Adobe Commerce asociado a una página de AEM mediante la configuración según el contexto de Sling.
