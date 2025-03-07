---
title: ¿Cómo se generan y trabajan con hashes en Dynamic PDF forms?
description: Generación y uso de hash en PDF forms dinámico.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 3fa1b6c9-fe73-4d76-aa72-20ce3e502941
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---

# Generar y trabajar con hash en formularios PDF dinámicos {#generate-work-with-hashes-dynamic-pdf-forms}

## Conocimientos previos requeridos {#prerequisite-knowledge}

Se requiere cierta experiencia con AEM Forms en JEE Designer, así como la capacidad de acceder y llamar a funciones en objetos de script.

## Nivel de usuario {#user-level}

Inicio

Cuando desea ocultar una contraseña en el formulario de PDF y no desea que esté en texto no cifrado dentro del código fuente o en cualquier otro lugar del documento de PDF, es fundamental saber cómo generar y trabajar con los hash MD4, MD5, SHA-1 y SHA-256.

La idea es ofuscar la contraseña generando un hash único y almacenarlo en el documento de PDF. Este hash único se puede generar mediante diferentes funciones hash y, en este artículo, se muestra cómo generarlas dentro del formulario de PDF y cómo trabajar con ellas.

Una función hash toma una cadena larga (o mensaje) de cualquier longitud como entrada y produce una cadena de longitud fija como salida, a veces denominada compendio de mensajes o huella digital.

AEM Forms en JEE Designer permite implementar las diferentes funciones hash en objetos de script como JavaScript y ejecutarlos dentro de un documento PDF dinámico. Los PDF de ejemplo que se incluyen con los archivos de ejemplo para este artículo utilizan implementaciones de código abierto de las siguientes funciones hash:

* MD4 y MD5: diseñados por Ronald Rivest

* SHA-1 y SHA-256 - tal como los define el NIST

La mayor ventaja de utilizar hashes es que no tiene que comparar contraseñas directamente comparando cadenas de texto no cifrado; en su lugar, puede comparar los dos hashes de las dos contraseñas. Dado que es poco probable que dos cadenas diferentes tengan el mismo hash, si ambos hashes son idénticos, puede suponer que las cadenas comparadas (en este caso, las contraseñas) también son idénticas.

>[!NOTE]
>
>Hay algunos problemas de seguridad conocidos (los llamados conflictos de hash) con MD4 o MD5. Debido a esos choques de hash y otros hacks SHA-1 (incluyendo las tablas del arco iris), decidí concentrarme en la función de hash SHA-256 en la segunda muestra. Para obtener más información, consulte las páginas de Wikipedia [Conflicto](https://en.wikipedia.org/wiki/Hash_collision) y [Tabla del arco iris](https://en.wikipedia.org/wiki/Rainbow_table).

## Examen de los objetos de script {#examining-script-objects}

Cuando abra uno de los dos ejemplos proporcionados en AEM Forms en JEE Designer, encontrará los cuatro objetos de script en la paleta Jerarquía (consulte la figura siguiente).

![Variables](assets/variables.jpg)

Para ver la implementación de JavaScript de las funciones hash dentro de estos objetos de script, seleccione el objeto de script y explore el código en el Editor de scripts. Puede ver cómo se ha implementado cada una de las siguientes funciones hash:

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1( )
* soHASHING_SHA1.str_sha1( )
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

Como puede ver en esta lista, hay diferentes funciones disponibles para los diferentes tipos de salida del hash. Puede elegir entre `hex_` para dígitos hexadecimales, `b64_` para salida codificada en Base64 o `str_` para codificación de cadena simple.

Según la función hash que elija, la longitud del hash variará:

* MD4: 128 bits
* MD5: 128 bits
* SHA-1: 160 bits
* SHA-256: 256 bits

## Prueba de PDF forms de muestra {#try-sample-pdf-forms}

Los archivos de ejemplo para este artículo incluyen dos PDF forms. El primer ejemplo permite escribir una cadena y, a continuación, generar valores hash MD4, MD5, SHA-1 y SHA-256 para la cadena. El segundo ejemplo es un formulario sencillo que desbloquea los campos de texto si se introduce una contraseña correcta.

### Ejemplo 1: generación de hashes {#generating-dashes}

Siga los pasos a continuación para probar el primer ejemplo:

1. Después de descargar y descomprimir los archivos de ejemplo, abra hashing_forms_sample1.pdf con AEM Forms en JEE Designer. También puede utilizar Adobe Reader o Adobe Acrobat Professional para abrir y ver el ejemplo, pero no puede ver el código fuente.
1. En el campo de texto etiquetado [!UICONTROL borrar texto], escriba una contraseña o cualquier otro mensaje que desee que tenga un cifrado hash.
1. Haga clic en uno de los cuatro botones para generar el hash MD4, MD5, SHA-1 o SHA-256. Según el botón que haya presionado, se llamará a una de las cuatro funciones hash que produce salida hexadecimal y la cadena o el mensaje tendrán un valor hash.

El resultado de la operación hash se muestra en el campo denominado [!UICONTROL hash]. La longitud del hash varía según la función hash que elija.

Todos los ejemplos utilizan dígitos hexadecimales como tipo de salida. Puede utilizar el Editor de secuencias de comandos para modificar los ejemplos y cambiar el tipo de salida a Base64 o String simple.

### Ejemplo 2: contraseñas coincidentes {#matching-passwords}

El segundo ejemplo muestra cómo se comparan los hash en segundo plano, sin tener que revelar la contraseña real. La contraseña introducida tiene un cifrado hash. La contraseña real, que se almacena en un campo invisible, también tiene un cifrado hash. La contraseña es segura no porque sea invisible, sino porque tiene un cifrado hash. Como es imposible reconstruir la contraseña a partir del valor con hash, es seguro exponer la contraseña en forma con hash. La comparación se realiza únicamente entre los hashes, no entre las contraseñas en texto no cifrado. Si ambos hashes son iguales, entonces puede suponer que las contraseñas son idénticas.

Siga los pasos a continuación para probar el segundo ejemplo:

1. Abra `hashing_forms_sample2.pdf` con AEM Forms en JEE Designer. También puede utilizar Adobe Reader o Adobe Acrobat Professional para abrir y ver el ejemplo, pero no puede ver el código fuente.
1. Elija uno de los dos campos de contraseña etiquetados como [!UICONTROL Password MAN] o [!UICONTROL Password WOMAN] y escriba las contraseñas:
   1. La contraseña del hombre es `bob`
   1. La contraseña de la mujer es `alice`
1. Al desplazar el enfoque fuera de los campos de contraseña o pulsar la tecla Intro, el hash de la contraseña introducida se genera automáticamente y se compara con el hash almacenado de la contraseña correcta en segundo plano. Las contraseñas correctas con hash se almacenan en los campos de texto invisible con las etiquetas `passwd_man_hashed` y `passwd_woman_hashed`. Si escribe la contraseña correcta para el comando man, los campos de texto etiquetados como `Man 1` y `Man 2` estarán accesibles para que pueda escribir texto en ellos. El mismo comportamiento se aplica a los campos de la mujer.
1. De forma opcional, puede hacer clic en el botón con la etiqueta &quot;eliminar contraseñas&quot;, lo que desactiva los campos de texto y cambia su borde.

El código para comparar los dos valores con hash y habilitar los campos de texto es sencillo:

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## A dónde ir desde aquí {#next-steps}

¿Dónde necesitarías algo como esto? Considere un formulario de PDF con campos que solo deben rellenar las personas autorizadas. Al proteger esos campos con una contraseña, que no se puede ver en texto no cifrado en ninguna parte del documento como en Sample_2.pdf, puede asegurarse de que esos campos solo son accesibles para los usuarios que conocen la contraseña.

Le animo a que siga explorando los dos archivos de muestra de PDF.  Puede generar nuevos valores hash con Sample_1.pdf y utilizar los valores generados para cambiar la contraseña o la función hash utilizada en Sample_2.pdf.  Los recursos enumerados en la sección Atribuciones también proporcionan información adicional sobre la función hash y las implementaciones específicas de JavaScript utilizadas en este artículo.

## Atribuciones {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [Conflicto de hash](https://en.wikipedia.org/wiki/Hash_collision)
* [Mesa arco iris](https://en.wikipedia.org/wiki/Rainbow_table)
* [Página de inicio del proyecto JavaScript MD5](https://pajhome.org.uk/crypt/md5/)
* [página principal del proyecto jsSHA2](https://anmar.eu.org/projects/jssha2/)
