---
title: Mejorar el rendimiento del servidor de aplicaciones
description: En este documento se describen las opciones opcionales que se pueden configurar para mejorar el rendimiento del servidor de aplicaciones de AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 0%

---

# Mejorar el rendimiento del servidor de aplicaciones{#enhancing-application-server-performance}

En este contenido se describen las opciones opcionales que se pueden configurar para mejorar el rendimiento del servidor de aplicaciones de AEM Forms.

## Configuración de fuentes de datos del servidor de aplicaciones {#configuring-application-server-data-sources}

AEM Forms utiliza el repositorio de formularios de AEM como fuente de datos. El repositorio de formularios de AEM almacena recursos de la aplicación y, en tiempo de ejecución, los servicios pueden recuperar recursos del repositorio como parte de la finalización de un proceso empresarial automatizado.

El acceso al origen de datos puede ser significativo, en función del número de módulos de formularios AEM Forms que se estén ejecutando y del número de usuarios simultáneos que accedan a la aplicación. El acceso a la fuente de datos se puede optimizar mediante la agrupación de conexiones. *Agrupación de conexiones* es una técnica que se usa para evitar la sobrecarga de realizar nuevas conexiones de base de datos cada vez que una aplicación o un objeto de servidor requiere acceso a la base de datos. La agrupación de conexiones se utiliza generalmente en aplicaciones empresariales y basadas en la web, y la gestiona, entre otras cosas, un servidor de aplicaciones.

Es importante configurar correctamente los parámetros del grupo de conexiones para que nunca se quede sin conexiones, lo que puede provocar que el rendimiento de la aplicación se deteriore.

Para establecer correctamente la configuración del grupo de conexiones, es importante que el administrador del servidor de aplicaciones supervise el grupo de conexiones durante las horas de mayor actividad del día. La monitorización garantiza que haya suficientes conexiones disponibles para las aplicaciones y los usuarios en todo momento. La mayoría de los servidores de aplicaciones incluyen herramientas de monitorización.

Puede monitorizar varias estadísticas para cada instancia de fuente de datos JDBC en su dominio mediante la consola de administración del servidor de WebLogic. Consulte la documentación de WebLogic para obtener más información.

Cuando el administrador del servidor de aplicaciones determina la configuración correcta del grupo de conexiones, esa persona debe comunicar esta información al administrador de la base de datos. El administrador de la base de datos necesita esta información porque el número de conexiones de base de datos es igual al número de conexiones del grupo de conexiones para el origen de datos. A continuación, complete los pasos para establecer la configuración del grupo de conexiones para el servidor de aplicaciones y el tipo de origen de datos como se describe a continuación.

### Configuración del grupo de conexiones para WebLogic para Oracle y MySQL {#configure-connection-pool-settings-for-weblogic-for-oracle-and-mysql}

1. En Estructura de dominio, haga clic en Servicios > JDBC > Fuentes de datos y, en el panel derecho, haga clic en IDP_DS.
1. En la siguiente pantalla, haga clic en la pestaña Configuración > Grupo de conexiones e introduzca un valor en los siguientes cuadros:

   * Capacidad inicial
   * Capacidad máxima
   * Incremento de capacidad
   * Tamaño del almacenamiento de instrucciones

1. Haga clic en Guardar y luego en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

### Configurar las opciones del grupo de conexiones para WebLogic para SQL Server {#configure-connection-pool-settings-for-weblogic-for-sqlserver}

1. En Centro de cambios, haga clic en Bloquear y editar.
1. En Estructura de dominio, haga clic en Servicios > JDBC > Fuentes de datos y, en el panel derecho, haga clic en EDC_DS.
1. En la siguiente pantalla, haga clic en la pestaña Configuración > Grupo de conexiones e introduzca un valor en los siguientes cuadros:

   * Capacidad inicial
   * Capacidad máxima
   * Incremento de capacidad
   * Tamaño del almacenamiento de instrucciones

1. Haga clic en Guardar y luego en Activar cambios.
1. Reinicie el servidor administrado por WebLogic.

### Configuración del grupo de conexiones para WebSphere para DB2 {#configure-connection-pool-settings-for-websphere-for-db2}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores JDBC. En el panel derecho, haga clic en el origen de datos que ha creado, ya sea Proveedor de controlador JDBC universal de DB2 o LiveCycle - db2 - IDP_DS.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la siguiente pantalla, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Máximo de conexiones y en el cuadro Mínimo de conexiones.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en configuración maestra.

### Configuración del grupo de conexiones para WebSphere para Oracle {#configure-connection-pool-settings-for-websphere-for-oracle}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores JDBC. En el panel derecho, haga clic en la fuente de datos del controlador JDBC de Oracle que ha creado.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la siguiente pantalla, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Máximo de conexiones y en el cuadro Mínimo de conexiones.
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en configuración maestra.

### Configurar la configuración del grupo de conexiones para WebSphere para SqlServer {#configure-connection-pool-settings-for-websphere-for-sqlserver}

1. En el árbol de navegación, haga clic en Recursos > JDBC > Proveedores JDBC y, en el panel derecho, haga clic en el origen de datos del controlador JDBC definido por el usuario que ha creado.
1. En Propiedades adicionales, haga clic en Fuentes de datos y, a continuación, seleccione IDP_DS.
1. En la siguiente pantalla, en Propiedades adicionales, haga clic en Propiedades del grupo de conexiones e introduzca un valor en el cuadro Máximo de conexiones y en el cuadro Mínimo de conexiones:
1. Haga clic en Aceptar o Aplicar y, a continuación, haga clic en Guardar directamente en configuración maestra.

## Optimización de documentos en línea e impacto en la memoria JVM {#optimizing-inline-documents-and-impact-on-jvm-memory}

Si normalmente procesa documentos de un tamaño relativamente pequeño, puede mejorar el rendimiento asociado con la velocidad de transferencia de documentos y el espacio de almacenamiento. Para ello, implemente las siguientes configuraciones de producto de los formularios AEM Forms:

* Aumente el tamaño máximo en línea del documento predeterminado para los formularios de AEM de modo que sea mayor que el tamaño de la mayoría de los documentos.
* Para procesar archivos de mayor tamaño, especifique los directorios de almacenamiento que se encuentran en un sistema de disco de alta velocidad o en un disco RAM.

El tamaño máximo en línea y los directorios de almacenamiento (el directorio de archivos temporales de formularios AEM Forms y el directorio GDS) se configuran en la consola de administración.

### Tamaño de documento y tamaño máximo en línea {#document-size-and-maximum-inline-size}

Cuando un documento enviado para su procesamiento por formularios AEM Forms tiene un tamaño en línea inferior o igual al tamaño en línea máximo del documento predeterminado, el documento se almacena en el servidor en línea y se serializa como un objeto de documento de Adobe. Almacenar documentos en línea puede tener importantes ventajas de rendimiento. Sin embargo, si utiliza el flujo de trabajo de formularios, el contenido también se puede almacenar en la base de datos para realizar un seguimiento. Por lo tanto, aumentar el tamaño máximo en línea puede afectar al tamaño de la base de datos.

Un documento que es mayor que el tamaño máximo en línea se almacena en el sistema de archivos local. El objeto Documento de Adobe que se transfiere desde y hacia el servidor es sólo un puntero a ese archivo.

Cuando el contenido del documento está en línea (es decir, es menor que el tamaño máximo en línea), el contenido se almacena en la base de datos como parte de la carga útil de serialización del documento. Por lo tanto, aumentar el tamaño máximo en línea puede afectar al tamaño de la base de datos.

**Cambiar el tamaño máximo en línea**

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Configuración > Configuración del sistema principal > Configuraciones.
1. Introduzca un valor en el cuadro Tamaño máximo en línea del documento predeterminado y haga clic en Aceptar.

   >[!NOTE]
   >
   >El valor de la propiedad Tamaño en línea máximo del documento debe ser idéntico para AEM Forms en un entorno JEE y AEM Forms en el paquete OSGi incluido en AEM Forms en un entorno JEE. Estos pasos actualizaron el valor solo para AEM Forms en el entorno JEE y no para AEM Forms en el paquete OSGi incluido AEM Forms en el entorno JEE.

1. Reinicie el servidor de aplicaciones con la siguiente propiedad del sistema:

   com.adobe.idp.defaultDocumentMaxInlineSize=`[value specified in Step 2]`

   >[!NOTE]
   >
   >La propiedad del sistema mencionada anteriormente anula el valor de la propiedad Tamaño en línea máximo del documento establecida para AEM Forms en el entorno JEE y AEM Forms en el paquete OSGi incluido AEM Forms en el entorno JEE.

>[!NOTE]
>
>El tamaño máximo predeterminado en línea es de 65536 bytes.

### Tamaño máximo de pila de JVM {#jvm-maximum-heap-size}

Un aumento en el tamaño máximo en línea requiere más memoria para almacenar los documentos serializados. Por lo tanto, generalmente también requiere un aumento en el tamaño máximo de pila de JVM.

Un sistema muy cargado que procesa muchos documentos puede saturar rápidamente la memoria de pila de JVM. Para evitar un OutOfMemoryError, aumente el tamaño máximo de la pila de JVM en una cantidad correspondiente al tamaño de los documentos en línea multiplicado por el número de documentos que se ejecutan normalmente en un momento determinado.

Aumento del tamaño máximo de la pila de JVM = (tamaño de documentos en línea) x (número medio de documentos procesados).

**Cálculo del tamaño máximo de pila de JVM**

En este ejemplo, el montón máximo de JVM actual está establecido en 512 MB y el tamaño máximo en línea es de 64 KB. El servidor debe configurarse para el escenario en el que se ejecutan 10 trabajos simultáneamente y cada trabajo tiene 9 archivos de entrada y 1 archivo de resultado (un total de 10 archivos por trabajo y 100 archivos procesados simultáneamente). Todos los archivos tienen un tamaño inferior a 512 KB.

Para almacenar todos los archivos en línea, establezca el tamaño máximo en línea de al menos 512 KB.

El aumento requerido en el tamaño máximo de pila de JVM se calcula mediante la siguiente ecuación:

(512 KB) x (100) = 51200 KB o 50 MB

El tamaño máximo de pila de JVM debe aumentarse en 50 MB para un total de 562 MB.

**Considerando la fragmentación de la pila**

Establecer el tamaño de los documentos en línea en valores grandes aumenta el riesgo de OutOfMemoryError en los sistemas propensos a la fragmentación de la pila. Para almacenar un documento en línea, la memoria de pila de JVM debe tener suficiente espacio contiguo. Algunos sistemas operativos, JVM y algoritmos de recolección de elementos no utilizados son propensos a la fragmentación de la pila. La fragmentación reduce la cantidad de espacio de pila contiguo y puede provocar un OutOfMemoryError incluso cuando existe suficiente espacio libre total.

Por ejemplo, las operaciones anteriores en el servidor de aplicaciones dejaban el montón JVM en un estado fragmentado y el recolector de elementos no utilizados no puede compactar el montón lo suficiente como para recuperar grandes bloques de espacio libre. OutOfMemoryError puede producirse aunque el tamaño máximo de pila de JVM se haya ajustado para un aumento del tamaño máximo en línea.

Para tener en cuenta la fragmentación de la pila, el tamaño del documento en línea no debe ser superior al 0,1 % del tamaño total de la pila. Por ejemplo, un tamaño máximo de pila de JVM de 512 MB puede admitir un tamaño máximo en línea de 512 MB x 0,001 = 0,512 MB o 512 KB.

## Mejoras del servidor de aplicaciones WebSphere {#websphere-application-server-enhancements}

En esta sección se describen las opciones específicas de un entorno de servidor de aplicaciones WebSphere.

### Aumento de la memoria máxima asignada a la JVM {#increasing-the-maximum-memory-allocated-to-the-jvm}

Si está ejecutando el Administrador de configuración o intentando generar el código de implementación de Enterprise JavaBeans (EJB) mediante la utilidad de línea de comandos *ejbdeploy* y se produce un error OutOfMemory (Memoria insuficiente), aumente la cantidad de memoria asignada a JVM.

1. Edite el script ejbdeploy en el directorio *[appserver root]*/deploytool/itp/:

   * (Windows) `ejbdeploy.bat`
   * (Linux y UNIX) `ejbdeploy.sh`

1. Busque el parámetro `-Xmx256M` y cámbielo por un valor más alto, como `-Xmx1024M`.
1. Guarde el archivo.
1. Ejecute el comando `ejbdeploy` o vuelva a implementar mediante el Administrador de configuración.

## Mejora del rendimiento de Windows Server 2003 con LDAP {#improving-windows-server-2003-performance-with-ldap}

Este contenido describe la configuración específica de un entorno de sistema operativo Microsoft Windows Server 2003.

El uso de la agrupación de conexiones en la conexión de búsqueda puede reducir el número de puertos necesarios hasta en un 50 %. Esto se debe a que esa conexión siempre utiliza las mismas credenciales para un dominio determinado y el contexto y los objetos relacionados se cierran explícitamente.

### Configurar el servidor de Windows para la agrupación de conexiones {#configure-your-windows-server-for-connection-pooling}

1. Haga clic en Inicio > Ejecutar para iniciar el editor del Registro y, en el cuadro Abrir, escriba `regedit` y haga clic en Aceptar.
1. Ir a la clave del Registro `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters`
1. En el panel derecho del editor del Registro, busque el nombre del valor TcpTimedWaitDelay. Si el nombre no aparece, seleccione Edición > Nuevo > Valor DWORD en la barra de menús para agregar el nombre.
1. En el cuadro Nombre, escriba `TcpTimedWaitDelay`

   >[!NOTE]
   >
   >Si no ve un cursor parpadeante y `New Value #` dentro del cuadro, haga clic con el botón secundario en el panel derecho, seleccione Cambiar nombre y, en el cuadro Nombre, escriba `TcpTimedWaitDelay`*.*

1. Repita el paso 4 para los nombres de valor MaxUserPort, MaxHashTableSize y MaxFreeTcbs.
1. Haga doble clic dentro del panel derecho para establecer el valor de TcpTimedWaitDelay. En Base, seleccione Decimal y, en el cuadro Valor, escriba `30`.
1. Haga doble clic dentro del panel derecho para establecer el valor de MaxUserPort. En Base, seleccione Decimal y, en el cuadro Valor, escriba `65534`.
1. Haga doble clic dentro del panel derecho para establecer el valor de MaxHashTableSize. En Base, seleccione Decimal y, en el cuadro Valor, escriba `65536`.
1. Haga doble clic dentro del panel derecho para establecer el valor de MaxFreeTcbs. En Base, seleccione Decimal y, en el cuadro Valor, escriba `16000`.

>[!NOTE]
>
>Pueden producirse problemas graves si modifica incorrectamente el Registro mediante el Editor del Registro o mediante otro método. Estos problemas pueden requerir que vuelva a instalar el sistema operativo. Modifique el registro bajo su propia responsabilidad.
