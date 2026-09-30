---
title: Revisar información del uso de credenciales
description: Obtenga información sobre cómo revisar la información de uso de las credenciales. Se puede acceder a la información de uso de credenciales, que describe su uso, a través de la extensión de Acrobat Reader.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 5cc5c9fe-50ce-4863-bfa4-a009a6c3b06f
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
ht-degree: 4%
---
# Revisar información del uso de credenciales {#review-credential-use-information}

La credencial contiene información que describe su uso previsto y a la que se puede acceder mediante la aplicación web de usuario final de extensiones de Acrobat Reader DC. Puede utilizar esta información para determinar el tipo de credencial instalada (ya sea de evaluación o de producción) y sus fechas de validez.

1. Abra un explorador web e introduzca esta dirección URL:

   http://localhost:port/ReaderExtensions (donde *port* es el número de puerto del servidor de aplicaciones)

1. Inicie sesión con el nombre de usuario y la contraseña predeterminados:

   Nombre de usuario: administrador

   Contraseña: password

   >[!NOTE]
   >
   >Debe tener privilegios de administrador o superusuario para iniciar sesión con el nombre de usuario y la contraseña predeterminados. Para permitir que otros usuarios tengan acceso a las extensiones de Acrobat Reader DC, cree las cuentas de usuario en Administración de usuarios y conceda a los usuarios la función Aplicación web de extensiones de Acrobat Reader DC.

1. Seleccione el alias de credencial de la lista Seleccionar credencial y revise la información incluida en Fecha de caducidad y Aviso de uso previsto.

>[!NOTE]
>
>La fecha de caducidad de la credencial también está disponible en la página Configuración > Administración del almacén de confianza > Credenciales locales de la consola de administración, en Fecha de caducidad.
