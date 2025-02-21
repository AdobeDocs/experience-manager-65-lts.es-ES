---
title: Ejecución de AEM en el modo Producción lista
description: Obtenga información sobre cómo ejecutar AEM en el modo Producción lista.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 3%

---

# Ejecución de AEM en el modo Producción lista{#running-aem-in-production-ready-mode}

Con AEM 6.1, Adobe introduce el nuevo modo de ejecución de `"nosamplecontent"`, que tiene como objetivo automatizar los pasos necesarios para preparar una instancia de AEM para su implementación en un entorno de producción.

El nuevo modo de ejecución no solo configurará automáticamente la instancia para que se adhiera a las prácticas recomendadas de seguridad descritas en la lista de comprobación de seguridad, sino que también eliminará todas las aplicaciones y configuraciones de Geometrixx de ejemplo en el proceso.

>[!NOTE]
>
>Dado que, por motivos prácticos, el modo Producción lista de AEM solo cubrirá la mayoría de las tareas necesarias para proteger una instancia, es muy recomendable que consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) antes de lanzarse a su entorno de producción.
>
>Tenga en cuenta también que ejecutar AEM en el modo Producción lista deshabilitará de forma eficaz el acceso a CRXDE Lite. Si lo necesita con fines de depuración, consulte [Habilitar CRXDE Lite en AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para ejecutar AEM en modo listo para la producción, lo único que debe hacer es agregar `nosamplecontent` mediante el modificador de modo de ejecución `-r` a los argumentos de inicio existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por ejemplo, puede utilizar la producción lista para iniciar una instancia de autor con persistencia MongoDB de esta manera:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Cambia parte del modo Producción lista {#changes-part-of-the-production-ready-mode}

Más específicamente, se realizan los siguientes cambios de configuración cuando AEM se ejecuta en modo listo para la producción:

1. El **paquete de soporte CRXDE** (`com.adobe.granite.crxde-support`) está deshabilitado de manera predeterminada en el modo listo para la producción. Se puede instalar en cualquier momento desde el repositorio Maven público de Adobe. Se requiere la versión 3.0.0 para AEM 6.1.

1. El paquete **Acceso simple de Apache Sling WebDAV a repositorios** ( `org.apache.sling.jcr.webdav`) solo estará disponible en **instancias de autor**.

1. Los usuarios recién creados deben cambiar la contraseña la primera vez que inicien sesión. Esto no se aplica al usuario administrador.
1. **Se ha deshabilitado la generación de información de depuración** para el **controlador de JavaScript Apache Sling**.

1. **El contenido asignado** y **Generar información de depuración** están deshabilitados para **Apache Sling JSP Script Handler**.

1. El filtro **Day CQ WCM Filter** se ha establecido en `edit` en **author** y `disabled` en **publish** instancias.

1. El **Administrador de bibliotecas Adobe Granite HTML** está configurado con la siguiente configuración:

   1. **Minificar:** `enabled`
   1. **Depuración:** `disabled`
   1. **Gzip:** `enabled`
   1. **Tiempo:** `disabled`

1. **Apache Sling GET Servlet** está configurado para admitir configuraciones seguras de forma predeterminada, de la siguiente manera:

| **Configuración** | **Autor** | **Publicar** |
|---|---|---|
| Representación TXT | desactivado | desactivado |
| Representación de HTML | desactivado | desactivado |
| Representación JSON | enabled | enabled |
| Representación XML | desactivado | desactivado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desactivado | desactivado |
