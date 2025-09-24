---
title: Configurar la página de redireccionamiento
description: Después de rellenar un formulario adaptable, los usuarios pueden ser redirigidos a una página web que los autores del formulario pueden configurar mientras lo crean..
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: dba191d6-4fe9-40e7-a995-00f0c3fd335d
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 92%

---

# Configurar la página de redireccionamiento{#configuring-redirect-page}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-redirect-page.html?lang=es).

Los autores de formularios pueden configurar una página para cada formulario, a la cual se redirigirá a los usuarios una vez enviado.

1. En el modo de edición, seleccione un componente y, a continuación, pulse ![field-level](assets/field-level.png) > **Contenedor de formulario adaptable** y haga clic en ![cmppr](assets/cmppr.png).

1. En la barra lateral, haga clic en **Envío**.

1. Proporcione la URL de la página de redirección en la sección Presentación de la página de agradecimiento.
1. De forma opcional, en Acción de envío, puede configurar el parámetro que se pasará a la página de redireccionamiento para la acción Enviar a extremo REST.

![Configuración de la página de redireccionamiento](assets/thank-you-setting-1.png)

Configuración de la página de redireccionamiento

Los autores de formularios pueden utilizar los siguientes parámetros, los cuales se pasan a la página de agradecimiento. Los parámetros `status` y `owner` se aprueban para todas las acciones de envío disponibles. Además de estos dos parámetros, se aprueban algunos parámetros adicionales para las siguientes acciones de envío:

* **Acción Almacenar contenido** (obsoleto) `contentPath`: se aprueba la ruta del nodo en el repositorio donde se almacenan los datos enviados.

* **Acción Almacenar PDF** (obsoleto): `contentPath`de los datos enviados y la ruta al nodo que almacena el archivo PDF en el repositorio, se aprueba 

* **Enviar al flujo de trabajo de Forms**: se aprueban los parámetros de salida devueltos por el flujo de trabajo de Forms.

* **Enviar a extremo REST**: se aprueban los parámetros agregados para la asignación de campos en uso a parámetros. Los parámetros `status` y `owner` no se aprueban en esta acción de envío. Para obtener más información, consulte [Configurar la acción Enviar al punto final REST](../../forms/using/configuring-submit-actions.md).
