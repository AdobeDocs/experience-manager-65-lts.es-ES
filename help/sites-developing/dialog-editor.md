---
title: Editor de diálogos
description: El editor de diálogos proporciona una interfaz gráfica para crear y editar fácilmente cuadros de diálogo y andamios.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 48cdca14c4e993281ed8c0a4a364aebe7a4611ad
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Editor de diálogos{#dialog-editor}

El editor de diálogos proporciona una interfaz gráfica para crear y editar fácilmente cuadros de diálogo y andamios.

Para ver cómo funciona, vaya a CRXDE Lite, abra el árbol del explorador en `/libs/foundation/components/chart` y haga doble clic en el nodo `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

El nodo de diálogo se abre en **editor de diálogos**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Resumen de interfaz de usuario {#user-interface-overview}

La interfaz del editor de diálogos se compone de cuatro paneles:

* La **paleta**, en la esquina superior izquierda. Este panel contiene los widgets disponibles para crear un cuadro de diálogo, como paneles de pestañas, campos de texto, listas de selección y botones. Puede expandir las diferentes categorías dentro de la paleta haciendo clic en la barra divisoria deseada.
* El panel **structure**, en la esquina inferior izquierda. Este panel muestra la estructura jerárquica de nodos que conforman la definición del cuadro de diálogo. Puede ver la misma estructura expandiendo el nodo de diálogo en CRXDE Lite o en el Explorador de contenido de CRX.
* El panel **render**, en el centro de la ventana. Este panel muestra cómo se representa la definición de cuadro de diálogo definida en el panel de estructura como un cuadro de diálogo real.
* El panel **propiedades**. Este panel muestra las propiedades del nodo resaltado en el panel de estructura.

### Uso del Editor de diálogos {#using-the-dialog-editor}

Para crear un cuadro de diálogo, el usuario arrastra y suelta los elementos desde la paleta hasta el panel de estructura y los coloca en su posición dentro de la jerarquía de definición del cuadro de diálogo.

Una vez completada la estructura deseada, el usuario hace clic en **Guardar**, en la parte superior del panel de procesamiento.

>[!CAUTION]
>
>El editor de diálogos sirve para crear diálogos simples. Es posible que no pueda editar definiciones de cuadros de diálogo más complejas. En los casos en los que el editor de diálogos no permite la edición de una estructura de diálogo, la definición del diálogo debe crearse, editarse o ambos manualmente. Para ello, edite directamente la estructura del nodo con CRXDE Lite o el Explorador de contenido de CRX, por ejemplo.

### Creación de un nuevo cuadro de diálogo {#creating-a-new-dialog}

Para crear un cuadro de diálogo, seleccione el componente requerido, haga clic en **Crear...** y luego en **Crear cuadro de diálogo...**.

Escriba los detalles necesarios y haga clic en **Guardar todo**. Ahora puede hacer doble clic en el cuadro de diálogo para que se abra con el editor.

### Uso del Editor de cuadros de diálogo para andamios {#using-the-dialog-editor-for-scaffolds}

Un andamio es una página especial que contiene un formulario que se puede rellenar y enviar en un solo paso. Esto permite crear rápidamente una página utilizando el contenido introducido.

El formulario que constituye un andamio se define mediante una definición de cuadro de diálogo, como un cuadro de diálogo normal, aunque aparece en la página de andamiaje de un formulario diferente. Dado que las definiciones de cuadros de diálogo se utilizan para definir andamios, estos se pueden diseñar con el editor de cuadros de diálogo. Al utilizar el editor de diálogos de esta manera, el panel de procesamiento sigue mostrando la definición del cuadro de diálogo en forma de cuadro de diálogo, no como un andamio.
