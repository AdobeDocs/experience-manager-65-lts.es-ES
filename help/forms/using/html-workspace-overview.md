---
title: Usar AEM Forms Workspace
description: Familiarícese con AEM Forms Workspace con esta breve descripción general de los flujos de trabajo de proceso.
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
exl-id: 7374797f-4154-402b-bb59-075134763c58
source-git-commit: 823923ab074bae1705cc1991e4079897e4c5cac8
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 97%

---

# Usar AEM Forms Workspace{#working-with-aem-forms-workspace}

## Introducción {#introduction}

AEM Forms Workspace forma parte de AEM Forms. Workspace facilita la representación de formularios HTML y PDF. Ahora puede participar en procesos empresariales desde interfaces móviles y aplicaciones web.

Además, AEM Forms Workspace ofrece un alto grado de personalización mediante HTML estándar y las metodologías de desarrollo de JavaScript™. Se trata de un software basado en componentes que se integra fácilmente con el resto de sus aplicaciones web.

Para obtener más información, consulte [Introducción al espacio de trabajo de AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Primeros pasos {#getting-familiar}

Para familiarizarse con el proceso completo de creación de una aplicación de Forms para automatizar un proceso empresarial, realice el tutorial. Puede crear, administrar y probar una aplicación mediante Workbench, Designer y AEM Forms Workspace después de completar el tutorial. Para obtener más información sobre la implementación, consulte [Creación de la primera aplicación de AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Información general funcional {#functional-overview}

Puede utilizar AEM Forms Workspace para realizar las siguientes tareas:

**Iniciar un proceso empresarial:** AEM Forms Workspace clasifica los procesos según se han diseñado y configurado en la organización. Puede marcar como favoritas las categorías más utilizadas para acceder rápidamente a ellas. Cuando se inicia un proceso, normalmente se rellena un formulario para iniciar un proceso empresarial que controla el flujo de trabajo de Forms. Para obtener más información, consulte [Inicio de procesos](/help/forms/using/starting-processes.md).

**Ver y actuar en tareas:** cuando vea las listas de tareas pendientes, verá las tareas de los procesos empresariales asignadas a usted, a uno de los grupos de los que es miembro, o las tareas compartidas de otros usuarios. Puede abrir, trabajar en las tareas y completarlas según sea necesario. Normalmente, completar una tarea implica proporcionar información y aprobar o rechazar un formulario. Para obtener más información, consulte [Uso de listas de tareas pendientes](/help/forms/using/todo-lists.md).

**Realizar un seguimiento de las tareas**: para realizar un seguimiento de sus tareas, utilice la pestaña Seguimiento de AEM Forms Workspace. Puede buscar procesos activos o completados que haya iniciado o en los que haya participado. Puede ver las tareas, asignaciones y formularios que formaban parte del proceso. También puede iniciar nuevos procesos utilizando los datos de formulario de un proceso que haya iniciado anteriormente. Para obtener más información, consulte [Seguimiento de procesos](/help/forms/using/tracking-processes.md).

## Nueva oferta de AEM Forms Workspace {#new-offering-of-aem-forms-workspace}

**Soporte para la aprobación masiva de tareas**:

puede aprobar varias tareas del mismo tipo. Una vez que seleccione una tarea para aprobarla, solo permanecerán habilitadas las tareas con el mismo proceso, con los mismos nombres y las mismas opciones de ruta. Consulte [Uso de listas de tareas pendientes](/help/forms/using/todo-lists.md) para obtener más información sobre la implementación.

## Migración de espacio de trabajo de Flex a AEM Forms Workspace {#migrating-from-flex-workspace-to-aem-forms-workspace}

Espacio de trabajo de Flex no es compatible con los clientes de AEM Forms. Todos los clientes que utilicen espacio de trabajo de Flex deben trasladarse a AEM Forms Workspace.

En AEM Forms Workspace, los servicios de procesamiento y envío predeterminados del perfil de acción predeterminado asociados a los formularios XDP han cambiado, y se han introducido nuevos servicios. Para obtener más información, consulte [Nuevo servicio de renderización y envío](/help/forms/using/new-render-submit-service.md). Para migrar los procesos existentes, que funcionan con formularios XDP, y para usar estos servicios, puede seguir [estos pasos](new-render-submit-service.md).

**Asignación de las personalizaciones de espacio de trabajo de Flex con AEM Forms Workspace**

La asignación entre varios tipos de personalizaciones en ambos espacios de trabajo es la siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Tipo de personalización </strong></td>
   <td><strong>Personalizaciones cubiertas </strong></td>
   <td><strong>Escenario de personalización de AEM Forms Workspace correspondiente</strong></td>
  </tr>
  <tr>
   <td>Personalización de la localización</td>
   <td>
    <ol>
     <li>Cambio de la configuración regional de Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Cambio de la configuración regional de AEM Forms Workspace</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalizar temáticas</td>
   <td>
    <ol>
     <li>Reemplazo de imágenes</li>
     <li>Modificación de colores</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Cambio del logotipo de la organización</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Cambio del esquema de color</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalización del diseño</td>
   <td>
    <ol>
     <li>Simplificación de la interfaz de usuario de Workspace<br /> </li>
     <li>Crear una nueva pantalla de inicio de sesión</li>
     <li>Creación de un contenedor de aprobación personalizado</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Uso de componentes reutilizables</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Crear una pantalla de inicio de sesión</a></li>
     <li>El contenedor de aprobación está obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Entre las funciones de espacio de trabajo de Flex que no están disponibles en AEM Forms Workspace se encuentran las siguientes: los mensajes y las notificaciones, la página de bienvenida, el contenedor de aprobación y la opción para administrar encabezados de columna. Para obtener una lista completa, consulte [Funciones del espacio de trabajo de Flex no disponibles en AEM Forms Workspace](/help/forms/using/features-flex-workspace-available-html.md).

## Desarrollo con AEM Forms Workspace {#developing-with-aem-forms-workspace}

### Arquitectura {#architecture}

AEM Forms Workspace es una aplicación web basada en HTML y JavaScript™ alojada en CRX™. Cuando se abre la URL de Workspace en un explorador, se accede a un recurso CRX™, y la aplicación se representa como una página HTML en el explorador. Las bibliotecas y el código personalizado de JavaScript administran el comportamiento interno y externo de la aplicación, como la interfaz de usuario, la interacción del usuario y la comunicación con el servidor de AEM Forms. Para obtener más información, consulte [Arquitectura](/help/forms/using/html-workspace-architecture.md) de AEM Forms Workspace.

### Personalización de AEM Forms Workspace {#aem-forms-workspace-customization}

AEM Forms Workspace admite una amplia variedad de personalizaciones para actualizar el diseño de la interfaz de usuario, su apariencia, su funcionalidad, y mucho más. Las personalizaciones implican actualizar una o más de las siguientes opciones:

* Aspectos visuales de la interfaz de usuario
* Funcionalidad mediante personalizaciones semánticas
* Reutilización de componentes HTML en otras aplicaciones web

El artículo [Personalización](introduction-customizing-html-workspace.md#types-of-customizations) explica los tipos de estas personalizaciones.

### Configuración del entorno de desarrollo {#set-up-the-developer-environment}

Las entregas de AEM Forms Workspace incluyen un paquete CRX implementado en CRX, un archivo SDK que contiene el código fuente completo, bibliotecas JavaScript de terceros y scripts de compilación de AEM Forms Workspace. Utilícelos para configurar el entorno de desarrollo y realizar las personalizaciones mencionadas anteriormente. Para obtener más información, consulte [Creación del código de espacio de trabajo de AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

Puede personalizar la mayor parte de la interfaz y las principales funcionalidades, como las fuentes, el esquema de color, el logotipo, la pantalla de inicio de sesión, los cuadros de diálogo de error, la integración con las aplicaciones de terceros y la reutilización de componentes en aplicaciones de terceros. También puede mejorar el contenido mostrado en la página Resumen de tareas, mostrar imágenes para acciones de ruta de tareas e incluso modificar las vistas y los modelos de Backbone de bajo nivel que crea la aplicación de AEM Forms Workspace.

### Representación del HTML de los formularios XDP {#html-rendering-of-xdp-forms}

En cada nuevo proceso, los formularios XDP se representan de forma predeterminada en formato PDF en los equipos de escritorio y en formato HTML en las tabletas. Siempre es posible procesar un formulario XDP en formato HTML. Para obtener más información, consulte [Nuevos servicios de renderización y envío](/help/forms/using/new-render-submit-service.md).

La funcionalidad [Mobile Forms](/help/forms/using/introduction.md), que funciona con [perfiles](/help/forms/using/custom-profile.md), habilita la representación HTML de formularios XDP. De forma predeterminada, la opción &quot;Renderizar nuevo formulario de HTML&quot; utiliza el perfil `default.html`, el cual puede cambiar. También puede agregar cambios personalizados que se produzcan antes de procesar un formulario XDP en formato de HTML.
