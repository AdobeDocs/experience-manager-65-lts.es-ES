---
title: Directrices para la resolución de problemas de AEM Forms Workspace
description: Habilitar los registros y utilizar el depurador en el explorador para solucionar problemas de AEM Forms Workspace.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 94%

---

# Directrices para la resolución de problemas de AEM Forms Workspace {#troubleshooting-guidelines-for-aem-forms-workspace}

Este artículo explica cómo depurar AEM Forms Workspace habilitando el registro y utilizando el depurador en un explorador. También se explican algunos problemas comunes que se pueden encontrar al utilizar AEM Forms Workspace y sus soluciones.

## No se puede instalar el paquete de AEM Forms Workspace {#unable-to-install-aem-forms-workspace-package}

Tras instalar el parche, abra AEM Forms Workspace. Si experimenta el error No se encontró ningún recurso, abra el Administrador de paquetes CRX y vuelva a instalar el paquete `adobe-lc-workspace-pkg-<version>.zip`.

Al instalar el paquete, si se produce un error `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, realice los pasos siguientes:

1. Inicie sesión en CRXDE Lite. La URL predeterminada es `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Elimine el siguiente nodo:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Vaya al Administrador de paquetes. La URL predeterminada es `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Busque e instale el paquete `adobe-lc-workspace-pkg-[version].zip`.
1. Reinicie el servidor de aplicaciones.

>[!NOTE]
>
> Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

## Registro de AEM Forms Workspace {#aem-forms-workspace-nbsp-logging}

Puede generar registros en varios niveles para permitir una solución óptima de los errores. Por ejemplo, en una aplicación compleja, el registro en el nivel de componente ayuda a depurar y solucionar problemas de componentes específicos.

En AEM Forms Workspace:

* Para obtener la información de registro sobre un archivo de componente específico, agregue `/log/<ComponentFile>/<LogLevel>` en la dirección URL y pulse `Enter`. Toda la información de registro del archivo de componente en el nivel de registro especificado se imprime en la consola.

* Para obtener la información de registro de todos los archivos de componente, agregue `/log/all/trace` en la dirección URL y pulse `Enter`.

* Formato de registro: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>De forma predeterminada, el nivel de registro de todos los componentes está establecido en INFO.

* El nivel de registro configurado por el usuario se mantiene solamente para esa sesión del explorador. Cuando el usuario actualiza la página, el nivel de registro se establece en su valor inicial para todos los componentes.

### Lista de archivos de componentes en AEM Forms Workspace {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetailsView</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### Niveles de registro disponibles en AEM Forms Workspace {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATAL
* ERROR
* AVISAR
* INFORMACIÓN
* DEPURAR
* ENCONTRAR
* DESACTIVADO

## Depuración de información para exploradores {#debugging-information-for-browsers}

Los scripts y los estilos se pueden depurar en distintos exploradores.

* **Depuración en IE**: Para depurar el espacio de trabajo de AEM Forms en IE, consulte: [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **Depuración en Chrome**: para abrir el depurador en Chrome, use el método abreviado: Ctrl+Mayús+I. Para obtener más información, consulte: [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **Depuración en Firefox**: Hay varios complementos disponibles para depurar scripts y estilos en Firefox. Por ejemplo, Firebug es una de estas utilidades de depuración ([https://getfirebug.com](https://getfirebug.com)).

## Preguntas frecuentes {#faqs}

1. El formulario PDF no se está representando ni enviando en Google Chrome.

   1. Instale el complemento Adobe® Reader®.
   1. En Chrome, abra chrome://plugins para ver los complementos disponibles.
   1. Deshabilite el complemento Visor de PDF de Chrome y habilite el complemento Adobe Reader.

1. El formulario o la guía SWF no se está representando en Google Chrome.

   1. En Chrome, abra chrome://plugins para ver los complementos disponibles.
   1. Consulte los detalles para el complemento Adobe Flash® Player.
   1. Deshabilite PepperFlash en el complemento Adobe Flash Player.

1. He personalizado AEM Forms Workspace, pero no puedo ver los cambios.

   Borre la caché del explorador y, a continuación, acceda al espacio de trabajo de AEM Forms.

1. ¿Qué debe hacer el usuario para permitir que el formulario se represente en HTML al abrirlo en el escritorio?

   Seleccione el botón de opción HTML del perfil predeterminado en el paso asignar tarea mientras utiliza Workbench.

1. Los archivos adjuntos no se muestran cuando se hace clic en ellos.

   Para ver los archivos adjuntos, habilite las ventanas emergentes en el explorador.

1. Un usuario ha iniciado sesión en una aplicación de formularios. Si el usuario intenta iniciar sesión en el espacio de trabajo, es posible que no se cargue si no tiene permisos de espacio de trabajo.

   Cierre sesión en la otra aplicación de formularios y, a continuación, inicie sesión en el espacio de trabajo.

1. Cuando se representan en AEM Forms Workspace los formularios HTML que utilizan propiedades del proceso en su diseño, dentro del formulario se muestra el botón Enviar.

   Cuando se diseñan formularios, al utilizar Propiedades del proceso, dentro del formulario se agrega un botón Enviar. Cuando se representa como PDF en AEM Forms Workspace, el botón Enviar no es visible para el usuario final. Sin embargo, cuando se representa como un formulario HTML en AEM Forms Workspace, el botón Enviar es visible para el usuario final. Al hacer clic en este botón Enviar, dentro del formulario, no se inicia ninguna acción. Al hacer clic en el botón Enviar en la parte inferior de AEM Forms Workspace, fuera del formulario, se completa la tarea.
