---
title: Administrar credenciales locales
description: Obtenga información sobre cómo administrar las credenciales locales mediante la administración del almacén de confianza. Los formularios AEM admiten credenciales RSA y DSA en un formulario PKCS12 estándar.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: d297ab09-2b92-442a-8b19-ffee86e24bb9
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 1%

---

# Administrar credenciales locales {#managing-local-credentials}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Las credenciales locales son credenciales de clave privada alojadas en Administración de almacén de confianza. Una *credencial local* identifica dónde se almacena la credencial DES de un usuario. Con la administración de almacén de confianza, puede importar y administrar sus credenciales locales utilizando, por ejemplo, archivos PFX existentes, de modo que pueda importar, editar y eliminar credenciales locales.

Los formularios AEM admiten credenciales RSA y DSA de hasta 4096 bits en formato PKCS12 estándar (archivos .pfx y .p12).

Puede importar y exportar cualquier número de credenciales. Si desea reemplazar una credencial caducada con el mismo alias, elimine la credencial y, a continuación, importe la nueva con el mismo alias.

Para obtener información e instrucciones relacionadas con las extensiones de Acrobat Reader DC, consulte [Configuración de credenciales para usarlas con las extensiones de Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).

## Importar una credencial {#import-a-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en Importar. En Tipo de almacén de confianza, seleccione una de estas opciones:

   * **Credencial de firma de documento:** Credencial utilizada para emitir una firma digital en un documento.
   * **Credencial de las extensiones de Acrobat Reader DC:** Certificado digital específico de las extensiones de Acrobat Reader DC que permite activar los derechos de uso de Adobe Reader en los documentos de PDF producidos.
   * **Valor predeterminado:** Indica que esta es la credencial predeterminada que se debe usar con las extensiones de Acrobat Reader DC.

   Para obtener información sobre cómo obtener una credencial, consulte [Preparación para instalar formularios de AEM](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar de la credencial en las extensiones de Acrobat Reader DC y en el servicio Signature. Este alias también se utiliza para acceder a las credenciales mediante programación utilizando AEM Forms SDK.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente a mayúsculas para su visualización. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Examinar para buscar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;No se pudieron importar las credenciales debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Exportar una credencial {#export-a-credential}

Las credenciales se exportan como archivos P12 en formato PKCS#12.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en el nombre de alias de la credencial que desea exportar y, a continuación, haga clic en Exportar.
1. En el cuadro Contraseña, escriba la contraseña. Esta contraseña es nueva y se utiliza para cifrar las credenciales exportadas.
1. Haga clic en Exportar, siga las instrucciones para exportar las credenciales y, a continuación, haga clic en Aceptar.

## Editar el alias o el tipo de almacén de confianza de una credencial {#edit-a-credential-s-alias-or-trust-store-type}

Una vez importadas las credenciales, puede editar el nombre de alias y el tipo de almacén de confianza.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Haga clic en el nombre de alias de la credencial que desea editar.
1. Haga clic en Actualizar credencial.
1. Edite el nombre del alias y el tipo de almacén de confianza según sea necesario y haga clic en Aceptar.

## Eliminar una credencial {#delete-a-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales locales.
1. Seleccione las casillas de verificación de las credenciales que desea eliminar.
1. Haga clic en Eliminar y, a continuación, en Aceptar.
