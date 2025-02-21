---
title: Representar la plantilla de formulario para formularios HTML5
description: Los perfiles de formulario HTML5 están asociados a procesamientos de perfiles. Los procesamientos de perfiles son páginas JSP responsables de generar la representaciones HTML del formulario al llamar al servicio OSGi de Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 100%

---

# Representar la plantilla de formulario para formularios HTML5 {#rendering-form-template-for-html-forms}

## Punto final de procesamiento {#render-endpoint}

Los formularios HTML5 tienen la noción **Perfiles** que se exponen como extremos REST para permitir el procesamiento móvil de plantillas de formulario. Estos perfiles están asociados a un **Procesador de perfiles**. Son páginas JSP responsables de generar la representación HTML del formulario al llamar al servicio Forms OSGi. La ruta JCR del nodo Perfil determina la dirección URL del punto final de procesamiento. El punto final de procesamiento predeterminado del formulario que señala al perfil “predeterminado” tiene este aspecto:

Ruta https://&lt;*host*>:&lt;*port*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*de la carpeta que contiene el formulario xdp*>&amp;template=&lt;*name of the xdp*>

Por ejemplo, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`. 

Para un perfil personalizado, el punto final cambia en consecuencia. Por ejemplo, el punto final del perfil personalizado con el nombre hrforms es el siguiente:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Si la plantilla reside en el repositorio de AEM en una aplicación llamada FormSubmission, el URI es el siguiente:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Parámetros de procesamiento {#render-parameters}

Los parámetros de solicitud compatibles al procesar el formulario como HTML son los siguientes:

<table>
 <tbody>
  <tr>
   <th><strong>Parámetro </strong></th>
   <th><strong>Descripción</strong></th>
  </tr>
  <tr>
   <td>template<br /> </td>
   <td>Este parámetro especifica el nombre del archivo de plantilla.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Este parámetro especifica la ruta donde residen la plantilla y los recursos asociados. Esta ruta puede ser la ruta del sistema de archivos del servidor, una ruta del repositorio o una ruta http o ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Este parámetro especifica la dirección URL a la que se publica el xml de datos del formulario.<br /> </td>
  </tr>
 </tbody>
</table>

### Combinar datos con la plantilla de formulario {#merge-data-with-form-template}

| Parámetro | Descripción |
|---|---|
| dataRef | Este parámetro especifica la **ruta absoluta** del archivo de datos que se combina con la plantilla. Este parámetro puede ser una URL a un servicio de rest que devuelva los datos en formato xml. |
| data | Este parámetro especifica los bytes de datos codificados UTF-8 que se combinan con la plantilla. Si se especifica este parámetro, el formulario HTML5 ignorará el parámetro dataRef. |

### Pasar el parámetro de procesamiento {#passing-the-render-parameter}

Los formularios HTML5 admiten tres métodos para pasar los parámetros de procesamiento. Puede pasar parámetros a través de direcciones URL, pares clave-valor y nodo de perfil. En el parámetro de procesamiento, el par clave-valor tiene la prioridad más alta seguida del nodo de perfil. El parámetro de solicitud de URL tiene la menor prioridad.

* **Parámetros de solicitud de URL**: puede especificar los parámetros de procesamiento en la URL. En los parámetros de solicitud de URL, los parámetros son visibles para el usuario final. Por ejemplo, la siguiente URL de envío contiene un parámetro de plantilla: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parámetros de solicitud de SetAttribute**: puede especificar los parámetros de procesamiento como un par clave-valor. En los parámetros de solicitud de SetAttribute, el usuario final no puede ver los parámetros. Puede reenviar una solicitud desde cualquier otro JSP al JSP del procesador de perfiles de formulario HTML5 y usar *setAttribute* en el objeto de solicitud para pasar todos los parámetros de procesamiento. Este método tiene la prioridad más alta.

* **Parámetros de solicitud del nodo de perfil:** puede especificar los parámetros de procesamiento como propiedades del nodo de un nodo de perfil. En los parámetros de solicitud del nodo de perfil, el usuario final no puede ver los parámetros. El nodo de perfil es el nodo al que se envía la solicitud. Para especificar parámetros como propiedades de nodo, utilice CRXDE lite.

### Parámetros de envío {#submit-parameters}

Los formularios HTML5 envían datos, ejecutan scripts del lado del servidor y servicios web en servidores de AEM. Para obtener información detallada sobre los parámetros utilizados para ejecutar scripts del lado del servidor y servicios web en servidores de AEM, consulte [Servicios Proxy de formularios HTML5](/help/forms/using/service-proxy.md).
