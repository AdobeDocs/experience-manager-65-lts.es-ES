---
title: 'Modelado de datos: el modelo de David Nuescheler'
description: Recomendaciones de modelado de contenido de David Nuescheler
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 0%

---

# Modelado de datos: el modelo de David Nuescheler{#data-modeling-david-nuescheler-s-model}

## Origen {#source}

Los siguientes detalles son ideas y comentarios expresados por David Nuescheler.

David fue cofundador y director de tecnología de Day Software AG, un proveedor líder de software de infraestructura de contenido y administración de contenido global, que fue adquirido por Adobe en 2010. David trabaja como becario y vicepresidente de tecnología empresarial en Adobe y también dirige el desarrollo de JSR-170, la interfaz de programación de aplicaciones (API) del repositorio de contenido Java™ (JCR), el estándar tecnológico para la administración de contenido.

También se pueden ver más actualizaciones en [https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel](https://cwiki.apache.org/confluence/display/jackrabbit/DavidsModel).

## Introducción de David {#introduction-from-david}

En varias discusiones, descubrí que los desarrolladores están un poco incómodos con las características y funcionalidades presentadas por JCR al modelar contenido. Todavía no hay ninguna guía y poca experiencia sobre cómo modelar contenido en un repositorio y por qué un modelo de contenido es mejor que otro.

Mientras que en el mundo relacional, la industria del software tiene experiencia en cómo modelar datos, aún se encuentra en las primeras etapas para el espacio del repositorio de contenido.

Me gustaría empezar a llenar este vacío expresando mis opiniones sobre cómo se debe modelar el contenido. Mi esperanza es que esto algún día pueda convertirse en algo más significativo para la comunidad de desarrolladores, que no sea solo &quot;mi opinión&quot; sino algo que sea más aplicable en general. Así que consideremos esto como mi primera puñalada que evoluciona rápidamente.

>[!NOTE]
>
>Descargo de responsabilidad: estas directrices expresan mis puntos de vista personales, a veces controvertidos. Espero con interés debatir estas directrices y perfeccionarlas.

## Siete reglas sencillas {#seven-simple-rules}

### #1 de regla: primero los datos y después la estructura. Tal vez. {#rule-data-first-structure-later-maybe}

#### Explicación {#explanation-1}

Recomiendo no preocuparse por una estructura de datos declarada en un sentido rojo. Inicialmente.

Aprende a amar a nt:unstructured (&amp; amigos) en el desarrollo.

Mi conclusión: La estructura es costosa y a menudo es totalmente innecesario declarar explícitamente la estructura al almacenamiento subyacente.

Existe un contrato implícito sobre la estructura que la aplicación utiliza de forma inherente. Supongamos que almacenamos la fecha de modificación de una publicación de blog en una propiedad lastModified. Mi aplicación sabe automáticamente que debe volver a leer la fecha de modificación de esa misma propiedad, por lo que no es necesario declararla explícitamente.

Solo deben aplicarse otras restricciones de datos, como obligatorias o restricciones de tipo y valor, cuando sea necesario por motivos de integridad de los datos.

#### Ejemplos {#example-1}

El ejemplo anterior de usar una propiedad Fecha `lastModified` en, por ejemplo, el nodo &quot;publicación de blog&quot;, no significa que sea necesario un tipo de nodo especial. Definitivamente usaría `nt:unstructured` para los nodos de mis publicaciones de blog al menos inicialmente. Ya que en mi aplicación de blogs, todo lo que voy a hacer es mostrar la fecha de lastModified de todos modos (posiblemente &quot;ordenar por&quot;) apenas me importa si es una fecha en absoluto. Como confío implícitamente en la aplicación de escritura de blogs para poner una &quot;fecha&quot; de todas formas, no es necesario declarar la presencia de una fecha `lastModified` en forma de nodo.

### #2 de reglas: Controle la jerarquía de contenido; no permita que esto ocurra. {#rule-drive-the-content-hierarchy-don-t-let-it-happen}

#### Explicación {#explanation-2}

La jerarquía de contenido es un recurso valioso. No dejes que suceda; diseña. Si no tiene un nombre &quot;bueno&quot; y legible en lenguaje natural para un nodo, probablemente sea algo que debería reconsiderar. Los números arbitrarios difícilmente son un &quot;buen nombre&quot;.

Si bien puede ser fácil poner rápidamente un modelo relacional existente en un modelo jerárquico, uno debe poner algo de pensamiento en ese proceso.

En mi experiencia, si se piensa en el control de acceso y la contención como buenos controladores para la jerarquía de contenido. Piense en ello como si fuera su sistema de archivos. Puede incluso utilizar archivos y carpetas para modelarlo en el disco local.

Personalmente, prefiero las convenciones de jerarquía sobre el sistema de escritura de nodos inicialmente, e introduzco la escritura más tarde.

>[!CAUTION]
>
>La forma en que se estructura un repositorio de contenido también puede afectar al rendimiento. Para obtener el mejor rendimiento, el número de nodos secundarios adjuntos a nodos individuales en un repositorio de contenido no debe superar 1000.
>
>Vea [¿Cuántos datos puede manejar CRX?](https://helpx.adobe.com/experience-manager/kb/CrxLimitation.html)

#### Ejemplos {#example-2}

Yo modelaría un sistema simple de blogueo de la siguiente manera. Inicialmente, ni siquiera me importan los tipos de nodos respectivos que utilizo en este punto.

```xml
/content/myblog
/content/myblog/posts
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping

/content/myblog/comments/iphone_shipping/i_like_it_too
/content/myblog/comments/iphone_shipping/i_like_it_too/i_hate_it
```

Creo que una de las cosas que se hace evidente es que la estructura del contenido se entiende a partir del ejemplo sin más explicaciones.

Lo que puede ser inesperado inicialmente es por qué no almacenaría los &quot;comentarios&quot; con el &quot;post&quot;, que se debe al control de acceso que me gustaría que se aplicara de una manera razonablemente jerárquica.

Con el modelo de contenido anterior, puedo permitir fácilmente que el usuario &quot;anónimo&quot; &quot;cree&quot; comentarios, pero mantener al usuario anónimo en modo de solo lectura para el resto del espacio de trabajo.

### #3 de reglas: Los espacios de trabajo son para clone(), merge() y update(). {#rule-workspaces-are-for-clone-merge-and-update}

#### Explicación {#explanation-3}

Si no usa los métodos `clone()`, `merge()` o `update()` en su aplicación, es probable que un solo espacio de trabajo sea el camino a seguir.

&quot;Nodos correspondientes&quot; es un concepto definido en la especificación JCR. Básicamente, se reduce a nodos que representan el mismo contenido, en diferentes espacios de trabajo.

JCR introduce el concepto abstracto de espacios de trabajo, lo que deja a muchos desarrolladores sin saber qué hacer con ellos. Me gustaría proponer poner su uso de espacios de trabajo a lo siguiente para probar.

Si tiene una superposición considerable de nodos &quot;correspondientes&quot; (esencialmente los nodos con el mismo UUID) en varios espacios de trabajo, probablemente haga un buen uso de los espacios de trabajo.

Si no hay superposición de nodos con el mismo UUID, probablemente esté abusando de los espacios de trabajo.

No utilice espacios de trabajo para el control de acceso. La visibilidad del contenido para un grupo particular de usuarios no es un buen argumento para separar cosas en diferentes espacios de trabajo. JCR incluye &quot;Control de acceso&quot; en el repositorio de contenido para proporcionarlo.

Los espacios de trabajo son los límites de las referencias y consultas.

#### Ejemplos {#example-3}

Utilice espacios de trabajo para cosas como:

* v1.2 del proyecto frente a a v1.3 del proyecto
* un estado de &quot;desarrollo&quot;, &quot;control de calidad&quot; y &quot;publicado&quot; de contenido

No utilice espacios de trabajo para tareas como las siguientes:

* directorios principales del usuario
* contenido distinto para distintas audiencias de destino como público, privado, local, ...
* bandejas de entrada de correo para distintos usuarios

### Regla #4: Tenga cuidado con los hermanos del mismo nombre. {#rule-beware-of-same-name-siblings}

#### Explicación {#explanation-4}

Same Name Siblings (SNS) se ha introducido en la especificación para permitir la compatibilidad con estructuras de datos diseñadas para y expresadas a través de XML y, por lo tanto, son valiosas para JCR. Sin embargo, SNS incluye sobrecarga y complejidad para el repositorio.

Cualquier ruta al repositorio de contenido que contenga un SNS en uno de sus segmentos de ruta se vuelve mucho menos estable. Si se quita o se reordena un SNS, esto afecta a las rutas de todos los demás SNS y sus elementos secundarios.

Para importar XML o interactuar con XML existente, SNS puede ser necesario y útil, pero nunca he utilizado SNS (ni tengo intención de hacerlo) en mis modelos de datos de &quot;campo verde&quot;.

#### Ejemplos {#example-4}

Uso

```xml
/content/myblog/posts/what_i_learned_today
/content/myblog/posts/iphone_shipping
```

En lugar de

```xml
/content/blog[1]/post[1]
/content/blog[1]/post[2]
```

### Regla #5: Las referencias se consideran perjudiciales. {#rule-references-considered-harmful}

#### Explicación {#explanation-5}

Las referencias implican integridad referencial. Es importante comprender que las referencias no solo agregan un coste adicional para el repositorio que administra la integridad referencial, sino que también son costosas desde la perspectiva de la flexibilidad del contenido.

Personalmente, solo utilizo referencias cuando realmente no puedo lidiar con una referencia colgada y, de lo contrario, utilizo una ruta, un nombre o un UUID de cadena para hacer referencia a otro nodo.

#### Ejemplos {#example-5}

Supongamos que permito &quot;referencias&quot; de un documento a) a otro documento b). Si modelo esta relación con propiedades de referencia, significa que los dos documentos están vinculados en un nivel de repositorio. No puedo exportar/importar el documento (a) individualmente, ya que es posible que el destino de la propiedad de referencia no exista. Otras operaciones como combinar, actualizar, restaurar o clonar también se ven afectadas.

Por lo tanto, modelaría esas referencias como &quot;referencias débiles&quot; (en JCR v1.0, esto esencialmente se reduce a propiedades de cadena que contienen el uuid del nodo de destino) o simplemente utilizaría una ruta. A veces, la ruta es más significativa para empezar.

Creo que hay casos prácticos en los que un sistema no puede funcionar si una referencia está colgando, pero no puedo encontrar un buen ejemplo &quot;real&quot; pero simple de mi experiencia directa.

### Regla #6: Los archivos son archivos. {#rule-files-are-files}

#### Explicación {#explanation-6}

Si un modelo de contenido expone algo que incluso huele remotamente a archivo o carpeta, intento usar (o ampliar desde) `nt:file`, `nt:folder` y `nt:resource`.

En mi experiencia, muchas aplicaciones genéricas permiten la interacción con nt:folder y nt:files implícitamente y saben cómo manejar y mostrar esos eventos si están enriquecidos con metainformación adicional. Por ejemplo, una interacción directa con implementaciones de servidor de archivos como CIFS o WebDAV ubicadas encima de JCR se vuelve implícita.

Creo que, como buena regla general, se podría utilizar lo siguiente: Si debe almacenar el nombre de archivo y el tipo MIME, `nt:file`/ `nt:resource` es una buena coincidencia. Si puede tener varios &quot;archivos&quot;, nt:folder es un buen lugar para almacenarlos.

Si debe agregar información meta para su recurso, por ejemplo una propiedad &quot;author&quot; o &quot;description&quot;, extienda `nt:resource` no `nt:file`. Rara vez extiendo nt:file y con frecuencia extiendo `nt:resource`.

#### Ejemplos {#example-6}

Supongamos que alguien desea cargar una imagen en una entrada de blog en:

```xml
/content/myblog/posts/iphone_shipping
```

Y tal vez la reacción intestinal inicial sería agregar una propiedad binaria que contenga la imagen.

Aunque hay buenos casos de uso para solo usar una propiedad binaria (digamos que el nombre es irrelevante y el tipo MIME está implícito), en este caso, recomiendo la siguiente estructura para mi ejemplo de blog.

```xml
/content/myblog/posts/iphone_shipping/attachments [nt:folder]
/content/myblog/posts/iphone_shipping/attachments/front.jpg [nt:file]
/content/myblog/posts/iphone_shipping/attachments/front.jpg/jcr:content [nt:resource]
```

### Regla #7: Los identificadores son malvados. {#rule-ids-are-evil}

#### Explicación {#explanation-7}

En las bases de datos relacionales, los ID son un medio necesario para expresar relaciones, por lo que las personas también tienden a utilizarlos en los modelos de contenido. Principalmente por las razones equivocadas a través de.

Si el modelo de contenido está lleno de propiedades que terminan en &quot;Id&quot;, es probable que no esté utilizando la jerarquía correctamente.

Es cierto que algunos nodos necesitan una identificación estable a lo largo de su ciclo de vida; menos de lo que podría pensar. Sin embargo, `mix:referenceable` tiene un mecanismo de este tipo integrado en el repositorio, por lo que no es necesario idear un medio adicional para identificar un nodo de forma estable.

Tenga en cuenta también que los elementos se pueden identificar por ruta. Y, a pesar de que los &quot;enlaces simbólicos&quot; tienen mucho más sentido para la mayoría de los usuarios que los enlaces duros en un sistema de archivos UNIX®, una ruta tiene sentido para la mayoría de las aplicaciones para referirse a un nodo de destino.

Y lo que es más importante, es **mix**:referenciable, lo que significa que se puede aplicar a un nodo en el momento en el que realmente debe hacer referencia a él.

Por lo tanto, el hecho de que desee poder hacer referencia potencialmente a un nodo de tipo &quot;Documento&quot; no significa que el tipo de nodo &quot;Documento&quot; tenga que extenderse desde `mix:referenceable` de forma estática. Esto se debe a que se puede agregar dinámicamente a cualquier instancia del documento.

#### Ejemplos {#example-7}

Utilice:

```xml
/content/myblog/posts/iphone_shipping/attachments/front.jpg
```

En lugar de:

```xml
[Blog]
-- blogId
-- author
[Post]
-- postId
-- blogId
-- title
-- text
-- date
[Attachment]
-- attachmentId
-- postId
-- filename
+ resource (nt:resource)
```
