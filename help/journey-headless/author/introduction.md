---
title: Creación para Headless con Adobe Experience Manager
description: Introducción a las potentes y flexibles funciones sin encabezado de Adobe Experience Manager y a cómo crear contenido para su proyecto.
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 87%

---

# Creación para usuarios sin encabezado con AEM: una introducción {#author-headless-introduction}

En esta parte del [Recorrido para autores de contenido sin encabezado de AEM](overview.md), puede aprender los conceptos (básicos) y la terminología necesarios para comprender la creación de contenido para la entrega de contenido sin encabezado con Adobe Experience Manager (AEM).

## Objetivo {#objective}

* **Audiencia**: principiante
* **Objetivo**: presentar los conceptos y la terminología relevantes para la creación sin encabezado.

## Sistema de administración de contenido (CMS) {#content-management-system}

¿Qué es un sistema de administración de contenido?

Un sistema de administración de contenido (CMS) es exactamente lo que su nombre indica: un sistema informático utilizado para administrar contenido. Eso es un poco general, así que para ser más precisos, (normalmente) se utiliza para administrar el contenido que desea hacer disponible en su(s) sitio(s) web.

## CMS sin encabezado {#headless-cms}

Sin encabezado es un término utilizado para describir los sistemas que disocian efectivamente el contenido de la forma de mostrar ese contenido en la web.

Tradicionalmente, el contenido se gestionaba en un CMS y el mismo CMS era el encargado de mostrarlo en las páginas web.

Ahora, sin encabezado significa que el conjunto de contenido se puede administrar en CMS y luego acceder a él una o más aplicaciones (independientes).

Esto quiere decir que el contenido puede enviarse a cualquier dispositivo, en una gran variedad de formatos. Esto hace que todo el proceso sea mucho más flexible, y también supone que no tiene que preocuparse por el diseño y el formato.

>[!NOTE]
>
>Si desea obtener más información acerca de los detalles técnicos de los CMS sin encabezado, puede leer más en Más información sobre el desarrollo de CMS sin encabezado.

## Adobe Experience Manager {#aem-cms}

¿Y qué es AEM?

Antes que nada, AEM es un sistema de administración de contenido con una amplia gama de características que también se pueden personalizar para satisfacer sus necesidades.

Todo esto significa que se puede utilizar como:

* CMS sin encabezado
   * Para sin encabezado, el contenido puede ser creado como **Fragmentos de contenido**.
Estos son elementos de contenido independientes a los que se puede acceder directamente desde varias aplicaciones, ya que tienen una estructura predefinida, basada en **Modelos de fragmentos de contenido**.
Esto quiere decir que el contenido puede llegar a una amplia gama de dispositivos, en una extensa serie de formatos y con una gran variedad de funcionalidades.
(Y como ventaja doble, estos fragmentos también se pueden utilizar al construir páginas web AEM, si así lo desea).

* CMS “tradicional”
   * El contenido se crea para las páginas web, utilizando una serie de componentes que definen cómo se mostrará el contenido en su sitio web. Incluso en este caso, AEM es sumamente flexible, ya que su equipo de proyectos puede desarrollar componentes personalizados.

## Modelado de contenido {#content-modeling}

El modelado de contenido (también conocido como modelado de datos) es otro término técnico, ¿por qué debería interesarle como autor?

Para que las aplicaciones sin encabezado puedan acceder a su contenido y hacer algo con él, el contenido debe tener una estructura predefinida. Sería posible que el contenido fuese de forma libre, pero complicaría *mucho* la vida a las aplicaciones.

Básicamente, el proceso de definición de la estructura a la que debe ceñirse el contenido implica el diseño de un modelo, y a esto se le conoce como modelado de datos.

En el caso de AEM, la función de arquitecto de contenido (normalmente una persona diferente) realizará el modelado de datos para diseñar una serie de **Modelos de fragmentos de contenido** que, a continuación, se utilizarán como base para el contenido mediante **Fragmentos de contenido**.

>[!NOTE]
>
>Si desea obtener más información acerca del modelado de datos, puede leer más en el Recorrido para arquitectos de contenido sin encabezado de AEM.

## Siguientes pasos {#whats-next}

Ahora que ya conoce los conceptos y la terminología, el siguiente paso es [Aprender los fundamentos de la creación de fragmentos de contenido](basics.md). Esto presentará el manejo básico de AEM junto con la forma de crear fragmentos de contenido.

## Recursos adicionales {#additional-resources}

* Recorrido para desarrolladores de AEM sin encabezado
   * [Obtenga más información acerca del desarrollo de CMS sin encabezado](/help/journey-headless/developer/learn-about.md)

* [Recorrido para arquitectos de contenido sin encabezado de AEM](/help/journey-headless/architect/overview.md)

* [Recorrido de traducción de contenidos sin encabezado de AEM](/help/journey-headless/translation/overview.md)

* [Introducción a AEM como CMS sin encabezado](/help/sites-developing/headless/introduction.md)

* [Portal para desarrolladores de AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=es)

* [Tutoriales de AEM sin encabezado](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=es)
