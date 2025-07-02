---
title: Instalar y configurar comunicaciones interactivas
description: Instale y configure AEM Forms Interactive Communications para crear correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida.
role: Admin, User, Developer
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication,Correspondence Management
exl-id: d03965e1-4fa3-414c-80b6-c9fca281bee4
source-git-commit: bd33420307a7be6664b6bbb52677af66edaa9c0e
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 84%

---

# Instalar y configurar comunicaciones interactivas{#install-and-configure-interactive-communications}

## Introducción {#introduction}

AEM Form permite centralizar la creación, el ensamblado, la gestión y el envío de documentos seguros e interactivos, como correspondencia comercial, documentos, declaraciones, avisos de beneficios, correos de marketing, facturas y kits de bienvenida. Esta capacidad se denomina Interactive Communications. La capacidad está incluida en el paquete de complementos de AEM Forms. El paquete de complementos se implementa en una instancia de autor o de publicación de AEM.

Puede utilizar la capacidad Interactive Communications para producir comunicaciones en diferentes formatos; por ejemplo, en formato web y PDF. Puede integrar Interactive Communications con el flujo de trabajo de AEM para procesar y entregar la comunicación ensamblada a los clientes en el canal de su elección. Por ejemplo, para enviar una comunicación al usuario final por correo electrónico.

Si está actualizando desde una versión anterior y ya ha adquirido Administración de correspondencia, puede instalar el [paquete de compatibilidad](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) para seguir utilizándola. Para obtener información sobre las diferencias entre Interactive Communications y Administración de correspondencia, consulte [Información general sobre Interactive Communications](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms es una potente plataforma de clase empresarial. Interactive Communications es solo una de las capacidades de AEM Forms. Para obtener la lista completa de capacidades, consulte [Introducción a AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topología de implementación {#deployment-topology}

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. Lo único que necesita es disponer al menos de una instancia de autor de AEM y otra de procesamiento para ejecutar la capacidad Interactive Communications. A continuación, encontrará una topología de carácter orientativo para ejecutar AEM Forms Interactive Communications, Administración de correspondencia, AEM Forms Data Capture y el flujo de trabajo centrado en Forms en las capacidades OSGi. Para obtener información detallada sobre la topología, consulte [Arquitectura y topologías de implementación para AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topología-recomendada](assets/recommended-topology.png)

AEM Forms Interactive Communications ejecuta interfaces de usuario de administración, creación y agente en las instancias de autor de AEM Forms. Las instancias de publicación alojan la versión final de las comunicaciones interactivas que están listas para ser consumidas por los usuarios finales.

## Requisitos del sistema {#system-requirements}

Antes de empezar a instalar y configurar las capacidades de comunicación interactiva y Administración de correspondencia de AEM Forms, asegúrese de lo siguiente:

* Se ha implementado la infraestructura de hardware y software. Para obtener una lista detallada del hardware y el software compatibles, consulte [Requisitos técnicos](/help/sites-deploying/technical-requirements.md).

* La ruta de instalación de la instancia de AEM no contiene espacios en blanco.
* Se está ejecutando una instancia de AEM. En la terminología de AEM, una &quot;instancia&quot; es una copia de AEM que se ejecuta en un servidor en el modo Autor o Publicación. Se necesita al menos una instancia de AEM (de autor o de procesamiento) para ejecutar las capacidades Interactive Communications y Administración de correspondencia de AEM Forms:

   * **Autor**: la instancia de AEM utilizada para crear, cargar y editar contenido y administrar el sitio web. Una vez que el contenido está listo para su publicación, se replica en la instancia de publicación.
   * **Procesamiento:** una instancia de procesamiento es una instancia de [autor de AEM protegida](/help/forms/using/hardening-securing-aem-forms-environment.md). Puede configurar una instancia de autor y protegerla después de realizar la instalación.

   * **Publicación**: la instancia de AEM que sirve el contenido publicado al público a través de Internet o de una red interna.

* Se cumplen los requisitos de memoria. El paquete de complementos de AEM Forms requiere:

   * 15 GB de espacio temporal para instalaciones basadas en Microsoft® Windows.
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

El paquete de complementos de AEM Forms es una aplicación implementada en AEM. El paquete contiene Interactive Communications de AEM Forms, Administración de correspondencia y otras capacidades. Siga estos pasos para instalar el paquete de complementos:

1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
1. En la sección **[!UICONTROL Filtros]**:
   1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
   2. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
1. Abra el [Administrador de paquetes](/help/sites-administering/package-manager.md) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

   También puede descargar el paquete a través del vínculo directo que aparece en el artículo [Versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

1. Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No reinicie el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere a que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTERED dejen de aparecer en el archivo [AEM-Installation-Directory]/crx-quickstart/logs/error.log y el registro sea estable.

   >[!NOTE]
   >
   > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

1. Repita los pasos del 1 al 7 en todas las instancias de autor y publicación.

## Configuraciones posteriores a la instalación {#post-installation-configurations}

AEM Forms incluye algunas configuraciones obligatorias y otras opcionales. Entre las configuraciones obligatorias se incluyen la configuración de las bibliotecas BouncyCastle y el agente de serialización. Entre las configuraciones opcionales se incluyen la configuración de Dispatcher y Adobe Target.

### Configuraciones posteriores a la instalación obligatorias {#mandatory-post-installation-configurations}

#### Configuración de las bibliotecas RSA y BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Realice los siguientes pasos en todas las instancias de autor y publicación para iniciar y delegar las bibliotecas:

1. Detenga la instancia de AEM subyacente.
1. Abra el [directorio de instalación de AEM]\crx-quickstart\conf\sling.properties para editarlo.

   Si usó [directorio de instalación de AEM]\crx-quickstart\bin\start.bat para iniciar AEM, edite el archivo sling.properties en [AEM_root]\crx-quickstart\.

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

#### Instalar el paquete de compatibilidad {#install-compatibility-package}

Interactive Communications es la forma predeterminada y recomendada de crear comunicaciones con los clientes en AEM 6.5 Forms. Si ha actualizado o migrado desde una versión anterior y piensa seguir utilizando cartas (Administración de correspondencia), instale el [paquete de compatibilidad de AEMFD](/help/forms/using/compatibility-package.md).

El paquete de compatibilidad de AEMFD le permite utilizar los siguientes recursos de AEM 6.4 Forms, AEM 6.3 Forms y AEM 6.2 Forms en AEM 6.5 Forms:

* Fragmentos de documento
* Cartas
* Diccionarios de datos
* Plantillas y páginas obsoletas de formularios adaptables

#### Configurar Dispatcher {#configure-dispatcher}

Dispatcher es la herramienta de equilibrio de carga y almacenamiento en caché de Adobe Experience Manager que se utiliza con un servidor web de clase empresarial. Si usa [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es), realice las siguientes configuraciones en AEM Forms:

1. Configure el acceso en AEM Forms:

   Abra el archivo dispatcher.any para editarlo. Vaya a la sección de filtros y agregue el siguiente filtro:

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Guarde y cierre el archivo. Para obtener información detallada sobre los filtros, consulte la [documentación de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es).

1. Configure el servicio del Filtro de referente:

   Inicie sesión en el Administrador de configuración de Apache Felix como administrador. La URL predeterminada del Administrador de configuración es https://&#39;server&#39;:[port_number]/system/console/configMgr.  En el menú **Configuraciones**, seleccione la opción **Filtro de referente de Apache Sling**. En el campo Permitir hosts, escriba el nombre de host de Dispatcher para permitirlo como referente y haga clic en **Guardar**. El formato de la entrada es https://&#39;[server]:[port]&#39;.

#### Integración con Adobe Target {#integrate-adobe-target}

Es probable que los clientes abandonen una comunicación interactiva si la experiencia que ofrece no es atractiva. Aunque para los clientes resulta frustrante, también aumenta el volumen y el coste de la asistencia en su organización. Identificar y ofrecer una experiencia del cliente correcta que aumente la tasa de conversión es fundamental, además de un desafío. AEM Forms es la solución a este problema.

AEM Forms se integra con Adobe Target, una solución de Adobe Experience Cloud, para ofrecer experiencias del cliente personalizadas y atractivas en varios canales digitales. Para utilizar Adobe Target para personalizar una comunicación interactiva, consulte [Integración de Adobe Target con AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurar la comunicación SSL para el modelo de datos de formulario  {#configure-ssl-communcation-for-form-data-model}

Puede activar la comunicación SSL para el modelo de datos de formulario. Para habilitar la comunicación SSL para el modelo de datos de formulario, antes de iniciar cualquier instancia de AEM Forms, agregue los certificados al almacén de confianza de Java™ de todas las instancias. Puede ejecutar el siguiente comando para añadir los certificados:

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Pasos siguientes {#next-steps}

Ha configurado un entorno para utilizar las capacidades Interactive Communications y Administración de correspondencia. Ahora, los pasos para utilizar esta capacidad son:

* [Información general sobre Administración de correspondencia](/help/forms/using/interactive-communications-overview.md)

* [Crear una comunicación interactiva](../../forms/using/create-interactive-communication.md)

* [Crear una carta de Administración de correspondencia](../../forms/using/create-letter.md)
