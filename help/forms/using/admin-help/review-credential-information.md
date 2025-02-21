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
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '193'
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
