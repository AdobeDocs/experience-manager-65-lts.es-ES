---
title: Configuración de componentes en el modo Diseño
description: Cuando se instala una instancia de AEM de forma predeterminada, una selección de componentes está disponible inmediatamente en la barra de tareas. Además de estos, también hay otros componentes disponibles. Puede utilizar el modo Diseño para habilitar o deshabilitar estos componentes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Configuración de componentes en el modo Diseño{#configuring-components-in-design-mode}

Cuando se instala una instancia de AEM de forma predeterminada, una selección de componentes está disponible inmediatamente en la barra de tareas.

Además de estos, también hay otros componentes disponibles. Puede usar el modo Diseño para [habilitar o deshabilitar estos componentes](#enabledisablecomponentsusingdesignmode). Cuando esté habilitado y ubicado en su página, puede usar el modo de diseño para [configurar aspectos del diseño del componente](#configuringcomponentsusingdesignmode) al editar los parámetros de atributo.

>[!NOTE]
>
>Se debe tener cuidado al editar estos componentes. La configuración de diseño suele ser parte integral del diseño de todo el sitio web, por lo que solo debe cambiarla alguien con los privilegios (y experiencia) adecuados, a menudo un administrador o desarrollador. Consulte [Desarrollar componentes](/help/sites-developing/components.md) para obtener más información.

En realidad, esto implica agregar o quitar los componentes permitidos en el sistema de párrafos de la página. El sistema de párrafos (`parsys`) es un componente compuesto que contiene todos los demás componentes de párrafo. El sistema de párrafos permite a los autores añadir componentes de diferentes tipos a una página, ya que contiene todos los demás componentes de párrafo. Cada tipo de párrafo se representa como un componente.

Por ejemplo, el contenido de una página de producto puede contener un sistema de párrafos que contenga lo siguiente:

* Una imagen del producto (en forma de imagen o de párrafo de imagen de texto)
* La descripción del producto (como párrafo de texto)
* Una tabla con datos técnicos (como un párrafo de tabla)
* Un formulario que los usuarios rellenan (al comenzar los formularios, el elemento y el párrafo final de los formularios)

>[!NOTE]
>
>Consulte [Desarrollar componentes](/help/sites-developing/components.md#paragraphsystem) y [Directrices para usar plantillas y componentes](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) para obtener más información sobre `parsys`.

## Habilitar/deshabilitar componentes {#enable-disable-components}

En el modo Diseño, la barra de tareas se minimiza y tiene la posibilidad de configurar los componentes accesibles para la creación:

1. Para entrar en el modo Diseño, abra una página para editarla y utilice el icono de Sidekick:

   ![Modo de diseño](do-not-localize/chlimage_1.png)

1. Haga clic en **Editar** en el sistema de párrafos (**Diseño de par**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. Se abrirá un cuadro de diálogo que enumera los grupos de componentes que se muestran en Sidekick junto con los componentes individuales que contienen.

   Seleccione según sea necesario para agregar o quitar los componentes que deben estar disponibles en la barra de tareas.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. Sidekick se minimiza en el modo Diseño. Al hacer clic en la flecha, puede maximizar la Sidekick y volver al modo de edición:

   ![Sidekick minimizado](do-not-localize/sidekick-collapsed.png)

## Configuración del diseño de un componente {#configuring-the-design-of-a-component}

En el modo Diseño, también puede configurar atributos para los componentes individuales. Cada componente tiene sus propios parámetros. El siguiente ejemplo muestra el componente **Image**:

1. Para entrar en el modo Diseño, abra una página para editarla y utilice el icono de Sidekick:

   ![Modo de diseño - Sidekick](do-not-localize/chlimage_1-1.png)

1. Puede configurar el diseño de los componentes.

   Por ejemplo, si hace clic en **Editar** en el componente Imagen (**Diseño de la imagen**), puede configurar los parámetros específicos del componente:

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Haga clic en **Aceptar** para guardar los cambios.

1. Sidekick se minimiza en el modo Diseño. Al hacer clic en la flecha, puede maximizar la Sidekick y volver al modo de edición:

   ![Sidekick minimizado](do-not-localize/sidekick-collapsed-1.png)
