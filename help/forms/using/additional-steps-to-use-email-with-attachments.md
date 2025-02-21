---
title: Pasos adicionales para obtener correo electrónico con archivos adjuntos
description: Obtenga información sobre cómo corregir el error cuando no puede recuperar correos electrónicos con archivos adjuntos para AEM Forms en plataformas JEE.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 66%

---

# No se puede obtener correo electrónico con archivos adjuntos para AEM Forms en plataformas JEE{#unable-to-get-email-with-attachments}

El problema se aplica a la siguiente versión:

* Experience Manager 6.5 Forms

## Problema {#issue}

El usuario no puede realizar operaciones como Enviar PDF por correo electrónico o Incluir archivos adjuntos con la configuración de envío.

## Solución {#solution}

1. Descargue jar como [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) y descomprima el archivo jar descargado para obtener el archivo de manifiesto.

1. Utilice el archivo de manifiesto de `java.mail-1.0.jar` recuperado del paso 1 para crear un archivo jar personalizado, por ejemplo, `java.mail-1.5.jar`.

1. Abra el archivo de manifiesto y reemplace todas las ocurrencias de `1.5.0` con `1.5.6` y `Bundle-Version: 1.0` con `Bundle-Version:1.5`

1. Cree un archivo jar personalizado (`java.mail-1.5.jar`) con el siguiente comando en la carpeta `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` como:
   `jar -cfm java.mail-1.5.jar manifest.mf`

   En el comando anterior, *manifest.mf* es el nombre del archivo de manifiesto y *java.mail-1.5.jar* es el nombre del archivo que se crearía después de ejecutar el comando anterior.

1. Descargue [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Navegue hasta `http://<server name>:<port>/lc/system/console/bundles` y elimine el paquete con un nombre como `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Instale `java.mail-1.5.jar` obtenido del paso 3. Este paso reinicia las propiedades sling de la implementación JEE. Espere a que se instalen los paquetes en `http://<server name>:<port>/lc/system/console/bundles` para mostrar el estado como **Activo**.

   >Si el estado sigue siendo **InActive**, reinicie   **JBoss®** de la **Consola de servicios**.


1. Instale el archivo `javax.mail-1.5.6.redhat-1.jar` descargado mediante el paso 5.

1. Detenga **JBoss®** desde la **Consola de servicios** y anexe las siguientes propiedades al archivo **Sling.properties**:
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Reinicie **JBoss®**.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.
