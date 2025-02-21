---
title: Análisis del rendimiento de la página
description: Utilice la página Perspectiva de contenido para analizar el rendimiento de la página que está creando
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Integration
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Análisis del rendimiento de la página{#analyzing-page-performance}

Abra la página [Perspectiva de contenido](/help/sites-authoring/content-insights.md) para analizar el rendimiento de la página que está creando. Configure el periodo del informe para centrar el análisis.

## Abrir Analytics y Recommendations para una página {#opening-analytics-and-recommendations-for-a-page}

Utilice el siguiente procedimiento para ver Analytics y Recommendations para una página:

1. Desplácese hasta la página que desee analizar.
1. En la barra de herramientas, haga clic en **Analytics y Recommendations**.

   >[!NOTE]
   >
   >Analytics y Recommendations para una página solo aparecen si configuró AEM para [integrarse con Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md).

   ![captura de pantalla_2019-03-05at115319](assets/screen-shot_2019-03-05at115319.png)

### Modificación del período de informe {#changing-the-reporting-period}

Cambie los siguientes aspectos relacionados con el tiempo de los informes de análisis:

* Período de tiempo para la creación del informe.
* La granularidad de los datos.

Las herramientas para cambiar los aspectos relacionados con el tiempo de los informes aparecen en la parte superior de la página Información del contenido. ![chlimage_1-126](assets/chlimage_1-126.png)

#### Modificación del período de informe {#changing-the-reporting-period-1}

Cambie el periodo de informe de la página Perspectiva de contenido para enfocar el análisis de la actividad de la página a un periodo de tiempo específico. Al cambiar el período de informe, los informes se actualizan automáticamente. El área sombreada en el periodo de tiempo representa el periodo del informe. Las fechas del periodo de tiempo aumentan de izquierda a derecha.

![chlimage_1-127](assets/chlimage_1-127.png)

Para cambiar el período de informe de una página de perspectiva de contenido:

1. Si el periodo no aparece en la parte superior de la página, haga clic en el icono Alternar periodo de tiempo.

   ![Alternar intervalo de tiempo](do-not-localize/chlimage_1-22.png)

1. Para cambiar la fecha de inicio del período de informe, arrastre el círculo que aparece a la izquierda del área sombreada hasta la fecha de inicio deseada.

   Si no puede ver el lado izquierdo del área sombreada, utilice la barra de desplazamiento para mostrarla.

1. Para cambiar la fecha final del período de informe, arrastre el círculo que aparece a la derecha del área sombreada hasta la fecha final deseada.

#### Modificación de la granularidad del periodo de la creación de informes {#changing-the-granularity-of-the-reporting-period}

Cambiar la cantidad de tiempo que cada punto de datos ocupa en un informe. Por ejemplo, cuando se selecciona la granularidad Semana, cada punto de datos en el informe Vistas representa el número de vistas durante una semana.

![screen_shot_2017-11-29at141001](assets/screen_shot_2017-11-29at141001.png)

La granularidad afecta a los informes que trazan los datos en función del tiempo, como los informes Vistas y Minutos de participación media de la página. La granularidad también afecta a la escala del periodo de tiempo.

1. Si no aparece el control de granularidad, haga clic en el icono Alternar granularidad.

   ![chlimage_1-128](assets/chlimage_1-128.png)

1. Haga clic en la granularidad deseada. Una vez seleccionado, el informe se actualiza automáticamente para reflejar la granularidad.

### Asignación de tareas para recomendaciones de SEO {#assigning-tasks-for-seo-recommendations}

Utilice el informe Recomendaciones de SEO para crear tareas que mejoren la visibilidad de la página en los motores de búsqueda. Para cada recomendación del informe que no tenga una marca de verificación, puede crear una tarea que asigne a un usuario para que realice el trabajo necesario.

![chlimage_1-129](assets/chlimage_1-129.png)

El estado de la recomendación SEO indica cuándo se crea la tarea, pero aún no se ha completado.

![chlimage_1-130](assets/chlimage_1-130.png)

Cuando se crea, la tarea aparece en la lista Tareas del usuario. Para obtener información acerca de las tareas, vea [Trabajar con tareas](/help/sites-authoring/task-content.md).

Utilice el siguiente procedimiento para crear una tarea para una recomendación de SEO.

1. Haga clic en el icono de información de la recomendación de SEO.

   ![Icono de información](do-not-localize/chlimage_1-23.png)

1. Haga clic en el icono de triángulo rodeado que aparece junto al icono de información.

   ![chlimage_1-131](assets/chlimage_1-131.png)

1. Rellene los campos de formulario que aparecen y, a continuación, seleccione Crear:

   * Proyecto: seleccione el proyecto en el que desea crear la tarea.
   * Nombre: nombre que identifica la tarea. El nombre predeterminado es el título de la recomendación de SEO.
   * Asignar a: seleccione el usuario al que desea asignar la tarea. Empiece a escribir el nombre del usuario para filtrar la lista.
   * Descripción: Una descripción de la actividad necesaria para completar la tarea. La descripción predeterminada es la información que acompaña a la recomendación de SEO.
   * Prioridad de la tarea: Prioridad de la tarea.
   * Fecha de vencimiento: fecha límite en la que se debe completar la tarea.

   **Nota:** La tarea que se crea también incluye la ruta de acceso a la página a la que se aplica la recomendación SEO.

1. Haga clic en Listo para cerrar el mensaje Creación de la tarea.
