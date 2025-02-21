---
title: Implementación de referencia de We.Retail
description: We.Retail es una previsualización tecnológica de una implementación de referencia que ilustra la forma recomendada de configurar una presencia en línea con AEM
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: ac26c0163309b6cb6c0cfde2098a8cc05955d03f
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 7%

---

# Implementación de referencia de We.Retail{#we-retail-reference-implementation}

## Introducción {#introduction}

We.Retail es una implementación de referencia y contenido de muestra que ilustra la forma recomendada de configurar una presencia en línea con Adobe Experience Manager.

We.Retail utiliza las últimas tecnologías de Adobe Experience Manager (AEM), como HTL, diseños adaptables, plantillas editables, componentes principales y mucho más.

Aunque ilustra un vertical minorista, la forma en que se configura el sitio se puede aplicar a cualquier vertical y solo las funciones del catálogo de productos y del carro de compras son específicas para minoristas.

## Características {#features}

Como implementación de referencia estándar de AEM, We.Retail muestra algunas de las funciones más potentes de AEM.

| **Característica** | **Descripción** | **Interesado?** |
|---|---|---|
| [Estructura del sitio globalizada](/help/sites-administering/tc-bp.md) | We.Retail incluye formatos de idioma que se copian en tiempo real en sitios específicos de cada país. | [¡Pruébelo!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Diseño interactivo](/help/sites-authoring/responsive-layout.md) | Todas las páginas tienen un diseño interactivo para adaptarse dinámicamente a la pantalla y al tamaño del dispositivo. | [¡Pruébelo!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Plantillas editables](/help/sites-developing/page-templates-editable.md) | Todas las páginas se basan en plantillas editables, lo que permite a los usuarios que no son desarrolladores adaptar y personalizar las plantillas. | [¡Pruébelo!](/help/sites-developing/we-retail-editable-templates.md) |
| [Lenguaje de plantilla HTML ](https://experienceleague.adobe.com/es/docs/experience-manager-htl/content/overview) | Todos los componentes se basan en HTL |  |
| [Componentes principales](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/introduction) | Todos los componentes se basan en los nuevos componentes principales y son más utilizables y configurables por el usuario de forma predeterminada | [¡Pruébelo!](/help/sites-developing/we-retail-core-components.md) |
| [Fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) | La sección Experiencias de We.Retail muestra la capacidad de reutilizar contenido mediante fragmentos de contenido. | [Pruébelos](/help/sites-developing/we-retail-content-fragments.md) |
| [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md) | Un fragmento de experiencia es un grupo de uno o más componentes, incluido el contenido y el diseño, a los que se puede hacer referencia dentro de las páginas. | [Pruébelos](/help/sites-developing/we-retail-experience-fragments.md) |

## Introducción {#getting-started}

We.Retail se entrega como contenido de muestra de AEM. Para usar, simplemente [inicie AEM como lo haría normalmente](/help/sites-deploying/deploy.md#getting-started), asegurándose de que el contenido de muestra no esté deshabilitado.

>[!CAUTION]
>
>No instale We.Retail en instancias de producción. Las instancias de producción deben iniciarse en `nosamplecontent` [modo de ejecución](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail se basa en la tecnología AEM más reciente y, por lo tanto, no admite la [creación clásica de IU](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md).

### Última versión {#latest-version}

Aunque We.Retail se distribuye con la versión de AEM, es posible que se actualicen el contenido y sus funciones después de la versión. Por lo tanto, es posible [descargar la última versión desde GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases), luego [cargarla](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [instalarla](/help/sites-administering/package-manager.md#installing-packages) como un paquete en su instancia de AEM.

### Primeros pasos {#first-steps}

1. Una vez iniciado AEM (o instalado We.Retail), el sitio **We.Retail** está disponible en la [consola Sites](/help/sites-authoring/basic-handling.md#global-navigation).
1. Por ejemplo, la siguiente página se puede abrir y debería tener el aspecto que se muestra en el [apéndice](#appendix) siguiente:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail y Geometrixx {#we-retail-geometrixx}

Geometrixx y sus muchas encarnaciones servían como contenido de muestra en versiones anteriores de AEM. Desde la versión 6.3, We.Retail ha sido el contenido de muestra entregado con AEM y sirve como la nueva implementación de referencia estándar.

We.Retail es técnicamente más robusta y aprovecha la tecnología más reciente de AEM para ser más flexible y escalable, a la vez que muestra las nuevas funciones del producto.

### Comparación de funciones {#feature-comparison}

En la tabla siguiente se ofrece una descripción general de las principales funciones disponibles en We.Retail en comparación con Geometrixx.

* **Disponible** significa que los ejemplos de la característica se encuentran en el contenido de muestra.
* **No disponible** significa que los ejemplos de la característica no están disponibles en el contenido de la muestra, pero no significa que la característica en sí no lo esté.

| **Característica** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Estructura del sitio globalizada | Los formatos de idiomas se copian en tiempo real en sitios específicos de cada país | No disponible |
| Fragmentos de contenido | Disponible | No disponible |
| Fragmentos de experiencias | Disponible | No disponible |
| Diseño adaptable | Para todas las páginas | Solo Geometrixx Media |
| Plantillas editables | Para todas las páginas | No disponible |
| HTL | Todos los componentes | Limitado |
| Direccionamiento | Para todas las páginas | Solo Geometrixx Outdoors |
| Manuscritos | No disponible | Disponible |
| Visualizador de carrusel, descargas y componentes de gráficos | No disponible | Disponible |
| Control de columna | Reemplazado por el contenedor de diseño | Disponible |
| Formularios | No disponible | Disponible |
| Campaign | No hay ejemplos de correo electrónico | Disponible |

>[!NOTE]
>
>Esta lista trata de ser completa, pero no debe considerarse exhaustiva.

## Contribute {#contribute}

We.Retail se ha lanzado como un proyecto de código abierto y la última versión del código fuente se puede descargar desde GitHub.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub.

* [Abrir proyecto aem-sample-we-retail en GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Descargar el proyecto como [archivo ZIP](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)

La última versión también se puede [descargar directamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0) como un paquete instalable.

Si tiene problemas, envíe un [problema de GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

No dude en ramificar o contribuir con [solicitudes de extracción](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Vista previa {#preview}

Vista previa de la página de bienvenida de We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
