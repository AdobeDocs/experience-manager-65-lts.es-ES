---
title: Adición de fuentes para la representación gráfica
description: AEM permite generar gráficos que incorporen texto tomado dinámicamente del contenido
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 5ceaa9f0-aba1-40a3-97ef-f5ade0c2a54a
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 5%
---
# Adición de fuentes para la representación gráfica{#adding-fonts-for-graphic-rendering}

AEM permite generar gráficos que incorporen texto tomado dinámicamente del contenido.

Para ello, también puede cargar y utilizar sus propias fuentes.

Actualmente todas las implementaciones de la plataforma Java admiten [TrueType](https://en.wikipedia.org/wiki/Truetype) fuentes.

1. Abra CRXDE Lite y vaya a la carpeta de la aplicación del proyecto:

   `/apps/<your-project>/`

1. En `/apps/<your-project>/`, cree un nodo:

   * **Nombre**: `fonts`
   * **Tipo**: `sling:Folder`

   Guarde todos los cambios.

1. Copie los archivos de fuente en esta carpeta; por ejemplo, mediante WebDAV.

   >[!NOTE]
   >
   >Los archivos de fuente del repositorio deben tener el sufijo `*.ttf` o `*.TTF`.

1. Actualice la [configuración de OSGi](/help/sites-deploying/configuring-osgi.md) de [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md). Agregue la ruta a la carpeta de fuentes; es decir, `/apps/<your-project>/fonts`.

1. Vuelva a CRXDE Lite. Ahora debería ver un nodo `.fontlist` en la carpeta que contiene el nombre de las fuentes importadas.

   Estas fuentes ya están listas para utilizarse en la API de Java.

Para obtener información detallada sobre cómo usar las fuentes con la API de Java, consulte la [documentación de la clase Font de la API de Java](https://download.oracle.com/javase/6/docs/api/java/awt/Font.html).
