---
title: Configurar la salida del formulario
description: Obtenga información sobre cómo configurar la salida del formulario. Para configurar la salida del formulario y habilitar la función, utilice secuencias de comandos personalizadas antes del envío del formulario.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2823d38e-f544-408e-9437-3d0fc622dc34
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 8%

---

# Configurar la salida del formulario{#configuring-form-output}

## Especifique el tipo de salida de HTML que se devuelve al explorador web {#specify-the-type-of-html-output-returned-to-the-web-browser}

1. En la consola de administración, haga clic en Servicios > Formularios.
1. En Salida de formulario, en la lista Tipo de salida, seleccione una de las siguientes opciones:

   **HTML completo:** Para procesar el formulario con etiquetas HTML completas (una página HTML completa). Este valor es el predeterminado.

   **Cuerpo del formulario:** Para procesar el formulario con `<BODY>` etiquetas (no es una página de HTML completa).

1. Haga clic en Guardar.

## Especifique la ubicación donde se renderiza el contenido de PDF {#specify-the-location-where-pdf-content-is-rendered}

1. En Salida de formulario, en la lista Procesar en, seleccione una de las siguientes opciones:

   **Cliente:** para procesar PDF forms en Adobe Acrobat o Adobe Reader. El procesamiento del lado del cliente mejora el rendimiento de los formularios de AEM y se aplica solo a la transformación del formulario PDF.

   **Servidor:** para procesar PDF forms en el servidor de aplicaciones.

   **Automático:** Para procesar el formulario de PDF en la ubicación especificada por el valor de configuración `dynamicRender` del archivo XDP. Este valor es el predeterminado.

1. Haga clic en Guardar.

## Configurar la invocación de scripts personalizados antes del envío del formulario {#configuring-invocation-of-custom-scripts-before-form-submit}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Siga los siguientes pasos para habilitar la función:

1. Inicie sesión en la consola de administración.
1. Vaya a **Servicios** > **formularios**.
1. Especifique el Tipo de salida como Cuerpo del formulario.
1. Guarde la configuración.
1. Declare una variable de JavaScript, __CUSTOM_SCRIPTS_VERSION, en la sección del encabezado del código de HTML y establezca su valor en 1.

   >[!NOTE]
   >
   >*Para deshabilitar esta característica, puede quitar la variable JavaScript o establecer su valor en 0.*
