---
title: Configurar la administración segura para AEM Forms en JEE
description: Aprenda a administrar cuentas de usuario y servicios que, aunque sean necesarios en un entorno de desarrollo privado, no sean necesarios en un entorno de producción de AEM Forms en JEE.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
hide: true
hidefromtoc: true
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
exl-id: 2278a4df-2584-4a15-9aaf-bbfc0487b72a
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 98%

---

# Configurar la administración segura para AEM Forms en JEE {#configuring-secure-administration-settings-for-aem-forms-on-jee}

Aprenda a administrar cuentas de usuario y servicios que, aunque sean necesarios en un entorno de desarrollo privado, no sean necesarios en un entorno de producción de AEM Forms en JEE.

Por lo general, los desarrolladores no utilizan el entorno de producción para crear y probar sus aplicaciones. Por lo tanto, debe administrar las cuentas de usuario y los servicios que, aunque sean necesarios en un entorno de desarrollo privado, no sean necesarios en un entorno de producción.

Este artículo describe métodos para reducir la superficie de ataque global mediante las opciones de administración que proporciona AEM Forms en JEE.

## Deshabilitar el acceso remoto no esencial a los servicios {#disabling-non-essential-remote-access-to-services}

Después de instalar y configurar AEM Forms en JEE, hay muchos servicios disponibles para la invocación remota a través de SOAP y Enterprise JavaBeans™ (EJB). El término remoto, en este caso, hace referencia a cualquier llamante que tenga acceso de red a los puertos SOAP, EJB o Action Message Format (AMF) para el servidor de aplicaciones.

Aunque AEM Forms en los servicios JEE requiere que se pasen credenciales válidas para un llamador autorizado, solo debe permitir el acceso remoto a los servicios a los que necesita tenerlo. Para lograr una accesibilidad limitada, debe reducir el conjunto de servicios de acceso remoto al mínimo posible para un sistema en funcionamiento y, a continuación, habilitar la invocación remota para los servicios adicionales que necesite.

AEM Forms en servicios JEE siempre necesita al menos acceso SOAP. Estos servicios suelen ser necesarios para usarlos en Workbench, pero también incluyen servicios a los que llama la aplicación web del espacio de trabajo.

Complete este procedimiento mediante la página web Aplicaciones y servicios de la consola de administración:

1. Inicie sesión en la consola de administración al escribir la siguiente URL en un explorador web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Haga clic en **Servicios > Aplicaciones y servicios > Preferencias**.
1. Establezca Preferencias para ver hasta 200 servicios y extremos en la misma página.
1. Haga clic en **Servicios** > **Aplicaciones y servicios** > **Administrar extremos**.
1. Seleccione **EJB** de la lista **Proveedor** y haga clic en **Filtro**.
1. Para deshabilitar todos los extremos de EJB, active la casilla situada junto a cada uno de la lista y haga clic en **Deshabilitar**.
1. Haga clic en **Siguiente** y repita el paso anterior para todos los extremos de EJB. Asegúrese de que EJB aparece en la columna Proveedor antes de deshabilitar los extremos.
1. Seleccione **SOAP** de la lista **Proveedor** y haga clic en **Filtro**.
1. Para quitar los extremos SOAP, active la casilla de verificación situada junto a cada uno de la lista y haga clic en **Quitar**. No quite los siguientes extremos:

   * AuthenticationManagerService
   * DirectoryManagerService
   * JobManager
   * event_management_service
   * event_configuration_service
   * ProcessManager
   * TemplateManager
   * RepositoryService
   * TaskManagerService
   * TaskQueueManager
   * TaskManagerQueryService
   * WorkspaceSingleSignOn
   * ApplicationManager

1. Haga clic en **Siguiente** y repita el paso anterior para los extremos SOAP que no estén en la lista anterior. Asegúrese de que SOAP aparece en la columna Proveedor antes de quitar los extremos.

## Deshabilitar el acceso anónimo no esencial a los servicios {#disabling-non-essential-anonymous-access-to-services}

Algunos servicios de Forms Server permiten invocaciones no autenticadas (anónimas) para algunas operaciones. Esto significa que una o más operaciones expuestas por el servicio pueden invocarse como cualquier usuario autenticado o como ninguno.

1. Inicie sesión en la consola de administración al escribir la siguiente URL en un explorador web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Haga clic en **Servicios > Aplicaciones y Servicios > Administrar servicios**.
1. Haga clic en el nombre del servicio que desea deshabilitar (por ejemplo, AuthenticationManagerService).
1. Haga clic en la pestaña **Seguridad**, deseleccione **Acceso anónimo permitido** y haga clic en **Guardar**.
1. Complete los pasos 3 y 4 para los siguientes servicios:

   * AuthenticationManagerService
   * EJB
   * Correo electrónico
   * JobManager
   * WatchedFolder
   * UsermanagerUtilService
   * Remoting
   * RepositoryProviderService
   * EMCDocumentumRepositoryProvider
   * IBMFilenetRepositoryProvider
   * FormAugmenter
   * TaskManagerService
   * TaskManagerConnector
   * TaskManagerQueryService
   * TaskQueueManager
   * TaskEndpointManager
   * UserService
   * WorkspaceSearchTemplateService
   * WorkspacePropertyService
   * OutputService
   * FormsService

   Si tiene intención de exponer cualquiera de estos servicios para invocarlos de manera remota, también debe considerar la posibilidad de deshabilitar el acceso anónimo para estos servicios. De lo contrario, cualquier llamante con acceso de red a este servicio podrá invocarlo sin pasar las credenciales.

   El acceso anónimo debe deshabilitarse para cualquier servicio que no sea necesario. Muchos servicios internos requieren que se habilite la autenticación anónima porque cualquier usuario del sistema debe invocarlos sin necesidad de una autorización previa.

## Modificar el tiempo de espera global predeterminado {#changing-the-default-global-time-out}

Los usuarios finales pueden autenticarse en AEM Forms a través de Workbench, aplicaciones web de AEM Forms o aplicaciones personalizadas que invoquen servicios de servidor de AEM Forms. Se utiliza una configuración global de tiempo de espera para especificar cuánto tiempo pueden interactuar estos usuarios con AEM Forms (mediante una aserción basada en SAML) antes de que se vean obligados a volver a autenticarse. El valor predeterminado es de dos horas. En un entorno de producción, la cantidad de tiempo debe reducirse al número mínimo de minutos aceptable.

### Minimizar el límite de tiempo para volverse a autenticar {#minimize-reauthentication-time-limit}

1. Inicie sesión en la consola de administración al escribir la siguiente URL en un explorador web:

   ```java
            https://[host name]:'port'/adminui
   ```

1. Haga clic en **Configuración > Administrar usuarios > Configuración > Importar y exportar archivos de configuración**.
1. Haga clic en **Exportar** para producir un archivo config.xml con la configuración existente de AEM Forms.
1. Abra el archivo XML en un editor y busque la siguiente entrada:

   `<entry key="assertionValidityInMinutes" value="120"/>`

1. Cambie el valor a cualquier número mayor de 5 (en minutos) y guarde el archivo.
1. En la consola de administración, navegue hasta la página Importar y exportar archivos de configuración.
1. Introduzca la ruta al archivo config.xml modificado o haga clic en Examinar para navegar hasta él.
1. Haga clic en **Importar** para cargar el archivo config.xml modificado y, a continuación, haga clic en **Aceptar**.
