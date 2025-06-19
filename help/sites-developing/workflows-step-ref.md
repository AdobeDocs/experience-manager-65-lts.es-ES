---
title: Referencia de pasos de flujo de trabajo
description: Consulte esta referencia de paso para flujos de trabajo en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: e82d97c2-c26a-48df-9210-47dc017c68c8
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '3226'
ht-degree: 6%

---

# Referencia de pasos de flujo de trabajo {#workflow-step-reference}

Los modelos de flujo de trabajo constan de una serie de pasos de varios tipos. Según el tipo, estos pasos se pueden configurar y ampliar con parámetros y secuencias de comandos para proporcionar la funcionalidad y el control necesarios.

>[!NOTE]
>
>Esta sección describe los pasos estándar del flujo de trabajo.
>
>Para ver los pasos específicos del módulo, consulte lo siguiente:
>
>* [Referencia de paso de flujo de trabajo de AEM Forms](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [Procesar Assets mediante controladores de medios y flujos de trabajo](/help/assets/media-handlers.md)
>

## Propiedades del paso {#step-properties}

Cada componente del paso tiene un cuadro de diálogo **Propiedades del paso** que le permite definir y editar las propiedades requeridas.

### Propiedades del paso: pestaña Común {#step-properties-common-tab}

Hay disponible una combinación de las siguientes propiedades para la mayoría de los componentes del paso de flujo de trabajo, en la pestaña **Común** del cuadro de diálogo de propiedades:

* **Título**
El título del paso.

* **Descripción**
Una descripción de la etapa.

* **Fase de flujo de trabajo**

  Un selector desplegable para aplicar un [Stage](/help/sites-developing/workflows.md#workflow-stages) al paso.

* **Tiempo de espera**

  Período después del cual se agota el tiempo de espera del paso.
Puede seleccionar entre: **Desactivado**, **Inmediato**, **1h**, **6h**, **12h**, **24h**.

* **Controlador de tiempo de espera**

  Controlador que controla el flujo de trabajo cuando se agota el tiempo de espera del paso. Por ejemplo, `Auto Advancer`

* **Avance de controlador**

  Seleccione esta opción para avanzar automáticamente el flujo de trabajo al siguiente paso después de la ejecución. Si no se selecciona, el script de implementación debe gestionar el avance del flujo de trabajo.

### Propiedades del paso: pestaña Usuario/grupo {#step-properties-user-group-tab}

Las siguientes propiedades están disponibles para muchos componentes de paso del flujo de trabajo, en la pestaña **Usuario/Grupo** del cuadro de diálogo de propiedades:

* **Notificar al usuario por correo electrónico**

   * Notifique a los participantes enviándoles un correo electrónico cuando el flujo de trabajo alcance el paso.
   * Si está habilitada, se envía un correo electrónico al usuario definido por la propiedad **Usuario/Grupo**, o a cada miembro del grupo si se define un grupo.

* **Usuario/grupo**

   * Un cuadro de selección desplegable le permite desplazarse hasta un usuario o grupo y seleccionarlos.
   * Si asigna el paso a un usuario específico, solo este puede actuar en el paso.
   * Si asigna el paso a un grupo completo, cuando el flujo de trabajo llegue a este paso, todos los usuarios de este grupo tendrán la acción en su **Bandeja de entrada de flujo de trabajo**.
   * Consulte [Participación en flujos de trabajo](/help/sites-authoring/workflows-participating.md) para obtener más información.

## División Y {#and-split}

**AND Split** crea una división en el flujo de trabajo, tras la cual ambas ramas están activas. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario. Este paso permite introducir varias rutas de procesamiento en el flujo de trabajo. Por ejemplo, puede permitir que ciertos pasos de revisión se produzcan en paralelo, lo que ahorra tiempo.

![wf-26](assets/wf-26.png)

### División AND: configuración {#and-split-configuration}

Para configurar la división:

* Editar las propiedades de división **AND**:

   * **Split Name**: asigne un nombre para fines explicativos
   * Seleccione el número de ramas necesarias; 2, 3, 4 o 5.

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

  ![wf-27](assets/wf-27.png)

## Etapa del contenedor {#container-step}

Un paso de contenedor inicia otro modelo de flujo de trabajo que se ejecuta como flujo de trabajo secundario.

Este contenedor puede permitirle reutilizar los modelos de flujo de trabajo para implementar secuencias comunes de pasos. Por ejemplo, un modelo del flujo de trabajo de traducción se puede utilizar en varios flujos de trabajo de edición.

![wf-28](assets/wf-28.png)

### Paso del contenedor: configuración {#container-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Contenedor**

   * **Flujo de trabajo secundario**: seleccione el flujo de trabajo que desea iniciar.

## Ir a la etapa {#goto-step}

El **Paso Ir a** le permite especificar el siguiente paso que se ejecutará en el modelo de flujo de trabajo. Puede especificar una definición de regla, un script externo o un script ECMA como expresión de enrutamiento para evaluar el siguiente paso del modelo de flujo de trabajo.

* Si la condición que ha especificado es verdadera, el **Paso Goto** finaliza y el motor de flujo de trabajo ejecuta el paso especificado.
* Si la condición especificada no es verdadera, el **Paso Ir a** finaliza y la lógica de enrutamiento normal determina el siguiente paso que se va a ejecutar.

El **Paso Goto** le permite implementar estructuras de enrutamiento avanzadas en sus modelos de flujo de trabajo. Por ejemplo, para implementar un bucle, el **Paso Goto** se puede definir para ejecutar un paso anterior en el flujo de trabajo, con la expresión de enrutamiento evaluando una condición de bucle.

### Paso Ir a: Configuración {#goto-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Paso de destino**: seleccione el paso que se ejecutará después de evaluar la condición para la expresión de enrutamiento.
   * **Expresión de enrutamiento**: seleccione la definición de regla, el script externo o un script ECMA que determine si se ejecutará el **paso de destino**.

      * **Definición de regla:** Use el [editor de expresiones](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) para definir la regla.
      * **Script externo:** La ruta de acceso del script externo.
      * **Script ECMA**: El script que determina si se ejecutará el **Paso Goto**.

#### Simulación de un bucle for {#simulating-a-for-loop}

La simulación de un &quot;bucle for&quot; requiere que mantenga un recuento del número de iteraciones de bucle que se han producido:

* El recuento suele representar un índice de elementos en los que se actúa en el flujo de trabajo.
* El recuento se evalúa como criterio de salida del bucle.

Por ejemplo, para implementar un flujo de trabajo que realice una acción en varios nodos JCR, puede utilizar un contador de bucle como índice para los nodos. Para mantener el recuento, almacene un valor `integer` en la asignación de datos de la instancia de flujo de trabajo. Para incrementar el recuento y comparar el recuento con los criterios de salida, use el script del **Paso Goto**.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### Simulación de un bucle for mediante la definición de regla {#simulateforloop}

También puede simular un bucle for utilizando la definición de regla como expresión de enrutamiento. [Crear una variable **count**](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) de tipo de datos Long. Use **Expression** como modo de asignación en el paso **[Establecer variable](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** para establecer el valor de la variable **count** en **count + 1** en cada ejecución del paso **Establecer variable**.

![Simulación de un bucle for](assets/variable_use_case_count_new.png)

En el **Paso Goto**, use **Establecer variable** como **Paso de destino** y **count &lt; 5** como expresión de enrutamiento.

![Condición para simular un bucle for](assets/variable_use_case_count1_new.png)

El paso **Establecer variable** se ejecuta repetidamente, incrementando el valor de la variable **count** en 1 en cada ejecución hasta que el valor alcance 5.

## División O {#or-split}

**OR Split** crea una división en el flujo de trabajo, después de la cual solo una rama está activa. Este paso le permite introducir rutas de procesamiento condicionales en su flujo de trabajo. Los pasos del flujo de trabajo se agregan a cada rama según sea necesario.

>[!NOTE]
>
>Ver [paso OR Split](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable)

![Bifurcación mediante OR Split](assets/variables_orsplit_new.png)

### OR Split - Configuración {#or-split-configuration}

Para configurar la división:

* Editar las propiedades de **OR Split**:

   * **Común**

      * Especifique el nombre de la división.

   * **Ramas (*x)***

      * **Agregar rama:** Agregue más ramas al paso.
      * **Seleccionar expresión de enrutamiento**: para evaluar la rama activa, seleccione la expresión de enrutamiento. Los valores posibles incluyen: Definición de regla, Script externo y script ECMA.
      * **Haga clic para agregar expresión**: Agregue expresión para evaluar la rama activa si selecciona **Definición de regla** como expresión de enrutamiento.
      * **Ruta de script**: La ruta a un archivo que contiene el script para evaluar la rama activa si selecciona **Script externo** como expresión de enrutamiento.
      * **Script**: agregue el script en el cuadro para evaluar la rama activa si selecciona **Script ECMA** como expresión de enrutamiento.
      * **Ruta predeterminada**: Si hay varias ramas, se sigue la rama predeterminada. Solo se puede especificar una rama como predeterminada.

  >[!NOTE]
  >
  >    * Se evalúa una rama a la vez en función de la expresión de enrutamiento.
  >    * Las ramas se evalúan de arriba a abajo.
  >    * Se ejecuta el primer script que se evalúa como true.
  >    * Si ninguna rama se evalúa como verdadera, el flujo de trabajo no avanza.
  >
  >

  >[!NOTE]
  >
  >Consulte [Definición de una regla para una división OR](/help/sites-developing/workflows-models.md#defineruleecmascript).

* Añada los pasos del flujo de trabajo a las ramas según sea necesario.

## Pasos y selectores de participantes {#participant-steps-and-choosers}

### Etapa de participante {#participant-step}

Un **Paso de participante** le permite asignar la propiedad de una acción en particular. El flujo de trabajo se ejecuta únicamente cuando el usuario ha reconocido manualmente el paso. Este flujo de trabajo se utiliza cuando desea que alguien actúe en él. Por ejemplo, un paso de revisión.

Aunque no está directamente relacionado, la autorización de usuario debe tenerse en cuenta al asignar una acción; el usuario debe tener acceso a la página que es la carga útil del flujo de trabajo.

#### Etapa de participante: configuración {#participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)

>[!NOTE]
>
>El iniciador del flujo de trabajo siempre recibe una notificación cuando:
>
>* El flujo de trabajo se ha completado (finalizado).
>* El flujo de trabajo se interrumpe (finaliza).
>

>[!NOTE]
>
>Algunas propiedades deben configurarse para habilitar las notificaciones por correo electrónico. También puede personalizar la plantilla de correo electrónico o agregar una plantilla de correo electrónico para un nuevo idioma. Para configurar las notificaciones por correo electrónico en AEM, consulte [Configuración de notificaciones por correo electrónico](/help/sites-administering/notification.md#configuringemailnotification).

### Etapa de participante de cuadro de diálogo {#dialog-participant-step}

Use un **Paso de participante del cuadro de diálogo** para recopilar información del usuario que tiene asignado el elemento de trabajo. Este paso es útil para recopilar pequeñas cantidades de datos que se utilizan más adelante en el flujo de trabajo.

Una vez completado el paso, el cuadro de diálogo **Completar elemento de trabajo** contiene los campos definidos en el cuadro de diálogo. Los datos recopilados en los campos se almacenan en los nodos de la carga útil del flujo de trabajo. Los pasos posteriores del flujo de trabajo pueden leer el valor desde el repositorio.

Para configurar el paso, especifique el grupo o usuario al que asignar el elemento de trabajo y la ruta al cuadro de diálogo.

#### Paso de participante del diálogo: configuración {#dialog-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Cuadro de diálogo**

   * **Ruta de diálogo**: La ruta al nodo de diálogo del [diálogo que ha creado](#dialog-participant-step-creating-a-dialog).

#### Paso de participante del diálogo: Creación de un cuadro de diálogo {#dialog-participant-step-creating-a-dialog}

Para crear un cuadro de diálogo, debe crearlo:

* Decida dónde se almacenan los datos resultantes [en la carga útil](#dialog-participant-step-storing-data-in-the-payload).
* [Defina el cuadro de diálogo; incluye la definición de los campos que se utilizan para recopilar y guardar los datos](#dialog-participant-step-dialog-definition).

#### Paso de participante del cuadro de diálogo: Almacenamiento de datos en la carga útil {#dialog-participant-step-storing-data-in-the-payload}

Puede almacenar datos de widget en la carga útil de flujo de trabajo o en los metadatos del elemento de trabajo. El formato de la propiedad `name` del nodo del widget determina dónde se almacenan los datos.

* **Almacenar datos con la carga útil**

   * Para almacenar datos de widget como una propiedad de la carga útil del flujo de trabajo, utilice el siguiente formato para el valor de la propiedad name del nodo de widget:
     `./jcr:content/nodename`

   * Los datos se almacenan en la propiedad `nodename` del nodo de carga útil. Si el nodo no contiene esa propiedad, se crea la propiedad.
   * Cuando se almacena con la carga útil, los usos posteriores del cuadro de diálogo con la misma carga útil sobrescriben el valor de la propiedad.

* **Almacenar datos con el elemento de trabajo**

   * Para almacenar los datos del widget como una propiedad de los metadatos del elemento de trabajo, utilice el siguiente formato para el valor de la propiedad name:
     `nodename`

   * Los datos se almacenan en la propiedad `nodename` del elemento de trabajo `metadata`. Los datos se conservan si el cuadro de diálogo se utiliza posteriormente con la misma carga útil.

#### Paso de participante del cuadro de diálogo: definición del cuadro de diálogo {#dialog-participant-step-dialog-definition}

1. **Estructura de diálogo**

   Los cuadros de diálogo de los pasos de los participantes del cuadro de diálogo son similares a los cuadros de diálogo que crea para los componentes de creación. Se almacenan en:

   `/apps/myapp/workflow/dialogs`

   Los cuadros de diálogo de la IU táctil estándar tienen la siguiente estructura de nodos:

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   >
   >Consulte [Creación y configuración de un cuadro de diálogo](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog).

1. **Propiedad de ruta de diálogo**

   El **Paso de participante de diálogo** tiene la propiedad **Ruta de diálogo** (junto con las propiedades de un [Paso de participante](#participant-step)). El valor de la propiedad **Dialog Path** es la ruta al nodo `dialog` del cuadro de diálogo.

   Por ejemplo, el cuadro de diálogo está contenido en un componente denominado `EmailWatch` que se almacena en el nodo:

   `/apps/myapp/workflows/dialogs`

   Para la IU táctil, se usa el siguiente valor para la propiedad **Ruta de diálogo**:

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **Ejemplo de definición de diálogo**

   El siguiente fragmento de código XML representa un cuadro de diálogo que almacena un valor `String` en el nodo `watchEmail` del contenido de carga útil. El nodo de título representa el componente [TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html):

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   En la IU táctil, este ejemplo genera un cuadro de diálogo como el siguiente:

   ![chlimage_1-70](assets/chlimage_1-70.png)

### Etapa de participante dinámica {#dynamic-participant-step}

El componente **Paso de participante dinámico** es similar a **[Paso de participante](#participant-step)** con la diferencia de que el participante se selecciona automáticamente en tiempo de ejecución.

Para configurar el paso, seleccione un **Selector de participantes** que identifique al participante al que asignar el elemento de trabajo, junto con un cuadro de diálogo.

#### Etapa de participante dinámica: configuración {#dynamic-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Selector de participantes**

   * **Selector de participantes**: Nombre del [selector de participantes que ha creado](#developingtheparticipantchooser).
   * **Argumentos**: Cualquier argumento requerido.
   * **Correo electrónico**: Indica si se debe enviar una notificación por correo electrónico al usuario.

* **Cuadro de diálogo**

   * **Ruta de diálogo**: La ruta al nodo de diálogo del [cuadro de diálogo que crea (como en el **Paso de participante del cuadro de diálogo**)](#dialog-participant-step-creating-a-dialog).

#### Etapa de participante dinámica: desarrollo del selector de participantes {#dynamic-participant-step-developing-the-participant-chooser}

Puede crear el selector de participantes. Por lo tanto, puede utilizar cualquier lógica o criterio de selección. Por ejemplo, el selector de participantes puede seleccionar el usuario (dentro de un grupo) que tenga menos elementos de trabajo. Puede crear cualquier número de selectores de participantes para utilizarlos con diferentes instancias del componente **Paso de participante dinámico** en sus modelos de flujo de trabajo.

Cree un servicio OSGi o un ECMAScript que seleccione un usuario al que asignar el elemento de trabajo.

* **ECMAscript**

  Los scripts deben incluir una función denominada getParticipant que devuelva un identificador de usuario como un valor `String`. Almacene sus scripts personalizados, por ejemplo, en la carpeta `/apps/myapp/workflow/scripts` o en una subcarpeta.

  Se incluye un script de ejemplo en una instancia de AEM estándar:

  `/libs/workflow/scripts/initiator-participant-chooser.ecma`

  >[!CAUTION]
  >
  >No cambie nada en la ruta de acceso `/libs`.
  >
  >
  >El motivo es que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y se sobrescribirá al aplicar una revisión o un paquete de características).

  Esta secuencia de comandos selecciona el iniciador del flujo de trabajo como participante:

  ```
  function getParticipant() {
      return workItem.getWorkflow().getInitiator();
  }
  ```

  >[!NOTE]
  >
  >El componente **Selector de participantes de iniciador de flujo de trabajo** amplía el **Paso de participante dinámico** y utiliza este script como implementación de paso.

* **Servicio OSGi**

  Los servicios deben implementar la interfaz [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html). La interfaz define los siguientes miembros:

   * Campo `SERVICE_PROPERTY_LABEL`: utilice este campo para especificar el nombre del selector de participantes. El nombre aparece en una lista de selectores de participantes disponibles en las propiedades de **Paso de participante dinámico**.

   * Método `getParticipant`: devuelve el ID principal resuelto dinámicamente como un valor `String`.

  >[!CAUTION]
  >
  >El método `getParticipant` devuelve el identificador principal resuelto dinámicamente. Este ID puede ser un ID de grupo o un ID de usuario.
  >
  >
  >Sin embargo, solo se puede usar un Id. de grupo para un **Paso de participante**, cuando se devuelva una lista de participantes. Para un **paso de participante dinámico**, se devuelve una lista vacía y no se puede usar para la delegación.

  Para que la implementación esté disponible para los componentes de **Dynamic Participant Step**, agregue la clase Java™ a un paquete OSGi que exporte el servicio e implemente el paquete en el servidor de AEM.

  >[!NOTE]
  >
  >**Selector aleatorio de participantes** es un servicio de ejemplo que selecciona un usuario aleatorio (`com.day.cq.workflow.impl.process.RandomParticipantChooser`). El ejemplo de componente **Selección aleatoria de participantes** r amplía el paso **Paso dinámico de participantes** y utiliza este servicio como implementación de paso.

#### Etapa de participante dinámica: ejemplo de servicio de selector de participantes {#dynamic-participant-step-example-participant-chooser-service}

La siguiente clase Java™ implementa la interfaz `ParticipantStepChooser`. La clase devuelve el nombre del participante que inició el flujo de trabajo. El código utiliza la misma lógica que el script de ejemplo (`initiator-participant-chooser.ecma`).

La anotación `@Property` establece el valor del campo `SERVICE_PROPERTY_LABEL` en `Workflow Initiator Participant Chooser`.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

En el cuadro de diálogo de propiedades de **Paso de participante dinámico**, la lista de **Selector de participantes** incluye el elemento `Workflow Initiator Participant Chooser (script)`, que representa este servicio.

Cuando se inicia el modelo de flujo de trabajo, el registro indica el ID del usuario que inició el flujo de trabajo y a quién se asigna el elemento de trabajo. En este ejemplo, el usuario `admin` inició el flujo de trabajo.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### Etapa de participante de formulario {#form-participant-step}

**Paso de participante de formulario** presenta un formulario cuando se abre el elemento de trabajo. Cuando el usuario rellena y envía el formulario, los datos de campo se almacenan en los nodos de la carga útil del flujo de trabajo.

Para configurar el paso, especifique el grupo o usuario al que asignar el elemento de trabajo y la ruta al formulario.

>[!CAUTION]
>
>Esta sección trata sobre la sección [Forms de componentes de base para la creación de páginas](/help/sites-authoring/default-components-foundation.md#form).

#### Paso de participante de formulario: configuración {#form-participant-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* [Usuario/grupo](#step-properties-user-group-tab)
* **Formulario**

   * **Ruta de formulario**: La ruta al [formulario que creó](#form-participant-step-creating-the-form).

#### Paso de participante del formulario: creación del formulario {#form-participant-step-creating-the-form}

Cree un formulario para utilizarlo con un **Paso de participante del formulario** como de costumbre. Sin embargo, los formularios de un paso de participante de formulario deben tener las siguientes configuraciones:

* El componente **Inicio del formulario** debe tener la propiedad **Tipo de acción** establecida en `Edit Workflow Controlled Resource(s)`.
* El componente **Inicio de formulario** debe tener un valor para la propiedad `Form Identifier`.
* Los componentes del formulario deben tener la propiedad **Element Name** establecida en la ruta del nodo donde se almacenan los datos del campo. La ruta debe localizar un nodo en el contenido de carga útil del flujo de trabajo. El valor utiliza el siguiente formato:

  `./jcr:content/path_to_node`

* El formulario debe incluir un componente **Botón de envío del flujo de trabajo**. No se configura ninguna propiedad del componente.

Los requisitos del flujo de trabajo determinan dónde se deben almacenar los datos de campo. Por ejemplo, los datos de campo se pueden utilizar para configurar las propiedades del contenido de la página. El siguiente valor de una propiedad **Element Name** almacena datos de campo como el valor de la propiedad `redirectTarget` del nodo `jcr:content`:

`./jcr:content/redirectTarget`

En el ejemplo siguiente, los datos de campo se utilizan como contenido de un componente **Text** en la página de carga útil:

`./jcr:content/par/text_3/text`

El primer ejemplo se puede utilizar para cualquier página que procese el componente `cq:Page`. El segundo ejemplo solo se puede usar cuando la página de carga útil incluye un componente **Text** con un identificador de `text_3`.

El formulario se puede encontrar en cualquier lugar del repositorio, pero los usuarios del flujo de trabajo deben tener autorización para leer el formulario.

### Selector aleatorio de participantes {#random-participant-chooser}

El paso **Selector aleatorio de participantes** es un selector de participantes que asigna el elemento de trabajo generado a un usuario que se ha seleccionado aleatoriamente de una lista.

![wf-31](assets/wf-31.png)

#### Selector aleatorio de participantes - Configuración {#random-participant-chooser-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Argumentos**

   * **Participantes**: especifica la lista de usuarios disponibles para la selección. Para agregar un usuario a la lista, haga clic en **Agregar elemento** y escriba la ruta de acceso principal del nodo de usuario o el identificador de usuario. El orden de los usuarios no afecta a la probabilidad de que se les asigne un elemento de trabajo.

### Selector de participantes del lanzador de flujo de trabajo {#workflow-initiator-participant-chooser}

El paso **Selector de participantes de iniciador de flujo de trabajo** es un selector de participantes que asigna el elemento de trabajo generado al usuario que inició el flujo de trabajo. No hay propiedades que configurar que no sean las propiedades **Common**.

#### Selector de participantes del iniciador de flujo de trabajo - Configuración {#workflow-initiator-participant-chooser-configuration}

Para configurar el paso, edite utilizando las siguientes pestañas:

* [Común](#step-properties-common-tab)

## Etapa del proceso {#process-step}

Un **paso de proceso** ejecuta un ECMAScript o llama a un servicio OSGi para realizar el procesamiento automático.

![wf-32](assets/wf-32.png)

### Etapa del proceso: configuración {#process-step-configuration}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](#step-properties-common-tab)
* **Proceso**

   * **Proceso**: Implementación de proceso que se va a ejecutar. Utilice el menú desplegable para seleccionar el servicio ECMAScript o OSGi. Para obtener información acerca de:

      * Los servicios estándar ECMAScripts y OSGi, vea [Procesos integrados para pasos de proceso](/help/sites-developing/workflows-process-ref.md).
      * Crear ECMAScripts para un paso del proceso, consulte [Implementación de un paso del proceso con un ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).
      * Creación de servicios OSGi para un paso de proceso, consulte [Implementación de un paso de proceso con una clase Java™](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class).

   * **Avance del controlador**: seleccione esta opción para avanzar automáticamente el flujo de trabajo al siguiente paso después de la ejecución. Si no se selecciona, el script de implementación debe gestionar el avance del flujo de trabajo.
   * **Argumentos**: argumentos que se van a pasar al proceso.

## Establecer variable {#set-variable}

El paso Establecer variable permite establecer el valor de una variable y definir el orden en que se configuran los valores. La variable se configura en el orden en que se enumeran las asignaciones de variables en el paso Establecer variable.

![Agregar asignación para establecer una variable](assets/set_variable_addmappingnew.png)

### Establecer variable - Configuración {#setvariable}

Para configurar el paso, edite y utilice las siguientes pestañas:

* [Común](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **Asignación**

   * **Seleccionar variable:** Utilice esta opción para seleccionar una variable y establecer su valor.
   * **Seleccionar modo de asignación:** Para establecer el valor de la variable, seleccione un modo de asignación. Según el tipo de datos de la variable, puede utilizar las siguientes opciones para establecer su valor:

      * **Literal:** utilice la opción cuando conozca el valor exacto que desea especificar.
      * **Expresión:** utilice la opción cuando el valor que se va a utilizar se calcule en función de una expresión. La expresión se crea en el editor de expresiones proporcionado.
      * **Notación de puntos JSON:** Utilice la opción para recuperar un valor de una variable de tipo JSON o FDM.
      * **XPATH:** Utilice la opción para recuperar un valor de una variable de tipo XML.
      * **En relación con la carga útil:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta relativa a la carga útil.
      * **Ruta absoluta:** Utilice la opción cuando el valor que se va a guardar en la variable esté disponible en una ruta absoluta.

   * **Especificar valor:** Para asignar a la variable, especifique un valor. El valor que especifique en este campo depende del modo de asignación.
   * **Agregar asignación:** Utilice esta opción para agregar más asignaciones y establecer un valor para la variable.
