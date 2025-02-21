---
title: Acciones y capacidades de los flujos de trabajo de AEM centrados en Forms en los flujos de trabajo de OSGi y JEE de AEM Forms
description: Acciones y capacidades de los flujos de trabajo de AEM centrados en Forms en los flujos de trabajo de OSGi y JEE de AEM Forms
contentOwner: khsingh
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 96%

---

# Acciones y capacidades de los flujos de trabajo de AEM centrados en Forms en los flujos de trabajo de OSGi y JEE de AEM Forms {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Bandeja de entrada de AEM y espacio de trabajo HTML  {#aem-inbox-and-html-workspace}

Puede utilizar la bandeja de entrada de AEM para ejecutar y supervisar los flujos de trabajo de AEM centrados en Forms en OSGi. Por su parte, HTML Workspace permite ejecutar y supervisar flujos de trabajo JEE de AEM Forms. La siguiente tabla le ayuda a comprender varias acciones importantes disponibles en la bandeja de entrada de AEM para flujos de trabajo de AEM centrados en Forms en OSGi y en el espacio de trabajo HTML para flujos de trabajo JEE de AEM Forms.

<table>
 <tbody>
  <tr>
   <td>Acciones</td>
   <td>Bandeja de entrada de AEM</td>
   <td>Espacio de trabajo HTML</td>
  </tr>
  <tr>
   <td>Iniciar un proceso, tarea o aplicación de formulario<br /> </td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Enviar tareas</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Asignar una tarea a un grupo</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Enviar a varias rutas</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Historial de tareas de seguimiento y resumen de tareas</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Notificaciones por correo electrónico</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Reasignar tareas</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Archivos adjuntos de nivel de campo para formularios adaptables</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Vista de calendario</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Comentarios de nivel de tarea</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Colas (cola personal compartida, Reclamar tareas de la cola)</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Notificación fuera de la oficina</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
    <tr>
   <td>Personalizar elementos de la interfaz de usuario</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Asignar una tarea a varios usuarios</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
 </tbody>
</table>

## Flujos de trabajo de AEM centrados en Forms en flujos de trabajo de OSGi y JEE de AEM Forms {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Flujos de trabajo de AEM centrados en Forms en flujos de trabajo de OSGi y JEE de AEM Forms (AEM Forms en JEE Process Management) tienen un conjunto diferente de capacidades. La siguiente tabla le ayuda a comprender las capacidades importantes disponibles en flujos de trabajo de AEM centrados en Forms en OSGi y en flujos de trabajo JEE en AEM Forms:

<table>
 <tbody>
  <tr>
   <td>Capacidades</td>
   <td>Flujos de trabajo AEM centrados en Forms en OSGi<br /> </td>
   <td>Flujos de trabajo JEE de AEM Forms </td>
  </tr>
  <tr>
   <td>Formularios adaptables</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Integración con otras soluciones de AEM</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Firma manuscrita</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Plantillas de correo electrónico personalizadas</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Definir la prioridad de la tarea</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Tiempo de espera de una tarea después de la fecha de vencimiento</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Bucles dentro del flujo de trabajo</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Selección dinámica de un usuario asignado </td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Usar metadatos personalizados</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Firma electrónica (Adobe Sign)</td>
   <td>Compatible<sup>[1]</sup></td>
   <td>Compatible<sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Administrar aplicaciones de formularios y tareas</td>
   <td>Compatible<sup>[2]</sup><br /> </td>
   <td>Compatible<sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Servicios de documentos</td>
   <td>Compatible<sup>[3]</sup></td>
   <td>Compatible<sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Procesar una tarea completada como formulario adaptable o documento PDF</td>
   <td>Compatible</td>
   <td>Compatible [4]</td>
  </tr>
  <tr>
   <td>Integración con Administración de correspondencia</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
   <tr>
   <td>Portales, SIN ESPERA </td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
   <tr>
   <td>Variables para almacenar datos </td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>OR, Y División</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Avatar del usuario</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Enviar un correo electrónico al final del flujo de trabajo</td>
   <td>Compatible<sup>[7]</sup></td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Llamar a un servicio web desde un flujo de trabajo</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Botón Restablecer</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Fases del flujo de trabajo</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Formularios adaptables de solo lectura</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Ocultar el botón de guardado predeterminado</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Control granular sobre la sección de detalles del flujo de trabajo</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Servicio de sondeo/programación</td>
   <td>Disponible de forma predeterminada</td>
   <td>Implementación personalizada requerida</td>
  </tr>
  <tr>
   <td>Aplicación de formularios adaptables</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Servicio Assembler </td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Servicio Generador de PDF</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Servicio de Forms</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Servicio de salida</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Seguro de documento</td>
   <td>Compatible</td>
   <td>Compatible  </td>
  </tr>
  <tr>
   <td>Ejecutar script</td>
   <td>Admite ECMAScript</td>
   <td>Admite fragmentos de código Java</td>
  </tr>
  <tr>
   <td>Assembler</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>  
  <tr>
   <td>Formularios HTML5, formularios PDF interactivos, Conjunto de formularios</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Informes de procesos</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Categorías de puntos de inicio</td>
   <td>No compatible </td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Aprobación de tareas masivas </td>
   <td>No compatible </td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Guardar borrador con un nombre personalizado</td>
   <td>No compatible </td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Iniciar un proceso con datos de proceso existentes<br /> </td>
   <td>No compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Guardar un punto de partida como borrador</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Vista Administrador</td>
   <td>No compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Buscar conjunto de datos</td>
   <td>No compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Integración con aplicaciones de terceros</td>
   <td>No compatible <sup>[6]</sup></td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Archivos adjuntos de nivel de tarea para la aplicación de flujo de trabajo o el punto de inicio</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Correo electrónico del recordatorio</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Cambiar título en tiempo de espera de tarea</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Correo electrónico en la delegación de tareas y la solicitud de tarea</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Delegar entre grupos separados</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Transformación XSLT</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Prioridad de tareas dinámicas</td>
   <td>No compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Título dinámico</td>
   <td>No compatible</td>
   <td>No compatible</td>
  </tr>
    <tr>
   <td>Descripción dinámica</td>
   <td>No compatible</td>
   <td>No compatible</td>
  </tr>
 </tbody>
</table>

1. Puede utilizar Flujos de trabajo de AEM centrados en Forms en OSGi para firmar un formulario adaptable rellenado. Los flujos de trabajo de AEM centrados en Forms en OSGi son compatibles con la firma fuera del formulario. La experiencia de [firma dentro del formulario](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) no es compatible.

1. Es necesario acceder a la bandeja de entrada de AEM para ejecutar y supervisar los flujos de trabajo centrados en Forms en AEM Forms OSGi y el espacio de trabajo HTML para ejecutar y supervisar los flujos de trabajo JEE de AEM Forms.
1. Los servicios de documentos nativos de AEM Forms están disponibles para los flujos de trabajo de AEM centrados en Forms en OSGi y en los flujos de trabajo JEE de AEM Forms. El flujo de trabajo de AEM utiliza servicios de documentos nativos para flujos de trabajo AEM centrados en Forms en los flujos de trabajo OSGi y JEE de AEM Forms (Process Management).
1. Los flujos de trabajo JEE de AEM Forms solo pueden procesar un formulario adaptable. No admite la representación de un formulario adaptable como documento PDF.
1. Los flujos de trabajo JEE de AEM Forms no tienen un paso independiente para Adobe Sign. Se necesita un formulario adaptable habilitado para Adobe Sign para los flujos de trabajo JEE de AEM Forms. Para obtener más información, consulte [Documentación de Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Puede usar el paso [Invocar el servicio del modelo de datos del formulario](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) paso para invocar un servicio web y publicar o recuperar datos de una aplicación de terceros.
1. Puede usar el paso [Enviar correo electrónico](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) para enviar correos electrónicos.

## Diferencias entre la bandeja de entrada de AEM y las características de la aplicación de AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Dos de las principales formas de iniciar un flujo de trabajo centrado en Forms son la [Bandeja de entrada de AEM](../../forms/using/manage-applications-inbox.md) y la aplicación de AEM Forms. Sin embargo, las capacidades de la bandeja de entrada de AEM y de la aplicación de AEM Forms. La Bandeja de entrada de AEM solo funciona con [flujos de trabajo centrados en Forms](../../forms/using/aem-forms-workflow.md), mientras que la aplicación de AEM Forms funciona tanto con flujos de trabajo centrados en Forms como con la administración de procesos.

La siguiente tabla muestra las capacidades de la bandeja de entrada de AEM y la aplicación de AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Acciones</strong></p> </td>
   <td><p><strong>Bandeja de entrada de AEM</strong></p> </td>
   <td><p><strong>Aplicación de AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Iniciar una aplicación de formulario</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible </p> </td>
  </tr>
  <tr>
   <td><p>Enviar tareas</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible </p> </td>
  </tr>
  <tr>
   <td><p>Delegar tareas</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Historial de tareas de seguimiento y resumen de tareas</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Agregar archivos adjuntos de nivel de tarea</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible </p> </td>
  </tr>
  <tr>
   <td><p>Visualizar archivos adjuntos en el nivel de tarea</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible </p> </td>
  </tr>
  <tr>
   <td><p>Agregar archivos adjuntos de nivel de campo</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible </p> </td>
  </tr>
  <tr>
   <td><p>Visualizar la vista de calendario</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Adición de comentarios</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible </p> </td>
  </tr>
 </tbody>
</table>
