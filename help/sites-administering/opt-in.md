---
title: Inclusión en Adobe Analytics y Adobe Target
description: Obtenga información sobre cómo adherirse a Adobe Analytics y Adobe Target.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 10%

---

# Inclusión en Adobe Analytics y Adobe Target{#opting-into-adobe-analytics-and-adobe-target}

AEM cuenta con un procedimiento de inclusión para ayudarle a integrar con Adobe Analytics y Adobe Target. Esta opción está disponible de forma predeterminada, como una tarea precargada asignada al grupo de usuarios del administrador.

Cuando inicia sesión como administrador, esta tarea (**Configuración de Analytics y Target**) está disponible en la [Bandeja de entrada](/help/sites-authoring/inbox.md#out-of-the-box-administrative-tasks). En función de las credenciales que proporcione, le ayuda a configurar e integrar estos servicios.

Tiene las siguientes opciones para configurar la integración:

* Configure la integración mediante la tarea.

  Esto se puede hacer de inmediato o más tarde, la tarea permanecerá en la Bandeja de entrada hasta que se realice alguna acción. En cualquier caso, la configuración se puede realizar directamente en la interfaz de usuario o con el uso de un archivo `.properties` predefinido.

* Exclusión de la integración.

  Considere esta opción si prefiere [configurar manualmente la integración](/help/sites-administering/marketing-cloud.md). Consulte también [Integración de AEM con Adobe Target y Adobe Analytics mediante DTM](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

* Configure la configuración y el aprovisionamiento mediante una secuencia de comandos.

## Configuración de la integración {#configuring-the-integration}

Inclusión en la integración con:

* Analytics para habilitar el uso de las funcionalidades de análisis y seguimiento de páginas.
* Target para habilitar el uso de sus capacidades de personalización.

Para cualquiera de las opciones, debe proporcionar la información de la cuenta de usuario y especificar las páginas de las que se realiza un seguimiento.

>[!NOTE]
>
>Si lo desea, puede proporcionar información de cuentas de Analytics y Target mediante un archivo de propiedades que se lee al iniciar el servidor. Ver [Proporcionar información de la cuenta mediante un archivo de propiedades](/help/sites-administering/opt-in.md#providing-account-information-using-a-properties-file).

Al adherirse a la integración, AEM realiza las siguientes tareas:

* Crea las configuraciones en la nube que habilitan la conexión con Analytics y Target.
* Crea los marcos que determinan los datos de los que se realiza un seguimiento.
* Configura las páginas web para utilizar estos servicios.

>[!NOTE]
>
>AT.js es la biblioteca de cliente predeterminada. Esto está configurado en su [configuración de servicios en la nube de Target](/help/sites-administering/target-configuring.md#creating-a-target-cloud-configuration).
>
>Adobe recomienda usar AT.js como biblioteca de cliente.

Para desactivar la tarea predeterminada precargada de, haga lo siguiente:

1. En la bandeja de entrada [seleccione y **abra** la tarea Configurar Analytics y Target](/help/sites-authoring/inbox.md#taking-action-on-an-item).

   ![optin-01](assets/optin-01.png)

1. Para Analytics:

   1. Escriba la información de la cuenta de usuario de Analytics y, a continuación, haga clic en el botón **Agregar** correspondiente.
   1. Se autentican las credenciales adecuadas.
   1. Cuando la cuenta de Analytics esté autenticada, seleccione el grupo de informes de Analytics que desee utilizar. AEM recupera esos grupos de informes de Analytics. El estado se ha actualizado a **Añadido**.

1. Para Target:

   1. Escriba la información de la cuenta de usuario de Target y haga clic en el botón **Agregar** correspondiente.
   1. Se autentican las credenciales adecuadas. El estado se ha actualizado a **Añadido**.

1. Seleccione **Siguiente**.
1. Seleccione los sitios para los que se deben usar Analytics o Target.

1. Seleccione **Listo** para completar.

   >[!CAUTION]
   >
   >Después de adherirse a la configuración, debe publicar el sitio o las páginas afectadas para replicar estos cambios en la instancia de publicación.

## Exclusión de la integración {#opting-out-of-the-integration}

Desactivar la integración con Analytics y Target cuando:

* No desea integrar con estos productos.
* Prefiera configurar las integraciones manualmente.

  Para obtener información sobre cómo configurar las integraciones manualmente, consulte [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md) e [Integración con Adobe Target](/help/sites-administering/target.md).

Para desactivar, debe completar la tarea precargada:

* En la bandeja de entrada [seleccione y **complete** la tarea Configurar Analytics y Target](/help/sites-authoring/inbox.md#taking-action-on-an-item).

## Proporcionar información de la cuenta mediante un archivo de propiedades {#providing-account-information-using-a-properties-file}

Instale un archivo de propiedades que AEM lea al iniciar el servidor para configurar las propiedades de la cuenta para la integración con Analytics y Target. Al utilizar el archivo de propiedades, el asistente de inclusión utiliza automáticamente las propiedades del archivo y la configuración de nube se crea en consecuencia.

El archivo de propiedades es un archivo de texto denominado marketingcloud.properties que se guarda en el directorio de trabajo que utiliza el proceso de AEM (normalmente en el mismo directorio que el archivo JAR). El archivo incluye las siguientes propiedades:

* analytics.server: la dirección URL del centro de datos de Analytics que utiliza.
* analytics.company: la empresa asociada a su cuenta de usuario de Analytics.
* analytics.username: su nombre de usuario de Analytics.
* analytics.secret: El secreto asociado al nombre de usuario de Analytics.
* analytics.reportsuite: nombre del grupo de informes de Analytics que se va a utilizar.
* target.clientcode: el código de cliente asociado a la cuenta de Target.
* target.email: la dirección de correo electrónico que utiliza para autenticar la cuenta de Target.
* target.password: la contraseña asociada a su dirección de correo electrónico.

Las propiedades y los valores se separan con signos iguales (=). Las propiedades de Analytics tienen el prefijo `analytics` y las de Target el prefijo `target`. Para configurar un servicio, proporcione valores para todas las propiedades de ese servicio. Si no desea configurar un servicio, no proporcione valores para ese servicio.

El siguiente archivo de ejemplo `.properties` incluye los valores de propiedad para crear una configuración de nube para Analytics:

```xml
analytics.server=https://test.omniture.com/login/
analytics.company=MyCompany
analytics.username=sbroders
analytics.secret=12345678
analytics.reportsuite=myreportsuite
target.clientcode=
target.email=
target.password=
```

El siguiente procedimiento describe cómo optar por la integración mediante el archivo de propiedades.

1. Cree el archivo `marketingcloud.properties` en el directorio de trabajo que está utilizando el proceso de AEM (instancia de autor).

   >[!NOTE]
   >
   >El directorio de trabajo suele ser el directorio que contiene el archivo jar o `license.properties`.
   >
   >Sin embargo, la propiedad del sistema también puede definirla como una ruta absoluta:
   >
   >`mac.provisioning.file.container`

1. Agregue los valores de propiedad según sus cuentas de Analytics o Target.
1. Inicie o reinicie el servidor y, a continuación, inicie sesión con una cuenta de administrador.
1. Abra la tarea Configurar Analytics y Target como se describe en [Configuración de la integración](/help/sites-administering/opt-in.md#configuring-the-integration). En lugar de solicitar la información de su cuenta, el asistente usa los valores del archivo `.properties`.

   Seleccione **Agregar** para el servicio apropiado y, a continuación, continúe con el asistente.

   ![optin-02](assets/optin-02.png)

## Acerca de las configuraciones en la nube {#about-the-cloud-configurations}

Al configurar la integración con Analytics y Target, AEM crea automáticamente las configuraciones y marcos de trabajo de nube necesarios. Por ejemplo, la configuración de nube de Analytics se llama Cuenta de Analytics aprovisionada.

No es necesario modificar las configuraciones en la nube. Sin embargo, puede configurar los marcos según sea necesario. (Vea [Asignar datos de componente con propiedades de Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md) y [Agregar un marco de trabajo de Target](/help/sites-administering/target.md)).

>[!NOTE]
>
>De forma predeterminada, al entrar en el asistente de configuración de Adobe Target, el direccionamiento preciso está habilitado.
>
>El direccionamiento preciso significa que la configuración del servicio en la nube espera a que el contexto se cargue antes de cargar el contenido. Como resultado, en términos de rendimiento, un direccionamiento preciso puede provocar un retraso de unos milisegundos antes de cargar el contenido.
>
>El direccionamiento preciso siempre está habilitado en la instancia de autor. Sin embargo, en la instancia de publicación puede optar por desactivar el direccionamiento preciso globalmente, desactivando la marca de verificación junto al direccionamiento preciso en la configuración del servicio en la nube (**http://localhost:4502/etc/cloudservices.html**). También puede activar y desactivar el direccionamiento preciso para componentes individuales independientemente de la configuración del servicio en la nube.
>
>Si ***ya*** ha creado componentes de destino y cambia esta configuración, los cambios no afectan a esos componentes. Realice cualquier cambio en esos componentes directamente.

>[!CAUTION]
>
>Cuando elige la configuración de Analytics y se selecciona un `reportsuite` específico, el marco de trabajo se restringe al modo de ejecución de publicación. Esto significa que el seguimiento solo funciona en la instancia de publicación.
>
>Si es necesario realizar el seguimiento en una instancia de creación, el valor debe cambiarse a `all`.

## Configuración de la instalación y el aprovisionamiento mediante script {#configuring-the-setup-and-provisioning-via-script}

Como administrador, es posible que desee almacenar en déclencheur la configuración y el aprovisionamiento con una secuencia de comandos en lugar de pasar manualmente por el asistente. Para ello, haga lo siguiente:

* Enviando una petición POST a **/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json** con los parámetros requeridos.

Los parámetros que envíe dependerán de lo siguiente:

* Si desea usar el archivo **marketingcloud.properties** con todas las credenciales necesarias, debe enviar los siguientes parámetros:

   * `automaticProvisioning`= `true`
   * `servicename`= `analytics|target`
   * `path`=ruta de acceso a una página de AEM para adjuntar las configuraciones creadas de Cloud Services

  Por ejemplo, una solicitud de pliegue que cree configuraciones de Analytics y Target y las adjunte a la página de we.retail sería:

  ```shell
  curl -v -u admin:admin -X POST -d"automaticProvisioning=true&servicename=target&servicename=analytics&path=/content/we-retail" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
  ```

* Si no desea usar el archivo **marketingcloud.properties**, debe enviar las credenciales y los parámetros. Por ejemplo:
   * automaticProvisioning= `true`
   * servicename= `analytics|target`
   * path=path to an AEM page to attachment the created cloud services configs; se pueden definir varias rutas
   * analytics.server= `https://servername`
   * analytics.company= `Name of company`
   * analytics.username= `me`
   * analytics.secret= `secret`
   * analytics.reportsuite= `we-retail`
   * target.clientcode= `mycompany`
   * target.email= `me@adobe.com`
   * target.password= `password`

  En este caso, la solicitud de pliegue que crea las configuraciones de Analytics y Target y las adjunta a la página web de venta minorista sería la siguiente:

  ```shell
  curl -v -u admin:admin -X POST -d"automaticProvisioning=false&servicename=target&servicename=analytics&path=/content/we-retail&analytics.server=https://servername/&analytics.company=Name of company&analytics.username=me&analytics.secret=secret&analytics.reportsuite=weretail&target.clientcode=mycompany&target.email=me@adobe.com&target.password=password" http://localhost:4502/libs/cq/cloudservicesprovisioning/content/autoprovisioning.json
  ```
