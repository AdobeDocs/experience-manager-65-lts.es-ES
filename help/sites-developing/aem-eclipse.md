---
title: Herramientas para desarrolladores de AEM para Eclipse
description: Obtenga información sobre las herramientas para desarrolladores de Adobe Experience Manager para Eclipse.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: 5aaf9560-fa44-49d3-96c0-47cc71e7e658
source-git-commit: c77c4cc5345a34d5504216d9e67af217acd644c2
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 2%

---


# Herramientas para desarrolladores de AEM para Eclipse {#aem-developer-tools-for-eclipse}

![Logotipo de herramientas para desarrolladores de Experience Manager para Eclipse](assets/eclipse-logo.png)

## Información general {#overview}

_Experience Manager Developer Tools for Eclipse_ es un complemento de Eclipse basado en el complemento [Eclipse para Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) lanzado bajo la licencia Apache 2.

Ofrece varias funciones que facilitan el desarrollo de AEM:

* Integración perfecta con las instancias de AEM a través del conector de servidor Eclipse
* Sincronización para paquetes OSGi y de contenido
* Compatibilidad de depuración con la capacidad de intercambio en caliente de código
* Bootstrap simple de proyectos de AEM mediante un asistente de creación de proyectos específico
* Edición sencilla de propiedades JCR

## Requisitos {#requirements}

Antes de utilizar las herramientas para desarrolladores de AEM, debe hacer lo siguiente:

* Descargue e instale [Eclipse IDE para desarrolladores web y Java empresariales.](https://www.eclipse.org/downloads/packages/)
   * La versión 1.4.0 de las herramientas para desarrolladores de AEM para Eclipse es compatible con Eclipse 2022-12 (4.26) o posterior y requiere Java 17 o posterior para ejecutarse.
* Configure su instalación de Eclipse para asegurarse de que tiene al menos 1 GB de memoria de pila editando el archivo de configuración `eclipse.ini` tal como se describe en las [Preguntas frecuentes sobre Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>En macOS, debes hacer clic con el botón derecho en **Eclipse.app** y, a continuación, seleccionar **Mostrar contenido del paquete** para encontrar tu `eclipse.ini`.

## Cómo instalar las herramientas para desarrolladores de AEM para Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

Cuando haya cumplido los [requisitos](#requirements) anteriores, puede instalar el complemento de herramientas para desarrolladores de la siguiente manera:

1. Abra el [sitio web de herramientas para desarrolladores de AEM.](https://eclipse.adobe.com/)

1. Copie el **vínculo de instalación**.

   * Como alternativa, puede descargar un archivo en lugar de utilizar el vínculo de instalación.
   * Este método permite la instalación sin conexión, pero no recibe notificaciones de actualización automáticas.

1. En Eclipse, abre el menú **Ayuda**.
1. Haga clic en **Instalar nuevo software**.
1. Haga clic en **Agregar...**.
1. En el campo **Nombre**, escriba `AEM Developer Tools`.
1. En el campo **Ubicación**, copie la URL de instalación.
1. Haga clic en **Agregar**.
1. Compruebe los complementos de **AEM** y **Sling**.
1. Haga clic en **Siguiente**.
1. En la ventana **Detalles de la instalación**, revise los elementos que se van a instalar y haga clic de nuevo en **Siguiente**.
1. Acepte los contratos de licencia y haga clic en **Finalizar**.
1. En el cuadro de diálogo **Autoridades de confianza** que aparece, seleccione la autoridad o el sitio `https://eclipse.adobe.com` y haga clic en **Confiar en seleccionados**.
1. En el cuadro de diálogo **Artefactos de confianza** que aparece, seleccione los firmantes de código y haga clic en **Confiar en seleccionados**.
1. Haz clic en **Reiniciar ahora** para reiniciar Eclipse.

## La perspectiva de AEM {#the-aem-perspective}

En Eclipse, una **perspectiva** determina las acciones y vistas disponibles dentro de una ventana y permite la interacción orientada a tareas con los recursos de Eclipse. Para obtener más información acerca de las perspectivas, consulte la [documentación de Eclipse.](https://help.eclipse.org/latest/index.jsp).

Las _herramientas de desarrollo de Experience Manager para Eclipse_ proporcionan una perspectiva de AEM que le ofrece control total sobre sus proyectos e instancias de AEM. Para abrir la perspectiva de AEM:

1. En la barra de menús de Eclipse, seleccione **Ventana** > **Perspectiva** > **Abrir perspectiva** > **Otra**.
1. Seleccione **AEM** en el cuadro de diálogo y haga clic en **Abrir**.

![La perspectiva de AEM en Eclipse](assets/eclipse-aem-perspective.png)

## Ejemplo de proyecto de varios módulos {#sample-multi-module-project}

Las _herramientas para desarrolladores de Experience Manager para Eclipse_ incluyen un proyecto de varios módulos de ejemplo que le ayudará a ponerse al día rápidamente con la configuración de un proyecto en Eclipse. También sirve como guía de prácticas recomendadas sobre varias funciones de AEM, en las que se aprovecha el [tipo de archivo del proyecto AEM.](https://github.com/adobe/aem-project-archetype)

Siga estos pasos para crear el proyecto de ejemplo:

1. En el menú **Archivo** > **Nuevo** > **Proyecto**, vaya a la sección **AEM** y seleccione **Proyecto de módulo múltiple de muestra de AEM**.

   ![Proyecto de módulo múltiple de muestra de AEM](assets/aem-sample-project.png)

1. Haga clic en **Siguiente**.

   >[!NOTE]
   >
   >Este paso podría demorar un poco porque [m2eclipse](https://eclipse.dev/m2e/) debe analizar los catálogos de arquetipos.

1. `com.adobe.aem : aem-project-archetype : <highest-number>` debe seleccionarse automáticamente en la lista desplegable **Tipo de archivo**. Seleccione una versión anterior si lo desea. Haga clic en **Siguiente**.

   ![Seleccionar versión de tipo de archivo](assets/select-archetype.png)

1. Proporcione los siguientes campos para el proyecto de ejemplo:

   * **Nombre**
   * **Id. de grupo**
   * **Id. de artefacto**
   * **appId**: es posible que tenga que expandir las opciones de **Avanzado** para establecer este valor.
   * **appTitle**: es posible que tenga que expandir las opciones de **Advanced** para establecer este valor.
   * **Paquete**: es posible que tenga que expandir las opciones de **Avanzado** para establecer este valor.

   ![Definir propiedades de tipo de archivo](assets/archetype-properties.png)

1. Haga clic en **Siguiente**.

1. Configure un servidor de AEM al que se conecte Eclipse seleccionando **Configurar nuevo servidor** y proporcionando un nombre de servidor y los detalles de conexión necesarios.

   ![Conectarse al servidor de AEM](assets/connect-server.png)

   * Para utilizar la característica del depurador, debe iniciar AEM en modo de depuración proporcionando el parámetro `-agentlib`, por ejemplo:

   ```text
   $ java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar aem-author-p4502.jar
   ```

   >[!TIP]
   >
   >Para obtener más información sobre la depuración del proyecto que se ejecuta en un SDK de AEM local, consulte el documento [Depuración remota de SDK de AEM.](https://experienceleague.adobe.com/es/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-sdk/remote-debugging)

1. Haga clic en **Finalizar**.

Se crea la estructura del proyecto. Puede tardar un momento en descargar los artefactos necesarios en el proyecto.

>[!NOTE]
>
>En una instalación nueva o cuando las dependencias de Maven no se han descargado anteriormente, Eclipse puede informar de que el proyecto se creó con errores. En este caso, siga el procedimiento descrito en la sección [Resolver la definición de proyecto no válida.](#resolving-invalid-project-definition)

## Cómo Importar Proyectos Existentes {#how-to-import-existing-projects}

Use la característica **Nuevo proyecto** para crear la estructura básica del proyecto.

1. Siga las instrucciones para crear un [Proyecto de módulo múltiple de ejemplo,](#sample-multi-module-project) que crea una estructura de proyecto básica con una separación correcta de preocupaciones:

   * `PROJECT.ui.apps` para el contenido `/apps` y `/etc`
   * `PROJECT.ui.content` para `/content` creado
   * `PROJECT.core` para paquetes Java
   * `PROJECT.it.launcher` y `PROJECT.it.tests` para pruebas de integración

1. Reemplace el contenido de su proyecto `PROJECT.ui.apps` por las carpetas `apps` y `etc` de su paquete:

   1. En el panel **Explorador del proyecto**, expanda `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Haga clic con el botón derecho en la carpeta `apps` y elija **Mostrar en** > **Explorador del sistema**.
   1. Elimine las carpetas `apps` y `etc` allí.
   1. En la misma ubicación, coloque las carpetas `apps` y `etc` del paquete de contenido.
   1. En Eclipse, haga clic con el botón secundario en el proyecto `PROJECT.ui.apps` y elija **Actualizar**.

1. A continuación, haga lo mismo para `PROJECT.ui.content` y reemplace su carpeta de contenido por el de sus paquetes:

   1. En el panel **Explorador del proyecto**, expanda `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Haga clic con el botón derecho en la carpeta de contenido más detallada y elija **Mostrar en** > **Explorador del sistema**.
   1. Elimine la carpeta de contenido allí.
   1. En la misma ubicación, coloque la carpeta de contenido del paquete de contenido.
   1. En Eclipse, haga clic con el botón secundario en el proyecto `PROJECT.ui.content` y elija **Actualizar**.

1. Actualice los `filter.xml` archivos de estos dos proyectos para que se correspondan con el contenido del paquete de contenido. Para ello, abra el archivo `META-INF/vault/filter.xml` del paquete de contenido en un editor de texto/código independiente.

   * Este es un ejemplo del aspecto que puede tener el archivo `filter.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. En cuanto al contenido del paquete que se dividió en dos proyectos, también debe dividir estas reglas de filtro en dos y actualizar los `filter.xml` archivos de los dos proyectos en consecuencia.

   1. En Eclipse, abra `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Reemplace el contenido del elemento `<workspaceFilter>` por las reglas del paquete que comiencen por `/apps` y `/etc`
      * Por ejemplo:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. Luego abra `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Reemplace las reglas por las del paquete que comiencen por `/content`.
      * Por ejemplo:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. Asegúrese de guardar todos los cambios. Ahora puede sincronizar ese nuevo contenido con la instancia de AEM.

1. En el panel **Servidores**, asegúrese de que la conexión esté iniciada y, en caso afirmativo, no iníciela.

1. Haga clic en el icono **Limpiar y publicar**.

Una vez finalizado, el paquete debería estar ejecutándose en su instancia. Al guardar, cualquier cambio se sincroniza automáticamente con la instancia.

Si desea volver a compilar un paquete a partir del proyecto, haga clic con el botón derecho en `PROJECT.ui.apps` o `PROJECT.ui.content` y elija **Ejecutar como** > **Instalación de Maven**.

Ahora tiene una carpeta de destino creada con el paquete dentro de (por ejemplo, `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Resolución de problemas {#troubleshooting}

### Resolver definición de proyecto no válida {#resolving-invalid-project-definition}

Para resolver dependencias no válidas y la definición del proyecto, siga estos pasos:

1. Seleccione todos los proyectos creados.
1. Haga clic con el botón derecho.
1. En el menú contextual, seleccione **Maven** > **Actualizar proyectos**.
1. Compruebe **Forzar actualizaciones de instantáneas/versiones**.
1. Haga clic en **OK**.

Eclipse descarga las dependencias requeridas. Esto puede tardar un momento.

## Más información {#more-information}

La herramienta oficial del IDE de Apache Sling para el sitio web de Eclipse proporciona información adicional útil:

* La [**Guía del usuario de herramientas del IDE de Apache Sling para Eclipse**](https://sling.apache.org/documentation/development/ide-tooling.html) le guía a través de los conceptos generales, la integración del servidor y las capacidades de implementación que admiten las herramientas de desarrollo de AEM.
* [Solución de problemas de las herramientas del IDE de Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [Lista de problemas conocidos](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

La siguiente documentación oficial de [Eclipse](https://www.eclipse.org/) puede ayudar a configurar su entorno:

* [Introducción a Eclipse](https://eclipseide.org/getting-started/)
* [Sistema de Ayuda de Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Integración de Maven (m2eclipse)](https://www.eclipse.org/m2e/)
