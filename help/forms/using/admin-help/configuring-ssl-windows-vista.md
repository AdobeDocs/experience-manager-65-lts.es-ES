---
title: Configurar SSL en Windows Vista
description: Obtenga información sobre cómo configurar SSL en Windows Vista. Utilice y ejecute la herramienta Java Keytool para generar el certificado SSL con claves RSA para la autenticación.
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: ee73f6a1-712c-461f-95e8-85f8c5694293
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 5%
---
# Configurar SSL en Windows Vista {#configuring-ssl-on-windows-vista}

Para configurar SSL en Windows Vista™, necesita un certificado SSL con claves RSA para la autenticación. Puede utilizar la herramienta clave de Java para crear el certificado.

>[!NOTE]
>
>Windows Vista no funciona con claves DSA.

Puede ejecutar keytool con un solo comando que incluya toda la información necesaria para crear el certificado y el repositorio de claves.

**Crear un certificado SSL**

1. En un símbolo del sistema, vaya a *`[JAVA HOME]`*/bin y escriba el siguiente comando para crear el certificado y el almacén de claves:

   `keytool -genkey -keyalg RSA -dname "CN=`*Nombre de host* `, OU=`*Nombre de grupo* `, O=`*Nombre de empresa* `,L=`*Nombre de ciudad* `, S=`*Estado* `, C=`*Código de país* `" -alias`*&quot;Certificado LC&quot;* `-keypass` `key`*_* *contraseña* `-keystore`*nombre de almacén* `.keystore`

   >[!NOTE]
   >
   >Reemplace *`[JAVA_HOME]`por el directorio donde está instalado el JDK y reemplace el texto en cursiva por valores que se correspondan con su entorno.*

1. Escriba `changeit` como contraseña. Esta contraseña es la predeterminada para una instalación de Java y es posible que el administrador del sistema la haya cambiado.
