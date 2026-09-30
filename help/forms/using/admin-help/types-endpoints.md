---
title: Tipos de extremos
description: Obtenga información acerca de los distintos tipos de extremos. Se pueden agregar diferentes tipos de extremos a los servicios, como correo electrónico, carpeta inspeccionada y muchos más.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 5ac3350d-8819-4b33-b1a1-9e686b6abd9e
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 1%
---
# Tipos de extremos {#types-of-endpoints}

Para poder utilizar un servicio, debe configurar y habilitar un extremo. Un extremo especifica cómo se va a invocar un servicio.

>[!NOTE]
>
>En Workbench, los puntos finales se denominan puntos iniciales.

Se pueden agregar los siguientes tipos de extremos a los servicios. No todos los servicios admiten todos los extremos:

**Correo electrónico:** Permite que un usuario invoque un servicio enviando un mensaje de correo electrónico con uno o más archivos adjuntos a una cuenta de correo electrónico especificada. Antes de configurar un extremo de correo electrónico, debe configurar las cuentas de correo electrónico necesarias. (Consulte Configuración de puntos finales de correo electrónico).

**Carpeta inspeccionada:** Permite que un usuario invoque un servicio colocando un archivo en una carpeta, que se analiza a un intervalo definido. (Consulte Configuración de puntos finales de carpetas vigiladas).

**TaskManager:** Permite que un usuario de Workspace invoque el servicio.

**Remoting:** habilita una aplicación creada con Flex para invocar el servicio mediante (obsoleto para formularios AEM) AEM Forms Remoting. Se crea automáticamente un extremo remoto para cada servicio activado. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

**SOAP:** habilita una aplicación cliente desarrollada mediante las API de programación de formularios de AEM para invocar el servicio mediante el modo SOAP. Se crea automáticamente un punto final de SOAP para cada servicio activado.

**nota**: *Se puede quitar la seguridad de los documentos de seguridad cuando se utiliza el extremo de SOAP mientras se visualizan los documentos en Adobe Acrobat o Adobe Reader. Para obtener más información sobre cómo deshabilitar los extremos de SOAP en sus documentos de CRM, consulte [Deshabilitar los extremos de SOAP para documentos de seguridad de documentos](/help/forms/using/admin-help/configuring-client-server-options.md#disable-soap-endpoints-for-document-security-documents)*

**EJB:** Habilita una aplicación cliente desarrollada mediante las API de programación de formularios AEM Forms para invocar el servicio mediante el modo Enterprise JavaBeans (EJB). Se crea automáticamente un extremo de EJB para cada servicio activado.

**WSDL:** habilita una aplicación cliente desarrollada mediante las API de programación de formularios de AEM para invocar el servicio mediante el Lenguaje de definición de servicios web (WSDL). La página Configuraciones principales contiene una opción para habilitar la generación de WSDL para todos los servicios que forman parte de los formularios de AEM. (Consulte Configuración general de formularios AEM Forms ).

**REST:** Los procesos creados en Workbench se pueden configurar para que pueda invocarlos mediante solicitudes de transferencia de estado representacional (REST). Las solicitudes REST se envían desde páginas de HTML. Es decir, puede invocar un proceso de formularios AEM Forms directamente desde una página web mediante una solicitud REST.

Los extremos Correo electrónico, TaskManager, Carpeta inspeccionada y Remoting exponen únicamente una operación específica del servicio. Para agregar estos extremos, es necesario realizar un segundo paso de configuración para seleccionar un método para invocar el servicio, establecer parámetros de configuración y especificar asignaciones de parámetros de entrada y salida.
