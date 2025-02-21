---
title: Autenticación para consultas de Adobe Experience Manager GraphQL remotas en fragmentos de contenido
description: Comprenda la autenticación necesaria para las consultas de Adobe Experience Manager GraphQL remotas a fin de proteger la entrega de contenido sin encabezado.
feature: Content Fragments,GraphQL API
solution: Experience Manager, Experience Manager Sites
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 42%

---

# Autenticación para consultas de Adobe Experience Manager GraphQL remotas en fragmentos de contenido {#authentication-for-remote-aem-graphql-queries-on-content-fragments}

Un caso de uso principal para la API de GraphQL de [Adobe Experience Manager (AEM) para la entrega de fragmentos de contenido](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) es aceptar consultas remotas desde aplicaciones o servicios de terceros. Estas consultas remotas pueden requerir acceso a una API autenticada para asegurar la entrega de contenido sin encabezado.

>[!NOTE]
>
>Para pruebas y desarrollo, también puede acceder a la API de GraphQL de AEM directamente mediante la [Interfaz de GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface).

Para la autenticación, el servicio de terceros debe autenticarse con el nombre de usuario y la contraseña de la cuenta de AEM.

<!-- 6.5.10.0 - does this content/page need to be migrated? -->

<!--
For authentication the third-party service needs to [retrieve an Access Token](#retrieving-access-token), that can then be [used in the GraphQL Request](#use-access-token-in-graphql-request).

## Retrieving an Access Token {#retrieving-access-token}

See [Generating Access Tokens for Server Side APIs](/help/sites-developing/generating-access-tokens-for-server-side-apis.md) for full details.

## Using the Access Token in a GraphQL Request {#use-access-token-in-graphql-request}

For a third-party service to connect with an AEM instance it needs to have an *Access Token*. The service must then add this token to the `Authorization` header on the POST request. 

For example, a GraphQL Authorization Header:

```xml
Authorization: Bearer <access_token>
```

## Permission Requirements {#permission-requirements}

All requests made using the access token will actually be made *by the user account that generated the token*. 

This means that you need to check that the account has the permissions required to run GraphQL queries. 

You can check this by using GraphiQL on the local instance.
-->
