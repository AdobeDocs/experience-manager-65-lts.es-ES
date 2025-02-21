---
title: Guía de tamaño de [!DNL Assets]
description: Prácticas recomendadas para determinar métricas eficientes a fin de estimar la infraestructura y los recursos necesarios para implementar [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 0%

---

# Guía de tamaño de [!DNL Assets] {#assets-sizing-guide}

Al cambiar el tamaño del entorno para una implementación de [!DNL Adobe Experience Manager Assets], es importante asegurarse de que haya suficientes recursos disponibles en términos de rendimiento de disco, CPU, memoria, E/S y red. El tamaño de muchos de estos recursos requiere una comprensión de cuántos recursos se cargan en el sistema. Si no hay una métrica mejor disponible, puede dividir el tamaño de la biblioteca existente por la edad de la biblioteca para encontrar la velocidad a la que se crean los recursos.

## Disco {#disk}

### DataStore {#datastore}

Un error común que se comete al dimensionar el espacio en disco necesario para una implementación de [!DNL Assets] es basar los cálculos en el tamaño de las imágenes sin procesar que se van a ingerir en el sistema. De manera predeterminada, [!DNL Experience Manager] crea tres representaciones además de la imagen original para usarlas en el procesamiento de los elementos de la interfaz de usuario [!DNL Experience Manager]. En implementaciones anteriores, se ha observado que estas representaciones suponen el doble del tamaño de los recursos que se incorporan.

La mayoría de los usuarios definen representaciones personalizadas además de las representaciones predeterminadas. Además de las representaciones, [!DNL Assets] le permite extraer recursos secundarios de tipos de archivo comunes, como [!DNL Adobe InDesign] y [!DNL Adobe Illustrator].

Por último, las capacidades de versiones de [!DNL Experience Manager] almacenan duplicados de los recursos en el historial de versiones. Puede configurar las versiones que desea purgar con frecuencia. Sin embargo, muchos usuarios eligen conservar las versiones en el sistema durante mucho tiempo, lo que consume espacio de almacenamiento adicional.

Teniendo en cuenta estos factores, necesita una metodología para calcular un espacio de almacenamiento aceptablemente preciso para almacenar los recursos del usuario.

1. Determine el tamaño y el número de recursos que se cargan en el sistema.
1. Obtenga una muestra representativa de los recursos que se van a cargar en [!DNL Experience Manager]. Por ejemplo, si planea cargar archivos de PSD, JPG, IA y PDF en el sistema, necesita varias imágenes de muestra de cada formato de archivo. Además, estas muestras deben ser representativas de los diferentes tamaños y complejidades de archivo de las imágenes.
1. Defina las representaciones que desea utilizar.
1. Cree las representaciones en [!DNL Experience Manager] utilizando [!DNL ImageMagick] o [!DNL Adobe Creative Cloud] aplicaciones. Además de las representaciones que especifiquen los usuarios, cree representaciones listas para usarse. Para los usuarios que implementan Dynamic Media, puede utilizar el binario IC para generar las representaciones PTIFF que se almacenarán en Experience Manager.
1. Si planea utilizar subrecursos, genérelos para los tipos de archivo adecuados.
1. Compare el tamaño de las imágenes, representaciones y subrecursos de salida con las imágenes originales. Permite generar un factor de crecimiento esperado cuando se carga el sistema. Por ejemplo, si genera representaciones y subrecursos con un tamaño combinado de 3 GB después de procesar 1 GB de recursos, el factor de crecimiento de la representación es 3.
1. Determine el tiempo máximo para el mantenimiento de las versiones de recursos en el sistema.
1. Determine la frecuencia con la que se modifican los recursos existentes en el sistema. Si [!DNL Experience Manager] se usa como centro de colaboración en flujos de trabajo creativos, la cantidad de cambios es alta. Si solo se cargan los recursos finalizados en el sistema, este número es mucho menor.
1. Determine cuántos recursos se cargan en el sistema cada mes. Si no está seguro, compruebe el número de recursos disponibles actualmente y divida el número por la edad del recurso más antiguo para calcular un número aproximado.

Al realizar los pasos anteriores, puede determinar lo siguiente:

* Tamaño sin procesar de los recursos que se van a cargar.
* Número de recursos que cargar.
* Factor de crecimiento de representación.
* Número de modificaciones de recursos realizadas por mes.
* Número de meses para mantener las versiones de los recursos.
* Número de nuevos recursos cargados cada mes.
* Años de crecimiento en la asignación de espacio de almacenamiento.

Puede especificar estos números en la hoja de cálculo Tamaño de la red para determinar el espacio total necesario para el almacén de datos. También es una herramienta útil para determinar el impacto de mantener versiones de recursos o modificar recursos en [!DNL Experience Manager] en el crecimiento del disco.

Los datos de ejemplo rellenados en la herramienta demuestran la importancia de realizar los pasos mencionados. Si cambia el tamaño del almacén de datos únicamente en función de las imágenes sin procesar que se están cargando (1 TB), es posible que haya subestimado el tamaño del repositorio en un factor de 15.

[Obtener archivo](assets/disk_sizing_tool.xlsx)

### Almacenes de datos compartidos {#shared-datastores}

Para los almacenes de datos grandes, puede implementar un almacén de datos compartido a través de un almacén de datos de archivos compartidos en una unidad conectada a la red o a través de un almacén de datos de Amazon S3. En este caso, las instancias individuales no necesitan mantener una copia de los binarios. Además, un almacén de datos compartido facilita la replicación sin binarios y ayuda a reducir el ancho de banda utilizado para replicar recursos en entornos de publicación.

#### Casos de uso {#use-cases}

El almacén de datos se puede compartir entre una instancia de autor principal y una instancia de autor en espera para minimizar el tiempo que se tarda en actualizar la instancia en espera con los cambios realizados en la instancia principal. También puede compartir el almacén de datos entre las instancias de autor y publicación para minimizar el tráfico durante la replicación.

#### Inconvenientes {#drawbacks}

Debido a algunos inconvenientes, no se recomienda compartir un almacén de datos en todos los casos.

#### Punto único de error {#single-point-of-failure}

Tener un almacén de datos compartido introduce un único punto de fallo en una infraestructura. Imagine un escenario en el que el sistema tenga una instancia de autor y dos instancias de publicación, cada una con su propio almacén de datos. Si alguno de ellos se bloquea, los otros dos aún pueden seguir corriendo. Sin embargo, si se comparte el almacén de datos, un solo error de disco puede acabar con toda la infraestructura. Por lo tanto, asegúrese de mantener una copia de seguridad del almacén de datos compartido desde el que pueda restaurarlo rápidamente.

Se prefiere implementar el servicio AWS S3 para almacenes de datos compartidos porque reduce significativamente la probabilidad de error en comparación con las arquitecturas de disco normales.

#### Mayor complejidad {#increased-complexity}

Los almacenes de datos compartidos también aumentan la complejidad de las operaciones, como la recolección de elementos no utilizados. Normalmente, la recolección de elementos no utilizados de un almacén de datos independiente se puede iniciar con un solo clic. Sin embargo, los almacenes de datos compartidos requieren operaciones de barrido de marca en cada miembro que utilice el almacén de datos, además de ejecutar la colección real en un solo nodo.

En el caso de las operaciones de AWS, la implementación de una única ubicación central (mediante Amazon S3), en lugar de crear una matriz RAID de volúmenes EBS, puede compensar de forma significativa la complejidad y los riesgos operativos del sistema.

#### Problemas de rendimiento {#performance-concerns}

Un almacén de datos compartido requiere que los binarios se almacenen en una unidad montada en red que se comparta entre todas las instancias. Dado que se accede a estos binarios a través de una red, el rendimiento del sistema se ve afectado negativamente. Puede mitigar parcialmente el impacto utilizando una conexión de red rápida a una matriz rápida de discos. Sin embargo, esta es una propuesta costosa. Si hay operaciones de AWS, todos los discos son remotos y requieren conectividad de red. Los volúmenes efímeros pierden datos cuando la instancia se inicia o detiene.

#### Latencia {#latency}

La latencia en las implementaciones de S3 se introduce mediante los hilos de escritura en segundo plano. Los procedimientos de copia de seguridad deben tener en cuenta esta latencia. Además, los índices de Lucene pueden permanecer incompletos al realizar una copia de seguridad. Se aplica a cualquier archivo con distinción de tiempo escrito en el almacén de datos S3 y al que se accede desde otra instancia.

### Almacén de nodos o almacén de documentos {#node-store-document-store}

Es difícil obtener cifras de tamaño precisas para un NodeStore o DocumentStore debido a los recursos consumidos por lo siguiente:

* Metadatos de recursos
* Versiones de recursos
* Registros de auditoría
* Flujos de trabajo archivados y activos

Dado que los binarios se almacenan en el almacén de datos, cada binario ocupa cierto espacio. La mayoría de los repositorios tienen menos de 100 GB. Sin embargo, puede haber repositorios más grandes de hasta 1 TB de tamaño. Además, para realizar la compactación sin conexión, necesita suficiente espacio libre en el volumen para reescribir el repositorio compactado junto con la versión precompactada. Una buena regla general es cambiar el tamaño del disco a 1,5 veces el tamaño esperado para el repositorio.

Para el repositorio, utilice SSD o discos con un nivel de IOPS mayor que 3000. Para eliminar las posibilidades de que las IOPS introduzcan cuellos de botella de rendimiento, monitorice los niveles de espera de E/S de CPU para detectar signos tempranos de problemas.

[Obtener archivo](assets/aem_environment_sizingtool.xlsx)

## Red {#network}

[!DNL Assets] tiene varios casos de uso que hacen que el rendimiento de la red sea más importante que en muchos de nuestros [!DNL Experience Manager] proyectos. Un cliente puede tener un servidor rápido, pero si la conexión de red no es lo suficientemente grande como para admitir la carga de los usuarios que cargan y descargan recursos del sistema, seguirá apareciendo como lenta. Hay una buena metodología para determinar el punto de estrangulamiento en la conexión de red de un usuario a [!DNL Experience Manager] en [Assets se tienen en cuenta la experiencia del usuario, el tamaño de las instancias, la evaluación del flujo de trabajo y la topología de red](/help/assets/assets-network-considerations.md).

## Limitaciones {#limitations}

Al cambiar el tamaño de una implementación, es importante tener en cuenta las limitaciones del sistema. Si la implementación propuesta supera estas limitaciones, emplee estrategias creativas, como dividir los recursos en varias implementaciones de [!DNL Assets].

El tamaño del archivo no es el único factor que contribuye a los problemas de falta de memoria (OOM). También depende de las dimensiones de la imagen. Puede evitar problemas de OM si proporciona un tamaño de pila mayor al iniciar [!DNL Experience Manager].

Además, puede editar la propiedad de tamaño de umbral del componente `com.day.cq.dam.commons.handler.StandardImageHandler` en el Administrador de configuración para utilizar un archivo temporal intermedio mayor que cero.

## Número máximo de recursos {#maximum-number-of-assets}

El límite del número de archivos que pueden existir en un almacén de datos puede ser de 2100 millones debido a las limitaciones del sistema de archivos. Es probable que el repositorio encuentre problemas debido a un gran número de nodos mucho antes de alcanzar el límite del almacén de datos.

Si las representaciones se generan incorrectamente, utilice la biblioteca de Camera Raw. Sin embargo, en este caso, el lado más largo de la imagen no debe ser mayor de 65000 píxeles. Además, la imagen no debe contener más de 512 MP (512 x 1024 x 1024 píxeles). El tamaño del recurso no importa.

Es difícil calcular con precisión el tamaño del archivo TIFF que se admite de forma predeterminada con un montón específico para [!DNL Experience Manager] porque factores adicionales, como el tamaño de los píxeles, influyen en el procesamiento. Es posible que [!DNL Experience Manager] pueda procesar de forma predeterminada un archivo de tamaño de 255 MB, pero no puede procesar un tamaño de archivo de 18 MB porque este último consta de un número de píxeles inusualmente mayor que el primero.

## Tamaño de los recursos {#size-of-assets}

De manera predeterminada, [!DNL Experience Manager] le permite cargar recursos con un tamaño de archivo de hasta 2 GB. Para cargar recursos muy grandes en [!DNL Experience Manager], consulte [Configuración para cargar recursos muy grandes](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
