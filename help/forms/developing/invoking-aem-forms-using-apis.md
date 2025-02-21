---
title: ¿Cómo invocar AEM Forms mediante API?
description: Aprenda a invocar servicios de AEM Forms mediante Java& trade; API, servicios web, Remoting y REST.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# Invocar AEM Forms mediante API {#invoking-aem-forms-using-apis}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Adobe Experience Manager Forms es un software empresarial basado en J2EE que consta de servicios que funcionan dentro de una infraestructura compartida. Las operaciones de servicio suelen consumir o producir documentos. Con AEM Forms, puede combinar Forms Workflow con formularios electrónicos, seguridad de los documentos y generación de documentos en un conjunto de servicios integrado y coherente. Se puede acceder a estos servicios desde dentro y fuera del cortafuegos.

Las aplicaciones cliente pueden invocar mediante programación los servicios de AEM Forms mediante una API de Java™, servicios web, Remoting y REST. Mediante la consola de administración, puede configurar un servicio para que exponga un extremo que permita a los servicios de AEM Forms invocar mediante programación. De forma predeterminada, la mayoría de los servicios están preconfigurados para exponer los extremos de Remoting™ Java y los servicios web.

Los requisitos empresariales determinan qué método de invocación utilizar. Por ejemplo, con la API de Java™, puede integrar la funcionalidad de AEM Forms en sus aplicaciones empresariales de Java™, como Java™ Entity y Message Beans. Del mismo modo, puede integrar la funcionalidad de AEM Forms en proyectos de .NET (u otros proyectos desarrollados con entornos de desarrollo compatibles con los estándares de servicios web) mediante servicios web.

Los servicios requieren un contenedor de servicio para ejecutarse, de forma similar a como Enterprise JavaBeans™ (EJB) requiere un contenedor J2EE. AEM Forms incluye solo una implementación de un contenedor de servicios. El contenedor de servicios es responsable de administrar la duración de un servicio, incluida su implementación, y de garantizar que todas las solicitudes se envíen al servicio correcto. También administra los documentos que consume o produce un servicio.

>[!NOTE]
>
>La programación con formularios AEM Forms no incluye información sobre cómo invocar AEM Forms mediante carpetas inspeccionadas o correo electrónico.
