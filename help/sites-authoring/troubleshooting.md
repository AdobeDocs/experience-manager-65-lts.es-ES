---
title: Solución de problemas al crear en AEM
description: Algunos problemas que pueden producirse al utilizar AEM.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
exl-id: 1e735d57-834a-4251-9b92-ccc6d4712f2a
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 39%
---
# Resolución de problemas de AEM durante la creación{#troubleshooting-aem-when-authoring}

La sección siguiente trata ciertos problemas que pueden producirse al utilizar AEM, así como sugerencias para solucionarlos.

>[!NOTE]
>
>Cuando tenga problemas, también vale la pena comprobar la lista de [Problemas conocidos](/help/release-notes/release-notes.md) de su instancia (versiones y paquetes de servicio).

>[!NOTE]
>
>Los usuarios con privilegios de administrador y que deseen solucionar problemas con AEM pueden utilizar los métodos de solución de problemas descritos en [Solución de problemas de AEM (para administradores)](/help/sites-administering/troubleshoot.md). Si no tiene privilegios suficientes, póngase en contacto con el administrador del sistema para solucionar los problemas de AEM.

## La versión anterior de la página sigue en el sitio publicado {#old-page-version-still-on-published-site}

* **Problema**:

  * Ha realizado cambios en una página y replicado la página en el sitio de publicación, pero la versión *antigua* de la página se sigue mostrando en el sitio de publicación.

* **Motivo**:

  * Esto puede tener varias causas, la mayoría de las veces la memoria caché (el explorador local o el Dispatcher), aunque a veces puede ser un problema con la cola de replicación.

* **Soluciones**:

  * Aquí hay varias posibilidades:
  * Confirme que la página se ha duplicado correctamente. Compruebe el estado de la página y, si es necesario, el estado de la cola de replicación.
  * Borre la caché del navegador local y vuelva a acceder a la página.
  * Agregar `?` al final de la dirección URL de la página. Por ejemplo:

    * `http://localhost:4502/sites.html/content?`
    * Esta acción solicitará la página directamente desde AEM y omitirá a Dispatcher. Si recibe la página actualizada quiere decir que debe borrar la caché de Dispatcher.

  * Póngase en contacto con el administrador del sistema si hay problemas con las colas de replicación.

## Acciones aplicables a los componentes no visibles en la barra de herramientas {#component-actions-not-visible-on-toolbar}

* **Problema**:

  * La gama completa de acciones aplicables a los componentes no aparece visible al editar una página de contenido en el entorno de creación.

* **Motivo**:

  * En casos excepcionales, una acción anterior podría afectar a la barra de herramientas.

* **Solución**:

  * Actualice la página.
