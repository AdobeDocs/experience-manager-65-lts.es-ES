---
title: Consola web en Adobe Experience Manager
description: Aprenda a utilizar la consola web de Adobe Experience Manager (AEM).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Consola web{#web-console}

La consola web de Adobe Experience Manager (AEM) se basa en [Apache Felix Web Management Console](https://felix.apache.org/documentation/subprojects/apache-felix-web-console.html). Apache Felix es un esfuerzo de la comunidad para implementar la plataforma de servicio OSGi R4, que incluye el marco OSGi y los servicios estándar.

>[!NOTE]
>
>En la consola web, cualquier descripción que mencione la configuración predeterminada está relacionada con los valores predeterminados de Sling.
>
>AEM tiene sus propios valores predeterminados y, por lo tanto, los valores predeterminados establecidos pueden diferir de los documentados en la consola.

La consola web ofrece una selección de pestañas para mantener los paquetes OSGi, que incluyen:

* [Configuración](#configuration): se usa para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar los parámetros del sistema de AEM
* [Paquetes](#bundles): utilizados para instalar paquetes
* [Componentes](#components): utilizados para controlar el estado de los componentes necesarios para AEM

Los cambios realizados se aplican inmediatamente al sistema en ejecución. No es necesario reiniciar.

Se puede tener acceso a la consola desde `../system/console`; por ejemplo:

`http://localhost:4502/system/console/components`

## Configuración {#configuration}

La pestaña **Configuration** se usa para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar los parámetros del sistema de AEM.

>[!NOTE]
>
>Consulte [Configuración de OSGi con la consola web](/help/sites-deploying/configuring-osgi.md) para obtener más información.

Se puede acceder a la ficha **Configuración** mediante:

* El menú desplegable:

  **OSGi >**

* La dirección URL; por ejemplo:

  `http://localhost:4502/system/console/configMgr`

Se muestra una lista de configuraciones:

![screen_shot_2012-02-15at52308pm](assets/screen_shot_2012-02-15at52308pm.png)

Hay dos tipos de configuraciones disponibles en las listas desplegables de esta pantalla:

* **Configuraciones**
Permite actualizar las configuraciones existentes. Tienen una identidad persistente (PID) y pueden ser las siguientes:

   * estándar e integral para AEM; estos son obligatorios; si se eliminan, los valores vuelven a la configuración predeterminada.
   * instancias creadas a partir de Configuraciones de fábrica; estas instancias las crea el usuario, la eliminación elimina la instancia.

* **Configuraciones de fábrica**
Permite crear una instancia del objeto de funcionalidad requerido.

  Se asigna a una identidad persistente y, a continuación, se enumera en la lista desplegable Configuraciones.

Al seleccionar cualquier entrada de la lista, se muestran los parámetros relacionados con esa configuración:

![chlimage_1-21](assets/chlimage_1-21a.png)

A continuación, puede actualizar los parámetros según sea necesario y:

* **Guardar**

  Guarde los cambios realizados.

  Para una configuración de fábrica, se crea una instancia con una identidad persistente. La nueva instancia se muestra en Configuraciones.

* **Restablecer**

  Restablezca los parámetros mostrados en la pantalla a los guardados en último lugar.

* **Eliminar**

  Eliminar la configuración actual. Si son estándar, los parámetros se devuelven a la configuración predeterminada. Si se crea a partir de una configuración de fábrica, se elimina la instancia específica.

* **Desenlazar**

  Desenlace la configuración actual del paquete.

* **Cancelar**

  Cancelar los cambios actuales.

## Paquetes {#bundles}

La pestaña **Paquetes** es el mecanismo para instalar los paquetes OSGi necesarios para AEM. Se puede acceder a la pestaña mediante cualquiera de los siguientes métodos:

* El menú desplegable:

  **OSGi >**

* La dirección URL; por ejemplo:

  `http://localhost:4502/system/console/bundles`

Se muestra una lista de paquetes:

![screen_shot_2012-02-15at44740pm](assets/screen_shot_2012-02-15at44740pm.png)

Con esta pestaña puede:

* **Instalar o actualizar**

  Puede **Examinar** para buscar el archivo que contiene su paquete y especificar si debe **Iniciar** inmediatamente y en qué **Nivel de inicio**.

* **Volver a cargar**

  Actualiza la lista mostrada.

* **Actualizar paquetes**

  Esto comprueba las referencias de todos los paquetes y actualizaciones, según sea necesario.

  Por ejemplo, después de una actualización, es posible que tanto la versión antigua como la nueva se sigan ejecutando debido a referencias anteriores. Esta opción comprueba y mueve todas las referencias a la nueva versión, lo que permite detener la versión antigua.

* **Inicial**

  Inicia un paquete según el nivel de inicio especificado.

* **Detener**

  Detiene el paquete.

* **Desinstalar**

  Desinstala el paquete del sistema.

* **ver el estado**

  La lista especifica el estado del paquete; al hacer clic en el nombre de un paquete específico con se muestra más información.

>[!NOTE]
>
>Después de **actualizar**, Adobe recomienda que realice **Actualizar paquetes**.

## Componentes {#components}

La pestaña **Componentes** le permite Habilitar o Deshabilitar los distintos componentes. Se puede acceder a ella mediante:

* El menú desplegable:

  **Principal >**

* La dirección URL; por ejemplo:

  `http://localhost:4502/system/console/components`

Se muestra una lista de componentes. Hay varios iconos disponibles para permitirle habilitar, deshabilitar o (cuando corresponda) abrir los detalles de configuración de un componente específico.

![screen_shot_2012-02-15at52144pm](assets/screen_shot_2012-02-15at52144pm.png)

Al hacer clic en el nombre de un componente en particular, se muestra más información sobre su estado. Aquí también puede habilitar, deshabilitar o volver a cargar el componente.

![chlimage_1-22](assets/chlimage_1-22a.png)

>[!NOTE]
>
>Activar o desactivar un componente solo se aplica hasta que se reinicia AEM/CRX.
>
>El estado de inicio se define dentro del descriptor del componente, que se genera durante el desarrollo y se almacena en el paquete en el momento de la creación del paquete.
