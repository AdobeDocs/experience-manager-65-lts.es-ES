---
title: Agregar propiedades personalizadas a los recursos de Administración de correspondencia
description: Obtenga información sobre cómo agregar propiedades personalizadas a recursos de Administración de correspondencia.
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '4434'
ht-degree: 93%

---

# Agregar propiedades personalizadas a los recursos de Administración de correspondencia{#add-custom-properties-to-correspondence-management-assets}

## Información general {#overview}

Puede personalizar la interfaz de usuario de Administración de correspondencia y presentar a los usuarios un conjunto personalizado de propiedades y pestañas. Esta personalización incluye agregar campos, propiedades y pestañas personalizadas a tipos/cartas de recurso específicos o a todos.

## Agregar propiedades personalizadas a los recursos de Administración de correspondencia {#adding-custom-properties-to-correspondence-management-assets}

Los siguientes escenarios muestran cómo se pueden agregar propiedades/pestañas a los recursos y cartas de Administración de correspondencia:

* Agregar una propiedad común a todos los tipos de recursos
* Agregar una pestaña común a todos los tipos de recursos
* Agregar propiedades personalizadas a tipos de recurso específicos

Al modificar las propiedades, las rutas y los valores de estos escenarios, puede agregar propiedades y pestañas personalizadas a un conjunto diferente de recursos según sus necesidades.

### Escenario: agregar un campo común (propiedad) a todos los tipos de recursos {#scenario-adding-a-common-field-property-to-all-the-asset-types}

Este escenario muestra cómo se puede agregar una propiedad personalizada a todos los tipos de recursos (fragmentos de texto, lista, condición y diseño) y a las cartas. En este escenario, se puede agregar una propiedad, la ubicación de los destinatarios, a todos los recursos y cartas. La propiedad Ubicación de los destinatarios ayuda a identificar a qué área geográfica de entrega corresponde un recurso o una carta.

>[!NOTE]
>
>Si ya ha agregado una propiedad personalizada, esta aparecerá en la página Creación de recursos. Para ocultar una propiedad de este tipo, consulte Mostrar u ocultar propiedades personalizadas en las páginas Creación de recursos y Propiedades.

![Se agregó una propiedad personalizada a todos los tipos de recursos](assets/lcoationofrecipientsui.png)

Complete los siguientes pasos para agregar una propiedad personalizada a todos los tipos de recursos y cartas:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada css con una ruta o estructura similares a la carpeta css (en la carpeta ccrui), para hacerlo, siga estos pasos:

   1. Haga clic con el botón derecho en la carpeta Elementos en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![Nodo de superposición](assets/itemsoverlaynode.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

      ![Nodo de superposición](assets/cmmetapropertiesoverlaynode.png)

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. En la carpeta Elementos recién creada, agregue un nodo para la propiedad personalizada en todo el recurso (Ejemplo: GeoLocation), para hacerlo, siga estos pasos:

   1. Haga clic con el botón derecho en la carpeta Elementos y seleccione **Crear** > **Crear nodo**.

      ![Crear nodo en CRX](assets/itemscreatenode.png)

   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** GeoLocation (o el nombre que desee dar a esta propiedad)

      **Tipo:** nt:unstructured

      ![Crear nodo: GeoLocation](assets/geographicallocationcreatenode.png)

   1. Haga clic en el nuevo nodo que ha creado (aquí GeoLocation). CRX muestra las propiedades del nodo.
   1. Agregue las siguientes propiedades al nodo (aquí GeoLocation):

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | fieldLabel | Cadena | El nombre que desea dar al campo/propiedad. (Aquí: Ubicación de los destinatarios) |
      | name | Cadena | `./extendedproperties/GeoLocation` (Mantenga el mismo valor que el nombre de campo creado en el nodo de elementos) |
      | renderReadOnly | Booleano | true |
      | sling:resourceType | Cadena | `granite/ui/components/coral/foundation/form/textfield` |

   1. Haga clic en **Guardar todo**.

1. Para ver la personalización, pase el ratón sobre un recurso (texto, lista, condición o fragmento de diseño) o una carta, haga clic en **Ver propiedades** y haga clic en **Editar**. El nuevo campo (Ubicación de los destinatarios) aparece en la pestaña Básico de las propiedades del recurso o la carta.

   >[!NOTE]
   >
   >Es posible que tenga que borrar la memoria caché del explorador antes de que aparezca la personalización en la interfaz de usuario.

   ![Se ha agregado una propiedad personalizada a todos los recursos](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >Las propiedades comunes de todos los recursos que agregue aparecen en la pestaña básica de las propiedades del recurso. De forma predeterminada, las propiedades comunes agregadas para todos los recursos aparecen en la página Propiedades y en la página Creación de recursos. Para ocultar las propiedades comunes, debe <!--link to show / hide properties]-->.

### Escenario: agregar valores y listas desplegables personalizados a un campo o propiedad personalizado {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

Este escenario muestra cómo se puede agregar una propiedad personalizada a todos los tipos de recursos y agregarle valores desplegables.

1. Haga clic con el botón derecho en la carpeta Elementos en la siguiente ruta y seleccione **Nodo de superposición**:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. En el nodo de superposición recién creado (/apps/fd/cm/ma/gui/content/cmmetadataproperties/commproperties/col1/items) cree un nodo para cada una de las propiedades (campos) para las que necesita crear una lista desplegable (aquí `geographicallocation`) del tipo nt:unstructured.
1. Agregue las siguientes propiedades al nodo (aquí geographicallocation) y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor </strong></td>
   </tr>
   <tr>
      <td>fieldLabel</td>
      <td>Cadena</td>
      <td>El nombre que desea dar al campo/propiedad. (Aquí: geographicallocation)</td>
   </tr>
   <tr>
      <td>name</td>
      <td>Cadena</td>
      <td>./extendedproperties/geographicallocation (Mantenga el valor igual que el nombre de campo que creó en el nodo de elementos)</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>Booleano</td>
      <td>true</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>Cadena</td>
      <td>granite/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. En el nodo de propiedades (aquí geographicallocation), agregue un nuevo nodo con el nombre `items`. Bajo el nodo de elemento, agregue un nodo para cada valor de la lista desplegable. Como práctica recomendada, agregue el primer nodo en blanco para que sirva como valor predeterminado de la lista desplegable y una opción para que el usuario no especifique ningún valor para el campo. Para agregar varias opciones o valores desplegables, repita los siguientes pasos:

   1. Haga clic con el botón derecho en el nodo de propiedades (aquí geographicallocation) y seleccione **Crear** > **Crear nodo**.
   1. Escriba el nombre del campo como `item1,` mantenga el tipo como nt:unstructured y haga clic en **Aceptar**.
   1. Agregue las siguientes propiedades al nodo recién creado (aquí item1) y haga clic en **Guardar todo**:

      <table>
         <tbody>
         <tr>
          <td><strong>Nombre</strong></td>
          <td><strong>Tipo</strong></td>
          <td><strong>Valor </strong></td>
         </tr>
         <tr>
          <td>text</td>
          <td>Cadena</td>
          <td>Este es el valor de la opción desplegable que es visible para el usuario. Deje en blanco el valor en blanco (predeterminado) o introduzca el valor, como <strong>Internacional</strong> o <strong>Dentro de EE. UU.</strong>.<br /> </td>
         </tr>
         <tr>
          <td>valor</td>
          <td>Cadena</td>
          <td>Valor almacenado en CRXDE para el texto. Escriba cualquier palabra clave única. <br /> </td>
         </tr>
         </tbody>
   </table>

   ![customizationdropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

La lista desplegable personalizada aparece de la siguiente manera en las propiedades de los recursos:

![drop-down_customization](assets/drop-down_customization.png)

### Escenario: pestaña común para todos los tipos de recursos {#scenario-common-tab-for-all-asset-types}

Este escenario muestra cómo se puede agregar una pestaña personalizada, Destinatarios, a todos los tipos de recursos (fragmentos de texto, lista, condición y diseño) y a las cartas. En la pestaña Destinatarios puede planificar la colocación de todas las propiedades personalizadas relevantes para los destinatarios.

![Se ha agregado una pestaña personalizada para todos los tipos de recursos](assets/recipientstab.png)

Con el siguiente procedimiento, puede agregar una pestaña con un campo a todos los recursos:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada cmmetadataproperties con una ruta o estructura similares a la carpeta cmmetadataproperties (en la carpeta de contenido), para hacerlo, siga estos pasos:

   1. Haga clic con el botón derecho en la carpeta cmmetadataproperties en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![Nodo de superposición](assets/cmmetadatapropertiesoverlaynode.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      ![Estructura de carpetas de superposición creada en CRX](assets/cmmetadatapropertiesappsfolder.png)

      Haga clic en **Guardar todo**.

1. En la carpeta cmmetadataproperties, agregue un nodo para crear una pestaña personalizada para todos los recursos (Ejemplo: pestaña común). Para hacerlo, siga estos pasos:

   1. Haga clic con el botón derecho en la carpeta cmmetadataproperties y seleccione **Crear** > **Crear nodo**.

      ![Crear nodo](assets/cmmetadatapropertiescreatenode.png)

   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** commontab (o el nombre que desee dar a esta propiedad)

      **Tipo:** nt:unstructured

   1. Haga clic en el nuevo nodo que ha creado (aquí commontab). CRX muestra las propiedades del nodo.
   1. Agregue las siguientes propiedades al nodo (aquí commontab):

      <table>
         <tbody>
         <tr>
          <td><strong>Nombre</strong></td>
          <td><strong>Tipo</strong></td>
          <td><strong>Valor</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>Cadena</td>
          <td>El nombre que desea dar a la columna. (Aquí: Destinatarios)</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>Cadena</td>
          <td>granite/ui/components/coral/foundation/container<br /> </td>
   </tr>
         </tbody>
       </table>

   1. Haga clic en **Guardar todo**.

1. Para el nodo de pestañas creado en el último paso (aquí, commontab), cree un nodo llamado Elementos mediante el siguiente paso:

   1. Haga clic con el botón derecho del ratón en el nodo correspondiente (aquí commontab) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:unstructured

   1. Haga clic en **Guardar todo:**

1. En el nodo Elementos que creó en el paso anterior (en commontab), agregue un nodo para crear una columna (aquí Column1) en la pestaña personalizada (commontab), para hacerlo siga los siguientes pasos (para agregar más columnas, repita este paso):

   1. Haga clic con el botón derecho en el nodo Elementos y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** Column1 (o el nombre que desee dar al nodo: este nombre no aparecerá en la interfaz de usuario).

      **Tipo:** nt:unstructured

   1. Agregue la siguiente propiedad al nodo (aquí Column1) y haga clic en **Guardar todo**:

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor </strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Cadena</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. En el nodo creado en el paso anterior (aquí Column1), agregue un nodo denominado Elementos, para hacerlo, siga los siguientes pasos:

   1. Haga clic con el botón derecho del ratón en el nodo (aquí Column1) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:unstructured

   1. Haga clic en **Guardar todo**.

1. Para crear un campo en la pestaña personalizada (aquí Destinatarios), agregue un nodo (aquí GeographicalLocation). Esta propiedad corresponde a la columna que ha creado. Siga estos pasos para crear el campo (para crear más campos/nodos, repita estos pasos).:

   1. Haga clic con el botón derecho en el nodo Elementos y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** GeographicalLocation (u otro nombre para la propiedad del campo)

      **Tipo:** nt:unstructured

   1. Agregue las siguientes propiedades al nodo de campo (aquí GeographicalLocation) y haga clic en **Guardar todo**.

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | fieldLabel | Cadena | Ubicación de los destinatarios (o el nombre que desee dar al campo ). |
      | name | Cadena | ./extendedproperties/GeographicalLocation |
      | renderReadOnly | Booleano | true |
      | sling:resourceType | Cadena | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. Para agregar esta pestaña para Cartas, cree una carpeta de superposición con una ruta o estructura similar a la siguiente carpeta Elementos en la siguiente ruta:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   Para crear superposición para una carta o un recurso diferente, utilice la siguiente ruta y reemplace [assettype] por text, condition, list, datadictionary o fragment:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. Haga clic con el botón derecho en la carpeta Elementos en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

   1. Haga clic en **Aceptar**. La carpeta se ha creado. Haga clic en **Guardar todo**.

1. En la carpeta Elementos recién creada, agregue un nodo para la pestaña personalizada en el recurso (aquí mytab - este nombre no aparecerá en la interfaz de usuario), para hacerlo, siga los siguientes pasos:

   1. Haga clic con el botón derecho en la carpeta Elementos y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** mytab (o el nombre que desee dar a esta propiedad)

      **Tipo:** nt:unstructured

   1. Haga clic en el nuevo nodo que ha creado (aquí mytab). CRX muestra las propiedades del nodo.
   1. Agregue las dos propiedades siguientes al nodo (aquí customtab):

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor </strong></td>
         </tr>
         <tr>
           <td>path<br /> </td>
           <td>Cadena</td>
           <td>fd/cm/ma/gui/content/cmmetadataproperties/commontab<br /> </td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Cadena</td>
           <td>granite/ui/components/coral/foundation/include<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Haga clic en **Guardar todo**.

1. Para ver la personalización, pase el ratón sobre el recurso correspondiente (aquí Carta), haga clic en Ver propiedades y, a continuación, haga clic en **Editar**. La nueva pestaña (Destinatarios) y el campo (Ubicación de los destinatarios) aparecen en la interfaz de usuario.

   >[!NOTE]
   >
   >Es posible que tenga que borrar la memoria caché del explorador antes de que aparezca la personalización en la interfaz de usuario.

   ![Pestaña personalizada agregada a Cartas](assets/recipientstab-1.png)

### Escenario: agregar propiedades personalizadas para tipos de recursos específicos {#scenario-adding-custom-properties-for-specific-asset-types}

Este escenario muestra cómo se puede agregar una propiedad a un tipo de recurso concreto, como un campo a todos los recursos de texto. Con este proceso, puede agregar propiedades a una de las siguientes opciones:

* Texto
* Condición
* Lista
* Fragmento de diseño
* Diccionario de datos
* Carta

Por ejemplo, solo para los recursos de texto, desea agregar la propiedad Ubicación de los destinatarios, para identificar para qué área geográfica es relevante un recurso.  ![Propiedad personalizada agregada a un recurso](assets/newtabui.png)

Para agregar una propiedad a un tipo de recurso, complete los siguientes pasos:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. Para crear una pestaña en un tipo de recurso (como Texto), cree la siguiente estructura de carpetas en la carpeta de aplicaciones:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [AssetType] = text, condition, list, letter, datadictionary o fragment

   A continuación se indican los pasos para crear esta estructura de carpetas:

   1. Haga clic con el botón derecho en la carpeta Elementos en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      Por ejemplo, si desea crear una propiedad para recursos de texto, seleccione la siguiente carpeta:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![Nodo de superposición](assets/textitemstabsitemsoverlaynode1.png)

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      Haga clic en **Guardar todo**.

1. En la carpeta Elementos recién creada, agregue un nodo para la pestaña personalizada en el recurso (Ejemplo: customtab), para hacerlo, siga estos pasos:

   1. Haga clic con el botón derecho en la carpeta Elementos y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** customtab (o el nombre que desee dar a esta propiedad)

      **Tipo:** nt:unstructured

   1. Haga clic en el nuevo nodo que ha creado (aquí customtab). CRX muestra las propiedades del nodo.
   1. Agregue las dos propiedades siguientes al nodo (aquí customtab):

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | sling:resourceType | Cadena | granite/ui/components/coral/foundation/container |
      | jcr:title | Cadena | El nombre del campo en la interfaz de usuario (aquí My tab) |

   1. Haga clic en **Guardar todo**.

1. En el nodo que ha creado en el paso anterior (aquí customtab), agregue un nodo denominado Elementos, para hacerlo, siga los siguientes pasos:

   1. Haga clic con el botón derecho del ratón en el nodo (aquí customtab) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:unstructured

   1. Haga clic en **Guardar todo**.

1. En el nodo de elementos que creó en el paso anterior (en la pestaña de personalización), agregue un nodo para crear una columna (aquí Column1) en la pestaña personalizada. Para hacerlo, siga los siguientes pasos (para agregar más columnas, repita este paso):

   1. Haga clic con el botón derecho en el nodo Elementos y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** Column1 (o el nombre que desee dar al nodo)

      **Tipo:** nt:unstructured

   1. Agregue la siguiente propiedad al nodo (aquí Column1) y haga clic en **Guardar todo**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor </strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>Cadena</td>
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. Para cada columna que cree (como se especifica en el paso anterior: aquí Column1), cree un nodo llamado Elemento, para hacerlo, siga los siguientes pasos:

   1. Haga clic con el botón derecho en el nodo de columna correspondiente (aquí Column1) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** elementos

      **Tipo:** nt:unstructured

   1. Haga clic en **Guardar todo:**

1. Para cada una de las columnas creadas, cree un nodo en el nodo Elementos para crear un campo en la nueva pestaña de la interfaz de usuario. Repita este paso para crear más campos en la columna:

   1. Haga clic con el botón derecho en el nodo correspondiente (aquí elementos en Column1) y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** un nombre de su elección (aquí GeoLocation)

      **Tipo:** nt:unstructured

   1. Agregue las siguientes propiedades al nodo y haga clic en **Guardar todo**.

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | fieldLabel | Cadena | Ubicación de los destinatarios (o el nombre que desee dar al campo ). |
      | name | Cadena | `./extendedproperties/GeoLocation` |
      | renderReadOnly | Booleano | true |
      | sling:resourceType | Cadena | granite/ui/components/coral/foundation/form/textfield |

1. Para ver la personalización, pase el ratón sobre el recurso correspondiente (aquí un texto), haga clic en Ver propiedades y, a continuación, haga clic en **Editar**. La nueva pestaña y campo (Ubicación de los destinatarios) aparecerán en la interfaz de usuario.

   >[!NOTE]
   >
   >Es posible que tenga que borrar la memoria caché del explorador antes de que aparezca la personalización en la interfaz de usuario.

   ![Propiedad personalizada agregada a un recurso específico](assets/newtabui-1.png)

### Mostrar propiedades personalizadas en la página Creación de recursos {#display-custom-properties-on-the-asset-creation-page}

De forma predeterminada, las propiedades personalizadas agregadas a las pestañas nuevas solo están visibles en la página de propiedades y no en la de creación de recursos, ya que la página de creación de recursos no tiene diseño de pestañas. Para mostrar las propiedades personalizadas en la página Creación de recursos junto con otras propiedades, debe hacer lo siguiente:

1. Haga clic con el botón derecho en la carpeta Elementos en la siguiente ruta y seleccione **Nodo de superposición**:

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores, por carta. Para otros tipos de recursos, la ruta se indica en la siguiente tabla:

   **Ruta:** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items

   **Ubicación:** /apps/

   **Tipos de nodos coincidentes:** Seleccionado

   Según el tipo de recurso, la ruta debe ser la siguiente:

   | **Tipo de recurso/documento** | **Ruta que se agregará** |
   |---|---|
   | Texto | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr:content/body/items/form/items/textwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | Lista | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr:content/body/items/form/items/listwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | Condición | /libs/fd/cm/ma/gui/content/createasset/createcondition/jcr:content/body/items/form/items/conditionwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | Fragmento | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr:content/body/items/form/items/fragmentwizard/items/properties/items/properties/items/tabs2/items/tab1/items |
   | Carta | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items |

1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

1. En el nodo de elementos de superposición que ha creado, cree un nodo con nombre col4 (o cualquier otro nombre) y haga clic en **Guardar todo**.

   Por ejemplo, a continuación se muestra el nodo de superposición creado para las cartas.

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. Agregue las siguientes propiedades al nodo recién creado (aquí col4) y haga clic en **Guardar todo**:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor </strong></td>
  </tr>
  <tr>
   <td>path</td>
   <td>Cadena</td>
   <td><p>Esta ruta indica la columna creada en la siguiente ruta:</p>
    <ul>
     <li>Para la pestaña común de todos los tipos de recursos: /apps/fd/cm/ma/gui/content/cmmetadataproperties/commtab/items/col1</li>
     <li>Para diferentes propiedades para diferentes tipos de recursos: /apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Cadena</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappearinginmainproperties](assets/customfieldappearinginmainproperties.png)

La propiedad personalizada Idioma aparece en la interfaz de usuario para crear una carta

## Personalice la vista de lista para mostrar propiedades personalizadas {#customize-the-list-view-to-show-custom-properties}

Después de agregar una propiedad personalizada a los recursos de Administración de correspondencia, debe realizar más cambios en CRX/DE para asegurarse de que la propiedad personalizada se muestre en la interfaz de usuario de Administración de correspondencia.

Complete los siguientes pasos para mostrar la propiedad personalizada en la interfaz de usuario de la lista de recursos de Administración de correspondencia:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. Cree la siguiente estructura de carpetas en la carpeta de aplicaciones:

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   A continuación se indican los pasos para crear esta estructura de carpetas:

   1. Haga clic con el botón derecho en la carpeta de columnas en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      Haga clic en **Guardar todo**.

1. Para cada una de las propiedades creadas, cree un nodo en el nodo Columns para crear una columna en la interfaz de usuario. Repita este paso para crear más columnas en la interfaz de usuario:

   1. Haga clic con el botón derecho del ratón en el nodo (Columnas) correspondiente y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** un nombre de su elección (aquí GeographicalLocation)

      **Tipo:** nt:unstructured

   1. Agregue las siguientes propiedades al nodo y haga clic en **Guardar todo**.

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor </strong></td>
         </tr>
         <tr>
           <td>jcr:primaryType</td>
           <td>Nombre</td>
           <td><p>nt:unstructured</p> </td>
         </tr>
         <tr>
           <td>jcr:title</td>
           <td>Cadena</td>
           <td><p>GeographicalLocation</p> <p>Este valor aparece como el encabezado de columna en la interfaz de usuario. </p> </td>
         </tr>
         <tr>
           <td>ordenable</td>
           <td>Booleano</td>
           <td><p>true</p> <p>Un valor true significa que el usuario puede ordenar los valores de esta columna. </p> </td>
         </tr>
         </tbody>
       </table>

1. Cree la siguiente estructura de carpetas en la carpeta de aplicaciones:

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   A continuación se indican los pasos para crear esta estructura de carpetas:

   1. Haga clic con el botón derecho en la carpeta de columnas en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

      Haga clic en **Guardar todo**.

1. Copie el archivo childlistpage.jsp desde la siguiente ubicación:

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   Pegue el archivo en la siguiente ubicación:

   /apps//fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/.

1. Abra el archivo childpage.jsp (/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp) y realice los siguientes cambios:

   1. Agregue lo siguiente a la línea 19 del archivo (después de la declaración de copyright).

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. Agregue el siguiente código de una función que obtenga valor para cada propiedad personalizada al final del archivo:

      ```jsp
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. Agregue lo siguiente antes del inicio de la etiqueta &lt;tr> (&lt;tr &lt;%= attrs.build() %>>):

      ```jsp
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      En el código, GeoLocation es el valor que establece en la propiedad Nombre al crear el nodo o campo personalizado. Al crear un nodo o campo personalizado, ha especificado el nombre de la propiedad con ./extendedproperties/ prefix: ./extendedproperties/GeoLocation. En el código, el prefijo no es obligatorio.

   1. Para mostrar la nueva propiedad en la interfaz de usuario, agregue una etiqueta TD como se muestra a continuación antes de la etiqueta de cierre (&lt;/tr>).

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      Para agregar más columnas, repita los pasos 6.3 y 6.4.

   1. Haga clic en **Guardar todo**.

1. Para ver la personalización, abra la vista de lista de fragmentos del documento o las cartas en las que haya agregado la propiedad personalizada.

   La columna IU y la propiedad agregadas en este procedimiento se muestran para todos los tipos de recursos. Sin embargo, los valores de estas propiedades se pueden introducir y mostrar solo para los tipos de recurso para los que agregó originalmente la propiedad personalizada.

   Por ejemplo, con el escenario: Agregar propiedades personalizadas para tipos de recursos específicos agrega una propiedad personalizada a los recursos de texto, puede introducir propiedades personalizadas solo a los recursos de texto. Sin embargo, si muestra esa propiedad personalizada en la interfaz de usuario, aparecerá la columna para todos los tipos de recursos.

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. (Opcional) De forma predeterminada, la nueva columna aparece como la última columna de la interfaz de usuario. Para que la columna aparezca en una posición específica, agregue la siguiente propiedad al nodo de columna:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor </strong></td>
  </tr>
  <tr>
   <td>sling:orderBefore</td>
   <td>Cadena</td>
   <td><p>El nombre del nodo de columna en la ruta “/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns” antes del cual debe aparecer una columna personalizada en la interfaz de usuario.</p> <p>En este caso, si desea que la columna Ubicación geográfica aparezca antes (a la izquierda) de la columna Versión, agregue la propiedad sling:orderBefore al nodo GeoLocation en la ruta “/apps/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns/GeoLocation” y establezca el valor de la propiedad en versión.</p> </td>
  </tr>
 </tbody>
</table>

Cuando agregue la propiedad sling:orderBefore para especificar la ubicación de la columna, también deberá actualizar el orden de las etiquetas &lt;td> especificadas en el paso 6.4 de este procedimiento. Por ejemplo, en este caso, debe asegurarse de que la etiqueta &lt;td> de Ubicación geográfica se coloque antes de la etiqueta &lt;td> de la columna Versión:

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## Habilitar la búsqueda de propiedades personalizadas {#enable-search-for-custom-properties}

De forma predeterminada, la búsqueda de texto completo no incluye propiedades personalizadas que se agregan a la interfaz de usuario mediante CRX/DE.

Para incluir las propiedades personalizadas en la búsqueda, debe permitir la indexación de propiedades personalizadas.

Para permitir la indexación de propiedades personalizadas, complete los siguientes pasos:

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. Vaya a `/oak:index/cmLucene` y agregue un nodo denominado **agregados** bajo ella.

   1. Haga clic con el botón derecho en la carpeta cmLucene y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** agregados

      **Tipo:** nt:unstructured

   1. Haga clic en **Guardar todo**.

1. En la carpeta de agregados recién creada, agregue un nodo cm:resource. Y en cm:resource, agregue un nodo llamado include0.

   1. Haga clic con el botón derecho en la carpeta de agregados y seleccione **Crear** > **Crear nodo**. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** cm:resource

      **Tipo:** nt:unstructured

   1. Haga clic con el botón derecho en la carpeta cm:resource y seleccione **Crear** > **Crear nodo**. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** include0

      **Tipo:** nt:unstructured

   1. Haga clic en el nuevo nodo que ha creado (aquí include0). CRX muestra las propiedades del nodo.
   1. Agregue la siguiente propiedad al nodo (aquí include0):

      <table>
         <tbody>
         <tr>
           <td><strong>Nombre</strong></td>
           <td><strong>Tipo</strong></td>
           <td><strong>Valor </strong></td>
         </tr>
         <tr>
           <td>path</td>
           <td>Cadena</td>
           <td>extendedProperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. Haga clic en **Guardar todo**.

1. Vaya a Propiedades en la siguiente ubicación y agregue una ubicación de nodo debajo de ella: `/oak:index/cmLucene/indexRules/cm:resource/properties`

   Repita este paso para cada una de las propiedades personalizadas que desee agregar a la búsqueda.

   1. Haga clic con el botón derecho en la carpeta de propiedades y seleccione **Crear** > **Crear nodo**.
   1. Asegúrese de que el cuadro de diálogo Crear nodo tiene los siguientes valores y haga clic en **Aceptar**:

      **Nombre:** ubicación (o el nombre de la propiedad personalizada que desee agregar a la búsqueda)

      **Tipo:** nt:unstructured

   1. Haga clic en el nuevo nodo que ha creado (aquí ubicación). CRX muestra las propiedades del nodo.
   1. Agregue las siguientes propiedades al nodo (aquí ubicación):

      | **Nombre** | **Tipo** | **Valor** |
      |---|---|---|
      | analizado | Cadena | true |
      | name | Cadena | ExtendedProperties/location (o el nombre de la propiedad que desee agregar a la búsqueda) |
      | propertyIndex | Booleano | true |
      | useInSuggest | Booleano | true |

   1. Haga clic en **Guardar todo**.

1. Ahora puede utilizar valores de propiedad personalizados en la búsqueda de texto completo para localizar los recursos relevantes.

>[!NOTE]
>
>Si todavía no puede buscar, podría deberse a un problema de indexación. Para volver a indexar, vaya al siguiente nodo y cambie el valor de la propiedad “re-index” a true:
>
>/oak:index/cmLucene” y cambie el valor de la propiedad

## Cambie la vista predeterminada de la página de búsqueda {#change-default-view-of-the-search-page}

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada Lista con una ruta/estructura similar a la carpeta Lista en /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views:

   1. Haga clic con el botón derecho en la carpeta Elementos en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. En el nodo recién creado, agregue la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor </strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Cadena</td>
      <td>tarjeta</td>
   </tr>
   </tbody>
   </table>

1. La personalización muestra los resultados de búsqueda en la vista de lista para todas las consolas, incluidas Formularios y documentos, Recursos y Sites.

## Cambiar la vista predeterminada de la página de recursos {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>Estos pasos cambian la vista predeterminada de todas las consolas, como Formularios y documentos, Recursos y Sites.

1. Vaya a `https://'[server]:[port]'/[ContextPath]/crx/de` e inicie sesión como administrador.
1. En la carpeta de aplicaciones, cree una carpeta denominada Lista con una ruta o estructura similares a la carpeta Lista de:

   /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/

   1. Haga clic con el botón derecho en la carpeta Elementos en la siguiente ruta y seleccione **Nodo de superposición**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. Asegúrese de que el cuadro de diálogo Nodo de superposición tenga los siguientes valores:

      **Ruta:** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list

      **Ubicación:** /apps/

      **Tipos de nodos coincidentes:** Seleccionado

   1. Haga clic en **Aceptar**. La estructura de carpetas se crea en la carpeta de aplicaciones.

   1. Haga clic en **Guardar todo**.

1. En el nodo recién creado, agregue la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor </strong></td>
   </tr>
   <tr>
      <td>sling:orderBefore<br /> </td>
      <td>Cadena</td>
      <td>tarjeta</td>
   </tr>
   </tbody>
   </table>

1. Borre las cookies del explorador o utilice el modo incógnito del explorador para ver los recursos. De forma predeterminada, la página de recursos aparece en el diseño de tarjeta.

## Mostrar u ocultar propiedades personalizadas en las páginas Creación de recursos y Propiedades {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

Para mostrar u ocultar las propiedades personalizadas, complete los siguientes pasos:

1. En el nodo de propiedad personalizada, como geographicallocation, cree un nodo con el nombre &quot;granite:rendercondition&quot; del tipo &quot;nt:unstructured&quot;.
1. Agregue la siguiente propiedad al nodo y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor </strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>Cadena</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. Para ocultar esta propiedad en la página de creación de recursos, agregue la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor </strong></td>
   </tr>
   <tr>
      <td>hideOnCreate<br /> </td>
      <td>Booleano</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

1. Para ocultar la propiedad personalizada en la página de propiedades de los recursos, agregue la siguiente propiedad y haga clic en **Guardar todo**:

   <table>
   <tbody>
   <tr>
      <td><strong>Nombre</strong></td>
      <td><strong>Tipo</strong></td>
      <td><strong>Valor </strong></td>
   </tr>
   <tr>
      <td>hideOnEdit<br /> </td>
      <td>Booleano</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

   Para volver a mostrar los valores, restablezca los valores de las propiedades en `false` o elimine las entradas de la propiedad.
