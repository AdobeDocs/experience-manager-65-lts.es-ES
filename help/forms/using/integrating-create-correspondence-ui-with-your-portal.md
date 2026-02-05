---
title: Integración de la solución Crear correspondencia con su portal personalizado
description: Aprenda a integrar la interfaz de usuario de Crear correspondencia con su portal personalizado
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 496b125b-b091-4843-ba9f-2479dbeba07b
source-git-commit: 16f57ae1663f035d1dc39005d37426c7a0d8dc16
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 46%

---

# Integración de la solución `Create Correspondence` con su portal personalizado{#integrating-create-correspondence-ui-with-your-custom-portal}

## Información general {#overview}

Este artículo detalla cómo puede integrar la solución `Create Correspondence` con su entorno.

## Invocación basada en URL {#url-based-invocation}

Una forma de llamar a la aplicación `Create Correspondence` desde un portal personalizado es preparar la dirección URL con los siguientes parámetros de solicitud:

* el identificador de la plantilla de carta (con el parámetro cmLetterId)

* la dirección URL de los datos XML recuperados de la fuente de datos deseada (con el parámetro cmDataUrl)

Por ejemplo, el portal personalizado prepararía la dirección URL como\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, la cual podría ser el href de un vínculo del portal.

>[!NOTE]
>
>Realizar la llamada de esta forma no es seguro, ya que los parámetros necesarios se pasan como una petición GET, exponiendo lo mismo (claramente visible) en la URL.

>[!NOTE]
>
>Antes de llamar a la aplicación `Create Correspondence`, guarde y cargue los datos para llamar a la interfaz de usuario de `Create Correspondence` en la dirección URL de datos especificada. Este proceso se puede realizar desde el propio portal personalizado o a través de otro proceso de back-end.

## Invocación basada en datos en línea {#inline-data-based-invocation}

Otra forma más segura de llamar a la aplicación `Create Correspondence` es ir a la dirección URL en https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html. Ejecute esta dirección URL al enviar los parámetros y datos para llamar a la aplicación `Create Correspondence` como una petición POST que los oculta al usuario final. Este flujo de trabajo también significa que ahora puede pasar los datos XML para la aplicación `Create Correspondence` en línea (como parte de la misma solicitud, utilizando el parámetro `cmData`). Este flujo de trabajo no era posible ni ideal en el caso del método anterior.

### Parámetros para especificar una carta {#parameters-for-specifying-letter}

| **Nombre** | **Tipo** | **Descripción** |
| --- | --- | --- |
| cmLetterInstanceId | Cadena | El identificador de la instancia de carta. |
| cmLetterId | Cadena | El nombre de la plantilla de carta. |

El orden de los parámetros de la tabla especifica la preferencia de los parámetros utilizados para cargar la carta.

### Parámetros para especificar la fuente de datos XML {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descripción</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>Datos XML de un archivo de origen mediante protocolos básicos, como cq, ftp, http o file.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Cadena</td> 
   <td>Uso de los datos xml disponibles en la instancia de carta.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Para reutilizar los datos de prueba adjuntos en un diccionario de datos.</td> 
  </tr>
 </tbody>
</table>

El orden de los parámetros de la tabla especifica la preferencia de los parámetros utilizados para cargar los datos XML.

### Otros parámetros {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nombre</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descripción</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>Booleano</td> 
   <td>True para abrir la carta en el modo de vista previa.<br /> </td> 
  </tr>
  <tr>
   <td>Aleatorio</td> 
   <td>Marca de tiempo</td> 
   <td>Para resolver los problemas de almacenamiento en caché del explorador.</td> 
  </tr>
 </tbody>
</table>

Si usa el protocolo http o cq para `cmDataURL`, la dirección URL de `http/cq` debe ser accesible de forma anónima.
