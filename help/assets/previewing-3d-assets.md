---
title: Vista previa de activos 3D
description: Obtenga información sobre cómo previsualizar recursos 3D en Experience Manager.
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 9%

---

# Vista previa de recursos 3D en Adobe Experience Manager {#previewing-3d-assets-aem}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=es) |
| AEM 6.5 | Este artículo |

Experience Manager admite la carga, el envío y la previsualización interactiva de recursos 3D como parte del proceso de creación.

El visor 3D interactivo está disponible en la página de detalles de recursos de Experience Manager. El visualizador incluye, entre otras cosas, una colección de controles de cámara interactivos que le permiten orbitar, ampliar o reducir y recorrer el recurso 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formatos compatibles con la vista previa 3D en Experience Manager {#supported-3d-previewing-assets}

La vista previa 3D interactiva admite los siguientes formatos de archivo:

| Extensión de archivo 3D | Formato del archivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmisión binaria GL | model/gltf-binary | |
| GLTF | Formato de transmisión GL | model/gltf+json | Ver **Nota** a continuación. |
| OBJ | Archivo de objeto 3D WaveFront | application/x-tgif | |
| STL | Estereolitografía | application/vnd.ms-pki.stl | |
| DN | Adobe Dimension | model/x-adobe-dn | Compatibilidad solo con la ingesta; vista previa no disponible. |
| USDZ | Universal Scene Description Archivo zip | model/vnd.usdz+zip | Compatibilidad solo con la ingesta; vista previa no disponible. |

>[!NOTE]
>
>Si los materiales no se representan en la vista previa de un modelo gLTF, asegúrese de que se les asignen nombres correctamente y que se encuentren en una carpeta `textures` en la misma carpeta raíz que el modelo, de forma similar a la siguiente:

    Recurso (carpeta)
    model.gltf
    model.bin
    textures (carpeta)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Consideraciones de rendimiento al previsualizar recursos 3D en Experience Manager{#performance-3d-previewing-assets}

El tiempo que se tarda en abrir un recurso 3D en la página de vista de detalles del recurso depende de varios factores, como el ancho de banda, la complejidad de la imagen y las latencias al servidor.

Además, las capacidades del equipo cliente, como una estación de trabajo, un portátil o un dispositivo táctil móvil, también son importantes a la hora de manipular la cámara de forma interactiva. Un sistema razonablemente potente con buenas capacidades gráficas puede hacer que la experiencia de visualización 3D interactiva sea más fluida y favorable.

**Para obtener una vista previa de recursos 3D en Experience Manager:**

1. Asegúrese de haber cargado recursos 3D en Experience Manager.
Ver [Formatos compatibles para vista previa 3D](#supported-3d-previewing-assets) y [Cargar Assets](/help/assets/manage-assets.md#uploading-assets).
1. En Experience Manager, en la página **[!UICONTROL Navegación]**, seleccione **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.

   ![Página de navegación](/help/assets/assets-dm/navigation-assets.png)

1. Cerca de la esquina superior derecha de la página, en la lista desplegable Ver, seleccione **[!UICONTROL Vista de tarjeta]** y, a continuación, desplácese hasta un recurso 3D que desee previsualizar.

   ![Selección de tarjeta 3D](/help/assets/assets-dm/3d-card-select.png)
   _En la vista de tarjeta, seleccione la tarjeta del recurso 3D que desea previsualizar._

1. Seleccione la tarjeta del recurso 3D.

   ![Vista previa 3D interactiva](/help/assets/assets-dm/3d-preview.png)
   _Vista previa interactiva de un recurso 3D en la página de vista de detalles del recurso._
1. En la página de vista de detalles del recurso para el recurso 3D, realice una de las siguientes acciones:

   | Ver | Descripción | Acción del ratón | Acción de pantalla táctil |
   | --- | --- | --- | --- |
   | **Gira tu cámara** | Haga girar la vista alrededor de la escena 3D y de los objetos. | Haga clic con el botón izquierdo + arrastre. | Presione con un solo dedo + arrastre. |
   | **Panorámica tu cámara** | Mueva la vista de forma panorámica a la izquierda, a la derecha, arriba o abajo. | Haga clic con el botón derecho y arrastre. | Presione con dos dedos + arrastre. |
   | **Haz zoom en tu cámara** | Desplazarse dentro y fuera de las áreas de la escena 3D. | Rueda de desplazamiento. | Pellizco de dos dedos. |
   | **Vuelva a centrar su cámara** | Vuelva a centrar la cámara en un punto de un objeto de la escena 3D. | Haga doble clic en. | Haga doble clic en. |
   | **Restablecer** | Cerca de la esquina inferior derecha de la página, seleccione el icono Restablecer para restaurar el punto de destino de vista en el centro del recurso 3D. El restablecimiento también acerca o aleja la cámara para mostrar el recurso en su totalidad y a un tamaño de visualización razonable. |   |   |
   | **Modo de pantalla completa** | Para acceder al modo de pantalla completa, en la esquina inferior derecha de la página, seleccione el icono Pantalla completa. |   |   |

1. Cuando termine, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Cerrar]**.
