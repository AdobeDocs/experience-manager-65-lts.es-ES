---
title: Notas de la versión para [!DNL Adobe Experience Manager] 6.5 LTS
description: Busque la información de la versión actual de Adobe Experience Manager 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 70436606-d95c-4208-94f6-e33f3eefdf66
source-git-commit: 160b27c188f8bcd3f3a668b50d3a824598909688
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 95%

---

# Notas de la versión actual de Adobe Experience Manager 6.5 LTS. {#release-notes}

## Información de la versión {#release-information}

| Producto | [!DNL Adobe Experience Manager] |
|---|---|
| Versión | 6.5 LTS |
| Tipo | Versión principal |
| Fecha de disponibilidad general | 7 de marzo de 2025 |

## Novedades {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS es una versión de actualización de la base de código de [!DNL Adobe Experience Manager] 6.5. Proporciona correcciones importantes para los clientes, mejoras de alta prioridad para los clientes y correcciones generales de errores orientadas a la estabilidad del producto. También incluye versiones Service Pack de [!DNL Adobe Experience Manager] 6.5 hasta SP22.

La lista siguiente proporciona una descripción general, mientras que las páginas siguientes enumeran todos los detalles.

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

La plataforma de [!DNL Adobe Experience Manager] 6.5 LTS se basa en versiones actualizadas del marco de trabajo basado en OSGi (Apache Sling y Apache Felix) y el repositorio de contenido de Java™: Apache Jackrabbit Oak 1.68.x.

Eclipse Jetty 11.0.x se utiliza como motor servlet para Quickstart.

#### Compatibilidad con Java™  {#java-support}

* Compatibilidad con Java™ 17 y Java™ 21.
* Para obtener un rendimiento óptimo, reemplace los valores predeterminados de GC por otros valores. Para obtener más información, consulte la sección [Instalación y actualización](/help/sites-deploying/custom-standalone-install.md).
* Adobe distribuye actualizaciones de mantenimiento de Java™ 17 y Java™ 21 para que las utilicen los clientes en proyectos relacionados con AEM cuando no están disponibles para el público desde Oracle.

#### Empaquetado de Uberjar {#uber-jar-packaging}

* Hay una ligera diferencia en el empaquetado de Uberjar de AEM 6.5 LTS. Para obtener más información, consulte [Actualizar la versión de AEM Uber Jar](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version).

#### Actualizar {#upgrade}

* Para obtener detalles acerca del procedimiento de actualización, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

## Instalación y configuración {#install-update}

Para conocer los requisitos de configuración, consulte las [instrucciones de instalación](/help/sites-deploying/custom-standalone-install.md).

Para obtener instrucciones detalladas, consulte la [documentación de actualización](/help/sites-deploying/upgrade.md).

>[!NOTE]
>
> Para instalaciones nuevas de AEM 6.5 LTS, las definiciones de índice deben instalarse por separado. Para obtener más información, vea [este artículo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions).

## Plataformas compatibles {#supported-platforms}

Encuentre la matriz completa de plataformas compatibles, incluido el nivel de compatibilidad, en [Requisitos técnicos de AEM 6.5 LTS](/help/sites-deploying/technical-requirements.md).

>[!NOTE]
>
>Java™ 17 y Java™ 21 son las versiones recomendadas para usar con AEM 6.5 LTS.

## Funciones en desuso y eliminadas {#deprecated-and-removed-features}

Adobe revisa continuamente las funciones de los productos para mejorar el valor para los clientes mediante la modernización o el reemplazo de funciones antiguas. Estos cambios se realizan prestando especial atención a la compatibilidad con versiones anteriores.

Para comunicar la inminente eliminación o sustitución de las funciones de Adobe Experience Manager (AEM), se aplican las siguientes reglas:

1. Primero se anuncia el desuso. Aunque están en desuso, las funciones siguen estando disponibles, pero no se siguen mejorando.
1. La eliminación de las funciones en desuso se produce en la siguiente versión principal como pronto. La fecha objetivo real para la eliminación está planeada para su anuncio más adelante.

Este proceso proporciona a los clientes un ciclo de lanzamiento para adaptar su implementación a una nueva versión o a la siguiente versión de una capacidad en desuso, antes de eliminarla.

### Funciones en desuso {#deprecated-features}

En esta sección se enumeran las características y funciones que Adobe ha dejado de utilizar en AEM 6.5 LTS. Normalmente, Adobe deja de utilizar las características antes de eliminarlas en una versión futura y proporciona una alternativa.


Se recomienda a los clientes que comprueben si utilizan la función o capacidad en su implementación actual, y que planifiquen el cambio de la implementación y usen la alternativa proporcionada.

| Área | Funcionalidad | Reemplazo | Versión (SP) |
|---|---|---|---|
| Sites | [Editor de SPA](/help/sites-developing/spa-overview.md) | Los editores preferidos para administrar el contenido sin encabezado en AEM son: <br> el [Editor universal](/help/sites-developing/universal-editor/introduction.md) para la edición visual.<br>- [El editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición basada en formularios. | 6.5 LTS GA |

### Funciones eliminadas {#removed-features}

En esta sección se enumeran las características y funciones que se han eliminado de AEM 6.5 LTS. Las versiones anteriores tenían estas funciones marcadas como en desuso.

| Área | Funcionalidad | Reemplazo | Versión (SP) |
|--- |--- |--- |--- |
| Comercio | AEM CIF Classic no es compatible. | Migre a [AEM CIF](/help/commerce/cif/migration.md). | 6.5 LTS GA |
| Soluciones | Social/Communities no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Screens | Screens no se admiten. | No hay sustitución disponible. | 6.5 LTS GA |
| Recursos | `dam-pim` y `dam-rating` no se admiten porque los paquetes dependen de las redes sociales. | No hay sustitución disponible. | 6.5 LTS GA |
| Recursos | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` se ha eliminado. | Utilice la API alternativa `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` que se ha añadido. | 6.5 LTS GA |
| Portal | AEM Portal Director no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | Se ha eliminado el paquete `com.adobe.granite.socketio`. | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` no es compatible.  | No hay sustitución disponible. | 6.5 LTS GA |
| Granite | `crx2oak` no es compatible.  | Elija la versión relevante de [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` no es compatible.  | No hay sustitución disponible. | 6.5 LTS GA |
| Guava | Todas las dependencias de Guava ahora se eliminan en AEM y, por lo tanto, el paquete `com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` no forma parte de AEM. | Los clientes pueden agregar Guava por su cuenta si dependen de Guava o reemplazar el código de Guava con colecciones de Java u otras alternativas si es posible. | 6.5 LTS GA |
| `We.Retail` | No se admite el sitio de muestra `We-retail`. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | El paquete `oak-solr-osgi` no es compatible. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | `org.apache.servicemix.bundles.abdera-parser`, `org.apache.servicemix.bundles.jdom` y `org.apache.sling.atom.taglib` no son compatibles. | No hay sustitución disponible. | 6.5 LTS GA |
| Código abierto | `org.apache.commons.io` paquetes se han exportado desde `org.apache.commons.commons-io`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | Se están exportando `javax.mail` paquetes desde el paquete `com.sun.javax.mail`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | `org.apache.jackrabbit.api` paquetes se han exportado ahora desde el paquete `org.apache.jackrabbit.oak-jackrabbit-api`. | No se requiere ningún cambio. | 6.5 LTS GA |
| Código abierto | `com.github.jknack.handlebars` no es compatible | Elija la [versión](https://mvnrepository.com/artifact/com.github.jknack/handlebars) pertinente. | 6.5 LTS GA |

## Problemas conocidos {#known-issues}

### Problema con el paquete de scripts JSP en AEM 6.5.21-6.5.23 y AEM 6.5 LTS GA

AEM 6.5.21, 6.5.22, 6.5.23 y AEM 6.5 LTS GA se envían con el paquete `org.apache.sling.scripting.jsp:2.6.0`, que contiene un problema conocido. El problema suele producirse con una carga alta cuando la instancia de AEM administra muchas solicitudes simultáneas.

Cuando se produce este problema, puede aparecer una de las siguientes excepciones en los registros de errores junto con las referencias a `org.apache.sling.scripting.jsp:2.6.0`:

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

Hay disponible una revisión [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) para resolver este problema.

### Error de conexión de Dispatcher con la función Solo SSL {#ssl-only-feature}

Al habilitar la función Solo SSL en las implementaciones de AEM, existe un problema conocido que afecta a la conectividad entre las instancias de Dispatcher y AEM. Después de habilitar esta función, las comprobaciones de estado pueden fallar y la comunicación entre las instancias de Dispatcher y AEM puede verse interrumpida. Este problema se produce específicamente cuando los clientes intentan conectarse a través de `https + IP` desde Dispatcher a instancias de AEM. Está relacionado con problemas de validación de SNI (Server Name Indication).

**Impacto:**

* Errores de comprobación de estado con códigos de respuesta HTTP 400
* Tráfico interrumpido entre instancias de Dispatcher y AEM
* El contenido no se puede proporcionar correctamente a través de Dispatcher
* Errores de conexión al utilizar HTTPS con direcciones IP en la configuración de Dispatcher
* Errores HTTP 400 del tipo &quot;SNI no válido&quot; al conectarse mediante HTTPS + IP

**Entornos afectados:**

* Implementaciones de AEM con configuraciones de Dispatcher
* Sistemas en los que se ha habilitado la función Solo SSL
* Configuraciones de Dispatcher que utilizan el método de conexión `https + IP` a instancias de AEM

**Solución:**
Si tiene este problema, póngase en contacto con Atención al cliente de Adobe. Hay disponible una revisión [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) para resolver este problema. No intente habilitar las funciones Solo SSL hasta que aplique la revisión necesaria.

## Sitios web restringidos{#restricted-sites}

Estos sitios solo están disponibles para los clientes. Si es cliente y necesita acceso, póngase en contacto con el Administrador de cuentas de Adobe.

* [Descarga de producto en licensing.adobe.com](https://licensing.adobe.com/)
* [Póngase en contacto con Atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/customer-one/using/home).