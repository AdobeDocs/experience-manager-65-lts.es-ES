---
title: Instrucciones de instalación de parches de AEM Forms para AEM Forms
description: Instrucciones de instalación del Service Pack de AEM Forms para el entorno OSGi y JEE
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
hide: true
hidefromtoc: true
source-git-commit: 8097d48b797759cc99e0b299a5dbca2d9f8194af
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 97%

---

# Instrucciones de instalación del paquete de servicio de AEM 6.5 Forms {#aem-form-patch-installation-instructions}

## Información de la versión

| Producto | Adobe Experience Manager 6.5 Forms |
|---|---|
| Versión | 6.5.22.0 |
| Tipo | Versión del Service Pack |
| Fecha | 29 de noviembre de 2024 |
| Descargar URL | [Últimas versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) |

>[!NOTE]
>
>Consulte las [Notas de la versión de AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es) más recientes para obtener una lista completa de los problemas corregidos.

## ¿Qué incluye Experience Manager Forms 6.5?

<span class="preview"> Si está actualizando a AEM Forms Service Pack 6.5 LTS, consulte [Actualizar a AEM Forms 6.5 LTS en OSGi](/help/forms/using/upgrade-forms-osgi.md). </span>

Adobe Experience Manager (AEM) Forms Service Pack incluye funciones nuevas y actualizadas, como mejoras clave solicitadas por el cliente, de rendimiento, estabilidad y seguridad. AEM Forms lanza Service Packs a intervalos regulares para ofrecer las últimas funciones y mejoras. Según la pila de tecnología, elija una de las siguientes rutas para descargar e instalar el Service Pack en su entorno:

* [Descargue e instale el Service Pack en un formulario de AEM en un entorno JEE](#download-and-install-for-jee-service-pack)
* [Descargue e instale el Service Pack en un formulario de AEM en un entorno OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe lanza un programa de instalación completo cada seis Service Packs. AEM 6.5 Forms Service Pack 18 (6.5.18.0) es el último programa de instalación completo de JEE. El programa de instalación completo admite nuevas plataformas, mientras que el programa de instalación normal del Service Pack incluye nuevas funciones, corrección de errores y mejoras generales. Si realiza una instalación nueva o planea utilizar el software más reciente para AEM Forms 6.5 en el entorno JEE, Adobe recomienda usar AEM 6.5.18.0 Forms en el programa de instalación completo de JEE lanzado el 31 de agosto de 2023, en lugar del de AEM Forms 6.5 lanzado el 8 de abril de 2019 o el de AEM 6.5.12.0 Forms lanzado el 3 de marzo de 2022.  Después de usar el programa de instalación completo, instale el Service Pack más reciente.
> * Las funcionalidades de AEM Forms, como los formularios adaptables, disponibles en [Inicio rápido de AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=es), se destinan solo a la exploración y la evaluación. Para su uso en producción, es esencial obtener una licencia válida para AEM Forms.

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## Descargue e instale el Service Pack en un formulario de AEM en un entorno de JEE {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++&#x200B;1. Realice una copia de seguridad del entorno existente

1. Haga una copia de seguridad de su [repositorio de CRX, esquema de base de datos y GDS (almacenamiento global de documentos)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=es).
1. Haga una copia de seguridad de &lt;*AEM_forms_root*>/carpeta de implementación.

>[!NOTE]
>
> Antes de ejecutar el programa de instalación del Service Pack de AEM, asegúrese de que tiene privilegios de acceso de escritura en el directorio de instalación de AEM.

+++

+++&#x200B;2. Descargue el software requerido

* [Service Pack de AEM Forms en JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)

* [Servlet de fragmento](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es)
  <!--* [Forms add-on package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html)-->


+++

+++&#x200B;3. Instale los paquetes redistribuibles de Microsoft Visual C++

* Descargue e instale la [versión de 64 bits de los paquetes redistribuibles de Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 y 2022](https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) en el equipo donde esté instalado AEM 6.5 Forms.

>[!NOTE]
>
> Asegúrese de instalar la versión redistribuible, incluso si está instalada una versión anterior, para garantizar la disponibilidad de la versión más reciente.

+++

+++&#x200B;4. Instale el Service Pack de AEM Forms en JEE:

1. Detenga el servidor de aplicaciones.
1. Extraiga el **archivo del programa de instalación del Service Pack de AEM Forms en JEE** en el disco duro:

   * **Windows**
Vaya al directorio correspondiente del medio de instalación o a la carpeta del disco duro donde copió el programa de instalación, y haga doble clic en el archivo `aemforms65_cfp_install.exe`.

      * (Windows de 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows de 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Vaya al directorio apropiado y, desde un shell, escriba `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Esto inicia un asistente de instalación que le guiará a través de la instalación.

1. En el panel Introducción, haga clic en **[!UICONTROL Siguiente]**.
1. En la pantalla **Elegir carpeta de instalación**, verifique que la ubicación predeterminada que se muestra es correcta para la instalación existente, o haga clic en **[!UICONTROL Examinar]** para seleccionar la carpeta alternativa en la que los formularios de AEM estén instalados y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información de resumen del Service Pack y haga clic en **[!UICONTROL Siguiente]**.
1. Lea la información del resumen previo a la instalación y haga clic en **[!UICONTROL Instalar]**.
1. Una vez finalizada la instalación, haga clic en **[!UICONTROL Siguiente]** para aplicar las actualizaciones de correcciones rápidas a los archivos instalados.
1. **[Solo para Windows]:** Complete uno de estos pasos:

   * Anule la selección de la opción **Iniciar el administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Ejecute el **administrador de configuración** mediante el archivo **ConfigurationManager.bat** en `[aem-forms root]\configurationManager\bin`.

   * O anule la selección de la opción **Iniciar el administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Antes de ejecutar el **administrador de configuración** con **ConfigurationManager.exe** o **ConfigurationManager_IPv6.exe**, vaya al directorio *`<AEMForms_Install_Dir>\configurationManager\bin`* y reemplace **ConfigurationManager.lax** y **ConfigurationManager_IPV6.lax** por los archivos [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) y [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax) más recientes, y busque y reemplace **axis-1.4.1.1.jar** por **axis-1.4.1.2.jar** en estos dos archivos.

     >[!NOTE]
     >
     >* Actualizar o reemplazar el archivo **ConfigurationManager.bat** le ayuda a evitar actualizar los archivos .lax manualmente.

1. **[Solo para usuarios basados en Unix]:** la casilla de verificación **Iniciar el administrador de configuración** está activada de forma predeterminada. Haga clic en **[!UICONTROL Listo]** para ejecutar el administrador de configuración al instante o para ejecutar el **administrador de configuración** más tarde, y anule la selección de la opción **Iniciar el administrador de configuración** antes de hacer clic en **[!UICONTROL Listo]**. Puede iniciar el **administrador de configuración** más adelante utilizando el script adecuado en el directorio `[AEM_forms_root]/configurationManager/bin`.

1. Según el servidor de aplicaciones, elija uno de los siguientes documentos y siga las instrucciones de la sección *Configuración e implementación de AEM Forms*.

   * [Instalación e implementación de AEM Forms para JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_es)
   * [Instalación e implementación de AEM Forms para WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_es)
   * [Instalación e implementación de AEM Forms para WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_es)
   * [Instalación e implementación de AEM Forms para el clúster de JBoss®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Instalación e implementación de AEM Forms para el clúster de WebSphere®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Instalación e implementación de AEM Forms para WebLogic Cluster](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* Después de instalar AEM Forms en el Service Pack de JEE, debe quitar el paquete de complementos de Forms de la carpeta `crx-repository\install` antes de reiniciar el servidor de aplicaciones. Descargue el paquete de complementos de Forms más reciente del [Portal de distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
>* Se recomienda utilizar el comando &quot;Ctrl + C&quot; para reiniciar el SDK. El reinicio del SDK de AEM mediante métodos alternativos, como detener los procesos de Java, puede generar incoherencias en el entorno de desarrollo de AEM.

+++

+++&#x200B;5. Instalar el fragmento de servlet si no está instalado (**Paso obligatorio**)

<!-- >[!NOTE] > > * If you are upgrading from **AEM Service Pack 6.5.15.0**, the installation of the **servlet fragment** is not required. For versions **AEM Service Pack 6.5.14.0** or earlier, it is **mandatory to install** the servlet fragment. -->

Para descargar e instalar el fragmento de servlet:

1. Si no ha descargado el fragmento, descárguelo de [Distribución de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

2. Inicie el servidor de aplicaciones, espere a que los registros se estabilicen y compruebe el estado del paquete.

3. Abra los paquetes de la consola web. La URL predeterminada es `http://[Server]:[Port]/system/console/bundles`.

4. Pulse Instalar/actualizar. Elija el fragmento descargado, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Haga clic en **Instalar** o **Actualizar**. Espere a que el servidor de aplicaciones se estabilice

5. Detenga el servidor de aplicaciones.

+++

+++&#x200B;6. Instale el Service Pack de AEM

1. Reinicie la instancia antes de la instalación si está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.
1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].
1. Descargue el Service Pack de [Distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra el administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar automáticamente el Service Pack de [!DNL ExperienceManager].<!--       UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea.
El paquete se instala de forma automática.

* Use la API [HTTP del Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es). Use `cmd=install&recursive=true` para que se instalen los paquetes anidados.

  >[!NOTE]
  >
  >El Service Pack de Experience Manager no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validación de la instalación**

  Para conocer las plataformas que están certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (spversion)` en [!UICONTROL Productos instalados].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Todos los paquetes OSGi tienen el valor **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).
   1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.14 o posterior (utilice WebConsole: `/system/console/bundles`).

+++

+++&#x200B;7. Instale el paquete de complementos de AEM Experience Manager Forms

1. Asegúrese de que ha instalado el Service Pack de [!DNL Experience Manager].
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para su sistema operativo.
1. Instale el paquete de complementos para Forms tal como se describe en la [instalación de paquetes de complementos para AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Si usa cartas en Experience Manager 6.5 Forms, instale el [último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

## Descargar e instalar el Service Pack en un formulario de AEM en un entorno OSGi {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++&#x200B;1. Realice una copia de seguridad del entorno existente

1. Haga una copia de seguridad de su [Repositorio de CRX y Esquema de base de datos](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=es).

>[!NOTE]
>
> Si instala el Service Pack de AEM Forms para la base de datos relacional, es obligatorio realizar una copia de seguridad de DB_schema.

+++

+++&#x200B;2. Descargue el software requerido

* [Service Pack de AEM](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=es)
* [Paquete de complemento de Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es)

+++

+++ &#x200B;3. Instale los paquetes redistribuibles de Microsoft Visual C++

* Descargue e instale la [versión de 64 bits de los paquetes redistribuibles de Microsoft Visual C++ para Visual Studio 2015, 2017, 2019 y 2022](https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) en el equipo donde esté instalado AEM 6.5 Forms.

>[!NOTE]
>
>
> Asegúrese de instalar la versión redistribuible, incluso si está instalada una versión anterior, para garantizar la disponibilidad de la versión más reciente.

+++

+++&#x200B;4. Instale el AEM Service Pack

1. Reinicie la instancia antes de la instalación si está en modo de actualización (cuando la instancia se haya actualizado desde una versión anterior). Adobe recomienda reiniciar si el tiempo de actividad actual de una instancia es alto.
1. Antes de realizar la instalación, realice una instantánea o una copia de seguridad nueva de la instancia de [!DNL Experience Manager].
1. Descargue el Service Pack de [Distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Abra el administrador de paquetes y seleccione **[!UICONTROL Cargar paquete]** para cargar el paquete. Para obtener más información, consulte [Administrador de paquetes](/help/sites-administering/package-manager.md).
1. Seleccione el paquete y haga clic en **[!UICONTROL Instalar]**.

**Instalación automática**

Existen dos métodos diferentes que puede utilizar para instalar de forma automática [!DNL Experience Manager] Service Pack.<!--  UPDATE FOR EACH NEW RELEASE -->

* Coloque el paquete en la carpeta `../crx-quickstart/install` cuando el servidor esté disponible en línea. El paquete se instala de forma automática.
* Use la [API HTTP del administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=es). Utilice `cmd=install&recursive=true` para que se instalen los paquetes anidados.

  >[!NOTE]
  >
  >Experience Manager Service Pack no admite la instalación de Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validación de la instalación**

  Para conocer las plataformas que están certificadas para funcionar con esta versión, consulte los [requisitos técnicos](/help/sites-deploying/technical-requirements.md).

   1. La página de información del producto (`/system/console/productinfo`) muestra la cadena de versión actualizada `Adobe Experience Manager (spversion)` en [!UICONTROL Productos instalados]. <!-- UPDATE FOR EACH NEW RELEASE -->

   1. Todos los paquetes OSGi tienen el valor **[!UICONTROL ACTIVO]** o **[!UICONTROL FRAGMENTO]** en la consola OSGi (utilice la consola web: `/system/console/bundles`).

      1. El paquete OSGi `org.apache.jackrabbit.oak-core` es de la versión 1.22.14 o posteriores (utilice la consola web: `/system/console/bundles`).

+++

+++&#x200B;5. Instale el paquete de complementos de Adobe Experience Manager Forms (AEM)

1. Asegúrese de que ha instalado [!DNL Experience Manager] Service Pack.
1. Descargue el paquete de complementos de Forms correspondiente que aparece en las [versiones de AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) para su sistema operativo.
1. Instale el paquete de complementos para Forms tal como se describe en la [instalación de paquetes de complementos para AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Si usa cartas en Experience Manager 6.5 Forms, instale el [último paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).

+++

## Resolución de problemas

* Si el **cuadro de diálogo en la IU del administrador de paquetes** se cierra durante la instalación del Service Pack, espere a que los registros de errores se estabilicen antes de acceder a la implementación. Espere los registros específicos relacionados con la desinstalación del paquete actualizador para asegurarse de que las instalaciones son correctas. Por lo general, este problema se produce en el explorador Safari, pero puede producirse de forma intermitente en cualquier explorador.

* Compruebe los registros del monitor (error.log) una vez que se haya completado la instalación de cualquier actividad. Espere unos minutos hasta que no haya actividad en los registros. Reinicie la instancia de AEM.

* En caso de que reciba un **error de servicio no disponible** después de instalar el Service Pack de AEM Forms 6.5.15.0 o posteriores, [instale el fragmento de servlet y el paquete](/help/forms/using/aem-service-pack-installation-solution.md) para corregir el error.
