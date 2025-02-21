---
title: Cómo acceder mediante programación al JCR de AEM
description: Puede modificar mediante programación nodos y propiedades ubicados dentro del repositorio de AEM, que forma parte de Adobe Experience Cloud
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 2%

---

# Cómo acceder mediante programación al JCR de AEM{#how-to-programmatically-access-the-aem-jcr}

Puede modificar mediante programación los nodos y las propiedades ubicados en el repositorio de Adobe CQ, que forma parte de Adobe Experience Cloud. Para acceder al repositorio de CQ, utilice la API de repositorio de contenido Java™ (JCR). Puede utilizar la API JCR de Java™ para crear, reemplazar, actualizar y eliminar contenido (CRUD) ubicado en el repositorio de Adobe CQ. Para obtener más información acerca de la API JCR de Java™, consulte [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Este artículo de desarrollo modifica el JCR Adobe CQ desde una aplicación Java™ externa. Por el contrario, puede modificar el JCR desde un paquete OSGi mediante la API JCR. Para obtener más información, consulte [Conservación de datos CQ en el repositorio de contenido Java™](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html).

>[!NOTE]
>
>Para usar la API JCR, agregue el archivo `jackrabbit-standalone-2.4.0.jar` a la ruta de clase de la aplicación Java™. Puede obtener este archivo JAR de la página web de la API JCR de Java™ en [https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html).

>[!NOTE]
>
>Para obtener información sobre cómo consultar el JCR de Adobe CQ mediante la API de consulta JCR, consulte [Consulta de datos de Adobe Experience Manager mediante la API de JCR](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html).

## Crear una instancia de repositorio {#create-a-repository-instance}

Aunque hay diferentes maneras de conectarse a un repositorio y establecer una conexión, este artículo de desarrollo utiliza un método estático que pertenece a la clase `org.apache.jackrabbit.commons.JcrUtils`. El nombre del método es `getRepository`. Este método toma un parámetro de cadena que representa la dirección URL del servidor Adobe CQ. Por ejemplo, `http://localhost:4503/crx/server`.

El método `getRepository` devuelve una instancia `Repository`, como se muestra en el ejemplo de código siguiente.

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## Crear una instancia de sesión {#create-a-session-instance}

La instancia `Repository` representa el repositorio de CRX. Utilice la instancia `Repository` para establecer una sesión con el repositorio. Para crear una sesión, invoque el método `login` de la instancia `Repository` y pase un objeto `javax.jcr.SimpleCredentials`. El método `login` devuelve una instancia `javax.jcr.Session`.

Para crear un objeto `SimpleCredentials`, utilice su constructor y pase los siguientes valores de cadena:

* El nombre de usuario;
* La contraseña correspondiente

Al pasar el segundo parámetro, llame al método `toCharArray` del objeto String. El código siguiente muestra cómo llamar al método `login` que devuelve un objeto `javax.jcr.Sessioninstance`.

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## Crear una instancia de nodo {#create-a-node-instance}

Usar una instancia de `Session` para crear una instancia de `javax.jcr.Node`. Una instancia de `Node` le permite realizar operaciones en el nodo. Por ejemplo, puede crear un nodo. Para crear un nodo que represente el nodo raíz, invoque el método `getRootNode` de la instancia `Session`, como se muestra en la línea de código siguiente.

```java
//Create a Node
Node root = session.getRootNode();
```

Una vez creada una instancia de `Node`, puede realizar tareas como crear otro nodo y agregarle un valor. Por ejemplo, el siguiente código crea dos nodos y agrega un valor al segundo nodo.

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## Recuperar valores de nodo {#retrieve-node-values}

Para recuperar un nodo y su valor, invoque el método `getNode` de la instancia `Node` y pase un valor de cadena que represente la ruta de acceso completa al nodo. Considere la estructura de nodos creada en el ejemplo de código anterior. Para recuperar el nodo de día, especifique adobe/day, como se muestra en el siguiente código:

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## Creación de nodos en el repositorio de Adobe CQ {#create-nodes-in-the-adobe-cq-repository}

El siguiente ejemplo de código Java™ representa una clase Java™ que se conecta a Adobe CQ, crea una instancia `Session` y agrega nuevos nodos. A un nodo se le asigna un valor de datos y, a continuación, el valor del nodo y su ruta se escriben en la consola. Cuando haya terminado con la sesión, asegúrese de cerrar la sesión.

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

Después de ejecutar el ejemplo de código completo y crear los nodos, puede ver los nuevos nodos en **[!UICONTROL CRXDE Lite]**, como se muestra en la siguiente ilustración.

![chlimage_1-68](assets/chlimage_1-68a.png)
