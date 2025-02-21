---
title: ¿Cómo se utiliza hCaptcha&reg; en un Forms de AEM 6.5?
description: Mejore la seguridad sin esfuerzo con el servicio hCaptcha®. Guía paso a paso en el interior
feature: Adaptive Forms, Foundation Components
role: User, Developer
source-git-commit: 1444b0fc0811cbb187d2a4d83b626444e44ef73f
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 27%

---

# Conecte su entorno AEM Forms con Chcaptcha® {#connect-your-forms-environment-with-hcaptcha-service}


<span class="preview">Esta característica no está habilitada de manera predeterminada. Puede escribir desde su dirección oficial a aem-forms-ea@adobe.com para solicitar acceso a la función.</span>

CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

Además de hCaptcha®, AEM Forms 6.5 admite las siguientes soluciones CAPTCHA:

* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [Cloudflare Turnstile](/help/forms/using/integrate-adaptive-forms-turnstile.md)

## Integrar el entorno de AEM Forms con Chcaptcha®

El servicio hCaptcha® protege sus formularios de bots, correos no deseados y abusos automatizados. Plantea un desafío tipo Widget de la casilla de verificación y evalúa la respuesta del usuario para determinar si es un humano o un bot el que interactúa con el formulario. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o actividades maliciosas.

AEM 6.5 Forms adaptable admite hCaptcha&amp;reg. Puede utilizarlo para presentar un desafío de widget de casilla de verificación al enviar el formulario.

<!-- ![hCaptcha&reg;](assets/hCaptcha&reg;-challenge.png)-->


### Requisitos previos para integrar el entorno de AEM Forms con Captcha® {#prerequisite}

Para configurar hCaptcha® con AEM Forms, necesita obtener la clave de sitio [hCaptcha® y la clave secreta](https://docs.hcaptcha.com/switch/#get-your-hcaptcha-sitekey-and-secret-key) del sitio web hCaptcha®.

### Configure Chcaptcha® {#steps-to-configure-hcaptcha}

Para integrar AEM Forms con el servicio hCaptcha®, realice los siguientes pasos:

1. Cree un contenedor de configuración en su entorno de AEM Forms, que contenga las configuraciones de nube utilizadas para conectar AEM a servicios externos. Para crear un contenedor de configuración:
   1. Abra el entorno de AEM Forms.
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. En el Explorador de configuración, puede seleccionar una carpeta existente o crear una nueva:
      * Para crear una nueva carpeta y habilitar las configuraciones en la nube:
         1. En el Explorador de configuración, pulse **[!UICONTROL Crear]**.
         1. En el cuadro de diálogo Crear configuración, especifique un nombre, un título y marque **[!UICONTROL Configuraciones de nube]**.
         1. Haga clic en **[!UICONTROL Crear]**.
      * Para habilitar la configuración de nube para una carpeta existente:
         1. En el Explorador de configuración, selecciona la carpeta y selecciona	**[!UICONTROL Propiedades]**.
         1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
         1. Haga clic en **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.

1. Configure sus servicios en la nube:
   1. En la instancia de autor de AEM, vaya a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** y haga clic en **[!UICONTROL hCaptcha®]**.
      ![hCaptcha® en la interfaz de usuario](assets/hcaptcha-in-ui.png)
   1. Seleccione un contenedor de configuración, creado o actualizado, como se describe en la sección anterior. Seleccione **[!UICONTROL Crear]**.
      ![Configuración hCaptcha®](assets/config-hcaptcha.png)
   1. Especificar **[!UICONTROL Título]**, <!--**[!UICONTROL Name]**--> **[!UICONTROL Clave del sitio]** y **[!UICONTROL Clave secreta]** para el servicio hCaptcha® [obtenida como requisito previo](#prerequisite).
   1. Haga clic en **[!UICONTROL Crear]**.

      ![Configure Cloud Service para conectar su entorno de AEM Forms con Chcaptcha®](assets/create-hcaptcha-config.png)

   >[!NOTE]
   > Los usuarios no tienen que modificar [la URL de validación de JavaScript del lado del cliente](https://docs.hcaptcha.com/#add-the-hcaptcha-widget-to-your-webpage) y [la URL de validación del lado del servidor](https://docs.hcaptcha.com/#verify-the-user-response-server-side), ya que ya están rellenadas previamente para la validación de hCaptcha®.

   Una vez configurado el servicio hCAPTCHA, estará disponible para su uso en el formulario adaptable.

## Usar hCaptcha® en un formulario adaptable {#using-hCaptcha-in-aem-6.5}

1. Abra el entorno de AEM Forms.
1. Vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione un formulario adaptable y haga clic en **[!UICONTROL Propiedades]**.
1. En el **[!UICONTROL Contenedor de configuración]**, seleccione el Contenedor de configuración que contiene la Configuración de nube que conecta AEM Forms con Chcaptcha.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   Si no tiene un contenedor de configuración para Chcaptcha, consulte la sección [Conectar su entorno de AEM Forms con Chcaptcha®](#configure-hcaptcha-steps-to-configure-hcaptcha) para obtener información sobre cómo crear un contenedor de configuración.

   ![Seleccionar el contenedor de configuración](/help/forms/using/assets/captcha-properties.png)

1. Seleccione un formulario adaptable y haga clic en **[!UICONTROL Editar]** para abrir el formulario en el editor.
1. Desde el navegador de componentes, arrastre y suelte el componente **[!UICONTROL Captcha]** en el formulario adaptable.
1. Seleccione el componente **[!UICONTROL Captcha]** y haga clic en las propiedades ![Icono de propiedades](assets/configure-icon.svg) para abrir el cuadro de diálogo de propiedades. Especifique las siguientes propiedades:

   ![hCaptcha® v1](assets/config-hcaptcha-v1-img.png)

   * **[!UICONTROL Título]:** Especifique el título del componente Captcha.
   * **[!UICONTROL Mensaje de validación]:** Proporcione un mensaje de validación para su validación Captcha al enviar el formulario o al realizar una acción del usuario.
   * **[!UICONTROL Servicio Captcha]:** Seleccione el servicio CAPTCHA para el envío del formulario, aquí selecciona Captcha®.
   * **[!UICONTROL Ajustes de configuración]:** Seleccione la configuración de nube configurada para hCaptcha®.
     >[!NOTE]
     >Puede tener varias configuraciones en la nube en su entorno para un propósito similar. Por lo tanto, elija el servicio con cuidado. Si no aparece ningún servicio, consulte [Conectar su entorno de AEM Forms con hCaptcha®](#connect-your-forms-environment-with-hcaptcha-service) para aprender a crear un Cloud Service que conecte su entorno de AEM Forms con el servicio hCaptcha®.

   * **[!UICONTROL Mensaje de error]:** Proporcione el mensaje de error que se mostrará al usuario cuando falle el envío del Captcha.
   * **[!UICONTROL Tamaño de captcha]:** Puede seleccionar el tamaño de visualización del cuadro de diálogo de desafío de captcha®. Use la opción **[!UICONTROL Compacta]** para mostrar un objeto de tamaño pequeño y **[!UICONTROL Normal]** para mostrar un cuadro de diálogo de desafío hCaptcha® de tamaño relativamente grande o **[!UICONTROL Invisible]** para validar hCaptcha® sin procesar explícitamente el widget de casilla de verificación en la interfaz de usuario.

1. Seleccione **[!UICONTROL Listo]**.


Ahora, solo se permiten para el envío del formulario los formularios legítimos, en los que el usuario que rellena el formulario borra correctamente el desafío planteado por el servicio hCaptcha®.

**hCaptcha® es una marca comercial registrada de Intuition Machines, Inc.**


## Preguntas frecuentes

* **Q: ¿Puedo usar más de un componente Captcha en un formulario adaptable?**
* **R:** No se admite el uso de más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar un componente Captcha en un fragmento o panel marcado para la carga diferida.

## Ver también {#see-also}

* [Usar CAPTCHA en formularios adaptables](/help/forms/using/captcha-adaptive-forms.md)
* [Usar Captcha de torniquete en formularios adaptables](/help/forms/using/integrate-adaptive-forms-turnstile.md)
