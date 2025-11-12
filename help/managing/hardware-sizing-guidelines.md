---
title: Directrices de tamaño de hardware
description: Estas directrices de tamaño ofrecen una aproximación a los recursos de hardware necesarios para implementar un proyecto de AEM.
solution: Experience Manager, Experience Manager 6.5 LTS
feature: Compliance
role: Developer,Leader
exl-id: dac9b87a-cbd2-49e3-bd4d-ebcccdec1659
source-git-commit: a5e7c2326785d6801601eabc71647923ba854f04
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 100%

---

# Directrices de tamaño de hardware{#hardware-sizing-guidelines}

Estas directrices de tamaño ofrecen una aproximación a los recursos de hardware necesarios para implementar un proyecto de AEM. Las estimaciones de tamaño dependen de la arquitectura del proyecto, la complejidad de la solución, el tráfico esperado y los requisitos del proyecto. Esta guía le ayuda a determinar las necesidades de hardware para una solución específica, o a encontrar una estimación superior e inferior para los requisitos de hardware.

Los factores básicos que debe considerar son los siguientes (en este orden):

* **Velocidad de red**

   * Latencia de red
   * Ancho de banda disponible

* **Velocidad de cómputo**

   * Eficiencia del almacenamiento en caché
   * Tráfico esperado
   * Complejidad de plantillas, aplicaciones y componentes
   * Autores simultáneos
   * Complejidad de la operación de creación (edición de contenido simple, despliegue de MSM, etc.)

* **Rendimiento de E/S**

   * Rendimiento y eficacia del almacenamiento de archivos o bases de datos

* **Disco duro**

   * al menos dos o tres veces superior al tamaño del repositorio

* **Memoria**

   * Tamaño del sitio web (número de objeto de contenido, páginas y usuarios)
   * Número de usuarios/sesiones activos al mismo tiempo

## Arquitectura {#architecture}

Una configuración típica de AEM consiste en un entorno de publicación y uno de creación. Estos entornos tienen diferentes requisitos con respecto al tamaño del hardware subyacente y a la configuración del sistema. Las consideraciones detalladas para ambos entornos se describen en las secciones [Entorno de creación](/help/managing/hardware-sizing-guidelines.md#author-environment-specific-calculations) y [Entorno de publicación](/help/managing/hardware-sizing-guidelines.md#publish-environment-specific-calculations).

En una configuración de proyecto típica, tiene varios entornos en los que se pueden organizar las fases del proyecto:

* **Entorno de desarrollo**
Para desarrollar nuevas funciones o realizar cambios significativos. La práctica recomendada es trabajar con un entorno de desarrollo por desarrollador (instalaciones locales en sus sistemas personales).

* **Entorno de pruebas del autor**
Para comprobar los cambios. El número de entornos de prueba puede variar según los requisitos del proyecto (por ejemplo, separados para control de calidad, pruebas de integración o pruebas de aceptación del usuario).

* **Entorno de pruebas de publicación**
Sobre todo para probar casos de uso de colaboración social o la interacción entre la creación y varias instancias de publicación.

* **Entorno de producción de creación**
Para que los autores editen el contenido.

* **Entorno de producción de publicación**
Para servir el contenido publicado.

Además, los entornos pueden variar, desde un sistema de un solo servidor que ejecute AEM y un servidor de aplicaciones, hasta un conjunto de gran escala de instancias agrupadas de varios servidores y CPU. Adobe recomienda que utilice un equipo independiente para cada sistema de producción y que no ejecute otras aplicaciones en estos equipos.

## Consideraciones genéricas de tamaño de hardware {#generic-hardware-sizing-considerations}

Las secciones siguientes proporcionan instrucciones sobre cómo calcular los requisitos de hardware, teniendo en cuenta diversas consideraciones. En el caso de los sistemas grandes, Adobe recomienda ejecutar un conjunto sencillo de pruebas de referencia internas en una configuración de referencia.

La optimización del rendimiento es una tarea fundamental que debe hacerse antes de poder realizar cualquier evaluación comparativa para un proyecto específico. Asegúrese de aplicar los consejos proporcionados en la [documentación de optimización de rendimiento](/help/sites-deploying/configuring-performance.md) antes de realizar pruebas de referencia y usar sus resultados para cualquier cálculo de tamaño de hardware.

Los requisitos de tamaño de hardware para casos de uso avanzados deben basarse en una evaluación detallada del rendimiento del proyecto. Las características de los casos de uso avanzados que requieren recursos de hardware excepcionales incluyen combinaciones de lo siguiente:

* alto rendimiento/carga útil de contenido
* amplio uso de código personalizado, flujos de trabajo personalizados o bibliotecas de software de terceros
* integración con sistemas externos no compatibles

## Espacio en disco/disco duro {#disk-space-hard-drive}

El espacio en disco necesario depende en gran medida del volumen y del tipo de la aplicación web. Los cálculos deben tener en cuenta lo siguiente:

* la cantidad y el tamaño de las páginas, los recursos y otras entidades almacenadas en el repositorio, como flujos de trabajo, perfiles, etc.
* la frecuencia estimada de los cambios de contenido y, por lo tanto, la creación de versiones de contenido
* el volumen de representaciones de recursos DAM que se generarán
* el crecimiento general del contenido con el tiempo

El espacio en disco se supervisa continuamente durante la Limpieza de revisiones en línea y sin conexión. Si el espacio disponible en disco cae por debajo de un valor crítico, el proceso se cancela. El valor crítico es el 25 % del espacio en disco actual del repositorio y no se puede configurar. Adobe recomienda dimensionar el disco al menos dos o tres veces más grande que el tamaño del repositorio, incluido el crecimiento estimado.

### Virtualización {#virtualization}

AEM funciona bien en entornos virtualizados, pero puede haber factores como CPU o E/S que no se pueden equiparar directamente con el hardware físico. Una recomendación es elegir una velocidad de E/S más alta (en general), ya que este es un factor crítico, por lo general. La evaluación comparativa de su entorno es necesaria para comprender con precisión qué recursos se requieren.

### Paralelización de instancias de AEM {#parallelization-of-aem-instances}

**Seguridad contra fallos**

Un sitio web a prueba de fallos se implementa en al menos dos sistemas independientes. Si un sistema se avería, otro sistema puede asumir el control y así compensar el fallo del sistema.

**Escalabilidad de los recursos del sistema**

Mientras todos los sistemas están en funcionamiento, se dispone de un mayor rendimiento informático. Ese rendimiento adicional no es necesariamente lineal con el número de nodos de clúster, ya que la relación depende en gran medida del entorno técnico. Consulte [Documentación sobre clústeres](/help/sites-deploying/recommended-deploys.md) para obtener más información.

La estimación de cuántos nodos de clúster son necesarios se basa en los requisitos básicos y casos de uso específicos del proyecto web en particular:

* Desde el punto de vista de la seguridad ante errores, es necesario determinar, para todos los entornos, la gravedad de los errores y el tiempo de compensación de los mismos en función del tiempo que tarda un nodo del clúster en recuperarse.
* Para el aspecto de la escalabilidad, el número de operaciones de escritura es básicamente el factor más importante. Se puede establecer el equilibrio de carga para las operaciones que tienen acceso al sistema únicamente para procesar las operaciones de lectura; consulte [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es) para obtener detalles.

### Recomendaciones de hardware {#hardware-recommendations}

Normalmente, puede utilizar el mismo hardware para el entorno de creación que se recomienda para el entorno de publicación. Normalmente, el tráfico del sitio web es menor en los sistemas de creación, pero la eficacia de la caché también es menor. Sin embargo, el factor fundamental aquí es el número de autores que trabajan en paralelo, junto con el tipo de acciones que se realizan en el sistema. En general, la agrupación en clúster de AEM (del entorno de creación) es más eficaz para escalar las operaciones de lectura; es decir, un clúster de AEM se adapta bien a los autores que realizan operaciones de edición básicas.

## Cálculos adicionales específicos de casos de uso {#additional-use-case-specific-calculations}

Además del cálculo para una aplicación web predeterminada, tenga en cuenta factores específicos para los siguientes casos de uso. Los valores calculados se añaden al cálculo predeterminado.

### Consideraciones específicas de recursos {#assets-specific-considerations}

El procesamiento extensivo de recursos digitales requiere recursos de hardware optimizados, los factores más relevantes son el tamaño de la imagen y el rendimiento máximo de las imágenes procesadas.

Asigne al menos 16 GB de memoria y configure el flujo de trabajo [!UICONTROL DAM Update Asset] para que use el [paquete de Camera Raw](/help/assets/camera-raw.md) para la ingesta de imágenes sin procesar.

>[!NOTE]
>
>Un mayor rendimiento de las imágenes significa que los recursos informáticos deben poder seguir el ritmo de E/S del sistema y a la inversa. Por ejemplo, si la importación de imágenes inicia flujos de trabajo, la carga de muchas imágenes a través de WebDAV podría provocar un registro de flujos de trabajo pendientes.
>
>El uso de discos independientes para TarPM, almacén de datos e índice de búsqueda, puede ayudar a optimizar el comportamiento de E/S del sistema (sin embargo, normalmente tiene sentido mantener el índice de búsqueda localmente).

>[!NOTE]
>
>Consulte también la [Guía de rendimiento de Assets](/help/sites-deploying/assets-performance-sizing.md).

### Administrador de varios sitios {#multi-site-manager}

El consumo de recursos al utilizar AEM MSM en un entorno de creación depende en gran medida de los casos de uso específicos. Los factores básicos son:

* Número de Live-Copies
* Periodicidad de los despliegues
* Tamaño del árbol de contenido a desplegar
* Funcionalidad conectada de las acciones de despliegue

La prueba del caso de uso planificado con un extracto representativo del contenido puede ayudarle a comprender mejor el consumo de recursos. Si extrapola los resultados con el rendimiento planificado, puede evaluar los recursos adicionales necesarios para el MSM de AEM.

Además, tenga en cuenta los autores que trabajan en paralelo. Percibirán efectos secundarios de rendimiento si los casos de uso de AEM MSM consumen más recursos de los planeados.
