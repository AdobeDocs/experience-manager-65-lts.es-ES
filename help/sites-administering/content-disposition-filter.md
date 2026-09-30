---
title: Filtro de disposición de contenido
description: Aprenda a utilizar el filtro de disposición de contenido para evitar ataques XSS.
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: 997cb6f3-1ef8-409c-acea-157d5b27a6b2
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%
---
# Filtro de disposición de contenido {#content-disposition-filter}

El filtro de disposición de contenido es una función de seguridad contra ataques XSS a archivos SVG.

Una vez instalado, el filtro bloquea el acceso a todos los recursos. Por ejemplo, no puede ver un PDF en línea. En esta sección se describe cómo configurar el filtro según sus necesidades.

## Configurar el filtro de disposición de contenido {#configure-content-disposition-filter}

Puede ver el filtro de disposición de contenido de [Apache Sling en GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Las opciones del Filtro de disposición de contenido proporcionan las siguientes funciones:

* **Rutas de disposición de contenido:** Una lista de rutas donde se aplica el filtro seguida de una lista de tipos MIME que se excluirán en esa ruta. Esta ruta de acceso debe ser una ruta de acceso absoluta y puede contener un comodín (`*`) al final, para que coincida cada ruta de acceso de recurso con el prefijo de ruta de acceso dado. Por ejemplo: `/content/*:image/jpeg,image/svg+xml` aplica el filtro a todos los nodos de `/content?` excepto a las imágenes de JPG y SVG.

* **Rutas de recursos excluidos:** Una lista de recursos excluidos, cada ruta de recursos debe darse como ruta absoluta y completa. No se admiten coincidencias de prefijos ni comodines.

* **Habilitar para todas las rutas de recursos:** Este indicador controla si se habilita este filtro para todas las rutas, excepto para las rutas excluidas definidas por las rutas de recursos excluidas. Si establece este indicador como &quot;true&quot;, se ignoran las rutas de disposición de contenido. Independientemente de la configuración, solo se tratan las rutas de recursos que contienen una propiedad denominada `jcr:data` o `jcr:content/jcr:data`.
