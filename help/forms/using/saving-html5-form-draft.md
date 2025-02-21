---
title: Guardar un formulario HTML5 como borrador
description: Guarde un formulario HTML5 como borrador y vuelva a rellenarlo en una fase posterior.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 95%

---

# Guardar un formulario HTML5 como borrador {#saving-an-html-form-as-a-draft}

Se puede guardar un formulario HTML5 como borrador y seguir rellenándolo en una fase posterior. El portal de formularios permite a cualquier usuario guardar y restaurar un formulario HTML5. Para habilitar la funcionalidad Guardar como borrador, agregue las siguientes configuraciones al nodo de perfil:

## Perfil personalizado para permitir la función Guardar como borrador {#custom-profile-to-allow-save-as-draft-feature}

De serie, AEM Forms proporciona un perfil **Guardar como borrador**. Puede procesar un formulario con el perfil Guardar como borrador para habilitar la funcionalidad de borrador para un formulario HTML5. Puede especificar el perfil de procesamiento del HTML para un formulario en [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Para habilitar la funcionalidad Guardar como borrador para los [perfiles personalizados](/help/forms/using/custom-profile.md) existentes, agregue las siguientes propiedades al nodo de perfil personalizado:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>Cadena</td>
   <td>true</td>
   <td><p>Habilita la función Guardar como borrador</p> <p>para este perfil.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Cadena</td>
   <td>true</td>
   <td><p>Permite cargar archivos adjuntos</p> <p>con este perfil.</p> </td>
  </tr>
 </tbody>
</table>

## Almacenar y listar borradores {#drafts-storage-and-listing}

Después de activar la función Guardar como borrador en un formulario; cuando se guarde el formulario, aparecerá en la lista [Componente Borradores y envíos](/help/forms/using/draft-submission-component.md). Puede recuperar y comenzar a rellenar el formulario guardado desde el componente Borradores y envíos.

Para habilitar la lista de formularios para el componente Borradores y envíos, agregue la siguiente propiedad al nodo de perfil:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de propiedad</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>Cadena</td>
   <td>true</td>
   <td>Para permitir que los borradores y formularios se incluyan en el<br /> Componente Borradores y envíos del portal de formularios después del envío</td>
  </tr>
 </tbody>
</table>

De forma predeterminada, AEM Forms almacena los datos de usuario asociados con el borrador y el envío de un formulario en el nodo /content/forms/fp de la instancia de publicación. Puede agregar su proveedor de almacenamiento personalizado; para obtener más información, consulte [Almacenamiento personalizado para el componente Borradores y envíos](/help/forms/using/adding-custom-storage-provider-forms.md).
