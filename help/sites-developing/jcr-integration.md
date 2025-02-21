---
title: Integración de JCR
description: Conozca algunas sugerencias para cuándo necesita integrarse con Adobe Experience Manager en el nivel JCR.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Integración de JCR{#jcr-integration}

## Preferir la API de recursos de Sling a la API de JCR {#prefer-the-sling-resource-api-to-jcr-api}

La API de Sling funciona en un nivel más alto y abstracto que la API de JCR. Esto permite que el código sea más reutilizable e independiente del almacenamiento subyacente. Esto facilita la inclusión de datos virtuales externos mediante el mecanismo ResourceProvider si es necesario.

## Evite consultas siempre que sea posible {#avoid-queries-wherever-possible}

Siempre es más rápido navegar por el repositorio para recuperar datos que ejecutar una consulta. Hay casos en que son necesarias consultas, como una consulta del usuario final o la necesidad de encontrar contenido estructurado de todo el repositorio, pero para todos los demás casos, se prefiere navegar a los nodos necesarios. Las consultas siempre deben evitarse en la lógica de procesamiento, como los componentes de navegación, una &quot;lista de elementos recientes&quot;, recuentos de elementos, etc. En estos casos, es mejor recorrer la jerarquía o prealmacenar en caché el resultado para que se pueda utilizar directamente cuando se represente.

## Restringir el ámbito de la observación JCR {#restrict-the-scope-of-jcr-observation}

Al escuchar eventos en el repositorio, es importante reducir el ámbito lo más posible. Por ejemplo, es mucho mejor escuchar un evento en `/etc/mycompany` que escuchar en `/etc`. Nunca escuchar eventos en la raíz del repositorio. Además, asegúrese de que los métodos de devolución de llamada se ejecutan lo más rápido posible cuando no tienen que hacer nada.

## Eliminar el uso del acceso de administrador de JCR {#eliminate-use-of-jcr-admin-access}

A partir de AEM 6, el inicio de sesión administrativo ha quedado obsoleto, al igual que la obtención de una sesión administrativa de ResourceResolverFactory. En su lugar, las cuentas de servicio deben crearse para las operaciones de back office que requerirían este tipo de acceso y ResourceResolverFactory puede utilizarse para obtener un ResourceResolver para esta cuenta.
