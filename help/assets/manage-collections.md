---
title: Administrar colecciones de recursos digitales
description: Conozca las tareas para administrar Colecciones de recursos, como crear, ver, eliminar, editar y descargar colecciones.
contentOwner: AG
mini-toc-levels: 1
role: User
feature: Collections,Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 14%

---

# Administrar colecciones {#managing-collections}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-collections.html?lang=en) |
| AEM 6.5 | Este artículo |

Una colección es un conjunto de recursos dentro de [!DNL Adobe Experience Manager Assets]. Utilice las colecciones para compartir recursos entre los usuarios. El conjunto puede ser una colección estática o dinámica basada en los resultados de búsqueda.

A diferencia de las carpetas, una colección puede incluir recursos de distintas ubicaciones. Puede compartir colecciones con varios usuarios a los que se les asignan diferentes niveles de privilegios, como ver, editar, etc.

Puede compartir varias colecciones con un usuario. Cada colección contiene referencias a recursos. La integridad referencial de los recursos se mantiene entre colecciones.

Las colecciones son de los siguientes tipos, según la forma en que intercalan los recursos:

* Colección que contiene una lista de referencia estática de recursos, carpetas y otras colecciones.

* Una colección inteligente que incluye recursos de forma dinámica en función de criterios de búsqueda.

## Acceso a la consola Colecciones {#navigating-the-collections-console}

Para abrir **[!UICONTROL Colecciones]**, en la interfaz de [!DNL Experience Manager], ve a **[!UICONTROL Assets]** > **[!UICONTROL Colecciones]**.

## Crear una colección {#creating-a-collection}

Puede crear una colección con [referencias estáticas](#creating-a-collection-with-static-references) o basada en un [filtro basado en criterios de búsqueda](#creating-a-smart-collection). También puede crear una colección a partir de una caja de luz.

### Crear una colección con referencias estáticas {#creating-a-collection-with-static-references}

Puede crear una colección con referencias estáticas; por ejemplo, una colección con referencias a recursos, carpetas, colecciones, conjuntos de giros y conjuntos de imágenes.

1. Vaya a la consola **[!UICONTROL Colecciones]**.
1. En la barra de herramientas, haga clic en **[!UICONTROL Crear]**.
1. En la página **[!UICONTROL Crear colección]**, escriba un título y una descripción opcional para la colección.
1. Agregue miembros a la colección y asigne los permisos correspondientes. Como alternativa, seleccione **[!UICONTROL Colección pública]** para permitir que todos los usuarios tengan acceso a la colección.

   >[!NOTE]
   >
   >Para permitir que los miembros compartan colecciones con otros usuarios, proporcione los permisos de lectura del grupo `dam-users` en la ruta `home/users`. Conceda permiso a los usuarios en la ubicación `/content/dam/collections` para que puedan ver las colecciones en las listas emergentes. Como alternativa, convierta al usuario en parte del grupo `dam-users`.

1. (Opcional) Agregue una imagen en miniatura para la colección.
1. Haga clic en **[!UICONTROL Crear]** y luego haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. En la consola Colecciones se abre una colección con el título y las propiedades especificados.

   >[!NOTE]
   >
   >[!DNL Experience Manager Assets] le permite crear tareas de revisión para una colección similar a la forma de crear tareas de revisión para una carpeta de recursos.

   Para agregar recursos a la colección, vaya a la interfaz de usuario [!DNL Assets]. Para obtener más información, consulte [Agregar recursos a una colección](#adding-assets-to-a-collection).

### Creación de colecciones mediante la Dropzone {#create-collections-using-dropzone}

Puede arrastrar recursos de la interfaz de usuario [!DNL Assets] a una colección. También puede crear una copia de una colección y arrastrar los recursos allí.

1. En la interfaz de usuario [!DNL Assets], seleccione los recursos que desee agregar a una colección.
1. Arrastre los recursos a la zona **[!UICONTROL Colocar en colección]**. También puede hacer clic en **[!UICONTROL Para la colección]** desde la barra de herramientas.

   ![drop_in_collection](assets/drop_in_collection.png)

1. En la página **[!UICONTROL Agregar a colección]**, haga clic en **[!UICONTROL Crear colección]** en la barra de herramientas.

   Si desea agregar los recursos a una colección existente, selecciónela en la página y haga clic en **[!UICONTROL Agregar]**. De forma predeterminada, se selecciona la colección con la fecha de actualización más reciente.

1. En el cuadro de diálogo **[!UICONTROL Crear nueva colección]**, indique un nombre para la colección. Si desea que todos los usuarios tengan acceso a la colección, seleccione **[!UICONTROL Colección pública]**.
1. Haga clic en **[!UICONTROL Continuar]** para crear la colección.

### Crear una colección inteligente {#creating-a-smart-collection}

Una colección inteligente utiliza un criterio de búsqueda para rellenar recursos de forma dinámica. Puede crear una colección inteligente utilizando sólo archivos y no carpetas o archivos y carpetas.

Para crear una colección inteligente, siga los pasos:

1. Vaya a la interfaz de usuario [!DNL Assets] y haga clic en buscar.

1. Escriba la palabra clave en el cuadro Omnisearch y seleccione `Enter`. Abra el panel Filtros y aplique un filtro de búsqueda.

1. En la lista **[!UICONTROL Archivos y carpetas]**, seleccione **[!UICONTROL Archivos]**.

   ![opciones_archivos](assets/files_option.png)

1. Haga clic en **[!UICONTROL Guardar colección inteligente]**.

1. Especifique un nombre para la colección. Seleccione **[!UICONTROL Público]** para agregar el grupo Usuarios de DAM con el rol de Visor a la colección inteligente.

   ![guardar_colección](assets/save_collection.png)

   >[!NOTE]
   >
   >Si selecciona **[!UICONTROL Público]**, la colección inteligente estará disponible para todos los que tengan la función de propietario después de crearla. Si cancela la opción **[!UICONTROL Public]**, el grupo de usuarios DAM ya no estará asociado a la colección inteligente.

1. Haga clic en **[!UICONTROL Guardar]** para crear la colección inteligente y, a continuación, cierre el cuadro de mensaje para completar el proceso.

   La nueva colección inteligente también se agrega a la lista **[!UICONTROL Búsquedas guardadas]**.

   ![lista_colecciones](assets/collection_listing.png)

   La etiqueta de la opción **[!UICONTROL Crear selección inteligente]** cambia a **[!UICONTROL Editar selección inteligente]**. Para editar la configuración de la colección inteligente, seleccione **[!UICONTROL Archivos]** en la lista **[!UICONTROL Archivos y carpetas]**. Haga clic en la opción **[!UICONTROL Editar selección inteligente]** ![editar colección inteligente](assets/do-not-localize/edit-smart-collection.png).

## Agregar recursos a una colección {#adding-assets-to-a-collection}

Puede agregar recursos a una colección que contenga una lista de recursos o carpetas a los que se hace referencia. Las colecciones inteligentes utilizan una consulta de búsqueda para rellenar recursos. Por lo tanto, las referencias estáticas a recursos y carpetas no son aplicables a ellos.

1. En la interfaz de usuario de [!DNL A]Assets, seleccione el recurso y haga clic en **[!UICONTROL Agregar a la colección]** ![agregar a la colección](assets/do-not-localize/add-to-collection.png) desde la barra de herramientas.
También puede arrastrar el recurso al área **[!UICONTROL Colocar en colección]** de la interfaz. Agregue los recursos cuando la etiqueta de la región cambie a **[!UICONTROL Colocar para agregar]**.

1. En la página **[!UICONTROL Agregar a colección]**, seleccione la colección a la que desea agregar el recurso.

1. Haga clic en **[!UICONTROL Agregar]** y cierre el mensaje de confirmación. El recurso se agrega a la colección.

## Edición de una colección inteligente {#editing-a-smart-collection}

Las colecciones inteligentes se crean guardando una búsqueda para que pueda modificar su contenido modificando los parámetros de búsqueda de [búsqueda guardada](#saved-searches).

1. En la interfaz de usuario [!DNL Assets], haga clic en la opción de búsqueda ![opción de búsqueda](assets/do-not-localize/search_icon.png) de la barra de herramientas.
1. Con el cursor en el cuadro Omnisearch, seleccione la clave `Return`.
1. En la interfaz [!DNL Experience Manager], abra el panel Filtros.
1. En la lista **[!UICONTROL Búsquedas guardadas]**, seleccione la colección inteligente que desee modificar. El panel Buscar aparecen los filtros configurados para la búsqueda guardada.

   ![select_smart_collection](assets/select_smart_collection.png)

1. En la lista **[!UICONTROL Archivos y carpetas]**, seleccione **[!UICONTROL Archivos]**.
1. Modifique uno o más filtros según sea necesario. Haga clic en **[!UICONTROL Editar colección inteligente]**.

   También puede editar el nombre de la colección inteligente.

   ![edit_smart_collection_dialog](assets/edit_smart_collectiondialog.png)

1. Haga clic en **[!UICONTROL Guardar]**. Aparecerá el cuadro de diálogo **[!UICONTROL Editar colección inteligente]**.
1. Haga clic en **[!UICONTROL Sobrescribir]** para reemplazar la colección inteligente original por la colección editada. También puede seleccionar **[!UICONTROL Guardar como]** para guardar la colección editada por separado.
1. En el cuadro de diálogo de confirmación, haga clic en **[!UICONTROL Guardar]** para completar el proceso.

## Ver y editar metadatos de colección {#view-edit-collection-metadata}

Los metadatos de la colección comprenden datos sobre la colección, incluidas las etiquetas añadidas.

1. En la consola [!UICONTROL Colecciones], seleccione una colección y haga clic en **[!UICONTROL Propiedades]** en la barra de herramientas.
1. En la página **[!UICONTROL Metadatos de la colección]**, consulte los metadatos de la colección desde las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]**.
1. Modifique los metadatos según sea necesario. Para guardar los cambios, haga clic en **[!UICONTROL Guardar y cerrar]** en la barra de herramientas.

## Edición masiva de metadatos de varias colecciones {#editing-collection-metadata-in-bulk}

Puede editar los metadatos de varias colecciones simultáneamente. Esta funcionalidad le ayuda a replicar rápidamente metadatos comunes en varias colecciones.

1. En la consola Colecciones, seleccione dos o más colecciones.
1. En la barra de herramientas, haga clic en **[!UICONTROL Propiedades]**.
1. En la página **[!UICONTROL Metadatos de la colección]**, edite los metadatos en las pestañas **[!UICONTROL Básico]** y **[!UICONTROL Avanzado]**, según sea necesario.
1. Para ver las propiedades de metadatos de una colección específica, cancele la selección de las colecciones restantes en la lista de colecciones. Los campos del editor de metadatos se rellenan con los metadatos de la colección en cuestión.

   >[!NOTE]
   >
   >* En la página [!UICONTROL Propiedades], puede quitar colecciones de la lista de colecciones cancelando la selección. La lista de colecciones tiene todas las colecciones seleccionadas de forma predeterminada. [!DNL Experience Manager] no actualiza los metadatos de las colecciones que usted quita.
   >* En la parte superior de la lista, active la casilla de verificación situada cerca de **[!UICONTROL Title]** para alternar entre seleccionar las colecciones y borrar la lista.

1. Haga clic en **[!UICONTROL Guardar y cerrar]** en la barra de herramientas y, a continuación, cierre el cuadro de diálogo de confirmación.
1. Para anexar los nuevos metadatos con los metadatos existentes, seleccione **[!UICONTROL Modo de anexar]**. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Haga clic en **[!UICONTROL Enviar]**.

   >[!NOTE]
   >
   >Los metadatos que agregue para las colecciones seleccionadas sobrescribirán los metadatos anteriores para estas colecciones. Use [!UICONTROL Modo de adición] para agregar nuevos valores a los metadatos existentes en los campos que pueden contener varios valores. Los campos de un solo valor siempre se sobrescriben. Todas las etiquetas que agregue al campo [!UICONTROL Etiquetas] se anexarán a la lista de etiquetas existente en los metadatos.

Para personalizar la página de metadatos [!UICONTROL Propiedades], incluidas las propiedades de adición, modificación y eliminación de metadatos, use el Editor de esquemas.

>[!TIP]
>
>El método de edición por lotes funciona para los recursos disponibles en una colección. Para los recursos que están disponibles en todas las carpetas o que coinciden con un criterio común, es posible [actualizar en lotes los metadatos después de buscar](/help/assets/search-assets.md#metadataupdates).

## Buscar colecciones {#searching-collections}

Puede buscar colecciones desde la consola Colecciones. Cuando busca con palabras clave en el cuadro Omnisearch, [!DNL Assets] busca nombres de colección, metadatos y las etiquetas agregadas a las colecciones.

Si busca colecciones desde el nivel superior, solo se devuelven colecciones individuales en los resultados de búsqueda. Se excluyen [!DNL Assets] o carpetas dentro de las colecciones. En todos los demás casos (por ejemplo, dentro de una colección individual o en una jerarquía de carpetas), se devuelven todos los recursos, carpetas y colecciones relevantes.

## Buscar en colecciones {#searching-within-collections}

En la consola Colecciones, haga clic en una colección para abrirla.

En una colección, la búsqueda de [!DNL Experience Manager] está restringida a los recursos (y sus etiquetas y metadatos) de la colección que está viendo. Al buscar dentro de una carpeta, se devuelven todos los recursos coincidentes y las carpetas secundarias de la carpeta actual. Cuando busca dentro de una colección, solo se devuelven los recursos, las carpetas y otras colecciones que coincidan y que sean miembros directos de la colección.

## Editar configuración de colección {#editing-collection-settings}

Puede editar la configuración de la colección, como el título y la descripción, o agregar miembros a una colección.

1. Seleccione una colección y haga clic en **[!UICONTROL Configuración]** en la barra de herramientas. También puedes usar la acción rápida **[!UICONTROL Settings]** de la miniatura de la colección.
1. Modifique la configuración de la colección en la página **[!UICONTROL Configuración de la colección]**. Por ejemplo, modifique el título de la colección, las descripciones, los miembros y los permisos tal como se describe en [Agregar colecciones](#creating-a-collection).

1. Para guardar los cambios, haga clic en **[!UICONTROL Guardar]**.

## Eliminar una colección {#deleting-a-collection}

1. En la consola Colecciones, seleccione una o varias colecciones y haga clic en eliminar en la barra de herramientas.

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Eliminar]** para confirmar la acción de eliminación.

   >[!NOTE]
   >
   >También puede eliminar colecciones inteligentes [eliminando búsquedas guardadas](#saved-searches).

## Descargar una colección {#downloading-a-collection}

Al descargar una colección, se descarga toda la jerarquía de recursos de la colección, incluidas las carpetas y las colecciones secundarias.

1. En la consola Colecciones, seleccione una o varias colecciones para descargar.
1. En la barra de herramientas, haga clic en **[!UICONTROL Descargar]**.
1. En el cuadro de diálogo **[!UICONTROL Descargar]**, haga clic en **[!UICONTROL Descargar]**. Si desea descargar las representaciones de los recursos de la colección, seleccione **[!UICONTROL Representaciones]**. Seleccione la opción **[!UICONTROL Email]** para enviar una notificación por correo electrónico al propietario de la colección.

   Al seleccionar una colección para descargar, se descarga toda la jerarquía de carpetas de la colección. Para incluir cada colección que descargue (incluidos los recursos de colecciones secundarias anidadas en la colección principal) en una carpeta individual, seleccione **[!UICONTROL Crear una carpeta independiente para cada recurso]**.

## Creación de colecciones anidadas {#creating-nested-collections}

Puede agregar una colección a otra colección para crear una colección anidada.

1. En la consola Colecciones, seleccione la colección o el grupo de colecciones que desee y haga clic en **[!UICONTROL Para la colección]** en la barra de herramientas.

1. En la página **[!UICONTROL Agregar a colección]**, seleccione la colección en la que desea agregar la colección.

   >[!NOTE]
   >
   >La colección actualizada más recientemente está seleccionada de manera predeterminada en la página **[!UICONTROL Agregar a colección]**.

1. Haga clic en **[!UICONTROL Agregar]**. Un mensaje confirma que la colección se agrega a la colección de destino en la página **[!UICONTROL Seleccionar destino]**. Cierre el mensaje para completar el proceso.

>[!NOTE]
>
>Las colecciones inteligentes no se pueden anidar. En otras palabras, las colecciones inteligentes no pueden contener ninguna otra colección.

## Búsquedas guardadas {#saved-searches}

En la interfaz de usuario [!DNL Assets], puede buscar o filtrar recursos en función de determinadas reglas, criterios de búsqueda o facetas de búsqueda personalizadas. Si los guarda como **[!UICONTROL Búsquedas guardadas]**, puede acceder a ellos más adelante desde la lista **[!UICONTROL Búsquedas guardadas]** del panel Filtro. Al crear una búsqueda guardada también se crea una colección inteligente.

![lista_búsquedas_guardadas](assets/saved_searches_list.png)

Las búsquedas guardadas se crean al crear una colección inteligente. Las colecciones inteligentes se agregan automáticamente a la lista **[!UICONTROL Búsquedas guardadas]**. La consulta [!UICONTROL Búsquedas guardadas] para la colección se guarda en la propiedad `dam:query` de CRXDE en la ubicación relativa `/content/dam/collections/`. No existen límites para las búsquedas que se pueden guardar y para las búsquedas guardadas que se muestran en la lista.

>[!NOTE]
>
>Puede compartir colecciones inteligentes del mismo modo que comparte colecciones estáticas.

Editar búsquedas guardadas es lo mismo que editar colecciones inteligentes. Para obtener más información, consulte [editar una colección inteligente](#editing-a-smart-collection).

Para eliminar búsquedas guardadas, siga estos pasos:

1. En la interfaz de usuario [!DNL Assets], haga clic en buscar ![opción de búsqueda](assets/do-not-localize/search_icon.png).
1. Con el cursor en el campo Omnisearch, seleccione la clave `Return`.
1. En la interfaz [!DNL Experience Manager], abra el panel Filtros.
1. En la lista **[!UICONTROL Búsquedas guardadas]**, haga clic en **[!UICONTROL Eliminar]** junto a la colección inteligente que desee eliminar.

   ![select_smart_collection](assets/select_smart_collection.png)

1. En el cuadro de diálogo, haga clic en **[!UICONTROL Eliminar]** para eliminar la búsqueda guardada.

## Ejecutar un flujo de trabajo en una colección {#running-a-workflow-on-a-collection}

Puede ejecutar un flujo de trabajo para los recursos de una colección. Si la colección contiene colecciones anidadas, el flujo de trabajo también se ejecuta en los recursos de las colecciones anidadas. Sin embargo, si la colección y la colección anidada contienen recursos duplicados, el flujo de trabajo solo se ejecuta una vez para esos recursos.

1. Abra **[!UICONTROL Assets]** > **[!UICONTROL Colecciones]**. Para ejecutar un flujo de trabajo en una colección específica, selecciónela.
1. Abra el carril **[!UICONTROL Cronología]**. Haga clic en ![cheurón superior](assets/do-not-localize/chevron-up-icon.png) y luego en **[!UICONTROL Iniciar flujo de trabajo]**.
1. En la sección **[!UICONTROL Iniciar flujo de trabajo]**, seleccione un modelo de flujo de trabajo de la lista. Por ejemplo, seleccione el modelo **[!UICONTROL Recurso de actualización DAM]**.
1. Escriba un título para el flujo de trabajo y haga clic en **[!UICONTROL Iniciar]**.
1. En el cuadro de diálogo, haga clic en **[!UICONTROL Continuar]**. El flujo de trabajo procesa todos los recursos de la colección seleccionada.

>[!MORELIKETHIS]
>
>* [Configurar notificaciones por correo electrónico de Experience Manager Assets](/help/sites-administering/notification.md#assetsconfig)
>* [Crear una tarea de revisión para Colecciones](bulk-approval.md)
