---
title: Eliminar formularios y recursos relacionados
description: Eliminar un formulario o un recurso en AEM Forms y el impacto en los recursos a los que se refiere y de referencia y en los formularios XFA.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 100%

---

# Eliminar formularios y recursos relacionados {#deleting-forms-and-related-resources}

Puede eliminar los formularios y recursos para quitar estos recursos del repositorio. La operación de eliminación funciona en todos los tipos de recursos y carpetas.

Si elimina un recurso de la instancia de autor, también se eliminará de la instancia de publicación. El servidor de AEM Forms consta de instancias de autor y de publicación. La instancia de autor se utiliza para crear y administrar recursos y recursos de formularios. La instancia de publicación contiene los recursos de formularios publicados y los recursos relacionados disponibles para los usuarios finales.

## Eliminar un formulario {#how-to-delete-a-form}

1. Inicie sesión en la interfaz de usuario de AEM Forms al acceder a `https://[hostname]:'port'/aem/forms.html.`
1. Desplácese hasta el formulario que quiera eliminar y selecciónelo. Haga clic en Eliminar ![aem6forms_delete2](assets/aem6forms_delete2.png) en la barra de herramientas y confirme la eliminación.

   >[!NOTE]
   >
   >Solo se puede eliminar un formulario a la vez. Elimine varios formularios individualmente o elimine la carpeta principal.

1. Antes de eliminar un recurso, AEM Forms comprobará si hay referencias y solicitará una confirmación explícita. Haga clic en Forzar eliminación si desea eliminar el recurso independientemente del estado de la relación.

   >[!NOTE]
   >
   >La eliminación de un recurso al que otros recursos hacen referencia podría causar problemas funcionales.

   >[!NOTE]
   >
   >Si el recurso seleccionado es una carpeta y contiene dicho recurso en su jerarquía, elimine otros recursos de forma individual o toda la carpeta.

## Impacto de eliminar un formulario XFA al que se hace referencia {#impact-of-deleting-a-referenced-xfa-form}

En AEM Forms, se puede hacer referencia a una plantilla de formulario XFA mediante un formulario adaptable u otra plantilla de formulario XFA. Además, una plantilla puede hacer referencia a un recurso u otra plantilla XFA.

No es aconsejable eliminar un formulario XFA al que se hace referencia mediante un formulario adaptable, ya que podría dañarlo. Cuando un formulario adaptable hace referencia a un formulario XFA, sus campos están enlazados. Tras la eliminación de XFA, el formulario adaptable no podrá sincronizar sus campos con los campos XFA y mostrará un mensaje de error para dichos campos. Para obtener más información sobre el impacto de la eliminación de XFA a la que se hace referencia y sobre los AF sucios, consulte [Actualizar formularios XFA a los que se hace referencia](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Para eliminar un formulario XFA de este tipo, actualice el formulario adaptable y quite los enlaces con los campos XFA.
