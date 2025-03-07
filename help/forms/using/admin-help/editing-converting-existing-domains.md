---
title: Editar y convertir dominios existentes
description: Aprenda a cambiar la configuración de los dominios existentes desde la página Administración de dominios. Convertir un dominio de empresa existente en un dominio híbrido o a la inversa.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 0dafef83-a516-48df-9175-019984843cfa
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 3%

---

# Editar y convertir dominios existentes{#editing-and-converting-existing-domains}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede cambiar la configuración de los dominios existentes desde la página Administración de dominios. También puede convertir un dominio de empresa existente en un dominio híbrido.

## Editar un dominio existente {#edit-an-existing-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio que desea editar.
1. Para cambiar el nombre de dominio, cambie el texto en el cuadro Nombre.
1. Para cambiar la información de autenticación de un dominio híbrido o empresarial, haga clic en el nombre de autenticación correspondiente en la parte inferior de la página. En la página Editar autenticación, cambie la configuración según sea necesario. (Consulte [Configuración de autenticación](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings).)
1. Para cambiar la información de directorio de un dominio de empresa, haga clic en el nombre de directorio correspondiente en la parte inferior de la página. En la página Editar directorio, cambie la configuración según sea necesario. (Consulte [Agregar directorios o SPI personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)).
1. Cuando haya completado los cambios, haga clic en Aceptar.

## Conversión de un dominio de empresa en un dominio híbrido {#convert-an-enterprise-domain-to-a-hybrid-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio de empresa que desea convertir.
1. Haga clic en Convertir en dominio híbrido.
1. Revise la información que aparece con respecto a los datos de usuarios y grupos y la autenticación de usuarios, y haga clic en Aceptar.
1. Edite la configuración del dominio híbrido y haga clic en Aceptar.

>[!NOTE]
>
>Si el dominio de empresa que está convirtiendo no contiene la configuración de directorio, se perderá la configuración de autenticación LDAP.

## Conversión de un dominio híbrido en un dominio de empresa {#convert-a-hybrid-domain-to-an-enterprise-domain}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Administración de dominios.
1. Haga clic en el nombre del dominio híbrido que desea convertir.
1. Haga clic en Convertir a dominio de empresa.
1. Revise la información que aparece con respecto a los datos de usuarios y grupos y la autenticación de usuarios, y haga clic en Aceptar.
1. Haga clic en Agregar directorio y configure la información de directorio necesaria. (Consulte [Agregar directorios o SPI personalizados](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)).
