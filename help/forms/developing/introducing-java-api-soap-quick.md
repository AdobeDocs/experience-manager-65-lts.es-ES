---
title: Introducción a Java&trade; API QuickStart
description: Descubra cómo se pueden realizar las operaciones de AEM Forms mediante la API de AEM Forms Java&trade; con establecimiento inflexible de tipos y habilitada con la conexión de SOAP.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Inicio rápido de la API de Java™ {#introducing-java-api-quickstart}

**Las muestras y los ejemplos de este documento solo son para AEM Forms en un entorno JEE.**

Inicio rápido de la API de Adobe AEM Forms puede ayudarle a acelerar sus esfuerzos para desarrollar programas que interactúen con los servicios de AEM Forms. *Inicio rápido* s son programas completos que puedes copiar y pegar en tus propios proyectos y usar como punto de partida. Puede ejecutar un Inicio rápido para ver cómo se comporta y modificarlo para sus propias necesidades.

Las operaciones de AEM Forms se pueden realizar mediante la API de AEM Forms con establecimiento inflexible de tipos y el modo de conexión debe establecerse en SOAP.

Inicio rápido de la API de Java™ con establecimiento inflexible de tipos proporciona una lista de los archivos JAR necesarios para ejecutar la aplicación Java™. La mayoría de los inicios rápidos de Java™ son aplicaciones de consola que se ejecutan dentro de `main`. Sin embargo, el Inicio rápido de la API de Forms Java™ con establecimiento inflexible de tipos se implementa como un servlet Java™ que se ejecuta dentro de una aplicación web.

La lista de archivos JAR se encuentra en una sección de comentarios al principio del Inicio rápido. Por ejemplo, el siguiente comentario se encuentra en un inicio rápido de salida y es una lista de archivos JAR típica que se encuentra en cada Inicio rápido de Java™.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## Inicio rápido de varios servicios {#multiple-services-quick-start}

Los inicios más rápidos en *Programación con AEM Forms en JEE* invocan un servicio específico para realizar una operación. Sin embargo, algunos inicios rápidos invocan varios servicios de AEM Forms para realizar un flujo de trabajo determinado. La siguiente lista proporciona inicios rápidos de Java™ que invocan más de un servicio de AEM Forms:

[Inicio rápido (modo SOAP): al pasar un documento del repositorio de AEM Forms al servicio Output mediante la API de Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (invoca el repositorio y el servicio Output)

[Inicio rápido (modo SOAP): al crear un documento de PDF basado en fragmentos mediante la API de Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api) (se invoca el servicio Assembler y Output)

[Inicio rápido (modo SOAP): al crear documentos de PDF con datos XML enviados mediante la API de Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api) (se invoca el servicio Forms, Output y Document Management)

[Inicio rápido (modo SOAP): pasar documentos al servicio Forms mediante la API de Java™](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api) (invoca el servicio Forms y Document Management)

[Inicio rápido (modo SOAP): firmar digitalmente un formulario basado en XFA mediante la API de Java™](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api) (invoca Forms y el servicio Signature)

[Inicio rápido (modo SOAP): administrar roles y permisos mediante la API de Java™](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api) (invoca el servicio DirectoryManager y AuthorizationManager )

[Inicio rápido (modo SOAP): pasando documentos al servicio Output mediante la API de Java™](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api) (invocar el servicio Output and Document Management)

>[!NOTE]
>
>Los inicios rápidos en programación con AEM Forms se basan en AEM Forms implementado en el servidor de aplicaciones JBoss® y en el sistema operativo Microsoft® Windows®. Sin embargo, si está utilizando otro sistema operativo, como UNIX®, reemplace las rutas específicas de Windows por rutas admitidas por el sistema operativo correspondiente. Del mismo modo, si está utilizando otro servidor de aplicaciones J2EE, asegúrese de especificar propiedades de conexión válidas. (Consulte [Establecimiento de propiedades de conexión](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>La mayoría de los inicios rápidos de servicios web se escriben en C# y utilizan .NET Framework. Sin embargo, puede crear una lógica de aplicación cliente que pueda invocar los servicios de AEM Forms en cualquier entorno de desarrollo compatible con los estándares de SOAP. (Consulte [Invocación de AEM Forms mediante servicios web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
