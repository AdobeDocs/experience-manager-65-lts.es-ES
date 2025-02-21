---
title: Crear un perfil personalizado para formularios HTML5
description: Un perfil de formularios HTML5 es un nodo de recursos en Apache Sling. Representa una versión personalizada del servicio de procesamiento de formularios HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 9cd22244-9aa6-4b5f-96cf-c9cb3d6f9c8a
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 96%

---

# Crear un perfil personalizado para formularios HTML5 {#creating-a-custom-profile-for-html-forms}

Un perfil es un nodo de recursos en [Apache Sling](https://sling.apache.org/). Representa la versión personalizada del servicio de representación de formularios HTML5. Puede utilizar el servicio de representación de formularios HTML5 para personalizar el aspecto, el comportamiento y las interacciones de los formularios HTML5. Existe un nodo de perfil en la carpeta `/content` en el repositorio JCR. Puede colocar el nodo directamente debajo de la carpeta `/content` o cualquier subcarpeta de la carpeta `/content`.

El nodo de perfil tiene la propiedad **sling:resourceSuperType** y el valor predeterminado es **xfaforms/profile**. El script de procesamiento para el nodo se encuentra en /libs/xfaforms/profile.

Los scripts de Sling son scripts JSP. Estos scripts JSP sirven como contenedores para reunir el HTML del formulario solicitado y los artefactos JS/CSS necesarios. Estos scripts de Sling también se denominan **Scripts de procesador de perfiles**. El procesador de perfiles llama al servicio OSGi de Forms para procesar el formulario solicitado.

El script de perfil se encuentra en html.jsp y html.POST.jsp para solicitudes de GET y POST. Puede copiar y modificar uno o más archivos para anular y agregar las personalizaciones. No realice ningún cambio local, la actualización del parche sobrescribirá dichos cambios.

Un perfil contiene varios módulos. Los módulos son formRuntime.jsp, config.jsp, toolbar.jsp, formBody.jsp, nav_footer.jsp y footer.jsp.

## formRuntime.jsp {#formruntime-jsp-br}

Los módulos formRuntime.jsp contienen referencias de las bibliotecas cliente. También muestra los métodos para extraer información de configuración regional de la solicitud e incluir los mensajes localizados en la solicitud. Puede incluir sus propias bibliotecas o estilos personalizados de JavaScript en formRuntime.jsp.

## config.jsp {#config-jsp}

El módulo config.jsp contiene varias configuraciones, como el registro, los servicios proxy y la versión de comportamiento. Puede agregar su propia configuración y personalización de widgets al módulo config.jsp. También puede agregar configuraciones como el registro de widgets personalizados al módulo config.jsp.

## toolbar.jsp {#toolbar-jsp}

El archivo toolbar.jsp contiene código para crear una barra de herramientas de color. Para quitar la barra de herramientas, quite toolbar.jsp del HTML.jsp

## formBody.jsp {#formbody-jsp}

El módulo formBody.jsp es para la representación HTML del formulario XFA.

## nav_footer.jsp {#nav-footer-jsp}

Al principio, el formulario HTML5 solo procesará la primera página del formulario. Cuando un usuario desplace el formulario, se cargará el resto de los formularios. Hace que la experiencia de carga sea más rápida. El componente nav_footer.jsp contiene todos los estilos y elementos necesarios para facilitar la carga de las páginas en el desplazamiento.

## footer.jsp {#footer-jsp}

El módulo footer.jsp está vacío. Permite añadir scripts que solo se utilizan para la interacción del usuario.

## Crear perfiles personalizados {#creating-custom-profiles}

Para crear un perfil personalizado, realice los siguientes pasos:

### Crear nodo de perfil {#create-profile-node}

1. Navegue hasta la interfaz CRX DE en la URL: `https://'[server]:[port]'/crx/de` e inicie sesión en la interfaz con credenciales de administrador.

1. En el panel izquierdo, navegue hasta la ubicación */content/xfaforms/profiles*.

1. Copie el nodo predeterminado y péguelo en una carpeta diferente (*/content/profiles*) con el nombre *hrform*.

1. Seleccione el nodo nuevo, *hrform* y agregue una propiedad de cadena: *sling:resourceType* con valor: *hrform/demo*.

1. Haga clic en Guardar todo en el menú de la barra de herramientas para guardar los cambios.

### Crear el script de procesamiento de perfil {#create-the-profile-renderer-script}

Después de crear un perfil personalizado, agregue información de procesamiento a este perfil. Al recibir una solicitud para el nuevo perfil, CRX verifica la existencia de la carpeta /apps para que se represente la página JSP. Cree la página JSP en la carpeta /apps.

1. En el panel izquierdo, navegue hasta la carpeta `/apps`.
1. Haga clic con el botón derecho en la carpeta `/apps` y elija crear una carpeta con el nombre **hrform**.
1. Dentro de la carpeta **hrform** cree una carpeta llamada **demo**.
1. Haga clic en el botón **Guardar todo**.
1. Navegue hasta `/libs/xfaforms/profile/html.jsp` y copie el nodo **html.jsp**.
1. Pegue el nodo **html.jsp** en la carpeta `/apps/hrform/demo` creada anteriormente con el mismo nombre **html.jsp** y haga clic en **Guardar**.
1. Si tiene cualquier otro componente del script de perfil, siga los pasos del 1 al 6 para copiar los componentes en la carpeta /apps/hrform/demo.

1. Para comprobar que el perfil se ha creado, abra la dirección URL `https://'[server]:[port]'/content/xfaforms/profiles/hrform.html`

Para comprobar los formularios, [Importe sus formularios](/help/forms/using/get-xdp-pdf-documents-aem.md) desde el sistema de archivos local a AEM Forms y [abra la vista previa del formulario](/help/forms/using/previewing-forms.md) en la instancia de autor del servidor de AEM.
