---
title: Configurar el proveedor de servicios SAML
description: Puede configurar el proveedor de servicios SAML para permitir que los usuarios inicien sesión y se autentiquen en formularios AEM a través de un proveedor de identidad de terceros (IDP) especificado.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 0f1b39e7-5de5-4b54-b622-61774ce839db
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 1%

---

# Configurar el proveedor de servicios SAML{#configure-saml-service-provider-settings}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El lenguaje de marcado de aserción de seguridad (SAML) es una de las opciones que puede seleccionar al configurar la autorización de un dominio híbrido o empresarial. SAML se utiliza principalmente para admitir SSO en varios dominios. Cuando SAML está configurado como su proveedor de autenticación, los usuarios inician sesión y se autentican en los formularios de AEM a través de un proveedor de identidad de terceros (IDP) especificado.

Para obtener una explicación de SAML, consulte [Descripción técnica del lenguaje de marcado de aserción de seguridad (SAML) V2.0](https://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html).

1. En la consola de administración, haga clic en Configuración > User Management > Configuración > Configuración de Proveedor de servicio de SAML.
1. En el cuadro ID de entidad de Service Provider, escriba un ID único para utilizarlo como identificador para la implementación del proveedor de servicios de AEM Forms. También puede especificar este identificador único al configurar el IDP (por ejemplo, `um.lc.com`). También puede usar la URL que se usa para acceder a los formularios de AEM (por ejemplo, `https://AEMformsserver`).
1. En el cuadro Dirección URL base de Service Provider, escriba la dirección URL base del servidor de Forms (por ejemplo, `https://AEMformsserver:8080`).
1. (Opcional) Para permitir que los formularios de AEM envíen solicitudes de autenticación firmadas al IDP, realice las siguientes tareas:

   * Use el Administrador de confianza para importar una credencial en formato PKCS #12 con la credencial de firma de documento seleccionada como tipo de almacén de confianza. (Consulte [Administrar credenciales locales](/help/forms/using/admin-help/local-credentials.md#managing-local-credentials).)
   * En la lista Alias de clave de credencial de proveedor de servicios, seleccione el alias que asignó a la credencial en el almacén de confianza.
   * Haga clic en Exportar para guardar el contenido de la URL en un archivo y, a continuación, importar ese archivo en el IDP.

1. (Opcional) En la lista Política de ID de nombres de proveedores de servicios, seleccione el formato de nombre que utiliza el IDP para identificar al usuario en una afirmación de SAML. Las opciones son Sin especificar, Correo electrónico y Nombre completo del dominio de Windows.

   >[!NOTE]
   >
   >Los formatos de nombre no distinguen entre mayúsculas y minúsculas.

1. (Opcional) Seleccione Habilitar Mensaje De Autenticación Para Usuarios Locales. Cuando se selecciona esta opción, los usuarios ven dos vínculos:

   * un vínculo a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio de Enterprise pueden autenticarse.
   * un vínculo a la página de inicio de sesión de formularios AEM Forms, donde los usuarios que pertenecen a un dominio local pueden autenticarse.

   Cuando esta opción no está seleccionada, los usuarios se dirigen directamente a la página de inicio de sesión del proveedor de identidad SAML de terceros, donde los usuarios que pertenecen a un dominio de Enterprise pueden autenticarse.

1. (Opcional) Seleccione Habilitar enlace de artefactos para habilitar la compatibilidad con enlaces de artefactos. De forma predeterminada, el enlace POST se utiliza con SAML. Pero si ha configurado el enlace de artefactos, seleccione esta opción. Cuando se selecciona esta opción, la afirmación del usuario real no se pasa a través de la solicitud del explorador. En su lugar, se pasa un puntero a la aserción y esta se recupera mediante una llamada al servicio web back-end.
1. (Opcional) Seleccione Habilitar enlace de redireccionamiento para admitir enlaces SAML que utilicen redirecciones.
1. (Opcional) En Propiedades personalizadas, especifique propiedades adicionales. Las propiedades adicionales son pares nombre=valor separados por nuevas líneas.

   * Puede configurar formularios AEM para que emitan una aserción SAML durante un período de validez que coincida con el período de validez de una aserción de terceros. Para respetar el tiempo de espera de aserción de SAML de terceros, agregue la siguiente línea en Propiedades personalizadas:

     `saml.sp.honour.idp.assertion.expiry=true`

   * Agregue la siguiente propiedad personalizada para utilizar RelayState para determinar la dirección URL a la que se redirigirá al usuario después de la autenticación correcta.

     `saml.sp.use.relaystate=true`

   * Agregue la siguiente propiedad personalizada para poder configurar la dirección URL de las páginas de servidor Java™ (JSP) personalizadas, que se utilizan para procesar la lista registrada de proveedores de identidad. Si no ha implementado una aplicación web personalizada, se utiliza la página predeterminada Administración de usuarios para procesar la lista.

   `saml.sp.discovery.url=/custom/custom.jsp`

1. Haga clic en Guardar.
