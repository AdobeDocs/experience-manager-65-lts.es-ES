---
title: Preguntas frecuentes sobre la entrega de contenido HTTP2
description: Obtenga información acerca de la entrega de contenido HTTP2 y cómo puede aumentar el rendimiento general del contenido web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# Preguntas frecuentes sobre la entrega de contenido HTTP2{#http-delivery-of-content-faq}

Adobe anuncia la disponibilidad de la entrega de contenido HTTP/2. Cuando se utiliza HTTP/2, se observa un aumento general del rendimiento.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que los exploradores y servidores se comunican, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El siguiente sitio web describe HTTP/2 y sus ventajas de forma breve y sencilla:

[Lo que debe saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html).

## ¿Cuáles son las principales ventajas de pasar a HTTP/2 para la entrega de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía considerablemente en función de factores como el código del sitio web, el uso de Dynamic Media, el dispositivo, la pantalla y la ubicación del cliente.

Las propias pruebas de Adobe arrojaron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró entre un 7 % y un 28 % en función del dispositivo y el explorador. Las mejoras de rendimiento más notables se obtuvieron en dispositivos iOS.
* Para los espectadores, el rendimiento del tiempo de carga mejoró un 15 %.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para las solicitudes de medios enriquecidos.
* Utilice la CDN (red de distribución de contenido) incluida en Adobe como parte de la licencia de Dynamic Media.
* Use un dominio dedicado (es decir, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico de Dynamic Media (es decir, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

  Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicia sesión en tu cuenta o cuentas de empresa. A continuación, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **Nombre de servidor publicado**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar que se traslade a su propio dominio personalizado como parte de esta transición.

## ¿Cuál es el proceso para habilitar HTTP/2 en mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [Use Admin Console para crear un caso de soporte](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) y solicite cambiar a HTTP/2; no se hace automáticamente por usted.
1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre del contacto principal, correo electrónico y número de teléfono.
   * Todos los dominios que deben transferirse a HTTP2. Es decir, `images.company.com` o `mycompany.scene7.com`.

     Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicia sesión en tu cuenta o cuentas de empresa. A continuación, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **[!UICONTROL Nombre de servidor publicado]**.

   * Compruebe que utiliza HTTPS seguro para solicitudes de medios enriquecidos.
   * Compruebe que está utilizando la CDN a través de Adobe y que no está gestionado con una relación directa.
   * Compruebe que está utilizando un dominio dedicado. Es decir, `images.company.com` o `mycompany.scene7.com`, no es un dominio genérico de Dynamic Media como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

     Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicia sesión en tu cuenta o cuentas de empresa. A continuación, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **[!UICONTROL Nombre de servidor publicado]**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar que se traslade a su propio dominio personalizado como parte de esta transición.

1. La Asistencia al cliente de Adobe le agrega a la lista de espera del cliente HTTP/2 en función del orden en que se enviaron las solicitudes.
1. Cuando Adobe esté listo para administrar la solicitud, la asistencia técnica se pondrá en contacto con usted para coordinar la transición y establecer una fecha objetivo.
1. Se le notificará una vez finalizado y podrá verificar que la transición a HTTP2 se ha realizado correctamente.

## ¿Cuándo puedo esperar realizar la transición a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se procesan en el orden en que se reciben en Asistencia al cliente de Adobe.

>[!NOTE]
>
>Hay un tiempo de espera largo porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, solo se pueden gestionar unas pocas transiciones de cliente a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché visita directamente los servidores de origen de Adobe hasta que se vuelve a crear la caché. Debido a esta acción, Adobe tiene previsto gestionar varias transiciones de cliente a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes del origen de Adobe.

## ¿Cómo puede verificar si una dirección URL o sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Descargue una extensión que pueda utilizar con su explorador web. Para Firefox y Chrome, hay una extensión llamada **[!UICONTROL HTTP/2 e indicador SPDY]**. Los navegadores solo admiten HTTP/2 de forma segura, por lo que es necesario llamar a una dirección URL con HTTPS para verificarla. Si se admite HTTP/2, se indica con la extensión en forma de símbolo de Flash azul y el encabezado &quot;X-Firefox-Spray&quot; : &quot;h2&quot;.
