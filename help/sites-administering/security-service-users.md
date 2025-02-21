---
title: Usuarios de servicio en Adobe Experience Manager
description: Obtenga información acerca de los usuarios de servicio en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
feature: Administering
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---


# Usuarios de servicio en Adobe Experience Manager (AEM) {#service-users-in-aem}

## Información general {#overview}

La forma principal de obtener una resolución de sesión o de recursos de administración en AEM era usar los métodos `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` proporcionados por Sling.

Sin embargo, ninguno de estos métodos se diseñó en torno al [principio del menor privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege). Facilita demasiado a los desarrolladores no planificar una estructura adecuada y los niveles de control de acceso (ACL) correspondientes para su contenido desde el principio. Si existe una vulnerabilidad en un servicio de este tipo, a menudo se producen escalaciones de privilegios para el usuario `admin`, incluso si el código en sí no necesita privilegios administrativos para funcionar.

## Cómo eliminar gradualmente las sesiones de administración {#how-to-phase-out-admin-sessions}

### Prioridad 0: ¿La función está activa/necesaria/abandonada? {#priority-is-the-feature-active-needed-derelict}

Puede haber casos en los que no se utilice la sesión de administración o en los que la función esté completamente deshabilitada. Si es así con su implementación, asegúrese de quitar la característica por completo o de ajustarla con [código NOP](https://en.wikipedia.org/wiki/NOP).

### Prioridad 1: Utilizar La Sesión De Solicitud {#priority-use-the-request-session}

Siempre que sea posible, refactorice la función para que la sesión de solicitud autenticada dada se pueda utilizar para leer o escribir contenido. Si esto no es factible, a menudo se puede lograr aplicando las prioridades siguientes a las siguientes.

### Prioridad 2: Reestructurar contenido {#priority-restructure-content}

Muchos problemas se pueden resolver reestructurando el contenido. Tenga en cuenta estas reglas sencillas al realizar la reestructuración:

* **Cambiar control de acceso**

   * Asegúrese de que los usuarios o grupos que realmente necesitan acceso tengan acceso;

* **Refinar la estructura de contenido**

   * Muévalo a otras ubicaciones, por ejemplo, donde el control de acceso coincida con las sesiones de solicitud disponibles;
   * Cambiar la granularidad del contenido;

* **Refactorice su código para que sea un servicio apropiado**

   * Cambie la lógica empresarial del código JSP al servicio. Esto permite modelar contenido de forma diferente.

Además, asegúrese de que todas las nuevas funciones que desarrolle se ajusten a estos principios:

* **Los requisitos de seguridad deben orientar la estructura de contenido**

   * La gestión del control de acceso debería ser natural
   * El control de acceso lo debe aplicar el repositorio, no la aplicación

* **Usar tipos de nodo**

   * Restringir el conjunto de propiedades que se pueden establecer

* **Respetar la configuración de privacidad**

   * Si hay perfiles privados, un ejemplo sería no exponer la imagen de perfil, el correo electrónico o el nombre completo que se encuentra en el nodo privado `/profile`.

## Estricto control de acceso {#strict-access-control}

Tanto si aplica el control de acceso al reestructurar el contenido como si lo hace para un nuevo usuario de servicio, debe aplicar las ACL más estrictas posibles. Utilice todas las posibilidades de control de acceso:

* Por ejemplo, en lugar de aplicar `jcr:read` en `/apps`, aplíquelo solo a `/apps/*/components/*/analytics`

* Usar [restricciones](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html?lang=es)

* Aplicar ACL para los tipos de nodo
* Limitar permisos

   * por ejemplo, cuando solo necesite escribir propiedades, no conceda el permiso `jcr:write`; use `jcr:modifyProperties` en su lugar

## Usuarios de servicio y asignaciones {#service-users-and-mappings}

Si lo anterior falla, Sling 7 ofrece un servicio de asignación de usuarios de servicio, que le permite configurar una asignación de paquete a usuario y dos métodos de API correspondientes:

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

Los métodos devuelven un solucionador de sesión/recurso con los privilegios de un usuario configurado solamente. Estos métodos tienen las siguientes características:

* Permiten asignar servicios a los usuarios
* Permiten definir a los usuarios de subservicios
* El punto de configuración central es: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [&quot;:&quot; subservice-name]

* `service-id` está asignado a un solucionador de recursos o a un ID de usuario del repositorio JCR para la autenticación
* `service-name` es el nombre simbólico del paquete que proporciona el servicio

## Otras recomendaciones {#other-recommendations}

### Reemplazar la sesión de administración por un usuario de servicio {#replacing-the-admin-session-with-a-service-user}

Un usuario de servicio es un usuario de JCR sin contraseña establecida y con un conjunto mínimo de privilegios necesarios para realizar una tarea específica. Si no se ha establecido ninguna contraseña, no es posible iniciar sesión con un usuario del servicio.

Una forma de dejar de utilizar una sesión administrativa es reemplazarla por sesiones de usuarios de servicio. También podría ser reemplazado por varios usuarios de subservicios si es necesario.

Para reemplazar la sesión de administración por un usuario de servicio, debe realizar los siguientes pasos:

1. Identifique los permisos necesarios para su servicio, teniendo en cuenta el principio de permisos mínimos.
1. Compruebe si ya hay un usuario disponible con exactamente la configuración de permisos que necesita. Cree un usuario de servicio del sistema si ningún usuario existente coincide con sus necesidades. RTC es necesario para crear un usuario de servicio. A veces, tiene sentido crear varios usuarios de subservicios (por ejemplo, uno para escribir y otro para leer) para compartimentar el acceso aún más.
1. Configure y pruebe los ACE para el usuario.
1. Agregue una asignación `service-user` para su servicio y para `user/sub-users`

1. Ponga a disposición del paquete la función de usuario sling: actualice a la versión más reciente de `org.apache.sling.api`.

1. Reemplace `admin-session` en su código con las API `loginService` o `getServiceResourceResolver`.

## Creación de un usuario de servicio {#creating-a-new-service-user}

Después de comprobar que ningún usuario de la lista de usuarios del servicio AEM es aplicable a su caso de uso y de aprobar los problemas de RTC correspondientes, agregue el nuevo usuario al contenido predeterminado.

El método recomendado es crear un usuario de servicio para usar el explorador del repositorio en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*

El objetivo es obtener una propiedad `jcr:uuid` válida que es obligatoria para crear el usuario mediante la instalación de un paquete de contenido.

Puede crear usuarios de servicios de:

1. Ir al explorador del repositorio en *https://&lt;server>:&lt;port>/crx/explorer/index.jsp*
1. Para iniciar sesión como administrador, presione el vínculo **Iniciar sesión** en la esquina superior izquierda de la pantalla.
1. A continuación, cree y asigne un nombre al usuario del sistema. Para crear el usuario como del sistema, establezca la ruta intermedia como `system` y agregue subcarpetas opcionales según sus necesidades:

   ![chlimage_1-102](assets/chlimage_1-102a.png)

1. Compruebe que el nodo de usuario del sistema tenga el siguiente aspecto:

   ![chlimage_1-103](assets/chlimage_1-103a.png)

   >[!NOTE]
   >
   >No hay tipos de mezcla asociados a usuarios del servicio. Esto significa que no hay directivas de control de acceso para los usuarios del sistema.

Al agregar el archivo .content.xml correspondiente al contenido del paquete, asegúrese de haber establecido `rep:authorizableId` y de que el tipo principal sea `rep:SystemUser`. Debería tener un aspecto similar al siguiente:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Agregar una modificación de configuración a la configuración de ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para agregar una asignación del servicio a los usuarios del sistema correspondientes, cree una configuración de fábrica para el servicio [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html). Para mantener este elemento modular, dicha configuración se puede proporcionar mediante el [mecanismo de modificación de Sling](https://issues.apache.org/jira/browse/SLING-3578). La manera recomendada de instalar estas configuraciones con su paquete es usando [Sling Initial Content Loading](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Cree una subcarpeta SLING-INF/content debajo de la carpeta src/main/resources del paquete
1. En esta carpeta, cree un archivo llamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.modified-&lt;algún nombre único para su configuración de fábrica>.xml con el contenido de su configuración de fábrica (incluidas todas las asignaciones de usuarios de subservicios). Ejemplo:

1. Crear una carpeta `SLING-INF/content` debajo de la carpeta `src/main/resources` del paquete;
1. En esta carpeta, cree un archivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` con el contenido de la configuración de fábrica, incluidas todas las asignaciones de usuario de subservicio.

   Por motivos ilustrativos, tome el archivo llamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <node>
       <primaryNodeType>sling:OsgiConfig</primaryNodeType>
       <property>
           <name>user.default</name>
           <value></value>
       </property>
       <property>
           <name>user.mapping</name>
           <values>
               <value>com.adobe.granite.auth.saml=authentication-service</value>
           </values>
       </property>
   </node>
   ```

1. Haga referencia al contenido inicial de Sling en la configuración de `maven-bundle-plugin` en `pom.xml` de su paquete. Ejemplo:

   ```xml
   <Sling-Initial-Content>
      SLING-INF/content;path:=/libs/system/config;overwrite:=true;
   </Sling-Initial-Content>
   ```

1. Instale el paquete y asegúrese de que la configuración de fábrica está instalada. Para ello:

   * Ir a la consola web en *https://serverhost:serveraddress/system/console/configMgr*
   * Busque **Servicio de asignación de usuarios de Apache Sling Service**
   * Haga clic en el vínculo para ver si se ha implementado la configuración adecuada.

## Tratar sesiones compartidas en servicios {#dealing-with-shared-sessions-in-services}

Las llamadas a `loginAdministrative()` suelen aparecer junto con las sesiones compartidas. Estas sesiones se adquieren al activarse el servicio y solo se cierran después de que este se detiene. Aunque esta es una práctica común, conduce a dos problemas:

* **Seguridad:** Estas sesiones de administración se usan para almacenar en caché y devolver recursos u otros objetos enlazados a la sesión compartida. Más adelante en la pila de llamadas, estos objetos podrían adaptarse a sesiones o solucionadores de recursos con privilegios elevados. A menudo, el llamador no tiene claro que es una sesión de administración con la que opera.
* **Rendimiento:** En Oak, las sesiones compartidas pueden causar problemas de rendimiento y no se recomienda usarlas.

La solución más obvia para el riesgo de seguridad es simplemente reemplazar la llamada de `loginAdministrative()` con una llamada de `loginService()` a un usuario con privilegios restringidos. Sin embargo, esto no tiene ningún impacto en ninguna degradación potencial del rendimiento. Una posibilidad de mitigar que es envolver toda la información solicitada en un objeto que no tiene asociación con la sesión. A continuación, cree (o destruya) la sesión bajo demanda.

El método recomendado es refactorizar la API del servicio para dar al que llama control sobre la creación o destrucción de la sesión.

## Sesiones administrativas en JSP {#administrative-sessions-in-jsps}

Los JSP no pueden usar `loginService()` porque no hay ningún servicio asociado. Sin embargo, las sesiones administrativas en los JSP suelen ser un signo de una violación del paradigma de MVC.

Esto se puede solucionar de dos maneras:

1. Reestructurar el contenido de manera que permita manipularlo con la sesión del usuario;
1. Extraer la lógica a un servicio que proporciona una API que luego JSP puede utilizar.

El primer método es el preferido.

## Procesamiento de eventos, preprocesadores de replicación y trabajos {#processing-events-replication-preprocessors-and-jobs}

Al procesar eventos o trabajos, y a veces flujos de trabajo, se pierde la sesión correspondiente que activó el evento. Esto lleva a que los controladores de eventos y los procesadores de trabajos a menudo utilicen sesiones administrativas para realizar su trabajo. Existen diferentes enfoques concebibles para resolver este problema, cada uno con sus ventajas y desventajas:

1. Pase `user-id` en la carga útil de evento y utilice la suplantación.

   **Ventajas:** Fácil de usar.

   **Desventajas:** Sigue usando `loginAdministrative()`. Vuelve a autenticar una solicitud que ya se ha autenticado.

1. Crear o reutilizar un usuario de servicio que tenga acceso a los datos.

   **Ventajas:** coherente con el diseño actual. Necesita un cambio mínimo.

   **Desventajas:** Necesita que los usuarios de servicios avanzados sean flexibles, lo que puede llevar fácilmente a escalaciones de privilegios. Elude el modelo de seguridad.

1. Pase una serialización de `Subject` en la carga útil de evento y cree un `ResourceResolver` basado en ese asunto. Un ejemplo sería el uso de JAAS `doAsPrivileged` en `ResourceResolverFactory`.

   **Ventajas:** Limpie la implementación desde el punto de vista de la seguridad. Evita la reautenticación y funciona con los privilegios originales. El código relevante para la seguridad es transparente para el consumidor del evento.

   **Desventajas:** Necesita refactorización. El hecho de que el código relevante para la seguridad sea transparente para el consumidor del evento también puede provocar problemas.

El tercer enfoque es la técnica de procesamiento preferida.

## Procesos de flujo de trabajo {#workflow-processes}

Dentro de las implementaciones de procesos de flujo de trabajo, se pierde la sesión de usuario correspondiente que activó el flujo de trabajo. Esto lleva a procesos de flujo de trabajo que a menudo utilizan sesiones administrativas para realizar su trabajo.

Para solucionar estos problemas, se recomienda utilizar los mismos enfoques mencionados en [Procesar eventos, Preprocesadores de replicación y Trabajos](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs).

## Procesadores Sling POST y páginas eliminadas {#sling-post-processors-and-deleted-pages}

Hay un par de sesiones administrativas utilizadas en las implementaciones del procesador Sling POST. Normalmente, las sesiones administrativas se utilizan para acceder a nodos que están pendientes de eliminación dentro del POST que se está procesando. En consecuencia, ya no están disponibles a través de la sesión de solicitud. Se puede acceder a un nodo cuya eliminación está pendiente para revelar metadatos que, de lo contrario, no deberían estar accesibles.
