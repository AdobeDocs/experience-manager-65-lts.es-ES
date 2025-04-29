---
title: Configurar OSGi
description: OSGi es un elemento fundamental de la pila tecnológica de Adobe Experience Manager (AEM). Se utiliza para controlar los paquetes compuestos de AEM y su configuración. Este artículo detalla cómo puede administrar los ajustes de configuración para estos paquetes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 3bf3ba2e-f5f2-428a-a1fc-36f885350f6b
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '1900'
ht-degree: 0%

---

# Configurar OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/) es un elemento fundamental en la pila de tecnología de Adobe Experience Manager (AEM). Se utiliza para controlar los paquetes compuestos de AEM y su configuración.

OSGi &quot;*proporciona las primitivas estandarizadas que permiten construir aplicaciones a partir de componentes pequeños, reutilizables y de colaboración. Estos componentes se pueden componer en una aplicación e implementarse*&quot;.

Al hacerlo, se puede administrar fácilmente los paquetes, ya que se pueden detener, instalar e iniciar individualmente. Las interdependencias se gestionan automáticamente. Cada componente OSGi (consulte la [especificación OSGi](https://docs.osgi.org/specification/)) está contenido en uno de los distintos paquetes.

Puede administrar los ajustes de configuración de estos paquetes mediante las siguientes opciones:

* usando la [consola web de Adobe CQ](#osgi-configuration-with-the-web-console)
* usando [archivos de configuración](#osgi-configuration-with-configuration-files)
* configurando [nodos de contenido (`sling:OsgiConfig`) en el repositorio](#osgi-configuration-in-the-repository)

Se puede usar cualquiera de los métodos aunque existen diferencias sutiles, principalmente en relación con [Modos de ejecución](/help/sites-deploying/configure-runmodes.md):

* [Consola web de Adobe CQ](#osgi-configuration-with-the-web-console)

   * La consola web es la interfaz estándar para la configuración de OSGi. Proporciona una interfaz de usuario para editar las distintas propiedades, donde es posible seleccionar valores de listas predefinidas.

     Como tal, es el método más fácil de usar.

   * Cualquier configuración realizada con la consola web se aplica inmediatamente y se aplica a la instancia actual, independientemente del modo de ejecución actual o de cualquier cambio posterior en el modo de ejecución.

* [archivos de configuración](#osgi-configuration-with-configuration-files)

   * Contiene la configuración definida en la consola web.
   * Se puede incluir en paquetes de contenido para usarlos en otras instancias.

* [content-nodes (sling:osgiConfig) en el repositorio](#osgi-configuration-in-the-repository)

   * Requiere una configuración manual con CRXDE Lite.
   * Debido a las convenciones de nomenclatura de los nodos `sling:OsgiConfig`, puede enlazar la configuración a un [modo de ejecución](/help/sites-deploying/configure-runmodes.md) específico. Incluso puede guardar configuraciones para más de un modo de ejecución en el mismo repositorio.
   * Las configuraciones adecuadas se aplican inmediatamente (según el modo de ejecución).

Sea cual sea el método que utilice, todos estos métodos de configuración:

* Asegúrese de que al copiar o replicar el contenido del repositorio se vuelven a crear configuraciones idénticas.
* Le permite retirar configuraciones a FileVault o Subversion; ya sea por seguridad o por más actualizaciones.
* Se puede guardar en paquetes para utilizarlos al configurar otras instancias.
* Permite realizar despliegues de configuración utilizando scripts para propagar los detalles de configuración.

>[!NOTE]
>
>Los detalles de ciertas opciones importantes se enumeran en [Opciones de configuración de OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configuración de OSGi con la consola web {#osgi-configuration-with-the-web-console}

La [consola web](/help/sites-deploying/web-console.md) de AEM proporciona una interfaz estandarizada para configurar los paquetes. La pestaña **Configuration** se usa para configurar los paquetes OSGi y, por lo tanto, es el mecanismo subyacente para configurar los parámetros del sistema de AEM.

Los cambios realizados se aplican inmediatamente a la configuración de OSGi correspondiente, no se requiere reiniciar.

>[!NOTE]
>
>Los cambios realizados en la consola web se guardarán en el repositorio como [archivos de configuración](#osgi-configuration-with-configuration-files). Estos archivos se pueden incluir en paquetes de contenido para reutilizarlos en instalaciones posteriores.

>[!NOTE]
>
>En la consola web, cualquier descripción que mencione la configuración predeterminada está relacionada con los valores predeterminados de Sling.
>
>Adobe Experience Manager tiene sus propios valores predeterminados y, por lo tanto, los valores predeterminados que se establecen podrían diferir de los valores predeterminados documentados en la consola.

Para actualizar una configuración con la consola web:

1. Para acceder a la ficha **Configuración** de la consola web, haga lo siguiente:

   * Abrir la consola web desde el vínculo del menú **Herramienta > Operaciones**. Después de iniciar sesión en la consola, puede utilizar el menú desplegable de:

     **OSGi >**

   * La dirección URL directa; por ejemplo:

     `http://localhost:4502/system/console/configMgr`

   Se muestra una lista.

1. Seleccione el paquete que desea configurar mediante:

   * haciendo clic en el icono **Editar** para ese paquete
   * haciendo clic en **Nombre** del paquete

1. Se abre un cuadro de diálogo. Aquí puede realizar las modificaciones necesarias. Por ejemplo, establezca el **Nivel de registro** en `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Las actualizaciones se guardan en el repositorio como [archivos de configuración](#osgi-configuration-with-configuration-files). Para localizar estos archivos posteriormente e incluirlos en un paquete de contenido para usarlos en otra instancia, por ejemplo, anote la identidad persistente ( `PID`).

1. Haga clic en **Guardar**.

   Los cambios se aplican inmediatamente a la configuración OSGi relevante del sistema en ejecución; no se requiere reiniciar.

   >[!NOTE]
   >
   >Ahora puede encontrar los [archivos de configuración](#osgi-configuration-with-configuration-files) relacionados. Por ejemplo, para incluir en un paquete de contenido para utilizarlo en otra instancia.

## Configuración de OSGi con archivos de configuración {#osgi-configuration-with-configuration-files}

Los cambios de configuración realizados mediante la consola web se mantienen en el repositorio como archivos de configuración ( `.config`) en:

`/apps`

Estos archivos se pueden incluir en paquetes de contenido y reutilizarse en otras instancias.

>[!NOTE]
>
>El formato de los archivos de configuración es específico; consulte la documentación de Sling Apache para obtener información sobre lo siguiente:
>* Detalles completos de [el modelo de aprovisionamiento de Apache Sling y Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>* Tutoriales y ejemplos de [obtención de recursos y propiedades en Sling](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html).
>
>Por este motivo, se recomienda crear y mantener el archivo de configuración realizando cambios reales en la consola web.

La consola web no muestra ninguna indicación de en qué parte del repositorio se han guardado los cambios, pero se pueden localizar fácilmente:

1. Cree el archivo de configuración [realizando un cambio inicial en la consola web](#osgi-configuration-with-the-web-console).
1. Abra CRXDE Lite.
1. En el menú **Herramientas**, seleccione **Consulta...** .
1. Para buscar el PID de la configuración que ha actualizado, envíe una consulta de **Tipo** `SQL`.

   Por ejemplo, **Apache Felix OSGi Management Console** tiene la identidad persistente (PID) de:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Por lo tanto, la consulta SQL podría ser:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. Se muestra el nodo del archivo de configuración.

   Para el ejemplo anterior:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Puede abrir este archivo para ver los cambios, pero para evitar errores de escritura, se recomienda realizar cambios reales con la consola.

1. Ahora puede crear un paquete de contenido que contenga este nodo y utilizarlo según sea necesario en las demás instancias.

## Configuración de OSGi en el repositorio {#osgi-configuration-in-the-repository}

Además de utilizar la consola web, también puede definir los detalles de configuración en el repositorio. Al hacerlo, puede configurar fácilmente los diferentes modos de ejecución.

Estas configuraciones se realizan creando `sling:OsgiConfig` nodos en el repositorio a los que el sistema hace referencia. Estos nodos reflejan las configuraciones de OSGi y se forma una interfaz de usuario para ellos. Para actualizar los datos de configuración, actualice las propiedades del nodo.

Si modifica los datos de configuración en el repositorio, los cambios se aplican inmediatamente a la configuración OSGi correspondiente. Es como si los cambios se hubieran realizado utilizando la consola web, con las comprobaciones de validación y coherencia adecuadas. Este flujo de trabajo también se aplica a la acción de copiar una configuración de `/libs/` a `/apps/`.

Como el mismo parámetro de configuración se encuentra en varios lugares, el sistema:

* busca todos los nodos de tipo `sling:OsgiConfig`
* filtros según el nombre del servicio
* filtros según el modo de ejecución


### Adición de una nueva configuración al repositorio {#adding-a-new-configuration-to-the-repository}

#### Lo que necesita saber {#what-you-need-to-know}

Para agregar una configuración al repositorio, debe saber lo siguiente:

1. La **identidad persistente** (PID) del servicio.

   Hacer referencia a **Configuraciones** en la consola web. El nombre se muestra en **Información de configuración** en la parte inferior de la página.

   Por ejemplo, `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. ¿Se requiere un [modo de ejecución](/help/sites-deploying/configure-runmodes.md) específico? Cree la carpeta:

   * `config` - para todos los modos de ejecución
   * `config.author` - para el entorno de creación
   * `config.publish` - para el entorno de publicación
   * `config.<run-mode>` - según corresponda

1. ¿Es necesaria una **configuración** o **configuración de fábrica**?
1. Los parámetros individuales que se van a configurar, incluidas las definiciones de parámetros existentes que se deben volver a crear.

   Haga referencia al campo de parámetro individual en la consola web. El nombre se muestra entre corchetes para cada parámetro.

   Por ejemplo, cree una propiedad
   `versionmanager.createVersionOnActivation` para configurar **Crear versión en la activación**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. ¿Existe una configuración en `/libs`? Para enumerar todas las configuraciones en su instancia, utilice la herramienta **Query** de CRXDE Lite para enviar la siguiente consulta SQL:

   `select * from sling:OsgiConfig`

   Si es así, esta configuración se puede copiar en ` /apps/<yourProject>/` y luego personalizar en la nueva ubicación.

#### Creación de la configuración en el repositorio {#creating-the-configuration-in-the-repository}

Para agregar realmente la nueva configuración al repositorio:

1. Utilice CRXDE Lite para desplazarse a:

   ` /apps/<yourProject>`

1. Si no existe, cree la carpeta `config` ( `sling:Folder`):

   * `config` - aplicable a todos los modos de ejecución
   * `config.<run-mode>` - específico para un modo de ejecución en particular

1. En esta carpeta, cree un nodo:

   * Tipo: `sling:OsgiConfig`
   * Nombre: la identidad persistente (PID);

     por ejemplo, para el Administrador de versiones de AEM WCM, use `com.day.cq.wcm.core.impl.VersionManagerImpl`

   >[!NOTE]
   >
   >Al hacer una configuración de fábrica, anexe `~<identifier>` al nombre.
   >
   >Como en: `org.apache.sling.commons.log.LogManager.factory.config~<identifier>`
   >
   >Donde `<identifier>` se reemplaza por texto libre que usted (debe) escribe para identificar la instancia (no puede omitir esta información); por ejemplo:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config~MINE`

1. Para cada parámetro que desee configurar, cree una propiedad en este nodo:

   * Nombre: el nombre del parámetro como se muestra en la consola web; el nombre se muestra entre corchetes al final de la descripción del campo. Por ejemplo, para `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * Tipo: según corresponda.
   * Valor: según sea necesario.

   Solo debe crear propiedades para los parámetros que desea configurar; otros siguen tomando los valores predeterminados establecidos por AEM.

1. Guarde todos los cambios.

   Los cambios se aplican cuando se actualiza el nodo reiniciando el servicio (como con los cambios realizados en la consola web).

>[!CAUTION]
>
>No cambie nada en la ruta de acceso `/libs`.

>[!CAUTION]
>
>La ruta completa de una configuración debe ser correcta para que se lea al inicio.

## Detalles de configuración {#configuration-details}

### Orden de resolución al inicio {#resolution-order-at-startup}

Se utiliza el siguiente orden de prioridad:

1. Nodos de repositorio bajo `/apps/*/config...`. ya sea con tipo `sling:OsgiConfig` o archivos de propiedad.

1. Nodos del repositorio con tipo `sling:OsgiConfig` en `/libs/*/config...`. (definiciones listas para usar).

1. Cualquier `.config` archivo de `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. en el sistema de archivos local.

Una configuración genérica de `/libs` se puede ocultar con una configuración específica del proyecto de `/apps`.

### Orden de resolución en tiempo de ejecución {#resolution-order-at-runtime}

Los cambios de configuración realizados mientras el sistema se está ejecutando déclencheur una recarga con la configuración modificada.

A continuación, se aplica el siguiente orden de prioridad:

1. Modificar una configuración en la consola web tiene un efecto inmediato, ya que tiene prioridad durante la ejecución.
1. Modificar una configuración en `/apps` surte efecto inmediatamente.
1. Modificar una configuración en `/libs` surte efecto inmediatamente, a menos que esté enmascarada por una configuración en `/apps`.

### Resolución de varios modos de ejecución {#resolution-of-multiple-run-modes}

Para las configuraciones específicas del modo de ejecución, se pueden combinar varios modos de ejecución. Por ejemplo, puede crear carpetas de configuración con el siguiente estilo:

`/apps/*/config.<runmode1>.<runmode2>/`

Las configuraciones en estas carpetas se aplican si todos los modos de ejecución coinciden con un modo de ejecución definido al inicio.

Por ejemplo, si se inició una instancia con los modos de ejecución `author,dev,emea`, se aplican los nodos de configuración de `/apps/*/config.emea`, `/apps/*/config.author.dev/` y `/apps/*/config.author.emea.dev/`, mientras que no se aplican los nodos de configuración de `/apps/*/config.author.asean/` y `/config/author.dev.emea.noldap/`.

Si se aplican varias configuraciones para el mismo PID, se aplica la configuración con el número más alto de modos de ejecución coincidentes.

Por ejemplo, si se inició una instancia con los modos de ejecución `author,dev,emea`, y tanto `/apps/*/config.author/` como `/apps/*/config.emea.author/` definen una configuración para
`com.day.cq.wcm.core.impl.VersionManagerImpl`, se ha aplicado la configuración de `/apps/*/config.emea.author/`.

La granularidad de esta regla es de nivel PID.
No puede definir algunas propiedades para el mismo PID en `/apps/*/config.author/` y otras más específicas en `/apps/*/config.emea.author/` para el mismo PID.
La configuración con el número más alto de modos de ejecución coincidentes es efectiva para todo el PID.

### Configuraciones estándar {#standard-configurations}

Si alguna configuración estándar reside en `/libs`, no debe editarse directamente, sino copiarse en el área de aplicación ( `/apps`) antes de la personalización.

Para enumerar todos los nodos de configuración de la instancia, use la funcionalidad **Query** en CRXDE Lite para enviar la siguiente consulta SQL:

`select * from sling:OsgiConfig`

### Persistencia de configuración {#configuration-persistence}

* Si cambia una configuración a través de la consola web, (normalmente) se escribe en el repositorio en:

  `/apps/{somewhere}`

   * De forma predeterminada `{somewhere}` es `system/config`, por lo que la configuración se escribe en

     `/apps/system/config`

   * Sin embargo, si está editando una configuración que inicialmente provino de otra parte del repositorio: por ejemplo:

     /libs/foo/config/someconfig

     A continuación, la configuración actualizada se escribe en la ubicación original; por ejemplo:

     `/apps/foo/config/someconfig`

* La configuración que ha cambiado `admin` se guarda en `*.config` archivos en:

  ```
     /crx-quickstart/launchpad/config
  ```

   * Esta área son los datos privados del administrador de configuración de OSGi y contiene todos los detalles de configuración especificados por `admin`, independientemente de cómo hayan entrado al sistema.
   * Esta área es un detalle de implementación y nunca debe editar este directorio directamente.
   * Sin embargo, es útil conocer la ubicación de estos archivos de configuración para que se puedan realizar copias de seguridad, instalaciones múltiples o ambas:

      * Consola de administración de Apache Felix OSGi

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Repositorio de cliente de CRX Sling

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Nunca edite las carpetas o archivos en:
>
>`/crx-quickstart/launchpad/config`
