---
title: Externalización de direcciones URL
description: El externalizador es un servicio OSGI que permite transformar mediante programación una ruta de recurso en una dirección URL externa y absoluta
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Externalización de direcciones URL{#externalizing-urls}

En Adobe Experience Manager (AEM), **Externalizer** es un servicio OSGI que le permite transformar mediante programación una ruta de acceso de recursos (por ejemplo, `/path/to/my/page`) en una dirección URL externa y absoluta (por ejemplo, `https://www.mycompany.com/path/to/my/page`) al anteponer a la ruta de acceso un DNS preconfigurado.

Dado que una instancia no puede conocer su URL visible externamente si se ejecuta detrás de una capa web y que, a veces, se debe crear un vínculo fuera del ámbito de la solicitud, este servicio proporciona un lugar central para configurar esas URL externas y crearlas.

En esta página se explica cómo configurar el servicio **Externalizer** y cómo utilizarlo. Para obtener más información, consulte [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html).

## Configuración del servicio externalizador {#configuring-the-externalizer-service}

El servicio **Externalizer** le permite definir de forma centralizada varios dominios que se pueden utilizar para prefijar mediante programación las rutas de recursos. Cada dominio se identifica con un nombre único que se utiliza para hacer referencia al dominio mediante programación.

Para definir una asignación de dominio para el servicio **Externalizer**:

1. Vaya al administrador de configuración a través de **Herramientas**, luego **Consola web** o escriba:

   `https://<host>:<port>/system/console/configMgr`

1. Haga clic en **Externalizador de vínculos CQ de día** para abrir el cuadro de diálogo de configuración.

   >[!NOTE]
   >
   >El vínculo directo a la configuración es `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Defina una asignación **Domains**: una asignación consta de un nombre único que se puede usar en el código para hacer referencia al dominio, a un espacio y al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Donde:

   * **scheme** es http o https, pero también puede ser ftp, etc.

      * si lo desea, utilice https para aplicar vínculos https
      * se utiliza si el código de cliente no anula el esquema al solicitar la externalización de una dirección URL.

   * **server** es el nombre de host (puede ser un nombre de dominio o una dirección ip).
   * **puerto** (opcional) es el número de puerto.
   * **contextpath** (opcional) solo se establece si AEM está instalado como aplicación web en una ruta de contexto diferente.

   Por ejemplo: `production https://my.production.instance`

   Los siguientes nombres de asignación están predefinidos y deben configurarse, ya que AEM depende de ellos:

   * `local`: la instancia local
   * `author`: DNS del sistema de creación
   * `publish`: DNS del sitio web público

   >[!NOTE]
   >
   >Una configuración personalizada le permite agregar una categoría, como `production`, `staging`, o incluso sistemas externos que no son de AEM, como `my-internal-webservice`. Es útil evitar codificar estas URL en diferentes lugares del código base de un proyecto.

1. Haga clic en **Guardar** para guardar los cambios.

>[!NOTE]
>
>Adobe recomienda [agregar la configuración al repositorio](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Uso del servicio externalizador {#using-the-externalizer-service}

Esta sección muestra algunos ejemplos de cómo se puede usar el servicio **Externalizer**:

1. **Para obtener el servicio externalizador en un JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Para externalizar una ruta de acceso con el dominio &#39;publicar&#39;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominio:

   * `publish https://www.website.com`

   `myExternalizedUrl` termina con el valor:

   * `https://www.website.com/contextpath/my/page.html`

1. **Para externalizar una ruta de acceso con el dominio &#39;author&#39;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominio:

   * `author https://author.website.com`

   `myExternalizedUrl` termina con el valor:

   * `https://author.website.com/contextpath/my/page.html`

1. **Para externalizar una ruta de acceso con el dominio &#39;local&#39;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominio:

   * `local https://publish-3.internal`

   `myExternalizedUrl` termina con el valor:

   * `https://publish-3.internal/contextpath/my/page.html`

1. Puede encontrar más ejemplos en [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/Externalizer.html).
