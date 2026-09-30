---
title: Configurar la administración de usuarios para un servidor LDAP habilitado para SSL
description: Obtenga información sobre cómo configurar la administración de usuarios para un servidor LDAP habilitado para SSL con el fin de permitir que la sincronización funcione correctamente en LDAPS.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: a97cb5a6-4097-4f2e-b932-cb858bd5681a
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
source-wordcount: '282'
ht-degree: 6%
---
# Configurar la administración de usuarios para un servidor LDAP habilitado para SSL {#configure-user-management-for-an-ssl-enabled-ldap-server}

Para que la sincronización funcione correctamente en LDAPS, los certificados LDAP emitidos por la autoridad de certificación (CA) deben estar presentes en el entorno de tiempo de ejecución de Java (JRE) del servidor de aplicaciones. Importe el certificado en el archivo cacerts JRE del servidor de aplicaciones, que normalmente se encuentra en el directorio *[JAVA_HOME]*/jre/lib/security/cacerts.

1. Habilite SSL en el servidor de directorio. Para obtener más información, consulte la documentación proporcionada por el proveedor del directorio.
1. Exporte un certificado de cliente desde el servidor de directorios.
1. Utilice el programa keytool para importar el archivo de certificado de cliente en el almacén de certificados predeterminado de la máquina virtual Java (JVM™) del servidor de aplicaciones de AEM Forms El procedimiento para esta tarea varía, según las rutas de instalación de JVM y cliente. Por ejemplo, si utiliza BEA WebLogic Server con JDK 1.5, desde un símbolo del sistema, escriba este texto:

   `keytool -import -alias`*alias* `-file certificatename -keystore C:\bea\jdk15_04\jre\lib\security\cacerts`

1. Cuando se le pida, escriba la contraseña. (Para Java, la contraseña predeterminada es `changeit`). Aparece un mensaje que indica que el certificado se ha importado correctamente.
1. Cuando se le pida, escriba `Yes` para confiar en el certificado.
1. Habilite SSL en Administración de usuarios y, al configurar los valores del directorio, seleccione Sí para la opción SSL y cambie la configuración del puerto en consecuencia. El número de puerto predeterminado es 636.

>[!NOTE]
>
>Si tiene algún problema al utilizar SSL, utilice un explorador LDAP para comprobar si puede acceder al sistema LDAP al utilizar SSL. Si el explorador LDAP no puede obtener acceso, el certificado o el servidor de aplicaciones no están configurados correctamente. Si el explorador LDAP funciona correctamente y sigue experimentando problemas, la administración de usuarios no está configurada correctamente.
