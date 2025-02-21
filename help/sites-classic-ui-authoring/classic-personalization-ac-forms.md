---
title: Creación de Adobe Campaign Forms en AEM
description: AEM permite crear y utilizar formularios que interactúen con Adobe Campaign en el sitio web. Se pueden insertar campos específicos en los formularios y asignarlos a la base de datos de Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 1a942dc471cde14fa3b811b31e54644e199f8738
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Creación de Adobe Campaign Forms en AEM{#creating-adobe-campaign-forms-in-aem}

AEM permite crear y utilizar formularios que interactúen con Adobe Campaign en el sitio web. Se pueden insertar campos específicos en los formularios y asignarlos a la base de datos de Adobe Campaign.

Puede administrar nuevas suscripciones de contacto, bajas de suscripción y datos de perfil de usuario, todo ello a la vez que integra sus datos en la base de datos de Adobe Campaign.

Para utilizar formularios Adobe Campaign en AEM, debe seguir estos pasos, que se describen en este documento:

1. Hacer que una plantilla esté disponible.
1. Creación de un formulario.
1. Editar contenido del formulario.

Hay tres tipos de formularios disponibles de forma predeterminada, específicos de Adobe Campaign:

* Guardar un perfil
* Suscripción a un servicio
* Cancelar la suscripción a un servicio

Estos formularios definen un parámetro de URL que acepta la clave principal cifrada de un perfil de Adobe Campaign. En función de este parámetro de URL, el formulario actualiza los datos del perfil de Adobe Campaign asociado.

Aunque estos formularios se crean de forma independiente, en un caso de uso habitual, se genera un vínculo personalizado a una página de formulario dentro del contenido del boletín informativo para que los destinatarios puedan abrir el vínculo y realizar ajustes en los datos de perfil (ya sea cancelar la suscripción, suscribirse o actualizar el perfil).

El formulario se actualiza automáticamente en función del usuario. Consulte [Edición del contenido del formulario](#editing-form-content) para obtener más información.

## Disponibilidad de una plantilla {#making-a-template-available}

Antes de poder crear formularios específicos de Adobe Campaign, debe hacer que las distintas plantillas estén disponibles en la aplicación de AEM.

En primer lugar, compruebe la conexión entre las instancias de autor y publicación, y Adobe Campaign está funcionando. Consulte [Integración con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integración con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la propiedad **acMapping** del nodo **jcr:content** de la página esté establecida en **mapRecipient** o **profile** al usar Adobe Campaign 6.1.x o Adobe Campaign Standard, respectivamente
>

### Creación de un formulario {#creating-a-form}

1. Comience en siteadmin.
1. Desplácese por la estructura de árbol para llegar al lugar en el que desee crear el formulario en el sitio web seleccionado.
1. Seleccione **Nueva** > **Nueva página...**.
1. Seleccione la plantilla **Adobe Campaign Profile (AC 6.1)** o **Adobe Campaign Profile (ACS)** e introduzca las propiedades de la página.

   >[!NOTE]
   >
   >Si la plantilla no está disponible, consulte la sección [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

1. Haga clic en **Crear** para crear el formulario.

   ![chlimage_1-187](assets/chlimage_1-187.png)

   A continuación, puede [editar y configurar el contenido del formulario](#editing-form-content).

## Edición del contenido del formulario {#editing-form-content}

Forms dedicado a Adobe Campaign tiene componentes específicos. Estos componentes tienen una opción para permitirle vincular cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>Si la plantilla deseada no está disponible, consulte [Disponibilidad de una plantilla](/help/sites-classic-ui-authoring/classic-personalization-ac.md#activatingatemplate).

Esta sección solo detalla los vínculos específicos a Adobe Campaign. Para obtener más información sobre una descripción general más general de cómo usar formularios en Adobe Experience Manager, consulte [Editar componentes de modo](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md).

1. Desplácese hasta el formulario que desee editar.
1. En el cuadro de herramientas, seleccione **Página** > **Propiedades de página...** y, a continuación, vaya a la pestaña **Cloud Services** de la ventana emergente.
1. Agregue el servicio Adobe Campaign haciendo clic en **Agregar servicio** y, a continuación, seleccionando la configuración que corresponda a su instancia de Adobe Campaign en la lista desplegable del servicio. Esta configuración se realiza al configurar la conexión entre las instancias. Para obtener más información, consulte [Conectar AEM a Adobe Campaign](/help/sites-administering/campaignonpremise.md#connecting-aem-to-adobe-campaign).

   >[!NOTE]
   >
   >Si es necesario, desbloquee la configuración haciendo clic en el icono de candado para poder agregar el servicio de Adobe Campaign.

1. Acceda a los parámetros generales del formulario con el botón **Editar** que se encuentra al principio del formulario. La pestaña **Form** le permite seleccionar una página de agradecimiento a la que se redirigirá al usuario después de haber validado el formulario.

   El formulario **Avanzado** le permite seleccionar el tipo de formulario. El campo **Opciones de publicación** le permite elegir entre tres tipos de formularios Adobe Campaign:

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscribirse a servicios**: permite administrar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.

   El campo **Configuración de la acción** le permite especificar si desea crear o no el perfil de destinatario en la base de datos de Adobe Campaign si aún no existe. Para ello, marque la opción **Crear usuario si no existe**.

1. Añada los componentes seleccionados arrastrándolos desde el cuadro de herramientas y soltándolos en el formulario. Para obtener más información sobre los componentes específicos de Adobe Campaign disponibles, consulte [Componentes de formularios Adobe](/help/sites-classic-ui-authoring/classic-personalization-ac-components.md).

   ![chlimage_1-188](assets/chlimage_1-188.png)

1. Configure los campos agregados haciendo doble clic en ellos. La pestaña **Adobe Campaign** le permite vincular el campo a un campo de la tabla de destinatarios de Adobe Campaign. También puede especificar si el campo forma parte de la clave de reconciliación que permite reconocer a los destinatarios que ya están presentes en la base de datos de Adobe Campaign.

   >[!CAUTION]
   >
   >El **Nombre de elemento** debe ser diferente para cada campo de formulario. Cámbielo si es necesario.
   >
   >Cada formulario debe contener un componente **Clave principal cifrada** para administrar correctamente los destinatarios en la base de datos de Adobe Campaign.

1. Para activar la página, seleccione **Página** > **Activar página** en la caja de herramientas. La página se activa en el sitio. Puede verla en la instancia de publicación de AEM. Los datos de la base de datos de Adobe Campaign se actualizan una vez validado un formulario.

## Prueba de un formulario {#testing-a-form}

Después de crear un formulario y editar su contenido, es posible que desee probar manualmente que el formulario funciona según lo esperado.

>[!NOTE]
>
>Debe tener un componente **Clave principal cifrada** en cada formulario. En Componentes, seleccione Adobe Campaign para que solo estén visibles esos componentes.
>
>Aunque en este procedimiento introduzca el número epk manualmente, en la práctica los usuarios obtendrían un vínculo a esta página (ya sea para cancelar la suscripción, suscribirse o actualizar su perfil) dentro de un boletín informativo. El epk se actualiza automáticamente en función del usuario.
>
>Para crear ese vínculo, usa la variable **Identificador de recurso principal**(Adobe Campaign Standard) o **Identificador cifrado** (Adobe Campaign 6.1) (por ejemplo, en un componente **Texto y Personalization (Campaign)**), que vincula al epk en Adobe Campaign.

Para ello, debe obtener manualmente el EPK de un perfil de Adobe Campaign y anexarlo a la dirección URL:

1. Para obtener la clave principal cifrada (EPK) de un perfil de Adobe Campaign:

   * En Adobe Campaign Standard: vaya a **Perfiles y audiencias** > **Perfiles**, que enumera los perfiles existentes. Asegúrese de que la tabla muestre el campo **Identificador de recurso principal** en una columna (esto se puede configurar haciendo clic o pulsando **Configurar lista**). Copie el identificador de recurso principal del perfil deseado.
   * En Adobe Campaign 6.11, vaya a **Perfiles y objetivos** > **Destinatarios**, que enumera los perfiles existentes. Asegúrese de que la tabla muestre el campo **Identificador cifrado** en una columna (esto se puede configurar haciendo clic con el botón derecho en una entrada y seleccionando **Configurar lista...**). Copie el identificador cifrado del perfil deseado.

1. En AEM, abra la página del formulario en la instancia de publicación y anexe el EPK del paso 1 como parámetro de URL: use el mismo nombre que definió anteriormente en el componente EPK al crear el formulario (por ejemplo: `?epk=...`)
1. Ahora el formulario se puede utilizar para modificar los datos y las suscripciones asociados al perfil de Adobe Campaign vinculado. Después de modificar algunos campos y enviar el formulario, puede comprobar dentro de Adobe Campaign que se han actualizado los datos correspondientes.

Los datos de la base de datos de Adobe Campaign se actualizan una vez validado un formulario.
