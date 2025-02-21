---
title: Consideraciones y requisitos de red
description: Explica las consideraciones de red al diseñar una implementación de  [!DNL Adobe Experience Manager Assets] .
contentOwner: AG
role: Architect, Admin
feature: Developer Tools
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---

# [!DNL Assets] consideraciones de red {#assets-network-considerations}

Comprender su red es tan importante como comprender [!DNL Adobe Experience Manager Assets]. La red puede afectar a las experiencias de carga, descarga y usuario. El diagrama de la topología de red ayuda a identificar los puntos de estrangulamiento y las áreas suboptimizadas de la red que debe corregir para mejorar el rendimiento de la red y la experiencia del usuario.

Asegúrese de incluir lo siguiente en el diagrama de red:

* Conectividad desde el dispositivo cliente (por ejemplo, equipo, móvil y tableta) a la red.
* Topología de la red corporativa.
* Vínculo superior a Internet desde la red corporativa y el entorno [!DNL Experience Manager].
* Topología del entorno [!DNL Experience Manager].
* Definir consumidores simultáneos de la interfaz de red [!DNL Experience Manager].
* Flujos de trabajo definidos de la implementación [!DNL Experience Manager].

## Conectividad desde el dispositivo cliente a la red corporativa {#connectivity-from-the-client-device-to-the-corporate-network}

Comience por crear un diagrama de la conectividad entre los dispositivos cliente individuales y la red corporativa. En esta fase, identifique los recursos compartidos, como las conexiones WiFi, en las que varios usuarios acceden al mismo punto o conmutan Ethernet para cargar y descargar recursos.

![chlimage_1-353](assets/chlimage_1-353.png)

Los dispositivos cliente se conectan a la red corporativa de varias formas, como WiFi compartida, Ethernet a un conmutador compartido y VPN. Identificar y comprender los puntos de estrangulamiento de esta red es importante para la planificación de [!DNL Assets] y para modificar la red.

En la parte superior izquierda del diagrama, tres dispositivos se representan compartiendo un punto de acceso WiFi de 48 Mbps. Si todos los dispositivos se cargan simultáneamente, el ancho de banda de la red WiFi se comparte entre los dispositivos. En comparación con el sistema en su conjunto, un usuario puede encontrar un punto de estrangulamiento diferente para los tres clientes a través de este canal dividido.

Es un desafío medir la velocidad real de una red WiFi porque un dispositivo lento puede afectar a otros clientes en el punto de acceso. Si planea utilizar WiFi para interacciones de recursos, realice una prueba de velocidad desde varios clientes simultáneamente para evaluar el rendimiento.

La parte inferior izquierda del diagrama muestra dos dispositivos conectados a la red corporativa a través de canales independientes. Por lo tanto, cada dispositivo puede disponer de una velocidad mínima de 10 Mbps y 100 Mbps.

El equipo mostrado a la derecha tiene un flujo ascendente limitado a la red corporativa a través de una VPN con una velocidad de 1 Mbps. La experiencia del usuario con la conexión de 1 Mbps es muy diferente de la experiencia del usuario con la conexión de 1 Gbps. Según el tamaño de los recursos con los que interactúen los usuarios, el vínculo superior de VPN puede ser inadecuado para la tarea.

## Topología de la red corporativa {#topology-of-the-corporate-network}

![chlimage_1-354](assets/chlimage_1-354.png)

El diagrama muestra velocidades de enlace ascendente más altas dentro de la red corporativa que las que se utilizan generalmente. Estas canalizaciones son recursos compartidos. Si se espera que el conmutador compartido gestione 50 clientes, puede ser potencialmente un punto de estrangulamiento. En el diagrama inicial, sólo dos equipos comparten la conexión concreta.

## Vincular a Internet desde la red corporativa y el entorno [!DNL Experience Manager] {#uplink-to-the-internet-from-the-corporate-network-and-aem-environment}

![chlimage_1-355](assets/chlimage_1-355.png)

Es importante tener en cuenta factores desconocidos en Internet y en la conexión de VPC, ya que el ancho de banda a través de Internet puede verse afectado debido a la carga máxima o a las interrupciones del proveedor a gran escala. En general, la conectividad a Internet es fiable. Sin embargo, a veces puede introducir puntos de estrangulamiento.

En el enlace ascendente de una red corporativa a Internet, puede haber otros servicios utilizando el ancho de banda. Es importante comprender qué parte del ancho de banda se puede dedicar o priorizar para Assets. Por ejemplo, si un vínculo de 1 Gbps ya está en un 80% de uso, sólo puede asignar un máximo del 20% del ancho de banda para [!DNL Experience Manager Assets].

Los servidores de seguridad y los servidores proxy empresariales también pueden configurar el ancho de banda de muchas maneras diferentes. Este tipo de dispositivo puede priorizar el ancho de banda mediante la calidad del servicio, las limitaciones de ancho de banda por usuario o las limitaciones de velocidad de bits por host. Estos son puntos de bloqueo importantes que deben examinarse ya que pueden afectar de manera significativa la experiencia del usuario [!DNL Assets].

En este ejemplo, la empresa tiene un vínculo superior de 10 Gb/s. Debe ser lo suficientemente grande para varios clientes. Además, el cortafuegos impone un límite de velocidad de host de 10 Mbps. Esta limitación puede limitar potencialmente el tráfico a un solo host a 10 Mbps, aunque el vínculo superior a Internet esté a 10 Gbps.

Este es el punto de estrangulamiento más pequeño orientado al cliente. Sin embargo, puede realizar una evaluación de un cambio o configurar una lista de permitidos con el grupo de operaciones de red a cargo de este cortafuegos.

A partir de los diagramas de ejemplo, puede concluir que seis dispositivos comparten un canal conceptual de 10 Mbps. Según el tamaño de los recursos utilizados, esto puede ser insuficiente para satisfacer las expectativas de los usuarios.

## Topología del entorno [!DNL Experience Manager] {#topology-of-the-aem-environment}

![chlimage_1-356](assets/chlimage_1-356.png)

El diseño de la topología del entorno [!DNL Experience Manager] requiere un conocimiento detallado de la configuración del sistema y de cómo está conectada la red dentro del entorno del usuario.

El escenario de ejemplo incluye un conjunto de servidores de publicación con cinco servidores, un almacén binario S3 y Dynamic Media configurado.

Dispatcher comparte su conexión de 100 Mbps con dos entidades, el mundo exterior y la implementación [!DNL Experience Manager]. Para realizar operaciones simultáneas de carga y descarga, se debe dividir este número entre dos. El almacenamiento externo adjunto utiliza una conexión independiente.

La implementación de [!DNL Experience Manager] comparte su conexión de 1 Gb/s con varios servicios. Desde la perspectiva de la topología de red, equivale a compartir un solo canal con distintos servicios.

Revisando la red desde el dispositivo cliente hasta la implementación [!DNL Experience Manager], el punto de estrangulamiento más pequeño parece ser el límite del firewall empresarial de 10 Mbits. Puede usar estos valores en la calculadora de tamaño de la [Guía de tamaño de Assets](assets-sizing-guide.md) para determinar la experiencia del usuario.

## Flujos de trabajo definidos de la implementación [!DNL Experience Manager] {#defined-workflows-of-the-aem-deployment}

Al considerar el rendimiento de la red, puede ser importante tener en cuenta los flujos de trabajo y la publicación que se producirán en el sistema. Además, S3 u otro almacenamiento conectado a la red que utilice y las solicitudes de E/S consumen ancho de banda de la red. Por lo tanto, incluso en una red totalmente optimizada, el rendimiento puede estar limitado por la E/S del disco.

Para optimizar los procesos relacionados con la ingesta de recursos (especialmente al cargar un gran número de recursos), explore los flujos de trabajo de recursos y conozca mejor su configuración.

Al evaluar la topología del flujo de trabajo interno, debe analizar lo siguiente:

* Procedimientos que escriben un recurso
* Flujos de trabajo/eventos en déclencheur al modificar recursos o metadatos
* Procedimientos que leen un recurso

Estos son algunos elementos que hay que tener en cuenta:

* Lectura/escritura diferida de metadatos XMP
* Activación y replicación automáticas
* Filigrana
* Ingesta de subrecursos/extracción de página
* Flujos de trabajo superpuestos.

Este es un ejemplo de cliente para la definición de un flujo de trabajo de recursos.

![chlimage_1-357](assets/chlimage_1-357.png)
