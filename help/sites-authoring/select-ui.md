---
title: Selección de la interfaz de usuario en AEM
description: Configure la interfaz que desea utilizar para trabajar en Adobe Experience Manager 6.5 LTS.
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 508f9dfb-1a4e-45bd-acdd-48cc910bdd0f
source-git-commit: d8057cf9ee86c2ec9c1f556fa7c18f98797fe982
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# Selección de la IU{#selecting-your-ui}

La IU táctil de Adobe Experience Manager (AEM) es la IU estándar. Sin embargo, puede haber ocasiones en que el usuario desee cambiar a la [IU clásica](/help/sites-classic-ui-authoring/classicui.md). Existen varias opciones para hacerlo.

Hay varias ubicaciones en las que puede definir qué interfaz de usuario se va a utilizar:

* [Configuración de la interfaz de usuario predeterminada para su instancia](#configuring-the-default-ui-for-your-instance)
Esto establece la interfaz de usuario predeterminada para mostrar al iniciar sesión el usuario. El usuario puede anular esto y seleccionar una interfaz de usuario diferente para su cuenta o sesión actual.

* [Creando IU clásica para tu cuenta](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Esto establece que la interfaz de usuario sea la predeterminada al editar páginas, aunque el usuario puede anularla y seleccionar una interfaz de usuario diferente para su cuenta o sesión actual.

* [Cambiando a la IU clásica para la sesión actual](#switching-to-classic-ui-for-the-current-session)
Cambia a la IU clásica para la sesión actual.

* En el caso de la creación de [páginas, el sistema realiza ciertas invalidaciones en la relación con la interfaz de usuario](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Varias opciones para cambiar a la IU clásica no están disponibles de forma inmediata, sino que deben configurarse para su instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

>[!NOTE]
>
>Las instancias actualizadas desde una versión anterior conservan la IU clásica para la creación de páginas.
>
>Después de la actualización, la creación de páginas no cambia automáticamente a la IU táctil, pero puede configurarla con la [configuración OSGi](/help/sites-deploying/configuring-osgi.md) del **servicio de modo de IU de creación de WCM** (servicio `AuthoringUIMode`). Consulte [Anulaciones de IU para el editor](#ui-overrides-for-the-editor).

## Configuración de la interfaz de usuario predeterminada para la instancia {#configuring-the-default-ui-for-your-instance}

Un administrador del sistema puede configurar la interfaz de usuario que se ve al iniciar y al iniciar sesión usando [Root Mapping](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Esto se puede sobrescribir por los valores predeterminados de usuario o la configuración de sesión.

## Configuración de la creación de IU clásica para su cuenta {#setting-classic-ui-authoring-for-your-account}

Cada usuario puede acceder a sus propias [preferencias de usuario](/help/sites-authoring/user-properties.md#userpreferences) para definir si desea utilizar la IU clásica para la creación de páginas, en lugar de la IU predeterminada.

Esto se puede anular mediante la configuración de la sesión.

## Cambio a la IU clásica para la sesión actual {#switching-to-classic-ui-for-the-current-session}

Al utilizar la IU táctil, es posible que los usuarios de escritorio deseen volver a la IU clásica (solo de escritorio). Existen varios métodos para cambiar a la IU clásica en la sesión actual:

* **Vínculos de navegación**

  >[!CAUTION]
  >
  >Esta opción para cambiar a la IU clásica no está disponible de forma inmediata, debe configurarse para su instancia.
  >
  >
  >Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

  Si está activada, cada vez que pase el ratón sobre una consola aplicable, aparecerá un icono (un símbolo de monitor). Al tocar o hacer clic en esta opción, se abre la ubicación adecuada en la IU clásica.

  Por ejemplo, los vínculos de **Sites** a **siteadmin**:

  ![syui-01](assets/syui-01.png)

* **URL**

  Se puede acceder a la IU clásica mediante la dirección URL de la pantalla de bienvenida en `welcome.html`. Por ejemplo:

  `https://localhost:4502/welcome.html`

  >[!NOTE]
  >
  >Se puede acceder a la interfaz de usuario táctil a través de `sites.html`. Por ejemplo:
  >
  >
  >`https://localhost:4502/sites.html`

### Cambio a la IU clásica al editar una página {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Esta opción para cambiar a la IU clásica no está disponible de forma inmediata, debe configurarse para su instancia.
>
>Consulte [Habilitar el acceso a la IU clásica](/help/sites-administering/enable-classic-ui.md) para obtener más información.

Si está habilitada, **Abrir la IU clásica** está disponible en el cuadro de diálogo **Información de la página**:

![syui-02](assets/syui-02.png)

### Anulaciones de IU del editor {#ui-overrides-for-the-editor}

El sistema puede anular la configuración definida por un usuario o un administrador del sistema si existe la creación de páginas.

* Al crear páginas:

   * Se fuerza el uso del editor clásico al acceder a la página con `cf#` en la dirección URL. Por ejemplo:
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * Se fuerza el uso del editor táctil al usar `/editor.html` en la URL o al usar un dispositivo táctil. Por ejemplo:
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Cualquier forzamiento es temporal y solo es válido para la sesión del explorador

   * Se establece un conjunto de cookies en función de si se utiliza táctil (`editor.html`) o clásico (`cf#`).

* Al abrir páginas a través de `siteadmin`, se comprueba la existencia de lo siguiente:

   * La cookie
   * Una preferencia de usuario
   * Si no existe ninguna de estas definiciones, toma como valor predeterminado las definiciones establecidas en la [configuración OSGi](/help/sites-deploying/configuring-osgi.md) del **servicio de modo de interfaz de usuario de creación de WCM** (`AuthoringUIMode`).

>[!NOTE]
>
>Si [un usuario ya ha definido una preferencia para la creación de páginas](#settingthedefaultauthoringuiforyouraccount), esto no se anulará al cambiar la propiedad OSGi.

>[!CAUTION]
>
>Debido al uso de cookies, como ya se ha descrito, no se recomienda:
>
>* Editar manualmente la URL: una URL no estándar podría dar como resultado una situación desconocida y falta de funcionalidad.
>* Haga que ambos editores abran al mismo tiempo, por ejemplo, en ventanas independientes.
