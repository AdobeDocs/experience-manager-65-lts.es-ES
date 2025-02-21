---
title: Administrar listas de revocación de certificados
description: Obtenga información sobre cómo administrar listas de revocación de certificados. Puede importar, editar y eliminar listas de revocación de certificados (CRL) mediante la administración del almacén de confianza.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 5%

---

# Administrar listas de revocación de certificados{#managing-certificate-revocationlists}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Con la administración de almacén de confianza, puede importar, editar y eliminar listas de revocación de certificados (CRL). Se admiten listas de revocación de certificados codificadas en DER y Base64.

## Importar una CRL {#import-a-crl}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Listas de revocación de certificados y, a continuación, haga clic en Importar.
1. En el cuadro Alias, escriba un identificador para la CRL.
1. Haga clic en Examinar para buscar la CRL y, a continuación, haga clic en Aceptar.

## Exportar una CRL {#export-a-crl}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Listas de revocación de certificados.
1. Haga clic en el nombre de alias de la CRL para poder exportar y, a continuación, haga clic en Exportar.
1. Siga las instrucciones para exportar la CRL. Las listas CRL se exportan con codificación Base64.
1. Haga clic en Aceptar.

## Eliminar una CRL {#delete-a-crl}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Listas de revocación de certificados.
1. Active las casillas de verificación de las listas CRL que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.
