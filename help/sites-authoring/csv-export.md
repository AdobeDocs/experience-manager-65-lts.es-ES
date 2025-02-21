---
title: Exportar a CSV
description: Exportar información sobre sus páginas a un archivo CSV en su sistema local
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 74%

---

# Exportar a CSV  {#export-to-csv}

**Al crear un informe de CSV** puede exportar información sobre las páginas a un archivo CSV en el sistema local.

* El archivo descargado se llama `export.csv`.
* El contenido depende de las propiedades que seleccione.
* Puede definir la ruta de la exportación, así como la profundidad.

>[!NOTE]
>
>Se utiliza la función de descarga (y el destino predeterminado) de su navegador.

El asistente **Crear exportación de CSV** le permite seleccionar:

* Propiedades para exportar
   * Metadatos
      * Nombre
      * Modificado
      * Publicado
      * Plantilla
      * Flujo de trabajo
   * Traducción
      * Traducido
   * Análisis
      * Vistas de la página
      * Visitantes únicos
      * Tiempo empleado en la página
* Profundidad
   * Ruta principal
   * Solo elementos secundarios directos
   * Niveles adicionales de tareas secundarias
   * Niveles

El archivo `export.csv` resultante se puede abrir en Excel o en cualquier otra aplicación compatible.

![etc-01](assets/etc-01.png)

La opción Crear **informe CSV** está disponible al examinar la consola **Sitios** (en la vista de lista): es una opción del menú desplegable **Crear**:

![etc-02](assets/etc-02.png)

Para crear una exportación de CSV: 

1. Abra la consola **Sites** y vaya a la ubicación requerida si es necesario.
1. Para abrir el asistente, en la barra de herramientas seleccione **Crear** y, a continuación, **Informe de CSV**:

   ![etc-03](assets/etc-03.png)

1. Seleccione las propiedades necesarias para exportar.
1. Seleccione **Crear**.
