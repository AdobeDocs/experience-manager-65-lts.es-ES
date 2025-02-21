---
title: Exportador JSON para servicios de contenido
description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web. Proporcionan la entrega de contenido a canales que no son páginas web tradicionales de AEM, utilizando métodos estandarizados que cualquier cliente puede consumir.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 23%

---

# Exportador JSON para servicios de contenido{#json-exporter-for-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir lo siguiente:

* [Aplicaciones de una sola página](spa-walkthrough.md)
* Aplicaciones móviles nativas
* Otros canales y puntos de contacto externos a AEM

Con los fragmentos de contenido que utilizan contenido estructurado, puede proporcionar servicios de contenido mediante el exportador JSON para entregar el contenido de cualquier página de AEM en formato de modelo de datos JSON. Este método lo pueden consumir sus propias aplicaciones.

>[!NOTE]
>
>La funcionalidad descrita aquí está disponible para todos los componentes principales desde la [versión 1.1.0 de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es).

## Exportador JSON con componentes principales de fragmentos de contenido {#json-exporter-with-content-fragment-core-components}

Con el exportador JSON de AEM, puede entregar el contenido de cualquier página de AEM en formato de modelo de datos JSON. Este método lo pueden consumir sus propias aplicaciones.

En AEM, la entrega se logra mediante el selector `model` y la extensión `.json`.

`.model.json`

1. Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Ofrece contenido como:

   ![chlimage_1-192](assets/chlimage_1-192.png)

Como alternativa, puede entregar el contenido de un fragmento de contenido estructurado segmentándolo específicamente.

Utilice toda la ruta de acceso al fragmento (mediante `jcr:content`); por ejemplo, con un sufijo como.

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

La página puede contener un solo fragmento de contenido o varios componentes de varios tipos. También puede utilizar mecanismos como componentes de lista para buscar automáticamente contenido relevante.

* Por ejemplo, una dirección URL como:

  ```shell
  http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
  ```

* Ofrece contenido como:

  ![chlimage_1-193](assets/chlimage_1-193.png)

  >[!NOTE]
  >
  >Puede [adaptar sus propios componentes](/help/sites-developing/json-exporter-components.md) para acceder a estos datos y utilizarlos.

  >[!NOTE]
  >
  >Aunque no es una implementación estándar, se admiten [varios selectores,](json-exporter-components.md#multiple-selectors) pero `model` debe ser el primero.

### Información adicional {#further-information}

Consulte también lo siguiente:

* API HTTP de recursos

   * [API HTTP de recursos](/help/assets/mac-api-assets.md)

* Modelos Sling:

   * [Modelos Sling: asociando una clase de modelo con un tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM con JSON:

   * [Obtener información de página en formato JSON](/help/sites-developing/pageinfo.md)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* El tema [Fragmentos de contenido en la guía del usuario de Assets](/help/assets/content-fragments/content-fragments.md)

* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Activación de la exportación de JSON para un componente](/help/sites-developing/json-exporter-components.md)

* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y el [componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es)
