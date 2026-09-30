---
title: Uso del editor de texto enriquecido para crear contenido
description: Uso del editor de texto enriquecido para crear contenido en Adobe Experience Manager 6.5 LTS.
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
exl-id: 01c2a67a-7168-4362-ad7d-f4990ea43ed8
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
source-wordcount: '295'
ht-degree: 32%
---
# Uso del editor de texto enriquecido para crear contenido {#use-rich-text-editor-to-author-content}

El editor de texto enriquecido (RTE) es un bloque de creación básico para insertar contenido de texto en AEM. Constituye la base de diversos componentes, entre ellos, los siguientes:

* [Texto](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/wcm-components/text)
* [Tabla](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/wcm-components/text#table)

## Edición in situ {#in-place-editing}

Si se selecciona un componente basado en texto con un solo clic, se mostrará [la barra de herramientas de componentes](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste), como con cualquier otro componente.

![screen_shot_2018-03-21at163054](assets/screen_shot_2018-03-21at163054.png)

Si vuelve a pulsar o hacer clic en el componente, o si inicialmente lo selecciona con un doble clic lento, se abre la edición in-situ, que tiene su propia barra de herramientas. Aquí puede editar el contenido y realizar cambios básicos de formato.

![screen_shot_2018-03-21at163214](assets/screen_shot_2018-03-21at163214.png)

Esta barra de herramientas ofrece las opciones siguientes:

* **Formato**: Esto le permite establecer negrita, cursiva y subrayado.
* **Listas**: con esta opción puede crear listas con viñetas o números, o establecer la sangría.
* **Hipervínculo**
* **Desvincular**
* **Pantalla completa**
* **Cerrar**
* **Guardar**

## Edición en pantalla completa {#full-screen-editing}

Para los componentes basados en texto, al pulsar el modo de pantalla completa en la barra de herramientas ![Modo de edición de pantalla completa](do-not-localize/screen_shot_2018-03-21at163236.png) se abre el editor de texto enriquecido y se oculta el resto del contenido de la página.

El modo de pantalla completa muestra todas las opciones configuradas que puede utilizar para la creación. La disponibilidad es opciones [depende de la configuración](/help/sites-administering/rich-text-editor.md).

![screen_shot_2018-03-21at163248](assets/screen_shot_2018-03-21at163248.png)

Entre las opciones adicionales del editor de texto enriquecido están:

* **Anclaje**: crea en el texto un anclaje al que posteriormente puede hacer referencia o emplear como vínculo.
* **Alinear texto a la izquierda**
* **Centrar texto**
* **Alinear texto a la derecha**

Cierre el modo de pantalla completa haciendo clic en el icono de minimizar.

![screen_shot_2018-03-21at163323](assets/screen_shot_2018-03-21at163323.png)

>[!NOTE]
>
>Copiar listas anidadas de Microsoft Word en el editor de texto enriquecido puede dar resultados incoherentes y necesitar un ajuste manual después de pegar el texto en el editor de texto enriquecido.
