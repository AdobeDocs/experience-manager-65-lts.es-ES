---
title: Funciones remotas en el Generador de expresiones
description: El generador de expresiones de Administración de correspondencia permite crear expresiones y funciones remotas.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 100%

---

# Funciones remotas en el Generador de expresiones{#remote-functions-in-expression-builder}

Con el generador de expresiones, puede crear expresiones o condiciones que realicen cálculos sobre los valores de datos proporcionados por el diccionario de datos o por usuarios finales. Administración de correspondencia utiliza el resultado de la evaluación de expresiones para seleccionar recursos como texto, imágenes, listas y condiciones e insertarlos en la correspondencia según sea necesario.

## Crear expresiones y funciones remotas con el generador de expresiones {#creating-expressions-and-remote-functions-with-expression-builder}

El generador de expresiones utiliza internamente bibliotecas JSP EL, por lo que la expresión se adhiere a la sintaxis JSPEL. Para obtener más información, consulte [Expresiones de ejemplo](#exampleexpressions).

![Generador de expresiones](assets/expressionbuilder.png)

### Operadores {#operators}

Los operadores que están disponibles para utilizarlos en expresiones están disponibles en la barra superior del generador de expresiones.

### Expresiones de ejemplo {#exampleexpressions}

Estos son algunos ejemplos de JSP EL que puede utilizar con frecuencia en su solución de Administración de correspondencia:

* Para agregar dos números: ${number1 + number2}
* Para concatenar dos cadenas: ${str1} ${str2}
* Para comparar dos números: ${age &lt; 18}

Puede encontrar más información en la sección [Especificación JSP EL](https://download.oracle.com/otn-pub/jcp/jsp-2.1-fr-spec-oth-JSpec/jsp-2_1-fr-spec-el.pdf). El administrador de expresiones del lado del cliente no admite determinadas variables y funciones en la especificación JSP EL, en concreto:

* Los índices de recopilación y las claves de asignación (con el uso de la notación []) no son compatibles con los nombres de variables para expresiones evaluadas del lado del cliente.
* Los siguientes son los tipos de parámetros o de funciones devueltos utilizados en las expresiones:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.util.list
   * java.lang.Short
   * corto
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Doble
   * java.lang.Long
   * Largo
   * java.lang.Float
   * Flotante
   * java.util.Calendar
   * java.util.Date
   * java.util.List

### Función remota {#remote-function}

Las funciones remotas proporcionan la capacidad de usar lógica personalizada en expresiones. Puede escribir lógica personalizada para utilizarla en la expresión como método en Java y se puede utilizar la misma función dentro de las expresiones. Las funciones remotas disponibles se muestran en la pestaña “Funciones remotas”, a la izquierda del Editor de expresiones.

![remotefunction](assets/remotefunction.png)

#### Agregar funciones remotas personalizadas {#adding-custom-remote-functions}

Puede crear un paquete personalizado para exportar sus propias funciones remotas para usarlas dentro de las expresiones. Para crear un paquete personalizado para exportar sus propias funciones remotas, realice las siguientes tareas. Muestra cómo escribir una función personalizada que pone en mayúsculas su cadena de entrada.

1. Defina una interfaz para el servicio OSGi que contenga métodos que exporte el Administrador de expresiones para utilizarlos.
1. Declare los métodos en la interfaz A y anótelos con la anotación @ServiceMethod (com.adobe.exm.expeval.ServiceMethod). El Administrador de expresiones ignora los métodos no anotados. La anotación ServiceMethod tiene los siguientes atributos opcionales que también se pueden especificar:

   1. **Habilitado**: determina si este método está habilitado. El Administrador de expresiones ignora los métodos desactivados.
   1. **familyId**: especifica la familia (grupo) del método. Si está vacío, el Administrador de expresiones supone que el método pertenece a la familia predeterminada. No hay ningún registro de familias (excepto el predeterminado) desde donde se eligen las funciones. El Administrador de expresiones crea de manera dinámica el registro mediante una unión de todos los ID de familia especificados por todas las funciones exportadas por los distintos paquetes. Asegúrese de que el ID que especifican aquí sea legible, ya que también se mostrará en la interfaz de usuario de creación de expresiones.
   1. **displayName**: un nombre legible en lenguaje natural para la función. Este nombre se utiliza con fines de visualización en la interfaz de usuario de creación. Si está vacío, el Administrador de expresiones creará un nombre predeterminado con el prefijo y el nombre local de la función.
   1. **Descripción**: una descripción detallada de la función. Esta descripción se utiliza con fines de visualización en la interfaz de usuario de creación. Si está vacía, el Administrador de expresiones creará una descripción predeterminada con el prefijo y el nombre local de la función.

   ```java
   package mergeandfuse.com;
   import com.adobe.exm.expeval.ServiceMethod;
   
   public interface RemoteFunction {
    @ServiceMethod(enabled=true,displayName="Returns_all_caps",description="Function to convert to all CAPS", familyId="remote")
    public String toAllCaps(String name);
   
   }
   ```

   Los parámetros de los métodos también se pueden anotar opcionalmente mediante la anotación @ServiceMethodParameter (com.adobe.exm.expeval.ServiceMethodParameter). Esta anotación solo se utiliza para especificar nombres legibles por humanos y descripciones de parámetros de método para su uso en la interfaz de usuario de creación. Asegúrese de que los parámetros y valores de retorno de los métodos de interfaz pertenecen a uno de los siguientes tipos:

   * java.lang.String
   * java.lang.Character
   * Char
   * java.lang.Boolean
   * Booleano
   * java.lang.Integer
   * Int
   * java.lang.Short
   * corto
   * java.lang.Byte
   * byte
   * java.lang.Double
   * Doble
   * java.lang.Long
   * Largo
   * java.lang.Float
   * Flotante
   * java.util.Calendar
   * java.util.Date
   * java.util.List

1. Defina la implementación de la interfaz, configúrela como un servicio OSGI y defina las siguientes propiedades de servicio:

```jsp
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "<service_id>"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
```

La entrada exm.service=true indica al administrador de expresiones que el servicio contiene funciones remotas adecuadas para su uso en expresiones. La variable &lt;service_id> debe ser un identificador de Java válido (alfanumérico,$, _ sin otros caracteres especiales). Este valor, con el prefijo REMOTE_ keyword, forma el prefijo que se utiliza dentro de las expresiones. Por ejemplo, se puede hacer referencia a una interfaz con un método anotado bar() y el ID de servicio en las propiedades del servicio dentro de expresiones mediante REMOTE_foo:bar().

```java
package mergeandfuse.com;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = true, immediate = true, label = "RemoteFunctionImpl")
@Service(value = RemoteFunction.class)
@org.apache.felix.scr.annotations.Properties({
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker", boolValue = true),
  @org.apache.felix.scr.annotations.Property(name = "connectors.jsoninvoker.alias", value = "test1"),
  @org.apache.felix.scr.annotations.Property(name = "exm.service", boolValue = true)})
public class RemoteFuntionImpl implements RemoteFunction {

 @Override
 public String toAllCaps(String name) {
  System.out.println("######Got######"+name);
  
  return name.toUpperCase();
 }
 
}
```

A continuación se muestran archivos de ejemplo para utilizar:

* **GoodFunctions.jar.zip** es el archivo jar con paquete que contiene una definición de función remota de ejemplo. Descargue el archivo GoodFunctions.jar.zip y descomprímalo para obtener el archivo jar.
* **GoodFunctions.zip** es el paquete de código fuente para definir una función remota personalizada y crear un paquete para ella.

GoodFunctions.jar.zip

[Obtener archivo](assets/goodfunctions.jar.zip)

GoodFunctions.zip

[Obtener archivo](assets/goodfunctions.zip)
