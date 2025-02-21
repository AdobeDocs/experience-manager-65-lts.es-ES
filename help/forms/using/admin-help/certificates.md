---
title: Administrar certificados
description: Obtenga información sobre cómo importar y exportar un certificado y editar su configuración de confianza.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 8%

---

# Administrar certificados {#managing-certificates}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Con la administración de almacén de confianza, puede importar, editar y eliminar certificados en los que confía en el servidor para validar firmas digitales y autenticación de certificados. Puede importar y exportar cualquier número de certificados. Una vez importado un certificado, puede editar la configuración de confianza y el tipo de almacén de confianza. Tenga en cuenta las siguientes opciones al combinar tipos de almacén de confianza:

* **Confianza para autenticación de certificado con CA:** Para la validación de CRL, seleccione también Confianza para identidad.
* **Confianza para autenticación de certificado con ICA:** Seleccione sólo Confianza para identidad. No se debe confiar en ICA para la autenticación mediante certificado. Si confía en el ICA para la autenticación de certificados, el ICA se convierte en una CA para la generación de rutas. Si el ICA es de confianza tanto para la autenticación como para la identidad del certificado, se omite el certificado del proveedor de CA porque el ICA se convierte en la CA.
* **Confiar en el servidor OCSP con direcciones HTTP:** Si el servidor de respuesta OSCP reside en una ubicación HTTP, también debe seleccionar Confiar en conexiones SSL. Si el encuestado de OSCP requiere validación de CRL, asegúrese de seleccionar también Confiar en la identidad.
* **Raíz de Adobe:** No seleccione Conexiones SSL ni Tipos de almacén de confianza del servidor OCSP. La raíz de Adobe no es de confianza para Conexiones SSL y Servidor OCSP. Adobe no emite certificados OCSP y SSL. La raíz de Adobe es de confianza implícita con un alias name=&quot;ADOBEROOT&quot;.

Solo se admiten certificados X509v3. Este tipo de certificado se puede proporcionar en un archivo binario con codificación DER (archivo .cer) o en un archivo de texto que contenga una versión codificada en Base64 del mismo certificado con codificación DER (incluidos los certificados X509 en formato de correo mejorado de privacidad (PEM)).

Los certificados necesarios para completar una verificación de firma deben estar en el mismo almacén (HSM o base de datos).

También puede importar y eliminar certificados mediante la API de Administrador de confianza. Para obtener más información, consulte &quot;Importación de certificados mediante la API de Trust Manager&quot; y &quot;Eliminación de certificados mediante la API de Trust Manager&quot; en [Programación con formularios AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importar un certificado {#import-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Haga clic en Importar y, en Tipo de almacén de confianza, seleccione una de estas opciones:

   * **Confianza para conexiones SSL:** Especifica que los formularios AEM pueden usar certificados para conectarse a sistemas externos a través de SSL.
   * **Confiar en la firma de certificado:** Especifica que los certificados son de confianza en las operaciones de firma de documentos para certificar firmas digitales de autor.
   * **Confianza para la firma:** Especifica que los certificados son de confianza en las operaciones de firma de documentos para firmas digitales que no son de autor.
   * **Confianza para la autenticación de certificados:** Especifica que los formularios de AEM utilizan certificados para autenticar a los usuarios mediante la autenticación mediante certificado o tarjeta inteligente.
   * **Confianza para el servidor OCSP:** Especifica que los formularios de AEM pueden utilizar certificados para conectarse a los respondedores externos de OCSP
   * **Confianza para identidad:** Especifica que se pueden usar certificados para confiar en información distinta de los tipos especificados anteriormente.

   >[!NOTE]
   >
   >El almacén de confianza confía implícitamente en un certificado raíz de Adobe para la autenticación de certificados, la firma, la firma de certificados y la identidad.

1. En el cuadro Alias, escriba el identificador del certificado.
1. Haga clic en **[!UICONTROL Examinar]** para buscar el certificado y, a continuación, haga clic en **[!UICONTROL Aceptar]**.

## Exportar un certificado {#export-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Haga clic en el nombre del alias del certificado que desea exportar. Se muestra la página **[!UICONTROL Detalles del certificado]**.
1. Haga clic en **[!UICONTROL Exportar]**, siga las instrucciones para exportar el certificado y, a continuación, haga clic en **[!UICONTROL Aceptar]**.

## Editar la configuración de confianza y el tipo de almacén de confianza de un certificado {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Haga clic en el nombre de alias del certificado que desea editar.
1. Haga clic en **[!UICONTROL Actualizar certificado]**.
1. Para cambiar el Nombre de alias del certificado, escriba un nombre nuevo en el cuadro Alias.
1. Para actualizar el tipo de almacén de confianza para el certificado, seleccione el tipo de almacén de confianza adecuado.
1. Para actualizar las restricciones de directiva, en el cuadro Directivas de certificado, escriba la información de directiva y, a continuación, haga clic en **[!UICONTROL Aceptar]**.

## Eliminar un certificado {#delete-a-certificate}

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración del almacén de confianza > Certificados]**.
1. Seleccione las casillas de verificación de los certificados que desea eliminar, haga clic en **[!UICONTROL Eliminar]** y, a continuación, haga clic en **[!UICONTROL Aceptar]**.
