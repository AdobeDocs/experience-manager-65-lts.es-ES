---
title: Configurar el almacenamiento en caché para la salida
description: El servicio Output almacena en caché los diseños de formulario, los fragmentos y las imágenes. Obtenga información sobre cómo configurar el almacenamiento en caché para los resultados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 1%

---

# Configurar el almacenamiento en caché para la salida  {#configuring-caching-for-output}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El servicio Output combina los datos de formulario XML con un diseño de formulario creado en Designer para crear una secuencia de salida de documento en varios formatos.

La página Salida de la consola de administración contiene opciones que controlan la forma en que el servicio Output almacena en caché los elementos. Puede ajustar esta configuración para optimizar el rendimiento del servicio Output.

El servicio Output almacena en caché los siguientes elementos:

* **diseños de formulario:** El servicio Output almacena en caché los diseños de formulario que recupera del repositorio o de orígenes HTTP. Este almacenamiento en caché mejora el rendimiento porque, para las solicitudes de procesamiento posteriores, el servicio Output recupera el diseño de formulario de la caché en lugar de hacerlo del repositorio.
* **fragmentos e imágenes:** El servicio Output puede almacenar en caché fragmentos e imágenes utilizados en diseños de formulario. Cuando el servicio Output almacena en caché estos objetos, mejora el rendimiento porque los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud.

La salida almacena la caché en dos ubicaciones:

* **en memoria:** elementos almacenados en memoria para acceso rápido. La caché en memoria tiene un tamaño limitado y se elimina al reiniciar el servidor.
* **en el disco:** elementos almacenados en el sistema de archivos del servidor. La caché de disco tiene una capacidad mayor que la caché en memoria y se conserva cuando se reinicia el servidor. La ubicación de la caché del disco depende del servidor de aplicaciones. Para obtener información acerca de cómo cambiar la ubicación de la caché del disco, vea [Especificar ubicaciones de archivos para la salida](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

## Especificación del modo de caché {#specifying-the-cache-mode}

La salida admite dos modos de almacenamiento en caché:

* incondicional
* uso del punto de comprobación de caché

Si cambia entre los modos de caché, reinicie el Servicio de salida para que el cambio surta efecto. Para reiniciar este servicio, usa Workbench o consulta [Iniciar o detener los servicios asociados con módulos de formularios AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

El tiempo del punto de comprobación de caché se restablece automáticamente al cambiar entre modos.

### Uso del almacenamiento en caché incondicional {#using-unconditional-caching}

En este modo, cuando el servicio Output recibe una solicitud, valida los recursos (diseño de formulario y cualquier recurso relacionado, como fragmentos e imágenes) necesarios. El servicio Output compara la marca de tiempo de los recursos del repositorio con la de los recursos de la caché. Si el recurso de la caché es anterior, el servicio Output lo actualiza.

Este modo de caché garantiza que se utilicen los recursos más recientes. Sin embargo, el rendimiento se ve afectado porque el servicio Output valida los elementos en caché con el repositorio con cada solicitud. Este modo de caché es adecuado para entornos de ensayo y desarrollo en los que los recursos se actualizan con frecuencia y el rendimiento no es una preocupación principal.

**Especificar almacenamiento en caché incondicional**

1. En la consola de administración, haga clic en Servicios > Resultados.
1. En Configuración de control de caché de salida, seleccione Incondicionalmente y haga clic en Guardar.

### Utilizar el punto de comprobación de caché {#use-the-cache-check-point}

En este modo, el servicio Output solo comprueba el repositorio en busca de versiones más recientes de los recursos cuando la marca de tiempo del recurso en caché es anterior a la hora del punto de comprobación de caché. El tiempo del último punto de comprobación de caché se muestra en la página Salida de la consola de administración.

Utilice este modo de caché en entornos de producción de alto rendimiento donde el rendimiento sea un problema y los cambios en los recursos sean poco frecuentes. Puede restablecer el punto de comprobación de caché cada vez que desee implementar cualquier cambio realizado en los recursos del repositorio.

**Especifique el uso de un punto de comprobación de caché**

1. En la consola de administración, haga clic en Servicios > Resultados.
1. En Configuración del control de caché de salida, seleccione Solo Si La Última Validación Se Realizó Antes Del Punto De Comprobación De Caché Y Haga Clic En Guardar.

**Restablecer el punto de comprobación de caché**

1. En la consola de administración, haga clic en Servicios > Resultados.
1. En Configuración del control de caché de salida, haga clic en Punto de comprobación de caché.

### Restablecer el contenido de la caché {#reset-the-cache-contents}

Puede borrar el contenido de la caché en cualquier momento. Después de restablecer la caché, la primera solicitud de cada formulario es más lenta porque el servicio Output realiza una representación completa y crea nuevo contenido de caché.

1. En la consola de administración, haga clic en Servicios > Resultados.
1. En Configuración de control de caché de salida, haga clic en Restablecer caché.

## Configuración de caché {#configuring-cache-settings}

Puede especificar la configuración que utiliza Output para el almacenamiento en caché, lo que puede optimizar el rendimiento del entorno de los formularios AEM Forms.

Para acceder a esta configuración, en la consola de administración, haga clic en Services > output.

>[!NOTE]
>
>Los requisitos de disco para la caché deben ser iguales al repositorio.

### Especificar la configuración de caché global {#specifying-global-cache-settings}

La configuración del área **Configuración de caché global** afecta a todos los tipos de cachés. Si cambia cualquiera de estas opciones, reinicie el Servicio de salida para que el cambio surta efecto. Para reiniciar este servicio, usa Workbench o consulta [Iniciar o detener los servicios asociados con módulos de formularios AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño máximo de documento de caché (KB):** Tamaño máximo, en kilobytes, de un diseño de formulario u otro recurso que se puede almacenar en cualquier caché en memoria. Se trata de una configuración global que se aplica a todas las cachés en memoria. Si el recurso es mayor que este valor, no se almacena en caché. El valor predeterminado es 1024 kilobytes. Esta configuración no afecta a la caché del disco.

**Caché de procesamiento de formularios habilitada:** De forma predeterminada, esta opción está seleccionada, lo que significa que los formularios procesados se almacenan en la caché para su recuperación posterior. Esta configuración tiene poco efecto en el rendimiento del servicio Output porque no almacena en caché documentos no interactivos. Esta opción no tiene efecto cuando utiliza el servicio Output para documentos no interactivos que se representan en el cliente.

### Almacenar en caché diseños de formulario {#caching-form-designs}

Cuando el servicio Output recibe una solicitud de procesamiento, recupera el diseño de formulario del repositorio o de una fuente HTTP y lo almacena en caché. Este almacenamiento en caché mejora el rendimiento porque, para las solicitudes de procesamiento posteriores, el servicio Output recupera el diseño de formulario de la caché en lugar de hacerlo del repositorio.

El servicio Output siempre almacena en caché los diseños de formulario en el disco. Si los diseños de formulario se almacenan en el servidor, esos archivos se consideran la caché de disco. El servicio Output también almacena en caché los diseños de formulario en la memoria, según la configuración del área **En caché de plantilla de memoria**. Si cambia cualquiera de estas opciones, reinicie el Servicio de salida para que el cambio surta efecto. Para reiniciar este servicio, usa Workbench o consulta [Iniciar o detener los servicios asociados con módulos de formularios AEM Forms](/help/forms/using/admin-help/starting-stopping-services.md#start-or-stop-the-services-associated-with-aem-forms-modules) para obtener instrucciones.

**Tamaño de caché de configuración de plantilla:** Número máximo de objetos de configuración de plantilla que se guardarán en la memoria. El valor predeterminado es 100. Se recomienda establecer este valor en mayor o igual que el valor de Tamaño de caché de la plantilla. Esta configuración no afecta a la caché del disco.

**Tamaño de caché de plantilla:** Número máximo de objetos de contenido de plantilla que se guardarán en la memoria. El valor predeterminado es 100. Esta configuración no afecta a la caché del disco.

**Habilitado:** De forma predeterminada, esta casilla de verificación está activada, lo que significa que las plantillas de formulario se almacenan en la memoria caché. Cuando esta opción no está seleccionada, las plantillas de formulario solo se almacenan en caché en el disco.

### Almacenamiento en caché de fragmentos e imágenes {#caching-fragments-and-images}

El servicio Output almacena en caché fragmentos e imágenes que se utilizan en diseños de formulario en disco. Esto mejora el rendimiento, ya que los fragmentos y las imágenes solo se leen desde el repositorio en la primera solicitud. A continuación, en solicitudes posteriores, el servicio Output lee fragmentos e imágenes de la caché de disco. Los fragmentos y las imágenes solo se almacenan en caché en el disco y no en la memoria.

Puede utilizar la siguiente configuración para controlar el almacenamiento en caché en disco de fragmentos e imágenes. Esta configuración se encuentra en el área **Configuración de caché de recursos de plantilla**:

**Almacenamiento en caché de recursos** Seleccione una de las siguientes opciones de la lista:

**Habilitado para fragmentos e imágenes:** El servicio Output almacena en caché fragmentos e imágenes. Esta es la opción predeterminada.

**Habilitado para fragmentos:** El servicio Output almacena en caché fragmentos, pero no imágenes.

**Deshabilitado:** El servicio Output no almacena en caché fragmentos o imágenes.

**Intervalo de limpieza (segundos):** Especifica la frecuencia con la que el Servicio de salida quita los archivos de caché antiguos no válidos. El servicio Output no quita los archivos de caché válidos. Si cambia el intervalo de limpieza, reinicie el Servicio de salida para que el cambio surta efecto. Para reiniciar este servicio, utilice Workbench o consulte Iniciar o detener los servicios asociados con módulos de formularios AEM Forms para obtener instrucciones.

## Consideraciones de clúster para cachés {#clustering-considerations-for-caches}

En un entorno agrupado, cada nodo mantiene su propia memoria en memoria y caché de disco. El contenido de la caché de cada nodo depende de los formularios que se hayan procesado en ese nodo.

La ubicación de la caché debe ser idéntica (mismo disco y ruta de acceso) en cada nodo del clúster. No coloque la caché en el almacenamiento compartido.

Si utiliza la página Salida de la consola de administración para cambiar la configuración de caché de un nodo concreto, la configuración de caché de otros nodos se actualiza cuando una solicitud va a ese nodo. Este comportamiento también se aplica al botón Restablecer caché. Si hace clic en el botón Restablecer caché de un nodo, la caché se elimina inmediatamente de ese nodo. La caché de otros nodos se borra cuando una solicitud va a ese nodo.
