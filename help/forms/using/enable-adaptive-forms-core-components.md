---
title: Cómo habilitar los componentes principales de Forms adaptable en AEM 6.5 Forms
description: Guía paso a paso para ayudarle a habilitar los componentes principales de Forms adaptable en un entorno de AEM 6.5 Forms.
keywords: Habilitar componentes principales, componentes principales, Forms adaptable, componentes principales en 6.5, componentes principales de Forms adaptable en AEM 6.5, componentes principales de AF en AEM 6.5, componentes principales de AEM 6.5 y Forms
role: Admin, Developer
feature: Adaptive Forms,Core Components
solution: Experience Manager, Experience Manager Forms
exl-id: a163598d-0a6e-45a8-b3b2-1f260007952b
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 48%

---

# Habilitar los componentes principales de Forms adaptable en AEM 6.5 Forms {#enable-adaptive-forms-core-components}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=es) |
| AEM 6.5 | Este artículo |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

Al habilitar los componentes principales de Forms adaptable, podrá empezar a crear, publicar y distribuir [componentes principales basados en Forms adaptable](create-an-adaptive-form-core-components.md) y [Forms adaptable sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=es) desde su entorno de AEM 6.5 Forms.

Para habilitar los componentes principales de Forms adaptable en el entorno de Forms de AEM 6.5, configure e implemente un proyecto basado en [AEM Archetype 41 o posterior](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) (con las opciones de formularios habilitadas) en todas las instancias de autor y publicación.

Este artículo contiene instrucciones detalladas para configurar e implementar un proyecto basado en AEM Archetype 41 o posterior en el entorno de AEM 6.5 Forms para habilitar los componentes principales de Forms adaptables. Puede consultar la lista siguiente de **versiones compatibles con AEM 6.5** para habilitar los componentes principales de Forms:

## Requisitos previos {#prerequisites}

Antes de habilitar los componentes principales de Forms adaptable en un entorno de AEM 6.5 Forms:

* [Actualice a AEM 6.5 Forms Service Pack 16 (6.5.16.0) o posterior](https://experienceleague.adobe.com/docs/experience-manager-65-lts/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* Instalar la última versión de [Apache Maven](https://maven.apache.org/download.cgi).

* Instale un editor de texto sin formato. Por ejemplo, Microsoft Visual Studio Code.

## Crear e implementar el último proyecto basado en el arquetipo de AEM

Para crear un proyecto basado en el arquetipo de AEM 41 o [posterior](https://github.com/adobe/aem-project-archetype) e implementarlo en todas las instancias de autor y publicación:

1. Inicie sesión en el equipo, aloje y ejecute la instancia de AEM 6.5 Forms, como administrador.
1. Abra el símbolo del sistema o el terminal y ejecute el siguiente comando para crear un proyecto de tipo de archivo de AEM (con las opciones de formularios habilitadas):

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux o Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   Cuando ejecute el comando anterior, asegúrese de tener en cuenta los siguientes puntos:

   * No cambie el valor de la propiedad `aemVersion` de `6.5.15.0` a ninguna otra cosa.

   * Establezca la propiedad `archetypeVersion` en `41` o posterior. Para obtener la versión más reciente, consulte la sección de requisitos del sistema en [Tipo de archivo del proyecto de AEM](https://github.com/adobe/aem-project-archetype).

   * Actualice el comando para reflejar los valores específicos de su entorno, incluidos `appTitle`, `appId` y `groupId`. Además, establezca el valor de la propiedad `includeFormsenrollment` en `y`. Si usa el portal de Forms, establezca la opción `includeExamples=y` para incluir los componentes principales del portal de Forms en su proyecto.


1. (Solo para proyectos basados en la versión 41 del arquetipo) Una vez creado el proyecto de arquetipo de AEM, habilite las temáticas para formularios adaptables basados en componentes principales. Para habilitar las temáticas, haga lo siguiente:

   1. Abra la [Carpeta de proyecto de arquetipo de AEM]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html para editarla:

   1. Agregue el siguiente código en la línea 21:

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Agregue el código mencionado anteriormente en la línea 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Guarde y cierre el archivo.

1. Actualizar el proyecto para que incluya la última versión de los componentes principales de Forms:

   1. Abra la [Carpeta de proyecto de arquetipo de AEM]/pom.xml para editarla.
   1. Establezca la versión de `core.forms.components.version` y `core.forms.components.af.version` en la [última versión de los componentes principales de Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history) y asegúrese de que ambos tengan la misma versión que los **componentes principales de Forms** mencionados en la tabla, y establezca la versión de `core.wcm.components.version` tal como se indica en los [componentes principales de WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html).

      >[!WARNING]
      >
      >* Al crear un proyecto Archetype con versión 45, `[AEM Archetype Project Folder]/pom.xml` establece inicialmente la versión de los componentes principales de Forms en 1.1.28. Antes de crear o implementar el proyecto Archetype, actualice la versión de los componentes principales de Forms a 1.1.26. Puede encontrar la versión más reciente en el [historial de versiones de AEM 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html#aem-as-form-version-history).

      >[!NOTE]
      >
      >* Si configura cualquier otra topología, asegúrese de agregar las direcciones URL de envío, de relleno previo y de otro tipo a la lista de permitidos de Dispatcher.

   1. Guarde y cierre el archivo.


1. Una vez que el proyecto de arquetipo de AEM se haya creado correctamente, cree el paquete de implementación para su entorno. Haga clic para generar el paquete:

   1. Vaya al directorio raíz del proyecto del arquetipo de AEM.

   1. Ejecute el siguiente comando para compilar el proyecto de arquetipo de AEM para su entorno:

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   Una vez que el proyecto de arquetipo de AEM se haya compilado correctamente, se generará un paquete de AEM. Puede encontrar el paquete en [Carpeta de proyecto de arquetipo de AEM]\all\target\[appid].all-[versión].zip

1. Utilice el [Administrador de paquetes](/help/sites-administering/package-manager.md) para implementar la [Carpeta de proyecto de arquetipo de AEM]\all\target\[appid].all-[versión].zip en el entorno de instancias de autor y publicación.

>[!NOTE]
>
>
>
> * Si tiene dificultades para acceder al cuadro de diálogo de inicio de sesión en una instancia de publicación, para instalar el paquete a través del Administrador de paquetes, intente utilizar la URL: `http://[Publish Server URL]:[PORT]/system/console` para iniciar sesión. Esto permite acceder a la página de inicio de sesión en una instancia de publicación, lo que le permite continuar con el proceso de instalación.
> * No elimine ni descarte el proyecto Archetype después de implementarlo en su entorno. El proyecto de tipo de archivo es necesario para agregar temas personalizados y nuevos de componentes principales de Forms adaptables a su entorno.

Los componentes principales están habilitados para su entorno. Se implementan una plantilla de formularios adaptables basados en componentes principales en blanco y una temática de Lienzo 3.0 que le permiten [crear formularios adaptables basados en los componentes principales](create-an-adaptive-form-core-components.md).

## Preguntas frecuentes

### ¿Qué son los componentes principales?

Los [componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) son un conjunto de componentes estandarizados de la administración de contenido web (WCM) para AEM con el objetivo de acelerar el tiempo de desarrollo y reducir el coste de mantenimiento de sus sitios web.

### ¿Qué funcionalidades completas se añaden al habilitar los componentes principales?


Cuando los componentes principales de formularios adaptables se habilitan para su entorno, se agrega a este una plantilla de formulario adaptable basada en componentes principales en blanco y una temática de Lienzo 3.0. Tras habilitar los componentes principales de formularios adaptables para su entorno, puede:

* Crear componentes principales basados en formularios adaptables.
* Crear componentes principales basados en plantillas de formulario adaptable.
* Crear temáticas personalizadas para componentes principales basadas en plantillas de formulario adaptable.
* Proporcione representaciones JSON de un formulario adaptable basado en componentes principales a canales como móvil, web, apps nativas y servicios que requieren la representación sin encabezado de un formulario.

## Siguientes pasos

* [Crear un formulario adaptable basado en componentes principales](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Crear o agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Crear temáticas para componentes principales basados en Forms adaptable](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Crear una plantilla para componentes principales basados en Forms adaptable](template-editor.md)
