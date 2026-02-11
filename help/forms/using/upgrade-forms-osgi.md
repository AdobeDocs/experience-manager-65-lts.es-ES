---
title: Actualizar a AEM 6.5 Forms LTS en OSGi
description: Puede realizar una actualización directa de AEM 6.5.22.0 Forms a AEM 6.5 Forms LTS.
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: b7aa877f9e782b0568adc7baa440dc630c690454
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 45%

---

# Actualizar a AEM 6.5 Forms LTS en OSGi {#upgrade-to-aem-forms-osgi}

Para [actualizar de AEM 6.5 a AEM 6.5 LTS](/help/sites-deploying/upgrade.md), actualice a AEM 6.5.22.0 Forms o posterior. Se admite una actualización directa de AEM 6.5.22.0 a AEM 6.5 Forms LTS.

Si utiliza AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms, AEM 6.3 Forms, AEM 6.4 Forms o AEM 6.5 Forms, no estará disponible la actualización directa a AEM 6.5 Forms LTS. Para obtener rutas de actualización detalladas, consulte la documentación de [Rutas de actualización](/help/forms/using/upgrade.md).

Después de actualizar al Service Pack AEM Forms 6.5.22.0, siga estos pasos para actualizar a AEM 6.5 LTS Forms:

1. Instalar el paquete de complementos para AEM Forms. A continuación se detallan los pasos que debe seguir:

   1. Abra [Distribución de software](https://experience.adobe.com/downloads). Necesitará un Adobe ID para iniciar sesión en la distribución de software.
   1. Seleccione **[!UICONTROL Adobe Experience Manager]** disponible en el menú del encabezado.
   1. En la sección **[!UICONTROL Filtros]**:
      1. Seleccione **[!UICONTROL Forms]** en la lista desplegable **[!UICONTROL Solución]**.
      1. Seleccione la versión y el tipo del paquete. También puede usar la opción **[!UICONTROL Buscar descargas]** para filtrar los resultados.
   1. Seleccione el nombre del paquete aplicable a su sistema operativo, seleccione **[!UICONTROL Aceptar términos de EULA]** y seleccione **[!UICONTROL Descargar]**.
   1. Abra el [Administrador de paquetes](/help/sites-administering/package-manager.md) y haga clic en **[!UICONTROL Cargar paquete]** para cargar el paquete.
   1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

      También puede descargar el paquete utilizando el vínculo directo que aparece en el artículo [Versiones de AEM Forms](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).

      Una vez instalado el paquete, se le pedirá que reinicie la instancia de AEM. **No detenga el servidor inmediatamente.** Antes de detener el servidor de AEM Forms, espere hasta que los mensajes ServiceEvent REGISTERED y ServiceEvent UNREGISTERED dejen de aparecer en el archivo &lt;crx-repository>/error.log y el registro esté estable. Tenga en cuenta también que algunos paquetes pueden permanecer en el estado instalado. Puede ignorar de forma segura el estado de estos paquetes.


      **Reinicie la instancia de AEM con los siguientes parámetros adicionales de la línea de comandos de JVM**:
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      Si el servidor se inicia mediante un script o servicio, actualícelo en consecuencia para incluir lo anterior, de modo que esto también sea efectivo después de los siguientes reinicios.

      >[!NOTE]
      >
      > Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

1. Realice actividades posteriores a la instalación.

   * **Ejecutar la utilidad de migración**

     La utilidad de migración hace que los recursos de administración de correspondencia y formularios adaptables de versiones anteriores sean compatibles con los formularios de AEM 6.5. Puede descargar la utilidad desde la distribución de software de AEM. Para obtener información paso a paso sobre cómo configurar y utilizar la utilidad de migración, consulte [utilidad de migración](../../forms/using/migration-utility.md).

     Si utiliza [Ejemplo para integrar el componente borradores y envíos](https://helpx.adobe.com/es/experience-manager/6-3/forms/using/integrate-draft-submission-database.html) con la base de datos y la actualización de una versión anterior, ejecute las siguientes consultas SQL tras realizar la actualización:

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **(Si solo se actualiza desde AEM 6.2 Forms o versiones anteriores) Vuelva a configurar Adobe Sign**

     Si tenía Adobe Sign configurado en la versión anterior de AEM Forms, vuelva a configurar Adobe Sign desde AEM Cloud Services. Para obtener más información, consulte [Integrar Adobe Sign con AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

   * **Compatibilidad con jQuery**

     En AEM 6.5 Forms, la versión de jQuery se actualiza a la 3.2.1 y la versión de la interfaz de usuario de jQuery se actualiza a la 1.12.1. AEM Forms utiliza JQuery en modo **noConflict**. Por lo tanto, si utiliza cualquier otra versión de jQuery, no se muestran problemas al realizar una actualización. Sin embargo, al actualizar a AEM 6.5 Forms:

      * Asegúrese de que los componentes personalizados, si los hay, sean compatibles con las versiones de jQuery admitidas.
      * Elimine las API no compatibles de los componentes personalizados. Consulte la [guía de actualización](https://jquery.com/upgrade-guide/3.0/) para ver la lista de API quitadas. Por ejemplo, se quita la compatibilidad con las API load(), .unload() y .error(). Utilice el método .on() en lugar de las API mencionadas. Por ejemplo, cambie $(&quot;img&quot;).load(fn) a $(&quot;img&quot;).on(&quot;load&quot;, fn).

   * **(Si solo se actualiza desde AEM 6.2 Forms o versiones anteriores) Vuelva a configurar los análisis e informes**

     En AEM 6.4 Forms, la variable de tráfico para el origen y el evento de éxito para la impresión no están disponibles. Por lo tanto, al actualizar desde AEM 6.2 Forms o versiones anteriores, AEM Forms deja de enviar datos al servidor de Adobe Analytics y los informes de análisis para los formularios adaptables no están disponibles. Además, AEM 6.4 Forms introduce una variable de tráfico para la versión del análisis de formularios y el evento de éxito para la cantidad de tiempo invertido en un campo. Por lo tanto, vuelva a configurar los análisis y los informes para su entorno de AEM Forms. Para ver los pasos detallados, consulte [Configurar análisis e informes](../../forms/using/configure-analytics-forms-documents.md).

1. Compruebe que el servidor se haya actualizado correctamente, que todos los datos también se hayan migrado correctamente y que puede funcionar con normalidad.

   * **Compruebe el estado de los paquetes:** Asegúrese de que todos los paquetes estén en estado activo.
   * **Compruebe la replicación y replicación inversa:** Publique, rellene y envíe algunos formularios migrados. Compruebe también los datos enviados.
   * **Compruebe el acceso a las interfaces de usuario de administrador y desarrollador:** Inicie sesión en la instancia de AEM desde una cuenta de administrador y compruebe que tiene acceso a las siguientes direcciones URL:

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >En AEM 6.4 Forms, la estructura del repositorio crx ha cambiado. Si actualiza de Forms 6.3 a AEM 6.5 Forms, utilice las rutas modificadas para la personalización que cree de nuevo. Para obtener la lista completa de las rutas cambiadas, consulte [Reestructurar el repositorio de Forms en AEM](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5).


## Implementación de AEM en JBoss EAP 8 (Windows)

### Información general

Esta guía proporciona instrucciones paso a paso para implementar Adobe Experience Manager (AEM) como archivo OSGi WAR independiente en JBoss Enterprise Application Platform (EAP) 8 en un entorno Windows con JDK 21.

### Requisitos del sistema

Antes de comenzar el proceso de implementación, asegúrese de que su entorno cumpla los siguientes requisitos:

| Componente | Requisito |
|-----------|-------------|
| Sistema operativo | Windows Server 2016 o posterior (64 bits) |
| Java Development Kit | JDK 21 (Oracle o OpenJDK) |
| Servidor de aplicaciones | JBoss EAP 8.x |
| Distribución de AEM | Archivo WAR de AEM (obtenido de Adobe) |

>[!NOTE]
>
> Compruebe que la variable de entorno `JAVA_HOME` apunta al directorio de instalación de JDK 21.

### Paso 1: Instalar JBoss EAP 8

#### Descargar JBoss EAP

1. Vaya al portal para desarrolladores de Red Hat:\
   [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. Descargue la distribución JBoss EAP 8 ZIP para Windows.

#### Extraer JBoss EAP

1. Extraiga el archivo ZIP descargado en el directorio de instalación preferido.

2. Tenga en cuenta esta ruta de acceso de directorio como `<JBOSS_HOME>` para su uso en esta guía.

   **Ejemplo:**\
   ```C:\jboss-eap-8.0```

### Paso 2: Preparar el archivo WAR de AEM

#### Obtener AEM WAR

Adquiera el archivo WAR de AEM desde la Distribución de software de Adobe o su representante de Adobe.

#### Cambiar nombre de archivo WAR

Cambie el nombre del archivo WAR para que refleje la ruta de contexto de URL deseada:

```
cq-quickstart.war
```

>[!IMPORTANT]
>
> El nombre de archivo WAR determina el contexto URL de la aplicación. Por ejemplo, `cq-quickstart.war` será accesible a las `/cq-quickstart`.


### Paso 3: Configuración de AEM WAR

Todas las modificaciones de configuración deben completarse **antes de** implementar en JBoss.

#### Crear directorio de trabajo

1. Cree un directorio de trabajo temporal:

   ```
   C:\aem\war-config
   ```

2. Copie `cq-quickstart.war` en este directorio.

#### Extraer contenido WAR

1. Abra **Símbolo del sistema** y vaya al directorio de trabajo:

   ```cmd
   cd C:\aem\war-config
   ```

2. Extraiga el archivo WAR:

   ```cmd
   jar -xvf cq-quickstart.war
   ```

   Esto crea una estructura de directorio con `WEB-INF` y otros archivos de aplicación.

### Paso 4: Configuración del descriptor de implementación de JBoss

#### Crear archivo de estructura de implementación

1. Vaya al directorio `WEB-INF` dentro del WAR extraído:

   ```cmd
   cd WEB-INF
   ```

2. Cree un nuevo archivo con el nombre `jboss-deployment-structure.xml`.

3. Añada el siguiente contenido XML:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jboss-deployment-structure xmlns="urn:jboss:deployment-structure:1.2">
       <deployment>
           <dependencies>
               <module name="jdk.unsupported" />
           </dependencies>
       </deployment>
   </jboss-deployment-structure>
   ```

4. Guarde y cierre el archivo.

**Propósito:** Esta configuración proporciona acceso a los módulos internos JDK requeridos por AEM.

### Paso 5: Configurar la carga de varias partes

>[!NOTE]
>
> El paso 5 solo es aplicable a **AEM Forms**. Si está configurando **solo AEM**, puede omitir este paso.


#### Modificar web.xml

1. Abra `WEB-INF\web.xml` en un editor de texto.

2. Busque la sección `<servlet>` que contiene la configuración del modo de ejecución:

   ```xml
   <!-- Set the runmode per default to author -->
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

3. Reemplazar la etiqueta `</servlet>` de cierre y la línea anterior por:

   ```xml
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <multipart-config>
       <max-file-size>1048576000</max-file-size>
       <max-request-size>1048576000</max-request-size>
       <file-size-threshold>0</file-size-threshold>
   </multipart-config>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

4. Guarde y cierre `web.xml`.

**Objetivo:** Esta configuración habilita cargas de archivos grandes (hasta 1 GB) para AEM Forms y la administración de recursos digitales.

### Paso 6: Volver a empaquetar el archivo WAR

Después de completar todos los cambios de configuración, vuelva a empaquetar el archivo WAR.

1. Vuelva al directorio de trabajo que contiene el contenido extraído:

   ```cmd
   cd C:\aem\war-config
   ```

2. Cree el nuevo archivo WAR:

   ```cmd
   jar -cvf cq-quickstart.war *
   ```

>[!IMPORTANT]
>
> Realice este paso solo una vez, una vez completadas todas las configuraciones.

### Paso 7: Implementar e iniciar AEM

#### Implementar WAR en JBoss

1. Copie el `cq-quickstart.war` vuelto a empaquetar en el directorio de implementaciones de JBoss:

   ```
   <JBOSS_HOME>\standalone\deployments
   ```

   **Ejemplo:**
   ```C:\jboss-eap-8.0\standalone\deployments```

#### Configuración de JVM (opcional pero recomendada)

Antes de iniciar JBoss, configure las opciones de memoria de JVM:

1. Abra `<JBOSS_HOME>\bin\standalone.conf.bat` en un editor de texto.

1. Modifique o agregue la siguiente línea para establecer la memoria de la pila:

   ```batch
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=512m"
   ```

>[!NOTE]
>
> Ajuste los valores de memoria en función de la capacidad del servidor y los requisitos de AEM.

1. Guarde y cierre el archivo.

#### Iniciar JBoss EAP

1. Abra **Símbolo del sistema** como **Administrador**.

1. Vaya al directorio bin de JBoss:

   ```cmd
   cd <JBOSS_HOME>\bin
   ```

   **Ejemplo:**
   ```cmd cd C:\jboss-eap-8.0\bin```

1. Inicie el servidor JBoss:

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

   **Parámetros:**
   * `-b 0.0.0.0` — enlaza el servidor a todas las interfaces de red
   * `-bmanagement 0.0.0.0` — enlaza la interfaz de administración a todas las interfaces de red

#### Supervisar implementación

Observe la salida de la consola para ver los mensajes de implementación. La implementación correcta se indica mediante:

```
Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
```

### Paso 8: Acceso a AEM

Una vez completada la implementación y iniciada por completo AEM:

**URL de autor de AEM:**
```http://<server-ip>:8080/cq-quickstart```

**Credenciales predeterminadas:**

* Nombre de usuario: `admin`
* Contraseña: `admin`

**Importante:** Cambie la contraseña predeterminada inmediatamente después del primer inicio de sesión.

### Solución de problemas

#### Problemas comunes

| Problema | Solución |
|-------|----------|
| La implementación falla con ClassNotFoundException | Verificar que `jboss-deployment-structure.xml` esté configurado correctamente |
| OutOfMemoryError durante el inicio | Aumentar memoria de montón en `standalone.conf.bat` |
| AEM no se inicia después de la implementación | Comprobar los registros de JBoss en `<JBOSS_HOME>\standalone\log\server.log` |
| No se puede acceder a AEM en el navegador | Verificar la configuración del firewall para permitir el puerto 8080 |

#### Archivos de registro

* **Registro del servidor JBoss:** `<JBOSS_HOME>\standalone\log\server.log`
* **Registro de errores de AEM:** Disponible a través de la consola web de AEM después del inicio en\
  `http://<server-ip>:8080/cq-quickstart/system/console`

### Configuración adicional

#### Configuración de modos de ejecución

Para cambiar los modos de ejecución de AEM (autor/publicación), modifique el parámetro `sling.run.modes` en `WEB-INF\web.xml` antes de volver a empaquetar WAR:

```xml
<init-param>
    <param-name>sling.run.modes</param-name>
    <param-value>publish</param-value>
</init-param>
```

#### Recomendaciones de producción

Para entornos de producción:

* Configuración de certificados SSL/TLS en JBoss
* Configuración de agentes de replicación de AEM
* Configurar Dispatcher para el equilibrio de carga
* Habilitar backups automatizados
* Implementación de monitorización y alertas

### Documentación relacionada

* [Documentación de JBoss EAP 8](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0)
* [Documentación de Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=es)
* [Guía de instalación e implementación de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=es)

### Información del documento

| Campo | Valor |
|-------|-------|
| Última actualización | Febrero de 2026 |
| Versión de AEM | 6.5+ (LTS) |
| Versión de JBoss | EAP 8.x |
| Versión de JDK | 21 |
| Plataforma | Windows |


