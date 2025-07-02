---
title: Aspectos básicos de la administración de certificados y credenciales
description: Obtenga información acerca de los conceptos básicos de la administración de certificados y credenciales.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 8aeacdb7-68a7-476f-a725-f9ad7406cc9c
source-git-commit: 02b9eb98d1fdf1b090166a6ae7c0a4379487d2e1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 4%

---

# Aspectos básicos de la administración de certificados y credenciales {#basics-of-managing-certificates-and-credentials}

Una *credencial* contiene la información de clave privada necesaria para firmar o identificar documentos. Un *certificado* es información de clave pública configurada para confianza. Los formularios AEM Forms utilizan certificados y credenciales de para varios fines:

* Las extensiones de Acrobat Reader DC utilizan una credencial para habilitar los derechos de uso de Adobe Reader en documentos de PDF. (Consulte [Configuración de credenciales para usarlas con las extensiones de Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)).
* Puede configurar Rights Management para que muestre las credenciales de uso en Acrobat únicamente de emisores de confianza. (Consulte [Configuración de la pantalla de Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) El nombre común (CN) debe estar presente en el certificado.
* El servicio Signature accede a los certificados y credenciales. Para obtener más información sobre el servicio Signature, consulte [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_65).

**Generando una clave de par**

Los formularios AEM Forms utilizan su almacén de confianza para almacenar y administrar certificados, credenciales y listas de revocación de certificados (CRL). Además, puede utilizar un dispositivo HSM (Hardware Security Module) independiente para almacenar claves privadas.

Los formularios de AEM no proporcionan ninguna opción para generar un par de claves. Sin embargo, puede generarla con herramientas como Java keytool e importarla en el almacén de confianza de formularios AEM Forms. Para obtener más información sobre la herramienta clave de Java, consulte lo siguiente:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

Los siguientes tipos de firma son compatibles y se pueden importar en formularios AEM Forms:

* Firma XML
* XMLTimeStampToken
* RFC 3161: TimeStampToken
* PKCS#7
* PKCS#1
* Firmas DSA

**Control de clave perdida o comprometida**

Si sospecha que la clave se ha perdido o se ha visto comprometida, realice las siguientes acciones:

1. Informe a la autoridad de certificación para que agregue la clave comprometida a la lista de revocación de certificados para revocarla.
1. Obtenga una clave nueva y sus certificados de la autoridad de certificación.
1. Vuelva a firmar los documentos firmados con la clave comprometida con la nueva clave.
