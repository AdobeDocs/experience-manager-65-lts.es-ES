---
title: Resolución de problemas de la aplicación de AEM Forms
description: Obtenga información sobre los problemas más comunes con la aplicación AEM Forms y cómo solucionarlos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 100%

---

# Resolución de problemas de la aplicación de AEM Forms {#troubleshoot-aem-forms-app}

Este artículo describe los mensajes de error que se pueden mostrar al generar la aplicación de AEM Forms y los pasos para resolverlos.

Las secciones de este artículo incluyen:

* [Pérdida de archivos adjuntos para usuarios de iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Los borradores de formulario HTML5 enviados por los usuarios de Workspace no son visibles en el portal](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Los formularios HTML5 (no almacenados en caché) no se pueden cargar en la aplicación AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms no se sincroniza en Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Versión incompatible de Gradle](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problemas de compatibilidad de los complementos de Gradle y Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Pérdida de archivos adjuntos para usuarios de iOS {#attachment-loss-for-ios-users}

La aplicación AEM Forms para iOS configurada para sincronizarse con AEM Forms en OSGi solo admite archivos adjuntos de nivel de campo. Todos los archivos adjuntos deben tener nombres únicos. Si varios archivos adjuntos tienen un nombre idéntico, solo se conserva uno, y el resto de los que tienen un nombre idéntico se pierden. Siga estos pasos para evitar que los usuarios de dispositivos iOS pierdan datos:

1. En el servidor conectado, vaya a **Adobe Experience Manager > Herramientas > Operaciones > Consola web**.
1. Busque y haga clic en **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]**.
1. En el cuadro de diálogo [!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables], habilite la opción **Convertir nombres de archivo en únicos**.

   Si la opción **Convertir nombres de archivo en únicos** está desactivada, los usuarios perderán datos cuando intenten enviar formularios adaptables con varios archivos adjuntos.

1. Haga clic en **Guardar**.

## Los borradores de formulario HTML5 enviados por los usuarios de Workspace no son visibles en el portal {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Los borradores guardados de los formularios HTML5 activados en la aplicación AEM Forms con el Perfil de procesamiento HTML **Guardar como borrador** no son visibles para los usuarios de Workspace. Para ver los borradores guardados de los formularios HTML5 enviados por los usuarios de Workspace en el portal, realice los siguientes pasos:

1. Abra CRXDE e inicie sesión con credenciales de administrador.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. En la ruta raíz de CRXDE, en la Lista de control de acceso de Control de acceso, haga clic en **+**.
1. En el cuadro de diálogo **Agregar nueva entrada**, haga clic en el botón de búsqueda de grupo del campo Principal.
1. En el campo Nombre del cuadro de diálogo Seleccionar principal, escriba `PERM_WORKSPACE_USER` y haga clic en **Buscar**.
1. Seleccione el grupo `PERM_WORKSPACE_USER` en el cuadro de diálogo Seleccionar principal y haga clic en **Aceptar**.
1. En el cuadro de diálogo Agregar nueva entrada, el grupo `PERM_WORKSPACE_USER` está seleccionado en el campo Principal.

   Habilite los privilegios `jcr:read` para el grupo de usuarios.

1. Haga clic en **Aceptar**.

## Los formularios HTML5 (no almacenados en caché) no se pueden cargar en la aplicación AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Cuando la aplicación AEM Forms está conectada a una versión anterior del servidor de AEM Forms, los formularios HTML5 no almacenados en caché no se cargan en la aplicación AEM Forms.

Siga estos pasos para resolver el problema:

1. En la instancia de autor, vaya a **Adobe Experience Manager > Herramientas > Configurar el servicio sin conexión de la aplicación de Workspace > Configurar ahora**.
1. En la página **Servicio sin conexión de la aplicación de Workspace**, haga clic en **Caché de recursos manual**.

   URL: https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. En la página **Caché de recursos manual**, haga clic en el botón **+** para añadir una ruta CRX.
1. En el campo **Agregar un nuevo recurso**, escriba: /etc.clientlibs/fd/xfaforms/I18N/en_US.js y haga clic en **Agregar**.
1. Haga clic en **Guardar**.

## AEM Forms no se sincroniza en Windows {#aem-forms-do-not-sync-on-windows}

En la aplicación de AEM Forms para Windows, un formulario no se sincroniza con el servidor conectado si la ruta del formulario o cualquiera de sus recursos contiene 256 caracteres o más.

Modifique la ruta del formulario y sus recursos para reducir el número de caracteres a menos de 256 caracteres.

## Versión incompatible de Gradle {#unsupported-version-of-gradle}

**Mensaje de error:** El proyecto utiliza una versión no compatible de Gradle.

El mensaje de error se muestra al generar la aplicación AEM Forms en Android Studio. El problema se debe a que la versión de Gradle no es compatible con el sistema.

**Resolución:** Haga clic en **Corregir el contenedor de Gradle y volver a importar el proyecto** para resolver el problema.

![versión_no_compatible_de_gradle](assets/gradle_unsupported_version.png)

## Problemas de compatibilidad de los complementos de Gradle y Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Mensaje de error:** Las versiones del complemento de Android Gradle y Gradle no son compatibles.

El mensaje de error se muestra al seleccionar la opción **Build APK** en el menú **Build** de la interfaz de usuario de Android Studio.

![compatibilidad_plugin_gradle](assets/gradle_plugin_compatibility.png)

**Solución:** Abra **Gradle Scripts** > **gradle-wrapper.properties** y edite la propiedad **distributionUrl**.

Por ejemplo, la consola de Android Studio recomienda reducir la versión de Gradle a 3.5. Edite la versión de **distributionUrl** del archivo **gradle-wrapper.properties**.

Seleccione **Build** > **Build APK** para resolver el error y generar el archivo .apk.

![propiedades_contenedor_gradle](assets/gradle_wrapper_properties.png)
