---
title: Integración de AEM y Commerce de terceros con Commerce integration framework
description: Los negocios empresariales pueden requerir soluciones de comercio de terceros adicionales para impulsar su tienda. Commerce integration framework (CIF) se puede utilizar en estos casos de integración para conectar una solución de comercio de terceros a Adobe Experience Manager mediante I/O Runtime.
thumbnail: cif-third-party-architecture.jpg
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Integración de AEM y Commerce de terceros con Commerce integration framework {#aem-third-party}

La integración de soluciones diferentes de Adobe Commerce es un escenario común para CIF. Las soluciones de terceros con diferentes API y esquemas se conectan mediante una capa de integración.

## Arquitectura {#architecture}

La arquitectura general es la siguiente:

![Descripción general de la arquitectura de terceros/AEM que no es Magento](../assets//AEM_nonMagento_Architecture.png)

El propósito de esta capa de integración es asignar API y esquemas de terceros a las API y esquemas de Adobe Commerce GraphQL compatibles fuera de Experience Manager. Gracias a esta encapsulación, la lógica y los sistemas de integración pueden actualizarse sin cambiar el código dentro de Experience Manager.

## Requisitos de solución para una integración

A medida que Experience Manager recupera datos bajo demanda, se requieren API en tiempo real para el catálogo de productos.

>[!TIP]
>
>Si no hay API en tiempo real disponibles, se debe utilizar una caché de producto externo con API para la integración. Ejemplo [Magento open-source](https://business.adobe.com/products/magento/open-source.html).

No es necesario implementar el esquema GraphQL completo, solo los objetos del esquema para habilitar los casos de uso deseados.

## Casos de uso back-end

CIF amplía Experience Manager con acceso al catálogo de productos en tiempo real y herramientas de administración de experiencias del producto. Esta integración optimizada permite a los autores acceder a los datos de comercio mediante IU incrustadas siempre que sea necesario sin salir del contexto de contenido.

Se requiere la integración de las API del catálogo de productos para desbloquear estos casos de uso.

## Casos de uso de front-end

[Componentes principales de AEM CIF](https://github.com/adobe/aem-core-cif-components) recuperan e intercambian datos a través de las API de Adobe Commerce compatibles con CIF. Para reutilizar componentes, se deben implementar las API respectivas.

La recomendación para los componentes del lado del cliente esenciales para el rendimiento es comunicarse directamente con la solución de terceros para evitar la latencia.

## Desarrollo de una integración {#develop-integration}

Adobe recomienda usar [Adobe I/O Runtime](https://developer.adobe.com/apis/experienceplatform/runtime.html) para la capa de integración. Se incluye en el complemento de CIF para terceros. Como funciona con un enfoque similar a un microservicio, es adecuado para integrar fácilmente varias soluciones.

La [implementación de referencia](https://github.com/adobe/commerce-cif-graphql-integration-reference) es un excelente punto de partida para compilar la integración en su solución de comercio. Aunque es compatible con GraphQL, también se puede integrar con cualquier otro tipo de API, como REST.

Esta capa de integración no es necesaria si hay una capa de terceros disponible (como Mulesoft) o la integración se crea sobre la solución de terceros.

## Conectores creados previamente {#connectors}

Los conectores son un buen punto de partida para los proyectos. Vienen con una conexión específica de la solución de comercio y una asignación de API predeterminada. Estos conectores los crean terceros y Adobe no los mantiene. Póngase en contacto con el socio correspondiente para obtener información.

* [SAP Commerce](https://github.com/diconium/commerce-cif-graphql-integration-hybris), creado por Diconium
* [Herramientas de comercio](https://github.com/diconium/commerce-cif-graphql-integration-commercetool), creadas por Diconium

>[!TIP]
>
>Aunque los conectores ayudan a los proyectos a acelerar la integración comercial, no son plug-n-play. Las soluciones de comercio empresarial están muy personalizadas y requieren una integración personalizada. Se requiere un buen conocimiento de la plataforma de comercio, los esquemas de Adobe Commerce GraphQL y Adobe I/O Runtime.
