---
title: Configurar servicios de almacenamiento para borradores y envíos
description: Aprenda a configurar el almacenamiento para borradores y envíos
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
exl-id: 33769e4f-2213-442b-bd1c-1728cd917460
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: fa155e29-cba2-5e77-9efd-4824be5ce4c8
    internal-label: Forms Portal
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 100%
---
# Configurar servicios de almacenamiento para borradores y envíos {#configuring-storage-services-for-drafts-and-submissions}

## Información general {#overview}

Con AEM Forms, puede almacenar:

* **Borradores**: formulario en curso que los usuarios finales rellenan y guardan y envían después.

* **Envíos**: formularios enviados que contienen datos proporcionados por el usuario.

Los servicios de metadatos y datos del portal de AEM Forms son compatibles con borradores y envíos. De forma predeterminada, los datos se almacenan en la instancia de publicación, que luego se replica de forma inversa en la instancia de autor configurada para que estén disponibles para la percolación en otras instancias de publicación.

La preocupación con el enfoque preestablecido existente es que almacena todos los datos en las instancias de publicación, incluidos los que pueden ser Información de identificación personal (PII).

Además del método predeterminado mencionado anteriormente, también hay una implementación alternativa disponible para insertar directamente los datos del formulario en el procesamiento en lugar de guardarlos localmente. Los clientes que tengan dudas sobre el almacenamiento de datos potencialmente confidenciales en la instancia de publicación pueden elegir la implementación alternativa en la que los datos se envían a un servidor de procesamiento. Dado que el procesamiento se produce en la instancia de autor, normalmente permanece en una zona segura.

>[!NOTE]
>
>Cuando se utiliza la acción de envío del portal de formularios o se habilita la opción Almacenar datos en el portal de formularios en formularios adaptables, los datos del formulario se almacenan en el repositorio de AEM. En un entorno de producción, se recomienda no almacenar datos de formularios en borradores o enviados en el repositorio de AEM. En lugar de ello, debe integrar los borradores y el componente de envío con un almacenamiento seguro, como la base de datos empresarial, para almacenar borradores y datos de formularios enviados.
>
>Para obtener más información, consulte [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md).

## Configurar los borradores y servicios de envíos del portal de formularios {#configuring-forms-portal-drafts-and-submissions-services}

En la configuración de la consola web de AEM ( `https://[host]:'port'/system/console/configMgr`), haga clic para abrir **Configuración de borradores y envíos del portal de formularios** en modo de edición.

Especifique los valores de las propiedades según sus necesidades, tal como se describe a continuación:

### Servicios predeterminados para almacenar datos en instancias de publicación {#out-of-the-box-services-to-store-data-on-publish-instance}

Los datos se replican de forma inversa en la instancia de autor configurada.

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>Servicio de datos de borrador del portal de formularios (Identificador del servicio de datos de borrador (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de metadatos de borrador del portal de formularios (Identificador del servicio de metadatos de borrador (<strong>borrador.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de datos del portal de formularios (identificador para el envío de datos (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de metadatos del portal de formularios (identificador para el envío de metadatos (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Servicios listos para usar para almacenar datos en instancias de procesamiento remotas {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

Los datos se insertan directamente en la instancia remota configurada

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>Servicio de datos de borrador del portal de formularios (Identificador del servicio de datos de borrador (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de metadatos de borrador del portal de formularios (Identificador del servicio de metadatos de borrador (<strong>borrador.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de datos del portal de formularios (identificador para el envío de datos (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Servicio de envío de metadatos del portal de formularios (identificador para el envío de metadatos (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Aparte de la configuración especificada arriba, proporcione información sobre la instancia de procesamiento remoto configurada.

En la configuración de la consola web de AEM ( `https://[host]:'port'/system/console/configMgr`), haga clic para abrir el **Servicio de configuración de AEM DS** en modo de edición. En el cuadro de diálogo Servicio de configuración de AEM DS, proporcione información sobre el procesamiento de la URL del servidor, el nombre de usuario del servidor de procesamiento y la contraseña.

>[!NOTE]
>
>También se proporciona una implementación de muestra para almacenar datos de usuario en una base de datos. Para comprender cómo configurar los servicios de datos y metadatos para almacenar datos de usuario en una base de datos externa, consulte [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md).
