---
title: Componente Borradores y envíos
description: El componente Borradores y envíos enumera los formularios que están en estado de borrador y los que ya se han enviado. Puede personalizar el aspecto y el estilo del componente.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 91%

---

# Componente Borradores y envíos{#drafts-and-submissions-component}

El componente Borradores y envíos enumera todos los formularios que están en estado de borrador y los que ya se han enviado. El componente tiene secciones independientes (pestañas) para formularios en borrador y enviados. Los usuarios solo pueden ver los formularios en borrador y los enviados.

## Configurar el componente {#configuring-the-component}

El componente Borradores y envíos tiene dos pestañas: Borradores y Envíos.

Para permitir que el envío de un formulario adaptable aparezca en la pestaña Envíos, establezca la **acción Enviar** como **[Acción de envío del portal de formularios](../../forms/using/configuring-submit-actions.md). Alternativamente,** habilite la opción Envío del portal de formularios. Cada vez que un usuario envíe el formulario, este se agregará a la pestaña envíos.

La funcionalidad de borradores está habilitada de forma predeterminada. Cuando un usuario haga clic en **Guardar** en un formulario adaptable, este se agregará a la pestaña Borradores.

Siga estos pasos para agregar y configurar el componente Borradores y envíos:

1. Arrastre y suelte el componente **Borradores y envíos** en la categoría Servicios de documentos del explorador de componentes de su página.
1. Seleccione el componente y, a continuación, seleccione ![settings_icon](assets/settings_icon.png) para abrir el cuadro de diálogo Editar del componente.

   ![Componente Borradores y envíos](assets/drafts-submissions-edit.png)

1. En el cuadro de diálogo Editar, especifique los siguientes detalles y seleccione **Listo** para guardar la configuración.

<table>
 <tbody>
  <tr>
   <th>Pestaña</th>
   <th>Configuración</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>General</td>
   <td>Resultado total</td>
   <td>Especifica el número máximo de resultados que se van a mostrar. Si el recuento de resultados aumenta el límite de resultados totales, aparecerá el vínculo <strong>Más </strong>en la parte inferior del componente. Si hace clic en <strong>Más</strong>, se mostrarán todos los formularios. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Tipo de estilo</td>
   <td>Especifica el estilo del componente. Puede especificar <strong>Sin estilo</strong>, <strong>Estilo predeterminado</strong> o <strong>Estilo personalizado</strong> para enumerar los formularios. Para la opción Estilo personalizado, puede especificar la ruta del archivo CSS personalizado en el campo <strong>Ruta de estilo personalizada</strong><strong>.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Ruta de estilo personalizada</td>
   <td>Si elige la opción <strong>Estilo personalizado</strong> en el campo <strong>Tipo de estilo</strong>, utilice la <strong>Ruta de estilo personalizada</strong> para especificar la ruta del archivo CSS personalizado. </td>
  </tr>
  <tr>
   <td> </td>
   <td>Opciones de visualización</td>
   <td><p>Especifica las pestañas que se van a mostrar. Puede elegir mostrar formularios en borrador, formularios enviados o ambos. </p> <p><strong>Nota</strong>:<em> Para <strong>Opciones de visualización</strong>, si selecciona una opción distinta de <strong>Ambos</strong>, la opción <strong>pestaña Predeterminada</strong> no se utilizará.</em></p> </td>
  </tr>
  <tr>
   <td> </td>
   <td>Pestaña predeterminada</td>
   <td>Especifica la pestaña que se mostrará cuando se cargue la página del portal de formularios. Puede elegir entre la <strong>Pestaña Formularios en borrador</strong> y <strong>Pestaña Formularios enviados</strong>.</td>
  </tr>
  <tr>
   <td>Configuración de pestañas de borrador de formularios</td>
   <td>Título personalizado</td>
   <td>Especifica el título de la pestaña <strong>Formularios en borrador</strong>. El valor predeterminado es <strong>Formularios en borrador.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica el diseño que se utiliza para la lista Formularios en borrador.</td>
  </tr>
  <tr>
   <td>Configuración de la pestaña Formularios enviados</td>
   <td>Título personalizado </td>
   <td>Especifica el título de la pestaña <strong>Formularios enviados</strong>. El valor predeterminado es <strong>Formularios enviados.</strong></td>
  </tr>
  <tr>
   <td> </td>
   <td>Plantilla de diseño</td>
   <td>Especifica el diseño que se va a utilizar para la lista <strong>Formularios enviados</strong>. </td>
  </tr>
 </tbody>
</table>

## Personalizar el almacenamiento {#customizing-the-storage}

Cuando se utiliza la acción de envío del portal de formularios o se activa la opción Almacenar datos en el portal de formularios en formularios adaptables, los datos del formulario se almacenan en el repositorio de AEM. En un entorno de producción, se recomienda no almacenar datos de formularios en borradores o enviados en el repositorio de AEM. En lugar de ello, debe integrar los borradores y el componente de envío con un almacenamiento seguro, como la base de datos empresarial, para almacenar borradores y datos de formularios enviados.

El portal de Forms permite almacenar datos en el repositorio local de AEM, en el repositorio remoto de AEM o en una base de datos. AEM Forms permite personalizar la implementación del almacenamiento de datos de usuario para borradores y envíos. Puede anular los métodos predeterminados para especificar cómo se almacenan los datos de borradores y envíos en el almacenamiento que elija. Por ejemplo, puede almacenar los datos en un repositorio de datos implementado en su organización actualmente.

El portal de formularios proporciona servicios listos para usar (API) para almacenar datos en el repositorio crx de instancias de publicación locales y remotas de AEM Forms. Puede reemplazar las implementaciones predeterminadas que se describen en [Configurar servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md), con implementaciones personalizadas para reemplazar la funcionalidad predeterminada. Para obtener información detallada sobre los métodos necesarios en una implementación personalizada para almacenar contenido en una ubicación segura, consulte [Personalizar los servicios de datos de Borradores y envíos](/help/forms/using/custom-draft-submission-data-services.md) y [Almacenamiento personalizado para el componente Borradores y envíos.](/help/forms/using/adding-custom-storage-provider-forms.md)

La documentación de AEM Forms proporciona un [Ejemplo para integrar el componente Borradores y envíos con la base de datos](integrate-draft-submission-database.md). Puede utilizar la implementación de muestra para desarrollar su propia implementación personalizada.

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Creación de una página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar el componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalizar el almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizar plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
