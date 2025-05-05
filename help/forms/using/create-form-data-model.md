---
title: 'Tutorial: Crear un modelo de datos de formulario '
description: Obtenga información sobre cómo configurar MySQL como fuente de datos, crear un modelo de datos de formulario (FDM), configurarlo y probar para AEM Forms.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 70%

---

# Tutorial: Crear un modelo de datos de formulario {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Este tutorial es un paso en la serie [Crear su primer formulario adaptable](../../forms/using/create-your-first-adaptive-form.md). Adobe recomienda seguir la serie en secuencia cronológica para comprender, realizar y mostrar el caso de uso completo del tutorial.

## Información sobre el tutorial {#about-the-tutorial}

El módulo de integración de datos de AEM [!DNL Forms] le permite crear un modelo de datos de formulario a partir de fuentes de datos backend dispares, como un perfil de usuario de AEM, servicios web RESTful, servicios web basados en SOAP, servicios OData y bases de datos relacionales. Puede configurar objetos y servicios del modelo de datos en un modelo de datos de formulario y asociarlo a un formulario adaptable. Los campos de formularios adaptables están enlazados a las propiedades del objeto del modelo de datos. Los servicios permiten rellenar previamente el formulario adaptable y escribir los datos de formulario enviados en el objeto del modelo de datos.

Para obtener más información sobre la integración y el modelo de datos de formulario, consulte [Integración de datos de AEM Forms](../../forms/using/data-integration.md).

Este tutorial lo acompañará durante los pasos para preparar, crear, configurar y asociar un modelo de datos de formulario con un formulario adaptable. Al final de este tutorial, podrá:

* [Configurar la base de datos MySQL como fuente de datos](#config-database)
* [Crear un modelo de datos de formulario mediante la base de datos MySQL](#create-fdm)
* [Configurar un modelo de datos de formulario](#config-fdm)
* [Probar un modelo de datos de formulario](#test-fdm)

El modelo de datos de formulario tendrá un aspecto similar al siguiente:

![form-data-model_l](assets/form-data-model_l.png)

**A.** Fuentes de datos configuradas **B.** Esquemas de fuentes de datos **C.** Servicios disponibles **D.** Objetos del modelo de datos **E.** Servicios configurados

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* Base de datos [!DNL MySQL]con datos de ejemplo como se indica en la sección Requisitos previos de [Crear su primer formulario adaptable](../../forms/using/create-your-first-adaptive-form.md)
* Paquete OSGi para el [!DNL MySQL] Controlador JDBC tal como se explica en [Agrupar el controlador de la base de datos JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulario adaptable, tal como se explica en el primer tutorial [Crear un formulario adaptable](/help/forms/using/create-adaptive-form.md)

## Paso 1: Configurar la base de datos MySQL como fuente de datos {#config-database}

Puede configurar distintos tipos de fuentes de datos para crear un modelo de datos de formulario. Para este tutorial, configure la base de datos MySQL que ha configurado y rellenado con datos de ejemplo. Para obtener información sobre otras fuentes de datos compatibles y cómo configurarlas, consulte [Integración de datos de AEM Forms](../../forms/using/data-integration.md).

Haga lo siguiente para configurar su base de datos [!DNL MySQL]:

1. Instale el controlador JDBC para la base de datos [!DNL MySQL]como paquete OSGi:

   1. Descargar el paquete OSGi del controlador JDBC [!DNL MySQL] de `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html`. <!-- This URL is an insecure link but using https is not possible -->
   1. Inicie sesión en la instancia de autor de AEM [!DNL Forms] como administrador y vaya a los paquetes de la consola web de AEM. La dirección URL predeterminada es [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Seleccione **[!UICONTROL Instalar/Actualizar]**. Aparecerá el cuadro de diálogo [!UICONTROL Cargar e instalar paquetes].

   1. Seleccione **[!UICONTROL Elegir archivo]** para examinar y seleccionar el paquete OSGi del controlador JDBC [!DNL MySQL]. Seleccione **[!UICONTROL Iniciar paquete]** y **[!UICONTROL Actualizar paquetes]**, y seleccione **[!UICONTROL Instalar o actualizar]**. Asegúrese de que el [!DNL Oracle Corporation's] Controlador JDBC para [!DNL MySQL] está activo. El controlador está instalado.

1. Configurar la base de datos [!DNL MySQL]como fuente de datos:

   1. Vaya a la consola web de AEM en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Localice la configuración **Apache Sling Connection Pooled DataSource**. Seleccione esta opción para abrir la configuración en modo de edición.
   1. En el cuadro de diálogo de configuración, especifique los siguientes detalles:

      * **Nombre del Datasource:** puede especificar cualquier nombre. Por ejemplo, especifique **WeRetailMySQL**.
      * **Nombre de propiedad del servicio DataSource**: especifique el nombre de la propiedad de servicio que contiene el nombre del DataSource. Se especifica al registrar la instancia de fuente de datos como servicio OSGi. Por ejemplo, **datasource.name**.
      * **Clase** de controlador JDBC: especifique el nombre de la clase Java™ del controlador JDBC. Para la base de datos[!DNL MySQL], especifique **com.mysql.jdbc.Driver**.
      * **URI de conexión JDBC**: especifique la dirección URL de conexión de la base de datos. Para la base de datos [!DNL MySQL] que se ejecuta en el puerto 3306 y en el esquema `weretail`, la dirección URL es: `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > Cuando la base de datos [!DNL MySQL] está detrás de un firewall, el nombre de host de la base de datos no es un DNS público. La dirección IP de la base de datos debe añadirse en el *archivo /etc/hosts* del AEM host máquina.

      * **Nombre de usuario:** nombre de usuario de la base de datos. Debe permitir que el controlador JDBC establezca una conexión con la base de datos.
      * **Contraseña:** contraseña de la base de datos. Debe permitir que el controlador JDBC establezca una conexión con la base de datos.

      >[!NOTE]
      >
      >AEM Forms no admite la autenticación NT para [!DNL MySQL]. Vaya a la consola web de AEM en [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) y busque &quot;Fuente de datos obtenida de una conexión Apache Sling&quot;. Para la propiedad &quot;URI de conexión JDBC&quot;, establezca el valor de &quot;integrationSecurity&quot; como False y use el nombre de usuario y la contraseña creados para conectarse con la base de datos [!DNL MySQL].

      * **Probar en el préstamo:** habilita la opción **[!UICONTROL Probar en el préstamo]**.
      * **Probar en la devolución:** habilita la opción **[!UICONTROL Probar en la devolución]**.
      * **Consulta de validación:** especifica una consulta SQL SELECT para validar conexiones desde el grupo. La consulta debe devolver al menos una fila. Por ejemplo, **seleccione &#42; desde customerdetails**.
      * **Aislamiento de transacciones**: establezca el valor en **READ_COMMITTED**.

        Deje otras propiedades con los valores[&#128279;](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) predeterminados y seleccione **[!UICONTROL Guardar]**.

        Se creará una configuración similar a la siguiente.

        ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Paso 2: Crear un modelo de datos de formulario {#create-fdm}

AEM [!DNL Forms] proporciona una interfaz de usuario intuitiva para [crear un modelo de datos de formulario](data-integration.md) desde fuentes de datos configuradas. Puede utilizar varias fuentes de datos en un modelo de datos de formulario. Para este caso de uso, puede utilizar el origen de datos [!DNL MySQL] configurado.

Para crear el modelo de datos de formulario, haga lo siguiente:

1. En la instancia de autor de AEM, navegue hasta **[!UICONTROL Formularios]** > **[!UICONTROL Integraciones de datos]**.
1. Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Modelo de datos de formulario]**.
1. En el cuadro de diálogo Crear un modelo de datos de formulario, especifique un **nombre** para el modelo de datos de formulario. Por ejemplo, **customer-shipping-billing-details**. Seleccione **[!UICONTROL Siguiente]**.
1. La pantalla Seleccionar fuente de datos enumera todas las fuentes de datos configuradas. Seleccione **WeRetailMySQL** fuente de datos y seleccione **[!UICONTROL Crear]**.

   ![data-source-selection](assets/data-source-selection.png)

Se creará el modelo de datos de formulario **customer-shipping-billing-details**.

## Paso 3: Configurar el modelo de datos de formulario {#config-fdm}

La configuración del modelo de datos de formulario implica:

* agregar objetos y servicios del modelo de datos
* configurar servicios de lectura y escritura para objetos del modelo de datos

Para configurar el modelo de datos de formulario, haga lo siguiente:

1. En la instancia de autor de AEM, navegue hasta **[!UICONTROL Formularios]** > **[!UICONTROL Integraciones de datos]**. La dirección URL predeterminada es [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. El modelo de datos de formulario **customer-shipping-billing-details** que ha creado anteriormente se muestra aquí. Ábralo en el modo de edición.

   La fuente de datos seleccionada **WeRetailMySQL** se configura en el modelo de datos de formulario.

   ![default-fdm](assets/default-fdm.png)

1. Expanda el árbol de fuentes de datos WeRailMySQL. Seleccione los siguientes objetos y servicios del esquema **weretail** > **customerdetails** para poder crear el modelo de datos:

   * **Objetos del modelo de datos**:

      * id
      * name
      * ShippingAddress
      * ciudad
      * estado
      * código postal

   * **Servicios:**

      * conseguir
      * actualizar

   Seleccione **Agregar selección** para agregar los objetos y servicios seleccionados al modelo de datos de formulario.

   ![Esquema de WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Los servicios predeterminados de obtener, actualizar e insertar para fuentes de datos JDBC se proporcionan ya preparados con el modelo de datos de formulario.

1. Configure los servicios de lectura y escritura para el objeto del modelo de datos.

   1. Seleccione el objeto del **modelo de datos customerdetails** y seleccione **[!UICONTROL Editar Propiedades]**.
   1. Seleccione **[!UICONTROL obtener]** de la lista desplegable Servicio de lectura. El argumento **id**, que es la clave principal del objeto del modelo de datos customerdetails, se agrega automáticamente. Seleccione ![aem_6_3_edit](assets/aem_6_3_edit.png) y configure el argumento de la siguiente manera.

      ![read-default](assets/read-default.png)

   1. Del mismo modo, seleccione **[!UICONTROL actualizar]** como servicio de escritura. El objeto **customerdetails** se agrega automáticamente como argumento. El argumento se configura de la siguiente manera.

      ![write-default](assets/write-default.png)

      Agregue y configure el argumento **id** como se indica a continuación.

      ![id-arg](assets/id-arg.png)

   1. Seleccione **[!UICONTROL Listo]** para guardar las propiedades del objeto del modelo de datos. A continuación, seleccione **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

      Los servicios **[!UICONTROL obtener]** y **[!UICONTROL actualizar]** se agregan como servicios predeterminados para el objeto del modelo de datos.

      ![data-model-object](assets/data-model-object.png)

1. Vaya a la pestaña **[!UICONTROL Servicios]** y configure los servicios **[!UICONTROL obtener]** y **[!UICONTROL actualizar]**.

   1. Seleccione el servicio **[!UICONTROL get]** y seleccione **[!UICONTROL Editar propiedades]**. Se abrirá el cuadro de diálogo Propiedades.
   1. Especifique lo siguiente en el cuadro de diálogo Editar propiedades:

      * **Título**: especifique el título del servicio. Por ejemplo: Recuperar dirección de envío.
      * **Descripción**: especifique la descripción que contiene el funcionamiento detallado del servicio. Por ejemplo:

        Este servicio recupera la dirección de envío y otros detalles del cliente de la base de datos [!DNL MySQL]

      * **Objeto de modelo de salida**: seleccione el esquema que contiene los datos del cliente. Por ejemplo:

        customerdetail schema

      * **Devolver matriz**: deshabilite la opción **Devolver matriz**.
      * **Argumentos**: seleccione el argumento llamado **Id.**.

      Seleccione **[!UICONTROL Listo]**.  El servicio para recuperar los detalles del cliente de la base de datos MySQL está configurado.

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Seleccione el servicio **[!UICONTROL update]** y seleccione **[!UICONTROL Editar propiedades]**. Se abrirá el cuadro de diálogo Propiedades.

   1. Especifique lo siguiente en el cuadro de diálogo [!UICONTROL Editar propiedades]:

      * **Título**: especifique el título del servicio. Por ejemplo, Actualizar dirección de envío.
      * **Descripción**: especifique la descripción que contiene el funcionamiento detallado del servicio. Por ejemplo:

        Este servicio actualiza la dirección de envío y los campos relacionados en la base de datos MySQL

      * **Objeto del modelo de entrada**: seleccione el esquema que contiene los datos del cliente. Por ejemplo:

        customerdetail schema

      * **Tipo de salida**: seleccione **BOOLEANO**.

      * **Argumentos**: seleccione el nombre del argumento **ID** y **customerdetails**.

      Seleccione **[!UICONTROL Listo]**.  El servicio **[!UICONTROL actualizar]** para actualizar los detalles del cliente en la base de datos [!DNL MySQL]está configurado.

      ![shiiping-address-update](assets/shiiping-address-update.png)

Se configuran el objeto y los servicios del modelo de datos de formulario. Ahora puede probar el modelo de datos de formulario.

## Paso 4: Probar el modelo de datos de formulario {#test-fdm}

Puede probar el objeto y los servicios del modelo de datos para comprobar que está configurado correctamente.

Haga lo siguiente para ejecutar la prueba:

1. Vaya a la ficha **[!UICONTROL Modelo]**, seleccione el objeto del modelo de datos **customerdetails** y seleccione **[!UICONTROL Objeto del modelo de prueba]**.
1. En la ventana [!UICONTROL Modelo/servicio de prueba], seleccione **[!UICONTROL Objeto del modelo de lectura]** de la lista desplegable **[!UICONTROL Seleccionar modelo/servicio]**.
1. En la **sección customerdetails**, especifique un valor para el argumento id **&#x200B;**&#x200B;que existe en la base de datos configurada [!DNL MySQL] y seleccione **[!UICONTROL Test]**.

   Los detalles del cliente asociados con el ID especificado se recuperan y se muestran en la sección **[!UICONTROL Salida]** como se muestra a continuación.

   ![test-read-model](assets/test-read-model.png)

1. Del mismo modo, puede probar el objeto y los servicios del modelo de escritura.

   En el siguiente ejemplo, el servicio de actualización actualiza correctamente los detalles de dirección del ID 7102715 de la base de datos.

   ![test-write-model](assets/test-write-model.png)

   Ahora, si vuelve a probar el servicio de modelo de lectura para el ID 7107215, recupera y muestra los detalles actualizados del cliente como se muestra a continuación.

   ![read-updated](assets/read-updated.png)


>[!NOTE]
>
> Puede crear y utilizar la configuración de la lista de SharePoint con el modelo de datos de formulario en un formulario adaptable para guardar datos o el documento de registro generado en una lista de SharePoint. Consulte [Conectar un formulario adaptable a la lista de Microsoft® SharePoint](/help/forms/using/configuring-submit-actions.md#create-a-sharepoint-list-configuration) para ver los pasos detallados.