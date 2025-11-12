---
title: Configuración de Dynamic Media, modo híbrido
description: 'Obtenga información sobre cómo configurar Dynamic Media: modo híbrido.'
mini-toc-levels: 3
role: User, Admin
feature: Configuration,Hybrid Mode
solution: Experience Manager, Experience Manager Assets
exl-id: 6252e61f-44b5-4931-80a0-426c6883092e
source-git-commit: 846b45f6ab83599eb709573a77422f2aba1ef047
workflow-type: tm+mt
source-wordcount: '7607'
ht-degree: 2%

---

# Configuración de Dynamic Media, modo híbrido {#configuring-dynamic-media-hybrid-mode}

>[!IMPORTANT]
>
>Fin de la compatibilidad con Secure Socket Layer 2.0 y 3.0 y Transport Layer Security 1.0 y 1.1.
>A partir del miércoles, 30 de abril de 2024, Adobe Dynamic Media deja de ofrecer asistencia para lo siguiente:
>
>* SSL (Secure Socket Layer) 2.0
>* SSL 3.0
>* TLS (Transport Layer Security) 1.0 y 1.1
>* Los siguientes cifrados débiles en TLS 1.2:
> `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
> `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
> `TLS_RSA_WITH_AES_256_GCM_SHA384`
> `TLS_RSA_WITH_AES_256_CBC_SHA256`
> `TLS_RSA_WITH_AES_256_CBC_SHA`
> `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
> `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
> `TLS_RSA_WITH_AES_128_GCM_SHA256`
> `TLS_RSA_WITH_AES_128_CBC_SHA256`
> `TLS_RSA_WITH_AES_128_CBC_SHA`
> `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
> `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
> `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
> `TLS_RSA_WITH_SDES_EDE_CBC_SHA`
>
> Consulte también [Limitaciones de Dynamic Media](/help/assets/limitations.md).

<!-- FOR ABOVE - CQDOC-19433 (original ticket)
and CQDOC-19792 (removed as per this ticket December 5, 2022) -->


Dynamic Media-Hybrid debe estar habilitado y configurado para su uso. Según su caso de uso, Dynamic Media tiene varias [configuraciones admitidas](#supported-dynamic-media-configurations).

>[!NOTE]
>
>Si tiene intención de configurar y ejecutar Dynamic Media en el modo de ejecución de Scene7, consulte [Configurar Dynamic Media - Modo de Scene7](/help/assets/config-dms7.md).
>
>Si tiene intención de configurar y ejecutar Dynamic Media en modo de ejecución híbrido, siga las instrucciones de esta página.

Más información sobre cómo trabajar con [video](/help/assets/video.md) en Dynamic Media.

>[!NOTE]
>
>Si utiliza la configuración de Adobe Experience Manager para diferentes entornos, como uno para desarrollo, ensayo y producción en directo, configure los servicios en la nube de Dynamic Media para cada entorno.

>[!NOTE]
>
>Si tiene problemas con la configuración de Dynamic Media, busque en los archivos de registro específicos de Dynamic Media. Estos archivos se instalan automáticamente al habilitar Dynamic Media:
>
>* `s7access.log`
>* `ImageServing.log`
>
>Están documentados en [Supervisar y mantener su instancia de Experience Manager](/help/sites-deploying/monitoring-and-maintaining.md).

La publicación y el envío híbridos son una función central de Dynamic Media, además de Adobe Experience Manager. La publicación híbrida permite entregar recursos de Dynamic Media, como imágenes, conjuntos y vídeos, desde la nube en lugar de desde los nodos de publicación de Experience Manager.

Otros contenidos, como los visualizadores de Dynamic Media, las páginas del sitio y el contenido estático, se siguen mostrando desde los nodos de publicación de Experience Manager.

Si es cliente de Dynamic Media, debe utilizar la entrega híbrida como mecanismo de entrega para todo el contenido de Dynamic Media.

## Arquitectura de publicación híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-506](assets/chlimage_1-428.png)

## Arquitectura de publicación híbrida para imágenes {#hybrid-publishing-architecture-for-images}

![chlimage_1-507](assets/chlimage_1-507.png)

## Configuraciones de Dynamic Media admitidas {#supported-dynamic-media-configurations}

Las tareas de configuración que siguen hacen referencia a los siguientes términos:

| **Término** | **Dynamic Media habilitado** | **Descripción** |
|---|---|---|
| Nodo Autor de Experience Manager | Marca de verificación blanca en un círculo verde | Nodo de autor que se implementa en las instalaciones o a través de Managed Services. |
| Nodo Publicación de Experience Manager | &quot;X&quot; blanca en un cuadrado rojo. | Nodo de publicación que se implementa en las instalaciones o a través de Managed Services. |
| Nodo de publicación del servicio de imágenes | Marca de verificación blanca en un círculo verde. | Nodo de publicación que se ejecuta en centros de datos administrados por Adobe. Hace referencia a la URL del servicio de imágenes. |

Puede elegir implementar Dynamic Media solo para imágenes, solo para vídeo o tanto para imágenes como para vídeo. Para determinar los pasos para configurar Dynamic Media para su escenario específico, consulte la siguiente tabla.

<table>
 <tbody>
  <tr>
   <td><strong>Escenario</strong></td>
   <td ><strong>Cómo funciona</strong></td>
   <td><strong>Pasos de configuración</strong></td>
  </tr>
  <tr>
   <td>Distribuya SOLO imágenes en producción</td>
   <td>Las imágenes se envían a través de servidores en centros de datos de todo el mundo de Adobe y, a continuación, una CDN las almacena en caché para obtener un rendimiento escalable y un alcance global.</td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> de Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>Configurar imágenes en <a href="#configuring-dynamic-media-cloud-services">Servicios de nube de Dynamic Media</a>.</li>
     <li><a href="#configuring-image-replication">Configurar la replicación de imágenes</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configuración del catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Usar filtros de recursos predeterminados para la replicación</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configurar el servidor de imágenes de Dynamic Media</a>.</li>
     <li><a href="#delivering-assets">Enviar recursos</a>.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Distribuya SOLO imágenes en preproducción (desarrollo, QE, ensayo, etc.)</td>
   <td>Las imágenes se entregan mediante el nodo de publicación de Experience Manager. En esta situación, como el tráfico es mínimo, no es necesario enviar imágenes al centro de datos de Adobe. Y permite una previsualización segura del contenido antes del lanzamiento de producción.</td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> de Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>En el nodo <strong>publish</strong> de Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li>Configure <a href="#setting-up-asset-filters-for-imaging-in-non-production-deployments">filtro de recursos para imágenes que no sean de producción</a>.</li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configure las opciones del servidor de imágenes de Dynamic Media.</a></li>
     <li><a href="#delivering-assets">Entrega de recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ofrezca SOLO vídeo en cualquier entorno (producción, desarrollo, QE, fase, etc.)</td>
   <td>Una CDN entrega y almacena en caché los vídeos para un rendimiento escalable y un alcance global. La imagen de póster de vídeo (miniatura del vídeo que se muestra antes de que se inicie la reproducción) la entrega la instancia de publicación de Experience Manager.</td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> de Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>En el nodo <strong>publish</strong> de Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a> (la instancia de publicación sirve la imagen de póster de vídeo y proporciona metadatos para la reproducción de vídeo).</li>
     <li>Configurar vídeo en <a href="#configuring-dynamic-media-cloud-services">Servicios de nube de Dynamic Media.</a></li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li>Configurar <a href="#setting-up-asset-filters-for-video-only-deployments">filtro de recursos solo para vídeo</a>.</li>
     <li><a href="#delivering-assets">Entrega de recursos.</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Distribución de imágenes y vídeo en producción</td>
   <td><p>Una CDN entrega y almacena en caché los vídeos para un rendimiento escalable y un alcance global. Las imágenes y los pósters de vídeo se envían a través de servidores ubicados en centros de datos de todo el mundo de Adobe y, a continuación, una red de distribución de contenido (CDN) las almacena en caché para obtener un rendimiento escalable y un alcance global.</p> <p>Consulte las secciones anteriores para configurar imágenes o vídeos en preproducción. </p> </td>
   <td>
    <ol>
     <li>En el nodo <strong>author</strong> de Experience Manager, <a href="#enabling-dynamic-media">habilite Dynamic Media</a>.</li>
     <li>Configurar vídeo en <a href="#configuring-dynamic-media-cloud-services">Servicios de nube de Dynamic Media.</a></li>
     <li>Configurar imágenes en <a href="#configuring-dynamic-media-cloud-services">Servicios de nube de Dynamic Media.</a></li>
     <li><a href="#configuring-image-replication">Configurar la replicación de imágenes</a>.</li>
     <li><a href="#replicating-catalog-settings">Replicar configuración del catálogo</a>.</li>
     <li><a href="#replicating-viewer-presets">Replicar ajustes preestablecidos de visor</a>.</li>
     <li><a href="#using-default-asset-filters-for-replication">Utilice los filtros de recursos predeterminados para la replicación.</a></li>
     <li><a href="#configuring-dynamic-media-image-server-settings">Configure las opciones del servidor de imágenes de Dynamic Media.</a></li>
     <li><a href="#delivering-assets">Entrega de recursos.</a></li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Habilitar Dynamic Media {#enabling-dynamic-media}

[Dynamic Media](https://business.adobe.com/es/products/experience-manager/assets/dynamic-media.html) está deshabilitado de forma predeterminada. Para aprovechar las características de Dynamic Media, debe habilitar Dynamic Media utilizando el modo de ejecución de `dynamicmedia` como lo haría, por ejemplo, en el modo de ejecución de `publish`. Antes de habilitar, asegúrese de revisar [los requisitos técnicos](/help/sites-deploying/technical-requirements.md#requirements-for-aem-dynamic-media-add-on).

>[!NOTE]
>
>Al habilitar Dynamic Media mediante el modo de ejecución, se reemplazará la funcionalidad de Experience Manager 6.1 y Experience Manager 6.0, donde habilitó Dynamic Media al establecer el indicador `dynamicMediaEnabled` en **[!UICONTROL true]**. Este indicador no tiene funcionalidad en Experience Manager 6.2 y versiones posteriores. Además, no es necesario reiniciar el inicio rápido para habilitar Dynamic Media.

Al habilitar Dynamic Media, las características de Dynamic Media están disponibles en la interfaz de usuario y cada recurso de imagen cargado recibe una representación *cqdam.pyramid.tiff* que se utiliza para la entrega rápida de representaciones de imágenes dinámicas. Estos PTIFF tienen ventajas significativas como las siguientes:

* La capacidad de administrar una sola imagen de origen principal y generar representaciones infinitas sobre la marcha sin ningún almacenamiento adicional.
* La capacidad de utilizar visualizaciones interactivas como zoom, desplazamiento y giro.

Si desea usar Dynamic Media Classic en Experience Manager, no habilite Dynamic Media a menos que esté usando un [escenario específico](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media). Dynamic Media está desactivado a menos que active Dynamic Media mediante el modo de ejecución.

Para habilitar Dynamic Media, debe habilitar el modo de ejecución de Dynamic Media desde la línea de comandos o desde el nombre del archivo de inicio rápido.

**Para habilitar Dynamic Media:**

1. En la línea de comandos, al iniciar el inicio rápido, haga lo siguiente:

   * Agregue `-r dynamicmedia` al final de la línea de comandos al iniciar el archivo jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -r dynamicmedia
   ```

   Si publica en s7delivery, también debe incluir los siguientes argumentos trustStore:

   ```shellsession {.line-numbers}
   -Djavax.net.ssl.trustStore=<absoluteFilePath>/customerTrustStoreFileName>
   
    -Djavax.net.ssl.trustStorePassword=<passwordForTrustStoreFile>
   ```

1. Solicite `https://localhost:4502/is/image` y asegúrese de que Image Server se esté ejecutando.

   >[!NOTE]
   >
   >Para solucionar problemas con Dynamic Media, consulte los siguientes registros en el directorio `crx-quickstart/logs/`:
   >
   >* ImageServer-&lt;PortId>-&lt;yyyy>&lt;mm>&lt;dd>.log: el registro de ImageServer proporciona estadísticas e información analítica utilizada para analizar el comportamiento del proceso interno de ImageServer.
   >
   >Ejemplo de nombre de archivo de registro de Image Server: `ImageServer-57346-2020-07-25.log`
   >
   >* s7access-&lt;yyyy>&lt;mm>&lt;dd>.log: el registro de acceso de s7registra todas las solicitudes realizadas a Dynamic Media a través de `/is/image` y `/is/content`.
   >
   >Estos registros solo se utilizan cuando Dynamic Media está habilitado. No se incluyen en el paquete **Descargar completo** que se genera desde la página `system/console/status-Bundlelist`; cuando llame a la atención al cliente si tiene un problema de Dynamic Media, anexe ambos registros al problema.

### Si instaló Experience Manager en un puerto o ruta de contexto diferente... {#if-you-installed-aem-to-a-different-port-or-context-path}

Si va a implementar [Experience Manager en un servidor de aplicaciones](/help/sites-deploying/application-server-install.md) y tiene habilitado Dynamic Media, debe configurar **self-domain** en el externalizador. De lo contrario, la generación de miniaturas para recursos no funciona correctamente para recursos de Dynamic Media.

Además, si ejecuta quickstart en un puerto o ruta de contexto diferente, también tiene que cambiar el **dominio propio**.

Cuando Dynamic Media está habilitado, las representaciones de miniaturas estáticas para los recursos de imagen se generan mediante Dynamic Media. Para que la generación de miniaturas funcione correctamente en Dynamic Media, Experience Manager debe realizar una solicitud de URL a sí mismo y debe conocer tanto el número de puerto como la ruta de contexto.

En Experience Manager:

* El **dominio propio** del [externalizador](/help/sites-developing/externalizer.md) se usa para recuperar el número de puerto y la ruta de acceso del contexto.
* Si no se ha configurado ningún **dominio propio**, el número de puerto y la ruta de contexto se recuperarán del servicio HTTP de Jetty.

En una implementación WAR de Experience Manager QuickStart, el número de puerto y la ruta de contexto no se pueden derivar, por lo que debe configurar un **dominio propio**. Consulte [Documentación del externalizador](/help/sites-developing/externalizer.md) sobre cómo configurar el **dominio propio**.

>[!NOTE]
>
>En una implementación independiente de [Experience Manager Quickstart](/help/sites-deploying/deploy.md), no suele ser necesario configurar un **dominio propio**, ya que el número de puerto y la ruta de contexto se pueden configurar automáticamente. Sin embargo, si todas las interfaces de red están desactivadas, debe configurar el **dominio propio**.

## Deshabilitar Dynamic Media  {#disabling-dynamic-media}

Dynamic Media no está habilitado de forma predeterminada. Sin embargo, si ha habilitado previamente Dynamic Media, puede desactivarlo más adelante.

Para deshabilitar Dynamic Media después de haberla habilitado, quite la marca del modo de ejecución `-r dynamicmedia`.

**Para deshabilitar Dynamic Media:**

1. En la línea de comandos, al iniciar el inicio rápido, puede realizar una de las siguientes acciones:

   * No agregue `-r dynamicmedia` a la línea de comandos al iniciar el archivo jar.

   ```shellsession {.line-numbers}
   java -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar
   ```

1. Solicitud `https://localhost:4502/is/image`. Recibirá un mensaje que indica que Dynamic Media está deshabilitado.

   >[!NOTE]
   >
   >Una vez deshabilitado el modo de ejecución de Dynamic Media, el paso de flujo de trabajo que genera la representación de `cqdam.pyramid.tiff` se omite automáticamente. También deshabilita la compatibilidad con representaciones dinámicas y otras funciones de Dynamic Media.
   >
   >Tenga en cuenta también que cuando el modo de ejecución de Dynamic Media está deshabilitado después de configurar el servidor de Experience Manager, todos los recursos que se cargaron en ese modo de ejecución ahora no son válidos.

## Configurar la replicación de imágenes {#configuring-image-replication}

La entrega de imágenes de Dynamic Media funciona publicando recursos de imagen, incluidas miniaturas de vídeo, de Experience Manager Author y replicándolos en el servicio de replicación bajo demanda de Adobe (la URL del servicio de replicación). A continuación, Assets se entrega a través del servicio de entrega de imágenes bajo demanda (la URL del servicio de imágenes).

Haga lo siguiente:

1. [Configurar autenticación](#setting-up-authentication).
1. [Configurar el agente de replicación](#configuring-the-replication-agent).

El agente de replicación publica recursos de Dynamic Media como imágenes, metadatos de vídeo y establece en el servicio de imágenes alojado en Adobe. El Agente de replicación no está habilitado de forma predeterminada.

Después de configurar el agente de replicación, debe [validar y probar que se ha configurado correctamente](#validating-the-replication-agent-for-dynamic-media). En esta sección se describen estos procedimientos.

>[!NOTE]
>
>El límite de memoria predeterminado para la creación de PTIFF es de 3 GB en todos los flujos de trabajo. Por ejemplo, puede procesar una imagen que requiera 3 GB de memoria mientras otros flujos de trabajo están en pausa, o puede procesar 10 imágenes en paralelo que requieran 300 MB de memoria cada una.
>
>El límite de memoria es configurable y se ajusta a la disponibilidad de recursos del sistema y al tipo de contenido de imagen que se procesa. Si tiene muchos recursos grandes y memoria suficiente en el sistema, puede aumentar este límite para asegurarse de que las imágenes se procesen en paralelo.
>
>Se rechaza una imagen que requiera más del límite máximo de memoria.
>
>Para cambiar el límite de memoria para la creación de PTIFF, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]** > **[!UICONTROL Adobe CQ Scene7 PTiffManager]** y cambie el valor de **[!UICONTROL maxMemory]**.

### Configurar autenticación {#setting-up-authentication}

Configure la autenticación de replicación en el autor para que pueda replicar imágenes en el servicio de entrega de imágenes de Dynamic Media. En primer lugar, obtenga un almacén de claves y, a continuación, guárdelo en el usuario **[!UICONTROL dynamic-media-replication]** y configúrelo. El administrador de su empresa recibió un correo electrónico de bienvenida con el archivo KeyStore y las credenciales necesarias durante el proceso de aprovisionamiento. Si no ha recibido esta información, póngase en contacto con el servicio de atención al cliente de Adobe.

**Para configurar la autenticación:**

1. Póngase en contacto con Asistencia al cliente de Adobe para obtener el archivo y la contraseña de KeyStore si aún no dispone del archivo y la contraseña. Esta información es una parte necesaria del aprovisionamiento. Asocia las claves a su cuenta.

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. En la página Administración de usuarios, vaya al usuario **[!UICONTROL dynamic-media-replication]** y, a continuación, seleccione para abrirlo.

   ![dm-replication](assets/dm-replication.png)

1. En la página Editar configuración de usuario para replicación de medios dinámicos, seleccione la pestaña **[!UICONTROL almacén de claves]** y, a continuación, seleccione **[!UICONTROL Crear almacén de claves]**.

   ![dm-replication-keystore](assets/dm-replication-keystore.png)

1. Escriba una contraseña y confírmela en el cuadro de diálogo **[!UICONTROL Establecer contraseña de acceso a KeyStore]**.

   >[!NOTE]
   >
   >Recuerde la contraseña porque debe introducirla de nuevo cuando configure el Agente de replicación más adelante.

   ![chlimage_1-508](assets/chlimage_1-508.png)

1. En la página **[!UICONTROL Editar configuración de usuario para replicación de medios dinámicos]**, expanda el área **Agregar clave privada del archivo KeyStore** y agregue lo siguiente (vea las imágenes siguientes):

   * En el campo **[!UICONTROL Nuevo alias]**, escriba el nombre de un alias que desee usar más adelante en la configuración de replicación. Por ejemplo, podría usar `replication` como alias.
   * Seleccionar **[!UICONTROL archivo KeyStore]**. Vaya al archivo KeyStore que Adobe le ha proporcionado, selecciónelo y, a continuación, seleccione **[!UICONTROL Abrir]**.
   * En el campo **[!UICONTROL Contraseña del archivo KeyStore]**, escriba la contraseña del archivo KeyStore. Esta contraseña es **no** la contraseña de KeyStore que creó en el paso 5, pero es la contraseña del archivo KeyStore que Adobe proporciona en el correo electrónico de bienvenida que se le envió durante el aprovisionamiento. Póngase en contacto con Asistencia al cliente de Adobe si no recibió una contraseña de archivo de KeyStore.
   * En el campo **[!UICONTROL Contraseña de clave privada]**, escriba la contraseña de clave privada (puede ser la misma contraseña de clave privada proporcionada en el paso anterior). Adobe proporciona la contraseña de clave privada en el correo electrónico de bienvenida que se le ha enviado durante el aprovisionamiento. Póngase en contacto con Asistencia al cliente de Adobe si no recibió una contraseña de clave privada.
   * En el campo **[!UICONTROL Alias de clave privada]**, escriba el alias de clave privada. Por ejemplo, `*companyname*-alias`. Adobe proporciona el alias de la clave privada en el correo electrónico de bienvenida que se le ha enviado durante el aprovisionamiento. Póngase en contacto con Asistencia al cliente de Adobe si no recibió un alias de clave privada.

   ![edit_settings_fordynamic-media-replication2](assets/edit_settings_fordynamic-media-replication2.png)

1. Seleccione **[!UICONTROL Guardar y cerrar]** para guardar los cambios de este usuario.

   A continuación, debe [configurar el agente de replicación](#configuring-the-replication-agent).

### Configuración del agente de replicación {#configuring-the-replication-agent}

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en Author]**.
1. En la página Agentes de autor, seleccione **[!UICONTROL Replicación de imagen híbrida de Dynamic Media (s7delivery)]**.
1. Seleccione **[!UICONTROL Editar]**.
1. Seleccione la ficha **[!UICONTROL Configuración]** y, a continuación, escriba lo siguiente:

   * **[!UICONTROL Habilitado]**: seleccione esta casilla de verificación para habilitar el agente de replicación.
   * **[!UICONTROL Región]** - Configurada en la región apropiada: Norteamérica, Europa o Asia
   * **[!UICONTROL ID de inquilino]**: este valor es el nombre de su empresa/inquilino que está publicando en el servicio de replicación. Este valor es el ID de inquilino que Adobe proporciona en el correo electrónico de bienvenida que se le ha enviado durante el aprovisionamiento. Si no ha recibido esta información, póngase en contacto con el servicio de atención al cliente de Adobe.
   * **[!UICONTROL Alias del almacén de claves]**: Este valor es el mismo que el valor de **Nuevo alias** establecido al generar la clave en [Configuración de la autenticación](#setting-up-authentication); por ejemplo, `replication`. (Consulte el paso 7 en [Configuración de la autenticación](#setting-up-authentication)).
   * **[!UICONTROL Contraseña del almacén de claves]**: La contraseña de KeyStore que se creó al pulsar **[!UICONTROL Crear almacén de claves]**. Adobe no proporciona esta contraseña. Consulte el paso 5 de [Configuración de la autenticación](#setting-up-authentication).

   La siguiente imagen muestra el agente de replicación con datos de ejemplo:

   ![chlimage_1-509](assets/chlimage_1-509.png)

1. Seleccione **[!UICONTROL Aceptar]**.

### Validar el agente de replicación para Dynamic Media {#validating-the-replication-agent-for-dynamic-media}

Para validar el agente de replicación para Dynamic Media, haga lo siguiente:

Seleccione **[!UICONTROL Probar conexión]**. Ejemplo de salida es la siguiente:

```shell
11.03.2016 10:57:55 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
11.03.2016 10:57:55 - * Auth User: replication-receiver
11.03.2016 10:57:55 - * HTTP Version: 1.1
11.03.2016 10:57:55 - * Using OAuth 2.0 Authorization Grants
11.03.2016 10:57:55 - * OAuth 2.0 User: dynamic-media-replication
11.03.2016 10:57:55 - * OAuth 2.0 Token: '*****' initialized
11.03.2016 10:57:55 - Publishing: POST[https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=xfpuu-6613]
11.03.2016 10:57:55 - Publish response: OK[]
11.03.2016 10:57:55 - Transfer succeeded in 141 ms for ReplicationAction{type=TEST, path[0]='/content/dam', time=1457722675402, userId='admin', revision='null'}
-------------------------------------------------------------------------------------------------------------------------------
Replication test succeeded
```

>[!NOTE]
>
>También puede comprobarlo realizando una de las siguientes acciones:
>
>* Compruebe los registros de replicación para asegurarse de que el recurso esté replicado.
>* Publique una imagen. Seleccione la imagen y seleccione **[!UICONTROL Visualizadores]** en el menú desplegable; a continuación, seleccione un ajuste preestablecido de visualizador. Seleccione **[!UICONTROL URL]**. Para comprobar que puede ver la imagen, copie y pegue la ruta URL en el explorador.
>

### Solucionar problemas de autenticación {#troubleshooting-authentication}

Al configurar la autenticación, puede encontrar algunos problemas con sus soluciones. Antes de comprobar estos problemas, asegúrese de haber configurado la replicación.

#### Problema: Código de estado HTTP 401 con mensaje: se requiere autorización {#problem-http-status-code-with-message-authorization-required}

Este problema puede deberse a un error al configurar el almacén de claves para el usuario `dynamic-media-replication`.

```shell
Replication test to s7delivery:https://s7bern.macromedia.com:8580/is-publish/
17.06.2016 18:54:43 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}
17.06.2016 18:54:43 - * Auth User: replication-receiver
17.06.2016 18:54:43 - * HTTP Version: 1.1
17.06.2016 18:54:43 - * Using OAuth 2.0 Authorization Grants
17.06.2016 18:54:43 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 18:54:43 - No OAuth token available. OAuth not initialized
17.06.2016 18:54:43 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 18:54:43 - Publishing: POST[https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough]
17.06.2016 18:54:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309, userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
17.06.2016 18:54:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466214883309,
 userId='admin', revision='null'}. java.io.IOException: Failed to execute request
'https://<localhost>:8580/is-publish//publish-receiver?Cmd=Test&RootId=brough':
 Server returned status code 401 with message: Authorization required.
```

**Solución:**
Compruebe que `KeyStore` se haya guardado en el usuario **dynamic-media-replication** y que se haya proporcionado con la contraseña correcta.

#### Problema: No Se Pudo Descifrar La Clave - No Se Pudieron Descifrar Los Datos {#problem-could-not-decrypt-key-could-not-decrypt-data}

```xml
Replication test to s7delivery:https://<localhost>:8580/is-publish/
17.06.2016 19:00:16 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}
17.06.2016 19:00:16 - * Auth User: replication-receiver
17.06.2016 19:00:16 - * HTTP Version: 1.1
17.06.2016 19:00:16 - * Using OAuth 2.0 Authorization Grants
17.06.2016 19:00:16 - * OAuth 2.0 User: dynamic-media-replication
17.06.2016 19:00:16 - No OAuth token available. OAuth not initialized
17.06.2016 19:00:16 - * Using Client Auth SSL alias - replication-alias *
17.06.2016 19:00:16 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1466215216662, userId='admin', revision='null'}. java.lang.SecurityException: java.security.UnrecoverableKeyException: Could not decrypt key: Could not decrypt data.
```

**Solución:**
Compruebe la contraseña. La contraseña guardada en el agente de replicación no es la misma contraseña que se utilizó para crear el almacén de claves.

#### Problema: InvalidAlgorithmParameterException {#problem-invalidalgorithmparameterexception}

Este problema se debe a un error de configuración en la instancia de autor de Experience Manager. El proceso Java™ del autor no está obteniendo el `javax.net.ssl.trustStore` correcto. Verá este error en el registro de replicación:

```shell
14.04.2016 09:37:43 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
14.04.2016 09:37:43 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1460651862089, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://<localhost>:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx2': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
```

O el registro de errores:

```shell
07.25.2019 12:00:59.893 *ERROR* [sling-threadpool-db2763bb-bc50-4bb5-bb64-10a09f432712-(apache-sling-job-thread-pool)-90-com_day_cq_replication_job_s7delivery(com/day/cq/replication/job/s7delivery)] com.day.cq.replication.Agent.s7delivery.queue Error during processing of replication.

java.io.IOException: Failed to execute request 'https://replicate-na.assetsadobe.com:8580/is-publish/publish-receiver?Cmd=Test&RootId=rbrough-osx': java.lang.RuntimeException: Unexpected error: java.security.InvalidAlgorithmParameterException: the trustAnchors parameter must be non-empty
        at com.scene7.is.catalog.service.publish.atomic.PublishingServiceHttp.executePost(PublishingServiceHttp.scala:195)
```

**Solución:**
Asegúrese de que el proceso Java™ del autor de Experience Manager tiene la propiedad del sistema `-Djavax.net.ssl.trustStore=` establecida en un almacén de confianza válido.

#### Problema: KeyStore no está configurado o no se ha inicializado {#problem-keystore-is-either-not-set-up-or-it-is-not-initialized}

Es probable que este problema se deba a una corrección rápida o a que un paquete de funciones sobrescriba el nodo dynamic-media-user o keystore.

Ejemplo de registro de replicación:

```shell
Replication test to s7delivery:https://replicate-na.assetsadobe.com/is-publish
02.08.2016 14:37:44 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}
02.08.2016 14:37:44 - * Auth User: replication-receiver
02.08.2016 14:37:44 - * HTTP Version: 1.1
02.08.2016 14:37:44 - * Using OAuth 2.0 Authorization Grants
02.08.2016 14:37:44 - * OAuth 2.0 User: dynamic-media-replication
02.08.2016 14:37:44 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470173864834, userId='admin', revision='null'}. com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised key store for user dynamic-media-replication
```

**Solución:**

1. Navegue hasta la página Administración de usuarios:
   `localhost:4502/libs/granite/security/content/useradmin.html`
1. En la página Administración de usuarios, navegue hasta el usuario `dynamic-media-replication` y, a continuación, seleccione para abrir.
1. Seleccione la ficha **[!UICONTROL KeyStore]**. Si aparece el botón **[!UICONTROL Crear almacén de claves]**, debe rehacer los pasos de [Configuración de la autenticación](#setting-up-authentication) anteriormente.
1. Si tuviste que rehacer la configuración de KeyStore, debes volver a [Configurar el agente de replicación](/help/assets/config-dynamic.md#configuring-the-replication-agent).

   Vuelva a configurar el agente de replicación de s7delivery.
   `localhost:4502/etc/replication/agents.author/s7delivery.html`

1. Seleccione **[!UICONTROL Probar conexión]** para que pueda comprobar que la configuración es válida.

#### Problema: El agente de publicación utiliza SSL en lugar de OAuth {#problem-publish-agent-is-using-ssl-instead-of-oauth}

Es probable que este problema se deba a una revisión o a que un paquete de funciones no se instaló correctamente o sobrescribió la configuración.

Ejemplo de registro de replicación:

```shell
01.08.2016 18:42:59 - Transferring content for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}
01.08.2016 18:42:59 - * Auth User: replication-receiver
01.08.2016 18:42:59 - * HTTP Version: 1.1
01.08.2016 18:42:59 - * Using Client Auth SSL alias - replication-receiver *
01.08.2016 18:42:59 - Publishing: POST[https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=altayerstaging]
01.08.2016 18:42:59 - Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
01.08.2016 18:42:59 - Error while replicating: com.day.cq.replication.ReplicationException: Transfer failed for ReplicationAction{type=TEST, path[0]='/content/dam', time=1470073379634, userId='admin', revision='null'}. java.io.IOException: Failed to execute request 'https://replicate-eu.assetsadobe2.com:443/is-publish/publish-receiver?Cmd=Test&RootId=rbroughstaging': Server returned status code 401 with message: Authorization required.
```

**Solución:**

1. En Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

   `localhost:4502/crx/de/index.jsp`

1. Vaya al nodo s7delivery Replication Agent.
   `localhost:4502/crx/de/index.jsp#/etc/replication/agents.author/s7delivery/jcr:content`

1. Agregue esta configuración al agente de replicación (booleano con valor establecido en **[!UICONTROL True]**):

   `enableOauth=true`

1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Guardar todo]**.

### Pruebe la configuración {#testing-your-configuration}

Adobe recomienda realizar una prueba completa de la configuración.

Asegúrese de haber realizado lo siguiente antes de comenzar esta prueba:

* Se agregaron ajustes preestablecidos de imagen.
* Configure **[!UICONTROL Configuración de Dynamic Media (anterior a 6.3)]** en Cloud Services. Se requiere la URL del servicio de imágenes para esta prueba

**Para probar la configuración:**

1. Cargue un recurso de imagen. (En Assets, vaya a **[!UICONTROL Crear]** > **[!UICONTROL Archivos]** y seleccione el archivo.)
1. Espere a que finalice el flujo de trabajo.
1. Publique el recurso de imagen. (Seleccione el recurso y seleccione **[!UICONTROL Publicación rápida]**).
1. Para desplazarse a las representaciones de esa imagen, abra la imagen y pulse **[!UICONTROL Representaciones]**.

   ![chlimage_1-510](assets/chlimage_1-510.png)

1. Seleccione cualquier representación dinámica.
1. Para obtener la URL de este recurso, seleccione **[!UICONTROL URL]**.
1. Vaya a la dirección URL seleccionada y compruebe si la imagen se comporta según lo esperado.

Otra forma de probar que los recursos se entregaron es anexar req=exists a la dirección URL.

## Configurar los servicios de nube de Dynamic Media {#configuring-dynamic-media-cloud-services}

Dynamic Media Cloud Service admite la publicación y entrega híbridas de imágenes y vídeo, análisis de vídeo y codificación de vídeo, entre otras cosas.

Como parte de la configuración, debe introducir un ID de registro, una URL de servicio de vídeo, una URL de servicio de imagen, una URL de servicio de replicación y configurar la autenticación. Esta información se le envió por correo electrónico como parte del proceso de aprovisionamiento de cuentas. Si no ha recibido esta información, póngase en contacto con su administrador de Adobe Experience Manager o con Asistencia al cliente de Adobe para obtener la información.

>[!NOTE]
>
>Antes de configurar los servicios en la nube de Dynamic Media, asegúrese de tener configurada la instancia de publicación. También debe tener configurada la replicación antes de configurar los servicios en la nube de Dynamic Media.

**Para configurar los servicios de nube de Dynamic Media:**

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Dynamic Media (anterior a 6.3)]**.
1. En la página Explorador de configuración de Dynamic Media, en el panel izquierdo, seleccione **[!UICONTROL global]**, luego seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración de Dynamic Media]**, en el campo Título, escriba un título.
1. Si está configurando Dynamic Media para vídeo,

   * En el campo **[!UICONTROL ID de registro]**, escriba su ID de registro.
   * En el campo **[!UICONTROL URL del servicio de vídeo]**, ingrese la URL del servicio de vídeo para Dynamic Media Gateway.

1. Si está configurando Dynamic Media para imágenes, en el campo **[!UICONTROL URL del servicio de imágenes]**, introduzca la URL del servicio de imágenes para Dynamic Media Gateway.
1. Seleccione **[!UICONTROL Guardar]** para volver a la página Explorador de configuración de Dynamic Media.
1. Para acceder a la consola de navegación global, seleccione el logotipo de Experience Manager.

## Configuración de informes de vídeo {#configuring-video-reporting}

Puede configurar los informes de vídeo en varias instalaciones de Experience Manager mediante Dynamic Media Hybrid.

**Cuándo se debe usar:** En el momento de configurar la Configuración de Dynamic Media (anterior a 6.3), se han iniciado numerosas funciones, incluidos los informes de vídeo. La configuración crea un grupo de informes en una empresa regional de Analytics. Si configura varios nodos Author, creará un grupo de informes independiente para cada uno de ellos. Como resultado, los datos de los informes no son coherentes entre las instalaciones. Además, si cada nodo Autor hace referencia al mismo servidor de publicación híbrido, la última instalación de Autor cambia el grupo de informes de destino para todos los informes de vídeo. Este problema sobrecarga el sistema de Analytics con demasiados grupos de informes.

**Introducción:** Configure los informes de vídeo realizando las tres tareas siguientes.

1. Cree un paquete de ajustes preestablecidos de Video Analytics después de configurar Dynamic Media Configuration (anterior a 6.3) en el primer nodo Author. Esta tarea inicial es importante porque permite que una nueva configuración siga utilizando el mismo grupo de informes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics en cualquier ***nuevo*** nodo de creación ***antes*** de configurar la configuración de Dynamic Media (anterior a 6.3).
1. Compruebe y depure la instalación del paquete.

### Cree un paquete de ajustes preestablecidos de Video Analytics después de configurar el primer nodo Autor {#creating-a-video-analytics-preset-package-after-configuring-the-first-author-node}

Cuando haya terminado esta tarea, tendrá un archivo de paquete que contiene los ajustes preestablecidos de Video Analytics. Estos ajustes preestablecidos contienen un grupo de informes, el servidor de seguimiento, el área de nombres de seguimiento y el ID de organización de Experience Cloud, si están disponibles.

1. Si aún no lo ha hecho, configure la Configuración de Dynamic Media (anterior a 6.3).
1. (Opcional) Consulte y copie la ID del grupo de informes (debe tener acceso al JCR). Aunque no es obligatorio tener el ID del grupo de informes, facilita la validación.
1. Cree un paquete con el Administrador de paquetes.
1. Edite el paquete para incluir un filtro.

   En Experience Manager: `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

1. Genere el paquete.
1. Descargue o comparta el paquete de ajustes preestablecidos de Video Analytics para que se pueda compartir con los nuevos nodos de Author subsiguientes.

### Instale el paquete de ajustes preestablecidos de Video Analytics antes de configurar más nodos de autor {#installing-the-video-analytics-preset-package-before-you-configure-additional-author-nodes}

Asegúrese de completar esta tarea ***antes de*** de configurar la Configuración de Dynamic Media (anterior a 6.3). Si no se hace esto, se creará otro grupo de informes que no se esté utilizando. Además, aunque los informes de vídeo siguen funcionando correctamente, la recopilación de datos no está optimizada.

Asegúrese de que se puede acceder al paquete de ajustes preestablecidos de Video Analytics desde el primer nodo Autor en el nuevo nodo Autor.

1. Cargue el paquete de ajustes preestablecidos de Video Analytics que creó anteriormente en el Administrador de paquetes.
1. Instale el paquete de ajustes preestablecidos de Video Analytics.
1. Configure la configuración de Dynamic Media (anterior a 6.3).

### Verificar y depurar la instalación del paquete {#verifying-and-debugging-the-package-installation}

1. Realice una de las siguientes acciones para verificar y, si es necesario, depurar la instalación del paquete:

   * **Compruebe el ajuste preestablecido de Video Analytics mediante el JCR**
Para comprobar el ajuste preestablecido de Video Analytics mediante el JCR, debe tener acceso a CRXDE Lite.

     Experience Manager: en CRXDE Lite, vaya a `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

     Como en `https://localhost:4502/crx/de/index.jsp#/conf/global/settings/dam/dm/presets/analytics/jcr%3Acontent/userdata`

     Si no tiene acceso a CRXDE Lite en el nodo Autor, puede comprobar el ajuste preestablecido a través del servidor de publicación.

   * **Compruebe el ajuste preestablecido de Video Analytics a través del servidor de imágenes**

     Puede validar el ajuste preestablecido de Video Analytics directamente realizando una solicitud req=userdata de Image Server.
Por ejemplo, para ver el ajuste preestablecido de Analytics en el nodo Autor, puede realizar la siguiente solicitud:

     `https://localhost:4502/is/image/conf/global/settings/dam/dm/presets/analytics?req=userdata`

     Para validar el ajuste preestablecido en los servidores de publicación, puede realizar una solicitud directa similar al servidor de publicación. Las respuestas son las mismas en los nodos Author y Publish. La respuesta tiene un aspecto similar al siguiente:

     ```
     marketingCloudOrgId=0FC4E86B573F99CC7F000101
      reportSuite=aemaem6397618-2018-05-23
      trackingNamespace=aemvideodal
      trackingServer=aemvideodal.d2.sc.omtrdc.net
     ```

   * **Compruebe el ajuste preestablecido de Video Analytics mediante la herramienta de informes de vídeo en Experience Manager**
Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Informes de vídeo]**

     `https://localhost:4502/mnt/overlay/dam/gui/content/s7dam/videoreports/videoreport.html`

     Si ve el siguiente mensaje de error, el grupo de informes está disponible, pero no se ha rellenado. Este error es correcto (y lo desea) en una nueva instalación antes de que el sistema recopile datos.

   ![screen_shot_2018-05-23at52254pm](assets/screen_shot_2018-05-23at52254pm.png)

   Para generar datos de informes, cargue y publique un vídeo. Use **[!UICONTROL Copiar URL]** y ejecute el vídeo al menos una vez.

   Pueden pasar hasta 12 horas antes de que los datos de informes se rellenen a partir del uso del Visor de vídeo.

   Si se produce un error y el grupo de informes no se configura correctamente, se muestra la siguiente alerta.

   ![screen_shot_2018-05-23at52612pm](assets/screen_shot_2018-05-23at52612pm.png)

   Este error también se muestra si se ejecuta Informes de vídeo antes de configurar los servicios de Configuración de Dynamic Media (anterior a 6.3).

### Solucionar problemas de configuración de informes de vídeo {#troubleshooting-the-video-reporting-configuration}

* Durante la instalación, a veces se agota el tiempo de espera de las conexiones al servidor de API de Analytics. La instalación reintenta la conexión 20 veces, pero sigue fallando. Cuando se produce esta situación, el archivo de registro registra varios errores. Busque `SiteCatalystReportService`.
* Si no instala primero el paquete de ajustes preestablecidos de Analytics, se puede crear un nuevo grupo de informes.
* Al actualizar de Experience Manager 6.3 a Experience Manager 6.4 o Experience Manager 6.4.1 y, a continuación, configurar la configuración de Dynamic Media (anterior a 6.3), se sigue creando un grupo de informes. Se sabe que este problema está programado para solucionarse en Experience Manager 6.4.2.

### Acerca del ajuste preestablecido de Video Analytics {#about-the-video-analytics-preset}

El ajuste preestablecido de Video Analytics, a veces denominado simplemente ajuste preestablecido de Analytics, se almacena junto a los ajustes preestablecidos de Visor en Dynamic Media. Es básicamente igual que un ajuste preestablecido de Visor, pero con información utilizada para configurar los informes de AppMeasurement y Video Heartbeat.

Las propiedades del ajuste preestablecido son las siguientes:

* `reportSuite`
* `trackingServer`
* `trackingNamespace`
* `marketingCloudOrgId` (no está presente en versiones anteriores de Experience Manager)

Experience Manager 6.4 y versiones más recientes guardan este ajuste preestablecido en `/conf/global/settings/dam/dm/presets/analytics/jcr:content/userdata`

## Replicar configuración del catálogo {#replicating-catalog-settings}

Publique su propia configuración de catálogo predeterminada como parte del proceso de configuración a través del JCR. Para replicar la configuración del catálogo:

1. En una ventana de terminal, ejecute lo siguiente:

   `curl -u admin:admin localhost:4502/libs/settings/dam/dm/presets/viewer.pushviewerpresets`

1. En Experience Manager, vaya a la siguiente ubicación en CRXDE Lite (requiere privilegios de administrador):

   `https://<*server*>:<*port*>/crx/de/index.jsp#/conf/global/settings/dam/dm/imageserver/`

1. Seleccione la ficha **[!UICONTROL Replicación]**.
1. Seleccione **[!UICONTROL Replicar]**.

## Replicar ajustes preestablecidos de visor {#replicating-viewer-presets}

Para entregar *un recurso con un ajuste preestablecido de visualizador, debe replicar/publicar* el ajuste preestablecido de visualizador. (Todos los ajustes preestablecidos de visor deben activarse *y* replicarse para obtener la URL o el código incrustado de un recurso.
Consulte [Publicar ajustes preestablecidos del visor](/help/assets/managing-viewer-presets.md#publishing-viewer-presets) para obtener más información.

>[!NOTE]
>
>De manera predeterminada, el sistema muestra varias representaciones al seleccionar **[!UICONTROL Representaciones]** y varios ajustes preestablecidos de visualizador al seleccionar **[!UICONTROL Visualizadores]** en la vista de detalles del recurso. Puede aumentar o disminuir el número de visualizaciones. Vea [Aumentar el número de ajustes preestablecidos de imagen que se muestran](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) o [Aumentar el número de ajustes preestablecidos de visor que se muestran](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

## Filtrado de recursos para la replicación {#filtering-assets-for-replication}

En implementaciones que no son de Dynamic Media, se replican *todos* los recursos (tanto imágenes como vídeo) del entorno de creación de Experience Manager en el nodo de publicación de Experience Manager. Este flujo de trabajo es necesario porque los servidores de publicación de Experience Manager también proporcionan los recursos.

Sin embargo, en implementaciones de Dynamic Media, como los recursos se entregan a través de la nube, no es necesario replicar esos mismos recursos en nodos de publicación de Experience Manager. Este flujo de trabajo de &quot;publicación híbrida&quot; evita costes de almacenamiento adicionales y tiempos de procesamiento más largos para replicar recursos. Otros contenidos, como los visualizadores de Dynamic Media, las páginas del sitio y el contenido estático, se siguen mostrando desde los nodos de publicación de Experience Manager.

Además de replicar los recursos, también se replican los siguientes recursos que no son de:

* Configuración de envío de Dynamic Media: `/conf/global/settings/dam/dm/imageserver/jcr:content`
* Ajustes preestablecidos de imagen: `/conf/global/settings/dam/dm/presets/macros`
* Ajustes preestablecidos de visor: `/conf/global/settings/dam/dm/presets/viewer`

Los filtros proporcionan una forma de *excluir* recursos de replicarse en el nodo de publicación de Experience Manager.

### Usar filtros de recursos predeterminados para la replicación {#using-default-asset-filters-for-replication}

Si usa Dynamic Media para (1) imágenes en producción *o* (2) imágenes y vídeo, puede usar los filtros predeterminados que Adobe proporciona tal cual. Los siguientes filtros están activos de forma predeterminada:

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Filter</strong></td>
   <td><strong>Tipo de mime</strong></td>
   <td><strong>Representaciones</strong></td>
  </tr>
  <tr>
   <td>Entrega de imágenes de Dynamic Media</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p> </p> </td>
   <td><p>Comienza con <strong>image/</strong></p> <p>Contiene <strong>application/</strong> y termina con <strong>set</strong>.</p> </td>
   <td>Los "filter-images" predeterminados (se aplica a recursos de imágenes únicas, incluidas imágenes interactivas) y "filter-sets" (se aplica a conjuntos de giros, conjuntos de imágenes, conjuntos de medios mixtos y conjuntos de carrusel):
    <ul>
     <li>Incluir imágenes PTIFF y metadatos para replicación (cualquier representación que comience por <strong>cqdam</strong>).</li>
     <li>Excluir de la replicación las representaciones de imagen original e imagen estática.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Entrega de vídeo de Dynamic Media</td>
   <td>filter-video</td>
   <td>Comienza con <strong>video/</strong></td>
   <td>El "filter-video" incorporado hará lo siguiente:
    <ul>
     <li>Incluya representaciones de vídeo proxy, miniaturas de vídeo/imagen de póster, metadatos (en representaciones de vídeo y vídeo principales) para replicación (cualquier representación que comience por <strong>cqdam</strong>).</li>
     <li>Excluya de la replicación el vídeo original y las representaciones de miniaturas estáticas.<br /> <br /> <strong>Nota:</strong> Las representaciones de vídeo proxy no contienen binarios, sino propiedades de nodo. Por lo tanto, no afecta al tamaño del repositorio del editor.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Integración de Dynamic Media Classic (Scene7)</td>
   <td><p>filter-images</p> <p>conjuntos de filtros</p> <p>filter-video</p> </td>
   <td><p>Comienza con <strong>image/</strong></p> <p>Contiene <strong>application/</strong> y termina con <strong>set</strong>.</p> <p>Comienza con <strong>video/</strong></p> </td>
   <td><p>Puede configurar el URI de transporte para que se vincule al servidor de publicación de Experience Manager en lugar de a la URL del servicio de replicación en la nube de Dynamic Media de Adobe. La configuración de este filtro permite que Dynamic Media Classic envíe recursos en lugar de la instancia de publicación de Experience Manager.</p> <p>Los "filter-images", "filter-sets" y "filter-video" predeterminados harán lo siguiente:</p>
    <ul>
     <li>Incluya imágenes PTIFF, representaciones de vídeo proxy y metadatos para la replicación. Sin embargo, como no existen en el JCR (para los que ejecutan Experience Manager), la integración de Dynamic Media Classic no hace nada.</li>
     <li>Excluya de la replicación la imagen original, las representaciones de imágenes estáticas, el vídeo original y las representaciones de miniaturas estáticas. En su lugar, Dynamic Media Classic ofrece recursos de imagen y vídeo.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los filtros se aplican a los tipos MIME y no pueden ser específicos de la ruta.

### Configurar filtros de recursos para implementaciones solo de vídeo {#setting-up-asset-filters-for-video-only-deployments}

Si utiliza Dynamic Media solo para vídeo, siga estos pasos para configurar filtros de recursos para la replicación:

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en Author]**.
1. En la página Agentes de autor, seleccione **[!UICONTROL Agente predeterminado (publicar)]**.
1. Seleccione **[!UICONTROL Editar]**.
1. En el cuadro de diálogo **[!UICONTROL Configuración del agente]**, en la ficha **[!UICONTROL Configuración]**, marque **[!UICONTROL Habilitado]** para activar el agente.
1. Seleccione **[!UICONTROL Aceptar]**.
1. En Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`
1. Busque **[!UICONTROL filter-video]**, haga clic con el botón derecho del ratón y seleccione **[!UICONTROL Copiar]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/publish`
1. Busque `jcr:content`, haga clic con el botón secundario en él y, a continuación, seleccione **[!UICONTROL Pegar]**.

En estos pasos se configura la instancia de publicación de Experience Manager para que proporcione la imagen de póster de vídeo y los metadatos de vídeo necesarios para la reproducción, mientras que el propio vídeo lo proporciona Dynamic Media Cloud Service. El filtro también excluye de la replicación el vídeo original y las representaciones de miniaturas estáticas, que no son necesarias en la instancia de publicación.

### Configuración de filtros de recursos para imágenes en implementaciones que no sean de producción {#setting-up-asset-filters-for-imaging-in-non-production-deployments}

Si utiliza Dynamic Media para generar imágenes en implementaciones que no son de producción, siga estos pasos para configurar filtros de recursos para la replicación:

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Replicación]** > **[!UICONTROL Agentes en Author]**.
1. En la página Agentes de autor, seleccione **[!UICONTROL Agente predeterminado (publicar)]**.
1. Seleccione **[!UICONTROL Editar]**.
1. En el cuadro de diálogo **[!UICONTROL Configuración del agente]**, en la ficha **[!UICONTROL Configuración]**, marque **[!UICONTROL Habilitado]** para activar el agente.
1. Seleccione **[!UICONTROL Aceptar]**.
1. En Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters`

   ![image-2018-01-16-10-22-40-410](assets/image-2018-01-16-10-22-40-410.png)

1. Busque **[!UICONTROL filter-images]**, haga clic con el botón derecho del ratón y seleccione **[!UICONTROL Copiar]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/publish`
1. Busque `jcr:content`, haga clic con el botón secundario en él y, a continuación, vaya a **[!UICONTROL Crear]** > **[!UICONTROL Crear nodo]**. Escriba el nombre `damRenditionFilters` del tipo `nt:unstructured`.
1. Busque `damRenditionFilters`, haga clic con el botón secundario en él y, a continuación, seleccione **[!UICONTROL Pegar]**.

Estos pasos configuran la instancia de publicación de Experience Manager para entregar las imágenes en un entorno que no sea de producción. El filtro también excluye de la replicación la imagen original y las representaciones estáticas, que no son necesarias en la instancia de publicación.

>[!NOTE]
>
>Si hay muchos filtros diferentes en un autor, cada agente necesita que se le asigne un usuario diferente. El código Granite aplica un modelo de filtro por usuario. Siempre tenga un usuario diferente para cada configuración de filtro.
>
>¿Está utilizando más de un filtro en un servidor? Por ejemplo, un filtro para que se publique la replicación y un segundo filtro para la entrega de s7. Si es así, debe asegurarse de que estos dos filtros tengan un **userId** diferente asignado en el nodo `jcr:content`. Vea la siguiente imagen:

![image-2018-01-16-10-26-28-465](assets/image-2018-01-16-10-26-28-465.png)

### Personalizar filtros de recursos para la replicación (opcional) {#customizing-asset-filters-for-replication}

1. En Experience Manager, seleccione el logotipo de Experience Manager para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.
1. En el árbol de carpetas izquierdo, navegue hasta `/etc/replication/agents.author/dynamic_media_replication/jcr:content/damRenditionFilters` para revisar los filtros.

   ![chlimage_1-511](assets/chlimage_1-511.png)

1. Para definir el tipo MIME para el filtro, puede localizar el tipo MIME de la siguiente manera:

   En el carril izquierdo, expanda `content > dam > <locate_your_asset> >  jcr:content > metadata` y luego, en la tabla, busque `dc:format`.

   El siguiente gráfico es un ejemplo de la ruta de un recurso a `dc:format`.

   ![chlimage_1-512](assets/chlimage_1-512.png)

   Observe que `dc:format` del recurso `Fiji Red.jpg` es `image/jpeg`.

   Para que este filtro se aplique a todas las imágenes, independientemente de su formato, establezca el valor en `image/*` donde `*` es una expresión regular que se aplica a todas las imágenes de cualquier formato.

   Para que el filtro se aplique solamente a imágenes del tipo JPEG, escriba un valor de `image/jpeg`.

1. Defina qué representaciones desea incluir o excluir de la replicación.

   Los caracteres que puede utilizar para filtrar la replicación son los siguientes:

   | Carácter que utilizar | Cómo filtra los recursos para la replicación |
   | --- | --- |
   | `*` | Carácter comodín |
   | `+` | Incluye recursos para la replicación |
   | `-` | Excluye recursos de la replicación |

   Navegue hasta `content/dam/<locate your asset>/jcr:content/renditions`.

   El siguiente gráfico es un ejemplo de las representaciones de un recurso.

   ![chlimage_1-513](assets/chlimage_1-4.png)

   En el ejemplo anterior, si solo desea replicar el PTIFF (TIFF piramidal), debe introducir `+cqdam,*`, que incluye todas las representaciones que comienzan con `cqdam`. En el ejemplo, esa representación es `cqdam.pyramid.tiff`.

   Si solo desea replicar el original, debe ingresar `+original`.

## Configuración del servidor de imágenes de Dynamic Media {#configuring-dynamic-media-image-server-settings}

La configuración del servidor de imágenes de Dynamic Media implica la edición del paquete de Adobe CQ Scene7 ImageServer y del paquete de Adobe CQ Scene7 PlatformServer.

>[!NOTE]
>
>Dynamic Media funciona de forma predeterminada [después de habilitarse](#enabling-dynamic-media). Sin embargo, si lo desea, puede ajustar la instalación configurando el servidor de imágenes de Dynamic Media para que cumpla determinadas especificaciones o requisitos.

**Requisito previo** - *Antes* de configurar el servidor de imágenes de Dynamic Media, asegúrese de que su VM de Windows® incluya una instalación de las bibliotecas de Microsoft® Visual C++. Las bibliotecas son necesarias para ejecutar Dynamic Media Image Server. Puede [descargar el paquete redistribuible de Microsoft® Visual C++ 2010 (x64) aquí](https://www.microsoft.com/en-us/download/details.aspx?id=26999).

Para establecer la configuración del servidor de imágenes de Dynamic Media:

1. En la esquina superior izquierda de Experience Manager, seleccione **[!UICONTROL Adobe Experience Manager]** para acceder a la consola de navegación global y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la página Configuración de la consola web de Adobe Experience Manager, vaya a **[!UICONTROL OSGi]** > **[!UICONTROL Configuración]** para ver una lista de todos los paquetes que se están ejecutando actualmente en Experience Manager.

   Los servidores de entrega de Dynamic Media se encuentran con los siguientes nombres en la lista:

   * `Adobe CQ Scene7 ImageServer`
   * `Adobe CQ Scene7 PlatformServer`

1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 ImageServer, seleccione el icono **[!UICONTROL Editar]**.
1. En el cuadro de diálogo Adobe CQ Scene7 ImageServer, defina los siguientes valores de configuración:

   >[!NOTE]
   >
   >Normalmente, no es necesario cambiar los valores predeterminados. Sin embargo, si cambia los valores predeterminados, debe reiniciar el paquete para que los cambios surtan efecto.

   | Propiedad | Valor predeterminado | Descripción |
   | --- | --- | --- |
   | `TcpPort.name` | *`empty`* | Número de puerto que se utilizará para la comunicación con el proceso de ImageServer. De forma predeterminada, el puerto libre se detecta automáticamente. |
   | `AllowRemoteAccess.name` | *`empty`* | Permitir o impedir el acceso remoto al proceso de ImageServer. Si es false, el servidor de imágenes solo escucha en localhost.<br> La configuración del externalizador predeterminado que señala al host local debe especificar el dominio o la dirección IP reales de la instancia de VM específica. El motivo es que el host local apunta al sistema principal de la VM.<br>Los dominios o direcciones IP de la VM deben tener una entrada de archivo host para que pueda resolverse por sí misma. |
   | `MaxRenderRgnPixels` | 16 MP | Tamaño máximo en megapíxeles que se procesa. |
   | `MaxMessageSize` | 16 MB | Tamaño máximo del mensaje en megabytes que se envía. |
   | `RandomAccessUrlTimeout` | 20 | Valor de tiempo de espera del tiempo en segundos que el servidor de imágenes espera a que el JCR responda a una solicitud de mosaico de intervalo. |
   | `WorkerThreads` | 10 | Número máximo de subprocesos de trabajo. |

1. Seleccione **[!UICONTROL Guardar]**.
1. En la lista de paquetes, a la derecha de Adobe CQ Scene7 PlatformServer, seleccione el icono **[!UICONTROL Editar]**.
1. En el cuadro de diálogo Adobe CQ Scene7 PlatformServer, defina las siguientes opciones de valor predeterminado:

   >[!NOTE]
   >
   >El servidor de imágenes de Dynamic Media utiliza su propia caché de disco para almacenar en caché las respuestas. La caché HTTP de Experience Manager y Dispatcher no se pueden usar para almacenar en caché las respuestas del servidor de imágenes de Dynamic Media.

   | Propiedad | Valor predeterminado | Descripción |
   |---|---|---|
   | Caché activada | Comprobado | Si la caché de respuestas está habilitada |
   | Raíces de caché | escondrijo | Una o varias rutas a las carpetas de la caché de respuestas. Las rutas relativas se resuelven en la carpeta del paquete de imagen s7 interna. |
   | Tamaño máximo de caché | 200000000 | Tamaño máximo de la caché de respuestas en bytes. |
   | Entradas máximas de caché | 100 000 | Número máximo de entradas permitidas en la caché. |

### Configuración de manifiesto predeterminada {#default-manifest-settings}

El manifiesto predeterminado permite configurar los valores predeterminados que se utilizan para generar las respuestas de envío de Dynamic Media. Puede ajustar la calidad (calidad de JPEG, resolución, modo de remuestreo), el almacenamiento en caché (caducidad) y evitar la representación de imágenes demasiado grandes (defaultpix, defaultthumbpix, maxpix).

La ubicación de la configuración de manifiesto predeterminada se toma del valor predeterminado **[!UICONTROL Catalog root]** del paquete **[!UICONTROL Adobe CQ Scene7 PlatformServer]**. De manera predeterminada, este valor se encuentra en la siguiente ruta en **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**

`/conf/global/settings/dam/dm/imageserver/`

![Configurar el servidor de imágenes en CRXDE Lite](assets/configimageservercrxdelite.png)

Puede cambiar los valores de las propiedades, tal como se describe en la tabla siguiente, introduciendo nuevos valores.

Cuando termine de cambiar el manifiesto predeterminado, en la esquina superior izquierda de la página, seleccione **[!UICONTROL Guardar todo]**.

Asegúrese de seleccionar la ficha **[!UICONTROL Control de acceso]** (a la derecha de la ficha Propiedades) y, a continuación, establezca los privilegios de control de acceso a `jcr:read` para todos los usuarios y para los usuarios de replicación de medios dinámicos.

![Configurar el servidor de imágenes en CRXDE Lite y establecer la ficha Control de acceso](assets/configimageservercrxdeliteaccesscontroltab.png)

Configuración de tabla de manifiesto y sus valores predeterminados:

| Propiedad | Valor predeterminado | Descripción |
| --- | --- | --- |
| `bkgcolor` | `FFFFFF` | Color de fondo predeterminado. Valor de RGB que se utiliza para rellenar las áreas de la imagen de respuesta que no contengan datos de imagen reales. Consulte también [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html?lang=es#image-serving-api) en la API del servicio de imágenes. |
| `defaultpix` | `300,300` | Tamaño de vista predeterminado. El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas, a no ser que la solicitud especifique el tamaño de vista por medio de wid=, hei= o scl=.<br>Se especifica como dos números enteros, 0 o más, separados por una coma. Ancho y alto en píxeles. Cualquiera de los dos valores, o ambos, se puede establecer en 0 para mantenerlos sin restricciones. No se aplica a solicitudes anidadas o incrustadas.<br>Consulte también [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html?lang=es#image-serving-api) en la API del servicio de imágenes.<br>Sin embargo, normalmente utiliza un ajuste preestablecido de visualizador o de imagen para entregar el recurso. La opción predeterminada solo se aplica a un recurso que no utiliza un ajuste preestablecido de visualizador o de imagen. |
| `defaultthumbpix` | `100,100` | Tamaño de miniatura predeterminado. Se usa en lugar del atributo::DefaultPix para solicitudes de miniaturas (`req=tmb`).<br>El servidor limita el tamaño de las imágenes de respuesta a esta altura y anchura máximas. Esta acción es verdadera si una solicitud de miniatura (`req=tmb`) no especifica el tamaño explícitamente ni el tamaño de vista explícitamente con `wid=`, `hei=` o `scl=`.<br>Se especifica como dos números enteros, 0 o más, separados por una coma. Ancho y alto en píxeles. Cualquiera de los dos valores, o ambos, se puede establecer en 0 para mantenerlos sin restricciones.<br>No se aplica a solicitudes anidadas/incrustadas.<br>Consulte también [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html?lang=es#image-serving-api) en la API del servicio de imágenes. |
| `expiration` | `36000000` | Duración predeterminada de la caché del cliente. Proporciona un intervalo de caducidad predeterminado en el caso de que el valor de catálogo::Expiration no sea válido en un registro de catálogo determinado.<br>Número real, 0 o superior. Número de milisegundos hasta la caducidad desde que se generaron los datos de respuesta. Si se establece en 0, la imagen de respuesta siempre caducará inmediatamente, lo que deshabilita el almacenamiento en caché del cliente. De forma predeterminada, este valor se establece en 10 horas, lo que significa que si se publica una imagen nueva, la imagen antigua tarda 10 horas en abandonar la caché del usuario. Póngase en contacto con Asistencia al cliente si necesita borrar la caché antes.<br>Consulte también [Caducidad](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html?lang=es) en la API del servicio de imágenes. |
| `jpegquality` | `80` | Atributos de codificación de JPEG predeterminados. Especifica los atributos predeterminados para las imágenes de respuesta de JPEG.<br>Número entero e indicador, separados por una coma. El primer valor está en el rango 1.. 100 y define la calidad. El segundo valor puede ser 0 para un comportamiento normal o 1 para desactivar la disminución de resolución de cromaticidad de RGB empleada por los codificadores JPEG.<br>Consulte también [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html?lang=es#image-serving-api) en la API del servicio de imágenes. |
| `maxpix` | `2000,2000` | Límite de tamaño de imagen de respuesta. Anchura y altura máximas para la imagen de respuesta que se devuelve al cliente.<br>El servidor devuelve un error si una solicitud genera una imagen de respuesta cuya anchura o altura sea mayor que el atributo::MaxPix.<br>Vea también [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html?lang=es#image-serving-api) en la API de servicio de imágenes. |
| `resmode` | `SHARP2` | Modo de remuestreo predeterminado. Especifica los atributos predeterminados de remuestreo e interpolación que se utilizarán para escalar los datos de imagen.<br>Se usa cuando `resMode=` no se especifica en una solicitud.<br>Los valores permitidos incluyen `BILIN`, `BICUB` o `SHARP2`.<br>Enumeración. Establezca como 2 para `bilin`, 3 para `bicub` o 4 para el modo de interpolación `sharp2`. Use `sharp2` para obtener mejores resultados.<br>Consulte también [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html?lang=es#image-serving-api) en la API de servicio de imágenes. |
| `resolution` | `72` | Resolución de objeto predeterminada. Proporciona una resolución de objeto predeterminada en el caso de que el valor de catálogo::Resolution no sea válido en un registro de catálogo determinado.<br>Número real, mayor que 0. Normalmente se expresa como píxeles por pulgada, pero también puede expresarse en otras unidades, como píxeles por metro.<br>Consulte también [Resolución](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-resolution.html?lang=es#image-serving-api) en la API del servicio de imágenes. |
| `thumbnailtime` | `1%,11%,21%,31%,41%,51%,61%,71%,81%,91%` | Estos valores representan una instantánea del tiempo de reproducción del vídeo y se pasan a [encoding.com](https://www.encoding.com/). Consulte [Acerca de la miniatura de vídeo](/help/assets/video.md#about-video-thumbnails-in-dynamic-media-hybrid-mode) para obtener más información. |

## Configuración de la administración de color de Dynamic Media {#configuring-dynamic-media-color-management}

La administración de color de Dynamic Media le permite corregir el color de los recursos para previsualizarlos.

Con la corrección de color, los recursos ingeridos conservan su espacio de color (RGB, CMYK, gris) y el perfil de color incrustado en la representación piramidal de TIFF generada. Cuando se solicita una representación dinámica, el color de la imagen se corrige en el espacio de color de destino. El perfil de color de salida se configura en la configuración de publicación de Dynamic Media en el JCR.

La gestión del color de Adobe utiliza perfiles ICC (International Color Consortium), un formato definido por ICC.

Puede configurar la administración de color de Dynamic Media y los ajustes preestablecidos de imagen mediante la salida CMYK, RGB o Gris. Consulte [Configuración de ajustes preestablecidos de imagen](/help/assets/managing-image-presets.md).

Los casos de uso avanzados podrían utilizar un modificador `icc=` de configuración manual para seleccionar explícitamente un perfil de color de salida:

* `icc` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html?lang=es](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-icc.html?lang=es)

* `iccEmbed` - [https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html?lang=es](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-iccembed.html?lang=es)

>[!NOTE]
>
>El conjunto estándar de perfiles de color de Adobe solo está disponible si tiene instalado [Feature Pack 12445 de Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-12445). Todos los paquetes de funciones y paquetes de servicio están disponibles en [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html). Feature Pack 12445 proporciona los perfiles de color de Adobe.


### Instalación del paquete de funciones 12445 {#installing-feature-pack}

Para utilizar las funcionalidades de administración de color de Dynamic Media, instale el paquete de funciones 12445.

**Para instalar el paquete de funciones 12445:**

1. Vaya a [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/es/aem.html) y descargue `cq-6.3.0-featurepack-12445`.

   Consulte [Cómo trabajar con paquetes](/help/sites-administering/package-manager.md) para obtener más información sobre cómo usar paquetes en [!DNL Adobe Experience Manager].

1. Instale el paquete de funciones.

### Configuración de los perfiles de color predeterminados {#configuring-the-default-color-profiles}

Después de instalar el paquete de funciones, configure los perfiles de color predeterminados adecuados para habilitar la corrección de color al solicitar datos de imagen RGB o CMYK.

**Para configurar los perfiles de color predeterminados:**

1. En **[!UICONTROL Herramientas]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**, vaya a `/conf/global/settings/dam/dm/imageserver/jcr:content` que contiene los perfiles de Adobe Color predeterminados.

   ![chlimage_1-514](assets/chlimage_1-514.png)

1. Agregue una propiedad de corrección de color desplazándose hasta la parte inferior de la ficha **[!UICONTROL Propiedades]**. Introduzca manualmente el nombre, el tipo y el valor de la propiedad, que se describe en las tablas siguientes. Después de escribir los valores, selecciona **[!UICONTROL Agregar]** y luego **[!UICONTROL Guardar todo]** para guardar los valores.

   Las propiedades de corrección de color se describen en la tabla **Propiedades de corrección de color**. Los valores que puede asignar a las propiedades de corrección de color se encuentran en la tabla **Perfil de color**.

   Por ejemplo, en **[!UICONTROL Nombre]**, agregue `iccprofilecmyk`, seleccione **[!UICONTROL Tipo]** `String` y agregue `WebCoated` como **[!UICONTROL Valor]**. A continuación, seleccione **[!UICONTROL Agregar]** y **[!UICONTROL Guardar todo]** para guardar sus valores.

   ![chlimage_1-515](assets/chlimage_1-515.png)

   **Tabla de propiedades de corrección de color**

<table>
 <tbody>
  <tr>
   <td><strong>Propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Predeterminado</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html?lang=es">iccprofilergb</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color predeterminado de RGB.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html?lang=es">iccprofilecmyk</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color CMYK predeterminado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html?lang=es">iccprofilegray</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color gris predeterminado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcrgb.html?lang=es">iccprofilesrcrgb</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color predeterminado de RGB utilizado para las imágenes de RGB que no tienen un perfil de color incrustado</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrccmyk.html?lang=es">iccprofilesrccmyk</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color CMYK predeterminado utilizado para imágenes CMYK que no tienen un perfil de color incrustado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilesrcgray.html?lang=es">iccprofilesrcgray</a></td>
   <td>Cadena</td>
   <td>&lt;empty&gt;</td>
   <td>Nombre del perfil de color gris predeterminado utilizado para imágenes CMYK que no tienen un perfil de color incrustado.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccblackpointcompensation.html?lang=es">iccblackpointcompensación</a></td>
   <td>Booleano</td>
   <td>Verdadero</td>
   <td>Especifica si la compensación del punto negro se realiza durante la corrección de color. Adobe recomienda que esta configuración esté activada.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccdither.html?lang=es">icoditera</a></td>
   <td>Booleano</td>
   <td>Falso</td>
   <td>Especifica si el tramado se realiza durante la corrección de color.</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html?lang=es">iccrenderIntent</a></td>
   <td>Cadena</td>
   <td>relativo</td>
   <td><p>Especifica la intención de procesamiento. Los valores aceptables son: <strong>perceptual, relative, saturation, absolute. </strong><i></i>Adobe recomienda <strong>relativo </strong><i></i>como valor predeterminado.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Los nombres de propiedad distinguen entre mayúsculas y minúsculas y deben estar en minúscula.

**Tabla de perfiles de color**

Se instalan los siguientes perfiles de color:

<table>
 <tbody>
  <tr>
   <th><p>Nombre</p> </th>
   <th><p>Ritmo de colores</p> </th>
   <th><p>Descripción</p> </th>
  </tr>
  <tr>
   <td>Adobe RGB</td>
   <td>RGB</td>
   <td>Adobe RGB (1998)</td>
  </tr>
  <tr>
   <td>AppleRGB</td>
   <td>RGB</td>
   <td>Apple RGB</td>
  </tr>
  <tr>
   <td>CIERGB</td>
   <td>RGB</td>
   <td>CIE RGB</td>
  </tr>
  <tr>
   <td>CoatedFogra27</td>
   <td>CMYK</td>
   <td>FOGRA27 recubierto (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedFogra39</td>
   <td>CMYK</td>
   <td>FOGRA39 recubierto (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>CoatedGraCol</td>
   <td>CMYK</td>
   <td>Revestido GRACoL 2006 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>ColorMatchRGB</td>
   <td>RGB</td>
   <td>ColorMatch RGB</td>
  </tr>
  <tr>
   <td>EuropeISOCoated</td>
   <td>CMYK</td>
   <td>Europa ISO Coated FOGRA27</td>
  </tr>
  <tr>
   <td>EuroscaleCoated</td>
   <td>CMYK</td>
   <td>Euro scale Coated v2</td>
  </tr>
  <tr>
   <td>EuroscaleUncovered</td>
   <td>CMYK</td>
   <td>Escala de euro sin recubrir v2</td>
  </tr>
  <tr>
   <td>JapanColorCoated</td>
   <td>CMYK</td>
   <td>Japón Color 2001 Revestido</td>
  </tr>
  <tr>
   <td>JapanColorNewspaper</td>
   <td>CMYK</td>
   <td>Japón Color 2002 Periódico</td>
  </tr>
  <tr>
   <td>JapanColorUncovered</td>
   <td>CMYK</td>
   <td>Japón Color 2001 Sin recubrimiento</td>
  </tr>
  <tr>
   <td>JapanColorWebCoated</td>
   <td>CMYK</td>
   <td>Japón Color 2003 Web Coated</td>
  </tr>
  <tr>
   <td>JapanWebCoated</td>
   <td>CMYK</td>
   <td>Japón Web Coated (Ad)</td>
  </tr>
  <tr>
   <td>NewsprintSNAP2007</td>
   <td>CMYK</td>
   <td>Boletín de Estados Unidos (SNAP 2007)</td>
  </tr>
  <tr>
   <td>NTSC</td>
   <td>RGB</td>
   <td>NTSC (1953)</td>
  </tr>
  <tr>
   <td>AMIGO</td>
   <td>RGB</td>
   <td>PAL/SECAM</td>
  </tr>
  <tr>
   <td>ProPhoto</td>
   <td>RGB</td>
   <td>ProPhoto RGB</td>
  </tr>
  <tr>
   <td>PS4Predeterminado</td>
   <td>CMYK</td>
   <td>CMYK predeterminado de Photoshop 4</td>
  </tr>
  <tr>
   <td>PS5Default</td>
   <td>CMYK</td>
   <td>CMYK predeterminado de Photoshop 5</td>
  </tr>
  <tr>
   <td>Revestido Con Hojas</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Coated v2</td>
  </tr>
  <tr>
   <td>Con hojasSin recubrir</td>
   <td>CMYK</td>
   <td>U.S. Sheetfed Uncovered v2</td>
  </tr>
  <tr>
   <td>SMPTE</td>
   <td>RGB</td>
   <td>SMPTE-C</td>
  </tr>
  <tr>
   <td>sRGB</td>
   <td>RGB</td>
   <td>sRGB IEC61966-2.1</td>
  </tr>
  <tr>
   <td>Fogra29 sin recubrimiento</td>
   <td>CMYK</td>
   <td>FOGRA29 sin recubrimiento (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoated</td>
   <td>CMYK</td>
   <td>U.S. Web Coated (SWOP) v2</td>
  </tr>
  <tr>
   <td>WebCoatedFogra28</td>
   <td>CMYK</td>
   <td>Revestimiento Web FOGRA28 (ISO 12647-2:2004)</td>
  </tr>
  <tr>
   <td>WebCoatedGrade3</td>
   <td>CMYK</td>
   <td>Papel SWOP 2006 Grado 3 Revestido por Web</td>
  </tr>
  <tr>
   <td>WebCoatedGrade5</td>
   <td>CMYK</td>
   <td>Papel SWOP 2006 Grado 5 Revestido por Web</td>
  </tr>
  <tr>
   <td>WebUncovered</td>
   <td>CMYK</td>
   <td>U.S. Web Uncovered v2</td>
  </tr>
  <tr>
   <td>WideGamutRGB</td>
   <td>RGB</td>
   <td>RGB de gama amplia</td>
  </tr>
 </tbody>
</table>

1. Seleccione **[!UICONTROL Guardar todo]**.

Por ejemplo, podría establecer **[!UICONTROL iccprofilergb]** en `sRGB` y **[!UICONTROL iccprofilecmyk]** en **[!UICONTROL WebCoated]**.

Al hacerlo, se haría lo siguiente:

* Activa la corrección de color para imágenes RGB y CMYK.
* Se supone que las imágenes de RGB que no tienen un perfil de color están en el espacio de color *sRGB*.
* Se supone que las imágenes CMYK que no tienen un perfil de color están en *WebCoated* espacio de color.
* Representaciones dinámicas que devuelven la salida de RGB, devuélvala en el espacio de color *sRGB.
* Representaciones dinámicas que devuelven resultados CMYK, devuélvalos en el espacio de color *WebCoated*.

## Entrega de Assets {#delivering-assets}

Una vez completadas todas las tareas anteriores, los recursos activados de Dynamic Media se proporcionan desde el servicio de imagen o vídeo. En Experience Manager, esta capacidad aparece en **[!UICONTROL Copiar URL de imagen]**, **[!UICONTROL Copiar URL del visor]**, **[!UICONTROL Incrustar código de visor]** y en WCM.

Consulte [Entrega de Dynamic Media Assets](/help/assets/delivering-dynamic-media-assets.md).

<table>
 <tbody>
  <tr>
   <td><strong>Cuando...</strong></td>
   <td><strong>Resultado</strong></td>
  </tr>
  <tr>
   <td>Copiar una URL de imagen</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una URL similar a la siguiente (la URL solo es para fines de demostración):</p> <p><code>https://IMAGESERVICEPUBLISHNODE/is/image/content/dam/path/to/Image.jpg?$preset$</code></p> <p>Donde <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar una URL de visor</td>
   <td><p>El cuadro de diálogo Copiar URL muestra una URL similar a la siguiente (la URL solo es para fines de demostración):</p> <p><code>https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/BasicZoomViewer.html?asset=/content/dam/path/to/Image.jpg&config=/conf/global/settings/dam/dm/presets/viewer/Zoom_dark&serverUrl=https://IMAGESERVICEPUBLISHNODE/is/image/&contentRoot=%2F</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación normal de Experience Manager y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de Dynamic Media Assets</a>.</p> </td>
  </tr>
  <tr>
   <td>Copiar el código incrustado de un visor</td>
   <td><p>El cuadro de diálogo Copiar código incrustado muestra un fragmento de código similar al siguiente (el ejemplo de código es solo para fines de demostración):</p> <p><code class="code">&lt;style type="text/css"&gt;
       &#x200B;#s7basiczoom_div.s7basiczoomviewer&lbrace;
       width:100%;
       height:auto;
       &rbrace;
       &lt;/style&gt;
       &lt;script
       type="text/javascript" src="https://PUBLISHNODE/etc/dam/viewers/s7viewers/html5/js/BasicZoomViewer.js"&gt;&lt;/script&gt;
       &lt;div id="s7basiczoom_div"&gt;&lt;/div&gt;
       &lt;script type="text/javascript"&gt;
       var s7basiczoomviewer = new s7viewers.BasicZoomViewer(&lbrace;
       "containerId" : "s7basiczoom_div",
       "params" : &lbrace;
       "serverurl" : "https://IMAGESERVICEPUBLISHNODE/is/image/",
       "contenturl" : "https://PUBLISHNODE/",
       "config" : "/conf/global/settings/dam/dm/presets/viewer/Zoom_dark",
       "asset" : "/content/dam/path/to/Image.jpg" &rbrace;
       &rbrace;).init();
       &lt;/script&gt;</code></p> <p>Donde <code>PUBLISHNODE</code> hace referencia al nodo de publicación normal de Experience Manager y <code>IMAGESERVICEPUBLISHNODE</code> hace referencia a la URL del servicio de imágenes.</p> <p>Consulte también <a href="/help/assets/delivering-dynamic-media-assets.md">Entrega de Dynamic Media Assets</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Componentes de Dynamic Media y Interactive Media de WCM {#wcm-dynamic-media-and-interactive-media-components}

Las páginas de WCM que hacen referencia a componentes de Dynamic Media e Interactive Media hacen referencia al servicio de entrega.
