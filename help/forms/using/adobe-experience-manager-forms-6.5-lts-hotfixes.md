---
title: Revisiones de Adobe Experience Manager Forms 6.5 LTS SP1
description: Proporciona información sobre cómo descargar e instalar una revisión para AEM Forms 6.5 LTS.
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 504240bdad9e964460a9fcdc555228c7cb02e314
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 45%

---


# Revisiones de Adobe Experience Manager Forms 6.5 LTS{#aem-form-hotfix}

Este artículo enumera las correcciones esenciales implementadas para solucionar problemas conocidos, mejorar la estabilidad del sistema y mejorar el rendimiento general de AEM Forms 6.5 LTS.

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
