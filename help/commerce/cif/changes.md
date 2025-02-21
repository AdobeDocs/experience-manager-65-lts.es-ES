---
title: Cambios importantes del complemento de Commerce integration framework (CIF)
description: Cambios importantes del complemento de Commerce integration framework (CIF) en comparación con las versiones de CIF anteriores.
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Cambios importantes en el complemento de Commerce integration framework (CIF){#notable-changes}

Este documento destaca las importantes diferencias entre el complemento de Commerce integration framework (CIF) y las versiones de CIF antiguas, conocidas principalmente como CIF Classic (Quickstart) y CIF Open-source.

## Instalación y actualizaciones

El paquete de complementos de AEM CIF se instala y actualiza con el Administrador de paquetes de AEM.

**Versiones anteriores de CIF**

* CIF Classic: no se necesita instalación, CIF formaba parte de Quickstart. Las actualizaciones de CIF formaban parte de las actualizaciones regulares de AEM o del Service Pack
* CIF Open-source: instalación mediante GitHub. Las actualizaciones formaban parte del trabajo de actualización/mantenimiento manual.

## Configuración de extremo

El extremo se configura mediante la consola OSGi.

**Versiones anteriores de CIF**

* CIF Classic: mediante la configuración OSGi en AEM
* CIF Open-source: A través del Explorador de configuración de CIF

## Implementación del proyecto Venia de CIF

Proyecto disponible en [GitHub AEM Guides - Proyecto CIF Venia](https://github.com/adobe/aem-cif-guides-venia) e implementación realizada a través del Administrador de paquetes de AEM.

**Versiones anteriores de CIF**

* CIF Classic: mediante la instalación de paquetes de AEM

## Datos del catálogo de productos

Los datos del catálogo de productos se solicitan bajo demanda mediante llamadas en tiempo real a un extremo externo que admite las API de GraphQL requeridas. Estas API admiten el acceso a datos activos o clasificados en cualquier fecha determinada. No se necesita replicación.

**Versiones anteriores de CIF**

* CIF Classic: los datos de productos en directo y clasificados se importan y persisten en JCR en AEM Author mediante la importación completa o delta de productos. Los datos del producto activos se replican en AEM Publish.

## Experiencias del catálogo de productos con procesamiento en AEM

AEM procesa experiencias de catálogo de productos sobre la marcha mediante plantillas de catálogo de AEM que se han asignado a productos y categorías. No se necesita replicación.

**Versiones anteriores de CIF**

* CIF Classic: el autor de AEM crea una página de AEM para cada categoría o producto mediante la herramienta de modelo de catálogo. Estas páginas se replican en AEM Publish.

>[!NOTE]
>
>Para obtener documentación adicional sobre cómo usar CIF con AEM Managed Service o AEM On-Premise, consulte [Commerce integration framework](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
