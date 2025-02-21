---
title: Administración de identidades
description: Obtenga información acerca del funcionamiento interno de la administración de identidades en AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 006e91327d15dd4dd0482230d6ad8535e924698e
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 1%

---


# Administración de identidades{#identity-management}

Los visitantes individuales del sitio web solo se pueden identificar si se permite que inicien sesión. Existen varias razones por las que puede que desee proporcionar una capacidad de inicio de sesión:

* [Grupos de usuarios cerrados](/help/sites-administering/cug.md)

  Es posible que deba limitar el acceso a su sitio web (o a secciones de este) a visitantes específicos.

* [Personalization](/help/sites-administering/personalization.md) permite que los visitantes configuren ciertos elementos para acceder al sitio web.

La funcionalidad de inicio (y cierre) de sesión la proporciona una cuenta de [con un **perfil**](#profiles-and-user-accounts), que contiene información adicional acerca del visitante (usuario) registrado. Los procesos reales de registro y autorización pueden diferir:

* Registro automático desde el sitio web

* Solicitud de registro en el sitio web

  En el caso de un grupo de usuarios cerrado, puede permitir a los visitantes solicitar el registro, pero exigir la autorización mediante un flujo de trabajo.

* Registre cada cuenta del entorno de creación

  Si tiene un pequeño número de perfiles, que necesitarán autorización de todos modos, puede decidir registrar cada uno directamente.

Para permitir que los visitantes se registren, se puede utilizar una serie de componentes y formularios para recopilar la información de identificación necesaria y, a continuación, la información de perfil adicional (a menudo opcional). Después de registrarse, también deben poder comprobar y actualizar los detalles que han enviado.

Se pueden configurar o desarrollar funciones adicionales:

* Configure cualquier replicación inversa que sea necesaria.
* Permiten que un usuario elimine su perfil desarrollando un formulario junto con un flujo de trabajo.

>[!NOTE]
>
>La información especificada en el perfil también se puede usar para proporcionar al usuario contenido de destino mediante [Segmentos](/help/sites-administering/campaign-segmentation.md) y [Campañas](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md).

## Forms de registro {#registration-forms}

Se puede usar un [formulario](/help/sites-authoring/default-components.md#form-component) para recopilar la información de registro y generar la nueva cuenta y perfil.

Por ejemplo, los usuarios pueden solicitar un perfil nuevo mediante la página de Geometrixx
`http://localhost:4502/content/geometrixx-outdoors/en/user/register.html`

![Formulario de registro de muestra](assets/registerform.png)

Al enviar la solicitud, se abre la página de perfil, donde el usuario puede proporcionar detalles personales.

![Página de perfil de muestra](assets/profilepage.png)

La nueva cuenta también está visible en la [consola Usuarios](/help/sites-administering/security.md).

## Inicio de sesión {#login}

El componente de inicio de sesión se puede utilizar para recopilar la información de inicio de sesión y, a continuación, activar el proceso de inicio de sesión.

Esto proporciona al visitante los campos estándar de **Nombre de usuario** y **Contraseña**, con un botón de **Inicio de sesión** para activar el proceso de inicio de sesión cuando se ingresen las credenciales.

Por ejemplo, los usuarios pueden iniciar sesión o crear una cuenta con la opción **Iniciar sesión** de la barra de herramientas de Geometrixx, que usa la página:

`http://localhost:4502/content/geometrixx-outdoors/en/user/sign-in.html`

![Página de inicio de sesión de muestra](assets/login.png)

## Cerrando sesión {#logging-out}

Dado que hay un mecanismo de inicio de sesión, también es necesario un mecanismo de cierre de sesión. Esta opción está disponible como la opción **Cerrar sesión** en Geometrixx.

## Visualización y actualización de un perfil {#viewing-and-updating-a-profile}

Según el formulario de registro, es posible que el visitante tenga información registrada en su perfil. Deberían poder ver o actualizar esto en una etapa posterior. Esto se puede hacer con un formulario similar; por ejemplo, en Geometrixx:

```
http://localhost:4502/content/geometrixx-outdoors/en/user/profile.html
```

Para ver los detalles del perfil, haz clic en **Mi perfil** en la esquina superior derecha de cualquier página; por ejemplo, con la cuenta de `admin`:
`http://localhost:4502/home/users/a/admin/profile.form.html/content/geometrixx-outdoors/en/user/profile.html.`

Puede ver otro perfil usando el [contexto de cliente](/help/sites-administering/client-context.md) (en el entorno de creación y con privilegios suficientes):

1. Abra una página; por ejemplo, la página de Geometrixx:

   `http://localhost:4502/cf#/content/geometrixx/en.html`

1. Haga clic en **Mi perfil** en la esquina superior derecha. Verá el perfil de su cuenta actual; por ejemplo, el administrador.
1. Presione **control-alt-C** para abrir el contexto del cliente.
1. En la esquina superior izquierda del contexto de cliente, haga clic en el botón **Cargar un perfil**.

   ![Cargar un icono de perfil](do-not-localize/loadprofile.png)

1. Seleccione otro perfil en la lista desplegable de la ventana de diálogo; por ejemplo, **Alison Parker**.
1. Haga clic en **OK**.
1. Haz clic de nuevo en **Mi perfil**. El formulario se actualizará con los detalles de Alison.

   ![Perfil de muestra de Alison](assets/profilealison.png)

1. Ahora puede usar **Editar perfil** o **Cambiar contraseña** para actualizar los detalles.

## Adición de campos a la definición del perfil {#adding-fields-to-the-profile-definition}

Puede añadir campos a la definición del perfil. Por ejemplo, para agregar un campo &quot;Color favorito&quot; al perfil de Geometrixx:

1. En la consola Sitios web, vaya a Sitio de Geometrixx Outdoors > Inglés > Usuario > Mi perfil.
1. Haga doble clic en la página **Mi perfil** para abrirla y editarla.
1. En la ficha **Componentes** de la barra de tareas, expanda la sección **Formulario**.
1. Arrastre una **lista desplegable** de la barra de tareas al formulario, justo debajo del campo **Acerca de mí**.
1. Haga doble clic en el componente **Lista desplegable** para abrir el cuadro de diálogo y especificar:

   * **Nombre de elemento** - `favoriteColor`
   * **Título** - `Favorite Color`
   * **Elementos** - Agregar varios colores como elementos

   Haga clic en **Aceptar** para guardar.

1. Cierre la página, vuelva a la consola **Sitios web** y active la página Mi perfil.

   La próxima vez que vea un perfil, puede seleccionar un color favorito:

   ![Campo de muestra de color favorito de Alison Parker](assets/aparkerfavcolour.png)

   El campo se guardará en la sección **perfil** de la cuenta de usuario correspondiente:

   ![Datos de Alison Parker en CRXDE](assets/aparkercrxdelite.png)

## Estados de perfil {#profile-states}

Hay varios casos de uso que requieren saber si un usuario (o más bien su perfil) está en un *estado específico* o no.

Esto implica definir una propiedad adecuada en el perfil de usuario de una manera que:

* es visible y accesible para el usuario
* define dos estados para cada propiedad
* permite alternar entre los dos estados definidos

Esto se realiza con:

* [Proveedores estatales](#state-providers)

  Para administrar los dos estados de una propiedad específica y las transiciones entre los dos.

* [Flujos de trabajo](#workflows)

  Para administrar acciones relacionadas con los estados.

Se pueden definir varios estados; por ejemplo, en Geometrixx, estos incluyen:

* suscripción (o cancelación de la suscripción) a notificaciones en boletines informativos o hilos de comentarios
* agregar y quitar una conexión a un amigo

### Proveedores estatales {#state-providers}

Un proveedor de estado administra el estado actual de la propiedad en cuestión, junto con las transiciones entre los dos estados posibles.

Los proveedores de estado se implementan como componentes, por lo que se pueden personalizar para el proyecto. En Geometrixx, estos incluyen:

* Suscribirse/cancelar suscripción de tema de foro
* Agregar o quitar amigo

### Flujos de trabajo {#workflows}

Los proveedores estatales administran una propiedad de perfil y sus estados.

Se necesita un flujo de trabajo para implementar las acciones relacionadas con los estados. Por ejemplo, al suscribirse a notificaciones, el flujo de trabajo gestiona la acción de suscripción real; al cancelar la suscripción a notificaciones, el flujo de trabajo gestiona la eliminación del usuario de la lista de suscripción.

## Perfiles y cuentas de usuario {#profiles-and-user-accounts}

Los perfiles se almacenan en el repositorio de contenido como parte de la [cuenta de usuario](/help/sites-administering/user-group-ac-admin.md).

El perfil se encuentra en `/home/users/geometrixx`:

![Perfiles tal como se ven en CRXDE](assets/chlimage_1-138.png)

En una instalación estándar (de autor o publicación), todos tienen acceso de lectura a toda la información de perfil de todos los usuarios. todos son un &quot;*grupo integrado que contiene automáticamente todos los usuarios y grupos existentes. La lista de miembros no se puede editar*&quot;.

Estos derechos de acceso se definen mediante la siguiente ACL comodín:

/home todos permitir jcr:leer rep:glob = &#42;/perfil&#42;

Esto permite:

* foro, comentarios o entradas de blog para mostrar información (como el icono o el nombre completo) del perfil correspondiente.
* vínculos a páginas de perfil de geometrixx

Si este acceso no es apropiado para su instalación, puede cambiar esta configuración predeterminada.

Esto se puede hacer con la ficha **[Control de acceso](/help/sites-administering/user-group-ac-admin.md#access-right-management)**:

![Administrar ACL en CRXDE](assets/aclmanager.png)

## Componentes de perfil {#profile-components}

También hay disponible una serie de componentes de perfil para definir los requisitos de perfil de su sitio.

### Campo de contraseña activado {#checked-password-field}

Este componente le proporciona dos campos para:

* la entrada de una contraseña
* una comprobación para confirmar que la contraseña se ha introducido correctamente.

Con la configuración predeterminada, el componente aparecerá de la siguiente manera:

![Cuadro de diálogo Comprobar contraseña](assets/dc_profiles_checkedpassword.png)

### Fotografía de avatar de perfil {#profile-avatar-photo}

Este componente proporciona al usuario un mecanismo para seleccionar y cargar un archivo de fotografía de avatar.

![Selector de avatar](assets/dc_profiles_avatarphoto.png)

### Nombre detallado de perfil {#profile-detailed-name}

Este componente permite al usuario introducir un nombre detallado.

![Cuadro de diálogo de nombres detallado](assets/dc_profiles_detailedname.png)

### Género de perfil {#profile-gender}

Este componente permite al usuario introducir su sexo.

![Selector de género](assets/dc_profiles_gender.png)
