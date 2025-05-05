---
title: Conectarse a Adobe Analytics y crear marcos
description: Obtenga información sobre cómo conectar AEM a SiteCatalyst y crear marcos de trabajo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1484'
ht-degree: 3%

---

# Conectarse a Adobe Analytics y crear marcos {#connecting-to-adobe-analytics-and-creating-frameworks}

Para realizar un seguimiento de los datos web de sus páginas de AEM en Adobe Analytics, cree una configuración de servicios de Adobe Analytics Cloud y un marco de trabajo de Adobe Analytics:

* **Configuración de Adobe Analytics:** La información sobre tu cuenta de Adobe Analytics. La configuración de Adobe Analytics permite que AEM se conecte a Adobe Analytics. Cree una configuración de Adobe Analytics para cada cuenta que utilice.
* **Marco de trabajo de Adobe Analytics:** Un conjunto de asignaciones entre las propiedades del grupo de informes de Adobe Analytics y las variables de CQ. Utilice un marco de trabajo para configurar cómo los datos del sitio web rellenan los informes de Adobe Analytics. Los módulos están asociados a una configuración de Adobe Analytics. Puede crear varios marcos de trabajo para cada configuración.

Cuando asocia una página web con un marco de trabajo, este realiza el seguimiento de esa página y de sus descendientes. Las vistas de página se pueden recuperar desde Adobe Analytics y mostrar en la consola Sitios.

## Requisitos previos {#prerequisites}

### Cuenta de Adobe Analytics {#adobe-analytics-account}

Para realizar un seguimiento de los datos de AEM en Adobe Analytics, debe tener una cuenta de Adobe Experience Cloud Adobe Analytics válida.

La cuenta de Adobe Analytics debe:

* Tiene privilegios de **administrador**
* Asignarse al grupo de usuarios **Acceso al servicio web**.

>[!CAUTION]
>
>Proporcionar privilegios de **administrador** (en Adobe Analytics) no es suficiente para permitir que un usuario se conecte de AEM a Adobe Analytics. La cuenta también debe tener privilegios de **acceso al servicio web**.

![chlimage_1-67](assets/chlimage_1-67.png)

Antes de continuar, asegúrese de que sus credenciales le permiten iniciar sesión en Adobe Analytics. Mediante cualquiera de las siguientes acciones:

* [Iniciar sesión en Adobe Experience Cloud](https://experience.adobe.com/#/@login/home)

* [Iniciar sesión en Adobe Analytics](https://sc.omniture.com/login/)

### Configuración de AEM para utilizar los centros de datos de Adobe Analytics {#configuring-aem-to-use-your-adobe-analytics-data-centers}

Los [centros de datos](https://experienceleague.adobe.com/docs/analytics/analyze/reports-analytics/reporting-interface/overview-data-collection.html) de Adobe Analytics recopilan, procesan y almacenan datos asociados con su grupo de informes de Adobe Analytics. Configure AEM para que utilice el centro de datos que aloja su grupo de informes de Adobe Analytics. El centro de datos se menciona en el contrato. Póngase en contacto con un administrador de su organización para obtener esta información.

Si es necesario, use lo siguiente para ser enrutado al centro de datos correcto: `https://api.omniture.com/`.

Si su organización requiere la recopilación o recuperación de datos de un centro de datos específico, utilice lo siguiente:

| Centro de datos | URL |
|---|---|
| Londres | `https://api3.omniture.com/` |
| Singapur | `https://api4.omniture.com/` |
| Oregón | `https://api5.omniture.com/` |

Use la consola web [para configurar el paquete OSGi](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) **Cliente HTTP de Adobe AEM Analytics**. Agregue la **URL del centro de datos** para el centro de datos que hospeda un grupo de informes para el cual las páginas de AEM recopilan datos.

![aa-07](assets/aa-07.png)

1. Abra la consola web en el explorador web. ([https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr))
1. Para acceder a la consola, introduzca sus credenciales.

   >[!NOTE]
   >
   >Para saber si tiene acceso a esta consola, póngase en contacto con el administrador del sitio.

1. Seleccione el elemento de configuración denominado **Cliente HTTP de Adobe AEM Analytics**.
1. Para agregar la URL de un centro de datos, presione el botón + situado junto a la lista **URL del centro de datos** y escriba la URL en el cuadro.

1. Para quitar una dirección URL de la lista, haga clic en el botón - situado junto a la dirección URL.
1. Haga clic en Guardar.

## Configuración de la conexión con Adobe Analytics {#configuring-the-connection-to-adobe-analytics}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>Ahora se debe usar el complemento [ActivityMap proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es).

## Configuración de para Activity Map {#configuring-for-the-activity-map}

>[!CAUTION]
>
>Debido a los cambios de seguridad de la API de Adobe Analytics, ya no es posible utilizar la versión de Activity Map incluida en AEM.
>
>Ahora se debe usar el complemento [ActivityMap proporcionado por Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=es).

## Creación de un marco de Adobe Analytics {#creating-a-adobe-analytics-framework}

En el caso del ID del grupo de informes (RSID) que esté utilizando, puede controlar qué instancias de servidor (autor, publicación o ambas) aportan datos al grupo de informes:

* **Todos**: la información del autor y de la instancia de publicación rellena el grupo de informes.
* **Autor**: Solo la información de la instancia de autor rellena el grupo de informes.
* **Publicar**: Solo la información de la instancia de publicación rellena el grupo de informes.

>[!NOTE]
>
>La selección del tipo de instancia de servidor no restringe las llamadas a Adobe Analytics, solo controla qué llamadas incluyen el RSID.
>
>Por ejemplo, un marco de trabajo está configurado para usar el grupo de informes *diweretail*, y el autor es la instancia de servidor seleccionada. Cuando las páginas se publican junto con el marco de trabajo, se siguen realizando llamadas a Adobe Analytics, pero estas llamadas no contienen el RSID. Solo las llamadas de la instancia de autor incluyen el RSID.

1. Usando **Navegación**, seleccione **Herramientas**, **Cloud Services** y después **Cloud Services heredados**.
1. Desplácese a **Adobe Analytics** y seleccione **Mostrar configuraciones**.
1. Haga clic en el vínculo **[+]** junto a la configuración de Adobe Analytics.

1. En el cuadro de diálogo **Crear módulo**:

   * Especifique un **Título**.
   * Opcionalmente, puede especificar **Name**, para el nodo que almacena los detalles del marco de trabajo en el repositorio.
   * Seleccione **Adobe Analytics Framework**

   Y haga clic en **Crear**.

   El marco de trabajo se abrirá para editarlo.

1. En la sección **Grupos de informes** del pod lateral (lado derecho del panel principal), haga clic en **Agregar elemento**. A continuación, utilice la lista desplegable para seleccionar el ID del grupo de informes (por ejemplo, `geometrixxauth`) con el que interactúa el marco de trabajo.

   >[!NOTE]
   >
   >El buscador de contenido de la izquierda se rellena con variables de Adobe Analytics (variables de SiteCatalyst) al seleccionar un ID de grupo de informes.

1. Para seleccionar las instancias de servidor que desea enviar información al grupo de informes, utilice la lista desplegable **Modo de ejecución** (junto al ID del grupo de informes).

   ![aa-framework-01](assets/aa-framework-01.png)

1. Para que el marco esté disponible en la instancia de publicación del sitio, en la ficha **Página** de la barra de tareas, haga clic en **Activar marco.**

### Configuración del servidor para Adobe Analytics {#configuring-server-settings-for-adobe-analytics}

El sistema de marcos permite cambiar la configuración del servidor dentro de cada marco de trabajo de Adobe Analytics.

>[!CAUTION]
>
>Esta configuración determina a dónde se envían los datos y cómo, por lo que es imperativo que *no altere esta configuración* y permita que su representante de Adobe Analytics la configure en su lugar.

Comience por abrir el panel. Presione la flecha hacia abajo situada junto a **Servidores**:

![server_001](assets/server_001.png)

* **Servidor de seguimiento**

   * contiene la dirección URL utilizada para enviar llamadas de Adobe Analytics

      * `cname` - toma como valor predeterminado *Nombre de compañía* de la cuenta de Adobe Analytics
      * `d1` - corresponde al centro de datos al que se envía la información (`d1`, `d2` o `d3`)
      * `sc.omtrdc.net` - nombre de dominio

* **Servidor de seguimiento seguro**

   * Tiene los mismos segmentos que el servidor de seguimiento
   * Se usa para enviar datos desde páginas seguras (`https://`)

* **Espacio de nombres del visitante**

   * El área de nombres determina la primera parte de la dirección URL de seguimiento.
   * Por ejemplo, si se cambia el espacio de nombres a **CNAME**, las llamadas realizadas a Adobe Analytics se parecerán a **CNAME.d1.omtrdc.net** en lugar del predeterminado.

## Asociación de una página a un marco de trabajo de Adobe Analytics {#associating-a-page-with-a-adobe-analytics-framework}

Cuando una página está asociada a un marco de trabajo de Adobe Analytics, la página envía datos a Adobe Analytics cuando se carga la página. Las variables que rellena la página se asignan y recuperan de las variables de Adobe Analytics en el marco de trabajo. Por ejemplo, las vistas de página se recuperan de Adobe Analytics.

Los descendientes de la página heredan la asociación con el marco. Por ejemplo, cuando asocia la página raíz del sitio con un marco de trabajo, todas las páginas del sitio se asocian al marco de trabajo.

1. En la consola **Sites**, seleccione la página que desee configurar con seguimiento.
1. Abra **[Propiedades de página](/help/sites-authoring/editing-page-properties.md)**, ya sea directamente desde la consola o desde el editor de páginas.
1. Abra la pestaña **&#x200B; Cloud Services**.

1. Utilice la lista desplegable **Agregar configuración** para seleccionar **Adobe Analytics** de las opciones disponibles. Si se hereda, desactívelo antes de que el selector esté disponible.

1. El selector desplegable de **Adobe Analytics** se anexa a las opciones disponibles. Seleccione la configuración del marco de trabajo necesaria.

1. Seleccione **Guardar y cerrar**.
1. Para activar la página y cualquier configuración o archivo conectado, **[publique](/help/sites-authoring/publishing-pages.md)** la página.
1. El paso final es visitar la página en la instancia de publicación y buscar una palabra clave (por ejemplo, berenjena) usando el componente **Search**.
1. A continuación, puede comprobar las llamadas realizadas a Adobe Analytics con una herramienta adecuada; por ejemplo, [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html).
1. Utilizando el ejemplo proporcionado, la llamada debe contener el valor introducido (es decir, berenjena) en eVar7 y la lista de eventos debe contener event3.

### Vistas de la página {#page-views}

Cuando una página está asociada a un marco de trabajo de Adobe Analytics, el número de vistas de página se puede mostrar en la vista de lista de la consola Sitios.

Consulte [Ver datos de análisis de página](/help/sites-authoring/page-analytics-using.md) para obtener más información.

### Configuración del intervalo de importación {#configuring-the-import-interval}

Configure la instancia apropiada del servicio **Importador de Sling de informes de AEM Analytics de Adobe**:

* **Intentos de recuperación**:
Número de intentos de recuperar un informe en cola.
El valor predeterminado es `6`.

* **Demora de recuperación**:
El número de milisegundos entre intentos de recuperar un informe en cola.
El valor predeterminado es `10000`. Como este valor se expresa en milisegundos, corresponde a 10 segundos.

* **Frecuencia de captura**:
Una expresión `cron` para determinar la frecuencia con la que se recupera el informe de Analytics.
El valor predeterminado es `0 0 0/12 * * ?`, que corresponde a 12 recuperaciones cada hora.

Para configurar este servicio OSGi, puede usar la [consola web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) o un nodo [osgiConfig en el repositorio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) (el PID del servicio es `com.day.cq.analytics.sitecatalyst.impl.importer.ReportImporterScheduler`).

## Edición de configuraciones y/o marcos de Adobe Analytics {#editing-adobe-analytics-configurations-and-or-frameworks}

Al igual que cuando crea una configuración o un marco de trabajo de Adobe Analytics, vaya a la pantalla (heredada) **Cloud Services**. Seleccione **Mostrar configuraciones** y luego haga clic en el vínculo a la configuración específica que desee actualizar.

Al editar una configuración de Adobe Analytics, presione **Editar** en la página de configuración para abrir el cuadro de diálogo **Editar componente**.

## Eliminación de marcos de Adobe Analytics {#deleting-adobe-analytics-frameworks}

Para eliminar un módulo de Adobe Analytics, primero [ábralo para editarlo](#editing-adobe-analytics-configurations-and-or-frameworks).

A continuación, seleccione **Eliminar marco** en la ficha **Página** de la barra de tareas.
