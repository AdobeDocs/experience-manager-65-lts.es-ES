---
title: Aplicación de AEM Forms
description: La aplicación de AEM Forms permite a los trabajadores utilizar formularios adaptables en sus dispositivos móviles.
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
exl-id: 9cc83733-630a-4846-bd9e-72fd76a3286d
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '2337'
ht-degree: 95%

---

# Introducción a la aplicación de AEM Forms {#aem-forms-app}

## Información general {#overview}

La aplicación de AEM Forms permite sincronizar formularios adaptables, formularios móviles y conjuntos de formularios en dispositivos móviles, en función del servidor. Puede definir flujos de trabajo que sean [flujos de trabajo centrados en Forms en OSGi](/help/forms/using/aem-forms-workflow.md) <!--or Forms workflows on JEE-->. Por ejemplo, ejecute una empresa bancaria y utilice AEM Forms para administrar las aplicaciones y comunicaciones de los clientes. Sus clientes rellenan un formulario y lo envían para su verificación. Si activa el formulario en dispositivos móviles, los clientes pueden rellenarlo en la aplicación de AEM Forms. También puede administrar el flujo de trabajo de verificación si habilita el formulario de verificación en dispositivos móviles. El trabajador puede llevar un dispositivo móvil al cliente, comprobar los detalles y enviar el formulario. La aplicación de AEM Forms se sincroniza con el servidor de AEM Forms y busca los formularios habilitados para dispositivos móviles. Si la aplicación está sin conexión, los datos se almacenarán localmente.

El código fuente de la aplicación de AEM Forms está disponible para los clientes a través de la distribución de software. El paquete de código fuente de distribución de software está disponible de la siguiente manera: `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

La aplicación de AEM Forms es compatible con dispositivos iOS, Android y Windows. Puede instalar la aplicación de AEM Forms para Android desde Google Play, iOS desde App Store y Windows desde Windows Store.

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms&amp;hl=es)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/es-es/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

Para instalar, personalizar y distribuir la aplicación en dispositivos iOS, Android o Windows, consulte [Personalizar, crear y distribuir la aplicación de AEM Forms](#customize-build-distribute).

## Requisitos previos {#prerequisites}

La aplicación de AEM Forms requiere un servidor de AEM Forms. Los usuarios pueden procesar formularios que se creen en el servidor de AEM Forms, rellenarlos, guardarlos como borradores y enviarlos. La aplicación se conecta al servidor y obtiene de él los formularios habilitados. La aplicación de AEM Forms se sincroniza con el servidor y, en cuanto los formularios se carguen en la aplicación, los usuarios podrán trabajar sin conexión. Si la aplicación está sin conexión, los datos se guardarán en el dispositivo y se sincronizarán con el servidor cuando la aplicación esté en línea.

### Aplicación de AEM Forms con servidores que utilizan AEM Forms Workflow {#aem-forms-app-with-servers-using-aem-forms-workflow}

Si tiene un servidor de flujo de trabajo de AEM Forms, puede procesar formularios como tareas en la aplicación de AEM Forms. Por ejemplo, ejecuta una empresa bancaria y el cliente rellena una solicitud para utilizar los servicios. La solicitud es un formulario adaptable que acepta información de sus clientes y la almacena como un envío para revisarla. El administrador examina la solicitud y envía una solicitud de verificación al trabajador. La aplicación reenviada habilita un formulario de verificación en la aplicación del trabajador como una tarea. El trabajador lleva el dispositivo móvil al cliente y verifica los detalles.

### Aplicación de AEM Forms con servidores que utilizan un flujo de trabajo centrado en Forms en OSGi {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

Si tiene un servidor de AEM Forms, puede procesar formularios adaptables como la aplicación de Bandeja de entrada de AEM y tareas en la aplicación de AEM Forms. Por ejemplo, ejecuta una empresa bancaria y el cliente rellena una solicitud para utilizar los servicios. La aplicación está asociada a un formulario adaptable que acepta información de sus clientes y la almacena como un envío para su revisión. El administrador revisa la tarea y aprueba la solicitud de verificación para el trabajador. El trabajador lleva el dispositivo móvil al cliente y verifica los detalles.

### Formularios independientes o aplicaciones de AEM Forms con servidores sin flujo de trabajo de AEM Forms {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

Un servidor de AEM Forms que no utiliza el flujo de trabajo de AEM Forms es AEM Forms en OSGi, un formulario móvil independiente o un formulario adaptable. La aplicación de AEM Forms funciona con la implementación de AEM Forms en [OSGi](/help/sites-deploying/configuring-osgi.md). Los formularios que habilite y publique para la aplicación de AEM Forms se encontrarán disponibles en la aplicación.

Los formularios se descargan en la aplicación y están disponibles sin conexión. Por ejemplo, ejecuta una empresa bancaria y un cliente rellena una solicitud en su sitio. La solicitud es un formulario adaptable que acepta información de sus clientes y la almacena para revisarla. El administrador revisa el formulario y crea un formulario de verificación en la instancia de autor de AEM. El administrador habilita la sincronización del formulario con la aplicación de AEM Forms y la publica. Si el formulario de verificación está disponible en la aplicación de AEM Forms, su agente de campo puede utilizar un dispositivo móvil para comprobar los detalles del cliente. El dispositivo móvil se sincroniza con el servidor y el formulario de verificación se carga en la aplicación. Su agente de campo puede visitar a su cliente, comprobar los detalles, guardar datos como borrador o enviar el formulario de verificación. El formulario se sincroniza con el servidor siempre que la aplicación esté en línea.

Para sincronizar su formulario en la aplicación de AEM Forms:

1. En la instancia de autor, seleccione un formulario y haga clic en **[!UICONTROL Ver propiedades]**.

1. En la página Propiedades, haga clic en **[!UICONTROL Avanzadas]**.
1. En Avanzadas, habilita la opción: **[!UICONTROL Sincronizar con la aplicación de AEM Forms]** y selecciona **[!UICONTROL Guardar]**.

Cuando se publique el formulario, la aplicación se sincronizará con el servidor y recuperará el formulario. Para sincronizar varios formularios, en la instancia de autor, selecciona varios formularios en el administrador de formularios y selecciona **[!UICONTROL Sincronizar con la aplicación de AEM Forms]**.

<!--

## Mobile device support {#mobile-device-support}

See [AEM Forms app (previously known as Mobile Workspace)](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

-->

## Características principales de la aplicación de AEM Forms {#key-features-of-aem-forms-app}

### Aplicación de AEM Forms con servidores de AEM Forms {#aem-forms-app-with-aem-forms-servers}

Puede sincronizar la aplicación con el servidor de AEM Forms y trabajar con formularios en su dispositivo móvil.

Con el servidor de flujo de trabajo de AEM Forms, un formulario se puede asociar a un punto de inicio en un proceso de área de trabajo y a la aplicación Bandeja de entrada de AEM. La aplicación Bandeja de entrada de AEM puede tener asociado un formulario adaptable. Un punto de inicio puede tener asociado un formulario adaptable, un formulario HTML5 o un conjunto de formularios. Un punto de inicio se puede enviar como tarea o se puede guardar como borrador. <!--For more information on differences between an AEM Inbox application and a startpoint see [Actions and capabilities of Form-centric AEM Workflows on OSGi and AEM Forms JEE workflows](capabilities-osgi-jee-workflows.md).-->

Con el servidor de AEM Forms sin flujo de trabajo de AEM Forms, se procesa en la aplicación de AEM Forms un formulario habilitado para la sincronización en la aplicación. Los formularios están disponibles en la pestaña Formularios de la aplicación y se pueden enviar o guardar como borrador. Los formularios adaptables y los formularios móviles son compatibles con la aplicación.

1. **Guardar una tarea o formulario como borrador**

   La opción Guardar como borrador guarda una captura de pantalla de una tarea o formulario junto con los datos rellenados y los archivos adjuntos en el formulario asociado. Los borradores se guardan en el dispositivo móvil y se sincronizan con el servidor de AEM Forms para recuperarlos más adelante.

   Consulte [Guardar una tarea o formulario como borrador](/help/forms/using/save-as-draft.md).

1. **Guardar formulario como plantilla**

   A veces, cuando los usuarios rellenan un formulario, las entradas de algunos campos son las mismas. Para estas instancias, puede rellenar los campos que requieran valores idénticos en cada caso y guardar el formulario o borrador como plantilla. Cada vez que cree una instancia de plantilla, los campos especificados ya se rellenarán con los valores especificados en la plantilla. Le ahorra tiempo y esfuerzo para rellenar el formulario.

   Consulte [Guardar formularios como plantillas](/help/forms/using/save-forms-and-start-points-as-templates.md).

### Trabajar con tareas y formularios {#working-with-tasks-and-forms}

Puede sincronizar la aplicación con el servidor de flujo de trabajo de AEM Forms y trabajar en tareas y formularios en su dispositivo móvil.

Una tarea en el dispositivo móvil contiene un formulario adaptable, un formulario HTML5 o un conjunto de formularios, y también puede contener archivos adjuntos y [URL de resumen](/help/forms/using/getting-task-variables-summary-url.md). De forma predeterminada, las tareas que se le asignen aparecerán en la carpeta **[!UICONTROL Tareas]**. Al trabajar en una tarea, puede cambiarla y guardar una copia como borrador de la tarea en el servidor de AEM Forms.

Un formulario en el dispositivo móvil puede ser un formulario adaptable o un formulario móvil. Los formularios habilitados para la sincronización en la aplicación de Forms están disponible en la carpeta Formularios. Puede sincronizar formularios habilitados en el servidor de AEM Forms sin el flujo de trabajo de AEM Forms (AEM Forms en OSGi).

Consulte:

* [Abrir una tarea](/help/forms/using/open-task.md)
* [Trabajar con un formulario](/help/forms/using/working-with-form.md)

### Trabajar sin conexión {#working-offline}

Puede trabajar en su dispositivo móvil en el modo sin conexión. Puede iniciar sesión en la aplicación incluso si no hay conexión de red y puede trabajar en todos los formularios sincronizados con el dispositivo cuando estuvo en línea por última vez. Para obtener más información sobre cómo sincronizar los formularios, consulte [Sincronizar la aplicación](/help/forms/using/sync-app.md). Si decide sincronizar los archivos adjuntos asociados a un formulario, también puede abrirlos en el modo sin conexión. Puede editar el formulario, agregar anotaciones y enviar o guardarlo en el modo sin conexión. El formulario se sincronizará con el servidor de AEM Forms la próxima vez que esté en línea.

Para obtener más información, consulte [Trabajar en el modo sin conexión](/help/forms/using/work-offline-mode.md).

### Agregar anotaciones {#adding-annotations}

Puede agregar los siguientes archivos adjuntos a un formulario en su dispositivo móvil

* **Notas**: puede utilizar la función Notas para agregar un garabato a mano alzada o una nota de texto en el formulario. Para obtener más información, consulte [Agregar una nota](/help/forms/using/add-attachments.md#adding-a-note).

* **Imagen**: la aplicación de AEM Forms incluye una función que utiliza la funcionalidad de la cámara o la galería de su dispositivo móvil. Mediante el archivo adjunto fotográfico, puede agregar una fotografía al formulario asociado. Para obtener más información, consulte [Agregar una fotografía](/help/forms/using/add-attachments.md#adding-a-photograph).

### Guardar automáticamente {#autosave}

Cuando un usuario introduce datos en la aplicación de AEM Forms, la función de guardado automático los guarda a intervalos regulares. La función de guardado automático de la aplicación de AEM Forms le ayuda a evitar la pérdida de datos si la aplicación se cierra debido a condiciones como batería reducida.

Consulte [Usar el guardado automático en la aplicación de AEM Forms](/help/forms/using/autosave-data-app.md).

## Diferencias entre la bandeja de entrada de AEM y las características de la aplicación de AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Dos de las principales formas de iniciar un flujo de trabajo centrado en Forms son la [Bandeja de entrada de AEM](/help/forms/using/manage-applications-inbox.md) y la aplicación de AEM Forms. Sin embargo, las capacidades de la bandeja de entrada de AEM y de la aplicación de AEM Forms. La Bandeja de entrada de AEM solo funciona con [flujos de trabajo centrados en Forms](/help/forms/using/aem-forms-workflow.md), mientras que la aplicación de AEM Forms funciona tanto con flujos de trabajo centrados en Forms como con la administración de procesos. <!--For more information on differences between AEM Inbox and AEM Forms app capabilities, see [Actions and capabilities of Form-centric AEM Workflows on OSGi and AEM Forms JEE workflows](capabilities-osgi-jee-workflows.md).-->

## Formularios compatibles {#supported-forms}

Tipos de formularios compatibles con la aplicación de AEM Forms:

### Formulario adaptable {#adaptive-form}

La aplicación de AEM Forms es compatible con formularios adaptables que se adaptan dinámicamente a las entradas del usuario. También son compatibles los formularios adaptables cargados de forma diferida.

### Formulario móvil {#mobile-form}

Puede crear formularios para dispositivos móviles en AEM Forms. Los formularios móviles se representan como formularios HTML en dispositivos móviles que se adaptan a los dispositivos de visualización.

### Conjunto de formularios {#formset}

Los conjuntos de formularios permiten agrupar varios formularios relacionados con un servicio o un proceso para automatizar un proceso empresarial y presentarlos a los usuarios finales. En este caso, los usuarios pueden rellenar todo el conjunto como un único formulario, y no es necesario archivar, enviar ni realizar un seguimiento de los formularios o procesos individuales.

>[!NOTE]
>
>Requiere flujo de trabajo de AEM Forms (AEM Forms en JEE).

## Cómo funciona la aplicación de AEM Forms {#how-aem-forms-app-works}

La aplicación de AEM Forms proporciona una solución móvil para que los trabajadores trabajen en formularios asignados a ellos. La aplicación almacena en la memoria caché todos los datos del servidor y proporciona una experiencia de usuario eficiente al guardar todo el trabajo de manera local. Los datos del disco se envían al servidor mediante actualizaciones de sincronización.

La aplicación de AEM Forms es una aplicación basada en PhoneGap 5.0 en la que el modelo de la red troncal se utiliza de forma eficaz para presentar los datos almacenados en los modelos a través de las vistas. Todas las operaciones nativas se realizan mediante complementos de PhoneGap.

## Personalizar, crear y distribuir la aplicación de AEM Forms {#customize-build-distribute}

>[!NOTE]
>
>Aplicable solo si utiliza el AEM Forms App Source Code para crear la aplicación.

La aplicación de AEM Forms es fácil de personalizar para las necesidades específicas de cada organización. El código fuente de la aplicación se proporciona junto con AEM Forms. Puede cambiar el código fuente y crear su propia solución móvil. También puede firmar la aplicación con su propia clave de empresa.

### Personalizar {#customize}

Puede personalizar la aplicación para lo siguiente:

**Personalización de marca**: cambie el icono de la aplicación, el nombre de la aplicación, las imágenes de inicio y las páginas en la aplicación de AEM Forms. También puede cambiar el texto para localizar la aplicación en una región específica. Para obtener más información sobre la personalización de la marca en la aplicación de AEM Forms, consulte [Personalización de la marca](/help/forms/using/branding-customization.md).

**Temática**: cambie estilos como colores, fuentes y espaciado en la interfaz de usuario de la aplicación de AEM Forms. Para obtener más información, consulte [Personalizar temáticas](/help/forms/using/theme-customization.md).

**Gesto**: cambie los gestos como deslizar a la derecha y deslizar a la izquierda en la interfaz de usuario de la aplicación de AEM Forms. Para obtener más información, consulte [Personalizar gestos](/help/forms/using/gesture-customization.md).

Para obtener más información sobre la personalización de un proyecto de aplicación de AEM Forms, consulte:

* [Configurar el entorno para la aplicación de AEM Forms](/help/forms/using/setup-environment-mobile-workspace.md)
* [Configurar el proyecto de Visual Studio y crear una aplicación de Windows](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [Configurar el proyecto Xcode y crear una aplicación de iOS](/help/forms/using/setup-xcode-project-build-installer.md)
* [Configurar el proyecto Eclipse y crear una aplicación de Android](/help/forms/using/setup-eclipse-project-build-installer.md)

### Crear y distribuir {#build-and-distribute}

El código fuente de la aplicación de AEM Forms se puede extraer del `adobe-lc-mobileworkspace-src.zip` que está disponible como parte del paquete fuente de aplicaciones de AEM Forms en Distribución de software.

Para obtener la fuente de la aplicación de AEM Forms, realice los siguientes pasos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
1. Abra el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

**Para iOS**:

Para obtener más información sobre cómo crear una aplicación de iOS (.ipa), consulte [Configurar el proyecto Xcode y compilar la aplicación de iOS](/help/forms/using/setup-xcode-project-build-installer.md).

Para obtener más información sobre cómo firmar la aplicación de AEM Forms con su perfil de aprovisionamiento, consulte [Configuración, proceso y solución de problemas de iOS Code Signing](https://developer.apple.com/es/support/code-signing/).

**Para Android**:

Para obtener más información sobre cómo crear una aplicación de Android (.apk), consulte [Configurar el proyecto Eclipse y crear una aplicación de Android.](/help/forms/using/setup-eclipse-project-build-installer.md).

Para obtener más información sobre cómo firmar la aplicación de AEM Forms, consulte [Firmar aplicaciones](https://developer.android.com/tools/publishing/app-signing.html).

**Para Windows**:

Para obtener más información sobre cómo crear una aplicación de Windows (.appx), consulte [Configurar el proyecto de Visual Studio y crear una aplicación de Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

Para obtener más información sobre cómo distribuir la aplicación mediante MDM, consulte [Distribuir aplicación de AEM Forms](/help/forms/using/distribute-mobile-workspace-app.md). La distribución de aplicaciones mediante MDM solo es aplicable para iOS y Android.

## Recomendaciones para actualizar el espacio de trabajo móvil en la aplicación de AEM Forms {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

Si actualiza a la última versión de la aplicación de AEM Forms, asegúrese de leer los siguientes puntos:

* **Si ha instalado una versión anterior de la aplicación desde Play Store en Android**
Puede actualizar la aplicación directamente desde Play Store.

* **Si la versión anterior de la aplicación se crea e instala con el código fuente (aplicable para iOS y Android)**:

  Antes de instalar la nueva aplicación, sincronice todos los datos con el servidor de AEM Forms. Una vez sincronizados los datos, desinstale la versión anterior de la aplicación e instale la nueva.
