---
title: Configurar credenciales para usarlas con extensiones de Acrobat Reader DC
description: Obtenga información sobre cómo configurar credenciales para utilizarlas con extensiones de Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# Configurar credenciales para usarlas con extensiones de Acrobat Reader DC{#configuring-credentials-for-use-with-acrobat-reader-dc-extensions}

Para aplicar derechos de uso a documentos de PDF, configure formularios de AEM con una credencial válida para las extensiones de Acrobat Reader DC. Es posible que se haya configurado una credencial durante la instalación de los formularios AEM. Si no configuró la credencial de las extensiones de Acrobat Reader DC mientras ejecutaba el Administrador de configuración o si necesita importar una credencial nueva o de reemplazo, puede hacerlo usando las páginas de Administración del almacén de confianza.

Si utiliza una credencial de evaluación, reemplácela por una credencial de producción al pasar al entorno de producción. Para actualizar una credencial caducada o de evaluaciones, elimine primero la credencial antigua de las extensiones de Acrobat Reader DC.

Para obtener información sobre cómo obtener una credencial, consulte [Preparación para instalar formularios de AEM (un solo servidor)](https://helpx.adobe.com/pdf/aem-forms/6-3/prepare-install-single-server.pdf).

El almacén de confianza puede contener más de una credencial de extensiones de Acrobat Reader DC. Designe una de esas credenciales como credencial predeterminada de las extensiones de Reader. La credencial predeterminada se utiliza cuando un usuario de Workbench no puede determinar qué credencial utilizar durante la creación del proceso. Estas reglas se aplican a las credenciales predeterminadas:

* Si importa una credencial de extensiones de Acrobat Reader DC y el almacén de confianza no contiene otras credenciales de extensiones de Acrobat Reader DC, se establece como predeterminada.
* Si importa una credencial de extensiones de Acrobat Reader DC con la opción predeterminada seleccionada, el tipo predeterminado se quita de una credencial predeterminada existente. La credencial importada se convierte en la predeterminada.
* No puede eliminar una credencial predeterminada de extensiones de Acrobat Reader DC. Para eliminar la credencial predeterminada, primero establezca otra credencial como predeterminada. Una excepción a esta regla es que si solo hay una credencial, puede eliminarla aunque sea la predeterminada.
* No puede actualizar una credencial predeterminada de extensiones de Acrobat Reader DC.

>[!NOTE]
>
>También puede importar y eliminar credenciales mediante programación. (Consulte [Programar con formularios AEM](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es)).

## Importar una credencial de extensiones de Acrobat Reader DC {#import-a-acrobat-reader-dc-extensions-credential}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione Credencial de extensiones de Acrobat Reader DC.
1. (Opcional) Para indicar que esta credencial es la predeterminada para usar con las extensiones de Acrobat Reader DC, seleccione Predeterminada.
1. En el cuadro Alias, escriba un identificador para la credencial. Este identificador se utiliza como nombre para mostrar de la credencial en las extensiones de Acrobat Reader DC. Este alias también se utiliza para acceder a las credenciales mediante programación utilizando AEM Forms SDK.

   >[!NOTE]
   >
   >El nombre del alias se convierte automáticamente a mayúsculas para su visualización. El nombre del alias no distingue entre mayúsculas y minúsculas cuando se hace referencia a él en un proceso.

1. Haga clic en Elegir archivo para buscar la credencial, escriba la contraseña de la credencial y, a continuación, haga clic en Aceptar.

   Si aparece el mensaje de error &quot;No se pudieron importar las credenciales debido a un formato de archivo incorrecto o a una contraseña incorrecta&quot;, compruebe que la contraseña sea válida.

## Quitar una credencial de extensiones de Acrobat Reader DC {#remove-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Seleccione la credencial y haga clic en Eliminar.

## Reemplazar una credencial de extensiones de Acrobat Reader DC {#replace-a-acrobat-reader-dc-extensions-credential}

1. En la consola de administración, haga clic en Configuración > Administración del almacén de confianza > Credenciales locales.
1. Tome nota del alias de la credencial existente, selecciónela y haga clic en Eliminar.
1. Importe la nueva credencial con el mismo nombre de alias.
