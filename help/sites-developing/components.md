---
title: Información general sobre componentes
description: Los componentes son unidades modulares que implementan una funcionalidad específica para presentar el contenido en su sitio web
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 45%

---

# Información general sobre componentes{#components-overview}

Esta página proporciona información general sobre los componentes de Adobe Experience Manager (AEM), como los [usados para la creación de páginas](/help/sites-authoring/default-components-foundation.md).

## ¿Qué son los componentes? {#what-exactly-is-a-component}

* Unidades modulares que implementan funcionalidades específicas para presentar el contenido en su sitio web.
* Reutilizable.
* Se desarrolla como unidades independientes dentro de una carpeta del repositorio.
* No tienen archivos de configuración ocultos.
* Pueden contener otros componentes.
* Puede ejecutarse en cualquier lugar dentro de cualquier sistema AEM. También se pueden limitar para que se ejecuten en componentes específicos.
* Disponen de una interfaz de usuario estandarizada.
* Tienen un comportamiento de edición que se puede configurar.
* Utilice cuadros de diálogo creados con subelementos basados en componentes de la interfaz de usuario de Granite
* Se han desarrollado con [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) (recomendado) o JSP.
* Se pueden desarrollar para crear componentes personalizados que amplíen la funcionalidad predeterminada.

Como los componentes son modulares, puede hacer lo siguiente:

* Desarrollar un nuevo componente en la instancia local.
* Implementarla en su entorno de prueba.
* Implementarla en su entorno de creación activo, donde permiten a los autores o administradores añadir y configurar contenido.
* Impleméntelo en los entornos de publicación activos, donde se utiliza para representar contenido para los visitantes del sitio web. Algunos componentes, por ejemplo, para las comunidades, también aceptan entradas de los usuarios.

Cada componente AEM:

* Es un tipo de recurso.
* Es una colección de scripts que realizan completamente una función específica.
* Puede funcionar en *aislamiento*, es decir, dentro de AEM o de un portal.

## Componentes listos para usar dentro de AEM {#out-of-the-box-components-within-aem}

AEM viene con una variedad de [componentes listos para usar](/help/sites-authoring/default-components.md) que proporcionan funcionalidad completa, entre ellos:

* Sistema de párrafos ( `parsys`)
* Página ( `responsivegrid` - solo IU táctil)
* Texto
* Imagen, con texto adjunto
* Barra de herramientas

Los componentes proporcionados y su uso en [los sitios web de We.Retail de ejemplo](/help/sites-developing/we-retail.md) proporcionados ilustran cómo implementar y utilizar componentes. Los componentes se proporcionan con todo el código fuente y se pueden utilizar tal cual o como puntos de partida para los componentes modificados o ampliados.

### Componentes principales y componentes básicos {#core-components-and-foundation-components}

Hay dos conjuntos de componentes de AEM proporcionados por Adobe disponibles:

* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
* [Componentes de base](/help/sites-authoring/default-components-foundation.md)

Los **componentes principales** se introdujeron con AEM 6.3 y ofrecen funciones flexibles y personalizables de creación. El [sitio de referencia de We.Retail](/help/sites-developing/we-retail.md) ilustra cómo se pueden utilizar los componentes principales y representa las prácticas recomendadas actuales de desarrollo de componentes.

**Componentes de base** han estado disponibles con AEM para muchas versiones y están disponibles de forma predeterminada en una instalación estándar de AEM. Aunque se siguen admitiendo, la mayoría han quedado obsoletas, ya no se mejoran y se basan en tecnologías heredadas.

>[!NOTE]
>
>[Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) representan las prácticas recomendadas actuales para el diseño y el desarrollo de componentes y sirven como implementaciones de referencia.
>
>[Las herramientas de modernización de AEM](modernization-tools.md) pueden ayudar a migrar a los componentes principales.

### Visualización de componentes disponibles {#viewing-available-components}

Para obtener una descripción general de todos los componentes disponibles en la instancia de AEM, use la [Consola de componentes](/help/sites-authoring/default-components-console.md).

Como alternativa, también puede utilizar CRXDE Lite para obtener una lista de todos los componentes disponibles en el repositorio.

1. En **[!UICONTROL CRXDE Lite]**, seleccione **[!UICONTROL Herramientas]** en la barra de herramientas y, a continuación, **[!UICONTROL Consulta]**, que abre la pestaña **[!UICONTROL Consulta]**.

1. En la pestaña **[!UICONTROL Consulta]**, seleccione `XPath` como **[!UICONTROL Tipo]**.

1. En el campo de entrada **[!UICONTROL Consulta]**, escriba la cadena siguiente:

   `//element(*, cq:Component)`

1. Cuando hace clic en **[!UICONTROL Ejecutar]**, se muestran los componentes.

## Recursos adicionales {#further-reading}

Las siguientes páginas proporcionan información más detallada sobre el desarrollo de estos y otros componentes:

* [Componentes de AEM: conceptos básicos](/help/sites-developing/components-basics.md)
* [Desarrollo de componentes de AEM](/help/sites-developing/developing-components.md)
* [Desarrollo de componentes de AEM: ejemplos de código](/help/sites-developing/developing-components-samples.md)
* [Configuración de varios editores locales](/help/sites-developing/multiple-inplace-editors.md)
* [Modo de desarrollador](/help/sites-developing/developer-mode.md)
* [Prueba de la IU](/help/sites-developing/hobbes.md)
* [Componentes para fragmentos de contenido](/help/sites-developing/components-content-fragments.md)
* [Obtener información de página en formato JSON](/help/sites-developing/pageinfo.md)
* [Internacionalización de componentes](/help/sites-developing/i18n.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
* [Uso de Ocultar condiciones](/help/sites-developing/hide-conditions.md)
* IU clásica

   * [Componentes de AEM (IU clásica)](/help/sites-developing/developing-components-classic.md)
   * [Uso y ampliación de widgets (IU clásica)](/help/sites-developing/widgets.md)
   * [Uso de xtypes (IU clásica)](/help/sites-developing/xtypes.md)
   * [Desarrollo de Forms (IU clásica)](/help/sites-developing/developing-forms.md)
