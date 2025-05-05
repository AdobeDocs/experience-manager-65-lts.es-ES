---
title: Reutilizar formularios adaptables
description: Puede reutilizar un formulario adaptable existente para crear formularios adaptables nuevos.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: ef564750-f107-41cb-887e-fc6d22b7d32e
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 99%

---

# Reutilizar formularios adaptables {#reusing-adaptive-forms}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/manage-metadata/reusing-adaptive-forms.html?lang=es) |
| AEM 6.5 | Este artículo |

## Introducción {#introduction}

Si desea utilizar algunas de las propiedades de un formulario adaptable existente para generar uno nuevo, puede utilizar simplemente la funcionalidad Copiar y pegar. Además, puede pegar el formulario adaptable nuevo en la ruta de carpeta deseada. Todas las propiedades de metadatos se replican y también se copian los XFA y los XSD de los formularios adaptables basados en XFA y XSD.

>[!NOTE]
>
>El estado y los detalles de la revisión no se copian. Por ejemplo, si el formulario adaptable se publica y, a continuación, lo copia, se cancelará la publicación del formulario adaptable pegado. Del mismo modo, si un recurso copiado está en revisión, el recurso pegado no estará incluido en la misma revisión.

### Copiar un formulario adaptable {#copy-an-adaptive-form}

Copie un formulario adaptable mediante cualquiera de los siguientes métodos:

1. Haga clic en el icono Copiar ![aem6forms_copy](assets/aem6forms_copy.png) en Acciones rápidas.

   >[!NOTE]
   >
   >Las acciones rápidas son los elementos de acción que se muestran sobre una miniatura al pasar el ratón por encima.

1. Seleccione el formulario adaptable. El proceso de selección es diferente para cada vista.

   Si está en la vista Tarjeta, vaya al modo de selección al hacer clic en el icono de selección ![aem6forms_check-circle](assets/aem6forms_check-circle.png) y haga clic en todos los formularios adaptables que desee copiar.

   Si está en la vista Lista, haga clic en las casillas de verificación de todos los formularios adaptables para seleccionarlos.

   >[!NOTE]
   >
   >Todos los recursos seleccionados deben ser formularios adaptables, ya que la funcionalidad Copiar y pegar solo es compatible con formularios adaptables y todos los recursos seleccionados deben encontrarse en la misma carpeta.

   Después de seleccionar los recursos, haga clic en el icono Copiar ![aem6forms_copy](assets/aem6forms_copy.png) que aparece en la barra de herramientas para copiar el formulario adaptable seleccionado.

### Pegar un formulario adaptable {#paste-an-adaptive-form}

Al hacer clic en la acción Copiar, abandonará automáticamente el modo de selección y podrá ver el icono Pegar ![aem6forms_paste](assets/aem6forms_paste.png). A continuación, vaya a la ruta de carpeta deseada y haga clic en el icono Pegar ![aem6forms_paste](assets/aem6forms_paste.png) para pegar el formulario adaptable copiado.

Si pega el formulario en la misma carpeta o existe otro archivo con el mismo nombre de nodo (con el que está almacenado en el repositorio CRX) en la carpeta de destino, se agrega un 1 al sufijo (por ejemplo, myaf se convierte en myaf1, y si ya existe myaf1 en la misma ubicación, se convierte en myaf2). Todas las demás propiedades serán las mismas que las del formulario adaptable original.

Después de hacer clic en el icono Pegar ![aem6forms_paste](assets/aem6forms_paste.png), este se volverá a ocultar. Solo puede utilizar la opción Pegar una vez simultáneamente. Para volver a crear una copia del mismo recurso, cópielo de nuevo.

### Cambiar el contenido del formulario adaptable nuevo  {#change-contents-of-new-adaptive-form}

El contenido de un formulario adaptable pegado se puede cambiar mediante los siguientes métodos para diferenciarlo del formulario copiado:

1. **Cambiar las propiedades de los metadatos:**

   Puede cambiar las propiedades de los metadatos del formulario adaptable, por ejemplo, el título y la descripción. Para obtener más información sobre las propiedades de los metadatos y cómo se pueden cambiar, consulte [Administración de metadatos de formulario](/help/forms/using/manage-form-metadata.md).

1. **Cambiar el XFA/XSD de los formularios adaptables basados en XFA/XSD:**

   Puede cambiar el XFA/XSD utilizado en los formularios adaptables. Para obtener información sobre cómo puede cambiar estos formularios adaptables, consulte [Administrar metadatos de formulario](/help/forms/using/manage-form-metadata.md).

1. **Volver a publicar el formulario:**

   El recurso pegado es diferente del copiado. Puede publicarlo como un nuevo recurso para que esté disponible para los usuarios finales. Para saber cómo publicar un recurso, consulte [Publicar y cancelar la publicación de formularios](/help/forms/using/publishing-unpublishing-forms.md)
