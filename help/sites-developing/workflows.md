---
title: Desarrollo y ampliación de flujos de trabajo
description: AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo y para interactuar mediante programación con flujos de trabajo
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 625affd0-0e1a-4db8-812f-b6ce70cfe035
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 3%

---

# Desarrollo y ampliación de flujos de trabajo{#developing-and-extending-workflows}

AEM proporciona varias herramientas y recursos para crear modelos de flujo de trabajo, desarrollar pasos de flujo de trabajo y para interactuar mediante programación con flujos de trabajo.

Los flujos de trabajo permiten automatizar procesos para administrar recursos y publicar contenido en el entorno de AEM. Los flujos de trabajo se componen de una serie de pasos, en los que cada paso realiza una tarea discreta. Puede utilizar la lógica y los datos de tiempo de ejecución para decidir cuándo puede continuar un proceso y seleccionar el siguiente paso de uno de los múltiples pasos posibles.

Por ejemplo, los procesos empresariales para crear y publicar páginas web incluyen tareas de aprobación y firma de varios participantes. Estos procesos se pueden modelar con flujos de trabajo de AEM y aplicarse a contenido específico.

Los aspectos clave se tratan a continuación, mientras que las siguientes páginas tratan más detalles:

* [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md)
* [Ampliación de la funcionalidad del flujo de trabajo](/help/sites-developing/workflows-customizing-extending.md)
* [Interactuar con flujos de trabajo mediante programación](/help/sites-developing/workflows-program-interaction.md)
* [Referencia de pasos de flujo de trabajo](/help/sites-developing/workflows-step-ref.md)
* [Referencia del proceso de flujo de trabajo](/help/sites-developing/workflows-process-ref.md)
* [Prácticas recomendadas de flujo de trabajo](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Para obtener información acerca de:
>
>* Al participar en flujos de trabajo, consulte [Uso de flujos de trabajo](/help/sites-authoring/workflows.md).
>* Para administrar flujos de trabajo e instancias de flujo de trabajo, consulte [Administrar flujos de trabajo](/help/sites-administering/workflows.md).
>* Para ver un artículo completo de la comunidad, consulte [Modificación de Digital Assets mediante flujos de trabajo de Adobe Experience Manager.](/help/assets/assets-workflow.md).
>* Consulte [Preguntar al seminario web de expertos de AEM sobre flujos de trabajo](https://communities.adobeconnect.com/p5s33iburd54/).
>* Cambios en las ubicaciones de la información, consulte [Prácticas recomendadas de flujo de trabajo - Ubicaciones](/help/sites-developing/workflows-best-practices.md#locations).

## Modelo {#model}

Un `WorkflowModel` representa una definición (modelo) de un flujo de trabajo. Está compuesto por `WorkflowNodes` y `WorkflowTransitions`. Las transiciones conectan los nodos y definen *flow*. El modelo siempre tiene un nodo de inicio y un nodo de finalización.

### Modelo Runtime {#runtime-model}

Los modelos de flujo de trabajo tienen versiones. Al ejecutar una instancia de flujo de trabajo, se utiliza y se mantiene el modelo de tiempo de ejecución del flujo de trabajo, tal como estaba disponible en el momento en que se inició el flujo de trabajo.

Se [genera un modelo en tiempo de ejecución cuando se activa **Sync** en el editor del modelo de flujo de trabajo](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Las ediciones realizadas en el modelo de flujo de trabajo, en los modelos de tiempo de ejecución generados o en ambos, *después de* de iniciar la instancia específica no se aplican a esa instancia.

>[!CAUTION]
>
>Los pasos realizados están definidos por el [modelo de tiempo de ejecución](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model), generado en el momento en que se activa la acción **Sincronizar** en el editor del modelo de flujo de trabajo.
>
>Si el modelo de flujo de trabajo cambia después de este momento (sin que se active **Sync**), la instancia de tiempo de ejecución no reflejará dichos cambios. Solo los modelos en tiempo de ejecución generados después de la actualización reflejan los cambios. Las excepciones son los scripts ECMA subyacentes, que se conservan una sola vez para que se realicen los cambios.

### Paso {#step}

Cada paso realiza una tarea discreta. Existen diferentes tipos de pasos del flujo de trabajo:

* Participante (usuario/grupo): estos pasos generan un elemento de trabajo y lo asignan a un usuario o grupo. Un usuario debe completar el elemento de trabajo para avanzar en el flujo de trabajo.
* Process (Script, Java™ method call): el sistema ejecuta estos pasos automáticamente. Un script ECMA o una clase Java™ implementan el paso. Los servicios se pueden desarrollar para escuchar eventos de flujo de trabajo especiales y realizar tareas según la lógica empresarial.
* Contenedor (subflujo de trabajo): este tipo de paso inicia otro modelo de flujo de trabajo.
* OR Split/Join: utilice la lógica para decidir qué paso ejecutar en el flujo de trabajo.
* División/unión AND: permite ejecutar varios pasos simultáneamente.

Todos los pasos comparten las siguientes propiedades comunes: `Autoadvance` y `Timeout` alertas (que se pueden usar como scripts).

### Transición {#transition}

Un(a) `WorkflowTransition` representa una transición entre dos `WorkflowNodes` de un(a) `WorkflowModel`.

* Define el vínculo entre dos pasos consecutivos.
* Es posible aplicar reglas.

### WorkItem {#workitem}

Un(a) `WorkItem` es la unidad que se pasa a través de una instancia `Workflow` de un(a) `WorkflowModel`. Contiene el `WorkflowData` en el que actúa la instancia y una referencia al `WorkflowNode` que describe el paso de flujo de trabajo subyacente.

* Se utiliza para identificar la tarea y se coloca en la bandeja de entrada correspondiente.
* Una instancia de flujo de trabajo puede tener uno o varios `WorkItems` al mismo tiempo (según el modelo de flujo de trabajo).
* `WorkItem` hace referencia a la instancia de flujo de trabajo.
* En el repositorio, `WorkItem` se almacena debajo de la instancia de flujo de trabajo.

### Carga útil {#payload}

Hace referencia al recurso que debe avanzarse a través de un flujo de trabajo.

La implementación de carga útil hace referencia a un recurso del repositorio (por ruta, UUID o URL) o por un objeto Java™ serializado. La referencia a un recurso en el repositorio es flexible y fiable, con sling productivo. Por ejemplo, el nodo al que se hace referencia podría representarse como un formulario.

### Ciclo de vida {#lifecycle}

Se crea al iniciar un nuevo flujo de trabajo (seleccionando el modelo de flujo de trabajo correspondiente y definiendo la carga útil) y finaliza cuando se procesa el nodo final.

Las siguientes acciones son posibles en una instancia de flujo de trabajo:

* Terminar
* Suspender
* Reanudar
* Reiniciar

Se archivan las instancias completadas y terminadas.

### Bandeja de entrada {#inbox}

Cada cuenta de usuario tiene su propia bandeja de entrada de flujo de trabajo en la que se puede acceder a los `WorkItems` asignados.

Los(as) `WorkItems` se asignan a la cuenta de usuario directamente o al grupo al que pertenecen.

### Tipos de flujo de trabajo {#workflow-types}

Existen varios tipos de flujo de trabajo como se indica en la consola Modelos de flujo de trabajo:

![wf-actualizado-03](assets/wf-upgraded-03.png)

* **Predeterminado**

  Estos tipos son los flujos de trabajo predeterminados incluidos en una instancia estándar de AEM.

* Flujos de trabajo personalizados (sin indicador en la consola)

  Estos flujos de trabajo se han creado como nuevos o a partir de flujos de trabajo integrados que se han superpuesto con las personalizaciones.

* **Heredado**

  Flujos de trabajo creados en una versión anterior de AEM. Estos flujos de trabajo se pueden retener durante una actualización o exportarse como un paquete de flujo de trabajo de la versión anterior y luego importarse en la nueva versión.

### Flujos de trabajo transitorios {#transient-workflows}

Los flujos de trabajo estándar guardan la información de tiempo de ejecución (historial) durante su ejecución. También puede definir un modelo de flujo de trabajo como **Transitorio** para evitar que dicho historial se mantenga. Este flujo de trabajo se utiliza para ajustar el rendimiento porque ahorra tiempo y recursos que se utilizan para mantener la información.

Los flujos de trabajo transitorios se pueden utilizar para cualquier flujo de trabajo que:

* se ejecutan a menudo.
* no necesita el historial del flujo de trabajo.

Se han introducido flujos de trabajo transitorios para cargar muchos recursos, donde la información del recurso es importante, pero no el historial de tiempo de ejecución del flujo de trabajo.

>[!NOTE]
>
>Consulte [Creación de un flujo de trabajo transitorio](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) para obtener más información.

>[!CAUTION]
>
>Cuando un modelo de flujo de trabajo se marca como Transitorio, hay algunos escenarios en los que la información de tiempo de ejecución debe persistir:
>
>* El tipo de carga útil (por ejemplo, vídeo) requiere pasos externos para el procesamiento; en estos casos, el historial de tiempo de ejecución es necesario para la confirmación de estado.
>* El flujo de trabajo introduce **AND Split**. En estos casos, el historial de tiempo de ejecución es necesario para la confirmación de estado.
>* Cuando el flujo de trabajo transitorio introduce un paso de participante, cambia de modo, durante la ejecución, a no transitorio. Como la tarea se pasa a una persona, el historial debe persistir.
>

>[!CAUTION]
>
>Dentro de un flujo de trabajo transitorio, no debería usar un **Paso Ir a**.
>
>El motivo es que **Ir al paso** crea un trabajo de sling para continuar el flujo de trabajo en el punto `goto`. Evita el propósito de hacer que el flujo de trabajo sea transitorio y genera un error en el archivo de registro.
>
>Use **OR Split** para hacer elecciones dentro de un flujo de trabajo transitorio.

>[!NOTE]
>
>Consulte las [Prácticas recomendadas para Assets](/help/assets/performance-tuning-guidelines.md#transient-workflows) para obtener más información sobre cómo los flujos de trabajo transitorios afectan el rendimiento de los recursos.

### Compatibilidad con varios recursos {#multi-resource-support}

Activar **Compatibilidad con varios recursos** para el modelo de flujo de trabajo significa que se inicia una sola instancia de flujo de trabajo incluso cuando se seleccionan varios recursos. Cada uno se adjunta como un paquete.

Si **Compatibilidad con varios recursos** no está activada para el modelo de flujo de trabajo y se seleccionan varios recursos, se inicia una instancia de flujo de trabajo individual para cada recurso.

>[!NOTE]
>
>Consulte [Configuración de un flujo de trabajo para la compatibilidad con varios recursos](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) para obtener más información.

### Fases del flujo de trabajo {#workflow-stages}

Las fases del flujo de trabajo ayudan a visualizar el progreso de un flujo de trabajo al administrar tareas. Se pueden utilizar para proporcionar una visión general de hasta dónde llega el flujo de trabajo a través del procesamiento. Cuando se ejecuta el flujo de trabajo, el usuario puede ver el progreso descrito por **Stage** (a diferencia del paso individual).

Como los nombres de paso individuales pueden ser específicos y técnicos, los nombres de fase se pueden definir para proporcionar una vista conceptual del progreso del flujo de trabajo.

Por ejemplo, para un flujo de trabajo con seis pasos y cuatro fases:

1. Puede [configurar las fases del flujo de trabajo (que muestran el progreso del flujo de trabajo) y luego asignar la fase adecuada a cada paso del flujo de trabajo](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * Se pueden crear varios nombres de fase.
   * A continuación, se asigna un nombre de etapa individual a cada paso (se puede asignar un nombre de etapa a uno o más pasos).

   | **Nombre del paso** | **Fase (asignada al paso)** |
   |---|---|
   | Etapa 1 | Crear |
   | Etapa 2 | Crear |
   | Etapa 3 | Revisión |
   | Etapa 4 | Aprobar |
   | Etapa 5 | Completado |
   | Etapa 6 | Completado |

1. Cuando se ejecuta el flujo de trabajo, el usuario puede ver el progreso según los nombres de las fases (en lugar de los nombres de las fases). El progreso del flujo de trabajo se muestra en la pestaña [WORKFLOW INFO de la ventana de detalles de la tarea del elemento de flujo de trabajo](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) enumerado en la [bandeja de entrada](/help/sites-authoring/inbox.md).

### Flujos de trabajo y Forms {#workflows-and-forms}

Normalmente, los flujos de trabajo se utilizan para procesar los envíos de formularios en AEM. Se puede combinar con los [componentes principales de los componentes de formulario](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html?lang=es) disponibles en una instancia de AEM estándar o con la [solución de AEM Forms](/help/forms/using/aem-forms-workflow.md).

Al crear un formulario, el envío del formulario se puede asociar fácilmente a un modelo del flujo de trabajo. Por ejemplo, para almacenar el contenido en una ubicación concreta del repositorio o para notificar a un usuario el envío del formulario y su contenido.

### Flujos de trabajo y traducción {#workflows-and-translation}

Los flujos de trabajo también forman parte del proceso [Translation](/help/sites-administering/translation.md).
