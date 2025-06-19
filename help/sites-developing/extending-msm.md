---
title: Ampliación del Administrador de varios sitios
description: Esta página le ayuda a ampliar las funcionalidades del Administrador de varios sitios
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 46300f72-730e-444c-8677-352a890e9910
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '2444'
ht-degree: 1%

---

# Ampliación del Administrador de varios sitios{#extending-the-multi-site-manager}

Esta página le ayuda a ampliar las funcionalidades del Administrador de varios sitios:

* Obtenga información acerca de los miembros principales de la API de Java de MSM.
* Cree una acción de sincronización que se pueda utilizar en una configuración de despliegue.
* Modifique el idioma y los códigos de país predeterminados.

<!-- * Remove the "Chapters" step in the Create Site wizard. -->

>[!NOTE]
>
>Esta página se debe leer junto con [Reutilización del contenido: Administrador de varios sitios](/help/sites-administering/msm.md).
>
>Las siguientes secciones de Reestructuración de repositorios de Sites también pueden ser de interés:
>* [Configuraciones de modelo de administrador de varios sitios](https://experienceleague.adobe.com/docs/experience-manager-65-lts/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-blueprint-configurations)
>* [Configuraciones de despliegue del administrador de varios sitios](https://experienceleague.adobe.com/docs/experience-manager-65-lts/deploying/restructuring/sites-repository-restructuring-in-aem-6-5.html#multi-site-manager-rollout-configurations)

>[!CAUTION]
>
>El Administrador de varios sitios y su API se utilizan durante la creación de un sitio web, por lo que solo están pensados para su uso en un entorno de creación.

## Información general sobre la API de Java {#overview-of-the-java-api}

Multi Site Management consta de los siguientes paquetes:

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/api/package-summary.html)
* [com.day.cq.wcm.msm.commons](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/commons/package-summary.html)

Los objetos principales de la API de MSM interactúan de la siguiente manera (consulte también [Términos utilizados](/help/sites-administering/msm.md#terms-used)):

![Objetos principales de la API de MSM](assets/chlimage_1-73.png)

* **`Blueprint`**

  Un `Blueprint` (como en la [configuración de modelo](/help/sites-administering/msm.md#source-blueprints-and-blueprint-configurations)) especifica las páginas desde las que una Live Copy puede heredar contenido.

  ![Modelo](assets/chlimage_1-74.png)

   * El uso de una configuración de modelo ( `Blueprint`) es opcional, pero:

      * Permite al autor utilizar la opción **Despliegue** en el origen (para insertar (explícitamente) modificaciones en Live Copies que heredan de este origen).
      * Permite al autor utilizar **Crear sitio**; esto permite al usuario seleccionar idiomas fácilmente y configurar la estructura de la Live Copy.
      * Define la configuración de despliegue predeterminada para cualquier Live Copies resultante.

* **`LiveRelationship`**

  El `LiveRelationship` especifica la conexión (relación) entre un recurso de la rama de Live Copy y su recurso de origen/modelo equivalente.

   * Las relaciones se utilizan para realizar la herencia y el despliegue.
   * Los objetos de `LiveRelationship` proporcionan acceso (referencias) a los objetos de las configuraciones de despliegue (`RolloutConfig`), `LiveCopy` y `LiveStatus` relacionados con la relación.

   * Por ejemplo, se crea una Live Copy en `/content/copy/us` a partir del origen/modelo en `/content/we-retail/language-masters`. Los recursos `/content/we.retail/language-masters/en/jcr:content` y `/content/copy/us/en/jcr:content` forman una relación.

* **`LiveCopy`**

  `LiveCopy` contiene los detalles de configuración para las relaciones ( `LiveRelationship`) entre los recursos de live copy y sus recursos de origen/modelo.

   * Utilice la clase `LiveCopy` para acceder a la ruta de acceso de la página, la ruta de acceso de la página de origen/modelo, las configuraciones de despliegue y si las páginas secundarias también se incluyen en `LiveCopy`.

   * Se crea un nodo `LiveCopy` cada vez que se usa **Crear sitio** o **Crear Live Copy**.

* **`LiveStatus`**

  Los objetos `LiveStatus` proporcionan acceso al estado de tiempo de ejecución de `LiveRelationship`. Se utiliza para consultar el estado de sincronización de una Live Copy.

* **`LiveAction`**

  Un `LiveAction` es una acción que se ejecuta en cada recurso involucrado en el despliegue.

   * Las LiveActions solo se generan mediante RolloutConfigs.

* **`LiveActionFactory`**

  Crea `LiveAction` objetos según una configuración de `LiveAction`. Las configuraciones se almacenan como recursos en el repositorio.

* **`RolloutConfig`**

  El `RolloutConfig` contiene una lista de `LiveActions`, que se utilizará cuando se active. `LiveCopy` hereda `RolloutConfig` y el resultado está presente en `LiveRelationship`.

   * La configuración de una Live Copy por primera vez también utiliza un RolloutConfig (que almacena en déclencheur las LiveActions).

## Creación de una nueva acción de sincronización {#creating-a-new-synchronization-action}

Cree acciones de sincronización personalizadas para utilizarlas con las configuraciones de despliegue. Cree una acción de sincronización cuando las [acciones instaladas](/help/sites-administering/msm-sync.md#installed-synchronization-actions) no cumplan con los requisitos específicos de la aplicación. Para ello, cree dos clases:

* Implementación de la interfaz [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) que realiza la acción.
* Componente OSGI que implementa la interfaz [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) y crea instancias de su clase `LiveAction`.

`LiveActionFactory` crea instancias de la clase `LiveAction` para una configuración determinada:

* `LiveAction` clases incluyen los siguientes métodos:

   * `getName`: Devuelve el nombre de la acción. El nombre se utiliza para hacer referencia a la acción, por ejemplo, en las configuraciones de despliegue.
   * `execute`: realiza las tareas de la acción.

* `LiveActionFactory` clases incluyen los siguientes miembros:

   * `LIVE_ACTION_NAME`: un campo que contiene el nombre del `LiveAction` asociado. Este nombre debe coincidir con el valor devuelto por el método `getName` de la clase `LiveAction`.

   * `createAction`: crea una instancia de `LiveAction`. El parámetro `Resource` opcional se puede usar para proporcionar información de configuración.

   * `createsAction`: devuelve el nombre del `LiveAction` asociado.

### Acceso al nodo de configuración de LiveAction {#accessing-the-liveaction-configuration-node}

Utilice el nodo de configuración `LiveAction` del repositorio para almacenar información que afecte al comportamiento en tiempo de ejecución de la instancia `LiveAction`. El nodo del repositorio que almacena la configuración de `LiveAction` está disponible para el objeto `LiveActionFactory` durante la ejecución. Por lo tanto, puede agregar propiedades al nodo de configuración a y utilizarlas en su implementación de `LiveActionFactory` según sea necesario.

Por ejemplo, un `LiveAction` necesita almacenar el nombre del autor del modelo. Una propiedad del nodo de configuración incluye el nombre de la propiedad de la página de modelo que almacena la información. En tiempo de ejecución, `LiveAction` recupera el nombre de propiedad de la configuración y, a continuación, obtiene el valor de propiedad.

El parámetro del método [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) es un objeto `Resource`. Este objeto `Resource` representa el nodo `cq:LiveSyncAction` para esta acción activa en la configuración de despliegue; consulte [Creación de una configuración de despliegue](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration). Como de costumbre al utilizar un nodo de configuración, debe adaptarlo a un objeto `ValueMap`:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Acceder a los nodos de Target, a los nodos de Source y a LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

Se proporcionan los objetos siguientes como parámetros del método `execute` del objeto `LiveAction`:

* Un objeto [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) que representa el origen de Live Copy.
* Un objeto `Resource` que representa el destino de Live Copy.
* El objeto [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) para Live Copy.
* El valor `autoSave` indica si su `LiveAction` debe guardar los cambios realizados en el repositorio.

* El valor reset indica el modo reset del despliegue.

Desde estos objetos puede obtener toda la información acerca de `LiveCopy`. También puede usar los objetos `Resource` para obtener los objetos `ResourceResolver`, `Session` y `Node`. Estos objetos son útiles para manipular el contenido del repositorio:

En la primera línea del siguiente código, el origen es el objeto `Resource` de la página de origen:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>Los argumentos `Resource` pueden ser objetos `null` o `Resources` que no se adaptan a objetos `Node`, como objetos [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/NonExistingResource.html).

## Creación de una nueva configuración de despliegue {#creating-a-new-rollout-configuration}

Cree una configuración de despliegue cuando las configuraciones de despliegue instaladas no cumplan los requisitos de la aplicación:

* [Crear la configuración de despliegue](#create-the-rollout-configuration).
* [Agregar acciones de sincronización a la configuración de despliegue](#add-synchronization-actions-to-the-rollout-configuration).

La nueva configuración de despliegue está disponible al establecer configuraciones de despliegue en una página de modelo o Live Copy.

>[!NOTE]
>
>Vea también las [prácticas recomendadas para personalizar despliegues](/help/sites-administering/msm-best-practices.md#customizing-rollouts).

### Creación de la configuración de despliegue {#create-the-rollout-configuration}

1. Abra CRXDE Lite; por ejemplo:
   [http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. Vaya a :
   `/apps/msm/<your-project>/rolloutconfigs`

   >[!NOTE]
   >Esta es la versión personalizada del proyecto de:
   >`/libs/msm/wcm/rolloutconfigs`
   >Si esta es su primera configuración, esta rama `/libs` debe usarse como plantilla para crear la nueva rama en `/apps`.

   >[!NOTE]
   >
   >No cambie nada en la ruta de acceso `/libs`.
   >Esto se debe a que el contenido de `/libs` se sobrescribirá la próxima vez que actualice la instancia (y es posible que se sobrescriba al aplicar una revisión o un paquete de características).
   >El método recomendado para la configuración y otros cambios es:
   >
   >* Vuelva a crear el elemento necesario (es decir, tal como existe en `/libs`) en `/apps`
   >* Realizar cambios en `/apps`

1. En este(a) **Crear** un nodo(a) con las siguientes propiedades:

   * **Nombre**: El nombre de nodo de la configuración de despliegue. md#install-synchronization-actions), por ejemplo, `contentCopy` o `workflow`.
   * **Tipo**: `cq:RolloutConfig`

1. Agregue las siguientes propiedades a este nodo:
   * **Nombre**: `jcr:title`

     **Tipo**: `String`
     **Valor**: Un título de identificación que aparecerá en la interfaz de usuario.
   * **Nombre**: `jcr:description`

     **Tipo**: `String`
     **Valor**: una descripción opcional.
   * **Nombre**: `cq:trigger`

     **Tipo**: `String`
     **Value**: [Déclencheur de despliegue](/help/sites-administering/msm-sync.md#rollout-triggers) que se va a usar. Seleccionar de:
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Haga clic en **Guardar todo**.

### Añadir acciones de sincronización a la configuración de despliegue {#add-synchronization-actions-to-the-rollout-configuration}

Las configuraciones de despliegue se almacenan debajo del [nodo de configuración de despliegue](#create-the-rollout-configuration) que ha creado en el nodo `/apps/msm/<your-project>/rolloutconfigs`.

Agregue nodos secundarios de tipo `cq:LiveSyncAction` para agregar acciones de sincronización a la configuración de despliegue. El orden de los nodos de acción de sincronización determina el orden en que se producen las acciones.

1. En CRXDE Lite, selecciona tu nodo [Configuración de despliegue](#create-the-rollout-configuration).

   Por ejemplo:
   `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`

1. **Crear** un nodo con las siguientes propiedades de nodo:

   * **Nombre**: El nombre de nodo de la acción de sincronización.
El nombre debe ser el mismo que **Action Name** de la tabla bajo [Acciones de sincronización](/help/sites-administering/msm-sync.md#installed-synchronization-actions), por ejemplo, `contentCopy` o `workflow`.
   * **Tipo**: `cq:LiveSyncAction`

1. Añada y configure tantos nodos de acción de sincronización como sea necesario. Reorganice los nodos de acción para que su orden coincida con el orden en que desea que se produzcan. El nodo de acción superior se produce primero.

## Crear y usar una clase LiveActionFactory simple {#creating-and-using-a-simple-liveactionfactory-class}

Siga los procedimientos de esta sección para desarrollar un(a) `LiveActionFactory` y utilizarlo en una configuración de despliegue. Los procedimientos utilizan Maven y Eclipse para desarrollar e implementar `LiveActionFactory`:

1. [Cree el proyecto Maven](#create-the-maven-project) e impórtelo a Eclipse.
1. [Agregar dependencias](#add-dependencies-to-the-pom-file) al archivo POM.
1. [Implemente la interfaz `LiveActionFactory`](#implement-liveactionfactory) e implemente el paquete OSGi.
1. [Crear la configuración de despliegue](#create-the-example-rollout-configuration).
1. [Crear Live Copy](#create-the-live-copy).

El proyecto Maven y el código fuente de la clase Java están disponibles en el repositorio Git público.

CÓDIGO EN GITHUB

Puede encontrar el código de esta página en GitHub

* [Abrir proyecto experiencemanager-java-msmrollout en GitHub](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout)
* Descargar el proyecto como [archivo ZIP](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout/archive/master.zip)

### Creación del proyecto Maven {#create-the-maven-project}

El siguiente procedimiento requiere que haya agregado el perfil público de Adobe al archivo de configuración de Maven.

* Para obtener información sobre el perfil público de Adobe, consulte [Obtención del complemento Maven del paquete de contenido](/help/sites-developing/vlt-mavenplugin.md#obtaining-the-content-package-maven-plugin)
* Para obtener información acerca del archivo de configuración de Maven, consulte la [Referencia de configuración](https://maven.apache.org/settings.html) de Maven.

1. Abra una sesión de terminal o de línea de comandos y cambie el directorio para que apunte a la ubicación de donde crear el proyecto.
1. Introduzca el siguiente comando:

   ```xml
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Especifique los siguientes valores en la solicitud interactiva:

   * `groupId`: `com.adobe.example.msm`
   * `artifactId`: `MyLiveActionFactory`
   * `version`: `1.0-SNAPSHOT`
   * `package`: `MyPackage`
   * `appsFolderName`: `myapp`
   * `artifactName`: `MyLiveActionFactory package`
   * `packageGroup`: `myPackages`

1. Inicie Eclipse y [importe el proyecto Maven](/help/sites-developing/howto-projects-eclipse.md#import-the-maven-project-into-eclipse).

### Añadir dependencias al archivo POM {#add-dependencies-to-the-pom-file}

Agregue dependencias para que el compilador Eclipse pueda hacer referencia a las clases que se utilizan en el código `LiveActionFactory`.

1. En el Explorador del proyecto Eclipse, abra el archivo:

   `MyLiveActionFactory/pom.xml`

1. En el editor, haga clic en la ficha `pom.xml` y busque la sección `project/dependencyManagement/dependencies`.
1. Agregue el siguiente XML dentro del elemento `dependencyManagement` y, a continuación, guarde el archivo.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Abra el archivo POM del paquete desde **Explorador de proyectos** en `MyLiveActionFactory-bundle/pom.xml`.
1. En el editor, haga clic en la ficha `pom.xml` y busque la sección proyecto/dependencias. Agregue el siguiente XML dentro del elemento dependencies y, a continuación, guarde el archivo:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementar LiveActionFactory {#implement-liveactionfactory}

La siguiente clase `LiveActionFactory` implementa un `LiveAction` que registra mensajes sobre las páginas de origen y destino, y copia la propiedad `cq:lastModifiedBy` del nodo de origen al nodo de destino. El nombre de la acción activa es `exampleLiveAction`.

1. En el Explorador del proyecto Eclipse, haga clic con el botón secundario en el paquete `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` y haga clic en **Nuevo** > **Clase**. Para **Name**, escriba `ExampleLiveActionFactory` y haga clic en **Finalizar**.
1. Abra el archivo `ExampleLiveActionFactory.java`, reemplace el contenido por el siguiente código y guarde el archivo.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;  
   
   import com.day.cq.wcm.api.NameConstants;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(
   service = LiveActionFactory.class,
   property = {LiveActionFactory.LIVE_ACTION_NAME + "=" + ExampleLiveActionFactory.LIVE_ACTION_NAME})
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
     private static final Logger logger = LoggerFactory.getLogger(ExampleLiveActionFactory.class);
   
     public static final String LIVE_ACTION_NAME = "CustomAction";
   
     public LiveAction createAction(Resource config) {
       ValueMap configs;
       /* Adapt the config resource to a ValueMap */
       if (config == null || config.adaptTo(ValueMap.class) == null) {
         configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
       } else {
         configs = config.adaptTo(ValueMap.class);
       }  
   
       return new ExampleLiveAction(LIVE_ACTION_NAME, configs);
     }
     public String createsAction() {
       return LIVE_ACTION_NAME;
     }  
   
     /************* LiveAction ****************/
     private static class ExampleLiveAction implements LiveAction {
       private String name;
       private ValueMap configs;
       private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);  
   
     public ExampleLiveAction(String nm, ValueMap config){
       name = nm;
       configs = config;
     }  
   
     public void execute(Resource source, Resource target,
                         LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
                       throws WCMException {  
   
       String lastMod = null;  
   
       log.info(" *** Executing ExampleLiveAction *** ");  
   
       /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
       if ((Boolean) configs.get("repLastModBy")){  
   
         /* get the source's cq:lastModifiedBy property */
         if (source != null && source.adaptTo(Node.class) !=  null){
           ValueMap sourcevm = source.adaptTo(ValueMap.class);
           lastMod = sourcevm.get(NameConstants.PN_PAGE_LAST_MOD_BY, String.class);
         }  
   
         /* set the target node's la-lastModifiedBy property */
         Session session = null;
         if (target != null && target.adaptTo(Node.class) !=  null){
           ResourceResolver resolver = target.getResourceResolver();
           session = resolver.adaptTo(javax.jcr.Session.class);
           Node targetNode;
           try{
             targetNode=target.adaptTo(javax.jcr.Node.class);
             targetNode.setProperty("la-lastModifiedBy", lastMod);
             log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
           }catch(Exception e){
             log.error(e.getMessage());
           }
         }
         if(autoSave){
           try {
             session.save();
           } catch (Exception e) {
             try {
               session.refresh(true);
             } catch (RepositoryException e1) {
               e1.printStackTrace();
             }
             e.printStackTrace();
           }
         }
       }
     }
     public String getName() {
       return name;
     }  
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
                        ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
                         ActionConfig arg2, boolean arg3, boolean arg4)
                       throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
       return null;
     }
     @Deprecated
       public String[] getPropertiesNames() {
         return null;
     }
     @Deprecated
     public int getRank() {
       return 0;
     }
     @Deprecated
     public String getTitle() {
       return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
   }
   ```

1. Usando la sesión de terminal o de comando, cambie el directorio al directorio `MyLiveActionFactory` (el directorio del proyecto Maven). A continuación, introduzca el siguiente comando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

   El archivo AEM `error.log` debe indicar que se ha iniciado el paquete.

   Por ejemplo, [https://localhost:4502/system/console/status-slinglogs](https://localhost:4502/system/console/status-slinglogs).

   ```xml
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Creación de la configuración de despliegue de ejemplo {#create-the-example-rollout-configuration}

Cree la configuración de despliegue de MSM que usa el `LiveActionFactory` que creó:

1. Cree y configure una [Configuración de despliegue con el procedimiento estándar](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) - y use las propiedades:

   * **Título**: Configuración de despliegue de ejemplo
   * **Nombre**: examplerolloutconfig
   * **cq:déclencheur**: `publish`

### Añadir la acción Live a la configuración de despliegue de ejemplo {#add-the-live-action-to-the-example-rollout-configuration}

Configure la configuración de despliegue que creó en el procedimiento anterior para que utilice la clase `ExampleLiveActionFactory`.

1. Abra CRXDE Lite; por ejemplo, [https://localhost:4502/crx/de](https://localhost:4502/crx/de).
1. Cree el siguiente nodo en `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Nombre**: `exampleLiveAction`
   * **Tipo**: `cq:LiveSyncAction`

1. Haga clic en **Guardar todo**.
1. Seleccione el nodo `exampleLiveAction` y agregue la siguiente propiedad:

   * **Nombre**: `repLastModBy`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Esta propiedad indica a la clase `ExampleLiveAction` que la propiedad `cq:LastModifiedBy` debe replicarse desde el nodo de origen al nodo de destino.

1. Haga clic en **Guardar todo**.

### Creación de la Live Copy {#create-the-live-copy}

[Cree una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) de la rama en inglés/productos del sitio de referencia de We.Retail usando su configuración de despliegue:

* **Source**: `/content/we-retail/language-masters/en/products`

* **Configuración de despliegue**: Ejemplo de configuración de despliegue

Active la página **Productos** (inglés) de la rama de origen y observe los mensajes de registro que genera la clase `LiveAction`:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

<!--
## Removing the Chapters Step in the Create Site Wizard {#removing-the-chapters-step-in-the-create-site-wizard}

In some cases, the **Chapters** selection is not required in the create site wizard (only the **Languages** selection is required). To remove this step in the default We.Retail English blueprint:

1. In CRX Explorer, remove the node:
   `/etc/blueprints/weretail-english/jcr:content/dialog/items/tabs/items/tab_chap`.

1. Navigate to `/libs/wcm/msm/templates/blueprint/defaults/livecopy_tab/items` and create a node:

    1. **Name** = `chapters`; **Type** = `cq:Widget`.

1. Add following properties to the new node:

    1. **Name** = `name`; **Type** = `String`; **Value** = `msm:chapterPages`

    1. **Name** = `value`; **Type** = `String`; **Value** = `all`

    1. **Name** = `xtype`; **Type** = `String`; **Value** = `hidden`
-->

## Cambiar nombres de idiomas y países predeterminados {#changing-language-names-and-default-countries}

AEM utiliza un conjunto predeterminado de códigos de idioma y país.

* El código de idioma predeterminado es el código de dos letras en minúsculas, tal como se define en la norma ISO-639-1.
* El código de país predeterminado es el código de dos letras en minúsculas o mayúsculas, tal como se define en la norma ISO 3166.

MSM utiliza una lista almacenada de códigos de idioma y país para determinar el nombre del país asociado al nombre de la versión de idioma de la página. Si es necesario, puede cambiar los siguientes aspectos de la lista:

* Títulos de idiomas
* Nombres de países
* Países predeterminados para idiomas (para códigos como `en`, `de`, entre otros)

La lista de idiomas se almacena debajo del nodo `/libs/wcm/core/resources/languages`. Cada nodo secundario representa un idioma o un idioma-país:

* El nombre del nodo es el código de idioma (como `en` o `de`) o el código de idioma_país (como `en_us` o `de_ch`).

* La propiedad `language` del nodo almacena el nombre completo del idioma del código.
* La propiedad `country` del nodo almacena el nombre completo del país para el código.
* Cuando el nombre del nodo consiste únicamente en un código de idioma (como `en`), la propiedad del país es `*` y una propiedad adicional de `defaultCountry` almacena el código del idioma-país para indicar el país que se va a utilizar.

![Definición de idioma](assets/chlimage_1-76.png)

Para modificar los idiomas:

1. Abra CRXDE Lite en el explorador web; por ejemplo, [https://localhost:4502/crx/de](https://localhost:4502/crx/de)
1. Seleccione la carpeta `/apps`, haga clic en **Crear** y luego en **Crear carpeta.**

   Asigne un nombre a la nueva carpeta `wcm`.

1. Repita el paso anterior para crear el árbol de carpetas `/apps/wcm/core`. Cree un nodo de tipo `sling:Folder` en `core` llamado `resources`. <!-- ![Resources](assets/chlimage_1-77.png) -->

1. Haga clic con el botón derecho en el nodo `/libs/wcm/core/resources/languages` y haga clic en **Copiar**.
1. Haga clic con el botón derecho en la carpeta `/apps/wcm/core/resources` y haga clic en **Pegar**. Modifique los nodos secundarios según sea necesario.
1. Haga clic en **Guardar todo**.
1. Haga clic en **Herramientas**, **Operaciones** y luego en **Consola web**. Desde esta consola, haz clic en **OSGi** y luego en **Configuración**.
1. Busque y haga clic en **Administrador de idioma CQ WCM Day**, cambie el valor de **Lista de idioma** a `/apps/wcm/core/resources/languages` y luego haga clic en **Guardar**.

   ![Administrador de idioma CQ WCM por día](assets/chlimage_1-78.png)

## Configuración de los bloqueos MSM en las propiedades de página (IU táctil) {#configuring-msm-locks-on-page-properties-touch-enabled-ui}

Al crear una propiedad de página personalizada, es posible que tenga que considerar si la nueva propiedad debe cumplir los requisitos para su despliegue en cualquier Live Copy.

Por ejemplo, si se agregan dos propiedades de página nuevas:

* Correo electrónico de contacto:

   * No es necesario desplegar esta propiedad, ya que será diferente en cada país (o marca, etc.).

* Estilo visual clave:

   * El requisito del proyecto es que esta propiedad se implemente, ya que es (generalmente) común a todos los países (o marcas, etc.).

A continuación, debe asegurarse de que:

* Correo electrónico de contacto:

* Se ha excluido de las propiedades desplegadas; consulte [Exclusión de propiedades y tipos de nodos de la sincronización](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization).

* Estilo visual clave:

* Asegúrese de que no tiene permiso para editar esta propiedad en la interfaz de usuario táctil a menos que se cancele la herencia, y que también puede restablecer la herencia; esto se controla haciendo clic en los vínculos de cadena/cadena rota que alternan para indicar el estado de la conexión.

La propiedad dialog controla si una propiedad de página está sujeta a despliegue y, por lo tanto, a cancelación o restablecimiento de la herencia al editar:

* `cq-msm-lockable`

   * es aplicable a los elementos de un cuadro de diálogo de IU táctil
   * creará el símbolo de vínculo de cadena en el cuadro de diálogo
   * solo permite editar si se cancela la herencia (el vínculo de cadena está roto)
   * solo se aplica al primer nivel secundario del recurso
      * **Tipo**: `String`

      * **Value**: contiene el nombre de la propiedad en consideración (y es comparable al valor de la propiedad `name`; por ejemplo, vea

        `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

Cuando se ha definido `cq-msm-lockable`, romper/cerrar la cadena interactuará con MSM de la siguiente manera:

* si el valor de `cq-msm-lockable` es:

   * **Relativo** (por ejemplo, `myProperty` o `./myProperty`)

      * agregará y quitará la propiedad de `cq:propertyInheritanceCancelled`.

   * **Absoluto** (por ejemplo, `/image`)

      * romper la cadena cancelará la herencia agregando el mixin `cq:LiveSyncCancelled` a `./image` y estableciendo `cq:isCancelledForChildren` en `true`.

      * al cerrar la cadena, se revierte la herencia.

>[!NOTE]
>
>`cq-msm-lockable` se aplica al primer nivel secundario del recurso que se va a editar y no funciona en ningún antecesor de nivel más profundo, independientemente de si el valor se define como absoluto o relativo.

>[!NOTE]
>
>Al volver a habilitar la herencia, la propiedad de página Live Copy no se sincroniza automáticamente con la propiedad de origen. Puede solicitar manualmente una sincronización si es necesario.
