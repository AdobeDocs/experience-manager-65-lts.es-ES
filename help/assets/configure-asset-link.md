---
title: Configuración de Experience Manager Assets para Adobe Asset Link
description: Configure Experience Manager Assets para utilizarlo con la extensión Adobe Asset Link para aplicaciones de Creative Cloud.
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
exl-id: 110b7175-d398-40ff-886e-5817a1df0ec9
source-git-commit: ce0da5056e0821c94eb06a05c663a3939b37f940
workflow-type: tm+mt
source-wordcount: '3056'
ht-degree: 0%

---

# Configuración de Experience Manager Assets para Adobe Asset Link {#adobe-asset-link}

[Adobe Asset Link (AAL)](https://www.adobe.com/es/creativecloud/business/enterprise/adobe-asset-link.html) optimiza la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido. Conecta Adobe Experience Manager Assets con aplicaciones de escritorio de Creative Cloud, Adobe InDesign, Adobe Photoshop y Adobe Illustrator. El panel Adobe Asset Link permite a los creativos acceder al contenido almacenado en los AEM Assets y modificarlo sin salir de las aplicaciones creativas con las que están más familiarizados.

Para configurar Experience Manager Assets para que se utilice con Asset Link, implemente las siguientes tareas. Utilice la cuenta de administrador de Experience Manager para realizar la configuración:

1. Instale los paquetes según sea necesario. Los detalles se encuentran en [requisitos previos](#prerequisites).

1. Configure Experience Manager [manualmente](#manual-configuration) o usando un [paquete](#configure-using-package).

1. Para asignar usuarios con licencia de Creative Cloud a usuarios de Experience Manager, administra [control de acceso de usuario](#user-access).

1. Cree [índice de consultas personalizado](#create-custom-index), configure [representaciones de FPO](/help/assets/configure-fpo-renditions.md) para InDesign, configure [integración de Adobe Stock](/help/assets/aem-assets-adobe-stock.md) y configure [búsqueda visual o de similitudes](/help/assets/search-assets.md#configvisualsearch).

## Requisitos previos y compatibilidad con varias funcionalidades {#prerequisites}

Asegúrese de instalar el paquete de servicio y el paquete adecuados según sea necesario. Consulte los siguientes requisitos para cada versión de Experience Manager y para obtener funciones específicas.

| Capacidad de Assets | Versión de Experience Manager y requisitos de asistencia |
|--- |--- |
| Asset Link funciona de forma predeterminada | Experience Manager 6.5 y 6.5.2 o posterior. </br> Experience Manager 6.4.4 y 6.4.6 o posterior. </br> Adobe recomienda instalar el [Service Pack (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=es) de Experience Manager más reciente antes de usar AAL. |
| Asset Link funciona después de instalar un paquete | Para Experience Manager 6.4.0 - 6.4.3, instale el paquete [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support). |
| Integración de Adobe Stock | Experience Manager 6.4.2 o posterior |
| Búsqueda visual o por similitud | Experience Manager 6.5.0 o posterior |


## Configure Experience Manager con el paquete de configuración {#configure-using-package}

Adobe recomienda instalar el paquete de configuración [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) para automatizar la mayoría de las tareas de configuración, seguido de algunas tareas manuales. También puede [configurar manualmente](#manual-configuration).

>[!CAUTION]
>
>Si la instancia de Experience Manager está configurada para que el usuario inicie sesión con cuentas de IMS de Adobe, no utilice el paquete de configuración. En su lugar, [configure manualmente](#manual-configuration) su instancia de Experience Manager.

1. Para abrir el Administrador de paquetes, en la interfaz web de Experience Manager, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Implementación]** > **[!UICONTROL Uso compartido de paquetes]**. Instale el paquete `adobe-asset-link-config`.

1. Acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Busque la configuración **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** y haga clic para editarla.

   Establezca las siguientes propiedades y guarde los cambios.

   * [!UICONTROL Asignaciones de grupo]: dejar vacío a menos que lo desee. Para obtener más información, consulte [Asignación de grupo](#group-mapping).
   * [!UICONTROL Organización]: escriba el identificador de organización que está usando en Adobe Admin Console. Para obtener más información sobre los identificadores de organización, consulte [Crear grupo de usuarios](https://helpx.adobe.com/es/enterprise/using/create-aal-user-group.html).

1. Busque la configuración **[!UICONTROL Controlador de autenticación del portador de Granite de Adobe]** y haga clic para editarla.

   Agregue los ID de cliente **[!UICONTROL InDesignAem2]** a la propiedad de configuración **[!UICONTROL ID de cliente OAuth permitidos]**.


## Configuración manual de Experience Manager {#manual-configuration}

Configure Experience Manager manualmente si decide no utilizar un paquete de configuración o si su implementación de Experience Manager está configurada para admitir el inicio de sesión del usuario con cuentas de IMS de Adobe.

Para configurar Experience Manager manualmente:

1. Para obtener acceso al administrador de configuración, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**. Seleccione **[!UICONTROL OSGi]** > **[!UICONTROL Configuración]** en el menú de la parte superior.

1. Busque la configuración **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** y haga clic para editarla.

   Establezca la siguiente configuración y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL Punto final de autorización]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL Extremo de token]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL Extremo de perfil]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL URL de validación]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL Organización]: establecida en el identificador de organización en [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL Asignaciones de grupos]: déjelo vacío a menos que tenga un caso especial. Para obtener más información, consulte [Asignación de grupo](#group-mapping).

1. Busque la configuración **[!UICONTROL Controlador de autenticación del portador de Granite de Adobe]** y haga clic para editarla.

   Agregue los siguientes ID de cliente a la propiedad de configuración **[!UICONTROL ID de cliente de OAuth permitidos]**: `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   Para agregar cada `Client ID`, haga clic en `+`. Haga clic en **[!UICONTROL Guardar]** después de agregar todos los identificadores.

1. En la configuración de **[!UICONTROL Proveedor y aplicación OAuth de Adobe Granite]**, inspeccione las instancias existentes de **[!UICONTROL Proveedor y aplicación OAuth de Adobe Granite]**. Si encuentra una instancia con el valor `Config ID` de `ims`, utilícela para las instrucciones de este procedimiento. De lo contrario, haga clic en `+` para crear una instancia de configuración. Establezca los siguientes valores de propiedad y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL ID de cliente]: no cambiar
   * [!UICONTROL Secreto de cliente]: No cambiar
   * [!UICONTROL Id. de configuración]: ` ims`
   * [!UICONTROL Ámbito]: `AdobeID, OpenID, read_organizations` (otros valores también pueden estar en la configuración)
   * [!UICONTROL Id. de proveedor]: ` ims`
   * [!UICONTROL Crear usuarios]: ` Checked`
   * [!UICONTROL Propiedad de ID de usuario]: `Email` para la configuración recién creada. De lo contrario, no cambie.

1. Busque la configuración del **[!UICONTROL Controlador de sincronización predeterminado de Apache Jackrabbit Oak]** con el **[!UICONTROL Nombre del controlador de sincronización]** `ims` y haga clic para editarlo.

   Establezca las siguientes propiedades de configuración y haga clic en **[!UICONTROL Guardar]**.

   * [!UICONTROL Tiempo de caducidad del usuario y caducidad de la pertenencia al usuario]: Tiempo en minutos seguido de &#39;m&#39; sin espacio. Por ejemplo, `15m` durante 15 minutos. Para obtener más información, consulte [Asignación de grupo](#group-mapping).
   * [!UICONTROL Inscripción automática de usuario]: No cambiar
   * [!UICONTROL Pertenencia dinámica de usuario]: ` Deslect`

1. Busque la configuración **[!UICONTROL Controlador de autenticación OAuth de Adobe Granite]** y haga clic para editarlo. Sin realizar ningún cambio, haz clic en **[!UICONTROL Guardar]**.

1. Para ajustar la prioridad relativa del controlador de autenticación del portador, en CRXDE, vaya a `/apps/system/config`. Busque `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` y abra su configuración. Al final, agregue `service.ranking=I"-10"`. Guarde los cambios.

   >[!NOTE]
   >
   >Cada solicitud autenticada con un token de portador incurre en la sobrecarga de tres llamadas a Adobe IMS, la sincronización de usuarios y la creación de un token de inicio de sesión en Experience Manager. Para compensar esta sobrecarga, Adobe Asset Link captura el token de inicio de sesión devuelto en la respuesta de Experience Manager y lo envía con solicitudes posteriores. Para que este proceso funcione, se debe ajustar la prioridad relativa del controlador de autenticación del portador.

1. (Opcional) Si los usuarios de Experience Manager tienen nombres de dominio en mayúsculas o en mayúsculas y minúsculas en sus ID de correo electrónico, seleccione **[!UICONTROL Cambiar el usuario de bloqueo a minúsculas]** en **[!UICONTROL Configuraciones de la plataforma ACP de Adobe Granite]** en la consola web de Experience Manager.

## Configuración adicional después de la migración a Perfiles de empresa {#configure-migration-activity}

Los usuarios de Adobe Asset Link pueden conectarse a Experience Manager para permitir el inicio de sesión de IMS desde la organización principal de Creative Cloud for Enterprise (CCE). Experience Manager utiliza los ID de cliente para identificar la organización de IMS permitida. Después de la migración a los perfiles empresariales, se debe configurar el ID de cliente y la clave secreta de la organización de IMS en Experience Manager para el controlador de autenticación del portador. Para obtener más información sobre los perfiles empresariales, consulte [introducción a los perfiles de Adobe](https://helpx.adobe.com/es/enterprise/kb/introducing-adobe-profiles.html?lang=es).

Solo se requiere una configuración adicional si utiliza diferentes organizaciones de Adobe IMS para Experience Manager y Creative Cloud para empresas (CCE) y se establece una relación de confianza de dominio entre estas dos organizaciones.

>[!NOTE]
>
>* La corrección de los perfiles empresariales se proporciona en Experience Manager 6.5.11.0.
>* La configuración existente sigue funcionando si utiliza la misma organización de Adobe IMS con Experience Manager y CCE.


**Requisitos previos**

1. Una instancia de Experience Manager en funcionamiento con la autenticación del portador configurada para AAL.
1. Instale el siguiente paquete (Service Pack 11) en su instancia de Experience Manager 6.5.

   [Descargar Experience Manager 6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Póngase en contacto con el [!UICONTROL Servicio de atención al cliente] para obtener el ID de cliente y la clave secreta para la autenticación del portador de su organización de IMS.

A continuación se indican las configuraciones adicionales que se requieren después de la migración a los perfiles empresariales:

1. En **[!UICONTROL Proveedor de configuración de Adobe Granite OAuth IMS]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`), establezca:

   * ID de configuración de OAuth (`oauth.configmanager.ims.configid`): `ims` (Verifíquelo una vez, puede que ya lo haya configurado)

   * Entidad propietaria de IMS (`ims.owningEntity`): su ID de organización de IMS

   ![ID de configuración de IMS](assets/bearer-authentication1.png)

1. Abra la configuración de **[!UICONTROL Controlador de autenticación del portador]** y agregue el ID de cliente obtenido de [!UICONTROL Atención al cliente] a la lista de **[!UICONTROL ID de cliente de OAuth permitidos]**.

   ![Agregar ID de cliente](assets/add-clientid-bearer-auth.png)

1. Abra la configuración **[!UICONTROL Aplicación y proveedor de Adobe Granite OAuth]** y agregue el **[!UICONTROL ID de cliente]** y el **[!UICONTROL Secreto de cliente]** (Clave secreta) obtenidos del Servicio de atención al cliente.

   Asegúrese de que el campo **[!UICONTROL Id. de configuración]** (`oauth.config.id`) contenga el mismo valor proporcionado en el campo **[!UICONTROL Id. de configuración de OAuth]** (`oauth.configmanager.ims.configid`) anterior.

   ![Verificar ID de cliente](assets/clientid-secretkey.png)

1. Abra la configuración del **[!UICONTROL Preprocesador de token de intercambio de clúster de Adobe Granite IMS]** y configúrelo en `enable`.

## Administrar el control de acceso de usuario {#user-access}

En esta sección se describe cómo administrar usuarios y su acceso al repositorio de Experience Manager.

### Asignación de grupos {#group-mapping}

La asignación de grupos determina cómo se corresponden los grupos en Experience Manager con los grupos en Adobe IMS. Desempeña un papel importante en la forma en que se concede permiso a los usuarios de Adobe Asset Link para acceder a Experience Manager Assets.

Cuando se utiliza con Adobe Asset Link, Experience Manager delega las funciones de administración de usuarios en Adobe IMS. Crea automáticamente usuarios y grupos que se corresponden con los usuarios y grupos de Adobe IMS. Además, sincroniza usuarios, grupos y miembros de grupos en Experience Manager para que coincidan con los de Adobe IMS.

Por ejemplo, imaginemos un escenario en el que los usuarios de Adobe Asset Link sean miembros del grupo de IMS de Adobe assetlink-users. En este caso, se crea un grupo sincronizado denominado assetlink-users en Experience Manager cuando un usuario de ese grupo de IMS de Adobe se conecta a Adobe Asset Link por primera vez. Cada nuevo usuario del grupo de IMS de Adobe se agrega al grupo correspondiente en Experience Manager cuando se conecta a Experience Manager a través de Adobe Asset Link por primera vez.

A los grupos de Experience Manager que corresponden a grupos de Adobe IMS y están sincronizados con ellos se les puede otorgar acceso directamente o haciéndolos miembros de otro grupo. A continuación, se muestra un ejemplo de cómo se pueden administrar los permisos.

![ejemplos de grupo](assets/group-examples.png)

Las siguientes reglas se aplican a las asignaciones de grupo en Experience Manager:

* Asegúrese de que la propiedad **[!UICONTROL Asignaciones de grupo]** de la configuración del **[!UICONTROL Proveedor de IMS de Adobe Granite OAuth]** esté en blanco.
* La pertenencia al grupo de usuarios de Adobe Asset Link se evalúa cuando el usuario se autentica y ha transcurrido el período de tiempo de la propiedad **[!UICONTROL Hora de caducidad del usuario]** en la configuración de **[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]**. Actualmente, los usuarios se pueden añadir y eliminar de grupos en Experience Manager para sincronizar con lo que se encuentra en Adobe IMS.
* Evite conflictos de nombres de grupo. Asegúrese de que los nombres utilizados para los grupos creados en Adobe IMS (para administrar usuarios) sean diferentes de todos los nombres de grupos del sistema de Experience Manager.

  Por ejemplo, asegúrese de que son diferentes del grupo `dam-users` y de los grupos creados por el administrador de Experience Manager.

  Un grupo de Adobe IMS cuyo nombre entra en conflicto con el de un grupo de sistema de Experience Manager o un grupo creado manualmente no se utiliza para controlar los permisos de usuario.
* Si un usuario de IMS de Adobe se conecta a una instancia de Experience Manager, en la que el nombre del usuario entra en conflicto con un usuario de Experience Manager creado anteriormente, se le asigna otro nombre con números añadidos para que sea único.

**Configurar el control de acceso por primera vez**

Los usuarios que se conectan mediante Adobe Asset Link solo pueden ver e interactuar con los recursos una vez que se les ha concedido el permiso necesario. La sección [Asignación de grupos](#group-mapping) anterior describe cómo se crean los grupos de usuarios en Experience Manager, que se corresponden con los grupos de usuarios de su organización dentro de Adobe IMS y se sincronizan con ellos. Se recomienda que los administradores de Experience Manager utilicen estos grupos para administrar el control de acceso de los usuarios de Adobe Asset Link.

Para cada grupo de Experience Manager sincronizado con un grupo de IMS de Adobe (que se utiliza para administrar el control de acceso de los usuarios):

1. Asegúrese de que el grupo tenga un miembro que pueda utilizarse para una conexión inicial desde Adobe Asset Link.
1. Utilice ese usuario para iniciar sesión en Adobe Asset Link y conectarse a Experience Manager. Se espera que esta conexión falle.
1. En Experience Manager, busque el grupo que corresponda al grupo en Adobe IMS y asígnele el control de acceso deseado. Por ejemplo, el nuevo grupo pasa a ser miembro del grupo dam-users.
1. Cierre Adobe Asset Link y reinicie la aplicación Creative Cloud.
1. Para comprobar que el usuario tiene el acceso esperado, vuelva a abrir Adobe Asset Link.

Una vez realizados estos pasos, otros usuarios del mismo grupo pueden conectarse a Experience Manager con Adobe Asset Link en su primer intento. Automáticamente tienen los mismos permisos que los demás usuarios del grupo.

## Administrar usuarios de Experience Manager para Adobe Asset Link {#manage-users}

Los usuarios de Adobe Asset Link pueden conectarse con Experience Manager cuando inician sesión en su aplicación de Creative Cloud. Esta autenticación utiliza la tecnología IMS de Adobe y crea información de usuario en Experience Manager, en caso de que no exista. Es habitual que los clientes empresariales de Experience Manager administren sus usuarios con un proveedor de identidad externo integrado con Experience Manager. Los proveedores de identidad incluyen Adobe IMS y otros productos que utilizan los protocolos SAML y LDAP. Alternativamente, los usuarios se pueden crear y administrar localmente en Experience Manager.

Los usuarios que se conectan a Experience Manager desde Adobe Asset Link no entran en conflicto con la información de usuario existente almacenada en Experience Manager desde el inicio de sesión directo anterior, en los casos siguientes:

* Todos los nombres de usuario utilizados para el inicio de sesión directo en Experience Manager son diferentes de los nombres de usuario utilizados en el inicio de sesión de Adobe IMS para Creative Cloud.
* Adobe IMS se utiliza como proveedor de identidad para el inicio de sesión directo de Experience Manager.
* Los usuarios se conectan a Experience Manager desde Adobe Asset Link antes de iniciar sesión directamente en Experience Manager con la misma cuenta.


Por otro lado, la información de usuario creada como resultado del inicio de sesión directo de Experience Manager debe actualizarse para que funcione con Adobe Asset Link, en los siguientes casos:

* El mismo nombre de usuario, como la dirección de correo electrónico del usuario, se utiliza para ambos: la cuenta en Creative Cloud, que utiliza Adobe IMS, y la cuenta en un proveedor de identidad externo que no sea Adobe IMS.
* Se utiliza el mismo nombre de usuario para la cuenta de Creative Cloud y para una cuenta de Experience Manager local.
* Las cuentas de Creative Cloud en Adobe IMS son Federated ID, que son proporcionadas por el mismo proveedor de identidad externo que se ha integrado con Experience Manager para el inicio de sesión directo.

Los usuarios creados a través de estos escenarios no tienen una propiedad que sea necesaria para los usuarios, los cuales se sincronizan con Adobe IMS.

Para actualizar a estos usuarios en Experience Manager para que trabajen con Adobe Asset Link:

1. En la consola web de Experience Manager, busque la configuración **[!UICONTROL Configuración principal externa de Apache Jackrabbit Oak]** y haga clic para editarla. Anule la selección de la casilla **[!UICONTROL Protección de identidad externa]** y haga clic en **[!UICONTROL Guardar]**.
1. Para obtener acceso a la interfaz de administración de usuarios en Experience Manager, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**. Seleccione el usuario que desea actualizar y anote el final de la ruta URL del explorador para ese usuario, empezando por `/home/users`. También puede buscar el nombre de usuario en CRXDE. Ruta de acceso de usuario de ejemplo: `/home/users/x/xTac082TDh-guJzzG7WM`.
1. En CRXDE, vaya a la ruta del usuario, seleccione el nodo del usuario y vea las propiedades del nodo seleccionando la pestaña **[!UICONTROL Propiedades]** en el área inferior central. Este nodo tiene un valor de propiedad `jcr:primaryType` de `rep:User`.
1. En la parte inferior del área de la ficha **[!UICONTROL Propiedades]**, escriba un valor `Name` de `rep:externalId`, un valor `Type` de `String` y un valor `Value` de `rep:authorizableId`;`ims`, donde `rep:authorizableId` es el valor de la propiedad `rep:authorizableId` del nodo. (Se utiliza un punto y coma sin espacios para separar el valor `rep:authorizableId` de `ims`.)
1. Haga clic en el botón **[!UICONTROL Agregar]** a la derecha de la nueva entrada y, a continuación, haga clic en **[!UICONTROL Guardar todo]**.
1. Repita los pasos del 2 al 5 con cualquier otro usuario que desee actualizar para trabajar con Adobe Asset Link.
1. En la consola web de Experience Manager, busque la configuración **[!UICONTROL Configuración principal externa de Apache Jackrabbit Oak]** y haga clic para editarla. Anule la selección de la casilla **[!UICONTROL Protección de identidad externa]** y haga clic en **[!UICONTROL Guardar]**.

>[!NOTE]
>
>Si los servicios no se restauran en unos minutos, reinicie Experience Manager para permitir autenticaciones correctas.

Después de este cambio, un usuario de Experience Manager actualizado puede conectarse con Adobe Asset Link y seguir utilizando el método de inicio de sesión directo en Experience Manager que se utilizaba antes de la actualización. Si la autenticación con Adobe IMS se realiza correctamente, la información del perfil de usuario de Experience Manager se sincroniza con el perfil de usuario en Adobe IMS.

Existe un método mediante el cual se puede realizar una migración masiva de varios usuarios de Experience Manager para permitirles trabajar con Adobe Asset Link. Póngase en contacto con Adobe Care para obtener más información y ayuda sobre cómo habilitar esta opción.

Como alternativa a los pasos, en determinadas circunstancias, se puede proporcionar a un usuario de Adobe Asset Link acceso rápido a Experience Manager. En estos casos, la información de usuario preexistente se encuentra y elimina con la administración de usuarios de Experience Manager o Experience Manager CRXDE antes de su conexión con Adobe Asset Link. La nueva información de usuario se crea en Experience Manager después de la conexión. Utilice este método solo si está seguro de que no hay datos importantes que se agreguen como secundarios del nodo de usuario. Estos datos adicionales son cualquier nodo que sea secundario del nodo del usuario distinto de los nodos `tokens`, `preferences`, `profile`, `profiles`, `profiles/public` y `rep:policy/*`.

## Flujo de trabajo de inicio automático para procesar recursos de forma condicional {#auto-start-workflow}

En Experience Manager 6.4 y Experience Manager 6.5, los administradores pueden configurar flujos de trabajo para que se ejecuten y procesen automáticamente los recursos en función de condiciones predefinidas.

La configuración es útil para usuarios y especialistas en marketing de línea de negocios, por ejemplo, para crear un flujo de trabajo personalizado en unas pocas carpetas específicas. Supongamos que todos los activos de la sesión fotográfica de una agencia pueden marcarse como agua o que todos los activos cargados por un freelancer pueden procesarse para crear representaciones específicas.

Para obtener más información y para la configuración de Experience Manager, consulte [flujo de trabajo de ejecución automática en los recursos](/help/assets/assets-workflow.md#auto-execute-workflow-on-some-assets).

## Crear un índice personalizado en las versiones de Experience Manager 6.4.x {#create-custom-index}

Experience Manager contiene índices que se utilizan para consultas. Cree el siguiente índice personalizado para la versión especificada. Experience Manager 6.5.0 contiene este índice de forma predeterminada. Adobe Asset Link requiere este índice para determinar qué recursos ha retirado un usuario.

1. En CRXDE, busque el nodo `/oak:index`. Cree un nodo denominado `cqDrivelock` y establezca su `Type` en `oak:QueryIndexDefinition`.

1. Agregue las siguientes propiedades al nuevo nodo y guarde los cambios:

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## Configurar la búsqueda visual o de similitudes {#configure-visual-similarity-search}

La funcionalidad Búsqueda visual permite buscar recursos visualmente similares en el repositorio de AEM Assets mediante el panel Adobe Asset Link. La funcionalidad está disponible en 6.5.0 o versiones posteriores y solo se buscan los recursos indexados. Para obtener más información, vea [cómo configurar la búsqueda visual](/help/assets/search-assets.md#configvisualsearch).

## Generar representaciones solo para ubicación para Adobe InDesign {#fpo-renditions}

Experience Manager proporciona representaciones que se utilizan solo para ubicación (FPO). Estas representaciones de FPO tienen un tamaño de archivo pequeño, pero son de la misma proporción de aspecto. Si una representación de FPO no está disponible para un recurso, Adobe InDesign utiliza el recurso original en su lugar. Este mecanismo de reserva garantiza que el flujo de trabajo creativo se desarrolle sin interrupciones. Para obtener más información, vea [generar representaciones de FPO](/help/assets/configure-fpo-renditions.md).


## Integración con Adobe Stock {#adobe-stock-integration}

Las organizaciones integran sus cuentas de Adobe Stock con Experience Manager Assets. Ayuda a los especialistas en marketing a poner a disposición de sus proyectos creativos y de marketing fotografías, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad y libres de derechos de autor. Los profesionales de Creative pueden utilizar estos recursos mediante el panel Asset Link.

Para integrar con Adobe Stock, consulte [Recursos de Adobe Stock en Experience Manager Assets](/help/assets/aem-assets-adobe-stock.md). Se requiere Experience Manager 6.4.2 o posterior para la integración con Adobe Stock.


## Solucionar problemas relacionados con Experience Manager {#troubleshoot}


Si tiene problemas al configurar o utilizar Adobe Asset Link, intente lo siguiente:

* Asegúrese de que la implementación cumpla los requisitos previos. Concretamente, asegúrese de que están instalados los paquetes de funciones o paquetes adecuados.
* Póngase en contacto con el socio o integrador de sistemas de su organización.
* Si los usuarios de Creative Cloud no pueden comprobar los recursos desprotegidos, compruebe el uso de mayúsculas y minúsculas en los nombres de dominio en los ID de correo electrónico. Para solucionarlo, consulte [configuración manual](#manual-configuration).
* Para obtener más información, consulte [solucionar problemas de Asset Link](https://helpx.adobe.com/es/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [Acerca de Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html)
>* [Use Asset Link en la aplicación de escritorio de Creative Cloud y administre recursos](https://helpx.adobe.com/es/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [Configurar Adobe Experience Manager Assets as a Cloud Service](https://helpx.adobe.com/es/enterprise/using/configure-aem-assets-for-asset-link.html).
