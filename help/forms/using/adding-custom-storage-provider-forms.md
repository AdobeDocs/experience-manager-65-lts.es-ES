---
title: Almacenamiento personalizado para borradores y componentes de envíos
description: Consulte cómo personalizar el almacenamiento de datos de usuario para borradores y envíos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
feature: Forms Portal
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 57%

---

# Almacenamiento personalizado para borradores y componentes de envíos {#custom-storage-for-drafts-and-submissions-component}

## Información general {#overview}

AEM Forms permite guardar un formulario como borrador. La funcionalidad de borrador le permite mantener un formulario de trabajo en curso, que puede completar y enviar más tarde desde cualquier dispositivo.

De forma predeterminada, AEM Forms almacena los datos de usuario asociados con el borrador y el envío de un formulario en el nodo `/content/forms/fp` de la instancia de publicación. Además, los componentes del portal de AEM Forms proporcionan servicios de datos, que puede utilizar para personalizar la implementación del almacenamiento de datos de usuario para borradores y envíos. Por ejemplo, puede almacenar datos de usuario en un repositorio de datos.

## Requisitos previos  {#prerequisites}

* Habilitar [componentes del portal de Forms](/help/forms/using/enabling-forms-portal-components.md)
* Crear una [página del portal de Forms](/help/forms/using/creating-form-portal-page.md)
* Habilitar [formularios adaptables para el portal de Forms](/help/forms/using/draft-submission-component.md)
* Más información sobre los [detalles de implementación del almacenamiento personalizado](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Servicio Datos de borrador {#draft-data-service}

Para personalizar el almacenamiento de los datos de usuario para los borradores, debe implementar todos los métodos de la interfaz `DraftDataService`. El siguiente código de ejemplo describe los métodos y argumentos.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null if there is creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

>[!NOTE]
>
>El valor mínimo de la longitud del campo de ID de borrador es de 26 caracteres. Adobe recomienda establecer la longitud de ID de borrador en 26 caracteres o más.

## Servicio Envío de datos {#submission-data-service}

Para personalizar el almacenamiento de los datos de usuario para los envíos, debe implementar todos los métodos de la interfaz `SubmitDataService`. El siguiente código de ejemplo describe los métodos y argumentos.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

El portal de Forms utiliza el concepto de identificador único universal (UUID) para generar un ID único para cada borrador y formulario enviado. También puede generar un ID único propio. Puede implementar la interfaz FPKeyGeneratorService, anular sus métodos y desarrollar una lógica personalizada para generar un ID único personalizado para cada formulario enviado y borrador. Establezca la clasificación del servicio de implementación de generación de ID personalizada más alta que 0. Garantizará que se utilice la implementación personalizada en lugar de la predeterminada.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

Puede utilizar la siguiente anotación para aumentar la clasificación del servicio para el ID personalizado generado con el código anterior:

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

Para utilizar la anotación anterior, importe lo siguiente a su proyecto:

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```
