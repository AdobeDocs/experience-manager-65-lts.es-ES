---
title: Asignación de datos de componente con propiedades de Adobe Analytics
description: Obtenga información sobre cómo asignar datos de componentes con propiedades de SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 0%

---

# Asignación de datos de componente con propiedades de Adobe Analytics{#mapping-component-data-with-adobe-analytics-properties}

Agregue componentes al marco de trabajo que recopilen los datos para enviarlos a Adobe Analytics. Los componentes diseñados para recopilar datos de análisis almacenan los datos en la **variable CQ** correspondiente. Cuando se agrega un componente de este tipo a un marco de trabajo, el marco de trabajo muestra la lista de variables de CQ para que pueda agregarlas a la **variable de Analytics** correspondiente.

![aa-11](assets/aa-11.png)

Cuando la **vista de AEM** está abierta, las variables de Analytics aparecen en el buscador de contenido.

![aa-12](assets/aa-12.png)

Puede asignar varias variables de Analytics con la misma **variable CQ**.

![chlimage_1-68](assets/chlimage_1-68.png)

Los datos asignados se envían a Adobe Analytics cuando se carga la página y se cumplen las siguientes condiciones:

* La página está asociada al marco de trabajo.
* La página utiliza los componentes que se añaden al marco de trabajo.

Utilice el siguiente procedimiento para asignar variables de componente CQ con propiedades de informe de Adobe Analytics.

1. En la **vista de AEM**, arrastre un componente de seguimiento de la barra de tareas al marco de trabajo. Por ejemplo, arrastre el componente **Página** desde la categoría **General**.

   ![aa-13](assets/aa-13.png)

   Hay varios grupos de componentes predeterminados: **General**, **Commerce**, **Communities** y **Other**. La instancia de AEM se puede configurar para mostrar diferentes grupos y componentes.

1. Para asignar variables de Adobe Analytics con variables definidas en el componente, arrastre una **variable de Analytics** desde el buscador de contenido a un campo del componente de seguimiento. Por ejemplo, arrastre `Page Name (pageName)` a `pagedata.title`.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >El ID del grupo de informes (RSID) seleccionado para el marco de trabajo determina las variables de Adobe Analytics que aparecen en el buscador de contenido.

1. Repita los dos pasos anteriores para otros componentes y variables.

   >[!NOTE]
   >
   >Puede asignar varias variables de Analytics (por ejemplo, `props`, `eVars`, `events`) a la misma variable de CQ (por ejemplo, `pagedata.title`)

   >[!CAUTION]
   >
   >Se recomienda encarecidamente que:
   >
   >* `eVars` y `props` están asignados a variables de CQ que comienzan por `pagedata.X` o `eventdata.X`
   >* los eventos deben asignarse a variables que empiecen por `eventdata.events.X`

1. Para que el marco de trabajo esté disponible en la instancia de publicación del sitio, abra la pestaña **Página** de la barra de tareas y haga clic en **Activar marco de trabajo**.

## Asignación de variables relacionadas con el producto {#mapping-product-related-variables}

AEM utiliza una convención de nombres de variables y eventos relacionados con productos que están pensados para asignarse a propiedades relacionadas con productos de Adobe Analytics:

| Variable CQ | Variable de Analytics | Descripción |
|--- |--- |--- |
| `product.category` | `product.category` (variable de conversión) | La categoría del producto. |
| `product.sku` | `product.sku` (variable de conversión) | El SKU del producto. |
| `product.quantity` | `product.quantity` (variable de conversión) | Número de productos que se están comprando. |
| `product.price` | `product.price` (variable de conversión) | El precio del producto. |
| `product.events.<eventName>` | Los eventos de éxito que se asociarán con el producto en el informe. | `product.events` es el prefijo de los eventos llamados *eventName.* |
| `product.evars.<eVarName>` | Las variables de conversión (`eVar`) que se van a asociar con el producto. | `product.evars` es el prefijo de las variables de eVar denominadas *eVarName.* |

Varios componentes de AEM Commerce utilizan estos nombres de variables.

>[!NOTE]
>
>No asigne la propiedad Productos de Adobe Analytics a una variable de CQ. La configuración de asignaciones relacionadas con productos como se describe en la tabla es equivalente a la asignación de la variable Products.

### Comprobación de informes en Adobe Analytics {#checking-reports-on-adobe-analytics}

1. Inicie sesión en el sitio web de Adobe Analytics con las mismas credenciales proporcionadas para AEM.
1. Asegúrese de que el RSID seleccionado sea el utilizado en los pasos anteriores.
1. En **Informes** (en el lado izquierdo de la página), seleccione **Conversión personalizada**, luego **Conversión personalizada 1-10** y seleccione la variable correspondiente a `eVar7`

1. Según la versión de Adobe Analytics que utilice, debe esperar una media de 45 minutos para que el informe se actualice con el término de búsqueda utilizado; por ejemplo, berenjena en el ejemplo

## Uso del buscador de contenido (cf#) con marcos de trabajo de Adobe Analytics {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

Inicialmente, cuando se abre un marco de trabajo de Adobe Analytics, el buscador de contenido contiene variables de Analytics predefinidas en:

* Tráfico
* Conversión
* Eventos

Cuando se selecciona un RSID, todas las variables que pertenecen a ese RSID se agregan a la lista.\
`cf#` es necesario para asignar variables de Analytics a las variables de CQ presentes en los diferentes componentes de seguimiento. Consulte Configuración de un marco de trabajo para el seguimiento básico.

Según la vista seleccionada para el marco de trabajo, el buscador de contenido se rellenará con variables de Analytics (en la vista de AEM) o variables CQ (en la vista de Analytics).

La lista se puede manipular de las siguientes maneras:

1. En **AEM view**, la lista se puede filtrar según el tipo de variable que se seleccione con los tres botones de filtro:

   * Si *no hay ningún botón* seleccionado, la lista muestra la lista completa.
   * Si el botón **Tráfico** está seleccionado, la lista solo mostrará las variables que pertenecen a la sección Tráfico.
   * Si el botón **Conversión** está seleccionado, la lista solo mostrará las variables que pertenecen a la sección Conversión.
   * Si se selecciona el botón **Events**, la lista solo mostrará las variables que pertenecen a la sección Events.

   >[!NOTE]
   >
   >Solo puede haber un botón de filtro activo a la vez.

   1. La lista también tiene una función de búsqueda que filtra los elementos según el texto introducido en el campo de búsqueda.
   1. Si se activa una opción de filtro al buscar elementos en la lista, los resultados mostrados se filtrarán también según el botón activo.
   1. La lista se puede volver a cargar en cualquier momento con el botón de flechas giratorias.
   1. Si se seleccionan varios RSID en el marco de trabajo, todas las variables de la lista se mostrarán con todas las etiquetas utilizadas dentro de los RSID seleccionados.

1. En la vista Adobe Analytics, el Buscador de contenido muestra todas las variables de CQ que pertenecen a los componentes de seguimiento arrastrados en la vista CQ.

   * Por ejemplo, en caso de que **Download component** sea el *único arrastrado* en la vista CQ (que tiene dos variables asignables *eventdata.downloadLink* y *eventdata.events.startDownload*), el buscador de contenido tendrá este aspecto al cambiar a la vista Adobe Analytics:

   ![aa-22](assets/aa-22.png)

   * Las variables se pueden arrastrar y soltar en cualquier variable de Adobe Analytics que pertenezca a una de las tres secciones de variables (**Tráfico**, **Conversión** y **Eventos**).

   * Al arrastrar un nuevo componente de seguimiento al marco de trabajo en la vista CQ, las variables CQ que pertenecen al componente se agregan automáticamente al Buscador de contenido (cf#) en la vista Adobe Analytics.

   >[!NOTE]
   >
   >Solo se puede asignar una variable de CQ a una variable de Adobe Analytics en un momento dado.

## Uso de las vistas AEM y Analytics {#using-aem-view-and-analytics-view}

En cualquier momento dado, los usuarios pueden cambiar entre dos formas de ver las asignaciones de Adobe Analytics en una página de marco de trabajo. Las dos vistas proporcionan una mejor visión general de las asignaciones dentro del marco, desde dos perspectivas distintas.

### Vista de AEM {#aem-view}

![aa-23](assets/aa-23.png)

Tomando la imagen anterior como ejemplo, la **vista de AEM** tiene las siguientes propiedades:

1. Esta es la vista predeterminada cuando se abre el marco de trabajo.
1. Izquierda: el buscador de contenido (cf#) se rellena con variables de Adobe Analytics basadas en los RSID seleccionados.
1. Encabezados de fichas (**vista de AEM** y **vista de Analytics**): úselos para cambiar entre las dos vistas.

1. **Vista de AEM**:

   1. Si el marco de trabajo tiene componentes heredados de su elemento principal, se enumerarán aquí, junto con las variables asignadas a los componentes.

      1. Los componentes heredados están bloqueados.
      1. Para desbloquear un componente heredado, haga doble clic en el candado situado junto al nombre del componente
      1. Para revertir la herencia, elimine el componente desbloqueado; después, recuperará su estado de bloqueado.

   1. **Arrastre los componentes aquí para incluirlos en el marco de análisis**: los componentes se pueden arrastrar desde Sidekick y soltar aquí.
   1. Puede encontrar todos los componentes que están incluidos actualmente en el marco de Analytics:

      1. Para agregar un componente, arrastre uno desde la pestaña Componentes de la barra de tareas
      1. Para eliminar un componente y todas sus asignaciones, seleccione Eliminar en el menú contextual del componente y, a continuación, acepte la eliminación en el cuadro de diálogo de confirmación.
      1. Tenga en cuenta que un componente solo se puede eliminar del marco en el que se creó y no se puede eliminar de los marcos secundarios en el sentido tradicional (solo se pueden sobrescribir).

### Vista de Analytics {#analytics-view}

![aa-24](assets/aa-24.png)

1. Se puede acceder a esta vista cambiando a la pestaña **Analytics view** del marco de trabajo.
1. Izquierda: el buscador de contenido (cf#) se rellena con variables CQ basadas en los componentes arrastrados al marco de trabajo en la vista CQ.
1. Encabezados de fichas (**vista de AEM** y **vista de Analytics**): úselos para cambiar entre las dos vistas.

1. Las tres tablas (Tráfico, Conversión, Evento) enumeran todas las variables de Adobe Analytics disponibles. pertenecen a los RSID seleccionados. Las asignaciones que se muestran aquí deben ser las mismas que en la vista de AEM:

   * **Tráfico**:

      * Variable de tráfico (`prop1`) asignada a una variable de CQ (`eventdata.downloadLink`)

      * Cuando el componente tiene un candado junto a él, significa que se hereda de un marco principal y, por lo tanto, no se puede editar

   * **Conversión**:

      * Variable de conversión (`eVar1`) asignada a una variable de CQ (`pagedata.title`)

      * La variable de conversión (`eVar3`) asignada a una expresión de JavaScript se agregó en línea al hacer doble clic en el campo de la variable CQ e ingresar el código manualmente

   * **Evento**:

      * Variable de evento (`event1`) asignada a un evento CQ ( `eventdata.events.pageView`)

>[!NOTE]
>
>La columna de variable CQ de cualquier tabla también se puede rellenar en línea, haciendo doble clic en el campo y agregándole texto. Estos campos aceptan JavaScript como entrada.
>
>Por ejemplo, junto a `prop3` puede agregar lo siguiente:
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
>para enviar el *título* de una página concatenada con su *sección del sitio* usando *:* (dos puntos) y con el prefijo *Adobe* como `prop3`
>

>[!CAUTION]
>
>Solo se puede asignar una variable de CQ a una variable de Adobe Analytics en un momento dado.
