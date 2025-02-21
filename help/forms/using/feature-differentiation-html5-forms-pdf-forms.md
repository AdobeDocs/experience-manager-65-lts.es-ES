---
title: Diferenciar entre las características de formularios HTML5 y PDF
description: Obtenga información sobre las diferencias entre las características de los formularios HTML5 y PDF forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 78%

---

# Diferenciar entre las características de formularios HTML5 y PDF {#feature-differentiation-between-html-forms-and-pdf-forms}

La siguiente tabla especifica la compatibilidad de funciones proporcionada para los formularios HTML5 y PDF:

<table>
 <tbody>
  <tr>
   <th>Función</th>
   <th>Formularios HTML5</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Códigos de barras<br /> </td>
   <td>No disponible en el nivel de interfaz de usuario. </td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Campo de firma<br /> </td>
   <td>Las <strong>firmas digitales</strong> no son compatibles, pero se agrega un nuevo campo de <strong>firma manuscrita</strong> para las firmas que simulan la escritura en papel. Se puede insertar una firma manuscrita en el formulario utilizando el campo <strong>Firma manuscrita</strong>. La firma se guarda en el formulario en forma de imagen. Puede guardar la información de geolocalización en el campo <strong>Firma manuscrita</strong>.</td>
   <td>Campo de firma disponible para <strong>firmas digitales</strong>.</td>
  </tr>
  <tr>
   <td>Combinación de datos</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Imágenes</td>
   <td>El esquema de URI de datos se utiliza para mostrar imágenes. Todas las versiones modernas de los exploradores admiten este esquema, pero hay diferencias en el rango de formatos de imagen que admite cada explorador.<br /> </td>
   <td>Los formatos .gif, .png, .jpeg, .bmp y .tiff son compatibles.</td>
  </tr>
  <tr>
   <td>Paginación<br /> </td>
   <td><p>Un formulario HTML5 se divide en paneles y cuadros para que tenga un aspecto similar al de los formularios PDF. El tamaño de la página se calcula dinámicamente. Si se elimina o se marca como oculto el contenido completo de una página de un formulario HTML5, la página en blanco se oculta. No se muestra ningún espacio vacío (espacio en blanco) entre las páginas que aparecen encima y debajo de la página en blanco.</p> <p>Si la combinación de datos o los scripts agregan contenido a una página, la longitud de la página se amplía para dar cabida al contenido recién agregado. No se agregarán nuevas páginas al formulario para acomodar el contenido que acaba de agregarse. </p> <p><strong>Nota:</strong> Cuando se elimina o se marca como oculto el contenido completo de una página de un formulario HTML5, la página en blanco (espacio en blanco) permanece visible entre la primera y la segunda página, pero no entre las demás.</p> </td>
   <td>La paginación del PDF depende del contenido combinado de los datos o del contenido del usuario, y el recuento de páginas se incrementa o se reduce en función de este.</td>
  </tr>
  <tr>
   <td>Encabezados/pies de página </td>
   <td>Compatible. <br /> <br /> Como los formularios móviles HTML5 no admiten saltos de página, los encabezados y los pies de página aparecen solo una vez. Sin embargo, puede configurarlos en el diseño para que aparezcan en varios sitios de la vista previa de los formularios móviles.<br /> </td>
   <td>Compatible.</td>
  </tr>
  <tr>
   <td>Widgets personalizados</td>
   <td>Se pueden personalizar los widgets para mejorar la experiencia del usuario en dispositivos móviles.<br /> </td>
   <td>Todos los widgets están bloqueados, y no se puede conectar ningún widget personalizado.<br /> </td>
  </tr>
  <tr>
   <td>API de scripts XFA</td>
   <td>Admite las construcciones de scripts XFA más utilizadas. Para obtener una lista detallada de las construcciones compatibles, consulte <a href="/help/forms/using/scripting-support.md">compatibilidad con scripts</a>.</td>
   <td>Admite todas las construcciones de scripts XFA.</td>
  </tr>
  <tr>
   <td>API de scripts de Acrobat </td>
   <td>Los formularios HTML5 admiten las API más utilizadas. Para obtener más información, consulte <a href="/help/forms/using/scripting-support.md">Compatibilidad con scripts</a>.</td>
   <td>Si el archivo PDF se abre en Acrobat o Reader, también admite todas las API de scripts que proporciona Acrobat.</td>
  </tr>
  <tr>
   <td>Compatibilidad con idiomas de derecha a izquierda </td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
