---
title: Entrega HTTP2 de contenido
description: Obtenga información sobre cómo HTTP/2 mejora la forma en que los exploradores y servidores se comunican, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: Publishing,Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 3%

---

# Entrega de contenido HTTP/2 {#http-delivery-of-content}

Adobe anuncia la disponibilidad del envío de contenido HTTP/2 con el beneficio general de mejorar el rendimiento.

>[!NOTE]
>
>Esta función requiere que utilice la CDN predeterminada que está integrada en Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que los exploradores y servidores se comunican, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El siguiente sitio web describe HTTP/2 y sus ventajas de forma breve y sencilla:

[Lo que debe saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## ¿Cuáles son las principales ventajas de pasar a HTTP/2 para la entrega de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento puede variar considerablemente. Se basa en muchos factores, como el código del sitio web, el uso de Dynamic Media, el dispositivo del consumidor, la pantalla y la ubicación.

Las propias pruebas de Adobe arrojaron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró entre un 7 % y un 28 % en función del dispositivo y el explorador. Las mejoras de rendimiento más notables se obtuvieron en dispositivos iOS.
* Para los espectadores, el rendimiento del tiempo de carga mejoró un 15 %.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para las solicitudes de medios enriquecidos.
* Utilice la CDN (red de distribución de contenido) incluida en Adobe como parte de la licencia de Dynamic Media.
* Utilice un dominio dedicado (que no sea company-h.assetsadobe#.com).

  Si ya tiene un dominio dedicado, puede optar por su inclusión a través de la Asistencia al cliente de Adobe.

  Si no tiene un dominio dedicado, Adobe tiene previsto programar la transición a HTTP/2 en 2018.

## ¿Cuál es el proceso para habilitar HTTP/2 en mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

La solicitud para cambiar a HTTP/2 se inicia automáticamente, pero no se realiza automáticamente.

1. Para cambiar a HTTP/2, inicie una solicitud de asistencia al cliente de Adobe. Ver [Abrir un ticket de asistencia](https://experienceleague.adobe.com/?support-solution=General&amp;lang=en&amp;support-tab=home#support).

   1. Proporcione la siguiente información en su solicitud de soporte:

      1. Nombre del contacto principal, correo electrónico, teléfono.
      1. Todos los dominios que deben transferirse a HTTP/2.
      1. Compruebe que utiliza HTTPS seguro para solicitudes de medios enriquecidos.
      1. Compruebe que utiliza la CDN a través de Adobe y que no se administra con una relación directa.
      1. Compruebe que utiliza un dominio dedicado. Si utiliza Dynamic Media, utilizará un dominio dedicado.

   1. Atención al cliente le añade a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
   1. Cuando Adobe esté listo para administrar su solicitud, el Servicio de atención al cliente se pondrá en contacto con usted para coordinar la transición y establecer una fecha objetivo.
   1. Se le notifica una vez finalizada y puede verificar que la transición a HTTP2 se ha realizado correctamente.

      Dado que el explorador no indica este hecho, es necesario descargar una extensión.

      Para Firefox y Chrome, hay una extensión llamada &quot;HTTP/2 e indicador SPDY&quot;. Los navegadores solo admiten http/2 de forma segura, por lo que es necesario llamar a una dirección URL con https para verificarla. Si se admite http/2, se indica con la extensión en forma de símbolo de Flash azul y el encabezado &quot;X-Firefox-Spray&quot; : &quot;h2&quot;.

## ¿Cuándo puedo esperar que se realice la transición a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se procesan en el orden en que se reciben en Asistencia al cliente.

>[!NOTE]
>
>Puede haber un tiempo de espera largo porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, solo se pueden gestionar unas pocas transiciones de cliente a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché visita directamente los servidores de origen de Adobe hasta que se vuelve a crear la caché. Como tal, Adobe tiene previsto gestionar varias transiciones de clientes a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes del origen.

## ¿Cómo puede verificar si una dirección URL o sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Dado que el explorador no indica este hecho, es necesario descargar una extensión.

Para Firefox y Chrome, hay una extensión llamada &quot;HTTP/2 e indicador SPDY&quot;. Los navegadores solo admiten http/2 de forma segura, por lo que es necesario llamar a una dirección URL con https para verificarla. Si http/2 es compatible, se indica con la extensión en forma de símbolo de Flash azul y un encabezado `X-Firefox-Spdy` : `h2`.
