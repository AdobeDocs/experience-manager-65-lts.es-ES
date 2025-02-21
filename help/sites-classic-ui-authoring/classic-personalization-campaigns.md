---
title: Administración de campañas
description: La administración de campañas ofrece a los especialistas en marketing digital la oportunidad de ofrecer contenido personalizado y, por lo tanto, crear experiencias dedicadas para los visitantes. Permite organizar las campañas de marketing en la web, el correo electrónico y los servicios móviles, y así atraer a los visitantes.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Administración de campañas{#campaign-management}

La administración de campañas ofrece a los especialistas en marketing digital la oportunidad de ofrecer contenido personalizado y, por lo tanto, crear experiencias dedicadas para los visitantes.

Permite organizar las campañas de marketing en la web, el correo electrónico y los servicios móviles, y así atraer a los visitantes. Puede crear contenido, segmentar visitantes, insertar y promocionar contenido segmentado para perfiles de usuario específicos y administrar campañas en varios canales.

Este documento describe los distintos elementos que componen las campañas. Encontrará información más detallada en los siguientes documentos:

* [Teasers and Strategies](/help/sites-classic-ui-authoring/classic-personalization-campaigns-teasers-strategy.md)
* [Marketing por correo electrónico](/help/sites-classic-ui-authoring/classic-personalization-campaigns-email.md)
* [Páginas de destino](/help/sites-classic-ui-authoring/classic-personalization-campaigns-landingpage.md)
* [Ofertas de Target](/help/sites-classic-ui-authoring/classic-personalization-campaigns-target-offers.md)
* [Trabajar con el administrador de campañas de marketing](/help/sites-classic-ui-authoring/classic-personalization-campaigns-mktg-manager.md)
* [Información acerca de la segmentación](/help/sites-classic-ui-authoring/classic-personalization-campaigns-segmentation.md)
* [Configuración de la campaña](/help/sites-classic-ui-authoring/classic-personalization-campaigns-setting-up-your.md)

La administración de campañas se compone de varios elementos:

* **Marcas**
En Adobe Experience Manager (AEM), las marcas son la unidad de nivel superior y forman una colección de **Campañas**.

* **Campañas**
Una campaña es una colección de **experiencias** individuales.

* **Experiencias**
El contenido enfocado forma las distintas experiencias que se presentan al visitante en **puntos de contacto**. Hay varios tipos de experiencia disponibles:

   * **Teasers**
     [Páginas teaser / Párrafos](#teasers) se usan para dirigir a visitantes específicos **Segmentos** a contenido que se centra en sus intereses.

     Las páginas teaser pueden:

      * presentar una serie de opciones para que el visitante elija entre ellas
      * mostrar solo un párrafo de teaser basado en el segmento específico del visitante. Por ejemplo, el párrafo de teaser que se muestra puede depender de la edad del visitante.

     Normalmente, una página teaser es una acción temporal que dura un período de tiempo específico, hasta que se reemplaza por la siguiente página de teaser.

   * **Boletines**

     Las [comunicaciones por correo electrónico](#emailmarketing) se utilizan para atraer a los usuarios y animarlos a que visiten su sitio web. Suelen adoptar la forma de una newsletter, que se envía a los **posibles clientes** (que se agrupan en **Listas**). **Nota:** Adobe no planea mejorar más esta capacidad. Se recomienda [usar Adobe Campaign y la integración en AEM](/help/sites-administering/campaign.md).

   * **Adobe Target**

     Esto permite la integración con Adobe Target (anteriormente Test&amp;Target), que proporciona a los especialistas en mercadotecnia una herramienta de optimización de sitios web de conversión con las funciones necesarias para garantizar que el contenido y las ofertas en línea sean relevantes para los clientes, lo que resultará en una mayor conversión. Adobe Target proporciona una interfaz intuitiva para diseñar y ejecutar pruebas, crear segmentos de audiencia y segmentar contenido desde una sola aplicación.

* **Puntos de contacto**

  Estos son los puntos de contacto entre el visitante y la campaña. Los puntos de contacto están conectados a las experiencias que ha creado.

  Por ejemplo, para los teasers, es la página de contenido donde se encuentra el párrafo de teaser; para un boletín, es la lista de correo.

* **Posibles clientes**

  La información que ha recopilado sobre sus visitantes y cómo ponerse en contacto con ellos forma la base de sus posibles clientes. **Nota:** Adobe no planea mejorar más esta capacidad.

  Se recomienda [usar Adobe Campaign y la integración en AEM](/help/sites-administering/campaign.md).

* **Listas**

  Los posibles clientes se agrupan en listas para que pueda realizar acciones colectivas en consecuencia. Nota: **Nota:** Adobe no planea mejorar más esta capacidad.

  Se recomienda [usar Adobe Campaign y la integración en AEM.](/help/sites-administering/campaign.md)

* **Segmentos**

  Los visitantes del sitio tienen diferentes intereses y objetivos cuando llegan a un sitio. Analizar esto según factores como la actividad en el sitio web, la información de perfil registrada y la actividad en otros sitios web, le ayuda a definir segmentos. El contenido puede personalizarse según las necesidades y los intereses del visitante, según los segmentos con los que coincidan.

* **MCM**

  El Administrador de campañas de marketing (MCM) es una consola que le permite acceder a toda la funcionalidad que necesita para crear y controlar campañas, marcas, experiencias, puntos de contacto, posibles clientes, listas, segmentos e informes.

  Se puede acceder a él desde varias ubicaciones (etiquetadas como **Campañas**) o, por ejemplo, con la dirección URL:

  `http://localhost:4502/libs/mcm/content/admin.html`
