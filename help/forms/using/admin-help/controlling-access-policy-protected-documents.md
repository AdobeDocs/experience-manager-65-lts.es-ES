---
title: Controlar el acceso a documentos protegidos por directivas
description: Consulte cómo puede ver, administrar y controlar el acceso a sus documentos protegidos por directivas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2167'
ht-degree: 0%

---

# Controlar el acceso a documentos protegidos por directivas {#controlling-access-to-policy-protected-documents}

Puede controlar la forma en que los destinatarios utilizan los documentos protegidos por directivas, independientemente de la amplitud de su distribución.

Mediante la página Documentos puede realizar las siguientes tareas:

* Busque y vea los detalles de documentos protegidos por directivas. Puede ver información sobre el nombre del documento, el nombre del editor, el nombre de la directiva y la fecha en que se aplicó la directiva. Si se elimina la directiva que protegía un documento, también puede ver el ID de directiva eliminado debajo del nombre de la directiva. Los usuarios pueden ver y administrar sus propios documentos protegidos por directivas. Los administradores pueden ver y administrar todos los documentos protegidos por directivas.
* Cambiar los detalles de la directiva aplicada a un documento. Los usuarios pueden editar sus propias directivas, los administradores pueden editar directivas personales y compartidas, y los coordinadores de conjuntos de directivas pueden editar directivas compartidas en los conjuntos de directivas para los que tienen permisos. Puede acceder a la directiva asociada a un documento directamente desde la página Detalles del documento.
* Revocar y restablecer el acceso a un documento protegido por una directiva. Los administradores pueden revocar y restablecer el acceso a cualquier documento. Los coordinadores de conjuntos de directivas (que tienen permiso para administrar documentos) pueden revocar y restablecer el acceso a los documentos protegidos por directivas que utilizan directivas compartidas desde sus conjuntos de directivas. Los usuarios pueden revocar el acceso a sus documentos protegidos por directivas si han creado la directiva que protege el documento o si la directiva es compartida y permite esta capacidad.
* Cambiar la directiva aplicada a un documento. Los usuarios que aplican directivas a los documentos pueden cambiar una directiva si la han creado o si es una directiva compartida la que habilita esta capacidad. Los coordinadores de conjuntos de directivas pueden cambiar las directivas de sus conjuntos de directivas. Los administradores pueden cambiar las directivas aplicadas a cualquier documento.

Cuando un documento está protegido por una directiva y usted anula los privilegios de acceso o cambia la directiva aplicada, los cambios surten efecto de la siguiente manera:

* Si el documento está en línea, los cambios se aplican inmediatamente a menos que el usuario tenga el documento abierto. En este caso, el usuario debe cerrar el documento para que los cambios surtan efecto.
* Si un destinatario utiliza el documento sin conexión (por ejemplo, en un portátil), los cambios surtirán efecto la próxima vez que el destinatario se sincronice con Document Security abriendo cualquier documento protegido por una directiva.

## Ver información sobre un documento {#view-information-about-a-document}

Para cada documento que aparece en la página Documentos, puede ver el nombre del documento, el nombre del editor, el nombre de la directiva y la fecha en la que se protegió el documento. Si se ha eliminado la directiva que protegía un documento, el ID de directiva se enumera en Nombre de directiva.

También puede ver más detalles, que se describen a continuación, sobre un documento concreto en la página Detalles del documento:

>[!NOTE]
>
>Utilice el vínculo Nombre de directiva de la página Detalle del documento para acceder a las directivas generadas automáticamente en Microsoft Outlook para los destinatarios de un documento adjunto a un mensaje de correo electrónico. Estas directivas no aparecen en la página de directivas.

**Nombre de documento:** Nombre del documento seleccionado.

**Id. de documento:** Identificador único que asigna Document Security cuando se aplica una directiva al documento. document security utiliza este número para realizar el seguimiento del documento.

**Estado del documento:** Estado del documento (por ejemplo, activo o revocado).

**Publicador:** Nombre del usuario que adjuntó la directiva al documento.

**Nombre de directiva:** Nombre de la directiva que se usa para proteger el documento. Puede hacer clic en el nombre para abrir la directiva. Utilice este vínculo para acceder a las directivas que Acrobat genera para los destinatarios de un documento adjunto a un mensaje de correo electrónico en Outlook. Estas directivas no aparecen en la página Directivas.

**Tipo de directiva:** Tipo de directiva que se aplicó al documento.

**Fecha de publicación:** Fecha en la que se aplicó la directiva al documento.

**Iteraciones relacionadas:** Si el documento tiene iteraciones relacionadas, este elemento también aparece en la lista. Haga clic en el vínculo para ver la lista de iteraciones relacionadas del documento.

Los usuarios pueden ver información sobre sus documentos protegidos. Los administradores pueden ver información sobre los documentos que cualquier usuario ha protegido con una directiva. Los coordinadores de conjuntos de directivas pueden ver información sobre los documentos protegidos por directivas desde sus conjuntos de directivas.

1. En la página Document Security, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente. Se abre la página Detalle del documento, que muestra información detallada sobre el documento. Esta página también proporciona opciones para revocar el acceso a documentos, cambiar la directiva y ver eventos relacionados con este documento.

## Ver iteraciones relacionadas de un documento {#view-related-iterations-for-a-document}

Si está activado el seguimiento de iteraciones relacionadas, puede realizar el seguimiento de versiones de un documento que varios usuarios hayan guardado. Esta función solo es compatible con determinadas aplicaciones, como PTC Pro/ENGINEER Wildfire.

Esta función es útil cuando varios usuarios están colaborando y están guardando distintas versiones del mismo documento. document security puede realizar un seguimiento de las distintas iteraciones; por lo tanto, puede ver fácilmente la información del documento para las diferentes versiones.

Si esta función está activada, puede ver las iteraciones relacionadas de un documento desde la página Documentos.

1. Permite ver la página de detalles del documento. (Vea [Ver información acerca de un documento](controlling-access-policy-protected-documents.md#view-information-about-a-document).)
1. Haga clic en Ver iteraciones relacionadas. La opción solo está disponible si la función está habilitada. Aparecerá la lista de iteraciones relacionadas. Para cada iteración, puede ver la siguiente información:

   * **Iteración:** El nombre de archivo. Puede ser diferente del nombre de archivo original y tiene un número de versión anexado al final.
   * **Editor:** El editor del documento original.
   * **Creado por:** El usuario que guardó la iteración.
   * **Fecha de creación:** La fecha y hora en que se guardó la iteración.
   * **Directiva:** Directiva que protege la iteración. Las distintas iteraciones pueden estar protegidas por distintas directivas.

1. Para mostrar la página Detalle del documento para esa iteración, haga clic en el nombre de archivo de una iteración.

## Revocar y restablecer el acceso a los documentos {#revoking-and-reinstating-access-to-documents}

Puede revocar y restablecer el acceso a documentos protegidos por directivas:

**Usuarios:** pueden revocar o restablecer el acceso a los documentos que protegen con sus propias directivas personales o con directivas compartidas para las que la capacidad de revocar está habilitada para el usuario que aplica la directiva. Los usuarios que no puedan revocar el acceso a un documento o cambiar una directiva deben ponerse en contacto con el administrador.

**Administradores:** pueden revocar o restablecer los privilegios de acceso a cualquier documento protegido por una directiva, incluidos los protegidos por directivas personales o compartidas. Si un administrador anula el acceso a un documento protegido con una directiva compartida, solo un administrador puede restablecer los privilegios de acceso para ese documento.

**Coordinadores de conjuntos de directivas:** pueden revocar o restablecer los privilegios de acceso para los documentos que protegen las directivas de sus conjuntos de directivas.

Al revocar o restablecer los privilegios de acceso a documentos, el cambio surte efecto en estos momentos:

* Si el documento está en línea y cerrado, el cambio surtirá efecto la próxima vez que el destinatario se sincronice con Document Security abriendo un documento protegido por una directiva.
* Si el documento está en línea y abierto, el cambio surte efecto cuando el destinatario cierra el documento.
* Si el documento está sin conexión (es decir, está en uso sin conexión a Internet, como en un equipo portátil), el cambio surtirá efecto la próxima vez que el destinatario se sincronice con Document Security.

**Revocar acceso a un documento protegido por una directiva**

1. En la página Document Security, haga clic en Documentos.
1. Seleccione la casilla de verificación situada junto al documento correspondiente y haga clic en Revocar. Puede revocar el acceso a varios documentos a la vez.
1. Seleccione un mensaje para mostrar a los usuarios que intenten abrir el documento después de revocarlo:

   * **Mensaje general:** Indica que el autor revocó el documento
   * **Documento finalizado:** Indica que el autor terminó el documento
   * **Documento revisado**: indica que el autor revisó el documento

1. (Opcional) Si hay disponible una versión más reciente del documento, introduzca la dirección URL y haga clic en Probar para comprobar la dirección URL.
1. Haga clic en Aceptar y, a continuación, en Aceptar de nuevo para volver a la página Documentos.

**Restablecer privilegios de acceso a documentos**

1. En la página Document Security, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente.
1. Haga clic en Anular revocación y luego en Aceptar.

## Cambiar una directiva aplicada a un documento {#switch-a-policy-that-is-applied-to-a-document}

Los usuarios, coordinadores de conjuntos de directivas y administradores pueden cambiar la directiva aplicada a un documento protegido por una directiva (sólo se puede aplicar una directiva a la vez a un documento). Los usuarios pueden cambiar directivas que se aplican a sus propios documentos protegidos por directivas si los han creado o si la directiva es una directiva compartida que tiene esta capacidad habilitada. De lo contrario, el administrador o el coordinador de conjuntos de directivas deben cambiar la directiva. Los administradores pueden cambiar las directivas de cualquier documento protegido por directivas del usuario. Los coordinadores de conjuntos de directivas pueden cambiar las directivas de sus conjuntos de directivas.

Al cambiar una directiva, la nueva directiva se aplica de la siguiente manera:

* Si el documento está en línea y cerrado, el cambio surtirá efecto la próxima vez que el destinatario se sincronice con Document Security abriendo en línea cualquier documento protegido por una directiva.
* Si el documento está en línea y abierto, el cambio surtirá efecto cuando el usuario cierre el documento.
* Si el documento está sin conexión (en uso sin una conexión activa a Internet o a la red, como en un equipo portátil), el cambio se aplicará la próxima vez que el usuario realice la sincronización con Document Security abriendo en línea un documento protegido por directivas.

>[!NOTE]
>
>Para permitir el acceso anónimo a un documento protegido por una directiva que actualmente no tiene este acceso, quite la directiva existente en la aplicación cliente y, a continuación, aplique una directiva que permita el acceso anónimo. Si cambia la directiva, los usuarios deben iniciar sesión para acceder al documento.

1. En la página Document Security, haga clic en Documentos.
1. En la lista de documentos, haga clic en el documento correspondiente.
1. Haga clic en Cambiar directiva. Aparecerá una lista de hasta 100 directivas.
1. Si no se muestra la directiva que desea, seleccione Nombre o Id. de directiva en la lista Buscar, escriba el nombre o Id. y haga clic en Buscar.
1. Haga clic en una directiva nueva de la lista.
1. Haga clic en Cambiar directiva y, a continuación, en Aceptar para volver a la página Documentos.

## Buscar un documento {#search-for-a-document}

Puede buscar documentos en la página Documentos usando una combinación de criterios de intervalo de fechas y los criterios de búsqueda disponibles en la lista. Estos criterios incluyen el nombre del documento, el nombre de la directiva o todos los documentos.

Algunas opciones de búsqueda adicionales solo están disponibles para los administradores:

**Id. de documento:** número de Id. único que Document Security asigna al documento cuando se aplica la directiva.

**Nombre de documento:** Nombre del documento.

**Nombre del editor:** Nombre del usuario que adjuntó la directiva al documento. Puede seleccionar el usuario de todos los dominios o de un dominio especificado.

**Id. de directiva:** número de id. de la directiva adjunta al documento.

**Nombre de directiva:** Nombre de la directiva adjunta al documento.

**Todos los documentos:** Todos los documentos protegidos por administradores y usuarios. El uso de la opción Todos los documentos para buscar puede devolver una larga lista de documentos.

1. En la página Document Security, haga clic en Documentos.
1. En la lista Buscar, seleccione los criterios de búsqueda necesarios.

   Puede especificar los criterios como ID de documento, nombre de documento, nombre del editor, ID de directiva, nombre de directiva o todos los documentos.

   Si especifica el nombre del editor, haga clic en el icono Libreta de direcciones y especifique el dominio en el que desea buscar al usuario. A continuación, haga clic en Aceptar para volver a la página de búsqueda Documentos.

1. (Opcional) En la lista Fecha, seleccione una opción de intervalo de fechas. Si selecciona Fechas personalizadas, escriba la fecha en formato aaaaa/mm/dd en los cuadros que aparecen o utilice el Selector de fecha para especificar el intervalo de fecha:

   * Haga clic en el calendario para abrir el Selector de fecha.
   * Utilice las flechas para buscar un año y un mes.
   * Haga clic en un día del mes del calendario.
   * Haga clic en Aceptar para cerrar el Selector de fecha.

1. Haga clic en Buscar.

## Ordenar la lista de documentos {#sort-the-document-list}

Puede ordenar la lista de documentos por encabezados de columna. Los iconos de triángulo junto al encabezado de la columna indican qué columna se utiliza actualmente para ordenar. Un triángulo que señala hacia arriba indica un orden ascendente, mientras que un triángulo que señala hacia abajo indica un orden descendente.

1. En la página Document Security, haga clic en Documentos.
1. Haga clic en el encabezado de columna correspondiente.
1. Para cambiar el orden, vuelva a hacer clic en la columna.

## Agregar portada a documentos protegidos por directivas {#add-cover-page-to-policy-protected-documents}

Si hay la mayoría de visores que no son de Adobe PDF, si abre un documento protegido por Document Security, la primera página se muestra como una página en blanco o la aplicación se interrumpe sin abrir el documento.

Puede utilizar la compatibilidad con la Página 0 (Documento envolvente) para permitir que los visualizadores que no sean de Adobe PDF abran un documento protegido y muestren una portada en el documento.

>[!NOTE]
>
>Al ver estos documentos (que contienen una Página 0) en Adobe Reader/Acrobat o Mobile Reader, el documento protegido se abre de forma predeterminada.

**Para agregar portada a un documento protegido por una directiva**

Utilice los siguientes procesos en Workbench:

**Proteger
Documento con portada:** protege un documento de PDF con la directiva especificada y agrega una portada al documento

**Extraer documento protegido:** Extrae el documento de PDF protegido por directivas del documento de PDF con portada

Utilice las siguientes API de Document Security:

**protectDocumentWithCoverPage:** protege un PDF determinado con la directiva especificada y devuelve un documento con una portada y el documento protegido como datos adjuntos
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** extrae el documento protegido que es un archivo adjunto en el documento con portada. El documento con la portada se puede crear mediante el método protectDocumentWithCoverPage
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
