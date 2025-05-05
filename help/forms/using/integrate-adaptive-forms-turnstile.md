---
title: ¿Cómo usar Turnstile en un formulario adaptable para AEM 6.5?
description: Mejore la seguridad de los formularios con el servicio Turnstile sin esfuerzo. Guía paso a paso en el interior
feature: Adaptive Forms, Foundation Components
role: User, Developer
source-git-commit: 1444b0fc0811cbb187d2a4d83b626444e44ef73f
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 18%

---

# Conecte su entorno de AEM Forms con Turnstile {#connect-your-forms-environment-with-turnstile-service}


<span class="preview">Esta característica no está habilitada de manera predeterminada. Puede escribir desde su dirección oficial a aem-forms-ea@adobe.com para solicitar acceso a la función.</span>

CAPTCHA (prueba de Turing completamente automática y pública para diferenciar ordenadores de humanos) es un programa que se utiliza comúnmente en transacciones en línea para distinguir entre humanos y programas o bots automatizados. Plantea un desafío y evalúa la respuesta del usuario para determinar si es un humano o un bot que interactúa con el sitio. Evita que el usuario continúe si la prueba falla y ayuda a que las transacciones en línea sean seguras al impedir que los bots publiquen contenido no deseado o con fines malintencionados.

AEM Forms es compatible con las siguientes soluciones CAPTCHA:

* [Turnstile Captcha](/help/forms/using/integrate-adaptive-forms-turnstile.md)
* [Google reCAPTCHA](/help/forms/using/captcha-adaptive-forms.md)
* [hCaptcha](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)


<!-- ![Turnstile](assets/Turnstile-challenge.png)-->

## Integración del entorno de AEM Forms con Turnstile Captcha

El Turnstile Captcha de Cloudflare es una medida de seguridad que tiene como objetivo proteger los formularios y sitios de bots automatizados, ataques maliciosos, spam y tráfico automatizado no deseado. Presenta una casilla de verificación en el envío del formulario para verificar que son humanos, antes de permitirles enviar el formulario.

>[!VIDEO](https://video.tv.adobe.com/v/3440940/)

### Requisitos previos para integrar el entorno de AEM Forms con Turnstile Captcha {#prerequisite}

Para configurar Turnstile para AEM Forms, necesita obtener la clave del sitio [Turnstile y la clave secreta](https://developers.cloudflare.com/turnstile/get-started/) del sitio web de Turnstile.

### Configurar torniquete {#steps-to-configure-hcaptcha}

Para integrar AEM Forms con el servicio de torniquete, realice los siguientes pasos:

1. Cree un contenedor de configuración en su entorno de AEM Forms. Un contenedor de configuración contiene las configuraciones de nube utilizadas para conectar AEM Forms a servicios externos. Para crear un contenedor de configuración:
   1. Abra el entorno de AEM Forms.
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. En el Explorador de configuración, seleccione una carpeta existente o cree una carpeta nueva:
      * Para crear una **carpeta nueva** y habilitar las configuraciones en la nube:
         1. En el Explorador de configuración, pulse **[!UICONTROL Crear]**.
         1. En el cuadro de diálogo Crear configuración, especifique un nombre, un título y marque **[!UICONTROL Configuraciones de nube]**.
         1. Haga clic en **[!UICONTROL Crear]**.
      * Para habilitar la configuración de nube para una **carpeta existente**:
         1. En el Explorador de configuración, seleccione la carpeta y haga clic en **[!UICONTROL Propiedades]**.
         1. En el cuadro de diálogo Propiedades de configuración, habilite **[!UICONTROL Configuraciones de nube]**.
         1. Haga clic en **[!UICONTROL Guardar y cerrar]** para guardar la configuración.

1. Configure sus servicios en la nube:
   1. En la instancia de autor de AEM, ve a ![tools-1](assets/tools-1.png) > **[!UICONTROL Cloud Services]** y haz clic en **[!UICONTROL Torniquete]**.

      ![Torniquete en Cloud Services](assets/turnstile-in-ui.png)
   1. Seleccione un contenedor de configuración, creado o actualizado, como se describe en la sección anterior. Haga clic en **[!UICONTROL Crear]**.

      ![Turnstile de configuración](assets/config-hcaptcha.png)
   1. Especifique **[!UICONTROL Tipo de widget]** como administrado, no interactivo o invisible.
   1. Proporcione otros detalles como **[!UICONTROL Title]**, **[!UICONTROL Name]**.
   1. Especifique **[!UICONTROL Clave del sitio]** y **[!UICONTROL Clave secreta]** para el servicio de torniquete [obtenido en el requisito previo](#prerequisite).
   1. Haga clic en **[!UICONTROL Crear]**.

      ![Configure Cloud Service para conectar su entorno de AEM Forms con Turnstile](assets/config-turntstile.png)

   >[!NOTE]
   > Los usuarios no tienen que modificar la URL de validación de JavaScript del lado del cliente y la URL de validación del lado del servidor, ya que ya están rellenadas previamente para la validación de Turnstile.

   Una vez configurado el servicio Turnstile Captcha, estará disponible para su uso en el formulario adaptable.

## Utilizar el torniquete en un formulario adaptable {#using-turnstile-aem-6.5}

1. Abra el entorno de AEM Forms.
1. Vaya a **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione un formulario adaptable y haga clic en **[!UICONTROL Propiedades]**. En **[!UICONTROL Contenedor de configuración]**, seleccione el contenedor de configuración que contiene la configuración de nube que conecta AEM Forms con Turnstile.
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   Si no tiene un contenedor de configuración para configurar el servicio Captcha, consulte la sección [Configurar el torniquete](#configure-turnstile-steps-to-configure-hcaptcha) para obtener información sobre cómo crear un contenedor de configuración.

   ![Seleccionar el contenedor de configuración](assets/captcha-properties.png)

1. Seleccione un formulario adaptable y haga clic en **[!UICONTROL Editar]** para abrir el formulario adaptable en el editor.
1. Desde el navegador de componentes, arrastre y suelte el componente **[!UICONTROL Captcha]** en el formulario adaptable.
1. Seleccione el componente **[!UICONTROL Captcha]** y haga clic en el icono de las propiedades ![Properties](assets/configure-icon.svg). Abre el cuadro de diálogo de propiedades. Especifique las siguientes propiedades:

   <!--![Turnstile v2](assets/turnstile-settings-v2.png)-->
   ![Torniquete Cloudfare v1](assets/turnstile-setting-v1.png)

   * **[!UICONTROL Título]:** Especifique el título del componente Captcha. puede identificar fácilmente un componente de formulario con su título único, tanto en el formulario como en el editor de reglas.
   * **[!UICONTROL Ajustes de configuración]:** Seleccione una configuración de nube configurada para el torniquete.
   * **[!UICONTROL Mensaje de validación]:** Proporcione un mensaje de validación para validar el captcha al enviar el formulario o en una acción del usuario.
   * **[!UICONTROL Servicio Captcha]:** Seleccione el servicio CAPTCHA para el envío del formulario, aquí selecciona Turnstile®.
   * **[!UICONTROL Ajustes de configuración]:** Seleccione la configuración de nube configurada para Turnstile®.

     >[!NOTE]
     >Puede tener varias configuraciones en la nube en su entorno para un propósito similar. Por lo tanto, elija el servicio con cuidado. Si no hay ningún servicio en la lista, consulte [Conectar su entorno de AEM Forms con Turnstile](#connect-your-forms-environment-with-turnstile-service) para aprender a crear un Cloud Service que conecte su entorno de AEM Forms con el servicio de Turnstile.

   * **[!UICONTROL Mensaje de error]:** Proporcione el mensaje de error que se mostrará al usuario cuando falle el envío del Captcha.
   * **Tamaño del captcha:** Puede seleccionar el tamaño de visualización del cuadro de diálogo de desafío de captcha®. Use la opción **[!UICONTROL Compacta]** para mostrar un objeto de tamaño pequeño y **[!UICONTROL Normal]** para mostrar un cuadro de diálogo de desafío hCaptcha® de tamaño relativamente grande.

1. Seleccione **[!UICONTROL Listo]**.


Ahora, solo se permiten para el envío del formulario los formularios legítimos, en los que el usuario que rellena el formulario borra correctamente el desafío planteado por el servicio Turnstile.

![Desafío de torniquete](assets/turnstile-challenge.png)


## Preguntas frecuentes

* **Q: ¿Puedo usar más de un componente Captcha en un formulario adaptable?**
* **R:** No se admite el uso de más de un componente Captcha en un formulario adaptable. Además, no se recomienda utilizar un componente Captcha en un fragmento o panel marcado para la carga diferida.

## Ver también {#see-also}

* [Usar CAPTCHA en formularios adaptables](/help/forms/using/captcha-adaptive-forms.md)
* [Usar Chcaptcha en formularios adaptables](/help/forms/using/integrate-adaptive-forms-hcaptcha.md)
