---
title: Integración de aplicaciones de terceros en AEM Forms Workspace
description: Integre aplicaciones de terceros como Administración de correspondencia en AEM Forms Workspace.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 80%

---

# Integración de aplicaciones de terceros en AEM Forms Workspace{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms Workspace admite la administración de las actividades de asignación y finalización de tareas en formularios y documentos. Estos formularios y documentos pueden ser formularios XDP, formularios de Flex® o guías (obsoletos) que se han procesado en los formatos XDP, PDF, HTML o Flex.

Estas capacidades se han mejorado aún más. AEM Forms ahora admite la colaboración con aplicaciones de terceros compatibles con funciones similares a las de AEM Forms Workspace. Uno de los aspectos comunes de estas funcionalidades son los flujos de trabajo de asignación y posterior aprobación de tareas. AEM Forms proporciona una experiencia unificada única para los usuarios empresariales de AEM Forms, de modo que todas estas asignaciones de tareas o aprobaciones para las aplicaciones compatibles se puedan administrar a través de AEM Forms Workspace.

Por ejemplo, consideremos Administración de correspondencia como el candidato de muestra para la integración con AEM Forms Workspace. Administración de correspondencia incluye el concepto de &quot;carta&quot;, la cual puede procesarse y permite realizar acciones.

## Crear recursos de Administración de correspondencia {#create-correspondence-management-assets}

Comience creando una plantilla de Administración de correspondencia de ejemplo que se procese en AEM Forms Workspace. Para obtener más información, consulte [Creación de una plantilla de carta](../../forms/using/create-letter.md).

Acceda a la plantilla de Administración de correspondencia en su URL para comprobar que se puede procesar correctamente. La URL tiene un patrón similar al siguiente: `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`,

Donde `encodedLetterId` es el ID de carta con codificación URL. Especifique el mismo ID de carta a la hora de definir el proceso de representación para la tarea de Workspace en Workbench.

## Creación de una tarea para procesar y enviar una carta en AEM Workspace {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

Antes de ejecutar estos pasos, asegúrese de que es miembro de los siguientes grupos:

* cm-agent-users
* Workspace Users

Para obtener más información, consulte [Adición y configuración de usuarios](/help/forms/using/admin-help/adding-configuring-users.md).

Siga estos pasos para crear una tarea para procesar y enviar una carta en AEM Workspace:

1. Inicie Workbench. Inicie sesión en localhost como administrador.
1. Haga clic en Archivo > Nuevo > Aplicación. En el campo Nombre de la aplicación, introduzca `CMDemoSample` y, a continuación, haga clic en Finalizar.
1. Seleccione `CMDemoSample/1.0` y haga clic con el botón derecho en `NewProcess`. En el campo de nombre, introduzca `CMRenderer` y, a continuación, haga clic en Finalizar.
1. Arrastre el selector de actividades de Punto de inicio y configúrelo:

   1. En Datos de presentación, seleccione Usar un recurso CRX.

      ![Usar-recurso-CRX](assets/useacrxasset.png)

   1. Busque un recurso. En el cuadro de diálogo Seleccionar recurso de formulario, la pestaña Cartas muestra todas las cartas del servidor.

      ![Pestaña Carta](assets/letter_tab_new.png)

   1. Seleccione la carta adecuada y haga clic en **Aceptar**.

1. Haga clic en Administrar perfiles de acción. Aparecerá el cuadro de diálogo Administrar perfil de acción. Asegúrese de que las opciones Procesar y Enviar procesos están correctamente seleccionadas.
1. Para abrir la carta con un archivo XML de datos, busque y seleccione el archivo de datos correspondiente en el Proceso de preparación de datos.
1. Haga clic en Aceptar.
1. Defina las variables para la salida del punto de inicio y los archivos adjuntos de la tarea. Las variables definidas contienen datos de salida del punto de inicio y datos adjuntos de la tarea.
1. (Opcional) Para agregar otro usuario al flujo de trabajo, arrastre un selector de actividades, configúrelo y asígnelo a un usuario. Escriba un contenedor personalizado (a continuación se muestra un ejemplo) o descargue e instale el DSC (el cual aparece más abajo) para la plantilla de carta exacta, la salida del punto de inicio y los archivos adjuntos de la tarea.

   A continuación, se muestra un ejemplo de contenedor personalizado:

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [Obtener archivo](assets/dscsample.zip)
Descargar DSC: hay disponible un DSC de ejemplo en el archivo DSCSample.zip adjunto anteriormente. Descargue y descomprima el archivo DSCSample.zip. Antes de utilizar el servicio DSC, debe configurarlo. Consulte [Configurar el servicio DSC](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p).

   En el cuadro de diálogo Definir actividad, seleccione la actividad adecuada, como getLetterInstanceInfo, y haga clic en **Aceptar**.

1. Implemente la aplicación. Si se le solicita, inicie sesión y guarde los recursos.
1. Inicie sesión en AEM Forms Workspace en https://&#39;[server]:[port]&#39;/lc/content/ws.
1. Abra la tarea que ha agregado, CMRenderer. Aparecerá la carta de Administración de correspondencia.

   ![cminworkspace](assets/cminworkspace.png)

1. Rellene los datos necesarios y envíe la carta. La ventana se cierra. En este proceso, la tarea se asigna al usuario especificado en el flujo de trabajo en el paso 9.

   >[!NOTE]
   >
   >El botón Enviar no está habilitado hasta que no se rellenan todas las variables obligatorias de la carta.
