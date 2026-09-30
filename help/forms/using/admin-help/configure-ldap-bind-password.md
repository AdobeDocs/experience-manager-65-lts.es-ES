---
title: Configurar la contraseña de enlace LDAP
description: Obtenga información sobre cómo configurar el campo de contraseña de enlace antes de importar el archivo de configuración en otro sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 33e0f81f-7867-4c59-a9e5-75bf5182a27c
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
source-wordcount: '196'
ht-degree: 5%
---
# Configurar la contraseña de enlace LDAP{#configure-the-ldap-bind-password}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Para evitar riesgos de seguridad, el campo de contraseña de enlace del archivo de configuración exportado (config.xml) no está configurado. Antes de importar el archivo de configuración a otro sistema, asegúrese de configurar esta contraseña. Esta contraseña anula una contraseña existente almacenada en la base de datos. Una contraseña nula no reemplaza un valor de contraseña no nula existente.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Para exportar la configuración actual a un archivo, haga clic en Exportar y guarde el archivo de configuración en otra ubicación.
1. En el archivo, busque el nodo `Domains` > *[Su nombre de dominio]* > `DirectoryConfigs` > `LDAPGroupConfig`. A continuación se muestra un ejemplo:

   ```xml
    <node name="LDAPGroupConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="batchSize" value="200" />
            <entry key="binduser" value="cn=Directory Manager" />
            <entry key="bindpassword" value="" />
        </map>
   ```

   Escriba un valor para `bindpassword` y guarde los cambios.

1. En el archivo, busque el nodo `Domains` > *[Su nombre de dominio]* > `DirectoryConfigs` > `LDAPGroupConfig` > `LDAPUserConfig`. A continuación se muestra un ejemplo:

   ```xml
    <node name="LDAPUserConfig">
        <map>
            <entry key="bindanonymously" value="false" />
            <entry key="batchSize" value="200" />
            <entry key="basedn" value="dc=corp,dc=adobe,dc=com" />
            <entry key="bindpassword" value="" />
            <entry key="binduser" value="cn=Directory Manager" />
        </map>
   ```

   Escriba un valor para `bindpassword` y guarde los cambios.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo, en Importar y, a continuación, en Aceptar.
