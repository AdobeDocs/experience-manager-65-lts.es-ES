---
title: Personalización de la consola Sitios web (IU clásica)
description: La consola Administración de sitios web se puede ampliar para mostrar columnas personalizadas
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 0%

---

# Personalización de la consola Sitios web (IU clásica){#customizing-the-websites-console-classic-ui}

## Adición de una columna personalizada a la consola Sitios web (siteadmin) {#adding-a-custom-column-to-the-websites-siteadmin-console}

La consola Administración de sitios web se puede ampliar para mostrar columnas personalizadas. La consola se ha creado a partir de un objeto JSON que se puede ampliar creando un servicio OSGI que implemente la interfaz `ListInfoProvider`. Este servicio modifica el objeto JSON que se envía al cliente para crear la consola.

Este tutorial paso a paso explica cómo mostrar una nueva columna en la consola Administración de sitios web implementando la interfaz `ListInfoProvider`. Consiste en los siguientes pasos:

1. [Creando el servicio OSGI](#creating-the-osgi-service) e implementando el paquete que lo contiene en el servidor de AEM.
1. (opcional) [Probando el nuevo servicio](#testing-the-new-service) emitiendo una llamada JSON para solicitar el objeto JSON que se usa para compilar la consola.
1. [Mostrando la nueva columna](#displaying-the-new-column) ampliando la estructura de nodos de la consola en el repositorio.

>[!NOTE]
>
>Este tutorial también se puede utilizar para ampliar las siguientes consolas de administración:
>
>* la consola Assets digital
>* la consola Comunidad
>

### Creación del servicio OSGI {#creating-the-osgi-service}

La interfaz `ListInfoProvider` define dos métodos:

* `updateListGlobalInfo`, para actualizar las propiedades globales de la lista,
* `updateListItemInfo`, para actualizar el elemento de lista única.

Los argumentos para ambos métodos son:

* `request`, el objeto de solicitud HTTP de Sling asociado,
* `info`, el objeto JSON que se va a actualizar, que es respectivamente la lista global o el elemento de lista actual,
* `resource`, un recurso de Sling.

La implementación de ejemplo es la siguiente:

* Agrega una propiedad *starred* a cada elemento, que es `true` si el nombre de página comienza con *e* y `false` en caso contrario.

* Agrega una propiedad *starredCount*, que es global para la lista y contiene el número de elementos de la lista con estrellas.

Para crear el servicio OSGI:

1. En CRXDE Lite, [cree un paquete](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. Agregue el código de ejemplo siguiente.
1. Genere el paquete.

El nuevo servicio está en funcionamiento.

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* Su implementación debe decidir, en función de la solicitud o el recurso proporcionados, si debe agregar la información al objeto JSON o no.
>* Si la implementación de `ListInfoProvider` define una propiedad que existe en el objeto de respuesta, el valor que proporcione sobrescribirá.
>
>  Puede usar [clasificación de servicio](https://docs.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) para administrar el orden de ejecución de varias implementaciones de `ListInfoProvider`.

### Prueba del nuevo servicio {#testing-the-new-service}

Cuando abre la consola de administración de sitios web y explora su sitio, el explorador emite una llamada Ajax para obtener el objeto JSON utilizado para crear la consola. Por ejemplo, cuando se desplaza a la carpeta `/content/geometrixx`, se envía la siguiente solicitud al servidor de AEM para crear la consola:

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

Para asegurarse de que el nuevo servicio se está ejecutando después de haber implementado el paquete que lo contiene:

1. Dirija el explorador a la siguiente dirección URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. La respuesta debe mostrar las nuevas propiedades como se indica a continuación:

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### Visualización de la nueva columna {#displaying-the-new-column}

El último paso consiste en adaptar la estructura de nodos de la consola de administración de sitios web para mostrar la nueva propiedad para todas las páginas de Geometrixx superponiendo `/libs/wcm/core/content/siteadmin`. Proceda como se indica a continuación:

1. En CRXDE Lite, cree la estructura de nodos `/apps/wcm/core/content` con nodos de tipo `sling:Folder` para reflejar la estructura `/libs/wcm/core/content`.

1. Copie el nodo `/libs/wcm/core/content/siteadmin` y péguelo debajo de `/apps/wcm/core/content`.

1. Copie el nodo `/apps/wcm/core/content/siteadmin/grid/assets` en `/apps/wcm/core/content/siteadmin/grid/geometrixx` y cambie sus propiedades:

   * Quitar **pageText**

   * Establecer **pathRegex** en `/content/geometrixx(/.*)?`
Esto hace que la configuración de cuadrícula esté activa para todos los sitios web de Geometrixx.

   * Establecer **storeProxySuffix** en `.pages.json`

   * Edite la propiedad multivalor **storeReaderFields** y agregue el valor `starred`.

   * Para activar la funcionalidad de MSM, agregue los siguientes parámetros MSM a la propiedad de varias cadenas **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. Agregue un nodo `starred` (de tipo **nt:unstructured**) debajo de `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` con las siguientes propiedades:

   * **dataIndex**: `starred` de tipo cadena

   * **encabezado**: `Starred` de tipo cadena

   * **xtype**: `gridcolumn` de tipo String

1. (opcional) Suelte las columnas que no desee mostrar en `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` es una ruta de acceso mnemónica que, de manera predeterminada, apunta a `/libs/wcm/core/content/siteadmin`.
Para redirigir esto a su versión de siteadmin en `/apps/wcm/core/content/siteadmin`, defina la propiedad `sling:vanityOrder` para que tenga un valor superior al definido en `/libs/wcm/core/content/siteadmin`. El valor predeterminado es 300, por lo que cualquier valor superior es adecuado.

1. Vaya a la consola de administración de sitios web y navegue hasta el sitio de Geometrixx:
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. La nueva columna llamada **Starred** está disponible y muestra información personalizada de la siguiente manera:

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>Si varias configuraciones de cuadrícula coinciden con la ruta solicitada definida por la propiedad **pathRegex**, se utilizará la primera y no la más específica, lo que significa que el orden de las configuraciones es importante.

### Paquete de muestra {#sample-package}

El resultado de este tutorial está disponible en el paquete [Personalización de la consola de administración de sitios web](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) en Uso compartido de paquetes.
