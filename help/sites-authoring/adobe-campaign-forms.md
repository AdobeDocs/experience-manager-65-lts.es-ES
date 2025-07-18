---
title: Creación de Adobe Campaign Forms en Adobe Experience Manager
description: Adobe Experience Manager permite crear y utilizar formularios que interactúen con Adobe Campaign en el sitio web
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization,Integration
role: User,Admin,Architect,Developer
exl-id: 6a72ba56-8222-4853-adc6-ee8f3d395d9d
source-git-commit: 2edf37c2d6bb04b418618f2780f773ab37559114
workflow-type: tm+mt
source-wordcount: '1280'
ht-degree: 0%

---

# Creación de Adobe Campaign Forms en AEM {#creating-adobe-campaign-forms-in-aem}

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

Para ello, consulte la [documentación de plantillas](/help/sites-developing/templates.md#template-availability).

## Creación de un formulario {#creating-a-form}

En primer lugar, compruebe la conexión entre las instancias de autor y publicación, y Adobe Campaign está funcionando. Ver [Integración con Adobe Campaign Standard](/help/sites-administering/campaignstandard.md) o [Integración con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md).

>[!NOTE]
>
>Asegúrese de que la propiedad **acMapping** del nodo **jcr:content** de la página esté establecida en **mapRecipient** o **profile** al usar Adobe Campaign Classic o Adobe Campaign Standard, respectivamente
>

1. En AEM, en Sitios, vaya a donde desee crear una página.
1. Cree una página, seleccione **Perfil de Adobe Campaign Classic** o **Perfil de Adobe Campaign Standard** y haga clic en **Siguiente**.

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >Si la plantilla deseada no está disponible, consulte [Disponibilidad de plantillas](/help/sites-developing/templates.md#template-availability).

1. En el campo **Nombre**, agregue el nombre de la página. Debe ser un nombre JCR válido.
1. En el campo **Título**, escriba un título y haga clic en **Crear**.
1. Abra la página y seleccione **Abrir propiedades**. En Cloud Services, agregue la configuración de Adobe Campaign y marque la casilla de verificación para guardar los cambios.

   ![chlimage_1-44](assets/chlimage_1-44a.png)

1. En la página, en el componente **Inicio del formulario**, seleccione el tipo de formulario que es: **Suscribirse, Cancelar la suscripción,** o **Guardar perfil**. Solo puede tener un tipo por formulario. Ahora puede [editar el contenido del formulario](#editing-form-content).

## Edición del contenido del formulario {#editing-form-content}

Forms dedicado a Adobe Campaign tiene componentes específicos. Estos componentes tienen una opción para permitirle vincular cada campo del formulario a un campo de la base de datos de Adobe Campaign.

>[!NOTE]
>
>Si la plantilla deseada no está disponible, consulte [Disponibilidad de una plantilla.](/help/sites-authoring/campaign.md)

Esta sección solo detalla los vínculos específicos a Adobe Campaign. Para obtener más información sobre una descripción general más general de cómo usar formularios en Adobe Experience Manager, consulte [Editar componentes de modo](/help/sites-authoring/default-components-foundation.md).

1. Seleccione **Abrir propiedades** y en Cloud Services agregue la configuración de Adobe Campaign y marque la casilla de verificación para guardar los cambios.

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. En la página, en el componente **Inicio del formulario**, haga clic en el icono Configuración.

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. Haga clic en la ficha **Avanzado** y seleccione el tipo de formulario que es: **Suscribirse, cancelar la suscripción,** o **Guardar perfil**. A continuación, haga clic en **Aceptar.**: solo puede tener un tipo por formulario.

   * **Adobe Campaign: Guardar perfil**: permite crear o actualizar un destinatario en Adobe Campaign (valor predeterminado).
   * **Adobe Campaign: Suscribirse a servicios**: permite administrar las suscripciones de un destinatario en Adobe Campaign.
   * **Adobe Campaign: Cancelar suscripción a los servicios**: permite cancelar las suscripciones de un destinatario en Adobe Campaign.

1. Debe tener un componente **Clave principal cifrada** en cada formulario. Este componente define qué parámetro de URL se utiliza para aceptar la clave principal cifrada de un perfil de Adobe Campaign. En Componentes, seleccione Adobe Campaign para que solo estén visibles esos componentes.
1. Arrastre el componente **Clave principal cifrada** al formulario (en cualquier lugar) y haga clic en el icono **Configuración**. En la ficha **Adobe Campaign**, especifique cualquier nombre para el parámetro de URL. Haga clic en la marca de verificación para guardar los cambios.

   Los vínculos generados para este formulario deben utilizar este parámetro de URL y asignarle la clave principal cifrada de un perfil de Adobe Campaign. La clave principal cifrada debe tener la codificación URL (porcentaje) correcta.

   ![chlimage_1-47](assets/chlimage_1-47a.png)

1. Agregue componentes al formulario según sea necesario, como un campo de texto, un campo de fecha, un campo de casilla de verificación, un campo de opción, etc. Consulte [Componentes de formularios Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) para obtener más información sobre cada componente.
1. Haga clic en el icono Configuración para abrir el componente. Por ejemplo, en el componente **Campo de texto (Campaign)**, cambie el título y el texto.

   Haga clic en **Adobe Campaign** para asignar el campo de formulario a una variable de metadatos de Adobe Campaign. Al enviar el formulario, el campo asignado se actualiza en Adobe Campaign. En el selector de variables solo están disponibles los campos con tipos coincidentes (por ejemplo, las variables de cadena para los campos de texto).

   ![chlimage_1-48](assets/chlimage_1-48a.png)

   >[!NOTE]
   >
   >Puede agregar o quitar campos que se muestran en la tabla de destinatarios siguiendo las instrucciones aquí: [https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/](https://blogs.adobe.com/experiencedelivers/experience-management/aem-campaign-integration/)

1. Haga clic en **Publicar página**. La página se activa en el sitio. Puede verla en la instancia de publicación de AEM. También puede [probar un formulario](#testing-a-form).

   >[!CAUTION]
   >
   >Debe proporcionar permisos de lectura al usuario anónimo en el servicio en la nube para utilizar formularios al publicar. Sin embargo, tenga en cuenta los posibles problemas de seguridad al proporcionar permisos de lectura al usuario anónimo y asegúrese de mitigarlo, por ejemplo, configurando Dispatcher.

## Prueba de un formulario {#testing-a-form}

Después de crear un formulario y editar su contenido, es posible que desee probar manualmente que el formulario funciona según lo esperado.

>[!NOTE]
>
>Debe tener un componente **Clave principal cifrada** en cada formulario. En Componentes, seleccione Adobe Campaign para que solo estén visibles esos componentes.
>
>Aunque en este procedimiento introduzca el número epk manualmente, en la práctica los usuarios obtendrían un vínculo a esta página (ya sea para cancelar la suscripción, suscribirse o actualizar su perfil) dentro de un boletín informativo. El epk se actualiza automáticamente en función del usuario.
>
>Para crear ese vínculo, usa la variable **Identificador de recurso principal**(Adobe Campaign Standard) o **Identificador cifrado** (Adobe Campaign Classic) (por ejemplo, en un componente **Texto y Personalization (Campaign)**), que se vincula al epk en Adobe Campaign.

Para ello, debe obtener manualmente el EPK de un perfil de Adobe Campaign y anexarlo a la dirección URL:

1. Para obtener la clave principal cifrada (EPK) de un perfil de Adobe Campaign:

   * En Adobe Campaign Standard: vaya a **Perfiles y audiencias** > **Perfiles**, que enumera los perfiles existentes. Asegúrese de que la tabla muestre el campo **Identificador de recurso principal** en una columna (esto se puede configurar haciendo clic o pulsando **Configurar lista**). Copie el identificador de recurso principal del perfil deseado.
   * En Adobe Campaign Classic, vaya a **Perfiles y objetivos** > **Destinatarios**, que enumera los perfiles existentes. Asegúrese de que la tabla muestre el campo **Identificador cifrado** en una columna (esto se puede configurar haciendo clic con el botón derecho en una entrada y seleccionando **Configurar lista...**). Copie el identificador cifrado del perfil deseado.

1. En AEM, abra la página del formulario en la instancia de publicación y anexe el EPK del paso 1 como parámetro de URL: use el mismo nombre que definió anteriormente en el componente EPK al crear el formulario (por ejemplo: `?epk=...`)
1. Ahora el formulario se puede utilizar para modificar los datos y las suscripciones asociados al perfil de Adobe Campaign vinculado. Después de modificar algunos campos y enviar el formulario, puede comprobar dentro de Adobe Campaign que se han actualizado los datos correspondientes.

Los datos de la base de datos de Adobe Campaign se actualizan una vez validado un formulario.
