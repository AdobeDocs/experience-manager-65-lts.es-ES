---
title: Descripción general del servicio de salida
description: La salida permite combinar los datos del formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 5708ff03-4af7-47a3-b385-34a3a94f7a7b
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 3%
---
# Descripción general del servicio de salida {#overview-of-output-service}

La salida permite combinar los datos del formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos. La secuencia de salida se puede enviar a una impresora de red, a una impresora local o a un archivo de disco

Puede utilizar la página Salida en la consola de administración para administrar el servicio Salida. La configuración que configure se utiliza en tiempo de ejecución cuando la configuración equivalente no se especificó a través de la API de formularios AEM Forms. La configuración realizada a través de AEM Forms SDK anula la configuración establecida mediante la consola de administración.

Para obtener información adicional acerca del servicio Output, vea [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_61).

En las páginas Salida de la consola de administración, puede realizar varias tareas:

* Especifique conjuntos de caracteres para la internacionalización. (Consulte [Cambiar el conjunto de caracteres](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Especifique rutas absolutas y relativas para direcciones URL, URI, XCI y ubicaciones de archivos. (Consulte [Especificar ubicaciones de archivos para la salida](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configure los tamaños y las políticas de la caché. (Consulte [Especificación del modo de caché](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) y [Configuración de la caché](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)).
* Hacer que las fuentes estén disponibles en el servidor de aplicaciones. (Consulte [Hacer que las fuentes estén disponibles](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Especificar fuentes para incrustar. (Consulte [Especificar fuentes para incrustar](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Especifique las opciones de configuración XCI. (Consulte [Especificar las opciones de configuración de XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)).
* Especifique la configuración de seguridad. (Consulte [Especificar la configuración de seguridad](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Después de cambiar la configuración, haga clic en Save para aplicarla a Output. No es necesario reiniciar el servidor para que los cambios surtan efecto, pero es posible que tenga que reiniciar el Servicio de salida al configurar la caché.
