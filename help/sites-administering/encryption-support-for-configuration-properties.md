---
title: Compatibilidad con cifrado para propiedades de configuración
description: Obtenga información acerca de la compatibilidad con el cifrado de las propiedades de configuración proporcionadas en AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Compatibilidad con cifrado para propiedades de configuración{#encryption-support-for-configuration-properties}

## Información general {#overview}

Esta función permite almacenar todas las propiedades de configuración de OSGi en un formulario cifrado protegido en lugar de texto no cifrado. El formulario de la IU de la consola web se utiliza para crear texto cifrado a partir de texto no cifrado mediante la clave maestra de cifrado de todo el sistema.

Se agregó compatibilidad con el complemento de configuración OSGi para descifrar la propiedad antes de que la utilice un servicio.

>[!NOTE]
>
>Los servicios que esperan un valor cifrado deben utilizar la comprobación IsProtected para ver si el valor está cifrado antes de intentar descifrarlo, ya que puede que ya se haya descifrado.

## Habilitar compatibilidad con cifrado {#enabling-encryption-support}

Estos pasos muestran cómo cifrar la contraseña SMTP del servicio de correo. Puede completar estos pasos para una propiedad OSGI que desee cifrar.

1. Vaya a la consola web de AEM en *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. En la esquina superior izquierda, vaya a **Principal - Crypto Support**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. Se muestra la página **Compatibilidad con cifrado de la consola web de Adobe Experience Manager**.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. En el campo **Texto sin formato**, escriba el texto de los datos confidenciales que desea proteger.
1. Seleccione **Proteger**. El texto protegido se muestra como texto cifrado.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copie el texto protegido del paso n.º 5 y péguelo en el valor del formulario OSGI. En este ejemplo, la **contraseña SMTP** cifrada se agrega al *servicio Day CQ Mail*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Guarde las propiedades del servicio Day CQ Mail. La contraseña SMTP se enviará ahora como un valor cifrado.

## Compatibilidad con descifrado {#decryption-support}

AEM ahora proporciona un complemento de configuración para descifrar las propiedades de configuración. Este complemento de AEM descifrará y recuperará automáticamente las propiedades de texto no cifrado.
