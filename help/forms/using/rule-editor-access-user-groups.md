---
title: Conceder acceso al Editor de reglas a determinados grupos de usuarios
description: Conceder acceso restringido al editor de reglas para seleccionar grupos de usuarios.
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 61%

---

# Conceder acceso al Editor de reglas a determinados grupos de usuarios{#grant-rule-editor-access-to-select-user-groups}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. En este artículo se describe un método antiguo para crear Forms adaptable mediante componentes de base. </span>

## Información general {#overview}

Existen diferentes tipos de usuarios con diversas aptitudes que trabajan con formularios adaptables. Aunque es posible que los usuarios expertos tengan los conocimientos necesarios para trabajar con scripts y reglas complejas, puede haber usuarios de nivel básico que únicamente necesiten trabajar con el diseño y las propiedades básicas de los formularios adaptables.

AEM Forms permite limitar el acceso de los usuarios al Editor de reglas en función de su rol o función. En los ajustes del servicio de configuración de Forms adaptable, puede especificar los [grupos de usuarios](/help/sites-administering/security.md) que pueden ver y acceder al editor de reglas.

## Especificar qué grupos de usuarios pueden acceder al Editor de reglas {#specify-user-groups-that-can-access-rule-editor}

1. Inicie sesión en AEM Forms como administrador.
1. En la instancia de autor, haga clic en ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Adobe Experience Manager > Herramientas ![hammer](assets/hammer.png) > Operaciones > Consola web. La consola web se abre en una nueva ventana.

   ![1-2](assets/1-2.png)

1. En la ventana Consola web, busque y haga clic en **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]**. Aparece el cuadro de diálogo **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]**. No cambie ningún valor y haga clic en **Guardar**.

   Crea el archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config en el repositorio de CRX.

1. Inicie sesión en CRXDE como administrador. Abra el archivo /apps/system/config/com.adobe.aemds.guide.service.impl.AdaptiveFormConfigurationServiceImpl.config para editarlo.
1. Utilice la siguiente propiedad para especificar el nombre de un grupo que puede acceder al Editor de reglas (por ejemplo, RuleEditorsUserGroup) y haga clic en **Guardar todo**.

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup"]`

   Para habilitar el acceso para varios grupos, especifique una lista de valores separados por comas:

   `af.ruleeditor.custom.groups=["RuleEditorsUserGroup", "PermittedUserGroup"]`

   ![Crear usuario](assets/create_user_new.png)

   Ahora, cuando un usuario que no forma parte del grupo de usuarios especificado (aquí RuleEditorsUserGroup) pulse un campo, el icono Editar regla ( ![edit-rules1](assets/edit-rules1.png)) no estará disponible para ellos en la barra de herramientas Componentes:

   ![componentstoolbarwithre](assets/componentstoolbarwithre.png)

   Barra de herramientas de componentes visible para un usuario con acceso al Editor de reglas

   ![componentstoolbarwithoutre](assets/componentstoolbarwithoutre.png)

   Barra de herramientas de componentes visible para un usuario sin acceso al Editor de reglas

   Para obtener instrucciones sobre cómo agregar usuarios a grupos, consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).
