---
title: Oriente su Adobe Campaign
description: Puede crear experiencias segmentadas para Adobe Campaign después de configurar la segmentación.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Developer
exl-id: ce6ebfff-3a1d-4c9f-aa50-23d1c3afc852
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: eb3ad9f8-54a2-45f3-abb1-d3976415a718
    internal-label: Personalization
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%
---

# Segmentación de Adobe Campaign{#targeting-your-adobe-campaign}

Para dirigirse al boletín informativo de Adobe Campaign, primero debe configurar la segmentación, que solo está disponible en la IU clásica (para el contexto de cliente). Después, puede crear experiencias segmentadas para Adobe Campaign. Ambos se describen en esta sección.

## Configuración de la segmentación en AEM {#setting-up-segmentation-in-aem}

Para configurar la segmentación, debe utilizar la IU clásica para configurar los segmentos. Los pasos restantes se pueden realizar en la interfaz de usuario estándar.

La configuración de la segmentación incluye la creación de segmentos, una marca, una campaña y experiencias.

>[!NOTE]
>
>El ID del segmento debe asignarse al del lado de Adobe Campaign.

### Creación de segmentos {#creating-segments}

Para crear segmentos:

1. Abra la [consola de segmentación](http://localhost:4502/miscadmin#/etc/segmentation) en **&lt;host>:&lt;port>/miscadmin#/etc/segmentation**.
1. Cree una página, escriba un título (por ejemplo, **Segmentos de CA**) y seleccione la plantilla **Segmento (Adobe Campaign)**.
1. Seleccione la página creada en la vista de árbol de la izquierda.
1. Cree un segmento, por ejemplo, dirigido a usuarios hombres, creando una página en el segmento que ha creado llamada Hombre y seleccione la plantilla **Segmento (Adobe Campaign)**.
1. Abra la página de segmentos creada y arrastre y suelte un **ID de segmento** de la barra de tareas en la página.
1. Haga doble clic en el rasgo, introduzca el ID que representa, en este caso, el segmento masculino definido en Adobe Campaign (por ejemplo, **MALE**) y haga clic en **Aceptar**. El siguiente mensaje debería aparecer: *`targetData.segmentCode == "MALE"`*
1. Repita los pasos para otro segmento, por ejemplo, un segmento dirigido a mujeres.

### Creación de una marca {#creating-a-brand}

Para crear una marca:

1. En **Sites**, vaya a la carpeta **Campaigns** (por ejemplo, en We.Retail).
1. Haga clic en **Crear página** e introduzca un título para la página como, por ejemplo, Marca We.Retail y seleccione la plantilla **Marca**.

### Creación de una campaña {#creating-a-campaign}

Para crear una campaña:

1. Abra la página **Marca** que creó.
1. Haga clic en **Crear página** e introduzca un título para su página como, por ejemplo, We.Retail Campaign, seleccione la plantilla **Campaign** y haga clic en **Crear**.

### Creación de experiencias {#creating-experiences}

Para crear experiencias para segmentos:

1. Abra la página **Campaign** que creó.
1. Cree experiencias para sus segmentos haciendo clic en **Crear página** e introduciendo un título para su página como, por ejemplo, Hombre mientras crea una experiencia para el segmento Hombre y seleccione la plantilla **Experiencia**.
1. Abra la página de experiencia creada.
1. Haz clic en **Editar** y luego, debajo de Segmentos, haz clic en **Agregar elemento**.
1. Introduzca la ruta al segmento masculino, por ejemplo, **/etc/segmentation/ac-segments/male**, y haga clic en **Aceptar**. Debería aparecer el siguiente mensaje: *La experiencia está dirigida a: Hombre*
1. Repita los pasos anteriores para crear una experiencia para todos los segmentos, por ejemplo, el segmento femenino.
