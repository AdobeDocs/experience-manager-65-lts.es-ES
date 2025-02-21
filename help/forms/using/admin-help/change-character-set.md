---
title: Cambiar el conjunto de caracteres
description: Puede especificar el conjunto de caracteres utilizado para codificar la secuencia de salida. Aprenda a cambiar el conjunto de caracteres.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 6%

---

# Cambiar el conjunto de caracteres {#change-the-character-set}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede especificar el conjunto de caracteres utilizado para codificar la secuencia de salida.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > resultado]**.
1. En Internacionalización, en la lista Conjunto de caracteres, seleccione un conjunto de caracteres. Esta configuración depende de `TransformationFormat` y `PrintFormat` especificados a través de la API. Para especificar un conjunto de caracteres distinto de los enumerados, seleccione Personalizado y especifique un valor de codificación en el cuadro que se muestra.

   Si `TransformationFormat` es PDF y PDF/A o `PrintFormat` es PCL, PostScript, Zebra label, IPL, DPL, TPCL, GenericColorPCL o GenericPSLevel3, solo se admiten conjuntos de caracteres específicos.

   El conjunto de caracteres debe ser un nombre canónico válido. El valor predeterminado es ISO-8859-1.

1. Haga clic en **[!UICONTROL Guardar]**.
