---
title: Integración con Silverpop Engage
description: Aprenda a integrar Adobe Experience Manager con Silverpop Engage.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Integración con Silverpop Engage{#integrating-with-silverpop-engage}

<!-- THIS ENTIRE TOPIC APPEARS OBSOLETE BECAUSE SILVERPOP NO LONGER EXISTS AND THERE ARE NO REDIRECTS FOR THE DOWNLOAD URL BELOW THAT IS 404.
>[!NOTE]
>
>Silverpop integration is **not** available out of the box. Download the Silverpop integration package `https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/aem620/product/cq-mcm-integrations-silverpop-content` from Package Share and install it on your instance. After you have installed the package, you can configure it as described in this document. -->

La integración de AEM con Silverpop Engage le permite administrar y enviar correos electrónicos creados en AEM mediante Silverpop. También le permite utilizar las funciones de administración de posibles clientes de Silverpop a través de formularios AEM en páginas de AEM.

La integración ofrece las siguientes funciones:

* La capacidad de crear correos electrónicos en AEM y publicarlos en Silverpop para su distribución.
* La capacidad de establecer la acción de un formulario de AEM para crear un suscriptor de Silverpop.

Una vez configurado Silverpop Engage, puede publicar boletines informativos o correos electrónicos en Silverpop Engage.

## Creación de una configuración de Silverpop {#creating-a-silverpop-configuration}

Las configuraciones de Silverpop se pueden agregar mediante **Cloud Services**, **Herramientas** o **puntos finales de API**. Todos los métodos se describen en esta sección.

### Configuración de Silverpop mediante Cloud Services {#configuring-silverpop-via-cloudservices}

Para crear una configuración de Silverpop en Cloud Services:

1. En AEM, haga clic en **Herramientas** > **Implementación** > **Cloud Services**. (O acceda directamente a en `https://<hostname>:<port>/etc/cloudservices.html`.)
1. En servicios de terceros, haga clic en **Silverop Engage** y luego en **Configurar**. Se abre la ventana de configuración de Silverpop.

   >[!NOTE]
   >
   >Silverpop Engage no está disponible como opción en los servicios de terceros a menos que descargue el paquete desde Package Share.

1. Escriba un título y, opcionalmente, un nombre y haga clic en **Crear**. Se abre la ventana de configuración de ** Configuración ** Silverpop.
1. Introduzca el nombre de usuario y la contraseña, y seleccione un punto final de API en la lista desplegable.
1. Haga clic en **Conectar con Silverpop.** Cuando se haya conectado correctamente, verá un cuadro de diálogo correcto. Haz clic en **Aceptar** para salir de la ventana. Para ir a Silverpop, haga clic en **Ir a Silverpop Engage**.
1. Silverpop se ha configurado. Puede editar la configuración haciendo clic en **Editar**.
1. Además, el marco de Silverpop Engage se puede configurar para acciones personalizadas proporcionando título y nombre (opcional). Al hacer clic en Crear, se crea correctamente el marco de trabajo para la conexión de Silverpop ya configurada.

   Las columnas de extensión de datos importadas se pueden usar posteriormente mediante el componente AEM: **Texto y Personalization**.

### Configuración de Silverpop mediante Herramientas {#configuring-silverpop-via-tools}

Para crear una configuración de Silverpop en Herramientas:

1. En AEM, haga clic en **Herramientas** > **Implementación** > **Cloud Services**. O bien, vaya directamente a `https://<hostname>:<port>/misadmin#/etc`.
1. Seleccione **Herramientas**, luego **Configuraciones de Cloud Services** y después **Silverpop Engage**.
1. Haga clic en **Nuevo**.

   ![chlimage_1-6](assets/chlimage_1-6.jpeg)

1. En la ventana **Crear página**, escriba el **Título** y, opcionalmente, el **Nombre**, y haga clic en **Crear**.
1. Introduzca la información de configuración como se describe en el paso 4 del procedimiento anterior. Siga ese procedimiento para poder finalizar la configuración de Silverpop.

### Añadir varias configuraciones {#adding-multiple-configurations}

Para agregar varias configuraciones:

1. En la página de bienvenida, haga clic en **Cloud Services** y luego en **Silverpop Engage**. Haga clic en el botón **Mostrar configuraciones** que aparece si hay una o más configuraciones de Silverpop disponibles. Se muestran todas las configuraciones disponibles.
1. Haga clic en el signo **+** junto a Configuraciones disponibles. Abre la ventana **Crear configuraciones**. Siga el procedimiento de configuración anterior para poder crear una configuración.

### Configuración de puntos finales de API para conectarse a Silverpop {#configuring-api-end-points-for-connecting-to-silverpop}

Actualmente, AEM tiene seis puntos finales no seguros (Participación 1 a 6). Silverpop ahora proporciona dos nuevos puntos finales y puntos finales de conexión modificados para los existentes.

Para configurar los puntos finales de la API:

1. Ir a `/libs/mcm/silverpop/components/silverpoppage/dialog/items/general/items/apiendpoint/options node` el `https://<hostname>:<port>/crxde.`
1. Haga clic con el botón derecho y seleccione **Crear**, luego **Crear nodo**.
1. Escriba **Name** como `sp-e0` y elija **Type** como `cq:Widget`.
1. Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Engage 0`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://api0.silverpop.com`

   ![chlimage_1-42](assets/chlimage_1-42.png)

   Haga clic en &quot;Guardar todo&quot;.

1. Cree uno o más nodos con **Name** como `sp-e7` y **Type** como `cq:Widget`.

   Agregue dos propiedades al nodo recién agregado:

   1. **Nombre**: `text`, **Tipo**: `String`, **Valor**: `Pilot`
   1. **Nombre**: `value`, **Tipo**: `String`, **Valor**: `https://apipilot.silverpop.com/XMLAPI`

1. Para cambiar los puntos finales de la API existentes (participación 1 a 6), haga clic en cada uno de ellos uno por uno y reemplace los valores de la siguiente manera:

   | **Nombre de nodo** | **Valor de punto final existente** | **Nuevo valor de punto final** |
   |---|---|---|
   | sp-e1 | `https://api.engage1.silverpop.com/XMLAPI` | `https://api1.silverpop.com` |
   | sp-e2 | `https://api.engage2.silverpop.com/XMLAPI` | `https://api2.silverpop.com` |
   | sp-e3 | `https://api.engage3.silverpop.com/XMLAPI` | `https://api3.silverpop.com` |
   | sp-e4 | `https://api.engage4.silverpop.com/XMLAPI` | `https://api4.silverpop.com` |
   | sp-e5 | `https://api.engage5.silverpop.com/XMLAPI` | `https://api5.silverpop.com` |
   | sp-e6 | `https://api.pilot.silverpop.com/XMLAPI` | `https://api6.silverpop.com` |

1. Haga clic en **Guardar todo**. AEM ya está listo para conectarse a Silverpop a través de puntos finales seguros.

   ![chlimage_1-7](assets/chlimage_1-7.jpeg)
