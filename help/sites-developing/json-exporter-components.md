---
title: Activación de la exportación de JSON para un componente
description: Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de trabajo del modelador.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 6%

---

# Activación de la exportación de JSON para un componente{#enabling-json-export-for-a-component}

Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de trabajo del modelador.

## Información general {#overview}

La exportación de JSON se basa en [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html) y en el marco de [Exportador de modelos Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que a su vez se basa en [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Esto significa que el componente debe tener un modelo Sling si debe exportar JSON. Por lo tanto, siga estos dos pasos para habilitar la exportación de JSON en cualquier componente.

* [Defina un modelo Sling para el componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Anotar la interfaz del modelo Sling](#annotate-the-sling-model-interface)

## Definir un modelo Sling para el componente {#define-a-sling-model-for-the-component}

En primer lugar, se debe definir un modelo Sling para el componente.

>[!NOTE]
>
>Para ver un ejemplo del uso de modelos Sling, consulte [Desarrollo de exportadores de modelos Sling en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=es).

La clase de implementación del modelo Sling debe estar anotada con lo siguiente:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Esto garantiza que el componente se pueda exportar solo, utilizando el selector `.model` y la extensión `.json`.

Además, esto especifica que la clase de modelo Sling se puede adaptar a la interfaz `ComponentExporter`.

>[!NOTE]
>
>Las anotaciones de Jackson no se especifican en el nivel de clase del Modelo Sling, sino en el nivel de interfaz del Modelo. Esto sirve para garantizar que la exportación de JSON se considere como parte de la API del componente.

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

Para que el marco del exportador JSON lo tenga en cuenta, la interfaz del modelo debe implementar la interfaz `ComponentExporter` (o `ContainerExporter`, si hay un componente contenedor).

La interfaz del modelo Sling correspondiente (`MyComponent`) se anotaría usando [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir cómo se debe exportar (serializar).

La interfaz del modelo debe estar anotada correctamente para definir qué métodos se deben serializar. De forma predeterminada, todos los métodos que respetan la convención de nombres habitual de los captadores se serializan y derivan sus nombres de propiedades JSON de forma natural de los nombres de captadores. Esto se puede evitar o sobrescribir usando `@JsonIgnore` o `@JsonProperty` para cambiar el nombre de la propiedad JSON.

## Ejemplos {#example}

Los componentes principales admiten la exportación de JSON desde la versión [1.1.0 de los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y se pueden usar como referencia.

Para ver un ejemplo, consulte la implementación del modelo Sling del componente principal de imagen y su interfaz anotada.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir el proyecto aem-core-wcm-components en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte lo siguiente:

* El tema [Fragmentos de contenido en la guía del usuario de Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-authoring/content-fragments.md)
* [Exportador JSON para servicios de contenido](/help/sites-developing/json-exporter.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y el [componente de fragmento de contenido](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
