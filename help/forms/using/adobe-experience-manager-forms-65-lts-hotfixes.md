---
title: Revisiones de Adobe Experience Manager Forms 6.5 LTS
description: Proporciona información sobre cómo descargar e instalar una revisión para AEM Forms 6.5 LTS. Para AEM 6.5 (no LTS), consulte el artículo Revisiones de AEM 6.5 Forms.
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: e485100f-3e16-4fd4-a8ce-af771d765dd1
source-git-commit: 989d83cfc56f7a7d4e2aea5a7ac1ca444d505859
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 11%
---
# Revisiones de Adobe Experience Manager Forms 6.5 LTS{#aem-form-hotfix}

Este artículo enumera las correcciones esenciales implementadas para solucionar problemas conocidos, mejorar la estabilidad del sistema y mejorar el rendimiento general de AEM Forms 6.5 LTS.


Este artículo se aplica a AEM Forms 6.5 LTS. Para implementaciones de AEM 6.5 (no LTS), consulte [Revisiones de Adobe Experience Manager Forms](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/release-notes/aem-forms-hotfix).

>[!NOTE]
>
> Las revisiones están diseñadas para ser acumulativas e incluyen todas las correcciones anteriores. Al aplicar la revisión más reciente a una versión, no solo se aborda el problema más reciente, sino que también incorpora todas las correcciones de errores y mejoras anteriores.

## Revisiones para AEM Forms 6.5 LTS {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Fecha</strong></td>
    <td><strong>Vínculo de descarga de revisión (vínculo de distribución de software de AEM)</strong></td>
    <td><strong>Problemas solucionados</strong></td>
  </tr>
  <tr>
    <td>
      <strong>21 de septiembre de 2026</strong><br>
      <em>Se aplica a:</em> implementaciones JEE del paquete de servicio 2 de AEM Forms 6.5 LTS (JBoss, WebLogic, WebSphere)<br>
    </td>
    <td>
    <p><strong>Para instalar esta revisión, complete estos pasos en orden:</strong></p>
    <p><strong>Paso 1: Instalar el parche</strong></p>
    <ul>
    <strong>JBoss:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-jboss.zip">revisión para AEM Forms 6.5 LTS SP2 en Windows para el servidor JEE de JBoss</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-jboss.tar.gz">revisión para AEM Forms 6.5 LTS SP2 en Linux para el servidor JEE de JBoss</a></li>
    <strong>WebLogic:</strong>
    <li>Windows: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-weblogic.zip">revisión para AEM Forms 6.5 LTS SP2 en Windows para el servidor JEE de Weblogic</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-weblogic.tar.gz">revisión para AEM Forms 6.5 LTS SP2 en Linux para el servidor JEE de Weblogic</a></li>
    <strong>WebSphere:</strong>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-websphere.zip">Revisión para AEM Forms 6.5 LTS SP2 en Windows para el servidor JEE de Websphere</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-websphere.tar.gz">revisión para AEM Forms 6.5 LTS SP2 en Linux para el servidor JEE de Websphere</a></li>
    </ul>
    <p>Instale el parche mediante el procedimiento de instalación del parche estándar de AEM Forms en JEE. <!-- TODO: link to the 6.5 LTS JEE patch installation instructions once available --></p>
    <p><strong>Paso 2: Instalar el paquete de corrección de vulnerabilidades</strong></p>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/SP2LTSBundles_VULN-36670.zip">Paquete de correcciones de vulnerabilidades para AEM Forms 6.5 LTS SP2</a></li>
    </ul>
    <ol>
    <li>Abra la consola OSGi en <code>http://&lt;host&gt;:&lt;port&gt;/lc/system/console/bundles</code>.</li>
    <li>Haga clic en <strong>Instalar/actualizar</strong>.</li>
    <li>Seleccione las casillas de verificación <strong>Iniciar paquete</strong> y <strong>Actualizar paquetes</strong>.</li>
    <li>Haga clic en <strong>Elegir archivo</strong> y, a continuación, cargue el paquete descargado.</li>
    <li>Espere hasta que el registro se establezca y el paquete se muestre como <strong>Activo</strong>.</li>
    </ol>
    <p><strong>Paso 3: Actualización del instalador de AEM Forms Workbench</strong></p>
    <p>Debe actualizar al instalador de AEM Forms Workbench más reciente. Descárguelo del <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/fd/workbench/6-5-0-20260902-1-45/Workbench_DVD.zip">instalador de AEM Forms Workbench</a>.</p>
    <p><strong>Paso 4: Actualización de archivos de biblioteca de cliente (desarrolladores)</strong></p>
    <p>Este parche incluye una actualización importante de la biblioteca de cliente de SDK <code>adobe-livecycle-client.jar</code> (consulte <a href="/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files">Inclusión de archivos de biblioteca Java de AEM Forms</a>). Si el proyecto usa este archivo JAR, actualice <code>adobe-livecycle-client.jar</code> en la ruta de clase del proyecto después de instalar la revisión. La versión más reciente está disponible en <code>&lt;AEM_Forms_Installation_dir&gt;\sdk\client-libs\common\adobe-livecycle-client.jar</code>.</p>
    <p>La revisión es acumulativa, por lo que puede aplicarla en AEM Forms 6.5 LTS Service Pack 2 o en un Service Pack anterior sin instalar primero el Service Pack 2.</p>
    </td>
    <td>
    <ul>
    <li><b>FORMS-26818</b> Después de actualizar Apache Shiro a la versión 2.1.0, AEM Forms en JEE no arranca con <code>NoClassDefFoundError</code> para el administrador de seguridad de Shiro. Esta revisión restaura el arranque correcto.</li>
    <li><b>FORMS-26819</b> AEM Forms en JEE falla con el error "no se encontró la clase" para <code>org.owasp.esapi.reference.JavaLogFactory</code>. Esta revisión resuelve la clase que falta.</li>
    <li><b>FORMS-26584, FORMS-26589</b> Después de actualizar a AEM Forms 6.5 LTS, se quitan los extremos de TaskManager. Esta revisión restaura los extremos de TaskManager.</li>
    <li><b>FORMS-26569</b> En JEE, el paso MergeEars del Administrador de configuración falla con un error de declaración DOCTYPE (<code>ALC-LCM-010-200</code>) debido al generador de XML seguro. Este hotfix permite completar el paso MergeEars.</li>
    <li>Faltan <b>FORMS-25063</b> registros de nivel de aplicación en las implementaciones de IBM WebSphere Liberty. Esta revisión restaura el registro en el nivel de aplicación.</li>
    <li><b>FORMS-24892</b> En JBoss, el correo electrónico falla con "IMAPProvider no es un subtipo". Esta revisión restaura la funcionalidad de correo electrónico en JBoss.</li>
    <li><b>FORMS-24692</b> En el perfil Liberty de WebSphere (WLP), el correo electrónico produce el error "No se pudo convertir el socket a TLS". Esta revisión restaura el correo electrónico a través de TLS en WLP.</li>
    <li><b>FORMS-26688</b> actualiza la biblioteca Gibson a la versión 6.0.29665850.</li>
    <li><b>FORMS-25222</b> respalda las mejoras de validación de aserción de SAML.</li>
    <li><b>FORMS-26733, FORMS-26734</b> Se ha actualizado Apache Log4j a la versión 2.25.5.</li>
    <li>Este hotfix también incluye correcciones de seguridad.</li>
    </ul>
    <p><strong>Compilación:</strong> AEMForms-6.6.0-0008</p>
    </td>
  </tr>
  <tr>
    <td>
      <strong>9 de septiembre de 2025</strong><br>
    <td>
    <ul>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Revisión2 para AEM Service Pack 6.5 LTS en Windows</a></li>
    <li>Linux: <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]revisión-en-complemento/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">revisión2 para AEM Service Pack 6.5 LTS en Linux</a></li>
     <li>MacOS- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">revisión2 para AEM Service Pack 6.5 LTS en MacOS</a></li>
    <td>
    <ul>
    <li>Se ha mejorado la fiabilidad del envío de formularios al solucionar un problema en el que los envíos pueden fallar cuando la validación del lado del servidor (SSV) está habilitada. Si tiene algún problema, póngase en contacto con el [Soporte técnico de Adobe Experience Manager Forms] (https://business.adobe.com/in/support/main.html).
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## Descargar e instalar una revisión de OSGi {#download-install-hotfix}

Realice los siguientes pasos para descargar e instalar la revisión:

1. Descargue la [revisión](#hotfix-for-adaptive-forms) mediante el vínculo de distribución de software.
1. Extraiga el archivo de revisión para poder obtener un paquete Experience Manager (.zip) y archivos de paquete (.jar).
1. Cargue e instale el paquete (.zip) mediante el [Administrador de paquetes](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Abra los paquetes del administrador de configuración `https://server:host/system/console/bundles`, cargue e instale el paquete (.jar). La revisión está instalada.
