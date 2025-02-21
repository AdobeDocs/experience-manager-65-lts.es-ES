---
title: Usar el flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro
description: Aprenda a utilizar los flujos de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro.
content-type: reference
topic-tags: develop
noindex: true
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 98%

---

# Usar el flujo de trabajo de traducción de AEM para localizar formularios adaptables y documentos de registro {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

Los formularios localizados le ayudan a llegar a una audiencia más amplia en todas las regiones geográficas. El flujo de trabajo de traducción de Adobe Experience Manager le ayuda a localizar formularios adaptables y sus documentos de registro. Puede usar la **traducción automática** o **traductores humanos** para localizar un formulario adaptable.

Este artículo explica el proceso para utilizar el flujo de trabajo de traducción de AEM con formularios adaptables y documentos de registro.

## Localizar un formulario adaptable y un documento de registro mediante traducción automática {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

El servicio de traducción automática traduce inmediatamente el contenido de los formularios adaptables y los documentos de registro. AEM Forms está preconfigurado para utilizar una versión de prueba de Microsoft Translator para la traducción automática. Realice los siguientes pasos para habilitar la traducción automática en los formularios adaptables y los documentos de registro:

1. En la interfaz de usuario de AEM Forms, selecciona un formulario y selecciona la opción **Agregar diccionario**.
1. En la pantalla **Agregar diccionario al proyecto de traducción**, seleccione las opciones **Crear un nuevo proyecto de traducción** o **Agregar a un proyecto de traducción existente**.
1. En el campo **Título del proyecto**, especifique el título. Por ejemplo, `Government Reference Site - German locale.`
1. En el campo **Idiomas de destino**, especifique una configuración regional (por ejemplo, `German(de)`) y haga clic en **Listo**. Puede especificar varias configuraciones regionales. El formulario se traduce a todas las configuraciones regionales especificadas en el campo **Idiomas de destino**.
1. En el cuadro de diálogo Diccionario agregado, haga clic en **Abrir proyectos**. En la pantalla Proyectos, abra el proyecto recién creado.
1. Haga clic en los **puntos suspensivos** que aparecen en la parte inferior del mosaico **Resumen de la traducción**. Se abre la pantalla Resumen de la traducción.
1. Haga clic en el icono **Editar** que aparece en la parte superior de la pantalla **Resumen de la traducción**. Abra la pestaña **Traducción** y seleccione Traducción automática en la pantalla **Método de traducción**. Seleccione el **Proveedor de traducción** y la **Configuración en la nube** adecuados. Haga clic en el icono **Listo** que aparece en la parte superior de la pantalla.
1. En el mosaico **Trabajo de traducción**, haga clic en el icono ![aem62forms_downarrow](assets/aem62forms_downarrow.png) y luego haga clic en **Iniciar**. El estado del mosaico cambia a Borrador. Al finalizar la traducción, el estado cambia a **Listo para revisión**. Actualice la página después de unos minutos y verifique el estado.
1. Una vez que el estado haya cambiado a **Listo para revisión** en el mosaico **Trabajo de traducción**, abra el formulario en una ventana del explorador. Se muestra una versión localizada del formulario.

   >[!NOTE]
   >
   >* Antes de abrir la versión localizada del formulario en la ventana del explorador, asegúrese de que la configuración regional del explorador esté establecida de forma que coincida con la configuración regional del formulario. Por ejemplo, si el formulario se traduce al alemán (de), establezca la configuración regional del explorador en alemán (de).
   >* Los componentes de un formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL), por ejemplo, hebreo.

   Junto con el formulario adaptable, también se localiza el documento de registro generado automáticamente.

   Para obtener más información sobre la configuración y las opciones del documento de registro, consulte:

[Configuración de la plantilla de un documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[Configuración del documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [Personalice la información de marca del documento de registro](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) y asegúrese de que la configuración regional del explorador está establecida en el mismo idioma en el que ha localizado el formulario adaptable mediante lenguaje de máquina. La configuración regional del explorador ayuda a localizar la información de marca en el documento de registro.
1. Para ver el documento de registro localizado, seleccione Generar previsualización. El PDF del documento de registro se genera y abre en una nueva pestaña del explorador.

## Localizar un formulario adaptable y su documento de registro mediante traducción humana {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

En la traducción humana, el contenido se envía a su proveedor de traducción y lo traducen traductores profesionales. Cuando se completa, el contenido traducido se devuelve e importa en AEM. Cuando el proveedor de traducción está integrado con AEM, el contenido se envía automáticamente a AEM y al proveedor de traducción.

Para la traducción, un diccionario que contiene archivos en formato XLIFF se comparte con los traductores profesionales. El diccionario incluye un archivo XLIFF independiente para cada configuración regional. Cada archivo XLIFF contiene texto que se mostrará a los usuarios finales y marcadores de posición para el texto localizado correspondiente.

Realice los siguientes pasos para localizar un formulario y su documento de registro mediante traductores humanos:

1. [Conectar AEM con su proveedor de servicios de traducción](/help/sites-administering/tc-tic.md) y [crear configuraciones del marco de trabajo de integración de traducción](/help/sites-administering/tc-tic.md).

1. [Asociar las páginas del maestro de idioma](/help/sites-administering/tc-tic.md) con el servicio de traducción y las configuraciones del marco de trabajo.

1. [Identificar el tipo de contenido](/help/sites-administering/tc-rules.md) para traducir.

1. [Preparar el contenido para su traducción](/help/sites-administering/tc-prep.md) creando el maestro de idioma y las páginas raíz de las copias de idioma.

1. [Crear proyectos de traducción](/help/sites-administering/tc-manage.md) para recopilar el contenido que se va a traducir y para preparar el proceso de traducción.

1. Utilizar los proyectos de traducción para [administrar el proceso de traducción de contenido](/help/sites-administering/tc-manage.md).

>[!NOTE]
>
>* Los componentes de un formulario adaptable no admiten los lenguajes de derecha a izquierda (RTL), por ejemplo, hebreo.
>
