---
title: Especificar ubicaciones de archivos para la salida
description: Obtenga información sobre cómo especificar ubicaciones de archivos para la salida para determinados tipos de archivos, por ejemplo, URI raíz de contenido, archivo de configuración XCI, caché y predeterminado.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 4%

---

# Especificar ubicaciones de archivos para la salida {#specify-file-locations-for-output}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Puede especificar las ubicaciones en las que Output busca determinados tipos de archivos que necesita.

1. En la consola de administración, haga clic en Servicios > Resultados.
1. En Ubicaciones, especifique las opciones adecuadas.
1. Haga clic en Guardar.

## Configuración de ubicaciones {#locations-settings}

**URI de raíz de contenido:** URI o ubicación absoluta del repositorio del que se recuperan los formularios. Este valor se combina con el parámetro sForm, especificado mediante la API, para construir la ruta absoluta al formulario que se recupera. Este valor puede hacer referencia a un directorio o a una ubicación web a la que se puede acceder mediante HTTP.

El valor predeterminado es una cadena vacía.

**Archivo de configuración XCI:** Ubicación relativa o absoluta del archivo de configuración XCI que el servicio Output utiliza para la representación. Para un valor relativo, se supone que el archivo XCI reside en el archivo EAR implementable de los formularios AEM Forms.

El valor predeterminado es `com/adobe/formServer/PA/pa_output.xci`.

**Ubicación de la caché:** Especifica la ubicación de la caché del disco de salida. Al cambiar esta configuración, se restablece toda la información de caché existente de la ubicación actual y se crea una nueva caché en la nueva ubicación. Seleccione una de las siguientes opciones:

**Ubicación predeterminada:** Esta es la selección predeterminada. Cuando se selecciona esta opción, la caché se crea en una ubicación que depende del servidor de aplicaciones que esté utilizando:

* **JBoss:** `[JBoss Home]\server\[install type]\svcdata\Output\Cache`
* **WebLogic:** `[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere:** `[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Directorio temporal LC:** La caché se crea en un subdirectorio del directorio temporal de AEM Forms, que se especifica en la consola de administración en Configuración > Configuración del sistema principal > Configuraciones > Ubicación del directorio temporal. El nombre del subdirectorio es `adobeoutput_[servername]`.

>[!NOTE]
>
>Si utiliza una utilidad de limpieza temporal, mientras que la eliminación de estos directorios no afecta a la funcionalidad, puede afectar significativamente al rendimiento durante un corto tiempo, hasta que se cree la nueva caché. Para evitar este problema, no elimine estos directorios mientras borra el directorio temporal de los formularios AEM Forms.
