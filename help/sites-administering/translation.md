---
title: Traducción de contenido para sitios multilingües
description: Aprenda a traducir contenido para sitios multilingües.
contentOwner: Guillaume Carlino
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 74%

---

# Traducción de contenido para sitios multilingües {#translating-content-for-multilingual-sites}

Automatice la traducción del contenido de la página, los activos y el contenido generado por el usuario para crear y mantener sitios web multilingües. Para automatizar los flujos de trabajo de traducción, se integran los proveedores de servicios de traducción con AEM y se crean proyectos para traducir contenido a varios idiomas. AEM admite flujos de trabajo de traducción automática y humana.

* Traducción humana: el contenido se envía a su proveedor de traducción y lo traducen traductores profesionales. Cuando se completa, el contenido traducido se devuelve e importa en AEM. Cuando el proveedor de traducción está integrado con AEM, el contenido se envía automáticamente a AEM y al proveedor de traducción.
* Traducción automática: el servicio de traducción automática traduce inmediatamente su contenido.

La traducción de contenido implica los siguientes pasos:

1. [Conectar AEM con su proveedor de servicios de traducción](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) y [crear configuraciones del marco de trabajo de integración de traducción](/help/sites-administering/tc-tic.md).
1. [Asociar las páginas del maestro de idioma](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) con el servicio de traducción y las configuraciones del marco de trabajo.
1. [Identificar el tipo de contenido](/help/sites-administering/tc-rules.md) para traducir.
1. [Preparar el contenido para su traducción](/help/sites-administering/tc-prep.md) creando el maestro de idioma y las páginas raíz de las copias de idioma.
1. [Crear proyectos de traducción](/help/sites-administering/tc-manage.md) para recopilar el contenido que se va a traducir y para preparar el proceso de traducción.
1. Utilice los proyectos de traducción para [administrar el proceso de traducción de contenido](/help/sites-administering/tc-manage.md).

Si el proveedor de servicios de traducción no proporciona un conector para la integración con AEM, este admite la extracción manual y la reinserción del contenido de traducción en formato XML.

>[!NOTE]
>
>El usuario debe ser miembro del grupo de administradores de proyectos para utilizar las funciones de copia de idioma.

## Prácticas recomendadas   {#best-practices}

La página [Prácticas recomendadas de traducción](/help/sites-administering/tc-bp.md) contiene información importante sobre la implementación.
