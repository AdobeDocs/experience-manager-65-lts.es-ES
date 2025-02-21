---
title: Configurar Microsoft Dynamics 365 para el flujo de trabajo de la hipoteca de vivienda del sitio de referencia We.Finance
description: Aprenda a utilizar los servicios de Microsoft&reg; Dynamics 365 a través de formularios adaptables para el flujo de trabajo de las hipotecas del sitio de referencia de We.Finance.
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 72%

---

# Configurar Microsoft Dynamics 365 para el flujo de trabajo de la hipoteca de vivienda del sitio de referencia We.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Aprenda a utilizar los servicios de Microsoft® Dynamics 365 mediante formularios adaptables en el flujo de trabajo de las hipotecas del sitio de referencia de We.Finance

## Información general {#overview}

Microsoft® Dynamics 365 es un software de gestión de relaciones con el cliente (CRM) y planificación de recursos empresariales (ERP) que proporciona soluciones empresariales para crear y administrar cuentas de cliente, contactos, posibles clientes, oportunidades y casos.

AEM Forms proporciona un servicio en la nube para integrar Dynamics 365 con el módulo [Integración de datos de Forms](/help/forms/using/data-integration.md). Antes de poder usar el tutorial de la solicitud de hipoteca con el escenario de Microsoft® Dynamics, debe configurar Microsoft® Dynamics 365 para utilizarlo con el sitio de referencia de We.Finance.

## Requisitos previos {#prerequisites}

Antes de comenzar a configurar Dynamics 365, asegúrese de que dispone de lo siguiente:

* AEM 6.3 Forms Service Pack 1 y versiones posteriores
* Una cuenta de Microsoft® Dynamics 365
* La aplicación registrada del servicio de Dynamics 365 con Microsoft® Azure Active Directory
* El ID de y el secreto de cliente de la aplicación registrada

## Vinculación del simulador de hipoteca con la página de inicio del sitio {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. En la instancia de autor, vaya a la siguiente página:

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Desplácese hacia abajo hasta el simulador de hipoteca.
1. Resalte el panel de la columna derecha (simulador) y seleccione para mostrar el menú emergente. En el menú emergente, seleccione Configurar. Se abre el cuadro de diálogo Editar contenedor de AEM Forms.

   ![panel_configuración_simulador](assets/calculatorconfigurepanel.png)

1. En el cuadro de diálogo Editar contenedor de AEM Forms, examine la ruta del recurso, seleccione el simulador de hipoteca en la siguiente ruta y seleccione **Confirmar**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selección_ruta_del_recurso](assets/selectassetpath.png)

1. Seleccione **Listo**.
1. Publique la página editada.

   >[!NOTE]
   >
   >El enlace de los campos del simulador con el FDM está preconfigurado a través del paquete del sitio de referencia de We.Finance. Para ver el enlace, puede abrir el formulario en el modo Autor y ver las referencias de enlace de campo.

1. Para crear una entidad personalizada para almacenar el registro de solicitantes de la solicitud de hipoteca, importe el paquete de la solución AEMFormsFSIRefsite_1_0.zip en la instancia de Microsoft® Dynamics:

   1. Descargue el paquete desde la siguiente ubicación:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importe el paquete de la solución en la instancia de Microsoft® Dynamics. En su instancia de Microsoft® Dynamics, vaya a **Configuración** > **Soluciones** y luego seleccione **Importar**.

1. Para configurar los detalles de contacto del usuario utilizados en el sitio de referencia, importe el paquete Sarah Rose Contact.CSV en su instancia de Microsoft® Dynamics:

   1. Descargue el paquete desde la siguiente ubicación:

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importe el paquete en la instancia de Microsoft® Dynamics. En su instancia de Microsoft® Dynamics, vaya a **Ventas** > **Contactos** y luego seleccione **Importar datos**.
