---
title: Migración de Dynamic Media (modo híbrido) a Dynamic Media (modo S7)
description: Obtenga información sobre cómo migrar la instancia de Dynamic Media (modo híbrido) a Dynamic Media (modo S7)
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
solution: Experience Manager, Experience Manager Assets
exl-id: 7d21d993-f7a3-4c12-aa4d-03057c8f29fc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: ee69dd13-2aba-4eb0-912b-399e82368d73
    internal-label: Scene7 mode
  - id: cf50b0d2-df62-495c-a741-4fa0284ca4fc
    internal-label: Hybrid mode
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%
---
# Acerca del paso de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#about-migrating}

Dynamic Media-Hybrid es una versión anterior de la integración de Dynamic Media con Adobe Experience Manager. La versión híbrida se introdujo por primera vez en Adobe Experience Manager 6.1. Aunque Adobe sigue admitiendo el modo híbrido, no es el modo preferido; Dynamic Media-Scene7 es el modo preferido para usar. El modo híbrido tampoco admite nuevas funciones como recorte inteligente e imágenes panorámicas, mientras que Dynamic Media-Scene7 sí las admite.

Otras diferencias clave entre Dynamic Media-Hybrid y Dynamic Media-Scene7 son las siguientes:

* Estructura de las direcciones URL.
* Ingesta de vídeos.
* Creación y almacenamiento de representaciones de imágenes.
* Configuración y credenciales de nube (aprovisionamiento).

Hay dos opciones disponibles al pasar de Dynamic Media-Hybrid a Dynamic Media-Scene7. La primera opción es simplemente aprovisionar una nueva instancia de Dynamic Media-Scene7 en Experience Manager. La segunda opción es migrar la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7. Esta opción describe el formulario de tabla siguiente: los pasos y las consideraciones que debe seguir durante el movimiento.

>[!IMPORTANT]
>
>Adobe recomienda no migrar una implementación híbrida de Dynamic Media a Dynamic Media-Scene7 en instancias de producción en directo.

## Opción 1: Aprovisionar una nueva instancia de Dynamic Media-Scene7 en Experience Manager {#provision-new-dms7}

Considere simplemente empezar de cero con una nueva instancia aprovisionada de Dynamic Media-Scene7 en Adobe Experience Manager. Además de la ingesta y el procesamiento de recursos mediante Dynamic Media Cloud Service, es muy recomendable realizar una auditoría Adobe del uso de recursos, flujos de trabajo y componentes. A menudo, puede reemplazar componentes y flujos de trabajo personalizados mediante el uso de funciones más nuevas y listas para usar.

## Opción 2: Migrar la instancia existente de Dynamic Media-Hybrid a Dynamic Media-Scene7 {#process-for-migrating}

| Paso | Tarea | Consideraciones |
|---|---|---|
| 1 | Clonar instancia de autor híbrida de Dynamic Media. | Mantenga la instancia existente de autor híbrido de Dynamic Media para fines de reserva hasta que los pasos restantes de este proceso de migración se completen correctamente. |
| 2 | Inicie la instancia de autor clonada en el modo Dynamic Media-Scene7. |  |
| 3 | En Adobe Experience Manager Cloud Services, configure Dynamic Media con las credenciales de Dynamic Media-Scene7. | Adobe debe aprobar el aprovisionamiento de Dynamic Media-Scene7. Como tal, tiene entornos simultáneos de Dynamic MediaM-Hybrid y Dynamic Media-Scene7 compatibles con Adobe, pero solo por un tiempo limitado. |
| 4 | Cree un paquete de migración para poder ingerir recursos según sea necesario.<br>Elimine los PTIFF locales que se crearon durante la ingesta inicial en Dynamic Media-Hybrid. | Si todos los recursos están disponibles actualmente en la instancia híbrida de Dynamic Media, un clon de que ya los incluye a todos. Por lo tanto, no se necesita ningún paquete. |
| 5 | Ejecute el flujo de trabajo de actualización de recursos para poder sincronizar recursos con Dynamic Media Cloud Service. | Adobe recomienda realizar el flujo de trabajo de actualización por lotes para permitir la compactación. |
| 6 | Migre ajustes preestablecidos de visualizador, imagen y vídeo. |  |
| 7 | Pase por cada recurso al que se hace referencia en la Administración de contenido web y actualice sus direcciones URL asociadas. |  |
| 8 | Migre los flujos de trabajo personalizados que desee que sean compatibles con el nuevo modo Dynamic Media-Scene7 (actualizaciones manuales). |  |
| 9 | Compruebe la carga y configuración de la gestión de contenido web. |  |
| 10 | Después de la verificación, obtenga una aprobación para deshabilitar el autor híbrido de Dynamic Media (mantener como reserva). |  |
| 11 | Elimine la instancia de autor híbrida de Dynamic Media después de aproximadamente un mes de uso correcto de Dynamic Media-Scene7. |  |
