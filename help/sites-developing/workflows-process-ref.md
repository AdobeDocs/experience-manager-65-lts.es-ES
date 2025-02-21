---
title: Referencia del proceso de flujo de trabajo
description: Consulte esta referencia de proceso para ver los flujos de trabajo en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---

# Referencia del proceso de flujo de trabajo{#workflow-process-reference}

AEM proporciona varios pasos de proceso que se pueden utilizar para crear modelos de flujo de trabajo. También se pueden agregar pasos de proceso personalizados para tareas que no estén cubiertas por los pasos integrados (consulte [Creación de modelos de flujo de trabajo](/help/sites-developing/workflows-models.md)).

## Características del proceso {#process-characteristics}

Para cada paso del proceso, se describen las siguientes características.

### Ruta de clase Java™ o ECMA {#java-class-or-ecma-path}

Los pasos del proceso se definen mediante una clase Java™ o ECMAScript.

* Para los procesos de clase Java™, se proporciona el nombre de clase completo.
* Para los procesos ECMAScript, se proporciona la ruta de acceso al script.

### Carga útil {#payload}

La carga útil es la entidad en la que actúa una instancia de flujo de trabajo. La carga útil se selecciona implícitamente mediante el contexto en el que se inicia una instancia de flujo de trabajo.

Por ejemplo, si se aplica un flujo de trabajo a una página de AEM *P*, *P* se pasa de un paso a otro a medida que el flujo de trabajo avanza y cada paso actúa de alguna manera de manera opcional en *P*.

En el caso más común, la carga útil es un nodo JCR en el repositorio (por ejemplo, una página o un recurso de AEM). La carga útil de un nodo JCR se pasa como una cadena que es una ruta JCR o un identificador JCR (UUID). A veces, la carga útil puede ser una propiedad JCR (pasada como ruta JCR), una URL, un objeto binario o un objeto Java™ genérico. Los pasos de proceso individuales que sí actúan en la carga útil generalmente esperan una carga útil de un tipo determinado o actúan de forma diferente según el tipo de carga útil. Para cada proceso descrito a continuación, se describe el tipo de carga útil esperado, de haber.

### Argumentos {#arguments}

Algunos procesos de flujo de trabajo aceptan argumentos que el administrador especifica al configurar el paso del flujo de trabajo.

Los argumentos se especifican como una sola cadena en la propiedad **Argumentos del proceso** del panel **Propiedades** del editor de flujo de trabajo. Para cada proceso que se describe a continuación, el formato de la cadena de argumento se describe en una gramática EBNF simple. Por ejemplo, lo siguiente indica que la cadena de argumento consta de uno o más pares delimitados por comas, donde cada par consta de un nombre (que es una cadena) y un valor, separados por dos puntos:

```
    args := name '::' value [',' name '::' value]*
    name := /* A string */
    value := /* A string */
```


### Tiempo de espera {#timeout}

Después de este período de tiempo de espera, el paso del flujo de trabajo deja de ser operativo. Algunos procesos de flujo de trabajo respetan el tiempo de espera, mientras que otros no lo hacen y lo ignoran.

### Permisos {#permissions}

La sesión pasada a `WorkflowProcess` está respaldada por el usuario de servicio para el servicio de proceso de flujo de trabajo, que tiene los siguientes permisos en la raíz del repositorio:

* `jcr:read`
* `rep:write`
* `jcr:versionManagement`
* `jcr:lockManagement`
* `crx:replicate`

Si ese conjunto de permisos no es suficiente para la implementación de `WorkflowProcess`, debe usar una sesión con los permisos requeridos.

La manera recomendada de hacerlo es utilizar un usuario de servicio creado con el subconjunto necesario, pero mínimo, de permisos necesarios.

>[!CAUTION]
>
>Si actualiza desde una versión anterior a AEM 6.2, es posible que tenga que actualizar la implementación.
>
>En versiones anteriores, la sesión de administración se pasaba a las implementaciones de `WorkflowProcess` y, a continuación, podía tener acceso completo al repositorio sin tener que definir ACL específicas.
>
>Los permisos ahora se definen como arriba ([Permisos](#permissions)). Como es el método recomendado para actualizar la implementación.
>
>También hay disponible una solución a corto plazo para fines de compatibilidad con versiones anteriores cuando no es posible realizar cambios en el código:
>
>* Usando la consola web (`/system/console/configMgr`), busque el **Servicio de configuración del flujo de trabajo de Adobe Granite**
>
>* habilitar el **Modo heredado del proceso de flujo de trabajo**
>
>Esto revierte al comportamiento anterior de proporcionar una sesión de administración a la implementación de `WorkflowProcess` y proporcionar acceso sin restricciones a la totalidad del repositorio una vez más.

## Procesos de control de flujo {#workflow-control-processes}

Los siguientes procesos no realizan ninguna acción en el contenido. Sirven para controlar el comportamiento del propio flujo de trabajo.

### AbsoluteTimeAutoAdvancer (Absolute Time Auto Advancer) {#absolutetimeautoadvancer-absolute-time-auto-advancer}

El proceso `AbsoluteTimeAutoAdvancer` (Absolute Time Auto Advancer) se comporta de manera idéntica a **AutoAdvancer**, excepto que se agota el tiempo de espera en una fecha y hora determinadas, en lugar de después de un período de tiempo determinado.

* **Clase Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AbsoluteTimeAutoAdvancer`
* **Carga**: Ninguna.
* **Argumentos**: Ninguno.
* **Tiempo de espera**: El proceso agota el tiempo de espera cuando se llega a la hora y fecha establecidas.

### AutoAdvancer (Auto Advancer) {#autoadvancer-auto-advancer}

El proceso `AutoAdvancer` avanza automáticamente el flujo de trabajo al paso siguiente. Si hay más de un paso siguiente posible (por ejemplo, si hay una división O), este proceso hará avanzar el flujo de trabajo a lo largo de la *ruta predeterminada*, si se ha especificado una, de lo contrario el flujo de trabajo no avanzará.

* **Clase Java™**: `com.adobe.granite.workflow.console.timeout.autoadvance.AutoAdvancer`

* **Carga**: Ninguna.
* **Argumentos**: Ninguno.
* **Tiempo de espera**: El proceso expira después de un período de tiempo establecido.

### ProcessAssembler (ensamblador de procesos) {#processassembler-process-assembler}

El proceso `ProcessAssembler` ejecuta varios subprocesos secuencialmente en un solo paso del flujo de trabajo. Para utilizar `ProcessAssembler`, cree un solo paso de este tipo en el flujo de trabajo y establezca sus argumentos para indicar los nombres y argumentos de los subprocesos que desea ejecutar.

* **Clase Java™**: `com.day.cq.workflow.impl.process.ProcessAssembler`

* **Carga útil**: Un recurso DAM, una página AEM o ninguna carga útil (depende de los requisitos de los subprocesos).
* **Argumentos**:

```
        args := arg [',' arg]
        arg := processname ['::' processargs]
        processname := /* A fully qualified Java Class or absolute
        repository path to an ECMAScript */
        processargs := processarg [';' processarg]*
        processarg := '[' nobracketprocessarg ']' | nobracketprocessarg
        nobracketprocessarg := listitem [':' listitem]*
        listitem := /* A string */
```

* **Tiempo de espera**: Respetado.

Por ejemplo:

* Extraiga los metadatos del recurso.
* Cree tres miniaturas de los tres tamaños especificados.
* Cree una imagen de JPEG a partir del recurso, suponiendo que este no sea originalmente un GIF ni un PNG (en cuyo caso no se crea ningún JPEG).
* Establezca la fecha de la última modificación del recurso.

```shell
com.day.cq.dam.core.process.ExtractMetadataProcess,
    com.day.cq.dam.core.process.CreateThumbnailProcess::[140:100];[48:48];[319:319:false],
    com.day.cq.dam.core.process.CreateWebEnabledImageProcess::dimension:1280:1280;mimetype:image/jpeg,
    com.day.cq.dam.core.process.AssetSetLastModifiedProcess
```

## Procesos básicos {#basic-processes}

Los siguientes procesos realizan tareas sencillas o sirven como ejemplos.

>[!CAUTION]
>
>No cambie nada en la ruta de acceso `/libs`.
>
>Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y puede sobrescribirse al aplicar una revisión o un paquete de características).

### eliminar {#delete}

Se elimina el elemento de la ruta determinada.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/delete.ecma`

* **Carga útil**: ruta JCR
* **Argumentos**: Ninguno
* **Tiempo de espera**: omitido

### noop {#noop}

Este es el proceso nulo. No realiza ninguna operación, pero registra un mensaje de depuración.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/noop.ecma`

* **Carga**: Ninguna
* **Argumentos**: Ninguno
* **Tiempo de espera**: omitido

### rule-false {#rule-false}

Este es un proceso nulo que devuelve `false` en el método `check()`.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/rule-false.ecma`

* **Carga**: Ninguna
* **Argumentos**: Ninguno
* **Tiempo de espera**: omitido

### muestra {#sample}

Este es un ejemplo de proceso ECMAScript.

* **Ruta de ECMAScript**: `/libs/workflow/scripts/sample.ecma`

* **Carga**: Ninguna
* **Argumentos**: Ninguno
* **Tiempo de espera**: omitido

### LockProcess {#lockprocess}

Bloquea la carga útil del flujo de trabajo.

* **Clase Java™:** `com.day.cq.workflow.impl.process.LockProcess`

* **Carga útil:** JCR_PATH y JCR_UUID
* **Argumentos:** Ninguno
* **Tiempo de espera:** omitido

El paso no tiene efecto en las siguientes circunstancias:

* La carga útil ya está bloqueada
* El nodo de carga útil no contiene un nodo secundario jcr:content

### UnlockProcess {#unlockprocess}

Desbloquea la carga útil del flujo de trabajo.

* **Clase Java™:** `com.day.cq.workflow.impl.process.UnlockProcess`

* **Carga útil:** JCR_PATH y JCR_UUID
* **Argumentos:** Ninguno
* **Tiempo de espera:** omitido

El paso no tiene efecto en las siguientes circunstancias:

* La carga útil ya está desbloqueada
* El nodo de carga útil no contiene un nodo secundario jcr:content

## Procesos de versiones {#versioning-processes}

El siguiente proceso realiza una tarea relacionada con la versión.

### CreateVersionProcess {#createversionprocess}

Crea una versión de la carga útil del flujo de trabajo (página AEM o recurso DAM).

* **Clase Java™**: `com.day.cq.wcm.workflow.process.CreateVersionProcess`

* **Carga útil**: Una ruta JCR o UUID que hace referencia a una página o recurso DAM
* **Argumentos**: Ninguno
* **Tiempo de espera**: Respetado
