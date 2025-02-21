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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

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
