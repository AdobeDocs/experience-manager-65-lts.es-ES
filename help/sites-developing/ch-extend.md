---
title: Ampliación de ContextHub
description: Defina nuevos tipos de módulos y tiendas de ContextHub cuando los que se proporcionan no cumplan con los requisitos de su solución
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Ampliación de ContextHub{#extending-contexthub}

Defina nuevos tipos de módulos y tiendas de ContextHub cuando los que se proporcionan no cumplan con los requisitos de su solución.

## Crear candidatos de tienda personalizados {#creating-custom-store-candidates}

Las tiendas de ContextHub se crean a partir de candidatos de tiendas registradas. Para crear un almacén personalizado, cree y registre un candidato de almacén.

El archivo JavaScript que incluye el código que crea y registra el candidato al almacén debe incluirse en una [carpeta de biblioteca de cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.store.[storeType]
```

La parte `[storeType]` de la categoría es el `storeType` con el que está registrado el candidato de tienda. (Consulte [Registro de un candidato a tienda ContextHub](/help/sites-developing/ch-extend.md#registering-a-contexthub-store-candidate)). Por ejemplo, para el storeType de `contexthub.mystore`, la categoría de la carpeta de biblioteca de cliente debe ser `contexthub.store.contexthub.mystore`.

### Creación de un candidato de tienda de ContextHub {#creating-a-contexthub-store-candidate}

Para crear una tienda candidata, utilice la función [`ContextHub.Utils.inheritance.inherit`](/help/sites-developing/contexthub-api.md#inherit-child-parent) para ampliar una de las tiendas base:

* [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore)
* [`ContextHub.Store.SessionStore`](/help/sites-developing/contexthub-api.md#contexthub-store-sessionstore)
* [`ContextHub.Store.JSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore)
* [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore)

Cada almacén base amplía el almacén [`ContextHub.Store.Core`](/help/sites-developing/contexthub-api.md#contexthub-store-core).

En el siguiente ejemplo se crea la extensión más sencilla del candidato de almacén `ContextHub.Store.PersistedStore`:

```
myStoreCandidate = function(){};
ContextHub.Utils.inheritance.inherit(myStoreCandidate,ContextHub.Store.PersistedStore);
```

De forma realista, los candidatos de la tienda personalizada definen funciones adicionales o anulan la configuración inicial de la tienda. Hay varios [candidatos de almacén de muestra](/help/sites-developing/ch-samplestores.md) instalados en el repositorio por debajo de `/libs/granite/contexthub/components/stores`. Para aprender de estos ejemplos, utilice CRXDE Lite para abrir los archivos de JavaScript.

### Registro de un candidato de tienda de ContextHub {#registering-a-contexthub-store-candidate}

Registre un candidato de tienda para integrarlo con el marco de ContextHub y permitir que se creen tiendas a partir de él. Para registrar un candidato de almacén, utilice la función [`registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) de la clase `ContextHub.Utils.storeCandidates`.

Al registrar un candidato de tienda, se proporciona un nombre para el tipo de tienda. Al crear un almacén a partir del candidato, se utiliza el tipo de almacén para identificar el candidato en el que se basa.

Cuando se registra un candidato a tienda, se indica su prioridad. Cuando se registra un candidato de tienda con el mismo tipo de tienda que un candidato de tienda ya registrado, se utiliza el candidato con la prioridad más alta. Por lo tanto, puede anular los candidatos de tienda existentes con nuevas implementaciones.

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandidate', 0);
```

Por lo general, solo se necesita un candidato y la prioridad se puede establecer en `0`. Pero si está interesado, puede obtener información acerca de [registros más avanzados](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies), que permite elegir una de las pocas implementaciones de la tienda en función de la condición de JavaScript (`applies`) y la prioridad de los candidatos.

## Creación de tipos de módulos de IU de ContextHub {#creating-contexthub-ui-module-types}

Cree tipos de módulos de IU personalizados cuando los que están [instalados con ContextHub](/help/sites-developing/ch-samplemodules.md) no cumplan con sus requisitos. Para crear un tipo de módulo de interfaz de usuario, cree un procesador de módulos de interfaz de usuario ampliando la clase `ContextHub.UI.BaseModuleRenderer` y registrándola después con `ContextHub.UI`.

Para crear un procesador de módulos de IU, cree un objeto `Class` que contenga la lógica que procesa el módulo de IU. Como mínimo, la clase debe realizar las siguientes acciones:

* Extienda la clase `ContextHub.UI.BaseModuleRenderer`. Esta clase es la implementación base para todos los procesadores de módulos de IU. El objeto `Class` define una propiedad denominada `extend` que se usa para asignar a esta clase el nombre que se está extendiendo.

* Proporcione una configuración predeterminada. Crear una propiedad `defaultConfig`. Esta propiedad es un objeto que incluye las propiedades definidas para el módulo de interfaz de usuario [`contexthub.base`](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) y cualquier otra propiedad que necesite.

El origen de `ContextHub.UI.BaseModuleRenderer` se encuentra en /libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js. Para registrar el procesador, utilice el método [`registerRenderer`](/help/sites-developing/contexthub-api.md#registerrenderer-moduletype-renderer-dontrender) de la clase `ContextHub.UI`. Proporcione un nombre para el tipo de módulo. Cuando los administradores crean un módulo de interfaz de usuario basado en este procesador, especifican este nombre.

Cree y registre la clase de procesador en una función anónima de ejecución automática. El siguiente ejemplo se basa en el código fuente del módulo de interfaz de usuario contexthub.browserinfo. Este módulo de interfaz de usuario es una extensión simple de la clase `ContextHub.UI.BaseModuleRenderer`.

```xml
;(function() {

    var SurferinfoRenderer = new Class({
        extend: ContextHub.UI.BaseModuleRenderer,

        defaultConfig: {
            icon: 'coral-Icon--globe',
            title: 'Browser/OS Information',

            storeMapping: {
                surferinfo: 'surferinfo'
            },

            template:
                '<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p>' +
                '<p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>'
        }
    });

    ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());

}());
```

El archivo JavaScript que incluye el código que crea y registra el procesador debe incluirse en una [carpeta de biblioteca de cliente](/help/sites-developing/clientlibs.md#creating-client-library-folders). La categoría de la carpeta debe coincidir con el siguiente patrón:

```xml
contexthub.module.[moduleType]
```

La parte `[moduleType]` de la categoría es el `moduleType` con el que está registrado el procesador de módulos. Por ejemplo, para `moduleType` de `contexthub.browserinfo`, la categoría de la carpeta de la biblioteca de cliente debe ser `contexthub.module.contexthub.browserinfo`.
