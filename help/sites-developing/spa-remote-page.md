---
title: El componente RemotePage
description: El componente RemotePage es un componente de página personalizado para editar el SPA de React remoto en AEM.
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
source-git-commit: cd23626858b9061228718a0455c8dd0812de92b3
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

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

## Requisitos  {#requirements}

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

* El componente RemotePage espera que la implementación proporcione un manifiesto de recurso como el que se encuentra aquí [.](https://github.com/shellscape/webpack-manifest-plugin) Sin embargo, el componente RemotePage solo se ha probado para que funcione con el marco de React (y Next.js a través del componente remote-page-next) y, por lo tanto, no admite la carga remota de aplicaciones desde otros marcos, como Angular.
* El CSS interno definido en el archivo HTML raíz de la aplicación y el CSS en línea en el nodo DOM raíz no estarán disponibles cuando se realice el procesamiento remoto en AEM.

## Detalles técnicos {#technical-details}

Al igual que el resto del proyecto de la SPA de AEM, el componente RemotePage es de código abierto. Para obtener todos los detalles técnicos del componente RemotePage, [consulte el repositorio de GitHub.](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
