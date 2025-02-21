---
title: Herramientas de desarrollo
description: Para desarrollar las aplicaciones JCR, Apache Sling o Adobe Experience Manager, hay disponibles varios conjuntos de herramientas.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 4%

---

# Herramientas de desarrollo{#development-tools}

Para desarrollar las aplicaciones JCR, Apache Sling o Adobe Experience Manager (AEM), existen los siguientes conjuntos de herramientas disponibles:

* un conjunto formado por [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) y WebDAV. CRXDE Lite está incrustado en CRX/AEM y le permite realizar tareas de desarrollo estándar en el explorador. Con CRXDE Lite, puede crear y editar archivos (como .jsp y .java), carpetas, plantillas, componentes, cuadros de diálogo, nodos, propiedades y paquetes al registrar e integrar con SVN.

  Se recomienda CRXDE Lite cuando no tiene acceso directo al servidor de CRX/AEM, cuando desarrolla una aplicación ampliando o modificando los componentes predeterminados y los paquetes Java™ o cuando no necesita un depurador dedicado, finalización de código y resaltado de sintaxis.

* un conjunto formado por lo siguiente:
   * Un Entorno De Desarrollo Integrado. Por ejemplo, [Eclipse](/help/sites-developing/howto-projects-eclipse.md) o [IntelliJ](/help/sites-developing/ht-intellij.md).
   * Una herramienta de compilación. Por ejemplo, [Apache Maven](/help/sites-developing/ht-projects-maven.md).
   * FileVault, desarrollado por Adobe para asignar un repositorio a un sistema de archivos, un sistema de control de versiones. Por ejemplo, Subversion.
   * Un sistema de seguimiento de errores. Por ejemplo, Jira.
   * Un sistema de administración de dependencias central. Por ejemplo, Apache Archiva.
   * Y construir un sistema de automatización. Por ejemplo, Apache Continuum.

  Esta configuración le permite integrar completamente su aplicación (contenido, código, configuración) en cualquier entorno y proceso de desarrollo. El vínculo entre los diferentes elementos es la representación del sistema de archivos del repositorio a través de FileVault, ya que todas las herramientas de desarrollo mencionadas anteriormente pueden trabajar con archivos.

## Extensiones para entornos de desarrollo integrados {#extensions-for-integrated-development-environments}

Adobe lanzó las siguientes extensiones:

* [Extensión de AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Extensión de AEM Brackets](/help/sites-developing/aem-brackets.md)

### Otras herramientas {#other-tools}

AEM se distribuye con otras herramientas que facilitan el desarrollo:

* [Editor de diálogos](/help/sites-developing/dialog-editor.md)
* [Uso de Translator para administrar diccionarios](/help/sites-developing/i18n-translator.md)
* [Administración de paquetes mediante Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Cómo desarrollar proyectos de AEM con Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Cómo crear proyectos de AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Cómo desarrollar proyectos de AEM con IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Cómo utilizar la herramienta VLT](/help/sites-developing/ht-vlttool.md)
* [Cómo utilizar la herramienta de servidor proxy](/help/sites-developing/ht-proxy-server.md)
* [Herramientas de modernización de AEM](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

Herramientas que facilitan la creación de nuevos proyectos:

* [Tipo de archivo del proyecto AEM](https://github.com/adobe/aem-project-archetype)
* [Plantillas de AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>El siguiente tutorial puede ser de interés para iniciar un nuevo proyecto de AEM:
>[Introducción a AEM Sites, parte 1: Configuración del proyecto](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
