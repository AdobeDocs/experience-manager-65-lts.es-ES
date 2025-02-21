---
title: Sugerencias de codificación
description: Conozca algunas sugerencias para codificar las prácticas recomendadas en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---

# Sugerencias de codificación{#coding-tips}

## Utilice etiquetas o HTL tanto como sea posible {#use-taglibs-or-htl-as-much-as-possible}

La inclusión de scripts en JSP dificulta la depuración de problemas en el código. Además, al incluir scripts en JSP, es difícil separar la lógica empresarial de la capa de vista, lo que supone una violación del principio de responsabilidad única y del patrón de diseño de MVC.

### Escribir código legible {#write-readable-code}

El código se escribe una vez, pero se lee muchas veces. Dedicar un poco de tiempo para limpiar el código que está escrito paga dividendos en el futuro a medida que usted y otros desarrolladores lo leen más tarde.

### Elija nombres que revelen la intención {#choose-intention-revealing-names}

Lo ideal es que otro programador no tenga que abrir un módulo para comprender lo que hace. Del mismo modo, deberían poder saber qué hace un método sin leerlo. Cuanto mejor pueda suscribirse a estas ideas, más fácil será leer el código y más rápido podrá escribirlo y cambiarlo.

En la base de código de AEM, se utilizan las siguientes convenciones:


* Una sola implementación de una interfaz se denomina `<Interface>Impl`, es decir, `ReaderImpl`.
* Varias implementaciones de una interfaz se denominan `<Variant><Interface>`, es decir, `JcrReader` y `FileSystemReader`.
* Las clases base abstractas se denominan `Abstract<Interface>` o `Abstract<Variant><Interface>`.
* Los paquetes se denominan `com.adobe.product.module`. Cada artefacto de Maven o paquete OSGi debe tener su propio paquete.
* Las implementaciones de Java™ se colocan en un paquete impl debajo de su API.


Estas convenciones no se aplican necesariamente a las implementaciones de los clientes, pero es importante que se definan y se cumplan las convenciones para que el código pueda mantenerse.

Idealmente, los nombres deberían revelar su intención. Una prueba de código común para los casos en los que los nombres no son tan claros como deberían ser es la presencia de comentarios que expliquen para qué sirve la variable o el método:

<table>
 <tbody>
  <tr>
   <td><p><strong>Poco Claro</strong></p> </td>
   <td><p><strong>Borrar</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //tiempo transcurrido en días</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### No repita usted mismo  {#don-t-repeat-yourself}

DRY afirma que el mismo conjunto de código nunca debe duplicarse. Esto también se aplica a elementos como literales de cadena. La duplicación de código abre la puerta a defectos cada vez que algo tiene que cambiar y debe buscarse y eliminarse.

### Evitar reglas CSS desnudas {#avoid-naked-css-rules}

Las reglas CSS deben ser específicas del elemento de destino en el contexto de la aplicación. Por ejemplo, una regla CSS aplicada a *.content .center* sería demasiado amplia y podría terminar afectando mucho contenido en el sistema, lo que requeriría que otros invalidaran este estilo en el futuro. Por su parte, *.myapp-centertext* sería una regla más específica ya que especifica *texto* centrado en el contexto de su aplicación.

### Eliminar el uso de API obsoletas {#eliminate-usage-of-deprecated-apis}

Cuando una API está en desuso, siempre es mejor encontrar el nuevo método recomendado en lugar de depender de la API en desuso. Esto garantizará actualizaciones más fluidas en el futuro.

### Escribir código localizable {#write-localizable-code}

Las cadenas que no proporcione un autor deben incluirse en una llamada al diccionario i18n de AEM a través de *I18n.get()* en JSP/Java y *CQ.I18n.get()* en JavaScript. Esta implementación devolverá la cadena que se le pasó si no se encuentra ninguna implementación, por lo que ofrece la flexibilidad de implementar la localización después de implementar las funciones en el idioma principal.

### Escape de rutas de recursos por seguridad {#escape-resource-paths-for-safety}

Aunque las rutas en el JCR no deben contener espacios, la presencia de ellos no debe provocar que el código se rompa. Jackrabbit proporciona una clase de utilidad Text con los métodos *escape()* y *escapePath()*. Para los JSP, la interfaz de usuario de Granite expone una función *granite:encodeURIPath() EL*.

### Utilice la API XSS o HTL para protegerse contra ataques de scripts entre sitios {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM proporciona una API XSS para limpiar fácilmente parámetros y garantizar la seguridad frente a ataques de scripts entre sitios. Además, HTL tiene estas protecciones integradas directamente en el lenguaje de creación de plantillas. Hay disponible una hoja de trucos de API para descargar en [Desarrollo - Directrices y prácticas recomendadas](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implementar el registro adecuado {#implement-appropriate-logging}

Para el código Java™, AEM admite slf4j como API estándar para registrar mensajes y debe utilizarse con las configuraciones disponibles a través de la consola OSGi para mantener la coherencia en la administración. Slf4j expone cinco niveles de registro diferentes. Adobe recomienda utilizar las siguientes directrices al elegir el nivel en el que registrar un mensaje:

* ERROR: cuando algo se ha roto en el código y el procesamiento no puede continuar. Esto suele ocurrir como resultado de una excepción inesperada. Es útil incluir los seguimientos de pila en estos escenarios.
* ADVERTENCIA: Cuando algo no ha funcionado correctamente, pero el procesamiento puede continuar. A menudo, esto será el resultado de una excepción que esperábamos, como una *PathNotFoundException*.
* INFORMACIÓN: Información que sería útil al monitorizar un sistema. Tenga en cuenta que este es el valor predeterminado y que la mayoría de los clientes lo dejarán en su lugar en sus entornos. Por lo tanto, no lo utilice en exceso.
* DEPURACIÓN: información de nivel inferior sobre el procesamiento. Resulta útil al depurar un problema compatible con.
* TRACE: la información de nivel inferior, como métodos de entrada y salida. Normalmente, solo lo utilizan los desarrolladores.

Si hay JavaScript, *console.log* solo se debe usar durante el desarrollo y todas las instrucciones de registro se deben eliminar antes del lanzamiento.

### Evitar programación de culto de carga {#avoid-cargo-cult-programming}

Evite copiar código sin comprender lo que hace. En caso de duda, siempre es mejor preguntar a alguien que tenga más experiencia con el módulo o la API que no tenga claro.
