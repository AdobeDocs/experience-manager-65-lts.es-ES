---
title: Texto de marcador de posición en AEM Forms
description: El texto de marcador de posición está diseñado para ayudar al usuario con la introducción de datos cuando el control no tiene valor. Puede ser un valor de muestra o una breve descripción del formato esperado.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%

---

# Texto de marcador de posición en AEM Forms {#placeholder-text-in-aem-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

El texto de marcador de posición representa una palabra o una frase corta. Está diseñado para ayudar al usuario a introducir los datos cuando el control no tiene valor. Un texto de marcador de posición puede ser un valor de muestra o una breve descripción del formato esperado. El texto de marcador de posición se muestra antes de que el usuario introduzca un valor, y se quita cuando el usuario introduce o selecciona un valor.

>[!NOTE]
>
>Si se especifica, el texto del marcador de posición debe tener un valor que no contenga caracteres de nueva línea.

![Componente de fecha con y sin texto de marcador de posición](assets/dat-picker-place-holder-text.png)

**A.** Componente de fecha con texto de marcador de posición **B.** Componente de fecha sin texto de marcador de posición

AEM Forms admite texto de marcador de posición en los campos Cuadro de contraseña, Selector de fecha, Cuadro numérico y Cuadro de texto.\
Los textos de los marcadores de posición no son compatibles con el widget de fecha HTML5 nativo. Para especificar un texto de marcador de posición:

1. Haga clic con el botón derecho en un componente que admita texto de marcador de posición y haga clic en **Editar**. Aparecerá el cuadro de diálogo Editar componente.

1. Abra la pestaña **Título y texto**.
1. Especifique una palabra o una frase corta en el **Cuadro de texto de marcador de posición**. Haga clic en **Aceptar**.

>[!NOTE]
>
>El texto del marcador de posición no es compatible con Microsoft Internet Explorer 9.
