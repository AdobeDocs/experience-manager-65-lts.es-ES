---
title: Configurar la autenticación basada en certificados
description: Importe un certificado de entidad emisora de certificados (CA) en el almacén de confianza y cree una asignación de certificado para la autenticación basada en certificados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 56603735-959e-4460-b642-bba63fa20c02
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# Configurar la autenticación basada en certificados {#configuring-certificate-based-authentication}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Administración de usuarios suele realizar la autenticación con un nombre de usuario y una contraseña. Administración de usuarios también admite la autenticación basada en certificados, que puede utilizar para autenticar a los usuarios mediante Acrobat o para autenticar a los usuarios mediante programación. Para obtener más información sobre cómo autenticar usuarios mediante programación, vea [Programar con formularios AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).

Para utilizar la autenticación basada en certificados, importe un certificado de entidad emisora de certificados (CA) de confianza en el almacén de confianza y, a continuación, cree una asignación de certificado.

## Importar el certificado de CA {#import-the-ca-certificate}

Al importar el certificado, seleccione las opciones Confiar en la autenticación de certificados y Confiar en la identidad, así como cualquier otra opción que necesite. Para obtener detalles acerca de la importación de certificados, vea [Administrar certificados](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configurar la asignación de certificados {#configuring-certificate-mapping}

Para habilitar la autenticación basada en certificados para los usuarios, cree una asignación de certificado. Una *asignación de certificados* define una asignación entre los atributos de un certificado y los atributos de los usuarios de un dominio. Puede asignar más de un certificado al mismo dominio.

Al probar un certificado, Administración de usuarios carga las comprobaciones de certificados para asegurarse de que cumple los siguientes requisitos:

* El certificado es válido.
* El emisor especificado puede comprobar el certificado.
* El certificado contiene el atributo necesario para la asignación.
* La asignación especificada asigna el certificado solo a un usuario de la base de datos de formularios de AEM. Se comprueban los usuarios actuales y obsoletos (eliminados) para determinar si coinciden con los criterios de asignación. Por lo tanto, la prueba de certificado falla si más de un usuario, incluidos los usuarios obsoletos, tiene el valor de atributo en consideración.

>[!NOTE]
>
>No se puede editar una asignación de certificado existente.

**Agregar una asignación de certificado**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Asignación de certificados.
1. Haga clic en Nueva asignación de certificado y, en la lista Para emisor, seleccione el alias de certificado según se ha configurado en Administración de almacén de confianza.
1. Asigne uno de los atributos del certificado al atributo de un usuario. Por ejemplo, puede asignar el nombre común del certificado al ID de inicio de sesión del usuario.

   Si el contenido del atributo en el certificado es diferente del contenido en el atributo del usuario en la base de datos de User Management, puede utilizar una expresión regular de Java (regex) para hacer coincidir los dos atributos. Por ejemplo, si los nombres comunes de los certificados son *Alex Pink (Authentication)* y *Alex Pink (Signing)* y el nombre común de la base de datos de User Management es *Alex Pink*, use una expresión regular para extraer la parte necesaria del atributo del certificado (en este ejemplo, *Alex Pink*). La expresión regular que especifique debe ajustarse a la especificación de Java regex.

   Puede transformar la expresión especificando el orden de los grupos en el cuadro Orden personalizado. El orden personalizado se usa con el método `java.util.regex.Matcher.replaceAll()`. El comportamiento que se ve se corresponderá con el comportamiento de ese método y la cadena de entrada (el orden personalizado) debe especificarse en consecuencia.

   Para probar la regex, introduzca un valor en el cuadro Parámetro de prueba y haga clic en Probar.

   Puede utilizar los siguientes caracteres en la regex:

   * . (cualquier carácter)
   * &amp;ast; (0 o más ocurrencias)
   * () (especifique el grupo entre corchetes)
   * \ (se utiliza para convertir un carácter regex en un carácter normal)
   * $n (se usa para hacer referencia al grupo nth)

   Ejemplos de expresiones regulares:

   * Para extraer &quot;Alex Pink&quot; de &quot;Alex Pink (Authentication)&quot;

     **Regex:** (.&amp;ast;) \(Authentication\)

   * Para extraer &quot;Alex Pink&quot; de &quot;Alex (Authentication) Pink&quot;

     **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

   * Para extraer &quot;Pink Alex&quot; de &quot;Alex (Authentication) Pink&quot;

     **Regex:** (.&amp;ast;)\(Authentication\) (.&amp;ast;)

     Pedido personalizado: $2 $1 (devuelve el segundo grupo, concatenado al primer grupo, capturado por el carácter de espacio en blanco)

   * Para extraer &quot;apink@sampleorg.com&quot; de &quot;smtp:apink@sampleorg.com&quot;

     **Regex:** smtp:(.&amp;ast;)

   Para obtener más información sobre el uso de expresiones regulares, consulte [Tutorial de Java sobre expresiones regulares](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. En la lista Para dominio, seleccione el dominio del usuario.
1. Para probar esta configuración, haga clic en Examinar para cargar un certificado de usuario de ejemplo, haga clic en Probar certificado y, si la configuración es correcta, haga clic en Aceptar.

**Editar una asignación de certificado existente**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración.
1. Haga clic en Asignación de certificados.
1. Seleccione la asignación de certificados para editar y editar su configuración. Puede actualizar la expresión regular y el orden personalizado.
1. Para probar los cambios, haga clic en Examinar para cargar un certificado de ejemplo, haga clic en Certificado de prueba y, a continuación, haga clic en Aceptar.

**Eliminar una asignación de certificado**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Asignación de certificados.
1. Active la casilla de verificación de la asignación de certificado que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.
