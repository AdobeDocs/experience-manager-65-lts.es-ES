---
title: Importar y administrar aplicaciones
description: Obtenga información sobre cómo importar y administrar aplicaciones. Una aplicación es un contenedor para almacenar los recursos necesarios para implementar una solución de formularios AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e0984513-f70c-4409-885b-a2eb50757a7d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Importar y administrar aplicaciones{#import-and-manage-applications}

En los formularios AEM Forms, una *aplicación* es un contenedor para almacenar los recursos necesarios para implementar una solución de formularios AEM Forms. Algunos ejemplos de recursos son diseños de formulario, fragmentos de formulario, imágenes, procesos, archivos DDX, guías de formulario, páginas HTML y archivos SWF. Durante la fase de desarrollo de un proyecto, los usuarios de Workbench pueden desplegar aplicaciones directamente desde la vista Aplicaciones en Workbench. Una vez desplegadas, estas aplicaciones aparecen en la consola de administración, en la ficha Aplicaciones de la página Administración de aplicaciones.

Cuando una aplicación está completa y lista para su implementación en un servidor de producción, el usuario de Workbench empaqueta la aplicación en un *archivo de aplicación de formularios de AEM* (.lca). A continuación, un administrador utiliza la consola de administración para importar e implementar el archivo de aplicación mediante el separador Aplicaciones de la página Administración de aplicaciones.

También puede utilizar la pestaña Archivos de la página Administración de aplicaciones para importar los LCA creados con Workbench 8.x.

>[!NOTE]
>
>Existe un problema conocido que indica que los archivos LCA de una versión futura no son necesariamente compatibles con versiones anteriores. Aunque es posible ver e importar archivos LCA de una versión futura de formularios AEM (por ejemplo, una versión de vista previa), no se admite y puede provocar un comportamiento aberrante.

Utilice la pestaña Aplicaciones para importar y gestionar aplicaciones creadas en Workbench. Los administradores de aplicaciones también pueden exportar la configuración en tiempo de ejecución de una aplicación. Exportar la configuración en tiempo de ejecución elimina la necesidad de volver a configurar manualmente las opciones en el entorno de producción antes de iniciar las aplicaciones implementadas. El archivo de configuración de tiempo de ejecución contiene:

* ajustes de configuración del servicio
* opciones de configuración del grupo
* opciones de configuración de extremo
* perfiles de seguridad

## Importar una aplicación o un archivo {#import-an-application-or-archive}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Haga clic en Importar.
1. Haga clic en Examinar, seleccione el archivo .lca que desea importar y haga clic en Vista previa. La página Vista previa de la aplicación muestra información sobre la aplicación.
1. (Opcional) Para ver una lista de los recursos contenidos en la aplicación, haga clic en Ver Assets.
1. (Opcional) Para implementar los recursos en tiempo de ejecución, seleccione Implementar Assets en tiempo de ejecución cuando se complete la importación. Si no selecciona esta opción, puede implementar los recursos más adelante.
1. Haga clic en Importar. La aplicación aparece en la ficha Aplicaciones.
1. Inicie sesión en el repositorio de CRX con credenciales de administrador.
1. Vaya a content/dam/lcapplications

   >[!NOTE]
   >
   >Las aplicaciones importadas se muestran en el nodo de aplicaciones.

1. Haga clic en una de las aplicaciones importadas.

   La pestaña Propiedades de la derecha muestra las propiedades del nodo CRX seleccionado.

   La propiedad **syncState** indica el estado de sincronización de datos entre el servidor de AEM Forms y el repositorio de CRX. Tan pronto como comience el proceso de importación, este estado se establece en 0 (cero). Este estado indica que los datos no están sincronizados actualmente. Cuando se sincronizan los datos, el estado se establece en 1.

## Implementación de una aplicación {#deploy-an-application}

Puede desplegar aplicaciones que haya importado o que los usuarios de Workbench hayan importado de Workbench.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Seleccione la casilla de verificación situada junto a la aplicación que desea desplegar y haga clic en Desplegar.
1. Haga clic en Aceptar en el cuadro de diálogo de confirmación que aparece.

## Anular la implementación de una aplicación {#undeploy-an-application}

Puede anular la implementación de aplicaciones desde el tiempo de ejecución.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Seleccione la casilla de verificación situada junto a la aplicación que desea anular la implementación y haga clic en Anular implementación.
1. Haga clic en Aceptar en el cuadro de diálogo de confirmación que aparece.

## Quitar una aplicación del servidor {#remove-an-application-from-the-server}

Anule la implementación de la aplicación antes de quitarla del servidor.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Seleccione la casilla de verificación situada junto a la aplicación que desee quitar y haga clic en Quitar.
1. Haga clic en Aceptar en el cuadro de diálogo de confirmación que aparece.

## Importar la configuración en tiempo de ejecución de una aplicación {#import-an-application-s-runtime-configuration}

Si un administrador de aplicaciones exportó la configuración de tiempo de ejecución de una aplicación, puede importarla en la aplicación implementada. Puede importarlo mediante la consola de administración o mediante una implementación LCA mediante scripts.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Haga clic en el nombre de la aplicación.
1. Haga clic en Importar configuración de tiempo de ejecución.
1. Haga clic en Examinar y seleccione el archivo XML que contiene la configuración de tiempo de ejecución.
1. Haga clic en Importar.

## Exportar la configuración en tiempo de ejecución de una aplicación {#export-an-application-s-runtime-configuration}

Puede exportar la información de configuración en tiempo de ejecución para las aplicaciones implementadas.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de aplicaciones.
1. Haga clic en el nombre de la aplicación.
1. Haga clic en Exportar configuración de tiempo de ejecución y guarde el archivo de configuración (XML) producido.

## Implementación mediante scripts de aplicaciones de formularios AEM Forms {#scripted-deployment-of-aem-forms-applications}

También puede utilizar una herramienta de implementación con scripts para implementar archivos de aplicación, incluido un archivo settings.xml que especifica la siguiente configuración:

* ajustes de configuración del servicio
* opciones de configuración del grupo
* opciones de configuración de extremo
* perfiles de seguridad

La implementación con scripts elimina la necesidad de reconfigurar manualmente la configuración en el entorno de producción antes de iniciar aplicaciones implementadas.

1. Desde un símbolo del sistema, vaya a *[aem-forms root]*/sdk/misc/Foundation/ArchiveManagement.
1. Revise el archivo ReadMe.txt para obtener instrucciones más detalladas.
1. Modifique manualmente los archivos scriptedDeploy.bat y sample-files/sample.xml tal como se describe en el archivo readme.txt.
1. Ejecute el archivo scriptedDeploy.bat. Esta acción implementa el archivo de formularios AEM Forms con la configuración de anulación.
