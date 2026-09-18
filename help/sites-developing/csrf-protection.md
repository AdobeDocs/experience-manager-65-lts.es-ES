---
title: El marco de protección CSRF
description: El marco de trabajo utiliza tokens para garantizar que la solicitud del cliente sea legítima
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: d6bd4028-56c9-4e09-9bba-1199a41b41b8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%
---
# El marco de protección CSRF{#the-csrf-protection-framework}

Además del Filtro de referente de Apache Sling, Adobe también proporciona un nuevo marco de protección CSRF para protegerse contra este tipo de ataque.

El marco de trabajo utiliza tokens para garantizar que la solicitud del cliente sea legítima. Los tokens se generan cuando el formulario se envía al cliente y se validan cuando se devuelve al servidor.

>[!NOTE]
>
>No hay tokens en las instancias de publicación para usuarios anónimos.

## Requisitos {#requirements}

### Dependencias {#dependencies}

Cualquier componente que dependa de la dependencia `granite.jquery` puede beneficiarse automáticamente del marco de protección de CSRF. Si no es así, para cualquiera de los componentes, debe declarar una dependencia en `granite.csrf.standalone` antes de poder utilizar el marco de trabajo.

### Duplicación de la clave criptográfica {#replicating-crypto-keys}

Para utilizar los tokens, debe replicar el binario HMAC en todas las instancias de la implementación. Consulte [Duplicación de la clave HMAC](/help/sites-administering/encapsulated-token.md#replicating-the-hmac-key) para obtener más información.

>[!NOTE]
>
>Asegúrese de realizar también los cambios de configuración necesarios en Dispatcher para utilizar el marco de protección CSRF:
>
>* [Configuración de Adobe Experience Manager Dispatcher para prevenir ataques de tipo CSRF](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/configuring/configuring-dispatcher-to-prevent-csrf)
>* [Información general de Dispatcher](https://experienceleague.adobe.com/es/docs/experience-manager-dispatcher/using/dispatcher)

>[!NOTE]
>
>Si usa la caché de manifiesto con su aplicación web, asegúrese de agregar &quot;**&amp;ast;**&quot; al manifiesto para asegurarse de que el token no desconecte la llamada de generación de token CSRF. Para obtener más información, consulte este [vínculo](https://www.w3.org/TR/offline-webapps/).
>
>Para obtener más información sobre los ataques de CSRF y las formas de mitigarlos, consulte la [página de OWASP de falsificación de solicitud en sitios múltiples](https://owasp.org/www-community/attacks/csrf).
