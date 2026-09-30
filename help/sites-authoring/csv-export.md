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
role: User,Admin,Developer
exl-id: ccd2ad37-7708-4422-9724-145628f36afc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 74%
---
# Exportar a CSV{#export-to-csv}

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
