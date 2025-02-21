---
title: Migrar recursos y documentos de AEM Forms
description: La utilidad de migración permite migrar recursos y documentos de Adobe Experience Manager (AEM) Forms desde AEM 6.3 Forms o versiones anteriores a AEM 6.4 Forms.
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ac26c0163309b6cb6c0cfde2098a8cc05955d03f
workflow-type: tm+mt
source-wordcount: '1723'
ht-degree: 53%

---

# Migrar recursos y documentos de AEM Forms{#migrate-aem-forms-assets-and-documents}

La utilidad de migración convierte los [recursos adaptables de Forms](../../forms/using/introduction-forms-authoring.md), las [configuraciones en la nube](/help/sites-developing/extending-cloud-config.md) y los [recursos de Administración de correspondencia](/help/forms/using/cm-overview.md) del formato utilizado en versiones anteriores al formato utilizado en Adobe Experience Manager (AEM) 6.5 Forms. Al ejecutar la utilidad de migración, se migran los siguientes elementos:

* Componentes personalizados para formularios adaptables
* Plantillas de formularios adaptables y Administración de correspondencia
* Configuraciones en la nube
* Recursos de Administración de correspondencia y formularios adaptables

>[!NOTE]
>
>Si hay una actualización fuera del sitio, para los recursos de Administración de correspondencia, puede ejecutar la migración cada vez que importe los recursos. Para realizar una migración de Administración de correspondencia, debe tener instalado el Paquete de compatibilidad de Forms.

## Método de migración {#approach-to-migration}

Puede [actualizar](../../forms/using/upgrade.md) a la versión más reciente de AEM Forms 6.5 desde AEM Forms 6.4, 6.3 o 6.2, o una instalación nueva. Dependiendo de si ha actualizado la instalación anterior o si ha realizado una instalación nueva, debe realizar una de las siguientes acciones:

**Si hay una actualización local**

Si ha realizado una actualización in situ, la instancia actualizada ya contiene los recursos y los documentos. Sin embargo, para poder usar los recursos y los documentos, debe instalar el [paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) (incluye el paquete de compatibilidad de Administración de correspondencia)

A continuación, debe actualizar los recursos y los documentos al [ejecutar la utilidad de migración](#runningmigrationutility).

**Si hay una instalación fuera del sitio**

Si se trata de una instalación fuera del sitio (nueva), para poder usar los recursos y documentos, debe instalar el [paquete de compatibilidad de AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) (incluye el paquete de compatibilidad de Administración de correspondencia).

A continuación, debe importar el paquete de recursos (zip o cmp) en la nueva configuración y, después, actualizar los recursos y los documentos [ejecutando la utilidad de migración](#runningmigrationutility). Adobe recomienda crear recursos en la nueva configuración solo después de ejecutar la utilidad de migración.

Debido a [cambios relacionados con la compatibilidad con versiones anteriores](/help/sites-deploying/backward-compatibility.md), las ubicaciones de algunas carpetas en el repositorio crx se cambian. Exportar e importar manualmente dependencias (bibliotecas y recursos personalizados) de la configuración anterior a un entorno nuevo.

## Antes de continuar con la migración {#prerequisites}

Para los recursos de Administración de correspondencia:

* En el caso de los recursos importados de la plataforma anterior, se agrega una propiedad, **fd:version=1.0**.
* A partir de AEM 6.1 Forms, los comentarios no están disponibles de forma predeterminada. Los comentarios que se agregaron anteriormente están disponibles en los recursos, pero no son visibles en la interfaz automáticamente. Personalice la propiedad extendedProperties en la interfaz de usuario de AEM Forms para que los comentarios sean visibles.
* En algunas versiones anteriores, como LiveCycle ES4, el texto se editaba con RichTextEditor de Flex, pero desde AEM 6.1 Forms, se utiliza un editor HTML. Debido a esta renderización y al aspecto de las fuentes, los tamaños y los márgenes de fuente pueden diferir de las versiones anteriores en la interfaz de usuario del Autor. Sin embargo, las cartas tienen el mismo aspecto cuando se representan.
* Las listas de los módulos de texto se han mejorado, y ahora se procesan de forma diferente. Es posible que haya diferencias visuales. Adobe recomienda procesar y ver las cartas en las que utiliza listas en módulos de texto.
* Dado que los módulos de contenido de imagen se convierten en recursos DAM, y que los diseños y los fragmentos se añaden a los formularios durante la migración, la propiedad Updated By de estos módulos cambia a admin.
* El historial de versiones de los recursos no se migra y no está disponible después de la migración. El historial de versiones posterior a la migración se conserva.
* El estado Listo para publicación está obsoleto desde AEM Forms 6.1, por lo que todos los recursos con este estado se cambian al estado Modificado.
* Dado que la interfaz de usuario se ha actualizado en AEM Forms 6.3, los pasos para realizar las personalizaciones también son diferentes. Vuelva a realizar la personalización si está migrando desde una versión anterior a la 6.3.
* Los fragmentos de diseño se mueven de `/content/apps/cm/layouts/fragmentlayouts/1001` a `/content/apps/cm/modules/fragmentlayouts`. La referencia del diccionario de datos en los recursos muestra la ruta del diccionario de datos en lugar de su nombre.
* Se deben reajustar los espacios de tabulación que se utilizan para la alineación en los módulos de texto. Para obtener más información, consulte [Administración de correspondencia - Use el espaciado del tabulador para organizar el texto](https://helpx.adobe.com/es/aem-forms/kb/cm-tab-spacing-limitations.html).
* Las configuraciones del Compositor de recursos cambian a las configuraciones de Administración de correspondencia.
* Los recursos se mueven a carpetas con nombres como Existing Text y Existing List.

## Uso de la utilidad de migración {#using-the-migration-utility}

### Ejecución de la utilidad de migración {#runningmigrationutility}

Ejecute la utilidad de migración antes de cambiar en los recursos o crear recursos. Adobe recomienda no ejecutar la utilidad después de realizar cambios o crear recursos. Asegúrese de que la interfaz de usuario de Administración de correspondencia o de los recursos de formularios adaptables no esté abierta mientras se esté ejecutando el proceso de migración.

Cuando ejecuta la utilidad de migración por primera vez, se crea un registro con la siguiente ruta y nombre: `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. Este registro sigue actualizándose con la información de migración de Administración de correspondencia y los formularios adaptables, como la transferencia de recursos.

>[!NOTE]
>
>Antes de ejecutar la utilidad de migración, asegúrese de haber realizado una copia de seguridad del repositorio CRX.

1. En una sesión del explorador, inicie sesión en la instancia de autor de AEM como administrador.

1. Abra la siguiente URL en el explorador:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   El explorador muestra cuatro opciones:

   * Migración de recursos de AEM Forms
   * Migración de componentes de formulario adaptable personalizados
   * Migración de plantillas de formulario adaptable
   * Migración de configuraciones en la nube de AEM Forms

1. Para realizar la migración, realice los siguientes pasos:

   * Para migrar **recursos**, seleccione Migración de AEM Forms Assets y, en la siguiente pantalla, seleccione **Iniciar migración**. Se migrarán los siguiente elementos:

      * Formularios adaptables
      * Fragmentos de documento
      * Temas
      * Cartas
      * Diccionarios de datos

   >[!NOTE]
   >
   >Durante la migración de recursos, puede encontrar mensajes de advertencia como &quot;Se ha detectado un conflicto entre...&quot;. Estos mensajes indican que no se han podido migrar las reglas de algunos de los componentes de los formularios adaptables. Por ejemplo, si el componente tenía un evento con reglas y scripts, si las reglas se aplican después de uno de los scripts, no se migran ninguna de las reglas del componente. Puede [migrar estas reglas abriendo el Editor de reglas](#migrate-rules) durante la creación de los formularios adaptables.

   * Para migrar componentes de formulario adaptable personalizados, seleccione **Migración de componentes personalizados de Forms adaptable** y, en la página Migración de componentes personalizados, seleccione **Iniciar migración**. Se migrarán los siguiente elementos:

      * Componentes personalizados escritos para formularios adaptables
      * Superposiciones de componentes, si las hay.

   * Para migrar plantillas de formulario adaptable, seleccione **Migración de plantillas de Forms adaptable** y, en la página Migración de componentes personalizados, seleccione **Iniciar migración**. Se migrarán los siguiente elementos:

      * Plantillas de formulario adaptable creadas en `/apps` o `/conf` con el Editor de plantillas de AEM.

   * Migre los servicios de configuración de AEM Forms Cloud para utilizar el nuevo paradigma de servicios en la nube sensibles al contexto, que incluye la interfaz de usuario táctil (en `/conf`). Cuando migre los servicios de configuración de AEM Forms Cloud, los servicios en la nube de `/etc` se mueven a `/conf`. Si no tiene personalizaciones de servicios en la nube que dependan de rutas heredadas (`/etc`), Adobe recomienda ejecutar la utilidad de migración después de actualizar a la versión 6.5; usar la interfaz de usuario táctil de la configuración en la nube para cualquier trabajo posterior. Si tiene personalizaciones de servicios en la nube existentes, continúe usando la IU clásica en la configuración actualizada hasta que las personalizaciones se actualicen para que se alineen con las rutas migradas (`/conf`) y luego ejecute la utilidad de migración.

   Para migrar **servicios en la nube de AEM Forms**, que incluyen lo siguiente, seleccione Migración de configuración de AEM Forms Cloud (la migración de configuración en la nube es independiente del paquete de compatibilidad de AEMFD). Seleccione Migración de configuraciones de AEM Forms Cloud y, a continuación, en la página Migración de configuración, seleccione **Iniciar migración**:

   * Servicios en la nube del modelo de datos de formulario

      * Ruta de origen: `/etc/cloudservices/fdm`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/fdm`

   * Recaptcha

      * Ruta de origen: `/etc/cloudservices/recaptcha`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/recaptcha`

   * Adobe Sign

      * Ruta de origen: `/etc/cloudservices/echosign`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/echosign`

   * Servicios de nube de Typekit

      * Ruta de origen: `/etc/cloudservices/typekit`
      * Ruta de destino: `/conf/global/settings/cloudconfigs/typekit`

   La ventana del explorador muestra lo siguiente a medida que se produce el proceso de migración:

   * Cuando se actualizan los recursos: Assets se actualiza correctamente.
   * Cuando se complete la migración: Migración de recursos finalizada.

   Cuando se ejecuta, la utilidad de migración realiza las siguientes acciones:

   * **Añade las etiquetas a los recursos**: agrega la etiqueta “Administración de correspondencia : Recursos migrados” / “Formularios adaptables: Recursos migrados”. a los recursos migrados, de forma que los usuarios puedan identificar los recursos migrados. Al ejecutar la utilidad de migración, todos los recursos existentes en el sistema se marcan como Migrados.
   * **Genera etiquetas**: las categorías y subcategorías presentes en el sistema anterior se crean como etiquetas y, a continuación, estas etiquetas se asocian a los recursos relevantes de Administración de correspondencia en AEM. Por ejemplo, una categoría (Reclamaciones) y una subcategoría (Reclamaciones) de una plantilla de carta se generan como etiquetas.

1. Una vez que la utilidad de migración haya terminado de ejecutarse, continúe con las [tareas de mantenimiento](#housekeepingtasks).

#### Migración de reglas mediante el Editor de reglas {#migrate-rules}

Estos componentes se pueden migrar abriéndolos en el Editor de reglas desde el Editor de Forms adaptable.

* Para migrar reglas y scripts (no es necesario si se actualiza desde la versión 6.3) de componentes personalizados, seleccione Migración de componentes personalizados de Forms adaptable y, en la pantalla siguiente, seleccione Iniciar migración. Se migrarán los siguiente elementos:

   * Reglas y scripts creados con el Editor de reglas (6.1 FP1 y versiones posteriores)

   * Scripts creados con la pestaña Script en la IU de 6.1 y versiones anteriores

* Para migrar plantillas (no es necesario si se actualiza desde las versiones 6.3 y 6.4), seleccione Migración de plantillas de Forms adaptable y, en la pantalla siguiente, seleccione Iniciar migración. Se migrarán los siguiente elementos:

   * Plantillas antiguas: las plantillas de formulario adaptable creadas en /apps con AEM 6.1 Forms o versiones anteriores. Eso incluye los scripts definidos en los componentes de plantilla.

   * Nuevas plantillas: las plantillas de formulario adaptable creadas con el editor de plantillas en `/conf`. Eso incluye la migración de reglas y scripts creados con el Editor de reglas.

### Tareas de mantenimiento después de ejecutar la utilidad de migración. {#housekeepingtasks}

Después de ejecutar la utilidad de migración, debe encargarse de las siguientes tareas de mantenimiento:

1. Asegúrese de que la versión XFA de los diseños y los diseños de fragmento sea la 3.3 o posterior. Si utiliza diseños y diseños de fragmento de una versión anterior, es posible que se produzcan problemas al procesar la carta. Para actualizar una versión de un XFA anterior a la versión más reciente, complete los siguientes pasos:

   1. [Descargue el XFA como archivo zip](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) desde la interfaz de usuario de Forms.
   1. Extraiga el archivo.
   1. Abra el archivo XFA en la última versión de Designer y guárdelo. El XFA se actualiza a la versión más reciente.
   1. Cargue el XFA en la interfaz de usuario de Forms.

1. Publique todos los recursos publicados en el sistema anterior antes de la migración. La utilidad de migración actualiza los recursos solo en la instancia de autor. Para actualizar los recursos en las instancias de publicación, debe publicarlos.

1. En AEM Forms 6.4 y 6.5, se cambian algunos derechos de los grupos forms users. Si desea que cualquiera de los usuarios pueda cargar XDP y Forms adaptable que contengan scripts o utilizar un editor de código, debe agregarlos al grupo forms-power-users. Del mismo modo, los autores de plantillas ya no pueden utilizar el editor de código del Editor de reglas. Para que los usuarios puedan utilizar un editor de código, agréguelos al grupo af-template-script-writers.