---
title: Habilitación de la exportación de JSON para un componente
description: Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de trabajo del modelador.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: aeb8e954-dd6c-4e18-bb78-6eaac86fa4b9
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---

# Habilitar la exportación de JSON para un componente{#enabling-json-export-for-a-component}

Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de trabajo del modelador.

## Información general {#overview}

La exportación de JSON se basa en [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html?lang=es) y en el marco de [Exportador de modelos Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que a su vez se basa en [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Este método significa que el componente debe tener un modelo Sling si debe exportar JSON. Por lo tanto, siga estos dos pasos para habilitar la exportación de JSON en cualquier componente.

* [Defina un modelo Sling para el componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Anotar la interfaz del modelo Sling](#annotate-the-sling-model-interface)

## Defina un modelo Sling para el componente {#define-a-sling-model-for-the-component}

En primer lugar, se debe definir un modelo Sling para el componente.

>[!NOTE]
>
>Para ver un ejemplo del uso de modelos Sling, consulte [Desarrollo de exportadores de modelos Sling en AEM](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter).

La clase de implementación del modelo Sling debe estar anotada con lo siguiente:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Al hacerlo, se asegura de que el componente se pueda exportar solo, utilizando el selector `.model` y la extensión `.json`.

Además, especifica que la clase de modelo Sling se puede adaptar a la interfaz `ComponentExporter`.

>[!NOTE]
>
>Las anotaciones de Jackson no se especifican en el nivel de clase del Modelo Sling, sino en el nivel de interfaz del Modelo. Este método consiste en garantizar que la exportación de JSON se considere como parte de la API del componente.

>[!NOTE]
>
>Las clases `ExporterConstants` y `ComponentExporter` provienen del paquete `com.adobe.cq.export.json`.

### Uso de varios selectores {#multiple-selectors}

Aunque no es un caso de uso estándar, es posible configurar varios selectores además del selector `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Sin embargo, en tal caso, el selector `model` debe ser el primer selector y la extensión debe ser `.json`.

## Anotar la interfaz del modelo Sling {#annotate-the-sling-model-interface}

Para que el marco del exportador JSON lo procese, la interfaz del modelo debe implementar la interfaz `ComponentExporter` (o `ContainerExporter` para un componente de contenedor).

La interfaz del modelo Sling correspondiente (`MyComponent`) se anotaría usando [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir cómo se debe exportar (serializar).

La interfaz del modelo debe estar anotada correctamente para definir qué métodos se serializan. De forma predeterminada, todos los métodos que respetan la convención de nombres habitual de los captadores se serializan y derivan sus nombres de propiedades JSON de forma natural de los nombres de captadores. Este enfoque se puede prevenir o anular usando `@JsonIgnore` o `@JsonProperty` para cambiar el nombre de la propiedad JSON.

## Ejemplo {#example}

Los componentes principales admiten la exportación de JSON desde la versión [1.1.0 de los componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/introduction) y se pueden usar como referencia.

Para ver un ejemplo, consulte la implementación del modelo Sling del componente principal de imagen y su interfaz anotada.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir el proyecto aem-core-wcm-components en GitHub](https://github.com/adobe/aem-core-wcm-components)
* Descargar el proyecto como [archivo ZIP](https://codeload.github.com/adobe/aem-core-wcm-components/zip/main)


## Documentación relacionada {#related-documentation}

* El tema [Fragmentos de contenido en la guía del usuario de Assets](https://experienceleague.adobe.com/en/docs/experience-manager-64/assets/home#)
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Exportador JSON para servicios de contenido](/help/sites-developing/json-exporter.md)
* [Componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/introduction) y el [componente de fragmento de contenido](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/content-fragment-component)
