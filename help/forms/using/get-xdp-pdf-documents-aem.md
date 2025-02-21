---
title: Obtener documentos XDP y PDF en AEM Forms
description: AEM Forms permite cargar formularios y recursos compatibles para utilizarlos con formularios adaptables. También puede cargar formularios de forma masiva y recursos relacionados como ZIP.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 95%

---

# Obtener documentos XDP y PDF en AEM Forms{#getting-xdp-and-pdf-documents-in-aem-forms}

## Información general {#overview}

Puede importar formularios desde el sistema de archivos local al repositorio CRX cargándolos en AEM Forms. La operación de carga es compatible con los siguientes tipos de recursos:

* Plantillas de formulario (formularios XFA)
* Formularios PDF
* Documento (documentos PDF planos)

Puede cargar los tipos de recursos compatibles de forma individual o como un archivo ZIP. Puede cargar un recurso del tipo `Resource`, solo junto con un formulario XFA en un archivo ZIP.

>[!NOTE]
>
>Asegúrese de que es miembro del grupo `form-power-users` para poder cargar archivos XDP. Póngase en contacto con su administrador para convertirse en miembro del grupo.

## Carga de formularios {#uploading-forms}

1. Inicie sesión en la interfaz de usuario de AEM Forms accediendo a `https://'[server]:[port]'/aem/forms.html`.
1. Vaya a la carpeta en la que desea cargar el formulario o la carpeta que contiene los formularios.
1. En la barra de herramientas de acciones, seleccione **Crear > Cargar archivo**.

   ![Archivos en la opción de almacenamiento local en Crear](assets/step.png)

1. El cuadro de diálogo Cargar formularios o paquetes permite examinar y elegir el archivo que desea cargar. El explorador de archivos solo muestra los formatos de archivo compatibles (ZIP, XDP y PDF).

   >[!NOTE]
   >
   >Un nombre de archivo solo puede contener caracteres alfanuméricos, guiones o guiones bajos.

1. Haga clic en Cargar después de seleccionar el archivo para cargar los archivos o haga clic en Cancelar para cancelar la carga. Una ventana emergente muestra los recursos que se agregan y los que se actualizan en la ubicación actual.

   >[!NOTE]
   >
   >Para un archivo ZIP, se muestran las rutas relativas de todos los recursos compatibles. Los recursos que no sean compatibles dentro del ZIP se ignoran y no aparecen en la lista. Sin embargo, si el archivo ZIP contiene solo los recursos no compatibles, se muestra un mensaje de error en lugar del cuadro de diálogo emergente. 


   ![Cuadro de diálogo Cargar al cargar un formulario XFA](assets/upload-scr.png)

1. Si uno o varios recursos tienen un nombre de archivo no válido, se muestra un error. Corrija los nombres de archivo resaltados en rojo y vuelva a cargarlos.

   ![Mensaje de error al cargar un formulario XFA](assets/upload-scr-err.png)

Una vez finalizada la carga, un flujo de trabajo en segundo plano genera miniaturas para todos los recursos en función de la previsualización de cada uno. Las versiones más recientes de los recursos, si se cargan, reemplazan los recursos existentes.

### Modo protegido {#protected-mode}

El servidor de AEM Forms permite ejecutar código JavaScript. Un código JavaScript malintencionado puede dañar un entorno de AEM Forms. El modo protegido restringe AEM Forms de forma que ejecute archivos XDP únicamente desde recursos y ubicaciones de confianza. Todos los XDP disponibles en la interfaz de usuario de AEM Forms se consideran recursos de confianza.

El modo protegido está activado de forma predeterminada. Si es necesario, puede desactivar el modo protegido:

1. Inicie sesión en la consola web de AEM como administrador. La URL es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Abra Configuraciones de Mobile Forms para editarlas.
1. Anule la selección de la opción Modo protegido y haga clic en **Guardar**. El modo protegido está desactivado.

## Actualización de formularios XFA a los que se hace referencia {#updating-referenced-xfa-forms}

En AEM Forms, se puede hacer referencia a una plantilla de formulario XFA mediante un formulario adaptable u otra plantilla de formulario XFA. Además, una plantilla puede hacer referencia a un recurso u otra plantilla XFA.

Un formulario adaptable que hace referencia a un XFA tiene sus campos enlazados con los campos disponibles en el XFA. Al actualizar una plantilla de formulario, el formulario adaptable asociado intenta sincronizarse con el XFA. Para obtener más información, consulte [Sincronización de formularios adaptables con el XFA asociado](../../forms/using/synchronizing-adaptive-forms-xfa.md).

Al quitar una plantilla de formulario, se corrompe el formulario adaptable o la plantilla de formulario dependientes. Algunas veces, a este tipo de formularios adaptables se les denomina informalmente &quot;formularios sucios&quot;. Puede buscar formularios sucios en la interfaz de usuario de AEM Forms de las dos formas siguientes.

* Se muestra un icono de advertencia en la miniatura del formulario adaptable de la lista de recursos, y al situar el puntero sobre él, aparece el siguiente mensaje.\
  `Schema/Form Template for this adaptive form has been updated so go to Authoring mode and rebase it with new version.`

![Advertencia para un formulario adaptable sin sincronizar después de actualizar el XFA asociado](assets/dirtyaf.png)

Se mantiene un indicador para mostrar que se trata de un formulario sucio. Esta información está disponible en la página de propiedades del formulario junto con sus metadatos. La propiedad de metadatos `Model Refresh` muestra el valor `Recommended` únicamente en el caso de los formularios adaptables sucios.

![Indicación de que un formulario adaptable no está sincronizado con el modelo XFA](assets/model-refresh.png)
