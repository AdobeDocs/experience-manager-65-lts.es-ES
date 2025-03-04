---
title: Instalación y configuración de un flujo de trabajo centrado en Forms de OSGi
description: Instale y configure AEM Forms Interactive Communications para crear correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida.
topic-tags: installing
docset: aem65
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication,AEM Forms on OSGi
source-git-commit: 168cb023768ff3139937ab7f437ab7d00185bca0
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 97%

---

# Instalación y configuración de un flujo de trabajo centrado en Forms de OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Introducción {#introduction}

Las empresas recopilan y procesan datos de varios formularios, sistemas back-end y otras fuentes de datos. El procesamiento de datos implica procedimientos de revisión y aprobación, tareas repetitivas y el archivo de datos; por ejemplo, al revisar un formulario y convertirlo en un documento PDF. Cuando se realizan manualmente, las tareas repetitivas pueden llevar mucho tiempo y muchos recursos.

Puede usar el [flujo de trabajo centrado en Forms de OSGi](../../forms/using/aem-forms-workflow.md) para crear rápidamente flujos de trabajo basados en formularios adaptables. Estos flujos de trabajo pueden ayudarle a automatizar los flujos de trabajo de revisión y aprobación, los flujos de trabajo de procesos empresariales y otras tareas repetitivas. Estos flujos de trabajo también ayudan a procesar documentos (crear, ensamblar, distribuir y archivar documentos PDF, agregar firmas digitales para limitar el acceso a documentos, descodificar formularios con códigos de barras, etc.) y utilizar el flujo de trabajo de firma de Adobe Sign con formularios y documentos.

Una vez configurados, estos flujos de trabajo se pueden activar manualmente para completar un proceso definido o ejecutarse programáticamente cuando los usuarios envíen un formulario o una comunicación interactiva. La capacidad está incluida en el paquete de complementos de AEM Forms.

AEM Forms es una potente plataforma de clase empresarial. El flujo de trabajo centrado en Forms de OSGi es solo una de las capacidades de AEM Forms. Para obtener la lista completa de capacidades, consulte [Introducción a AEM Forms](introduction-aem-forms.md).

>[!NOTE]
>
>Con el flujo de trabajo centrado en Forms de OSGi, puede generar e implementar rápidamente flujos de trabajo para diversas tareas en la pila OSGi, sin tener que instalar la capacidad Process Management completa en la pila JEE. Consulte una [comparación](capabilities-osgi-jee-workflows.md) de los flujos de trabajo de AEM centrados en Forms de OSGi y Process Management en JEE para conocer las diferencias y similitudes en las capacidades.
>
>Después de la comparación, si decide instalar la capacidad Process Management en la pila de JEE, consulte [Instalación o actualización de AEM Forms en JEE](/help/forms/using/introduction-aem-forms.md) para obtener información detallada sobre la instalación y configuración de la pila JEE y las funcionalidades de Process Management.

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Lo único que necesita es disponer al menos de una instancia de autor o procesamiento (autor de producción) de AEM para ejecutar el flujo de trabajo centrado en Forms en la capacidad OSGi. Una instancia de procesamiento es una instancia de [autor de AEM protegida](/help/forms/using/hardening-securing-aem-forms-environment.md). No realice ninguna tarea de creación real, como la creación de flujos de trabajo o formularios adaptables, en el autor de producción.

A continuación, encontrará una topología de carácter orientativo para ejecutar AEM Forms Interactive Communications, Administración de correspondencia, AEM Forms Data Capture y el flujo de trabajo centrado en Forms en las capacidades OSGi. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología-recomendada](assets/recommended-topology.png)

El flujo de trabajo centrado en Forms de AEM Forms en OSGi ejecuta la Bandeja de entrada de AEM y la interfaz de usuario del modelo de flujo de trabajo en las instancias de autor de AEM Forms.

## Requisitos del sistema {#system-requirements}

>[!NOTE]
>
>Pase a la sección [Pasos siguientes](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) del documento si ya ha instalado AEM Forms en OSGi como se explica en el artículo [Instalación y configuración de las capacidades de captura de datos](../../forms/using/installing-configuring-aem-forms-osgi.md).

Antes de empezar a instalar y configurar el flujo de trabajo centrado en Forms de OSGi, asegúrese de lo siguiente:

* Se ha implementado la infraestructura de hardware y software. Para obtener una lista detallada del hardware y el software compatibles, consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En la terminología de AEM, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en el modo Autor o Publicación. Se necesita al menos una instancia de AEM (de autor o procesamiento) para ejecutar el flujo de trabajo centrado en Forms de OSGi:

   * **Autor**: la instancia de AEM utilizada para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para su publicación, se replica en la instancia de publicación.
   * **Procesamiento:** una instancia de procesamiento es una instancia de [autor de AEM protegida](/help/forms/using/hardening-securing-aem-forms-environment.md). Puede configurar una instancia de autor y protegerla después de realizar la instalación.

   * **Publicación**: la instancia de AEM que sirve el contenido publicado al público a través de Internet o de una red interna.

* Se cumplen los requisitos de memoria. El paquete de complementos de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft Windows.
   * 6 GB de espacio temporal para instalaciones basadas en UNIX.

* Requisitos adicionales para sistemas basados en UNIX: si está utilizando un sistema operativo basado en UNIX, instale los siguientes paquetes desde los medios de instalación del sistema operativo correspondiente.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Instalación del paquete de complementos de AEM Forms {#install-aem-forms-add-on-package}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene un flujo de trabajo centrado en Forms de OSGi y otras capacidades. Siga estos pasos para instalar el paquete de complementos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
1. Abra el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65-lts/administering/contentmanagement/package-manager.html) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

   También puede descargar el paquete a través del vínculo directo que aparece en el artículo [Versiones de AEM Forms](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html).

1. Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No reinicie el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere a que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTERED dejen de aparecer en el archivo [AEM-Installation-Directory]/crx-quickstart/logs/error.log y el registro sea estable.

   >[!NOTE]
   >
   > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

1. Repita los pasos del 1 al 7 en todas las instancias de autor y publicación.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

AEM Forms incluye algunas configuraciones obligatorias y otras opcionales. Entre las configuraciones obligatorias se incluyen la configuración de las bibliotecas BouncyCastle y el agente de serialización. Entre las configuraciones opcionales se incluyen la configuración de Dispatcher y Adobe Target.

### Configuraciones posteriores a la instalación obligatorias {#mandatory-post-installation-configurations}

#### Configuración de las bibliotecas RSA y BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Realice los siguientes pasos en todas las instancias de autor y publicación para iniciar y delegar las bibliotecas:

1. Detenga la instancia de AEM subyacente.
1. Abra el [directorio de instalación de AEM]\crx-quickstart\conf\sling.properties para editarlo.

   Si usa el [directorio de instalación de AEM]\crx-quickstart\bin\start.bat para iniciar AEM, edite el archivo sling.properties ubicado en [AEM_root]\crx-quickstart\.

1. Agregue las siguientes propiedades al archivo sling.properties:

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Guarde y cierre el archivo e inicie la instancia de AEM.
1. Repita los pasos del 1 al 4 en todas las instancias de autor y publicación.

#### Configuración del agente de serialización {#configure-the-serialization-agent}

Siga estos pasos en todas las instancias de autor y publicación para incluir el paquete en la lista de permitidos:

1. Abra el Administrador de configuración de AEM en una ventana del explorador. La URL predeterminada es https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Busque y abra **Deserialización de la configuración de Firewall**.
1. Agregue el paquete **sun.util.calendar** en el campo **Lista de permitidos**. Haga clic en Guardar.
1. Repita los pasos del 1 al 3 en todas las instancias de autor y publicación.

### Configuraciones posteriores a la instalación opcionales {#optional-post-installation-configurations}

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher es una herramienta de almacenamiento en caché y equilibrio de carga de AEM. AEM Dispatcher también contribuye a proteger el servidor de AEM de ataques. Puede reforzar la seguridad de su instancia de AEM mediante Dispatcher y un servidor web de clase empresarial. Si usa [Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher-configuration.html), realice las siguientes configuraciones en AEM Forms:

1. Configure el acceso en AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y agregue el siguiente filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre los filtros, consulte la [documentación de Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configure el servicio del Filtro de referente:

   Inicie sesión en el Administrador de configuración de Apache Felix como administrador. La URL predeterminada del Administrador de configuración es https://&#39;server&#39;:[port_number]/system/console/configMgr.  En el menú **Configuraciones**, seleccione la opción **Filtro de referente de Apache Sling**. En el campo Permitir hosts, introduzca el nombre de host de Dispatcher para permitirlo como referente y haga clic en **Guardar**. El formato de la entrada es `https://'[server]:[port]'`.

#### Configurar la caché {#configure-cache}

Una caché es un mecanismo para acortar los tiempos de acceso los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de los formularios adaptables almacena únicamente el contenido HTML y la estructura JSON de un formulario adaptable sin guardar los datos rellenados previamente. Esto contribuye a reducir el tiempo necesario para representar un formulario adaptable.

* Cuando utilice la caché de los formularios adaptables, utilice [AEM Dispatcher](https://helpx.adobe.com/es/experience-manager/dispatcher/using/dispatcher-configuration.html) para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* A la hora de desarrollar componentes personalizados, mantenga deshabilitada la caché de los formularios adaptables en el servidor utilizado para el desarrollo.

Realice los siguientes pasos para configurar la caché de los formularios adaptables:

1. Vaya al Administrador de configuración de la consola web de AEM en `https://'[server]:[port]'/system/console/configMgr`.
1. Haga clic en **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]** para editar sus valores de configuración. En el cuadro de diálogo Editar valores de configuración, especifique el número máximo de formularios o documentos que una instancia del servidor de AEM Forms puede almacenar en caché en el campo **Número de formularios adaptables**. El valor predeterminado es 100. Haga clic en **Guardar**.

   >[!NOTE]
   >
   >Para deshabilitar la caché, establezca el valor del campo Número de formularios adaptables en **0**. La caché se restablece y todos los formularios y documentos se eliminan de ella cuando se desactiva o cambia su configuración.

#### Configuración de Adobe Sign {#configure-adobe-sign}

Adobe Sign permite los flujos de trabajo de firma electrónica en los formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para el área legal, ventas, nóminas, administración de recursos humanos y muchas más.

Normalmente, en los flujos de trabajo de Adobe Sign centrados en Forms de OSGi, un usuario cumplimenta un formulario adaptable para **solicitar un servicio**. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de solicitud para una prestación. Cuando un usuario cumplimenta, envía y firma el formulario de solicitud, se inicia un flujo de trabajo de aprobación/rechazo. El proveedor de servicio revisa la solicitud en la Bandeja de entrada de AEM y utiliza Adobe Sign para firmar electrónicamente la solicitud. Para habilitar este tipo de flujos de trabajo de firma electrónica, puede integrar Adobe Sign con AEM Forms.

Para usar Adobe Sign con AEM Forms, consulte [Integración de Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Pasos siguientes {#next-steps}

Ha configurado un entorno para utilizar el flujo de trabajo centrado en Forms en las capacidades OSGi. Ahora, los pasos para utilizar esta capacidad son los siguientes:

* [Uso del flujo de trabajo centrado en Forms de OSGi](../../forms/using/aem-forms-workflow.md)
* [Referencia de pasos de flujo de trabajo](/help/sites-developing/workflows-step-ref.md)
* [Procesamiento posterior de cartas y comunicaciones interactivas](../../forms/using/submit-letter-topostprocess.md)
