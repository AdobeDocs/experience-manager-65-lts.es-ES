---
title: Reutilización de recursos mediante MSM
description: Utilice recursos en varias páginas o carpetas que se deriven de recursos principales y estén vinculadas a ellos. Los recursos permanecen sincronizados con una copia principal y, con unos pocos clics, reciben las actualizaciones de los recursos principales.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 29365a8a-7d29-41b2-9a54-d12fe802f6ed
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '3261'
ht-degree: 9%

---

# Reutilizar recursos usando MSM para [!DNL Assets] {#reuse-assets-using-msm-for-assets}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/reuse-assets-using-msm.html?lang=es) |
| AEM 6.5 | Este artículo |

La funcionalidad Administrador de varios sitios (MSM) en [!DNL Adobe Experience Manager] permite a los usuarios reutilizar contenido creado una vez y reutilizado en varias ubicaciones web. Lo mismo está disponible para los recursos digitales que MSM para la funcionalidad [!DNL Assets]. Con MSM para [!DNL Assets], puede:

* Cree recursos una vez y luego haga copias de estos para reutilizarlos en otras áreas del sitio.
* Mantenga varias copias en sincronización y actualice la copia principal original una vez para insertar los cambios en las copias secundarias.
* Realice cambios locales suspendiendo temporal o permanentemente la vinculación entre los recursos principales y secundarios.

## Comprender las ventajas y los conceptos {#concepts}

### Cómo funciona y sus ventajas {#how-it-works-and-the-benefits}

Para comprender los escenarios de uso para reutilizar el mismo contenido (texto y recursos) en varias ubicaciones web, consulte [posibles escenarios de MSM](/help/sites-administering/msm.md). [!DNL Experience Manager] mantiene un vínculo entre el recurso original y sus copias vinculadas, denominado Live Copies (LC). La vinculación mantenida permite insertar cambios centralizados en muchas Live Copies. Esto permite realizar actualizaciones más rápidas, pero elimina las limitaciones de administrar copias duplicadas. La propagación de cambios está libre de errores y centralizada. La funcionalidad permite espacio para actualizaciones que se limitan a copias en directo seleccionadas. Los usuarios pueden desasociar el vínculo, es decir, interrumpir la herencia, y realizar ediciones locales que no se sobrescriban la próxima vez que se actualice la copia principal y se implementen los cambios. La desasociación se puede realizar para algunos campos de metadatos seleccionados o para un recurso completo. Permite la flexibilidad para actualizar localmente los recursos que se heredan originalmente de una copia principal.

MSM mantiene una relación activa entre el recurso de origen y sus Live Copies para lo siguiente:

* Los cambios en los recursos de origen también se aplican (despliegan) a las Live Copies, es decir, las Live Copies se sincronizan con el origen.
* Puede actualizar las Live Copies suspendiendo la relación activa o eliminando la herencia para algunos campos limitados. Las modificaciones en el origen ya no se aplican a la Live Copy.

### Glosario de MSM para términos de [!DNL Assets] {#glossary}

**Source:** Los recursos o carpetas originales. Copia principal de la que se derivan Live Copies.

**Live Copy:** La copia de los recursos o carpetas de origen que están sincronizados con su origen. Live Copies puede ser una fuente de Live Copies adicionales. Consulte cómo crear LC.

**Herencia:** Un vínculo o referencia entre un recurso o carpeta de Live Copy y su origen que el sistema usa para recordar dónde enviar las actualizaciones. La herencia existe a nivel granular para los campos de metadatos. La herencia se puede eliminar para campos de metadatos selectivos al tiempo que se conserva la relación activa entre el origen y su Live Copy.

**Despliegue:** Una acción que inserta las modificaciones realizadas en el origen descendente en sus Live Copies. Es posible actualizar una o más Live Copies de una sola vez mediante la acción de despliegue. Consulte Despliegue.

**Configuración de despliegue:** Reglas que determinan qué propiedades se sincronizan, cómo y cuándo. Estas configuraciones se aplican al crear Live Copies, se pueden editar más adelante y un elemento secundario puede heredar la configuración de despliegue de su recurso principal. Para MSM de [!DNL Assets], use solamente la configuración de despliegue estándar. Las otras configuraciones de despliegue no están disponibles para MSM para [!DNL Assets].

**Sincronizar:** Otra acción, además del despliegue, que aporta paridad entre el origen y su Live Copy al enviar las actualizaciones del origen a Live Copies. Se inicia una sincronización para una Live Copy determinada y la acción extrae los cambios del origen. Con esta acción, solo es posible actualizar una de las Live Copies. Consulte Acción de sincronización.

**Suspender:** Quite temporalmente la relación activa entre una Live Copy y su recurso o carpeta de origen. Puede reanudar la relación. Consulte acción de suspensión.

**Reanudar:** Reanudar la relación activa para que una Live Copy vuelva a recibir las actualizaciones del origen. Consulte Acción de reanudar.

**Restablecer:** La acción Restablecer vuelve a convertir la Live Copy en una réplica del origen al sobrescribir los cambios locales. También elimina las cancelaciones de herencia y restablece la herencia en todos los campos de metadatos. Para realizar modificaciones locales en el futuro, debe cancelar de nuevo la herencia de campos específicos. Consulte modificaciones locales de la LC.

**Desasociar:** quite de forma irrevocable la relación activa de un recurso o una carpeta de Live Copy. Después de la acción de desasociar, las Live Copies nunca podrán recibir actualizaciones del origen y dejarán de ser una Live Copy. Consulte Eliminar relación.

## Crear una Live Copy de un recurso {#createlc}

Para crear Live Copy a partir de uno o varios recursos o carpetas de origen, siga uno de estos procedimientos:

* Método 1: seleccione los recursos de origen y haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]** en la barra de herramientas de la parte superior.
* Método 2: en la interfaz de usuario de [!DNL Experience Manager], haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]** en la esquina superior derecha de la interfaz.

Puede crear Live Copies de un recurso o una carpeta a la vez. Puede crear Live Copies que se deriven de un recurso o una carpeta que sea una Live Copy en sí. Los fragmentos de contenido (CF) no son compatibles con el caso de uso. Al intentar crear sus Live Copies, los CF se copian tal cual sin ninguna relación. Los CF copiados son una instantánea en el tiempo y no se actualiza cuando se actualizan los CF originales.

Para crear Live Copies mediante el primer método, siga estos pasos:

1. Seleccione los recursos o carpetas de origen. En la barra de herramientas, haz clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]**.

   ![Crear Live Copy desde la interfaz [!DNL Experience Manager]](assets/create_lc1.png)

   *Figura: Crear Live Copy desde la interfaz [!DNL Experience Manager].*

1. Seleccione una carpeta de destino. Haga clic en **[!UICONTROL Siguiente]**.
1. Proporcione un título y un nombre. Assets no tiene elementos secundarios. Al crear una Live Copy de carpetas, puede elegir incluir o excluir elementos secundarios.
1. Seleccione una configuración de despliegue. Haga clic en **[!UICONTROL Crear]**.

Para crear Live Copies mediante el segundo método, siga estos pasos:

1. En la interfaz [!DNL Experience Manager], en la esquina superior derecha, haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Live Copy]**.

   ![Crear Live Copy desde la interfaz [!DNL Experience Manager]](assets/create_lc2.png)

   *Figura: Crear Live Copy desde la interfaz [!DNL Experience Manager].*

1. Seleccione el recurso o la carpeta de origen. Haga clic en **[!UICONTROL Siguiente]**.
1. Seleccione la carpeta de destino. Haga clic en **[!UICONTROL Siguiente]**.
1. Proporcione un título y un nombre. Assets no tiene elementos secundarios. Al crear una Live Copy de carpetas, puede elegir incluir o excluir elementos secundarios.
1. Seleccione una configuración de despliegue. Haga clic en **[!UICONTROL Crear]**.

>[!NOTE]
>
>Cuando se mueve un origen o una Live Copy, las relaciones se conservan. Cuando se elimina una Live Copy, se eliminan las relaciones.

## Ver varias propiedades y estados de origen y Live Copy {#properties}

Puede ver la información y los estados relacionados con MSM de Live Copy, como la relación, la sincronización, los despliegues y mucho más, en las distintas áreas de la interfaz de usuario de [!DNL Experience Manager].

Los dos métodos siguientes funcionan para recursos y carpetas:

* Seleccione el recurso de Live Copy y busque la información en su página Propiedades.
* Seleccione la carpeta de origen y busque la información detallada de cada Live Copy en [!UICONTROL Live Copy Console].

>[!TIP]
>
>Para comprobar el estado de algunas Live Copies independientes, use el primer método para comprobar la página **[!UICONTROL Propiedades]**. Para comprobar los estados de muchas Live Copies, use el segundo método para comprobar la página **[!UICONTROL Estado de relación]**.

### Información y estado de una Live Copy {#statuslcasset}

Para comprobar la información y los estados de un recurso de Live Copy o una carpeta, siga estos pasos.

1. Seleccione un recurso de Live Copy o una carpeta. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede usar el método abreviado de teclado `p`.
1. Haga clic en **[!UICONTROL Live Copy]**. Puede comprobar la ruta del origen, el estado de suspensión, el estado de sincronización, la fecha del último despliegue y el usuario que realizó el último.

   ![La información y los estados de Live Copy se muestran en una consola en Propiedades](assets/lcfolder_info_properties.png)

   *Imagen: información y estados de Live Copy.*

1. Puede habilitar o deshabilitar si los recursos secundarios toman prestada la configuración de Live Copy.

1. Puede elegir la opción para que Live Copy herede la configuración de despliegue del elemento principal o cambie la configuración.

### Información y estados de todas las Live Copies de una carpeta {#status-lc-folder}

[!DNL Experience Manager] proporciona una consola para comprobar los estados de todas las Live Copies de una carpeta de origen. Esta consola muestra el estado de todos los recursos secundarios.

1. Seleccione una carpeta de origen. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede usar el método abreviado de teclado `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Para abrir la consola, haga clic en **[!UICONTROL Descripción general de Live Copy]**. Este tablero proporciona un estado de nivel superior de todos los recursos secundarios.

   ![Ver los estados de Live Copies en la consola Live Copy del origen](assets/livecopy-statuses.png)

   *Imagen: vea los estados de Live Copies en la [!UICONTROL consola de Live Copy] del origen.*

1. Para ver la información detallada sobre cada recurso en la carpeta Live Copy, seleccione un recurso y haga clic en **[!UICONTROL Estado de relación]** en la barra de herramientas.

   ![Información detallada y estado de un recurso secundario de Live Copy en una carpeta](assets/livecopy_relationship_status.png)

   Información detallada y estado de un recurso secundario de Live Copy en una carpeta

>[!TIP]
>
>Puede ver rápidamente los estados de las Live Copies de otras carpetas sin tener que examinar demasiado. Cambie la carpeta desde la parte media superior de la interfaz de **[!UICONTROL Información general de Live Copy]**.

### Acciones rápidas del carril Referencias para el origen {#refrailsource}

Para un recurso o carpeta de origen, puede ver la siguiente información y realizar las siguientes acciones directamente desde el carril Referencias:

* Consulte las rutas de las Live Copies.
* Abra o muestre una Live Copy específica en la interfaz de usuario de [!DNL Experience Manager].
* Sincronizar las actualizaciones con una Live Copy específica.
* Suspender la relación o cambiar la configuración de despliegue de una Live Copy específica.
* Acceda a la consola de información general de live copy.

Seleccione el recurso o la carpeta de origen, abra el carril izquierdo y haga clic en **[!UICONTROL Referencias]**. Como alternativa, seleccione un recurso o una carpeta y utilice el método abreviado de teclado `Alt + 4`.

![Acciones e información disponible en el carril Referencias para el origen seleccionado](assets/referencerail_source.png)

*Figura: acciones e información disponible en el carril Referencias para el origen seleccionado.*

Para una Live Copy específica, haga clic en **[!UICONTROL Editar Live Copy]** para suspender la relación o cambiar la configuración de despliegue.

![Para una Live Copy específica, la opción para suspender la relación o cambiar la configuración de despliegue es accesible desde el carril Referencias cuando se selecciona el recurso de origen](assets/referencerail_editlc_options.png)

*Imagen: suspenda la relación o cambie la configuración de despliegue de una Live Copy específica.*

### Acciones rápidas del carril Referencias para la Live Copy {#ref-rail-lc}

Para un recurso o una carpeta de Live Copy, puede ver la siguiente información y realizar las siguientes acciones directamente desde el carril Referencias:

* Consulte la ruta de su origen.
* Abra o muestre una Live Copy específica en la interfaz de usuario de [!DNL Experience Manager].
* Despliegue las actualizaciones.

Seleccione una carpeta o un recurso de Live Copy, abra el carril izquierdo y haga clic en **[!UICONTROL Referencias]**. Como alternativa, seleccione un recurso o una carpeta y utilice el método abreviado de teclado `Alt + 4`.

![Acciones disponibles en el carril Referencias para la Live Copy seleccionada](assets/referencerail_livecopy.png)

*Figura: Acciones disponibles en el carril Referencias para la Live Copy seleccionada.*

## Propagación de modificaciones desde el origen a Live Copies {#rolloutsync}

Una vez modificado un origen, los cambios se pueden propagar a las Live Copies mediante una acción de sincronización o de despliegue. Para comprender la diferencia entre ambas acciones, vea [glosario](#glossary).

### Acción de despliegue {#rollout}

Puede iniciar una acción de despliegue desde el recurso de origen y actualizar todas las Live Copies o algunas.

1. Seleccione un recurso de Live Copy o una carpeta. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede usar el método abreviado de teclado `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Haga clic en **[!UICONTROL Despliegue]** en la barra de herramientas.
1. Seleccione las Live Copies que desee actualizar. Haga clic en **[!UICONTROL Despliegue]**.
1. Para desplegar las actualizaciones realizadas en los recursos secundarios, seleccione **[!UICONTROL Desplegar Source y todos los elementos secundarios]**.

   ![Desplegar las modificaciones del origen en algunas o en todas las Live Copies](assets/livecopy_rollout_page.png)

   *Imagen: despliegue las modificaciones del origen en algunas o en todas las Live Copies.*

>[!NOTE]
>
>Las modificaciones realizadas en un recurso de origen solo se implementan en las Live Copies directamente relacionadas. Si una Live Copy se deriva de otra Live Copy, las modificaciones no se implementan en la Live Copy derivada.

También puede iniciar una acción de despliegue desde el carril Referencias después de seleccionar una Live Copy específica. Para obtener más información, consulte [Acciones rápidas del carril Referencias para Live Copy](#ref-rail-lc). En este método de despliegue, solo se actualiza la Live Copy seleccionada y, opcionalmente, sus elementos secundarios.

![Desplegar las modificaciones del origen en la Live Copy seleccionada](assets/livecopy_rollout_dialog.png)

*Figura: Despliegue las modificaciones del origen en la Live Copy seleccionada.*

### Acerca de la acción sincronizar {#about-sync}

Una acción de sincronización extrae las modificaciones de un origen solo para la Live Copy seleccionada. La acción de sincronización respeta y mantiene las modificaciones locales realizadas después de cancelar la herencia. Las modificaciones locales no se sobrescriben y la herencia cancelada no se restablece. Puede iniciar una acción de sincronización de tres formas.

| Dónde en la interfaz [!DNL Experience Manager] | Cuándo y por qué utilizar | Cómo usar |
|---|---|---|
| [!UICONTROL Referencias] carril | Sincronice rápidamente cuando ya tenga seleccionado el origen. | Ver [acciones rápidas del carril Referencias para el origen](#refrailsource) |
| Barra de herramientas en la página [!UICONTROL Propiedades] | Inicie una sincronización cuando ya tenga abiertas las propiedades de Live Copy. | Ver [Sincronizar una Live Copy](#sync-lc) |
| [!UICONTROL Información general de Live Copy] consola | Sincronice rápidamente varios recursos (no necesariamente todos) cuando la carpeta de origen esté seleccionada o la consola [!UICONTROL Información general de Live Copy] ya esté abierta. La acción de sincronización se inicia para un recurso a la vez, pero es una forma más rápida de realizar la sincronización de varios recursos de una sola vez. | Ver [Acciones en varios recursos de una carpeta de Live Copy](#bulk-actions) |

### Sincronización de una Live Copy {#sync-lc}

Para iniciar una acción de sincronización, abra la página **[!UICONTROL Propiedades]** de una Live Copy, haga clic en **[!UICONTROL Live Copy]** y, a continuación, seleccione la acción que desee en la barra de herramientas.

Para ver los estados y la información relacionados con una acción de sincronización, consulte [Información y estado de una Live Copy](#statuslcasset) e [Información y estados de todas las Live Copy de una carpeta](#status-lc-folder).

![La acción Sincronizar extrae los cambios realizados en el origen](assets/livecopy_sync.png)

*Figura: la acción Sincronizar extrae los cambios realizados en el origen.*

>[!NOTE]
>
>Si la relación está suspendida, la acción de sincronización no está disponible en la barra de herramientas. Mientras que la acción de sincronización está disponible en el carril Referencias, las modificaciones no se propagan ni siquiera tras un despliegue correcto.

## Suspender y reanudar la relación {#suspend-resume}

Puede suspender temporalmente la relación para evitar que una Live Copy reciba modificaciones realizadas en el recurso o la carpeta de origen. La relación también se puede reanudar para que Live Copy empiece a recibir las modificaciones del origen.

Para suspender o reanudar, abra la página **[!UICONTROL Propiedades]** de una Live Copy, haga clic en **[!UICONTROL Live Copy]** y seleccione la acción que desee en la barra de herramientas.

También puede suspender o reanudar rápidamente las relaciones de varios recursos en una carpeta de Live Copy desde la consola **[!UICONTROL Información general de Live Copy]**. Consulte [Realizar acciones en varios recursos de las carpetas de Live Copy](#bulk-actions).

## Realización de modificaciones locales en una Live Copy {#local-mods}

Una Live Copy es una réplica del origen original cuando se crea. Los valores de metadatos de una Live Copy se heredan del origen. Los campos de metadatos mantienen individualmente la herencia con los campos respectivos del recurso de origen.

Sin embargo, tiene la flexibilidad de realizar modificaciones locales en una Live Copy para cambiar algunas propiedades seleccionadas. Para realizar modificaciones locales, cancele la herencia de la propiedad deseada. Cuando se cancela la herencia de uno o varios campos de metadatos, se conserva la relación activa del recurso y la herencia de los demás campos de metadatos. Cualquier sincronización o implementación no sobrescribe las modificaciones locales. Para ello, abra la página **[!UICONTROL Properties]** de un recurso de Live Copy y haga clic en la opción **[!UICONTROL cancel inheritance]** junto a un campo de metadatos.

Puede deshacer todas las modificaciones locales y revertir el recurso al estado de su origen. La acción Restablecer anula de forma irrevocable e instantánea todas las modificaciones locales y restablece la herencia en todos los campos de metadatos. Para volver, desde la página **[!UICONTROL Propiedades]** de un recurso de Live Copy, haga clic en **[!UICONTROL Restablecer]** en la barra de herramientas.

![La acción Restablecer sobrescribe las ediciones locales y trae la Live Copy en parte con su origen.](assets/livecopy_reset.png)

*Imagen: la acción Restablecer sobrescribe las ediciones locales y trae la Live Copy en parte con su origen.*

## Quitar relación activa {#detach}

Puede eliminar por completo la relación entre un origen y una Live Copy mediante la acción Desasociar. La Live Copy se convierte en un recurso o carpeta independiente después de desasociarse. Se muestra como un nuevo recurso en la interfaz [!DNL Experience Manager], inmediatamente después de la desasociación. Para separar una Live Copy de su origen, siga estos pasos.

1. Seleccione una carpeta o un recurso de Live Copy. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede usar el método abreviado de teclado `p`.

1. Haga clic en **[!UICONTROL Live Copy]**. Haga clic en **[!UICONTROL Desasociar]** en la barra de herramientas. Haga clic en **[!UICONTROL Desasociar]** del cuadro de diálogo presentado.

   ![La acción Desasociar elimina completamente la relación entre el origen y la Live Copy](assets/livecopy_detach.png)

   *Imagen: la acción de desasociar elimina por completo la relación entre el origen y la Live Copy.*

   >[!CAUTION]
   >
   >La relación se quita inmediatamente al hacer clic en **[!UICONTROL Desasociar]** del cuadro de diálogo. No puede deshacer la acción haciendo clic en **[!UICONTROL Cancelar]** en la página Propiedades.

También puede desasociar rápidamente varios recursos de una carpeta de Live Copy desde la consola **[!UICONTROL Información general de Live Copy]**. Consulte [Realizar acciones en varios recursos de las carpetas de Live Copy](#bulk-actions).

## Acciones masivas en una carpeta de Live Copy {#bulk-actions}

Si tiene varios recursos en una carpeta de Live Copy, iniciar acciones en cada recurso puede resultar tedioso. Puede iniciar rápidamente las acciones básicas en muchos recursos desde [!UICONTROL Live Copy Console]. Los métodos anteriores siguen funcionando para recursos individuales.

1. Seleccione una carpeta de origen. Haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas. También puede usar el método abreviado de teclado `p`.
1. Haga clic en **[!UICONTROL Origen de Live Copy]**. Para abrir la consola, haga clic en **[!UICONTROL Descripción general de Live Copy]**.
1. En este tablero, seleccione un recurso de Live Copy de una carpeta de Live Copy. Haga clic en las acciones que desee en la barra de herramientas. Las acciones disponibles son **[!UICONTROL Sincronizar]**, **[!UICONTROL Restablecer]**, **[!UICONTROL Suspender]** y **[!UICONTROL Desasociar]**. Puede iniciar rápidamente estas acciones en cualquier recurso de cualquier número de carpetas de Live Copy que estén en una relación activa con la carpeta de origen seleccionada.

   ![Actualice fácilmente muchos recursos en carpetas de Live Copy desde la consola de información general de Live Copy](assets/livecopyconsole_update_many_assets.png)

   *Imagen: actualice fácilmente muchos recursos en carpetas de Live Copy desde la consola [!UICONTROL Información general de Live Copy].*

## Impacto de las tareas de administración de recursos en Live Copies {#manage-assets}

Las Live Copies y fuentes son recursos o carpetas que se pueden administrar, en cierta medida, como recursos digitales. Algunas tareas de administración de recursos en [!DNL Experience Manager] tienen un impacto específico en las Live Copies.

* Al copiar una Live Copy, se crea un recurso de Live Copy con el mismo origen que la primera Live Copy.
* Cuando mueve un origen o su Live Copy, la relación dinámica se conserva.
* La acción de edición no funciona para los recursos de Live Copy. Si el origen de una Live Copy es una Live Copy en sí misma, la acción de edición no funciona para ella.
* La acción de desprotección no está disponible para los recursos de Live Copy.
* Para la carpeta de origen, está disponible la opción para crear tareas de revisión.
* Al ver la lista de recursos en la vista de lista y la vista de columna, un recurso o carpeta de Live Copy muestra &quot;Live Copy&quot; en relación con ella. Ayuda a identificar fácilmente las Live Copies de una carpeta.

## Comparar MSM para [!DNL Assets] y [!DNL Sites] {#comparison}

En más escenarios, MSM para [!DNL Assets] coincide con el comportamiento de MSM para la funcionalidad de Sites. Algunas diferencias clave que hay que tener en cuenta son:

* El modelo de MSM para [!DNL Sites] se llama origen de Live Copy en MSM para [!DNL Assets].
* En Sites, puede comparar un modelo y su Live Copy, pero no es posible en [!DNL Assets] comparar un origen con su Live Copy.
* No puede editar una Live Copy en [!DNL Assets].
* Los sitios generalmente tienen elementos secundarios, pero [!DNL Assets] no. La opción para incluir o excluir elementos secundarios no está presente al crear Live Copies de recursos individuales.
* MSM no admite la eliminación del paso de capítulos del asistente para crear sitio para [!DNL Assets].
* La configuración de los bloqueos de MSM en las propiedades de página (IU táctil) no se admite en MSM para [!DNL Assets].
* Para MSM de [!DNL Assets], use solamente la **[!UICONTROL configuración de despliegue estándar]**. Las otras configuraciones de despliegue no están disponibles para MSM para [!DNL Assets].

## Prácticas recomendadas {#best-practices}

Algunas prácticas recomendadas para MSM son las siguientes:

* Planifique las relaciones principal-secundario de los recursos y los flujos de contenido antes de iniciar la implementación.

## Limitaciones y problemas conocidos de MSM para [!DNL Assets] {#limitations}

A continuación se muestra una limitación de MSM para [!DNL Assets].

* Los fragmentos de contenido (CF) no son compatibles con el caso de uso. Al intentar crear sus Live Copies, los CF se copian tal cual sin ninguna relación. Los CF copiados son una instantánea en el tiempo y no se actualizan cuando se actualizan los CF originales.

* MSM no funciona con la reescritura de metadatos habilitada. Tras la reescritura, la herencia se interrumpe.
