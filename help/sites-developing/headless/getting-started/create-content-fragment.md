---
title: Guía de inicio rápido Creación de fragmentos de contenido sin encabezado
description: Aprenda a utilizar fragmentos de contenido de AEM para diseñar, crear, depurar y utilizar contenido independiente de las páginas para una entrega sin encabezado.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
exl-id: 7b26e5cb-3aab-4f69-a0f1-42268c39bba8
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 73%
---
# Guía de inicio rápido Creación de fragmentos de contenido sin encabezado {#creating-content-fragments}

Aprenda a utilizar fragmentos de contenido de AEM para diseñar, crear, depurar y utilizar contenido independiente de las páginas para una entrega sin encabezado.

## ¿Qué son los fragmentos de contenido? {#what-are-content-fragments}

[Ahora que ha creado una carpeta de recursos](create-assets-folder.md) donde puede almacenar los fragmentos de contenido, puede crear los fragmentos.

Los fragmentos de contenido permiten diseñar, crear, depurar y publicar contenido independiente de cualquier página. Permiten preparar contenido listo para su uso en varias ubicaciones y en varios canales.

Los fragmentos de contenido contienen contenido estructurado y se pueden entregar en formato JSON.

## Cómo crear un fragmento de contenido {#how-to-create-a-content-fragment}

Los autores de contenido generarán el número de fragmentos de contenido que corresponda para representar el contenido que crean. Esta será su tarea principal en AEM. Para los fines de esta guía de introducción, solo necesitamos crear uno.

1. Inicie sesión en AEM y, en el menú principal, seleccione **Navegación > Assets**.
1. Vaya a la [carpeta que creó anteriormente.](create-assets-folder.md)
1. Haga clic en **Crear > Fragmento de contenido**.
1. La creación de un fragmento de contenido se presenta como un asistente en dos pasos. Seleccione primero qué modelo desea utilizar para crear el fragmento de contenido y haga clic en **Siguiente**.
   * Los modelos disponibles dependen de la [**Configuración de nube** que definió para la carpeta de recursos](create-assets-folder.md) en el que está creando el fragmento de contenido.
   * Si recibe el mensaje `We could not find any models`, compruebe la configuración de la carpeta de recursos.

   ![Selección del modelo de fragmentos de contenido](assets/content-fragment-model-select.png)
1. Proporcione un **Título**, **Descripción** y **Etiquetas** según sea necesario y haga clic en **Crear**.

   ![Creación de un fragmento de contenido](assets/content-fragment-create.png)
1. Haga clic en **Abrir** en la ventana de confirmación.

   ![Confirmación de fragmento de contenido creado](assets/content-fragment-confirmation.png)
1. Proporcione los detalles del fragmento de contenido en el Editor de fragmentos de contenido.

   ![Editor de fragmentos de contenido](assets/content-fragment-edit.png)
1. Haz clic en **Guardar** o en **Guardar y cerrar**.

Los fragmentos de contenido pueden hacer referencia a otros fragmentos de contenido, lo que permite anidar una estructura de contenido si es necesario.

Los fragmentos de contenido también pueden hacer referencia a otros recursos en AEM. [Estos recursos deben almacenarse en AEM](/help/assets/manage-assets.md) antes de crear una referencia a un fragmento de contenido.

## Siguientes pasos {#next-steps}

Ahora que ha creado un fragmento de contenido, puede pasar a la parte final de la guía de introducción y [crear solicitudes de API para acceder y entregar fragmentos de contenido.](create-api-request.md)

>[!TIP]
>
>Para obtener información detallada acerca de la administración de fragmentos de contenido, consulte la [Documentación de fragmentos de contenido](/help/assets/content-fragments/content-fragments.md)
