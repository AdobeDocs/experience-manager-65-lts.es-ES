---
title: Depurar formularios HTML5
description: Los pasos de la lista de documentos para solucionar varios problemas conocidos.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 93%

---

# Depurar formularios HTML5 {#debugging-html-forms}

Este documento incluye varios casos de resolución de problemas. Para cada escenario, se proporcionan algunos pasos para solucionar el problema. Sígalos y, si el problema persiste, configure el registrador para obtener y revisar los registros en busca de errores/advertencias. Para obtener más información sobre el registro de formularios HTML5, consulte [Generar registros para formularios HTML5](/help/forms/using/enable-logs.md).

## Problema: Al procesar el formulario, veo la página de excepciones org.apache.sling.api.SlingException {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

En los detalles de la excepción, busque **causado por**.

Probablemente, el motivo es que uno o más parámetros de la dirección URL sean incorrectos.

Compruebe los siguientes parámetros:

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>plantilla</td>
   <td>El nombre de archivo de la plantilla</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>La ruta donde residen la plantilla y los recursos asociados</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Ruta absoluta del archivo de datos que se combina con la plantilla.<br /> Nota: La ruta define la ruta absoluta del archivo de datos.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de datos codificados UTF-8 que se combinan con la plantilla.</td>
  </tr>
 </tbody>
</table>

## Problema: No se puede procesar un formulario (se muestra un mensaje de error) {#problem-unable-to-render-form}

1. Asegúrese de que los parámetros especificados sean correctos. Para obtener información detallada sobre los parámetros, consulte [Parámetros de procesamiento](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. Inicie sesión en el Administrador de paquetes de CRX (en https://&lt;server>:&lt;port>/crx/packmgr/index.jsp) y compruebe si los siguientes paquetes están instalados correctamente:

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. Inicie sesión en la consola web de CQ (Consola Felix) en https://&lt;server>:&lt;port>/system/console/bundles.

   Asegúrese de que el estado de los siguientes paquetes sea “habilitado”.

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * Procesador de formularios XFA de Adobe

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Conector de formularios XFA LC de Adobe

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## Problema: El formulario se procesa sin estilos {#problem-form-renders-without-styles}

1. En el explorador, abra **Herramientas para desarrolladores**. Asegúrese de que profile.css esté disponible.
1. Si el archivo profile.css no está disponible, inicie sesión en CRX DE en https://&lt;server>:&lt;port>/crx/de.
1. En la jerarquía de carpetas de la izquierda, navegue hasta /etc/clientlibs/fd/xfaforms/. Abra los archivos css.txt que aparecen en las carpetas.

   * perfil
   * tiempo de ejecución
   * scrollnav
   * barra de herramientas
   * xfalib

1. Compruebe que los archivos mencionados dentro de css.txt estén presentes en CRX DE lite en /libs/fd/xfaforms/clientlibs/xfalib/css.

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. Si los archivos mencionados no están disponibles, instale de nuevo el paquete adobe-lc-forms-runtime-pkg-&lt;version>.zip

### Problema: Error inesperado {#problem-unexpected-error-encountered}

1. En la dirección URL del formulario, agregue el parámetro de consulta debugClientLibs y establezca su valor en true (Por ejemplo: https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path>&amp;template=&lt;name of xdp file>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. En un navegador de escritorio, como Chrome, vaya a Herramientas para desarrolladores > Consola.
1. Abra los registros para identificar el tipo de error. Para obtener información detallada sobre los registros, consulte [registros para formularios HTML5](/help/forms/using/enable-logs.md).
1. Vaya a Herramientas para desarrolladores > Consola. Utilice el seguimiento en pila para localizar el código que causa el error. Depure el error para resolver el problema.

   >[!NOTE]
   >
   >Si se trata de un error de script, compruebe si el mismo problema se produce durante la representación del formulario PDF. Si es así, hay un problema en la lógica del script del formulario.

## Problema: No se puede enviar el formulario {#problem-unable-to-submit-the-form}

1. Asegúrese de que tiene derechos para acceder al servidor de AEM y de que está conectado al servidor.
1. Compruebe que el parámetro submitUrl sea correcto.
1. Habilite los registros del lado del cliente como se menciona en [Registros para formularios HTML5](/help/forms/using/enable-logs.md) usar la opción depurar como **1-a5-b5-c5**. A continuación, procese el formulario y haga clic en enviar. Abra la consola de depuración del explorador y compruebe si hay algún error.
1. Localice los registros del servidor como se menciona en [Registros para formularios HTML5](/help/forms/using/enable-logs.md). Compruebe si ocurrió algún error en los registros del servidor durante el envío.

## Problema: No se muestran los mensajes de error localizados {#problem-localized-error-messages-do-not-display}

1. Procese el formulario con un parámetro de consulta adicional **debugClientLibs=true** en el explorador de escritorio y, a continuación, vaya a Herramientas para desarrolladores > Recursos y busque el archivo I18N.css.
1. Si el archivo no está disponible, inicie sesión en CRX DE en https://&lt;server>:&lt;port>/crx/de.
1. En la jerarquía de carpetas de la izquierda, navegue hasta /libs/fd/xfaforms/clientlibs/I18N y asegúrese de que existan los siguientes archivos y carpetas:

   * Namespace.js
   * LogMessages.js
   * Carpetas para idiomas

1. Si alguno de los archivos o carpetas anteriores no existe, instale de nuevo el paquete **adobe-lc-forms-runtime-pkg-&lt;version>.zip**.
1. Navegue hasta la carpeta que tiene el mismo nombre que la configuración regional y compruebe su contenido. La carpeta debe contener los siguientes archivos:

   * I18N.js
   * js.txt

1. Compruebe el contenido de js.txt y asegúrese de que tiene las siguientes entradas.

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## Problema: La imagen no aparece {#problem-image-not-showing-up}

1. Asegúrese de que la dirección URL de la imagen sea correcta.
1. Compruebe si su explorador admite ese tipo de imagen.
1. En los detalles de la excepción, busque **causado por**.

   Probablemente, el motivo es que uno o más parámetros de la dirección URL sean incorrectos.

   Compruebe los siguientes parámetros: Texto del paso

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>plantilla</td>
   <td>El nombre de archivo de la plantilla</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>La ruta donde residen la plantilla y los recursos asociados</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>Ruta absoluta del archivo de datos que se combina con la plantilla.<br /> Nota: La ruta define la ruta absoluta del archivo de datos.</td>
  </tr>
  <tr>
   <td>data</td>
   <td>Bytes de datos codificados UTF-8 que se combinan con la plantilla.</td>
  </tr>
 </tbody>
</table>

1. En el explorador de escritorio, vaya a Herramientas para desarrolladores > Recursos.

   Compruebe si esa imagen se muestra en el lado izquierdo en Imagen.
