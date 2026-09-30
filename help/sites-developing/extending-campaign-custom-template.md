---
title: Creación de una plantilla de página de AEM personalizada con componentes de formulario de Adobe Campaign
description: Crear una plantilla de página personalizada que utilice componentes de formularios Adobe Campaign Forms
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 59a79455-c108-4f4b-93c1-d8c6f23aec88
index: false
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
source-wordcount: '307'
ht-degree: 9%
---

# Creación de una plantilla de página de AEM personalizada con componentes de formulario de Adobe Campaign{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

En esta página se explica cómo crear una plantilla de página personalizada que use los componentes de [Adobe Campaign Form](/help/sites-authoring/adobe-campaign-components.md) al examinar cómo se implementa la plantilla de Geometrixx-outdoors (`/apps/geometrixx-outdoors/components/page_campaign_profile`), y se proporciona información importante que puede necesitar al crear su propia plantilla personalizada.

>[!CAUTION]
>
>Los componentes de correo electrónico de AEM se han quedado obsoletos. Debido a la naturaleza del correo electrónico, que combina contenido y estilo, los componentes de correo electrónico proporcionados de forma predeterminada por AEM se vuelven de reutilización limitada para los clientes debido a la necesidad de implementar estilos personalizados en los componentes que sean necesarios para los proyectos.
>
>Los componentes de correo electrónico se pueden implementar en el nivel de proyecto y los componentes de correo electrónico de AEM obsoletos ilustran cómo se puede lograr. Sin embargo, no utilice estos componentes obsoletos en proyectos.


Para crear una plantilla de página de AEM personalizada con componentes de formulario Adobe Campaign, asegúrese de que dispone de lo siguiente:

1. **ResourceSuperType correcto**

   Asegúrese de que el componente de página herede de `mcm/campaign/components/profile`.

   Esto es necesario para que los servlets obtengan y guarden información

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Configuración de ClientContext**

   Cuando vea la configuración de clientcontext (`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`), verá la siguiente configuración:

   * ClientContext apunta a `/etc/clientcontext/campaign`
   * También hay un nodo *config* adicional.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   En **head.jsp**, verá las siguientes líneas que utilizan **clientcontext-config** y **cloudservice-hook**:

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   En **body.jsp**, los servicios en la nube se cargan en la parte inferior de la página:

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Propiedades de la página de campaña**

   Para poder seleccionar una plantilla de Adobe Campaign, las propiedades de página se amplían con la pestaña **Campaign**:

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Configuración de plantilla**.

   En la plantilla ( `/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) verá los siguientes valores predeterminados:

   | **acMapping** | mapRecipient (para Adobe Campaign 6.1), profile (para Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | correo |

   ![chlimage_1-204](assets/chlimage_1-204.png)
