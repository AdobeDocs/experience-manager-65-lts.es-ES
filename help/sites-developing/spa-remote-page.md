---
title: El componente RemotePage
description: El componente RemotePage es un componente de página personalizado para editar el SPA de React remoto en AEM.
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: 9c8dff52-3860-4f71-a0d9-993574f1d654
index: false
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: a9f7d31e-bbe1-4475-966a-5f213546fcd9
    internal-label: SPA Editor
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%
---

# El componente RemotePage {#remote-page-component}

Al decidir qué nivel de integración desea tener entre su SPA externo y AEM, a menudo está claro que necesita poder ver y editar la SPA dentro de AEM. El componente RemotePage es un componente de página personalizado solo para este propósito.

## Información general {#overview}

El componente RemotePage obtiene todos los recursos necesarios del `asset-manifest.json` generado por la aplicación y lo utiliza para procesar el SPA en AEM.

* RemotePage permite insertar los scripts y las hojas de estilo de una SPA en el cuerpo de un componente de página de AEM.
* Los componentes de front-end virtuales le permiten marcar secciones como editables en el Editor de SPA de AEM.
* Juntos, un SPA alojado en un dominio diferente se puede hacer editable en AEM.

Consulte el artículo [Edición de un SPA externo en AEM](spa-edit-external.md) para obtener más información sobre los SPA externos editables en AEM.

{{ue-over-spa}}

## Requisitos {#requirements}

* Habilitar CORS en desarrollo
* Configurar URL remota en Propiedades de página
* Procesar el SPA en AEM
* La aplicación web debe utilizar un manifiesto de recurso de paquete como uno de los siguientes y exponer un archivo asset-manifest.json en la raíz del dominio que enumera en una propiedad de puntos de entrada todos los archivos CSS y JS que se van a cargar:
  * https://github.com/shellscape/webpack-manifest-plugin
  * https://github.com/webdeveric/webpack-assets-manifest
  * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

  ![Puntos de entrada](assets/asset-manifest-entrypoints.png)

* La aplicación debe poder inicializarse en un(a) `<div id="root"></div>` debajo del elemento body. Si se espera un marcado diferente para que la aplicación cree una instancia, esto debe ajustarse en consecuencia en los scripts HTL del componente proxy que tiene un `sling:resourceSuperType="spa-project-core/components/remotepage`.

## Limitaciones {#limitations}

* El componente RemotePage espera que la implementación proporcione un manifiesto de recurso como el que se encuentra [aquí.](https://github.com/shellscape/webpack-manifest-plugin) Sin embargo, el componente RemotePage solo se ha probado para que funcione con el marco de React (y Next.js a través del componente remote-page-next) y, por lo tanto, no admite la carga remota de aplicaciones desde otros marcos, como Angular.
* El CSS interno definido en el archivo HTML raíz de la aplicación y el CSS en línea en el nodo DOM raíz no estarán disponibles cuando se realice el procesamiento remoto en AEM.

## Detalles técnicos {#technical-details}

Al igual que el resto del proyecto de la SPA de AEM, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
