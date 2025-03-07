---
title: Información general sobre la configuración de SSL
description: Obtenga información sobre cómo mejorar la seguridad de la comunicación configurando SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2e81b9b9-321d-4423-9748-6385956b1d90
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 3%

---

# Información general sobre la configuración de SSL {#overview-of-configuring-ssl}

Puede crear credenciales de Secure Sockets Layer (SSL) y configurar SSL en el servidor de aplicaciones para mejorar la seguridad de la comunicación con el servidor de aplicaciones.

Como producto de seguridad, Rights Management requiere la configuración de SSL. Al configurar los certificados SSL, asegúrese de utilizar solo claves RSA. No se admiten certificados SSL con claves DSA.

La información proporcionada se aplica a instalaciones llave en mano, automáticas y manuales. Ofrece un ejemplo de método para configurar SSL. También puede utilizar otros métodos que sean más adecuados para su red u organización.

>[!NOTE]
>
>Se recomienda completar la instalación, configuración e implementación de los módulos de formularios AEM Forms y asegurarse de que los productos se ejecutan correctamente antes de configurar SSL en el servidor de aplicaciones.

>[!NOTE]
>
>Al crear certificados y credenciales de seguridad SSL, utilice los mismos privilegios de cuenta de usuario que utilizó para ejecutar el servidor de aplicaciones. Si el servidor de aplicaciones se ejecuta con otros privilegios de usuario, es posible que el formulario no se represente correctamente para representaciones de PDFForm cuando ContentRootURI señala a https.

Si tiene un servidor LDAP habilitado para SSL, configure Administración de usuarios para que funcione con él. (Consulte [Configurar la administración de usuarios para un servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)).
