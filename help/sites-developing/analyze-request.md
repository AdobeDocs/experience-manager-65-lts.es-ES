---
title: Script de análisis de solicitud
description: El script de análisis de solicitud se realiza para facilitar el análisis de los archivos access.log y producir un informe legible para un procesamiento posterior
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 9fe575ad-1e8d-460f-a933-ddc2e927a6e8
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 6%
---
# Script de análisis de solicitud{#request-analysis-script}

## Descargar {#download}

Este script se crea para facilitar el análisis de los archivos de `access.log` y generar un informe legible para su procesamiento posterior.

[Obtener archivo](assets/analyse-access.sh)

## Descripción {#description}

Este script se crea para facilitar el análisis de los archivos de `access.log` y generar un informe legible para su procesamiento posterior.

Produce el número de solicitudes generales, GET frente a POST, la distribución de solicitudes a lo largo del tiempo y más.

El resultado está en sintaxis Markdown, por lo tanto, será más fácil convertirlo a PDF con herramientas como pandoc o mostrarlo en un navegador con complementos como Markdown viewer.

Puede analizar una ruta personalizada proporcionada en la línea de comandos.

Tomar del comentario dentro del archivo que le indica cómo ejecutarlo:

Analice CQ `access.log` extrapolando información diversa y generando un resultado de Markdown en `stdout`.

## Uso {#usage}

`./analyse-access.sh access.log.2013-&ast;`

puede proporcionar rutas personalizadas adicionales para analizar en la línea de comandos

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

se puede guardar la salida mediante una tubería simple

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
