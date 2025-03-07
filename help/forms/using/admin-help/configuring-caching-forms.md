---
title: Configurar el almacenamiento en caché para Forms
description: Obtenga información sobre cómo configurar las opciones de caché y cómo agrupar las consideraciones para las cachés.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 3606e945-7f97-482f-9010-75314c23f6ac
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 1%

---

# Configurar el almacenamiento en caché para Forms{#configuring-caching-for-forms}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El servicio Forms toma diseños de formulario creados en Designer y los procesa en varios formatos.

La página Forms de la consola de administración contiene opciones que controlan la forma en que el servicio Forms almacena en caché los elementos. Puede ajustar esta configuración para optimizar el rendimiento del servicio de Forms.

El servicio Forms almacena en caché los siguientes elementos:

* **diseños de formulario:** El servicio Forms almacena en caché los diseños de formulario que recupera del repositorio o de orígenes HTTP. Este almacenamiento en caché mejora el rendimiento porque, para las solicitudes de procesamiento posteriores, el servicio Forms recupera el diseño de formulario de la caché en lugar de hacerlo del repositorio.
* **fragmentos e imágenes:** El servicio Forms puede almacenar en caché fragmentos e imágenes utilizados en diseños de formulario. Cuando el servicio Forms almacena en caché estos objetos, mejora el rendimiento porque los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud.
* **formularios:** El servicio Forms almacena en caché los formularios que procesa. Este tipo de almacenamiento en caché mejora el rendimiento porque el servicio Forms no necesita resolver y procesar el mismo formulario en solicitudes posteriores.

Forms almacena la caché en dos ubicaciones:

* **en memoria:** elementos almacenados en memoria para acceso rápido. La caché en memoria tiene un tamaño limitado y se elimina al reiniciar el servidor.
* **en el disco:** elementos almacenados en el sistema de archivos del servidor. La caché de disco tiene una capacidad mayor que la caché en memoria y se conserva cuando se reinicia el servidor. La ubicación de la caché del disco depende del servidor de aplicaciones. Para obtener información acerca de cómo cambiar la ubicación de la memoria caché del disco, vea [Configurar ubicaciones para Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).

## Especificación del modo de caché {#specifying-the-cache-mode}

Forms admite dos modos de almacenamiento en caché:

* incondicional
* uso del punto de comprobación de caché

Si cambia entre los modos de caché, reinicie el servicio Forms para que el cambio surta efecto. Para reiniciar este servicio, usa Workbench o consulta [Iniciar o detener los servicios asociados con módulos de formularios AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

El tiempo del punto de comprobación de caché se restablece automáticamente al cambiar entre modos.

### Uso del almacenamiento en caché incondicional {#using-unconditional-caching}

En este modo, cuando el servicio Forms recibe una solicitud, valida los recursos (diseño de formularios y cualquier recurso relacionado, como fragmentos e imágenes) necesarios. El servicio Forms compara la marca de tiempo de los recursos del repositorio con la de los recursos de la caché. Si el recurso de la caché es anterior, el servicio de Forms lo actualiza.

Este modo de caché garantiza que se utilicen los recursos más recientes. Sin embargo, el rendimiento se ve afectado porque el servicio Forms valida los elementos en caché con el repositorio con cada solicitud. Este modo de caché es adecuado para entornos de ensayo y desarrollo en los que los recursos se actualizan con frecuencia y el rendimiento no es una preocupación principal.

**Especificar almacenamiento en caché incondicional**

1. En la consola de administración, haga clic en Servicios > Forms.
1. En Configuración de control de caché de Forms, seleccione Incondicionalmente y haga clic en Guardar.

### Utilizar el punto de comprobación de caché {#use-the-cache-check-point}

En este modo, el servicio Forms solo comprueba el repositorio en busca de versiones más recientes de los recursos cuando la marca de tiempo del recurso en caché es anterior a la hora del punto de comprobación de caché. El tiempo del último punto de comprobación de caché se muestra en la página Forms de la consola de administración.

Utilice este modo de caché en entornos de producción de alto rendimiento donde el rendimiento sea un problema y los cambios en los recursos sean poco frecuentes. Puede restablecer el punto de comprobación de caché cada vez que desee implementar cualquier cambio realizado en los recursos del repositorio.

**Especifique el uso de un punto de comprobación de caché**

1. En Administration Console, haga clic en Services > Forms.
1. En Configuración de control de caché de Forms, seleccione Solo Si La Última Validación Se Realizó Antes Del Punto De Comprobación De Caché Y Haga Clic En Guardar.

**Restablecer el punto de comprobación de caché**

1. En la consola de administración, haga clic en Servicios > Forms.
1. En Configuración de control de caché de Forms, haga clic en Punto de comprobación de caché.

**Restablecer el contenido de la caché**

Puede borrar el contenido de la caché en cualquier momento. Después de restablecer la caché, la primera solicitud de cada formulario es más lenta porque el servicio de Forms realiza una representación completa y crea nuevo contenido de caché.

1. En la consola de administración, haga clic en Servicios > Forms.
1. En Configuración de control de caché de Forms, haga clic en Restablecer caché.

## Configuración de caché {#configuring-cache-settings}

Puede especificar la configuración que utiliza Forms para el almacenamiento en caché, lo que puede optimizar el rendimiento del entorno de los formularios de AEM.

Para acceder a esta configuración, en la consola de administración, haga clic en Servicios > Forms.

>[!NOTE]
>
>Los requisitos de disco para la caché deben ser iguales al repositorio.

### Especificar la configuración de caché global {#specifying-global-cache-settings}

La configuración del área **Configuración de caché global** afecta a todos los tipos de cachés. Si cambia cualquiera de estas opciones, reinicie el servicio Forms para que el cambio surta efecto. Para reiniciar este servicio, usa Workbench o consulta [Iniciar o detener los servicios asociados con módulos de formularios AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño máximo de documento de caché (KB):** Tamaño máximo, en kilobytes, de un diseño de formulario u otro recurso que se puede almacenar en cualquier caché en memoria. Se trata de una configuración global que se aplica a todas las cachés en memoria. Si un recurso es mayor que este valor, no se almacena en caché. El valor predeterminado es 1024 kilobytes. Esta configuración no afecta a la caché del disco.

**Caché de procesamiento de formularios habilitada:** De forma predeterminada, esta opción está seleccionada, lo que significa que los formularios procesados se almacenan en la caché para su recuperación posterior. Esta configuración mejora el rendimiento porque el servicio Forms solo debe procesar un formulario concreto una vez y, a continuación, utiliza la versión en caché. Esta opción funciona con la propiedad de almacenamiento en caché del diseño de formulario. Para obtener información sobre la configuración de este valor en el diseño de formulario, consulte la Ayuda de Designer.

### Almacenar en caché diseños de formulario {#caching-form-designs}

Cuando el servicio de Forms recibe una solicitud de procesamiento, recupera el diseño de formulario del repositorio y lo almacena en caché. Este almacenamiento en caché mejora el rendimiento porque, para las solicitudes de procesamiento posteriores, el servicio Forms recupera el diseño de formulario de la caché en lugar de hacerlo del repositorio.

El servicio Forms siempre almacena en caché los diseños de formulario del disco. Si los diseños de formulario se almacenan en el servidor, esos archivos se consideran la caché de disco. El servicio Forms también almacena en caché los diseños de formulario en la memoria, según la configuración del área **En caché de plantilla de memoria**. Si cambia cualquiera de estas opciones, reinicie el servicio Forms para que el cambio surta efecto. Para reiniciar este servicio, usa Workbench o consulta [Iniciar o detener los servicios asociados con módulos de formularios AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño de caché de configuración de plantilla:** Número máximo de objetos de configuración de plantilla que se guardarán en la memoria. El valor predeterminado es 100. Se recomienda establecer este valor en mayor o igual que el valor de Tamaño de caché de la plantilla. Esta configuración no afecta a la caché del disco.

**Tamaño de caché de plantilla:** Número máximo de objetos de contenido de plantilla que se guardarán en la memoria. El valor predeterminado es 100. Esta configuración no afecta a la caché del disco.

**Habilitado:** De forma predeterminada, esta casilla de verificación está activada, lo que significa que las plantillas de formulario se almacenan en la memoria caché. Cuando esta opción no está seleccionada, las plantillas de formulario solo se almacenan en caché en el disco.

### Almacenar formularios procesados en caché {#caching-rendered-forms}

El servicio Forms almacena en caché los formularios procesados para que no necesite resolver y procesar el mismo formulario en solicitudes posteriores. Los formularios procesados se almacenan en caché tanto en el disco como en la memoria.

Esta configuración se encuentra en el área **En caché para procesamiento de formularios en memoria**. Si cambia cualquiera de estas opciones, reinicie el servicio Forms para que el cambio surta efecto. Para reiniciar este servicio, usa Workbench o consulta [Iniciar o detener los servicios asociados con módulos de formularios AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño de caché:** Especifica el número máximo de formularios procesados que pueden residir en la caché en memoria. El valor predeterminado es 100. Esta configuración no afecta a la caché del disco.

**Habilitado:** De forma predeterminada, esta opción está seleccionada, lo que significa que los formularios procesados se almacenan en la memoria caché. Cuando esta opción no está seleccionada, los formularios procesados solo se almacenan en caché en el disco.

### Almacenamiento en caché de fragmentos e imágenes {#caching-fragments-and-images}

El servicio Forms almacena en caché fragmentos e imágenes que se utilizan en diseños de formulario en el disco. Esto mejora el rendimiento, ya que los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud. A continuación, en las solicitudes posteriores, el servicio Forms lee fragmentos e imágenes de la memoria caché del disco. Los fragmentos y las imágenes solo se almacenan en caché en el disco y no en la memoria.

Puede utilizar la siguiente configuración para controlar el almacenamiento en caché en disco de fragmentos e imágenes. Esta configuración se encuentra en el área **Configuración de caché de recursos de plantilla**:

**Almacenamiento en caché de recursos** Seleccione una de las siguientes opciones de la lista:

**Habilitado para fragmentos e imágenes:** El servicio Forms almacena en caché fragmentos e imágenes. Esta es la opción predeterminada.

**Habilitado para fragmentos:** El servicio Forms almacena en caché fragmentos, pero no imágenes.

**Deshabilitado:** El servicio Forms no almacena en caché fragmentos o imágenes.

**Intervalo de limpieza (segundos):** Especifica la frecuencia con la que el servicio Forms quita los archivos de caché antiguos no válidos. El servicio Forms no quita los archivos de caché válidos. Si cambia el intervalo de limpieza, reinicie el servicio Forms para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte Iniciar o detener los servicios asociados con módulos de formularios AEM Forms para obtener instrucciones. El valor predeterminado es 600 segundos.

## Consideraciones de clúster para cachés {#clustering-considerations-for-caches}

En un entorno agrupado, cada nodo mantiene su propia memoria en memoria y caché de disco. El contenido de la caché de cada nodo depende de los formularios que se hayan procesado en ese nodo.

La ubicación de la caché debe ser idéntica (mismo disco y ruta de acceso) en cada nodo del clúster. No coloque la caché en el almacenamiento compartido.

Si utiliza la página Forms de la consola de administración para cambiar la configuración de caché de un nodo concreto, la configuración de caché de otros nodos se actualiza cuando una solicitud va a ese nodo. Este comportamiento también se aplica al botón Restablecer caché. Si hace clic en el botón Restablecer caché de un nodo, la caché se elimina inmediatamente de ese nodo. La caché de otros nodos se borra cuando una solicitud va a ese nodo.
