---
title: Prácticas recomendadas para desarrolladores de AEM
description: Los equipos de ingeniería y consultoría de Adobe han desarrollado un conjunto completo de prácticas recomendadas para los desarrolladores de AEM.
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2a406ca2870e241539819ae62c6a14904ee71211
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 3%

---

# Prácticas recomendadas{#best-practices}

## Prácticas recomendadas para desarrolladores: Introducción {#best-practices-for-developers-getting-started}

Los equipos de ingeniería y consultoría de Adobe han desarrollado un conjunto completo de prácticas recomendadas para los desarrolladores de AEM. Los desarrolladores de Adobe se adhieren a estas prácticas recomendadas a medida que desarrollan actualizaciones principales de productos de AEM y códigos de cliente para implementaciones de clientes.

Antes de iniciar el proyecto de desarrollo de AEM, revise primero estas prácticas recomendadas:

* [Prácticas de desarrollo](/help/sites-developing/development-practices.md)
* [Arquitectura de contenido](/help/sites-developing/content-architecture.md)
* [Arquitectura de software](/help/sites-developing/software-architecture.md)
* [Sugerencias de codificación](/help/sites-developing/coding-tips.md)
* [Problemas de código](/help/sites-developing/code-pitfalls.md)
* [Interacción JCR](/help/sites-developing/jcr-integration.md)
* [Paquetes OSGi](/help/sites-developing/osgi-bundles.md)
* [Prácticas recomendadas para la API de Java](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html?lang=es)

### Información adicional sobre prácticas recomendadas {#additional-best-practices-information}

Las siguientes áreas tienen documentación disponible específica para el desarrollo de prácticas recomendadas:

* [Sites](#sites)
* [Herramientas/HTL](#tooling-htl)

En las tablas siguientes se describen y vinculan documentos específicos.

Para conocer las prácticas recomendadas sobre la administración, la implementación, el mantenimiento o la creación, consulte una de las siguientes opciones:

* [Prácticas recomendadas de administración](/help/sites-administering/administer-best-practices.md)
* [Prácticas recomendadas de creación](/help/sites-authoring/best-practices.md)
* [Implementación de prácticas recomendadas](/help/sites-deploying/best-practices.md)

## Sites {#sites}

La administración y creación del contenido del sitio web tiene algunas prácticas recomendadas descritas a continuación:

<table>
 <tbody>
  <tr>
   <td>Parte de la teoría detrás de la IU táctil estándar.</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">IU táctil: conceptos</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">IU táctil: estructura</a></p> </td>
   <td>Estos documentos proporcionan información general sobre los conceptos y la estructura de la IU táctil.</td>
  </tr>
  <tr>
   <td>IU táctil: personalización de consolas </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">Personalización de consolas de IU táctiles</a></td>
   <td>Este documento describe la mejor manera de ampliar las consolas para la IU táctil.</td>
  </tr>
  <tr>
   <td>IU táctil: personalizar la creación de páginas</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">Personalizar la creación de páginas de IU táctiles</a></td>
   <td>Describe cómo ampliar la creación de páginas para la IU táctil.</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">Desarrollo y ampliación de flujos de trabajo</a></td>
   <td><p>Los flujos de trabajo le permiten automatizar las actividades de Adobe Experience Manager (AEM) y pueden representar una gran cantidad del procesamiento que se produce en un entorno de AEM, por lo que es muy recomendable planificar las implementaciones de flujos de trabajo con cuidado.</p> </td>
  </tr>
 </tbody>
</table>

## Herramientas/HTL {#tooling-htl}

El lenguaje de plantilla HTML (HTL) es un nuevo sistema de plantillas de HTML, introducido con AEM 6.0. Sustituye a JSP y ESP como sistema de plantillas preferido de AEM.

|  |  |  |
|---|---|---|
| Información general sobre HTL | [Resumen y sintaxis de HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es) | Este documento describe qué es HTL, cómo pasar a HTL, un proyecto de ejemplo, sintaxis, expresiones e instrucciones |
| Uso de la API en Java | [HTL Java Use-API](https://helpx.adobe.com/es/experience-manager/htl/using/use-api.html) | La API de uso de Java de HTL permite que un archivo HTL acceda a los métodos de ayuda en una clase Java personalizada. |

>[!NOTE]
>
>Los siguientes tutoriales de varias partes pueden ser de interés para la práctica recomendada de configuración de un nuevo proyecto de AEM, que detalla los componentes principales, las plantillas editables, las bibliotecas de clientes y el desarrollo de componentes:
>[Introducción a AEM Sites: Tutorial de WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
