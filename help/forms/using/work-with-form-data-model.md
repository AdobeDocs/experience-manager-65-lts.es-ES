---
title: Trabajar con el modelo de datos de formulario
description: La integración de datos proporciona un editor de modelos de datos de formulario para configurar y trabajar con modelos de datos de formulario.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: e95c4cc4-1800-4bd8-a3c4-c6c868a1276d
source-git-commit: 30ec8835be1af46e497457f639d90c1ee8b9dd6e
workflow-type: tm+mt
source-wordcount: '4168'
ht-degree: 95%

---

# Trabajar con el modelo de datos de formulario{#work-with-form-data-model}

## Se aplica a {#applies-to}

Esta documentación se aplica a **AEM 6.5 LTS Forms**.

Para obtener documentación de AEM as a Cloud Service, consulte [AEM Forms en Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/work-with-form-data-model.html?lang=es).

![data-integration](do-not-localize/data-integeration.png)

El editor del modelo de datos de formulario proporciona una interfaz de usuario intuitiva y herramientas para editar y configurar un modelo de datos de formulario. Con el editor, se pueden agregar y configurar objetos, propiedades y servicios del modelo de datos desde fuentes de datos asociadas en el modelo de datos de formulario. Además, permite crear objetos y propiedades de modelos de datos sin fuentes de datos y enlazarlos posteriormente con objetos y propiedades de modelos de datos respectivos. También puede generar y editar datos de muestra para propiedades de objetos del modelo de datos que puede utilizar para prerrellenar formularios adaptables y comunicaciones interactivas al previsualizar. Puede probar los objetos y servicios del modelo de datos configurados en un modelo de datos de formulario para asegurarse de que está correctamente integrado con las fuentes de datos.

Si acaba de empezar con la integración de datos de Forms y no ha configurado una fuente de datos o creado un modelo de datos de formulario, consulte los temas siguientes:

* [Integración de datos de AEM Forms](/help/forms/using/data-integration.md)
* [Configurar fuentes de datos](/help/forms/using/configure-data-sources.md)
* [Crear un modelo de datos de formulario](/help/forms/using/create-form-data-models.md)

Continúe leyendo para obtener más información sobre las diversas tareas y configuraciones que puede realizar con el editor del modelo de datos de formulario.

>[!NOTE]
>
>Debe ser miembro de los grupos **fdm-author** y **forms-user** para poder crear y trabajar con el modelo de datos de formulario. Póngase en contacto con su administrador de AEM para convertirse en miembro de los grupos.

## Agregar objetos y servicios del modelo de datos {#add-data-model-objects-and-services}

Si ha creado un modelo de datos de formulario con fuentes de datos, puede utilizar el editor del modelo de datos de formulario para agregar objetos y servicios del modelo de datos, configurar sus propiedades, crear asociaciones entre objetos del modelo de datos y probar el modelo de datos de formulario y los servicios.

Puede agregar objetos y servicios del modelo de datos desde fuentes de datos disponibles en el modelo de datos de formulario. Cuando los objetos del modelo de datos agregados aparecen en la pestaña Modelo, los servicios que se hayan añadido aparecen en la pestaña Servicios.

Para agregar objetos y servicios del modelo de datos:

1. Inicie sesión en la instancia de autor de AEM, vaya a **[!UICONTROL Formularios > Integraciones de datos]** y abra el modelo de datos de formulario en el que desea agregar objetos.
1. En el panel Fuentes de datos, amplíe las opciones para ver los objetos y servicios disponibles del modelo de datos.
1. Seleccione los objetos y servicios del modelo de datos que desee agregar al modelo de datos de formulario y seleccione **[!UICONTROL Agregar selección]**.

   ![selected-objects](assets/selected-objects.png)

   Objetos y servicios del modelo de datos seleccionado

   >[!NOTE]
   >
   > Si el modelo de datos de Forms contiene un objeto que es una palabra clave reservada para la base de datos relacional, puede provocar problemas de adición, actualización o recuperación de datos. Por lo tanto, evite utilizar estos objetos en el modelo de datos de formulario.

   La pestaña Modelo muestra una representación gráfica de todos los objetos del modelo de datos y sus propiedades agregadas al modelo de datos de formulario. Cada objeto del modelo de datos se representa mediante un cuadro en el modelo de datos de formulario.

   ![model-tab](assets/model-tab.png)

   La pestaña Modelo muestra los objetos del modelo de datos agregados

   >[!NOTE]
   >
   >Puede mantener y arrastrar cuadros de objetos del modelo de datos alrededor para organizarlos en el área de contenido. Todos los objetos del modelo de datos agregados en el modelo de datos de formulario aparecen atenuados en el panel Fuentes de datos.

   La pestaña Servicios enumera los servicios añadidos.

   ![services-tab](assets/services-tab.png)

   La pestaña Servicios muestra los servicios del modelo de datos

   >[!NOTE]
   >
   >Además de los objetos y servicios del modelo de datos, el documento de metadatos del servicio OData incluye propiedades de navegación que definen la asociación entre dos objetos del modelo de datos. Para obtener más información, consulte [Uso de las propiedades de navegación de los servicios de OData](#work-with-navigation-properties-of-odata-services).

1. Selecciona **[!UICONTROL Guardar]** para guardar el objeto del modelo de formulario.

   >[!NOTE]
   >
   >Puede invocar los servicios que configuró en la pestaña Servicios de un modelo de datos de formulario mediante las reglas de los formularios adaptables. Los servicios configurados están disponibles en la acción Invocar servicios del editor de reglas. Para obtener más información sobre el uso de estos servicios en las reglas de los formularios adaptables, consulte las reglas Invoke service y Set Value Of en el [editor de reglas](/help/forms/using/rule-editor.md).

## Crear objetos del modelo de datos y propiedades secundarias {#create-data-model-objects-and-child-properties}

### Crear objetos del modelo de datos {#create-data-model-objects}

Aunque puede agregar objetos de modelo de datos desde fuentes de datos configuradas, también puede crear objetos o entidades de modelo de datos sin fuentes de datos. Resulta útil, especialmente si no se han configurado fuentes de datos en el modelo de datos de formulario.

Para crear un objeto de modelo de datos sin fuentes de datos:

1. Inicie sesión en la instancia de autor de AEM, vaya a **[!UICONTROL Formularios > Integraciones de datos]** y abra el modelo de datos de formulario en el que desea crear una entidad u objeto del modelo de datos.
1. Selecciona **[!UICONTROL Crear entidad]**.
1. En el cuadro de diálogo Crear modelo de datos, especifique un nombre para el objeto del modelo de datos y seleccione **[!UICONTROL Agregar]**. Se agrega un objeto de modelo de datos al modelo de datos de formulario. El objeto del modelo de datos recién agregado no está enlazado a una fuente de datos y no tiene propiedades como se muestra en la siguiente imagen.

   ![new-entity](assets/new-entity.png)

A continuación, puede agregar propiedades secundarias en objetos del modelo de datos no enlazados.

### Agregar propiedades secundarias {#child-properties}

El editor del modelo de datos de formulario permite crear propiedades secundarias en un objeto del modelo de datos. La propiedad cuando se crea no está enlazada a ninguna propiedad de una fuente de datos. Posteriormente, puede enlazar la propiedad secundaria con otra propiedad del objeto del modelo de datos que la contiene.

Para crear una propiedad secundaria:

1. En un modelo de datos de formulario, selecciona un objeto de modelo de datos y selecciona **[!UICONTROL Crear propiedad secundaria]**.
1. En el cuadro de diálogo **[!UICONTROL Crear propiedad secundaria]**, especifique un nombre y un tipo de datos para la propiedad en los campos **[!UICONTROL Nombre]** y **[!UICONTROL Tipo]**, respectivamente. Si lo desea, puede especificar un título y una descripción para la propiedad.
1. Habilite la opción Calculada si la propiedad es una propiedad calculada. El valor de una propiedad calculada se evalúa en función de una regla o una expresión. Para obtener más información, consulte [Editar propiedades](#edit-properties).
1. Si el objeto del modelo de datos está enlazado a una fuente de datos, la propiedad secundaria agregada se enlazará automáticamente a la propiedad del objeto del modelo de datos principal con el mismo nombre y tipo de datos.

   Para enlazar manualmente una propiedad secundaria con una propiedad de objeto del modelo de datos, selecciona el icono de examinar situado junto al campo **[!UICONTROL Referencia de enlace]**. El cuadro de diálogo **[!UICONTROL Seleccionar objeto]** enumera todas las propiedades del objeto del modelo de datos principal. Selecciona una propiedad con la que enlazar el objeto y selecciona el icono del tic. Tenga en cuenta que solo puede seleccionar una propiedad del mismo tipo de datos que la propiedad secundaria.

1. Selecciona **[!UICONTROL Listo]** para guardar la propiedad secundaria y selecciona **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario. La propiedad secundaria se agrega ahora al objeto del modelo de datos.

Después de crear objetos y propiedades del modelo de datos, puede seguir creando formularios adaptables y comunicaciones interactivas basados en el modelo de datos de formulario. Posteriormente, cuando haya fuentes de datos disponibles y configuradas, puede enlazar el modelo de datos de formulario con ellas. El enlace se actualizará automáticamente en los formularios adaptables y comunicaciones interactivas asociados. Para obtener más información sobre la creación de formularios adaptables y comunicaciones interactivas mediante el modelo de datos de formulario, consulte [Uso del modelo de datos de formulario](/help/forms/using/using-form-data-model.md).

### Enlazar objetos y propiedades del modelo de datos {#bind-data-model-objects-and-properties}

Cuando las fuentes de datos que desea integrar con el modelo de datos de formulario están disponibles, puede agregarlas al modelo tal y como se describe en [Actualizar fuentes de datos](/help/forms/using/create-form-data-models.md#update). A continuación, haga lo siguiente para enlazar los objetos y propiedades del modelo de datos independiente:

1. En el modelo de datos de formulario, seleccione la fuente de datos independiente que desea enlazar con una fuente de datos.
1. Selecciona **[!UICONTROL Editar propiedades]**.
1. En el panel **[!UICONTROL Editar propiedades]**, selecciona el icono de examinar situado junto al campo **[!UICONTROL Enlace]**. Abre el cuadro de diálogo **[!UICONTROL Seleccionar objeto]** que enumera las fuentes de datos agregadas en el modelo de datos de formulario.

   ![select-object](assets/select-object.png)

1. Despliega el árbol de fuentes de datos, selecciona un objeto del modelo de datos con el que enlazar y selecciona el icono del tic.
1. Selecciona **[!UICONTROL Listo]** para guardar las propiedades y, a continuación, selecciona **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario. El objeto del modelo de datos ahora está enlazado con una fuente de datos. Observe que el objeto del modelo de datos ya no está marcado como No enlazado.

   ![bound-model-object](assets/bound-model-object.png)

## Configurar servicios {#configure-services}

Para leer y escribir para un objeto de modelo de datos, haga lo siguiente para configurar los servicios de lectura y escritura:

1. Selecciona la casilla de verificación situada en la parte superior de un objeto del modelo de datos para seleccionarlo y seleccione **[!UICONTROL Editar propiedades]**.

   ![edit-properties](assets/edit-properties.png)

   Editar propiedades para configurar los servicios de lectura y escritura de un objeto de modelo de datos

   Se abre el cuadro de diálogo Editar propiedades.

   ![edit-properties-2](assets/edit-properties-2.png)

   Cuadro de diálogo Editar propiedades

   >[!NOTE]
   >
   >Además de los objetos y servicios del modelo de datos, el documento de metadatos del servicio OData incluye propiedades de navegación que definen la asociación entre dos objetos del modelo de datos. Cuando se agrega una fuente de datos del servicio OData a un modelo de datos de formulario, hay un servicio disponible en el modelo para todas las propiedades de navegación de un objeto del modelo de datos. Puede utilizar este servicio para leer las propiedades de navegación del objeto del modelo de datos correspondiente.
   >
   >
   >Para obtener más información sobre el uso del servicio, consulte [Uso de las propiedades de navegación de los servicios de OData](#work-with-navigation-properties-of-odata-services).

1. Cambie a **[!UICONTROL Objeto de nivel superior]** para especificar si el objeto del modelo de datos es de nivel superior.

   Los objetos de modelo de datos configurados en un modelo de datos de formulario están disponibles para su uso en la pestaña Objetos del modelo de datos del explorador de contenido de un formulario adaptable basado en el modelo de datos del formulario. Cuando se agrega una asociación entre dos objetos del modelo de datos, el objeto del modelo de datos con el que se asocia se anida en el objeto del modelo de datos que se asocia en la pestaña Objetos del modelo de datos. Si el modelo de datos anidado es un objeto de nivel superior, también aparecerá por separado en la pestaña Objetos del modelo de datos. Por lo tanto, se verán dos entradas, una dentro y otra fuera de la jerarquía anidada, que pueden confundir a los autores del formulario. Para que el objeto del modelo de datos asociado aparezca solo en la jerarquía anidada, desactive la propiedad Objeto de nivel superior.

1. Seleccione los servicios de lectura y escritura para los objetos del modelo de datos seleccionado. Aparecen los argumentos de los servicios.

   ![read-write-services](assets/read-write-services.png)

   Servicios de lectura y escritura configurados para la fuente de datos de los empleados

1. Selecciona ![aem_6_3_edit](assets/aem_6_3_edit.png) en el argumento de servicio de lectura para [enlazar el argumento a un atributo de perfil de usuario, atributo de solicitud o valor literal](#bindargument) y especifica el valor de enlace.
1. Selecciona **[!UICONTROL Listo]** para guardar el argumento, **[!UICONTROL Listo]** para guardar las propiedades y, a continuación, **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

### Vincular argumentos del servicio de lectura {#bindargument}

Enlace el argumento del servicio de lectura a un atributo de perfil de usuario, atributo de solicitud o valor literal basado en un valor de enlace. El valor se pasa al servicio como un argumento para recuperar detalles asociados con el valor especificado de la fuente de datos.

#### Valor literal {#literal-value}

Seleccione **[!UICONTROL Literal]** en el menú desplegable **[!UICONTROL Enlace a]** e indique un valor en el campo **[!UICONTROL Valor de enlace]**. Los detalles asociados con el valor se recuperan de la fuente de datos. Utilice esta opción para recuperar los detalles asociados a un valor estático.

En este ejemplo, los detalles asociados con **4367655678**, como el valor del argumento `mobilenum`, se recuperan de la fuente de datos. Los detalles asociados si transfiere el valor de un argumento de número móvil pueden incluir propiedades como nombre de cliente, dirección de cliente y ciudad.

![Valor literal](assets/fdm_binding_literal_new.png)

#### Atributo de perfil de usuario {#user-profile-attribute}

Seleccione **[!UICONTROL Atributo de perfil de usuario]** del menú desplegable **[!UICONTROL Enlace a]** e indique el nombre del atributo en el campo **[!UICONTROL Valor de enlace]**. Los detalles del usuario que ha iniciado sesión en la instancia de AEM se recuperan de la fuente de datos en función del nombre del atributo.

El nombre de atributo especificado en el campo **[!UICONTROL Valor de enlace]** debe incluir la ruta de enlace completa hasta el nombre de atributo del usuario. Abra la siguiente URL para acceder a los detalles del usuario sobre CRXDE:

`https://[server-name]:[port]/crx/de/index.jsp#/home/users/`

![Perfil de usuario](assets/binding_crxde_user_profile_new.png)

En este ejemplo, especifique `profile.empid` en el campo **[!UICONTROL Valor de enlace]** para el usuario `grios`.

![Editar argumento](assets/edit_argument_user_profile_new.png)

El argumento `id` toma el valor del atributo `empid` del perfil de usuario y lo pasa como argumento al servicio de lectura. Lee y devuelve valores de propiedades asociadas a partir del objeto del modelo de datos de empleado para `empid` asociado al usuario que ha iniciado sesión.

#### Solicitar atributo {#request-attribute}

Utilice el atributo de solicitud para recuperar las propiedades asociadas de la fuente de datos.

1. Seleccione **[!UICONTROL Atributo de solicitud]** del menú desplegable **[!UICONTROL Enlace a]** e indique el nombre del atributo en el campo **[!UICONTROL Valor de enlace]**.

1. Cree una [superposición](../../../help/sites-developing/overlays.md) para head.jsp. Para crear la superposición, abra CRX DE y copie el archivo `https://<server-name>:<port number>/crx/de/index.jsp#/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp` en `https://<server-name>:<port number>/crx/de/index.jsp#/apps/fd/af/components/page2/afStaticTemplatePage/head.jsp`. 

   >[!NOTE]
   >
   >* Si utiliza una plantilla estática, superponga head.jsp en:
   >  `/libs/fd/af/components/page2/afStaticTemplatePage/head.jsp`
   >* Si utiliza una plantilla editable, superponga aftemplatedpage.jsp en:
   >  `/libs/fd/af/components/page2/aftemplatedpage/aftemplatedpage.jsp`

1. Establezca [!DNL paramMap] para el atributo de solicitud. Por ejemplo, incluya el siguiente código en el archivo .jsp de la carpeta de aplicaciones:

   ```javascript
   <%Map paraMap = new HashMap();
    paraMap.put("<request_attribute>",request.getParameter("<request_attribute>"));
    request.setAttribute("paramMap",paraMap);
   ```

   Por ejemplo, utilice el siguiente código para recuperar el valor de petid de la fuente de datos:


   ```javascript
   <%Map paraMap = new HashMap();
   paraMap.put("petId",request.getParameter("petId"));
   request.setAttribute("paramMap",paraMap);%>
   ```

Los detalles se recuperan de la fuente de datos en función del nombre de atributo especificado en la solicitud.

Por ejemplo, si especifica el atributo como `petid=100` en la solicitud, se recuperan las propiedades asociadas al valor del atributo desde la fuente de datos.

## Agregar asociaciones {#add-associations}

Normalmente, hay asociaciones creadas entre objetos del modelo de datos en una fuente de datos. La asociación puede ser de uno a uno o de uno a varios. Por ejemplo, puede haber varios dependientes asociados a un empleado. Se denomina asociación de uno a varios y se representa mediante `1:n` en la línea que conecta los objetos del modelo de datos asociados. Sin embargo, si una asociación devuelve un nombre de empleado único para un ID de empleado determinado, se denomina asociación uno a uno.

Cuando se agregan objetos del modelo de datos asociados en una fuente de datos a un modelo de datos de formulario, sus asociaciones se retienen y se muestran como conectadas mediante líneas de flecha. Puede agregar asociaciones entre objetos del modelo de datos en distintas fuentes de datos en un modelo de datos de formulario.

>[!NOTE]
>
>Las asociaciones predefinidas en una fuente de datos JDBC no se conservan en el modelo de datos de formulario. Créelos manualmente.

Para agregar una asociación:

1. Selecciona la casilla de verificación situada en la parte superior de un objeto del modelo de datos para seleccionarlo y selecciona **[!UICONTROL Agregar asociación]**. Se abre el cuadro de diálogo Agregar asociación.

   ![add-association](assets/add-association.png)

   >[!NOTE]
   >
   >Además de los objetos y servicios del modelo de datos, el documento de metadatos del servicio OData incluye propiedades de navegación que definen la asociación entre dos objetos del modelo de datos. Puede utilizar estas propiedades de navegación cuando agregue asociaciones en el modelo de datos de formulario. Para obtener más información, consulte [Uso de las propiedades de navegación de los servicios de OData](#work-with-navigation-properties-of-odata-services).

   Se abre el cuadro de diálogo Agregar asociación.

   ![add-association-2](assets/add-association-2.png)

   Cuadro de diálogo Agregar asociación

1. En el panel Agregar asociación:

   * Especifique un título para la asociación.
   * Seleccione el tipo de asociación — Uno a uno o Uno a varios.
   * Seleccione el objeto del modelo de datos que desea asociar.
   * Seleccione el servicio de lectura para leer los datos del objeto de modelo seleccionado. Aparece el argumento de servicio de lectura. Edite para cambiar el argumento, si es necesario, y enlácelo a la propiedad del objeto del modelo de datos que desea asociar.

   En el siguiente ejemplo, el argumento predeterminado para el servicio de lectura del objeto del modelo de datos de Dependents (dependientes) es `dependentid`.

   ![add-association-example](assets/add-association-example.png)

   El argumento predeterminado para el servicio de lectura de dependientes es dependentid.

   Sin embargo, el argumento debe ser una propiedad común entre el objeto del modelo de datos asociado, que en este ejemplo es `Employeeid`. Por lo tanto, el argumento `Employeeid` debe enlazarse a la propiedad `id` del objeto del modelo de datos Employee (empleado) para recuperar los detalles de dependientes asociados del objeto del modelo de datos Dependents.

   ![add-association-example-2](assets/add-association-example-2.png)

   Argumento y enlace actualizados

   Selecciona **[!UICONTROL Listo]** para guardar el argumento.

1. Selecciona **[!UICONTROL Listo]** para guardar la asociación y, a continuación, **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.
1. Repita los pasos para crear más asociaciones según sea necesario.

>[!NOTE]
>
>La asociación agregada aparece en el cuadro de objetos del modelo de datos con el título especificado y una línea que conecta los objetos del modelo de datos asociados.
>
>Para editar una asociación, selecciona la casilla de verificación correspondiente y selecciona **[!UICONTROL Editar asociación]**.

![added-association](assets/added-association.png)

## Editar propiedades {#properties}

Puede editar las propiedades de los objetos del modelo de datos, sus propiedades y los servicios que se agreguen en el modelo de datos de formulario.

Para editar propiedades:

1. Active la casilla de verificación situada junto a un objeto de modelo de datos, una propiedad o un servicio del modelo de datos de formulario.
1. Selecciona **[!UICONTROL Editar propiedades]**. Se abre el panel **[!UICONTROL Editar propiedades]** del objeto, de la propiedad o del servicio del modelo seleccionado.

   * **Objeto del modelo de datos**: especifique los servicios de lectura y escritura y edite los argumentos.
   * **Propiedad**: especifique el tipo, subtipo y formato de la propiedad. También puede especificar si la propiedad seleccionada es la clave principal del objeto del modelo de datos.
   * **Servicio**: especifique el objeto del modelo de entrada, el tipo de salida y los argumentos del servicio. Para un servicio Get-Service, puede especificar si se espera que devuelva una matriz.

   ![edit-properties-service](assets/edit-properties-service.png)

   Cuadro de diálogo Editar propiedades para Get-Service

1. Selecciona **[!UICONTROL Listo]** para guardar las propiedades y, a continuación, **[!UICONTROL Guardar]** para guardar el modelo de datos de formulario.

### Crear propiedades calculadas {#computed}

Una propiedad calculada es aquella cuyo valor se calcula en función de una regla o una expresión. Con una regla, puede establecer el valor de una propiedad calculada en una cadena literal, un número, el resultado de una expresión matemática o el valor de otra propiedad en el modelo de datos de formulario.

Por ejemplo, puede crear una propiedad calculada **FullName** cuyo valor es resultado de la concatenación de las propiedades **FirstName** y **LastName**. Para ello:

1. Cree una propiedad con el nombre `FullName` cuyo tipo de datos sea Cadena.
1. Habilita la opción **[!UICONTROL Calculada]** y selecciona **[!UICONTROL Listo]** para crear la propiedad.

   ![computed](assets/computed.png)

   Se crea la propiedad calculada FullName. Fíjese en el icono que aparece junto a la propiedad para mostrar una propiedad calculada.

   ![computed-prop](assets/computed-prop.png)

1. Selecciona la propiedad FullName y selecciona **[!UICONTROL Editar regla]**. Se abre una ventana del editor de reglas.
1. En la ventana del editor de reglas, selecciona **[!UICONTROL Crear]**. Se abre una ventana de la regla **[!UICONTROL Set Value]**.

   En la lista desplegable Seleccionar opción, elija **[!UICONTROL Expresión matemática]**. Otras opciones disponibles son **[!UICONTROL Objeto Modelo de datos de formulario]** y **[!UICONTROL Cadena]**.

1. En la expresión matemática, seleccione **[!UICONTROL FirstName]** y **[!UICONTROL LastName]** en los objetos primero y segundo, respectivamente. Seleccione **[!UICONTROL más]** como operador.

   Selecciona **[!UICONTROL Listo]** y, a continuación, selecciona **[!UICONTROL Cerrar]** para cerrar la ventana del editor de reglas. La regla presenta un aspecto similar al siguiente.

   ![rule](assets/rule.png)

1. En el modelo de datos de formulario, selecciona **[!UICONTROL Guardar]**. La propiedad calculada está configurada.

## Trabajar con propiedades de navegación de los servicios OData {#work-with-navigation-properties-of-odata-services}

En los servicios OData, las propiedades de navegación se utilizan para definir asociaciones entre dos objetos del modelo de datos. Estas propiedades se definen en un tipo de entidad o un tipo complejo. Por ejemplo, en el siguiente extracto del archivo de metadatos de los servicios de muestra OData de [TripPin](https://www.odata.org/blog/trippin-new-odata-v4-sample-service/), la entidad de la persona contiene tres propiedades de navegación: Friends (amigos), BestFriend (mejores amigos) y Trips (viajes).

Para obtener más información sobre las propiedades de navegación, consulte [Documentación de OData](https://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part3-csdl/odata-v4.0-errata03-os-part3-csdl-complete.html#_Toc453752536).

```xml
<edmx:Edmx xmlns:edmx="https://docs.oasis-open.org/odata/ns/edmx" Version="4.0">
<script/>
<edmx:DataServices>
<Schema xmlns="https://docs.oasis-open.org/odata/ns/edm" Namespace="Microsoft.OData.Service.Sample.TrippinInMemory.Models">
<EntityType Name="Person">
<Key>
<PropertyRef Name="UserName"/>
</Key>
<Property Name="UserName" Type="Edm.String" Nullable="false"/>
<Property Name="FirstName" Type="Edm.String" Nullable="false"/>
<Property Name="LastName" Type="Edm.String"/>
<Property Name="MiddleName" Type="Edm.String"/>
<Property Name="Gender" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.PersonGender" Nullable="false"/>
<Property Name="Age" Type="Edm.Int64"/>
<Property Name="Emails" Type="Collection(Edm.String)"/>
<Property Name="AddressInfo" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location)"/>
<Property Name="HomeAddress" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Location"/>
<Property Name="FavoriteFeature" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature" Nullable="false"/>
<Property Name="Features" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Feature)" Nullable="false"/>
<NavigationProperty Name="Friends" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person)"/>
<NavigationProperty Name="BestFriend" Type="Microsoft.OData.Service.Sample.TrippinInMemory.Models.Person"/>
<NavigationProperty Name="Trips" Type="Collection(Microsoft.OData.Service.Sample.TrippinInMemory.Models.Trip)"/>
</EntityType>
```

Al configurar un servicio OData en un modelo de datos de formulario, todas las propiedades de navegación de un contenedor de entidades están disponibles a través de un servicio del modelo. En este ejemplo de servicio OData de TripPin, las tres propiedades de navegación en el contenedor de la entidad `Person` pueden leerse mediante un servicio `GET LINK` en el modelo de datos de formulario.

A continuación se destaca el servicio `GET LINK of Person /People` en el modelo de datos de formulario, que es un servicio combinado para las tres propiedades de navegación en la entidad `Person` del servicio OData de TripPin.

![nav-prop-service](assets/nav-prop-service.png)

Una vez que agregue el servicio `GET LINK` a la pestaña Servicios del modelo de datos de formulario, puede editar las propiedades para elegir el objeto del modelo de salida y la propiedad de navegación a utilizar en el servicio. Por ejemplo, el servicio `GET LINK of Person /People` del siguiente ejemplo utiliza Trip (viaje) como objeto de modelo de salida y la propiedad de navegación como Trips.

![edit-prop-nav-prop](assets/edit-prop-nav-prop.png)

>[!NOTE]
>
>Los valores disponibles en el campo **Valor predeterminado** del argumento **NavigationPropertyName** dependen del estado botón de opción **¿Devolver matriz?**. Cuando se habilita la opción, se muestran las propiedades de navegación del tipo Colección.

En este ejemplo, también puede elegir el objeto del modelo de salida como argumento de propiedad Person (persona) y navegación como Friends o BestFriend (en función de si **¿Devolver matriz?** está habilitada o deshabilitada).

![edit-prop-nav-prop2](assets/edit-prop-nav-prop2.png)

Del mismo modo, puede elegir un servicio de `GET LINK` y configurar sus propiedades de navegación al agregar asociaciones en el modelo de datos de formulario. Sin embargo, para poder seleccionar una propiedad de navegación, asegúrese de que el campo **[!UICONTROL Enlace a]** está configurado como **Literal**.

![add-association-nav-prop](assets/add-association-nav-prop.png)

## Generar y editar datos de muestra {#sample}

El editor del modelo de datos de formulario permite generar datos de ejemplo para todas las propiedades de objetos del modelo de datos, incluidas las propiedades calculadas, en un modelo de datos de formulario. Es un conjunto de valores aleatorios que cumplen con el tipo de datos configurado para cada propiedad. También puede editar y guardar datos, que se conservan incluso si se regeneran los datos de muestra.

Para generar y editar datos de muestra, haga lo siguiente:

1. Abra un modelo de datos de formulario y seleccione **[!UICONTROL Editar datos de ejemplo]**. Genera y muestra los datos de muestra en la ventana Editar datos de muestra.

   ![Generar datos de muestra](assets/form_data_model_generate_sample_data_new.png)

1. En la ventana **[!UICONTROL Editar datos de muestra]**, edita los datos, según sea necesario, y selecciona **[!UICONTROL Guardar]**.

A continuación, puede utilizar los datos de muestra para prerrellenar y probar comunicaciones interactivas basadas en el modelo de datos de formulario. Para obtener más información, consulte [Usar el modelo de datos de formulario](/help/forms/using/using-form-data-model.md).

## Probar objetos y servicios del modelo de datos {#test-data-model-objects-and-services}

El modelo de datos de formulario está configurado, pero antes de ponerlo en uso, es posible que desee comprobar si los objetos y servicios funcionan según lo esperado. Para probar los objetos y servicios del modelo de datos:

1. Seleccione un objeto del modelo de datos o un servicio en el modelo de datos de formulario y seleccione **[!UICONTROL Objeto del modelo de prueba]** o **[!UICONTROL Servicio de prueba]**, respectivamente.

   Se abre la ventana Modelo de datos de formulario de prueba.

   ![test-data-model](assets/test-data-model.png)

1. En la ventana Modelo de datos de formulario de prueba, seleccione el objeto o servicio del modelo de datos que desea probar en el panel Entrada.

1. Especifica un valor de argumento en el código de prueba y selecciona **[!UICONTROL Prueba]**. Una prueba que funcione correctamente devuelve el resultado en el panel Salida.

   ![Resultados de la prueba](assets/test_results_form_data_model_new.png)

Del mismo modo, se pueden probar otros objetos y servicios del modelo de datos de formulario.

## Validación automática de los datos de entrada {#automated-validation-of-input-data}

El modelo de datos de formulario valida los datos recibidos como entrada al invocar la API DermisBridge (según los criterios de validación disponibles en el modelo de datos de formulario). La validación se basa en el indicador `ValidationOptions` establecido en el objeto de consulta que se utiliza para invocar la API.

El indicador se puede establecer en cualquiera de los siguientes valores:

* **COMPLETO**: FDM realiza la validación en función de todas las restricciones.
* **DESACTIVADO**: sin validación.
* **BÁSICO**: FDM realiza la validación en función de las restricciones “requeridas” y “admisibles”

Si no se establece ningún valor para el `ValidationOptions` indicador, se aplica una validación de nivel **BÁSICO** en los datos de entrada.

A continuación se muestra un ejemplo de cómo configurar el indicador de validación en **COMPLETO**:

```java
operationOptions.setValidationOptions(ValidationOptions.FULL);
```

>[!NOTE]
>
>El valor que proporcione para un atributo en los datos de entrada debe coincidir con el tipo de datos definido para el atributo en el documento de metadatos.\
>Si el valor no coincide con el tipo de datos definido para el atributo, la API DermisBridge muestra una excepción independientemente del valor del indicador `ValidationOptions`. Si el nivel de registro está configurado en Depuración, se registra un error en el archivo **error.log**.

El modelo de datos de formulario valida los datos de entrada basándose en una lista de restricciones de tipo de datos. La lista de restricciones para los datos de entrada puede variar en función de la fuente de datos.

En la tabla siguiente se enumeran las restricciones para los datos de entrada en función de la fuente de datos:

<table>
 <tbody> 
  <tr> 
   <td>Restricciones</td> 
   <td>Descripción</td> 
   <td>Fuente de datos de entrada</td> 
  </tr> 
  <tr> 
   <td>required</td> 
   <td>Si es True, el parámetro debe incluirse en los datos de entrada.</td> 
   <td>Swagger, WSDL y base de datos</td> 
  </tr> 
  <tr> 
   <td>nullable</td> 
   <td>Si es True, el valor del parámetro se puede establecer en NULL en los datos de entrada.</td> 
   <td>WSDL, OData y base de datos</td> 
  </tr> 
  <tr> 
   <td>maximum</td> 
   <td>Especifica el límite superior de los valores numéricos. El valor máximo especificado como límite superior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>minimum</td> 
   <td>Especifica el límite inferior de los valores numéricos. El valor mínimo especificado como límite inferior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMaximum</td> 
   <td>Especifica el límite superior de los valores numéricos. El valor máximo especificado como límite superior no debe asignarse al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>exclusiveMinimum</td> 
   <td>Especifica el límite inferior de los valores numéricos. El valor mínimo especificado como límite inferior no debe asignarse al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>minLength</td> 
   <td>Especifica el límite inferior del número de caracteres incluidos en una cadena. El valor mínimo especificado como límite inferior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>maxLength</td> 
   <td>Especifica el límite superior del número de caracteres incluidos en una cadena. El valor máximo especificado como límite superior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger, WSDL, Odata y base de datos</td> 
  </tr> 
  <tr> 
   <td>pattern</td> 
   <td>Especifica una secuencia fija de caracteres. La cadena de entrada solo se valida correctamente si los caracteres se ajustan al patrón especificado.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>minItems</td> 
   <td>Especifica el número mínimo de elementos de una matriz. El valor mínimo especificado como límite inferior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>maxItems</td> 
   <td>Especifica el número máximo de elementos de una matriz. El valor máximo especificado como límite superior también se puede asignar al parámetro en los datos de entrada.</td> 
   <td>Swagger y WSDL</td> 
  </tr> 
  <tr> 
   <td>uniqueItems</td> 
   <td>Si es True, todos los elementos de la matriz deben ser únicos en los datos de entrada.</td> 
   <td>Swagger</td> 
  </tr> 
  <tr> 
   <td>enum (cadena)<br /> <br /> </td> 
   <td>Restringe el valor de un parámetro en los datos de entrada a un conjunto fijo de valores de cadena. Debe ser una matriz con al menos un elemento, donde cada elemento sea único.</td> 
   <td>Swagger, WSDL y OData</td> 
  </tr> 
  <tr> 
   <td>enum (número)<br /> <br /> </td> 
   <td>Restringe el valor de un parámetro en los datos de entrada a un conjunto fijo de valores numéricos. Debe ser una matriz con al menos un elemento, donde cada elemento sea único.</td> 
   <td>WSDL</td> 
  </tr> 
 </tbody> 
</table>

En este ejemplo, los datos de entrada se validan en función de las restricciones máximas, mínimas y requeridas definidas en el archivo Swagger. Los datos de entrada solo cumplen los criterios de validación si el ID de pedido está presente y su valor está entre 1 y 10.

```json
   parameters: [
   {
   name: "orderId",
   in: "path",
   description: "ID of pet that needs to be fetched",
   required: true,
   type: "integer",
   maximum: 10,
   minimum: 1,
   format: "int64"
   }
   ]
```

Se muestra una excepción si los datos de entrada no cumplen los criterios de validación. Si el nivel de registro está configurado en **Depuración**, se registra un error en el archivo **error.log**. Por ejemplo,

```verilog
21.01.2019 17:26:37.411 *ERROR* com.adobe.aem.dermis.core.validation.JsonSchemaValidator {"errorCode":"AEM-FDM-001-044","errorMessage":"Input validations failed during operation execution.","violations":{"/orderId":["numeric instance is greater than the required maximum (maximum: 10, found: 16)"]}}
```

## Pasos siguientes {#next-steps}

Tiene un modelo de datos de formulario en funcionamiento que ya está listo para su uso en flujos de trabajo y comunicaciones interactivas de formularios adaptables. Para obtener más información, consulte [Usar el modelo de datos de formulario](/help/forms/using/using-form-data-model.md).
