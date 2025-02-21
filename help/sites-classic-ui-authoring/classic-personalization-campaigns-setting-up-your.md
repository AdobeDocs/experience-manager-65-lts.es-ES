---
title: Configuración de la campaña
description: La configuración de una nueva campaña requiere la creación de una marca que contenga sus campañas, la creación de una campaña que incluya experiencias y la definición final de las propiedades de la nueva campaña.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2194'
ht-degree: 0%

---

# Configuración de la campaña{#setting-up-your-campaign}

La configuración de una nueva campaña incluye los siguientes pasos (genéricos):

1. [Crea una marca](#creating-a-new-brand) para albergar tus campañas.
1. Si es necesario, puede [definir las propiedades de su nueva marca](#defining-the-properties-for-your-new-brand).
1. [Cree una campaña](#creating-a-new-campaign) para albergar experiencias; por ejemplo, páginas de teaser o un boletín informativo.
1. Si es necesario, puede [definir las propiedades de su nueva campaña](#defining-the-properties-for-your-new-campaign).

A continuación, según el tipo de experiencias que cree, debe [crear una experiencia](#creating-a-new-experience). Los detalles de la experiencia y las acciones que siguen a su creación dependen del tipo de experiencia que desee crear:

* Si crea un teaser:

   1. [Crear una experiencia de teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaserexperience).
   1. [Agregar contenido al teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttoyourteaser).
   1. [Crear un punto de contacto para el teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (agregue el teaser a una página de contenido).

* Si crea una newsletter:

   1. [Crear una experiencia de newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletterexperience).
   1. [Añadir contenido al boletín informativo.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   1. [Personalice la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   1. [Crear una página de aterrizaje de newsletter atractiva](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).
   1. [Envíe la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) a los suscriptores o posibles clientes.

* Si crea una oferta de Adobe Target (anteriormente Test&amp;Target):

   1. [Crear una experiencia de oferta de Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetofferexperience).
   1. [Integración con Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#integratewithadobetesttarget)

>[!NOTE]
>
>Consulte [Segmentación](/help/sites-administering/campaign-segmentation.md) para obtener instrucciones detalladas sobre cómo definir los segmentos.

## Crear una nueva marca {#creating-a-new-brand}

1. Abra **MCM** y seleccione **Campañas** en el panel izquierdo.

1. Seleccione **Nuevo...** para ingresar el **Título** y el **Nombre** y la plantilla que se usarán para su nueva marca:

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Haga clic en **Crear**. La nueva marca se muestra en el MCM (con un icono predeterminado).

### Definición de las propiedades de la nueva marca {#defining-the-properties-for-your-new-brand}

1. De **Campañas** en el panel izquierdo, selecciona tu nuevo icono de marca en el panel derecho y haz clic en **Propiedades...**

   Puede escribir **Título**, **Descripción** y una imagen para usarla como icono.

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. Haga clic en **Aceptar** para guardar.

### Creación de una nueva campaña {#creating-a-new-campaign}

1. En **Campañas**, seleccione su nueva marca en el panel izquierdo o haga doble clic en el icono en el panel derecho.

   Se muestra la descripción general (vacío si la marca es nueva).

1. Haga clic en **Nuevo...** y especifique el **Título**, **Nombre** y la plantilla que se utilizarán para la nueva campaña.

   ![chlimage_1-19](assets/chlimage_1-19.png)

1. Haga clic en **Crear**. La nueva campaña se muestra en el MCM.

### Definición de las propiedades de la nueva campaña {#defining-the-properties-for-your-new-campaign}

Configure las propiedades de la campaña que controlan el comportamiento:

* **Prioridad:** Prioridad de esta campaña en relación con otras campañas. Cuando se activan varias campañas simultáneamente, la campaña que tiene la prioridad más alta controla la experiencia del visitante.
* **Tiempo de activación y desactivación:** estas propiedades controlan el período de tiempo en que la campaña controla la experiencia del visitante. La propiedad On Time controla el momento en el que la campaña empieza a controlar la experiencia. La propiedad Tiempo de inactividad controla cuándo las campañas dejan de controlar la experiencia.
* **Imagen:** La imagen que representa la campaña en AEM.
* **Servicios de nube:** Las configuraciones de Cloud Service con las que está integrada la campaña. (Consulte [Integración con Adobe Marketing Cloud](/help/sites-administering/marketing-cloud.md).)

* **Adobe Target:** propiedades que configuran campañas integradas con Adobe Target. (Consulte [Integración con Adobe Target](/help/sites-administering/target.md).)

1. De **Campañas**, selecciona tu marca. En el panel derecho, seleccione su campaña y haga clic en **Propiedades**.

   Puede introducir varias propiedades, entre ellas **Title**, **Description** y cualquier **servicio en la nube** que desee.

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Haga clic en **Aceptar** para guardar.

### Creación de una nueva experiencia {#creating-a-new-experience}

El procedimiento para crear una experiencia depende del tipo de experiencia:

* [Creación de un teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingateaser)
* [Creación de una newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatinganewsletter)
* [Creación de una oferta de Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatesttargetoffer)

>[!NOTE]
>
>Al igual que con las versiones anteriores, aún es posible crear la experiencia como página en la consola **Sitios web** (y cualquier página de este tipo creada en versiones anteriores sigue siendo totalmente compatible).
>
>Ahora se recomienda utilizar el MCM para crear experiencias.

### Configuración de la nueva experiencia {#configuring-your-new-experience}

Ahora que ha creado el esqueleto básico para la experiencia, debe continuar con las siguientes acciones, según el tipo de experiencia:

* [Teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#teasers):

   * [Conecte la página de teaser a segmentos del visitante.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#applyingasegmenttoyourteaser)
   * [Crear un punto de contacto para el teaser](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#creatingatouchpointforyourteaser) (agregue el teaser a una página de contenido).

* [Newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#newsletters):

   * [Añadir contenido al boletín informativo.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#addingcontenttonewsletters)
   * [Personalice la newsletter.](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#personalizingnewsletters)
   * [Envíe la newsletter](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#sendingnewsletters) a los suscriptores o posibles clientes.
   * [Crear una página de aterrizaje de newsletter atractiva](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#settingupanewsletterlandingpage).

* [Oferta de Adobe Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#testtargetoffers):

   * [Integración con Adobe Target](/help/sites-administering/target.md)

### Adición de un nuevo punto de contacto {#adding-a-new-touchpoint}

Si tiene experiencias existentes, puede agregar un punto de contacto directamente desde la vista Calendario de MCM:

1. Seleccione la vista de calendario de la campaña.

1. Haga clic en **Agregar punto de contacto...** para abrir el cuadro de diálogo. Especifique la experiencia que desea agregar:

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. Haga clic en **Aceptar** para guardar.

## Uso de posibles clientes {#working-with-leads}

>[!NOTE]
>
>Adobe no tiene previsto mejorar esta capacidad (administración de posibles clientes).
>Se recomienda usar [Adobe Campaign y la integración con AEM](/help/sites-administering/campaign.md).

En AEM MCM, puede organizar y agregar posibles clientes introduciéndolos manualmente o importando una lista separada por comas, por ejemplo, una lista de correo. Otras formas de generar posibles clientes son las suscripciones a boletines informativos o las suscripciones a la comunidad (si se configuran, pueden almacenar en déclencheur un flujo de trabajo que rellene los posibles clientes).

Los posibles clientes generalmente se clasifican y se colocan en una lista para que más tarde pueda realizar acciones en toda la lista, por ejemplo, enviar un correo electrónico personalizado a una lista determinada.

En el panel, para acceder a todos los posibles clientes, haga clic en **Posibles clientes** en el panel izquierdo. También puede obtener acceso a los posibles clientes desde el panel **Listas**.

![screen_shot_2012-02-21at114748am](assets/screen_shot_2012-02-21at114748am.png)

>[!NOTE]
>
>Para agregar o modificar los avatares de los usuarios, abra la nube del flujo de navegación (Ctrl+Alt+c), cargue el perfil y haga clic en **Editar**.

### Creación de nuevos posibles clientes {#creating-new-leads}

Después de crear nuevos clientes potenciales, asegúrese de [activarlos](#activating-or-deactivating-leads) para que pueda rastrear su actividad en la instancia de publicación y personalizar su experiencia.

Para crear un posible cliente manualmente:

1. En AEM, vaya al MCM. En el panel, haga clic en **Posibles clientes**.
1. Haga clic en **Nuevo**. Se abre la ventana **Crear nuevo**.

   ![screen_shot_2012-02-21at115008am](assets/screen_shot_2012-02-21at115008am.png)

1. Introduzca información en los campos, según corresponda. Haga clic en la ficha **Dirección**.

   ![screen_shot_2012-02-21at115045am](assets/screen_shot_2012-02-21at115045am.png)

1. Introduzca la información de la dirección, según corresponda. Haga clic en **Guardar** para guardar el posible cliente. Si necesita agregar posibles clientes adicionales, haga clic en **Guardar y nuevo**.

   El nuevo posible cliente aparecerá en el panel Posibles clientes. Al hacer clic en la entrada, toda la información introducida aparece en el panel derecho. Después de crear un posible cliente, puede agregarlo a una lista.

   ![screen_shot_2012-02-21at120307pm](assets/screen_shot_2012-02-21at120307pm.png)

### Activar o desactivar posibles clientes {#activating-or-deactivating-leads}

La activación de posibles clientes le ayuda a realizar un seguimiento de su actividad en la instancia de publicación y le permite personalizar su experiencia. Cuando ya no desee rastrear su actividad, puede desactivarlos.

Para posibles clientes activos o desactivados:

1. En AEM, vaya al MCM y haga clic en **Posibles clientes**.

1. Seleccione los posibles clientes que quiera activar o desactivar y haga clic en **Activar** o **Desactivar**.

   ![screen_shot_2012-02-21at120620pm](assets/screen_shot_2012-02-21at120620pm.png)

   Al igual que con las páginas de AEM, el estado de publicación se indica en la columna **Publicado**.

   ![screen_shot_2012-02-21at122901pm](assets/screen_shot_2012-02-21at122901pm.png)

### Importación de nuevos posibles clientes {#importing-new-leads}

Al importar nuevos posibles clientes, puede agregarlos automáticamente a una lista existente o crear una lista para incluirlos.

Para importar posibles clientes de una lista separada por comas:

1. En AEM, vaya al MCM y haga clic en **Posibles clientes**.

   >[!NOTE]
   >
   >Como alternativa, puede importar posibles clientes mediante uno de los procedimientos siguientes:
   >
   >* En el panel, haga clic en **Importar posibles clientes** en el panel **Listas**
   >* Haga clic en **Listas** y en el menú **Herramientas**, seleccione **Importar posibles clientes**.

1. En el menú **Herramientas**, seleccione **Importar** **Posibles clientes**.

1. Introduzca la información tal como se describe en Datos de ejemplo. Se pueden importar los campos siguientes: email,familyName,givenName,gender,aboutMe,city,country,phoneNumber,postalCode,region,streetAddress

   >[!NOTE]
   >
   >La primera fila de la lista CSV son etiquetas predefinidas que deben escribirse exactamente como en el ejemplo:
   >
   >
   >`email,givenName,familyName`: si se escribe como `givenname`, por ejemplo, el sistema no lo reconocerá.
   >
   >

   ![screen_shot_2012-02-21at123055pm](assets/screen_shot_2012-02-21at123055pm.png)

1. Haga clic en **Siguiente**. Aquí puede previsualizar los posibles clientes para asegurarse de que son precisos.

   ![screen_shot_2012-02-21at123104pm](assets/screen_shot_2012-02-21at123104pm.png)

1. Haga clic en **Siguiente**. Seleccione la lista a la que desea que pertenezcan los posibles clientes. Si no desea que pertenezcan a una lista, elimine la información del campo. De forma predeterminada, AEM crea un nombre de lista que incluye la fecha y la hora. Haga clic en **Importar**.

   ![screen_shot_2012-02-21at123123pm](assets/screen_shot_2012-02-21at123123pm.png)

   El nuevo posible cliente aparecerá en el panel Posibles clientes. Si hace clic en la entrada, toda la información introducida aparecerá en el panel derecho. Después de crear un posible cliente, puede agregarlo a una lista.

### Adición de posibles clientes a listas {#adding-leads-to-lists}

Para agregar posibles clientes a listas preexistentes:

1. En el MCM, haga clic en **Posibles clientes** para ver todos los posibles clientes disponibles.

1. Seleccione los posibles clientes que desee agregar a una lista seleccionando la casilla de verificación situada junto al posible cliente. Puede agregar todos los posibles clientes que desee.

   ![screen_shot_2012-02-21at123835pm](assets/screen_shot_2012-02-21at123835pm.png)

1. En el menú **Herramientas**, seleccione **Agregar a lista....** Se abre la ventana **Agregar a la lista**.

   ![screen_shot_2012-02-21at124019pm](assets/screen_shot_2012-02-21at124019pm.png)

1. Seleccione a qué lista desea agregar los posibles clientes y haga clic en **Aceptar**. Los posibles clientes se agregan a las listas correspondientes.

### Visualización de información de posibles clientes {#viewing-lead-information}

Para ver la información del posible cliente, en el MCM, haga clic en la casilla de verificación situada junto al posible cliente y se abrirá un panel derecho con toda la información del posible cliente, incluida la afiliación a la lista.

![screen_shot_2012-02-21at124228pm](assets/screen_shot_2012-02-21at124228pm.png)

### Modificación de posibles clientes existentes {#modifying-existing-leads}

Para modificar la información de posibles clientes existente:

1. En el MCM, haga clic en **Posibles clientes**. En la lista de posibles clientes, active la casilla de verificación situada junto al posible cliente que desea editar. Toda la información del posible cliente aparece en el panel derecho.

   ![screen_shot_2012-02-21at124514pm](assets/screen_shot_2012-02-21at124514pm.png)

   >[!NOTE]
   >
   >Solo puede editar un posible cliente a la vez. Si necesita modificar los posibles clientes que forman parte de la misma lista, puede modificarla en su lugar.

1. Haga clic en **Editar**. Se abre la ventana **Editar posible cliente**.

   ![screen_shot_2012-02-21at124609pm](assets/screen_shot_2012-02-21at124609pm.png)

1. Realice las modificaciones necesarias y haga clic en **Guardar** para guardar los cambios.

   >[!NOTE]
   >
   >Para cambiar el avatar del posible cliente, vaya al perfil de los usuarios. Puede cargar el perfil en la nube del flujo de navegación si presiona CTRL+ALT+c, hace clic en **Cargar** y, a continuación, selecciona el perfil.

### Eliminar posibles clientes existentes {#deleting-existing-leads}

Para eliminar posibles clientes existentes en el MCM, seleccione la casilla de verificación situada junto al posible cliente y haga clic en **Eliminar**. El posible cliente se elimina de la lista de posibles clientes y de todas las listas asociadas.

>[!NOTE]
>
>Antes de eliminar, AEM confirma que desea eliminar el posible cliente existente. Una vez eliminado, no se puede recuperar.

## Uso de listas {#working-with-lists}

>[!NOTE]
>
>Adobe no planea mejorar esta capacidad (administración de listas).
>Se recomienda usar [Adobe Campaign y la integración con AEM](/help/sites-administering/campaign.md).

Las listas permiten organizar los posibles clientes en grupos. Con las listas, puede dirigir sus campañas de marketing a un grupo selecto de personas; por ejemplo, puede enviar una newsletter segmentada a una lista. Las listas son visibles en el MCM, ya sea en el panel o haciendo clic en **Listas**. Ambos le proporcionan el nombre de la lista y el número de miembros.

![screen_shot_2012-02-21at125021pm](assets/screen_shot_2012-02-21at125021pm.png)

Si hace clic en **Listas**, también puede ver si la lista es miembro de otra lista y ver una descripción.

![screen_shot_2012-02-21at124828pm](assets/screen_shot_2012-02-21at124828pm.png)

### Creación de nuevas listas {#creating-new-lists}

1. En el panel MCM, haga clic en **Nueva lista ...** o en **Listas**, haga clic en **Nuevo** ... Se abrirá la ventana Crear lista.

   ![screen_shot_2012-02-21at125147pm](assets/screen_shot_2012-02-21at125147pm.png)

1. Escriba un nombre (obligatorio) y, si lo desea, una descripción y haga clic en **Guardar**. La lista aparece en el panel **Listas**.

   ![screen_shot_2012-02-21at125320pm](assets/screen_shot_2012-02-21at125320pm.png)

### Modificación de listas existentes {#modifying-existing-lists}

1. En el MCM, haga clic en **Listas**.

1. En la lista, seleccione la casilla de verificación que está junto a la lista que desea editar y haga clic en **Editar**. Se abre la ventana **Editar lista**.

   ![screen_shot_2012-02-21at125452pm](assets/screen_shot_2012-02-21at125452pm.png)

   >[!NOTE]
   >
   >Solo se puede editar una lista a la vez.

1. Realice las modificaciones necesarias y haga clic en **Guardar** para guardar los cambios.

### Eliminación de listas existentes {#deleting-existing-lists}

Para eliminar listas existentes, en el MCM, active la casilla de verificación situada junto a la lista y haga clic en **Eliminar**. Se eliminará la lista. Los posibles clientes que estaban afiliados a la lista no se eliminan, solo se elimina la afiliación con la lista.

>[!NOTE]
>
>Antes de eliminar, AEM confirma que desea eliminar las listas existentes. Una vez eliminado, no se puede recuperar.

### Combinación de listas {#merging-lists}

Puede combinar una lista existente con otra lista. Al hacerlo, la lista que está combinando se convierte en miembro de la otra lista. Sigue existiendo como una entidad independiente y no debe eliminarse.

Puede combinar listas si tiene la misma conferencia en dos ubicaciones diferentes y desea combinarlas en una lista de asistentes de todas las conferencias.

Para combinar listas existentes:

1. En el MCM, haga clic en **Listas**.

1. Seleccione la lista con la que desea combinar otra lista activando la casilla de verificación situada junto a ella.

1. En el menú **Herramientas**, seleccione **Lista de combinación**.

   >[!NOTE]
   >
   >Solo se puede combinar una lista a la vez.

1. En la ventana **Combinar lista**, seleccione la lista con la que desee combinar y haga clic en **Aceptar**.

   ![screen_shot_2012-02-21at10259pm](assets/screen_shot_2012-02-21at10259pm.png)

   La lista que ha combinado debe aumentar en un miembro. Para ver que la lista se ha combinado, seleccione la lista que ha combinado y, en el menú **Herramientas**, seleccione **Mostrar posibles clientes**.

1. Repita el paso hasta que haya combinado todas las listas que desee.

   ![screen_shot_2012-02-21at10538pm](assets/screen_shot_2012-02-21at10538pm.png)

>[!NOTE]
>
>Quitar una lista combinada de sus miembros es idéntico a quitar un posible cliente de una lista. Abra la ficha **Lists**, seleccione la lista que incluye la lista combinada y quite la pertenencia haciendo clic en el círculo rojo situado junto a la lista.

### Visualización de posibles clientes en listas {#viewing-leads-in-lists}

En cualquier momento, puede ver qué posibles clientes pertenecen a una lista específica explorando o buscando miembros.

Para ver los posibles clientes en las listas:

1. En el MCM, haga clic en **Listas**.

1. Active la casilla de verificación situada junto a la lista cuyos miembros desea ver.

1. En el menú **Herramientas**, seleccione **Mostrar posibles clientes**. AEM muestra los posibles clientes que son miembros de esa lista. Puede examinar la lista o buscar miembros.

   >[!NOTE]
   >
   >Además, puede eliminar posibles clientes de una lista seleccionándolos y haciendo clic en **Quitar pertenencia**.

   ![screen_shot_2012-02-21at10828pm](assets/screen_shot_2012-02-21at10828pm.png)

1. Haga clic en **Cerrar** para volver al MCM.
