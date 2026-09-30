---
title: Administración de puntos de conexión de GraphQL en AEM
description: Obtenga información sobre cómo administrar los extremos de GraphQL en Adobe Experience Manager para la entrega de contenido sin encabezado.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
exl-id: 13a2e067-878f-4580-9d7f-cfb3237a335d
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
source-wordcount: '510'
ht-degree: 91%
---
# Administración de puntos de conexión de GraphQL en AEM {#graphql-aem-endpoint}

El punto de conexión es la ruta utilizada para acceder a GraphQL para AEM. Al utilizar esta ruta, usted (o su aplicación) puede hacer lo siguiente:

* acceder al esquema de GraphQL,
* enviar sus consultas de GraphQL,
* recibir las respuestas (a sus consultas de GraphQL).

Hay dos tipos de puntos de conexión en AEM:

* Globales
  * Disponibles para su uso en todos los sitios.
  * Este punto de conexión puede utilizar todos los modelos de fragmento de contenido de todas las configuraciones de sitios (definidas en el [Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)).
  * Si hay algún modelo de fragmento de contenido que debería compartirse entre las configuraciones de Sites, estos deberían crearse en las configuraciones globales de Sites.
* Configuraciones de Sites:
  * Corresponde a una configuración de Sites, tal como se define en el [Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
  * Específico de un sitio o proyecto concreto.
  * Un punto de conexión específico de la configuración de Sites usará los modelos de fragmento de contenido de esa configuración de Sites específica junto con los de la configuración de Sites global.

>[!CAUTION]
>
>El editor de fragmentos de contenido puede permitir que un fragmento de contenido de una configuración de Sites haga referencia a un fragmento de contenido de otra configuración de Sites (a través de políticas).
>
>En tal caso, no todo el contenido se podrá recuperar mediante un punto de conexión específico de configuración de Sites.
>
>El autor del contenido debe controlar este escenario; por ejemplo, puede resultar útil considerar la posibilidad de colocar los modelos de fragmento de contenido compartido en la configuración de Sites global.

La ruta del repositorio del punto de conexión global de GraphQL para AEM es la siguiente:

`/content/cq:graphql/global/endpoint`

Para lo cual su aplicación puede utilizar la siguiente ruta en la dirección URL de la solicitud:

`/content/_cq_graphql/global/endpoint.json`

Para habilitar un punto de conexión para GraphQL para AEM, debe hacer lo siguiente:

* [Habilitar el punto de conexión de GraphQL](#enabling-graphql-endpoint)
* [Publicar el punto de conexión de GraphQL](#publishing-graphql-endpoint)

## Habilitación del punto de conexión de GraphQL {#enabling-graphql-endpoint}

Para habilitar un punto de conexión de GraphQL, primero debe tener una configuración adecuada. Consulte [Fragmentos de contenido: explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>Si [no se ha habilitado el uso de modelos de fragmentos de contenido](/help/assets/content-fragments/content-fragments-configuration-browser.md), la opción **Crear** no estará disponible.

Para habilitar el punto de conexión correspondiente:

1. Vaya a **Herramientas**, **Assets** y, a continuación, seleccione **GraphQL**.
1. Seleccione **Crear**.
1. Se abre el cuadro de diálogo **Crear nuevo punto final de GraphQL**. Aquí puede especificar lo siguiente:
   * **Nombre**: nombre del punto de conexión; puede escribir cualquier texto.
   * **Utilice el esquema GraphQL proporcionado por**: utilice la lista desplegable para seleccionar el sitio o proyecto requerido.

   >[!NOTE]
   >
   >La siguiente advertencia se muestra en el cuadro de diálogo:
   >
   >* *Los puntos finales de GraphQL pueden introducir problemas de rendimiento y seguridad de datos si no se administran con cuidado. Asegúrese de establecer los permisos adecuados después de crear un extremo.*

1. Confirme con **Crear**.
1. El diálogo **Pasos siguientes** proporciona un vínculo directo a la consola de seguridad para que pueda cerciorarse de que el punto de conexión recién creado tenga los permisos adecuados.

   >[!CAUTION]
   >
   >El punto de conexión es accesible para todos. Esto puede suponer un problema de seguridad, especialmente en las instancias de publicación, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
   >
   >Puede configurar ACL, según su caso de uso, en el punto de conexión.

## Publicación del punto de conexión de GraphQL {#publishing-graphql-endpoint}

Seleccione el nuevo punto de conexión y **Publicación** para que esté totalmente disponible en todos los entornos.

>[!CAUTION]
>
>El punto de conexión es accesible para todos.
>
>En instancias de publicación esto puede suponer un problema de seguridad, ya que las consultas de GraphQL pueden imponer una carga pesada en el servidor.
>
>Configure ACL adecuados para su caso de uso en el punto de conexión.
