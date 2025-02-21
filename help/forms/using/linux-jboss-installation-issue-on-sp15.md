---
title: Problema de instalación del Service Pack 6.5.15.0 de AEM Forms JEE en el entorno JBoss® Linux®
description: El Service Pack 6.5.15.0 de AEM Forms JEE no está instalado correctamente en el entorno JBoss® Linux®, los cambios de parche no se aplican al servidor de aplicaciones. Añada el archivo RUP_BOM.xml al directorio XML.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---

# Problema de instalación del paquete de servicio JEE de AEM Forms 6.5.15.0 en el entorno JBoss® {#aem-forms-installation-issue-environment}

## Problema {#issue}

El Service Pack 6.5.15.0 de AEM Forms JEE no está instalado correctamente en el entorno JBoss® Linux®. En el archivo `PatchInstallerProcessing[1-9*].log`, la entrada de registro `[AEM_Forms_JEE_DIR]/patch/AEMForms-6.5.0-0057/xml/RUP_BOM.xml not found! Assuming this component is not in the installation. Skipping Processing` está registrada. Esta entrada indica que la instalación del Service Pack 6.5.15.0 de AEM Forms JEE no se ha realizado correctamente.

## Se aplica a {#applies-to}

Esta solución se aplica a:
* Entorno JBoss® Linux®

>[!NOTE]
>
> Asegúrese de que el Service Pack 6.5.15.0 de AEM Forms JEE esté instalado en el servidor de aplicaciones al menos una vez antes de realizar los pasos de [agregar el archivo RUP_BOM.xml al directorio XML](#solution-solution).

## Solución {#solution}

Para solucionar el problema de instalación del Service Pack de AEM Forms JEE 6.5.15.0, agregue el archivo `RUP_BOM.xml` al directorio XML:
1. Vaya a la carpeta donde extrajo el parche `AEMForms-6.5.0-0057_jboss_linux.tar.gz`.
1. Vaya a la ubicación `/CDROM_Installers/Linux/Disk1/InstData` y busque el archivo `Resource1.zip`.
1. Copie el archivo `Resource1.zip` en otra ubicación fuera de la carpeta extraída y descomprima el archivo `Resource1.zip`.
1. Vaya a `/C_/builds/dev_releng/branches/rrt/aem6.5.0_rollup/tier1/install/patch/fileset_dir/xml` y copie el archivo `RUP_BOM.xml`.
1. Pegue el archivo RUP_BOM.xml en `[aem_forms_jee_installation_dir]/patch/AEMForms-6.5.0-0057/xml`.
1. Vuelva a instalar el [Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) de AEM Forms JEE 6.5.15.0.
