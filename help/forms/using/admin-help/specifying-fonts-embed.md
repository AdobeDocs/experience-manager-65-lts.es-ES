---
title: Especificar fuentes para incrustar
description: Obtenga información sobre cómo especificar fuentes para incrustarlas en un formulario adaptable. Puede especificar qué fuentes están incrustadas o nunca están incrustadas con los formularios que genera el servicio Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c73dced8-7242-465c-85bc-9315a9a08605
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 3%

---

# Especificar fuentes para incrustar {#specifying-fonts-to-embed}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede especificar qué fuentes están siempre incrustadas o nunca incrustadas con los formularios que genera el servicio Forms. La incrustación de fuentes aumenta el tamaño de archivo de los formularios. Incruste fuentes inusuales que los usuarios rara vez tienen en sus sistemas. No incruste fuentes comunes que normalmente tienen instaladas.

>[!NOTE]
>
>Si ha especificado un archivo XCI personalizado para Forms, la opción de fuente incrustada en el archivo XCI anula esta configuración. (Consulte [Configuración de ubicaciones para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > Forms]**.
1. En **[!UICONTROL Configuración de incrustación de fuentes]**, en el cuadro **[!UICONTROL Incrustar siempre fuentes]**, escriba los nombres de las fuentes que desea incrustar con los formularios, separados por comas. Las fuentes especificadas solo están incrustadas en el formulario generado si se utilizan en el formulario. Esta configuración se ignora si la opción de fuente incrustada se ha activado en el archivo XCI enviado al servicio porque, en ese caso, todas las fuentes utilizadas en PDF siempre están incrustadas.
1. En el cuadro **[!UICONTROL No incrustar nunca fuentes]**, escriba los nombres de las fuentes que no desea incrustar con los formularios, separados por comas. Las fuentes especificadas no están incrustadas en PDF, aunque se utilicen en el PDF generado. Esta configuración se ignora si la opción de fuente incrustada se ha desactivado en el archivo XCI enviado al servicio porque, en ese caso, ninguna de las fuentes utilizadas en PDF está incrustada.
1. Haga clic en **[!UICONTROL Guardar]**.
