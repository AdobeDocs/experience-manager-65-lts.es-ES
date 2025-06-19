---
title: Autenticación IMS de Adobe y  [!DNL Admin Console] compatibilidad con Adobe Experience Manager Managed Services
description: Aprenda a utilizar  [!DNL Admin Console]  en Adobe Experience Manager.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 63f42a35-fbd5-4b1b-bba1-1bdcfd23dd33
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 6%

---

# Autenticación IMS de Adobe y compatibilidad con [!DNL Admin Console] para AEM Managed Services {#adobe-ims-authentication-and-admin-console-support-for-aem-managed-services}

>[!NOTE]
>
>Esta función solo está disponible para los clientes de Adobe Managed Services.

## Introducción {#introduction}

AEM 6.4.3.0 incluye compatibilidad con [!DNL Admin Console] para instancias de AEM y autenticación basada en Adobe IMS (Identity Management System) para clientes de **AEM Managed Services**.

La incorporación de AEM a [!DNL Admin Console] permitirá a los clientes de AEM Managed Services administrar todos los usuarios de Experience Cloud en una consola. Los usuarios pueden asignarse a perfiles de producto asociados a instancias de AEM, lo que les permite iniciar sesión en una específica.

## Puntos clave destacados {#key-highlights}

* La compatibilidad con la autenticación IMS de AEM solo está disponible para autores, administradores o desarrolladores de AEM, no para usuarios finales externos de sitios de clientes como visitantes del sitio
* [!DNL Admin Console] representará a los clientes de AEM Managed Services como organizaciones de IMS y sus instancias como contextos de producto. Los administradores de sistemas de clientes y productos podrán administrar el acceso a las instancias
* AEM Managed Services sincronizará las topologías de clientes con [!DNL Admin Console]. Habrá una instancia de contexto de producto de AEM Managed Services por instancia en [!DNL Admin Console].
* Los perfiles de producto de [!DNL Admin Console] determinarán las instancias a las que puede tener acceso un usuario
* Se admite la autenticación federada mediante los propios proveedores de identidad compatibles con SAML 2 de los clientes
* Solo se admiten los Enterprise ID o Federated ID (para el inicio de sesión único del cliente), no los Adobe ID personales.
* [!DNL User Management] (en Adobe [!DNL Admin Console]) seguirá siendo propiedad de los administradores del cliente.

## Arquitectura {#architecture}

La autenticación IMS funciona mediante el protocolo OAuth entre AEM y el punto final IMS de Adobe. Una vez que se añade un usuario a IMS y tiene una identidad de Adobe, puede iniciar sesión en las instancias de AEM Managed Services con las credenciales de IMS.

El flujo de inicio de sesión del usuario se muestra a continuación; se redirige al usuario a IMS y, opcionalmente, al IDP de cliente para la validación de SSO y, a continuación, a AEM.

![image2018-9-23_23-55-8](assets/image2018-9-23_23-55-8.png)

## Cómo Se Configura {#how-to-set-up}

### Incorporando organizaciones a [!DNL Admin Console] {#onboarding-organizations-to-admin-console}

La incorporación del cliente a [!DNL Admin Console] es un requisito previo para utilizar Adobe IMS para la autenticación de AEM.

Como primer paso, los clientes deben disponer de una organización en Adobe IMS. Los clientes de Adobe Enterprise están representados como organizaciones de IMS en [Adobe [!DNL Admin Console]](https://helpx.adobe.com/es/enterprise/using/admin-console.html).

Los clientes de AEM Managed Services ya deben tener una organización aprovisionada y, como parte del aprovisionamiento de IMS, las instancias de cliente estarán disponibles en [!DNL Admin Console] para administrar los derechos de usuario y el acceso.

El paso a IMS para la autenticación de usuarios será un esfuerzo conjunto entre AMS y los clientes, cada uno de los cuales tendrá que completar sus flujos de trabajo.

Una vez que un cliente existe como organización de IMS y AMS se completa con el aprovisionamiento del cliente para IMS, este es el resumen de los flujos de trabajo de configuración necesarios:

![image2018-9-23_23-33-25](assets/image2018-9-23_23-33-25.png)

1. El administrador del sistema designado recibe una invitación para iniciar sesión en [!DNL Admin Console]
1. El administrador del sistema reclama el dominio para confirmar la propiedad del dominio (en este ejemplo, acme.com)
1. El administrador del sistema configura los directorios de usuario
1. El administrador del sistema configura el proveedor de identidad (IDP) en la configuración de [!DNL Admin Console] para SSO.
1. El administrador de AEM administra los grupos locales, los permisos y los privilegios de la forma habitual. Consulte Sincronización de usuarios y grupos

>[!NOTE]
>
>Para obtener más información sobre los conceptos básicos de Adobe Identity Management, incluida la configuración de IDP, consulte el artículo sobre [Configurar la identidad y el inicio de sesión único](https://helpx.adobe.com/es/enterprise/using/set-up-identity.html).
>
>Para obtener más información acerca de la administración de la empresa y [!DNL Admin Console], consulte la [Guía de administración de equipos y empresas](https://helpx.adobe.com/es/enterprise/managing/user-guide.html).

### Incorporando usuarios a [!DNL Admin Console] {#onboarding-users-to-the-admin-console}

Existen tres formas de incorporar usuarios en función del tamaño del cliente y de sus preferencias:

1. Crear usuarios y grupos manualmente en [!DNL Admin Console]
1. Cargar un archivo CSV con usuarios
1. Sincronizar usuarios y grupos desde el Active Directory empresarial del cliente.

#### Adición manual mediante la interfaz de usuario [!DNL Admin Console] {#manual-addition-through-admin-console-ui}

Los usuarios y grupos se pueden crear manualmente en la interfaz de usuario de [!DNL Admin Console]. Este método se puede utilizar si no tienen muchos usuarios que administrar. Por ejemplo, menos de 50 usuarios de AEM.

Los usuarios también se pueden crear manualmente si el cliente ya está utilizando este método para administrar otros productos de Adobe como Adobe Analytics, Adobe Target o aplicaciones de Adobe Creative Cloud.

![image2018-9-23_20-39-9](assets/image2018-9-23_20-39-9.png)

#### Carga de archivos en la interfaz de usuario de [!DNL Admin Console] {#file-upload-in-the-admin-console-ui}

Para facilitar la gestión de la creación de usuarios, se puede cargar un archivo CSV para añadir usuarios de forma masiva:

![image2018-9-23_18-59-57](assets/image2018-9-23_18-59-57.png)

#### Herramienta de sincronización de usuarios {#user-sync-tool}

La herramienta de sincronización de usuarios (o UST abreviada) permite a los clientes empresariales crear o administrar usuarios de Adobe que utilizan Active Directory u otros servicios de directorio OpenLDAP probados. Los usuarios de destino son administradores de identidad de TI (Enterprise Directory y administradores del sistema) que pueden instalar y configurar la herramienta. La herramienta de código abierto es personalizable para que los clientes puedan hacer que un desarrollador la modifique para adaptarla a sus propios requisitos particulares.

Cuando se ejecuta la sincronización de usuarios, se obtiene una lista de usuarios de Active Directory de la organización (o de cualquier otro origen de datos compatible) y se compara con la lista de usuarios dentro de [!DNL Admin Console]. A continuación, llama a la API de Adobe [!DNL User Management] para sincronizar [!DNL Admin Console] con el directorio de la organización. El flujo de cambios es totalmente unidireccional; las ediciones realizadas en [!DNL Admin Console] no se insertan en el directorio.

La herramienta permite al administrador del sistema asignar grupos de usuarios en el directorio del cliente con la configuración del producto y los grupos de usuarios en [!DNL Admin Console]. La nueva versión de UST también permite la creación dinámica de grupos de usuarios en [!DNL Admin Console].

Para configurar la sincronización de usuarios, la organización debe crear un conjunto de credenciales de la misma manera que usaría la [[!DNL User Management] API](https://adobe-apiplatform.github.io/user-sync.py/en/success-guide/identify_server.html).

![image2018-9-23_13-36-56](assets/image2018-9-23_13-36-56.png)

La sincronización de usuarios se distribuye a través del repositorio de Adobe Github en esta ubicación:

[https://github.com/adobe-apiplatform/user-sync.py/releases/latest](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)

Tenga en cuenta que hay disponible una versión preliminar 2.4RC1 con compatibilidad para la creación de grupos dinámicos y que se puede encontrar aquí: [https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)

Las características principales de esta versión son la capacidad de asignar dinámicamente nuevos grupos LDAP para la pertenencia de usuarios en [!DNL Admin Console] y la creación dinámica de grupos de usuarios.

Puede encontrar más información sobre las nuevas funciones de grupo aquí:

[https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options](https://adobe-apiplatform.github.io/user-sync.py/es/user-manual/advanced_configuration.html#additional-group-options)

>[!NOTE]
>
>Para obtener más información, consulte:
>
>* la [Herramienta de sincronización de usuarios - Sincronización de usuarios de Adobe](https://adobe-apiplatform.github.io/user-sync.py/es/)
>
>* la herramienta de sincronización de usuarios debe registrarse como cliente de Adobe I/O UMAPI mediante el procedimiento descrito en [Autenticación para acceso a API](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)
>
>* la [documentación de Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/).
>
>* la [Documentación de la API de administración de usuarios](https://adobe-apiplatform.github.io/umapi-documentation/en/).
>

>[!NOTE]
>
>El equipo de Adobe Managed Services se encargará de la configuración de AEM IMS. Sin embargo, el administrador del cliente puede modificarla según sus necesidades (por ejemplo, Pertenencia a un grupo automático o Asignación de grupos). El cliente IMS también será registrado por su equipo de Managed Services.

## Usos {#how-to-use}

### Administrar productos y acceso de usuarios en [!DNL Admin Console] {#managing-products-and-user-access-in-admin-console}

Cuando el administrador de productos del cliente inicia sesión en [!DNL Admin Console], ve varias instancias del contexto de producto de AEM Managed Services, como se muestra a continuación:

![screen_shot_2018-09-17at105804pm](assets/screen_shot_2018-09-17at105804pm.png)

En este ejemplo, la organización *AEM-MS-Onboard* tiene 32 instancias que abarcan diferentes topologías y entornos como Stage, Prod, etc.

![screen_shot_2018-09-17at105517pm](assets/screen_shot_2018-09-17at105517pm.png)

Los detalles de la instancia se pueden comprobar para identificar la instancia:

![screen_shot_2018-09-17at105601pm](assets/screen_shot_2018-09-17at105601pm.png)

En cada instancia de contexto de producto, habrá un perfil de producto asociado. Este perfil de producto se utiliza para asignar acceso a los usuarios.

![image2018-9-18_7-48-50](assets/image2018-9-18_7-48-50.png)

Todos los usuarios añadidos bajo este perfil de producto podrán iniciar sesión en esa instancia, como se muestra en el ejemplo siguiente:

![screen_shot_2018-09-17at105623pm](assets/screen_shot_2018-09-17at105623pm.png)

### Inicio de sesión en AEM {#logging-into-aem}

#### Inicio de sesión de administrador local {#local-admin-login}

AEM puede seguir admitiendo inicios de sesión locales para usuarios administradores, ya que la pantalla de inicio de sesión tiene una opción para iniciar sesión localmente:

![screen_shot_2018-09-18at121056am](assets/screen_shot_2018-09-18at121056am.png)

#### Inicio de sesión basado en IMS {#ims-based-login}

Para otros usuarios, el inicio de sesión basado en IMS se puede utilizar una vez que IMS esté configurado en la instancia. El usuario primero hace clic en **Iniciar sesión con Adobe**, como se muestra a continuación:

![image2018-9-18_0-10-32](assets/image2018-9-18_0-10-32.png)

A continuación, se les redirige a la pantalla de inicio de sesión de IMS e introducen sus credenciales:

![screen_shot_2018-09-17at115629pm](assets/screen_shot_2018-09-17at115629pm.png)

Si se configura un IDP federado durante la configuración inicial de [!DNL Admin Console], se redirigirá al usuario al IDP del cliente para SSO.

El IDP es Okta en el siguiente ejemplo:

![screen_shot_2018-09-17at115734pm](assets/screen_shot_2018-09-17at115734pm.png)

Una vez finalizada la autenticación, se redirige al usuario a AEM para iniciar sesión:

![screen_shot_2018-09-18at120124am](assets/screen_shot_2018-09-18at120124am.png)

### Migración de usuarios existentes {#migrating-existing-users}

Para las instancias de AEM existentes que utilizan otro método de autenticación y que ahora se migran a IMS, debe haber un paso de migración.

Los usuarios existentes en el repositorio de AEM (procedentes de forma local, a través de LDAP o SAML) se pueden migrar para que apunten a IMS como IDP mediante la utilidad de migración de usuarios.

El equipo de AMS ejecutará esta utilidad como parte del aprovisionamiento de IMS.

### Administración de permisos y ACL en AEM {#managing-permissions-and-acls-in-aem}

El control de acceso y los permisos se seguirán administrando en AEM; esto se puede lograr separando los grupos de usuarios procedentes de IMS (por ejemplo, AEM-GRP-008 en el ejemplo siguiente) y los grupos locales donde se definen los permisos y el control de acceso. Los grupos de usuarios sincronizados desde IMS se pueden asignar a grupos locales y heredar los permisos.

En el ejemplo siguiente, se añaden grupos sincronizados al grupo local *Dam_Users* como ejemplo.

En este caso, también se ha asignado un usuario a algunos grupos de [!DNL Admin Console]. (Los usuarios y grupos se pueden sincronizar desde LDAP mediante la herramienta de sincronización de usuarios o crearse localmente. Ver **Incorporación de usuarios a[!DNL Admin Console]** anteriormente).

>[!NOTE]
>
>Los grupos de usuarios solo se sincronizan cuando los usuarios inician sesión en la instancia.

![screen_shot_2018-09-17at94207pm](assets/screen_shot_2018-09-17at94207pm.png)

El usuario forma parte de los siguientes grupos en IMS:

![screen_shot_2018-09-17at94237pm](assets/screen_shot_2018-09-17at94237pm.png)

Cuando el usuario inicia sesión, se sincronizan las suscripciones al grupo, como se muestra a continuación:

![screen_shot_2018-09-17at94033pm](assets/screen_shot_2018-09-17at94033pm.png)

En AEM, los grupos de usuarios sincronizados con IMS se pueden agregar como miembros a grupos locales existentes, por ejemplo, usuarios de DAM.

![screen_shot_2018-09-17at95804pm](assets/screen_shot_2018-09-17at95804pm.png)

Como se muestra a continuación, el grupo *AEM-GRP_008* hereda los permisos y privilegios de los usuarios de DAM. Se trata de una forma eficaz de administrar permisos para grupos sincronizados y se utiliza comúnmente también en métodos de autenticación basados en LDAP.

![screen_shot_2018-09-17at110505pm](assets/screen_shot_2018-09-17at110505pm.png)
