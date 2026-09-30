---
title: Habilitación de CRXDE Lite en AEM
description: Obtenga información sobre cómo habilitar CRXDE Lite en Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 109ab777-c7be-4725-8b91-c4e5d6a735ab
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 6%
---
# Habilitación de CRXDE Lite en AEM{#enabling-crxde-lite-in-aem}

Para garantizar que las instalaciones de AEM sean lo más seguras posible, la lista de comprobación de seguridad recomienda [deshabilitar WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) en entornos de producción.

Sin embargo, CRXDE Lite depende del paquete `org.apache.sling.jcr.davex` para funcionar correctamente, por lo que al deshabilitar WebDAV también se deshabilitará CRXDE Lite.

Cuando esto sucede, al examinar `https://serveraddress:4502/crx/de/index.jsp` se muestra un nodo raíz vacío, y todas las solicitudes HTTP a los recursos de CRXDE Lite producirán un error:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Aunque esta recomendación pretende reducir las superficies de ataque en la medida de lo posible, los administradores del sistema a veces pueden necesitar acceso a CRXDE Lite para examinar el contenido o depurar problemas en instancias de producción.

Puede habilitar CRXDE Lite con [configuración OSGi](#enabling-crxde-lite-osgi) o con un [comando cURL](#enabling-crxde-lite-curl).

>[!WARNING]
>
>Debido a pequeñas diferencias en el funcionamiento de estos métodos, debería usar ***OSGI*** ***o cURL***.
>
>Los dos métodos son ***no*** intercambiables.

## Habilitar CRXDE Lite con OSGI {#enabling-crxde-lite-osgi}

Si está desactivado, puede activar CRXDE Lite siguiendo el siguiente procedimiento:

1. Vaya a la consola Componentes de OSGi en `http://localhost:4502/system/console/components`
1. Busque el siguiente componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Haga clic en el icono de la llave inglesa junto a ella para ver sus opciones de configuración:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Cree la siguiente configuración:

   * **Ruta de acceso raíz:** `/crx/server`
   * Marque la casilla bajo **Usar URI absolutos**.

1. Cuando termine de usar CRXDE Lite, asegúrese de volver a deshabilitar WebDAV.

## Habilitar CRXDE Lite con cURL {#enabling-crxde-lite-curl}

También puede habilitar CRXDE Lite mediante cURL ejecutando (ambos) estos dos comandos:

* Habilitar `create-absolute-uri` :

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&dav.create-absolute-uri=true&propertylist=dav.create-absolute-uri'
  ```

* Definir `alias` :

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&alias=/crx/server&propertylist=alias'
  ```

## Otros recursos {#other-resources}

Para obtener más información sobre las funciones de seguridad de AEM 6, consulte las siguientes páginas:

* [La lista de comprobación de seguridad de AEM](/help/sites-administering/security-checklist.md)
* [Ejecución de AEM en el modo listo para la producción](/help/sites-administering/production-ready.md)
