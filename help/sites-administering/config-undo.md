---
title: Configurar Deshacer para editar páginas
description: Obtenga información sobre cómo configurar la compatibilidad con Deshacer para editar páginas en AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# Configurar Deshacer para editar páginas{#configuring-undo-for-page-editing}

El servicio [OSGi](/help/sites-deploying/configuring-osgi.md) **Configuración de deshacer de CQ WCM de día** ( `com.day.cq.wcm.undo.UndoConfigService`) expone varias propiedades que controlan el comportamiento de los comandos de deshacer y rehacer para editar páginas.

## Configuración predeterminada {#default-configuration}

En una instalación estándar, la configuración predeterminada se define como propiedades en el nodo `sling:OsgiConfig`:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Este nodo contiene `cq.wcm.undo.whitelist` y `cq.wcm.undo.blacklist` propiedades. Para las demás propiedades se toman los valores predeterminados.

>[!CAUTION]
>
>Usted ***no debe*** cambiar nada en la ruta de acceso `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).

## Configuración de Deshacer y Rehacer {#configuring-undo-and-redo}

Puede configurar estas propiedades del servicio OSGi para su propia instancia.

>[!NOTE]
>
>Al trabajar con AEM, existen varios métodos para administrar las opciones de configuración de dichos servicios; consulte [Configuración de OSGi](/help/sites-deploying/configuring-osgi.md) para obtener más información y las prácticas recomendadas.

A continuación, se enumeran las propiedades tal como se muestran en la consola web, seguidas del nombre del parámetro OSGi correspondiente, junto con una descripción y el valor predeterminado (cuando corresponda):

* **Habilitar**
( `cq.wcm.undo.enabled`)

   * **Descripción**: Determina si los autores de la página pueden deshacer y rehacer los cambios.
   * **Predeterminado**: `Selected`
   * **Tipo**: `Boolean`

* **Ruta**
( `cq.wcm.undo.path`)

   * **Descripción**: La ruta de acceso del repositorio para los datos de deshacer binarios persistentes. Cuando los autores cambian datos binarios, como imágenes, la versión original de los datos se mantiene aquí. Cuando se deshacen los cambios en los datos binarios, estos datos de deshacer binarios se restauran en la página.
   * **Predeterminado**: `/var/undo`
   * **Tipo**: `String`

  >[!NOTE]
  >
  >De manera predeterminada, solamente los administradores pueden tener acceso al nodo `/var/undo`. Los autores solo pueden realizar operaciones de deshacer y rehacer en el contenido binario una vez que se les han concedido permisos para acceder a los datos de deshacer binarios.

* **Min. validez**
( `cq.wcm.undo.validity`)

   * **Descripción**: Cantidad mínima de tiempo que se almacenan los datos de deshacer binarios, en horas. Después de este período de tiempo, los datos binarios están disponibles para su eliminación, para conservar espacio en disco.
   * **Predeterminado**: `10`
   * **Tipo**: `Integer`

* **Pasos**
( `cq.wcm.undo.steps`)

   * **Descripción**: Número máximo de acciones de página almacenadas en el historial de deshacer.
   * **Predeterminado**: `20`
   * **Tipo**: `Integer`

* **Persistencia**
( `cq.wcm.undo.persistence`)

   * **Descripción**: La clase que persiste en el historial de deshacer. Se proporcionan dos clases de persistencia:

      * `CQ.undo.persistence.WindowNamePersistence`: conserva el historial utilizando la propiedad window.name.
      * `CQ.undo.persistence.CookiePersistance`: conserva el historial usando cookies.

   * **Predeterminado**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`

* **Modo de persistencia**
( `cq.wcm.undo.persistence.mode`)

   * **Descripción**: Determina cuándo se mantiene el historial de deshacer. Seleccione esta opción para mantener el historial de deshacer después de cada edición de página. Desactive esta opción para que solo se mantenga cuando se vuelva a cargar una página (por ejemplo, cuando el usuario navegue a una página diferente).

     La persistencia del historial de deshacer utiliza recursos del explorador web. Si el explorador del usuario reacciona lentamente a las ediciones de página, intente mantener el historial de deshacer en las recargas de la página.

   * **Predeterminado**: `Selected`
   * **Tipo**: `Boolean`

* **Modo de marcador**
( `cq.wcm.undo.markermode`)

   * **Descripción**: Especifica la referencia visual que se debe utilizar para indicar qué párrafos se ven afectados cuando se deshace o rehace una acción. Los siguientes valores son válidos:

      * flash: El indicador de selección de los párrafos parpadea temporalmente.
      * select: El párrafo está seleccionado.

   * **Predeterminado**: `flash`
   * **Tipo**: `String`

* **Componentes correctos**
( `cq.wcm.undo.whitelist`)

   * **Descripción**: Una lista de los componentes que desea que se vean afectados por los comandos Deshacer y Rehacer. Añada rutas de componentes a esta lista cuando funcionen correctamente con Deshacer/Rehacer. Anexe un asterisco (&amp;ast;) para especificar un grupo de componentes:

      * El siguiente valor especifica el componente de texto de base:

        `foundation/components/text`

      * El siguiente valor especifica todos los componentes de base:

        `foundation/components/*`

   * Cuando se emiten acciones de deshacer o rehacer a un componente que no está en esta lista, aparece un mensaje que indica que el comando puede no ser fiable.

   * **Predeterminado**: la propiedad se rellena con muchos componentes que proporciona AEM.
   * **Tipo**: `String[]`

* **Componentes incorrectos**
( `cq.wcm.undo.blacklist`)

   * **Descripción**: Una lista de componentes u operaciones de componentes que no desea que se vean afectadas por el comando Deshacer. Añada componentes y operaciones de componentes que no se comporten correctamente con el comando Deshacer:

      * Agregue una ruta de acceso al componente cuando no desee ninguna de sus operaciones en el historial de deshacer, por ejemplo, `collab/forum/components/post`
      * Agregue dos puntos (:) y una operación a la ruta de acceso cuando desee que esa operación específica se omita del historial de deshacer (otras operaciones funcionan correctamente), por ejemplo, `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >Cuando una operación está en esta lista, se agrega al historial de deshacer. Los usuarios no pueden deshacer operaciones anteriores a una operación de **componente incorrecto** en el historial de deshacer.

   * Los nombres de operación habituales son los siguientes:

      * `insertParagraph`: el componente se agrega a la página.
      * `removeParagraph`: el componente se ha eliminado.
      * `moveParagraph`: el párrafo se mueve a una ubicación diferente.
      * `updateParagraph`: las propiedades del párrafo se han cambiado.

   * **Predeterminado**: la propiedad se rellena con varias operaciones de componente.
   * **Tipo**: `String[]`
