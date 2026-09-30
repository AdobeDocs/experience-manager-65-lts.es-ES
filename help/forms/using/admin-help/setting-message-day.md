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
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 9581155d-5346-4346-b483-ecb0c51b53e3
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '186'
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
