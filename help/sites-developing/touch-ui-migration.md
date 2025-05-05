---
title: Migración a la IU táctil
description: Obtenga información acerca de la migración de Adobe Experience Manager a la IU táctil y cómo le afecta.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: e9b26de3-6e14-4187-8f25-6e56ee3092a7
source-git-commit: 013c9155817811913963ca514f7a6369b338d487
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 3%

---

# Migración a la IU táctil{#migration-to-the-touch-ui}

A partir de la versión 6.0, Adobe Experience Manager (AEM) introdujo una nueva interfaz de usuario denominada *IU táctil* (también conocida como *IU táctil*). Se alinea con Adobe Experience Cloud y con las directrices generales de la interfaz de usuario de Adobe. Esta se ha convertido en la interfaz de usuario estándar en AEM con la interfaz heredada orientada al escritorio conocida como *IU clásica*.

Si ha estado utilizando AEM con la IU clásica, tome medidas para migrar la instancia. Esta página está diseñada para actuar como un trampolín al proporcionar vínculos a recursos individuales.

>[!NOTE]
>
>Este proyecto de migración puede tener un impacto significativo en su instancia. Consulte [Administración de proyectos - Prácticas recomendadas](/help/managing/best-practices.md) para ver las directrices recomendadas.

## Conceptos básicos {#the-basics}

Al migrar, tenga en cuenta las siguientes diferencias principales entre la IU clásica y la táctil:

<table>
 <tbody>
  <tr>
   <td>IU clásica</td>
   <td>IU táctil.</td>
  </tr>
  <tr>
   <td>Se describe en el repositorio JCR como una estructura de nodos. Cada nodo que representa un elemento de la interfaz de usuario se denomina <em>widget ExtJS</em> y <code>ExtJS</code> lo procesa en el lado del cliente.</td>
   <td>También se describe en el repositorio JCR como una estructura de nodos. Sin embargo, en este caso, cada nodo hace referencia a un tipo de recurso de Sling (componente de Sling), que se encarga de su procesamiento. Por lo tanto, la interfaz de usuario se procesa (básicamente) en el lado del servidor.</td>
  </tr>
  <tr>
   <td><p><code>sling:resourceType</code></p>
    <ul>
     <li>no se usa</li>
    </ul> </td>
   <td><code>sling:resourceType</code>
    <ul>
     <li>usado</li>
     <li>por ejemplo<br /> <code>cq/gui/components/authoring/dialog</code><br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Nodos de diálogo:</p>
    <ul>
     <li>Nombre: <code>dialog</code></li>
     <li><code>jcr:primaryType</code>: <code>cq:Dialog</code></li>
    </ul> </td>
   <td><p>Nodos de diálogo:</p>
    <ul>
     <li>Nombre: <code>cq:dialog</code></li>
     <li><code>jcr:primaryType</code>: <code>nt:unstructured</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Ubicación de JavaScript:</p>
    <ul>
     <li>Las partes imperativas se incrustan directamente mediante oyentes o se administran en clientlibs.</li>
    </ul> </td>
   <td><p>Ubicación de JavaScript:</p>
    <ul>
     <li>Las partes imperativas no pueden incorporarse en la definición del diálogo; separación de responsabilidades.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Gestión de eventos:</p>
    <ul>
     <li>Los widgets de diálogo hacen referencia directamente al código JavaScript.</li>
    </ul> </td>
   <td><p>Gestión de eventos:</p>
    <ul>
     <li>JavaScript observa los eventos de diálogo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Representación realizada por el cliente:
    <ul>
     <li>El cliente crea dinámicamente los componentes de la IU.</li>
     <li>El cliente solicita la definición del componente (como JSON) desde el servidor.</li>
    </ul> </td>
   <td>Representación realizada por el servidor:
    <ul>
     <li>El cliente solicita páginas junto con la interfaz de usuario relacionada.</li>
     <li>El servidor envía (push) la interfaz de usuario como documentos de HTML; se utilizan componentes de la interfaz de usuario de Coral.<br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

En otras palabras, migrar una sección de la interfaz de usuario de la IU clásica a la IU táctil significa trasladar un *widget ExtJS* a un *componente Sling*. Para facilitar esto, la interfaz de usuario táctil se basa en el marco de trabajo de la interfaz de usuario de Granite, que ya proporciona algunos componentes de Sling para la interfaz de usuario (denominados componentes de la interfaz de usuario de Granite).

Los conceptos básicos del desarrollo de la IU táctil proporcionan una base sólida:

* [Conceptos de la IU táctil de AEM](/help/sites-developing/touch-ui-concepts.md)
* [Estructura de la IU táctil de AEM](/help/sites-developing/touch-ui-structure.md)

## Migración de creación de páginas {#migrating-page-authoring}

Los cuadros de diálogo son un factor importante a la hora de migrar los componentes:

* [Desarrollar componentes de AEM](/help/sites-developing/developing-components.md) (con la IU táctil)
* [Migración desde un componente clásico](/help/sites-developing/developing-components.md#migrating-from-a-classic-component)
* [Herramientas de modernización de AEM](/help/sites-developing/modernization-tools.md): para ayudarle a convertir los cuadros de diálogo de sus componentes de la IU clásica a la IU táctil

   * Hay una capa de compatibilidad en la IU táctil para abrir un cuadro de diálogo de IU clásica dentro de un &quot;envoltorio de IU táctil&quot;, pero esto tiene una funcionalidad limitada y no se recomienda a largo plazo.

* [Personalizar campos de diálogo en la IU táctil](https://helpx.adobe.com/es/experience-manager/kt/eseminars/gems/aem-customizing-dialog-fields-in-touch-ui.html)
* [Creación de un nuevo componente de campo de IU de Granite](/help/sites-developing/granite-ui-component.md)
* [Personalización de la creación de páginas](/help/sites-developing/customizing-page-authoring-touch.md) (con la IU táctil)

## Migración de consolas {#migrating-consoles}

También puede personalizar las consolas:

* [Personalización de las consolas](/help/sites-developing/customizing-consoles-touch.md) (para la IU táctil)

## Consideraciones relacionadas {#related-considerations}

Aunque no están directamente relacionados con una migración a la interfaz de usuario táctil, hay problemas relacionados que vale la pena considerar al mismo tiempo, ya que también son una práctica recomendada:

* [Plantillas](/help/sites-developing/templates.md) - [Plantillas editables](/help/sites-developing/page-templates-editable.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)
* [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es)

>[!NOTE]
>
>Ver también [Desarrollo - Prácticas recomendadas](/help/sites-developing/best-practices.md).

## Otros recursos {#further-resources}

Para obtener información completa sobre el desarrollo de AEM, consulte la recopilación de recursos en:

* [Guía del usuario sobre desarrollo](/help/sites-developing/getting-started.md)
* [Documentación de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
* [Tutoriales y vídeos de AEM 6.5 Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/overview.html?lang=es)
* [Introducción al desarrollo de AEM Sites: Tutorial de WKND](/help/sites-developing/getting-started.md)
* [Gems de AEM](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/overview.html?lang=es)
* [Herramientas de modernización de AEM](https://opensource.adobe.com/aem-modernize-tools/)

>[!CAUTION]
>
>Las herramientas de modernización de AEM son un esfuerzo de la comunidad y Adobe no las admite ni las garantiza.
