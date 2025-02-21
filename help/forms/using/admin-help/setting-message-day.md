---
title: Configurar el mensaje del día
description: El mensaje del día permite configurar un mensaje para que se muestre en la página de bienvenida de la interfaz de usuario de Workspace.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# Configurar el mensaje del día {#setting-the-message-of-the-day}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede configurar un mensaje para que se muestre en la página de bienvenida de la interfaz de usuario de Workspace.

Si es necesario, puede utilizar las etiquetas de HTML compatibles con Adobe Flash® Player para dar formato al aspecto del texto:

* &lt;a> Etiqueta de anclaje
* &lt;b> Etiqueta en negrita
* &lt;br> Etiqueta de interrupción
* &lt;font> Etiqueta de fuente
* Etiqueta de imagen &lt;img>
* &lt;i> Etiqueta en cursiva
* &lt;li> Etiqueta de elemento de lista
* &lt;p> Etiqueta de párrafo
* &lt;span> Etiqueta de alcance
* Etiqueta de formato de texto &lt;textformat>
* &lt;u> Etiqueta de subrayado

Para obtener más información acerca de las etiquetas admitidas, vea la definición de la propiedad `htmlText` para la clase TextField en [Referencia del lenguaje Flex](https://flex.apache.org/).

## Establecer el mensaje del día {#set-the-message-of-the-day}

1. En la consola de administración, haga clic en Servicios > Workspace > Mensaje del día.
1. En el cuadro Mensaje del día, proporcione el texto que se mostrará en la pantalla de bienvenida.
1. Haga clic en Guardar.

>[!NOTE]
>
>Flex Workspace ya no se utiliza para la versión de formularios AEM.
