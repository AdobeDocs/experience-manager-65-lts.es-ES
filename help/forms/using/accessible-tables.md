---
title: Crear tablas complejas accesibles en formularios HTML5
description: Aprenda a crear tablas accesibles en formularios HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 76%

---

# Crear tablas complejas accesibles en formularios HTML5 {#create-accessible-complex-tables-in-html-forms}

La implementación predeterminada de tablas en formularios HTML5 utiliza elementos DIV HTML para procesar una tabla. El procesamiento implica el uso de funciones ARIA para satisfacer los requisitos de accesibilidad.

Para evitar problemas de accesibilidad con lectores de pantalla que no admiten completamente las funciones ARIA utilizadas con tablas de datos, los formularios HTML5 proporcionan una representación alternativa para las tablas. Estas tablas se basan en el nuevo formato de tabla introducido en Designer, que también admite:

* Encabezados de fila
* Intervalos de fila

Para utilizar el nuevo formato en formularios HTML5, marque la tabla como compleja. Para marcar la tabla como compleja, agregue la etiqueta `extras` en la fuente XML del subformulario de tabla de la siguiente manera:

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

Las tablas marcadas como *complexTable* siguen la representación nativa del HTML y proporcionan un soporte de accesibilidad mejor para determinados lectores de pantalla.  Para crear un intervalo de filas, seleccione celdas consecutivas de una tabla en la misma columna, haga clic con el botón secundario en la selección y, a continuación, haga clic en **[!UICONTROL Combinar celdas]**.

>[!NOTE]
>
>La creación de un intervalo de filas solo funciona para celdas de la izquierda.

Para marcar una fila como encabezado de fila, seleccione todas las celdas de la fila, haga clic con el botón secundario en la selección y, a continuación, haga clic en **[!UICONTROL Marcar encabezado]**.

Para marcar una celda como encabezado de columna, seleccione cualquier celda de la columna, haga clic con el botón secundario en la selección y, a continuación, haga clic en **[!UICONTROL Marcar encabezado]**.

Limitaciones en el formato nuevo *Tabla accesible*:

* Falta de compatibilidad con campos ampliables si se utiliza rowspan en la tabla
* No se admiten tablas anidadas (tablas dentro de celdas de tabla)
* La compatibilidad con el intervalo de filas está limitada a las filas y celdas de encabezado
* El soporte se limita a tablas regulares
* No se admiten prefijos de datos en tablas con intervalo de tiempo > 1
