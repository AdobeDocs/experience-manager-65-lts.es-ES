---
title: Configuración de AEM Forms para enviar datos a un proceso de AEM Forms en JEE
description: Integrar formularios adaptables con AEM Forms en procesos JEE para procesar datos de formulario.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 39%

---

# Configurar AEM Forms para enviar datos de formulario a un formulario de AEM en un proceso JEE{#configuring-aem-forms-to-submit-form-data-to-an-aem-forms-on-jee-process}

Los formularios adaptables admiten el envío de datos a AEM Forms en un proceso JEE para un procesamiento posterior. Permite almacenar en déclencheur un proceso de AEM Forms en JEE con los datos disponibles en el formulario enviado. Realice los siguientes pasos para permitir que la instancia de AEM Forms envíe un formulario adaptable a AEM Forms durante el proceso JEE:

## Configuración del servidor de AEM Forms {#configure-your-aem-forms-server}

Realice los siguientes pasos para permitir que el servidor de AEM Forms envíe datos a AEM Forms en un servidor JEE:

1. Vaya a la página de configuración de la web de AEM en https://[*host*]:[*port*]/system/console/configMgr.

1. Busque y haga clic en el componente **Configurar el SDK de cliente de LiveCycle de Adobe**.
1. Haga clic para editar la URL del servidor de configuración, el nombre de usuario y la contraseña para AEM Forms en el servidor JEE.
1. Revise la configuración y haga clic en **Guardar**.

![Configurar el SDK de cliente de LiveCycle de Adobe](assets/clientsdkconfiguration.jpg)

## Asignar datos a campos de proceso {#map-data-with-process-fields}

Después de configurar AEM Forms, asigne los datos XML y los archivos adjuntos del formulario enviado a los campos del proceso de AEM Forms en JEE. Haga lo siguiente:

1. En la consola de configuración web de AEM, haga clic para editar la configuración de la **Guía de localización e invocación de procesos de LiveCycle**.
1. Especifique los siguientes parámetros:

   * **Nombre del parámetro xml de datos** (obligatorio): especifique el archivo de propiedad XML del proceso de AEM Forms en JEE que debe procesar los datos enviados. El valor predeterminado es **dataxml**.

   * **Nombre del parámetro de archivos adjuntos** (opcional): especifique la lista de objetos de documento que debe procesar el proceso de AEM Forms en JEE. El valor predeterminado es **fileAttachmentsList**.

1. Revise la configuración y haga clic en **Guardar**.

![Guía de localización e invocación de procesos de LiveCycle](assets/test3.jpg)

Una vez configurada, la acción Enviar al flujo de trabajo de formularios envía una lista de los procesos de AEM Forms en el servidor JEE que contienen el parámetro xml de datos especificado.
