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
exl-id: 893d04cb-3a71-4400-9ca4-62ad46aacfdd
source-git-commit: 4c6423d295aa93f6f7048a5ac919b551f3f305d7
workflow-type: tm+mt
source-wordcount: '1872'
ht-degree: 84%

---

# Usuarios de servicio en Adobe Experience Manager (AEM) {#service-users-in-aem}

## Información general {#overview}

La forma principal de obtener una resolución de sesiones o de recursos de administración en AEM era usar los métodos `SlingRepository.loginAdministrative()` y `ResourceResolverFactory.getAdministrativeResourceResolver()` proporcionados por Sling.

Sin embargo, ninguno de estos métodos se diseñó en torno al [principio de mínimo privilegio](https://en.wikipedia.org/wiki/Principle_of_least_privilege). Hace que sea demasiado fácil para un desarrollador no planificar desde el principio una estructura adecuada y los correspondientes niveles de control de acceso (ACL) para su contenido. Si existe una vulnerabilidad en un servicio de este tipo, a menudo se producen escalaciones de privilegios para el usuario `admin`, incluso si el código en sí no necesita privilegios administrativos para funcionar.

## Cómo eliminar gradualmente las sesiones de administración {#how-to-phase-out-admin-sessions}

### Prioridad 0: ¿La función está activa/es necesaria/está en desuso? {#priority-is-the-feature-active-needed-derelict}

Puede haber casos en los que no se utilice la sesión de administración o en los que la función esté deshabilitada por completo. Si es así con su implementación, asegúrese de quitar la característica del todo o de ajustarla con [código NOP](https://en.wikipedia.org/wiki/NOP).

### Prioridad 1: Utilizar la sesión de solicitud {#priority-use-the-request-session}

Siempre que sea posible, refactorice la función para que la sesión de solicitud autenticada dada se pueda utilizar para leer o escribir contenido. Si esto no es factible, a menudo se puede lograr aplicando las prioridades que se indican a continuación.

### Prioridad 2: Reestructurar el contenido {#priority-restructure-content}

Muchos problemas se pueden resolver reestructurando el contenido. Tenga en cuenta estas reglas sencillas al realizar la reestructuración:

* **Cambiar el control de acceso**

   * Asegúrese de que los usuarios o grupos que de verdad necesiten acceso lo tengan;

* **Refinar la estructura de contenido**

   * Muévalo a otras ubicaciones, por ejemplo, donde el control de acceso coincida con las sesiones de solicitud disponibles;
   * Cambiar la granularidad del contenido;

* **Refactorizar su código para que sea un servicio apropiado**

   * Cambie la lógica empresarial del código JSP al servicio. Esto permite un modelado de contenido diferente.

Además, asegúrese de que todas las nuevas funciones que desarrolle se ajusten a estos principios:

* **Los requisitos de seguridad deben dirigir la estructura de contenido**

   * La administración del control de acceso debería ser natural
   * El control de acceso lo debe aplicar el repositorio, no la aplicación

* **Utilizar tipos de nodos**

   * Restrinja el conjunto de propiedades que se pueden establecer

* **Respetar la configuración de privacidad**

   * Si hay perfiles privados, un ejemplo sería no exponer la imagen de perfil, el correo electrónico o el nombre completo que se encuentra en el nodo privado `/profile`.

## Aplique un control de acceso estricto {#strict-access-control}

Tanto si aplica el control de acceso al reestructurar el contenido como si lo hace para un nuevo usuario de servicio, debe aplicar los ACL más estrictos posibles. Utilice todas las posibilidades del control de acceso:

* Por ejemplo, en lugar de aplicar `jcr:read` en `/apps`, aplíquelo solo a `/apps/*/components/*/analytics`

* Usar [restricciones](https://jackrabbit.apache.org/oak/docs/security/authorization/restriction.html?lang=es)

* Aplicar ACL para los tipos de nodos
* Limitar permisos

   * por ejemplo, cuando solo necesite escribir propiedades, no conceda el permiso `jcr:write`; use `jcr:modifyProperties` en su lugar

## Usuarios de servicio y asignaciones {#service-users-and-mappings}

Si lo anterior falla, Sling 7 ofrece un servicio de asignación de usuarios de servicio, que le permite configurar una asignación de paquete a usuario y dos métodos de API correspondientes:

* [`SlingRepository.loginService()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/jcr/api/SlingRepository.html#loginService-java.lang.String-java.lang.String-)
* [`ResourceResolverFactory.getServiceResourceResolver()`](https://sling.apache.org/apidocs/sling7/org/apache/sling/api/resource/ResourceResolverFactory.html#getServiceResourceResolver-java.util.Map-)

Los métodos devuelven una resolución de sesiones/recursos con los privilegios de un usuario configurado solamente. Estos métodos tienen las siguientes características:

* Permiten asignar servicios a los usuarios
* Permiten definir a los usuarios de subservicio
* El punto de configuración central es: `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl`
* `service-id` = `service-name` [&quot;:&quot; subservice-name]

* `service-id` está asignado a una resolución de recursos o a un ID de usuario del repositorio JCR para la autenticación
* `service-name` es el nombre simbólico del paquete que proporciona el servicio

## Otras recomendaciones {#other-recommendations}

### Reemplazar la sesión de administración por un usuario de servicio {#replacing-the-admin-session-with-a-service-user}

Un usuario de servicio es un usuario de JCR sin contraseña establecida y con un conjunto mínimo de privilegios necesarios para realizar una tarea específica. Si no se ha establecido ninguna contraseña, no es posible iniciar sesión con un usuario de servicio.

Una forma de poner en desuso una sesión administrativa es reemplazarla por sesiones de usuarios de servicio. También podría sustituirse por varios usuarios de subservicios, si es necesario.

Para reemplazar la sesión de administración por un usuario de servicio, debe seguir estos pasos:

1. Identifique los permisos necesarios para su servicio y tenga en cuenta el principio de permisos mínimos.
1. Compruebe si ya hay un usuario disponible con exactamente la configuración de permisos que necesita. Cree un usuario de servicio del sistema si ningún usuario existente coincide con sus necesidades. Se necesita RTC para crear un usuario de servicio. A veces, tiene sentido crear varios usuarios de subservicios (por ejemplo, uno de escritura y otro de lectura) para compartimentar el acceso aún más.
1. Configure y pruebe las ACE para el usuario.
1. Añada una asignación `service-user` para su servicio y para `user/sub-users`

1. Haga que la funcionalidad de usuario de servicio de Sling esté disponible en su paquete: actualice a la versión más reciente de `org.apache.sling.api`.

1. Reemplace `admin-session` en su código con las API `loginService` o `getServiceResourceResolver`.

## Creación de un usuario de servicio {#creating-a-new-service-user}

Después de comprobar que ningún usuario de la lista de usuarios de servicio de AEM es aplicable a su caso de uso y de aprobar los problemas de RTC correspondientes, añada el nuevo usuario al contenido predeterminado.

>[!IMPORTANT]
>
>El Explorador de CRX (`/crx/explorer/index.jsp`) no está disponible en entornos AEM 6.5 LTS y no debe usarse para crear usuarios de servicio. Los usuarios de servicio existentes creados mediante el Explorador de CRX siguen funcionando. Para nuevos usuarios del servicio, utilice uno de los enfoques que se describen a continuación.

>[!NOTE]
>
>No hay tipos de mezcla asociados a usuarios de servicio en el nivel de nodo JCR. Esto significa que los nodos de usuario del sistema no tienen directivas de control de acceso adjuntas directamente a ellos. En su lugar, el control de acceso se administra por separado, por ejemplo, mediante instrucciones ACL RepoInit o la configuración ACL de nivel de repositorio.

### Uso de la inicialización del repositorio de Sling (RepoInit) {#creating-service-user-repoinit}

El método recomendado es usar [Inicialización del repositorio de Sling (RepoInit)](https://sling.apache.org/documentation/bundles/repository-initialization.html) para crear usuarios de servicio. RepoInit permite definir los usuarios del servicio y sus ACL de forma declarativa mediante un lenguaje de script simple.

Para crear un usuario de servicio con RepoInit, agregue una propiedad `scripts` a una configuración OSGi para `org.apache.sling.jcr.repoinit.RepositoryInitializer`:

```
create service user my-service-user with path system/cq

set ACL for my-service-user
    allow jcr:read on /content
end
```

La directiva `with path system/cq` coloca al usuario del servicio bajo `/home/users/system/cq` en el repositorio. Puede elegir una ruta que coincida con la estructura organizativa del proyecto (por ejemplo, `system/myproject`). Si los nodos de ruta intermedia no existen, use `with forced path` para crearlos automáticamente.

Este método es recomendable porque:

* Define los usuarios y permisos del servicio como código, lo que los hace reproducibles y controlados por versiones
* Gestiona automáticamente la creación durante la inicialización del repositorio
* Funciona en los entornos AEM 6.5 LTS y AEM as a Cloud Service, aunque pueden existir diferencias de sintaxis menores entre las versiones de Sling. Consulte la documentación de RepoInit para su plataforma de destino

### Uso de un paquete de contenido {#creating-service-user-content-package}

También puede crear un usuario de servicio incluyendo `.content.xml` en el paquete de contenido. Asegúrese de haber establecido `rep:authorizableId` y de que el tipo principal es `rep:SystemUser`. Se requiere una propiedad `jcr:uuid` válida para que el usuario se cree correctamente durante la instalación del paquete de contenido. Puede generar un UUID con un generador UUID v4 estándar (por ejemplo, la herramienta de línea de comandos `uuidgen` o cualquier generador UUID en línea). `.content.xml` debe tener un aspecto similar al siguiente:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:rep="internal"
    jcr:primaryType="rep:SystemUser"
    jcr:uuid="4917dd68-a0c1-3021-b5b7-435d0044b0dd"
    rep:principalName="authentication-service"
    rep:authorizableId="authentication-service"/>
```

## Adición de una modificación de configuración a la configuración de ServiceUserMapper {#adding-a-configuration-amendment-to-the-serviceusermapper-configuration}

Para añadir una asignación desde su servicio a los usuarios del sistema correspondientes, cree una configuración de fábrica para el servicio [`ServiceUserMapper`](https://sling.apache.org/apidocs/sling7/org/apache/sling/serviceusermapping/ServiceUserMapper.html).  Para mantener este elemento modular, dicha configuración se puede proporcionar mediante el [mecanismo de modificación de Sling](https://issues.apache.org/jira/browse/SLING-3578). La manera recomendada de instalar estas configuraciones con su paquete es usando la [carga inicial de contenido de Sling](https://sling.apache.org/documentation/bundles/content-loading-jcr-contentloader.html):

1. Cree una subcarpeta SLING-INF/content debajo de la carpeta src/main/resources del paquete
1. En esta carpeta, cree un archivo llamado org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-&lt;algún nombre único para su configuración de fábrica>.xml con el contenido de su configuración de fábrica (incluidas todas las asignaciones de usuarios de subservicios). Ejemplo:

1. Cree una carpeta `SLING-INF/content` debajo de la carpeta `src/main/resources` del paquete;
1. En esta carpeta, cree un archivo `named org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-<a unique name for your factory configuration>.xml` con el contenido de la configuración de fábrica, incluidas todas las asignaciones de usuario de subservicio.

   Por motivos ilustrativos, coja el archivo llamado `org.apache.sling.serviceusermapping.impl.ServiceUserMapperImpl.amended-com.adobe.granite.auth.saml.xml`:

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

1. Instale el paquete y asegúrese de que la configuración de fábrica está instalada. Para ello, haga lo siguiente:

   * Visite la consola web en *https://serverhost:serveraddress/system/console/configMgr*
   * Busque **Apache Sling Service User Mapper Service Amendment**
   * Haga clic en el vínculo para ver si se ha implementado la configuración adecuada.

## Trato de sesiones compartidas en servicios {#dealing-with-shared-sessions-in-services}

Las llamadas a `loginAdministrative()` suelen aparecer junto con las sesiones compartidas. Estas sesiones se adquieren al activarse el servicio y solo se cierran después de que este se detenga. Aunque esta es una práctica común, causa dos problemas:

* **Seguridad:** estas sesiones de administración se usan para almacenar en caché y devolver recursos u otros objetos enlazados a la sesión compartida. Más adelante en la pila de llamadas, estos objetos podrían adaptarse a sesiones o resoluciones de recursos con privilegios elevados. A menudo, quien realiza la llamada no tiene claro que está operando con una sesión de administración.
* **Rendimiento:** en Oak, las sesiones compartidas pueden causar problemas de rendimiento y no se recomienda usarlas.

La solución más obvia para el riesgo de seguridad es simplemente reemplazar la llamada de `loginAdministrative()` con una llamada de `loginService()` a un usuario con privilegios restringidos. Sin embargo, esto no tiene ningún impacto en ninguna degradación potencial del rendimiento. Una posibilidad de mitigarlo es envolver toda la información solicitada en un objeto que no esté asociado con la sesión. A continuación, cree (o destruya) la sesión bajo demanda.

El enfoque recomendado es refactorizar la API del servicio para dar control a quien realiza la llamada sobre la creación o destrucción de la sesión.

## Sesiones administrativas en JSP {#administrative-sessions-in-jsps}

Las JSP no pueden usar `loginService()`, ya que no hay ningún servicio asociado. Sin embargo, las sesiones administrativas en las JSP suelen indicar una vulneración del paradigma MVC.

Esto se puede solucionar de dos maneras:

1. Reestructurando el contenido de forma que permita manipularlo con la sesión del usuario;
1. Extrayendo la lógica a un servicio que proporcione una API que luego pueda utilizar la JSP.

El primer método es el preferido.

## Procesamiento de eventos, preprocesadores de replicación y trabajos {#processing-events-replication-preprocessors-and-jobs}

Al procesar eventos o trabajos, y a veces flujos de trabajo, se pierde la sesión correspondiente que activó el evento. Esto lleva a que los controladores de eventos y los procesadores de trabajos a menudo utilicen sesiones administrativas para hacer su trabajo. Existen diferentes enfoques concebibles para resolver este problema, cada uno con sus ventajas y desventajas:

1. Pasar `user-id` en la carga útil de evento y utilice la suplantación.

   **Ventajas:** es fácil de usar.

   **Desventajas:** sigue utilizando `loginAdministrative()`. Vuelve a autenticar una solicitud que ya se ha autenticado.

1. Crear o reutilizar un usuario de servicio que tenga acceso a los datos.

   **Ventajas:** es coherente con el diseño actual. Necesita un cambio mínimo.

   **Desventajas:** necesita que los usuarios de servicio avanzados sean flexibles, lo que puede llevar fácilmente a escalaciones de privilegios. Elude el modelo de seguridad.

1. Pasar una serialización de `Subject` en la carga útil de evento y cree una `ResourceResolver` basado en ese asunto. Un ejemplo sería el uso de JAAS `doAsPrivileged` en `ResourceResolverFactory`.

   **Ventajas:** es una implementación limpia desde el punto de vista de la seguridad. Evita la reautenticación y funciona con los privilegios originales. El código relevante para la seguridad es transparente para el consumidor del evento.

   **Desventajas:** necesita refactorización. El hecho de que el código relevante para la seguridad sea transparente para el consumidor del evento también puede provocar problemas.

El tercer enfoque es la técnica de procesamiento preferida.

## Procesos de flujo de trabajo {#workflow-processes}

Dentro de las implementaciones de procesos de flujo de trabajo, se pierde la sesión de usuario correspondiente que activó el flujo de trabajo. Esto lleva a procesos de flujo de trabajo que, a menudo, utilizan sesiones administrativas para hacer su trabajo.

Para solucionar estos problemas, se recomienda emplear los mismos enfoques mencionados en [Procesamiento de eventos, preprocesadores de replicación y trabajos](/help/sites-administering/security-service-users.md#processing-events-replication-preprocessors-and-jobs).

## Procesadores POST de Sling y páginas eliminadas {#sling-post-processors-and-deleted-pages}

Hay un par de sesiones administrativas utilizadas en las implementaciones de procesadores POST de Sling. Por lo general, las sesiones administrativas se usan para acceder a nodos que están pendientes de eliminación dentro del POST que se está procesando. En consecuencia, ya no están disponibles a través de la sesión de solicitud. Se puede acceder a un nodo cuya eliminación está pendiente para revelar metadatos que, de otro modo, no deberían estar accesibles.
