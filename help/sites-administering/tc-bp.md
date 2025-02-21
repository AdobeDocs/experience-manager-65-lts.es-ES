---
title: Prácticas recomendadas de traducción
description: Descubra las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha proyectos de traducción.
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 93%

---

# Prácticas recomendadas de traducción{#translation-best-practices}

## General {#general}

La creación o ampliación de una presencia web global puede ser un proceso complejo, pero con una buena previsión y planificación, AEM puede simplificar sus esfuerzos y apoyar sus objetivos empresariales globales.

* **Plan de expansión global** antes de implementar su primer sitio. Adaptar un sitio existente para una cobertura global cuando el sitio se implementó con poco tiempo de antelación, generalmente es más difícil que planificar la expansión global al principio:

   * Evalúe el estado actual de la madurez de la localización de su organización. Determine si tiene las suficientes **herramientas**, **procesos** y **recursos** para apoyar la expansión global.
   * Tenga en cuenta las **regulaciones globales** y las **preferencias de idioma regional**. Diseñe estructuras y procesos de contenido flexibles que puedan adaptarse a un entorno comercial global cambiante.

* Determine un modelo de **gobernanza** que sea compatible con su negocio global y utilice mecanismos de AEM como MSM y permisos de usuario para aplicar el modelo elegido. Por ejemplo, determine si el contenido se creará de forma centralizada y si se &quot;insertará&quot; o &quot;extraerá&quot; a regiones/países. Determine qué contenido se puede desbloquear y modificar en las regiones geográficas. Determine quién es el responsable de iniciar y administrar las traducciones.
* Si los recursos lo permiten, es mejor administrar la actividad de traducción desde un equipo central que pueda desarrollar conocimiento en las herramientas, los procesos y las relaciones con los proveedores necesarios.
* **Planee**, **cree un prototipo** y **pruebe** su estructura y procesos globales para garantizar que respaldan el negocio y que cuenta con el apoyo necesario de las partes interesadas en las regiones geográficas.

## Estructura del sitio    {#site-structure}

* Al diseñar la estructura del sitio, comience por examinar el contenido y determinar dónde y en qué idioma se crea el contenido. Esta ubicación debe ser el nivel superior del sitio.
* Una práctica recomendada es la **estructura basada en un idioma** con no más de tres niveles entre el nivel superior de creación y los sitios del país.
* Utilice una convención de nomenclatura de sitios por idioma/país que siga los **estándares W3C**.
* Determine cómo se distribuye el contenido por regiones y países. Considere qué países comparten idiomas. Se recomienda crear formatos de idiomas, una capa de páginas no activadas, donde el contenido traducido puede revisarse y modificarse, luego ser transferido o llevado a un sitio de un país que comparta ese idioma.
* Existen dos métodos para crear formatos de idiomas: usando copias de idioma y usando MSM/Live Copies.

   * El método de copia de idioma es el que utiliza el marco de trabajo de integración de traducciones predeterminado de AEM y, por lo tanto, es la forma más sencilla de empezar. El marco de trabajo proporciona una interfaz de usuario que facilita inicialmente la propagación y traducción de los cambios de contenido del formato de idioma principal (por ejemplo, inglés) a los otros formatos de idioma. Sin embargo, a medida que el proyecto crece, la automatización del flujo de trabajo se hace cada vez más necesaria para administrar la traducción del mayor número de páginas o idiomas.
   * El método MSM/Live Copy puede ser una alternativa para casos de uso avanzados, donde los sitios son más grandes y complejos. Es necesario contar con una buena gobernanza y una automatización del flujo de trabajo desde el principio para gestionar las complejas relaciones de herencia entre los formatos de inglés y de otros idiomas, así como para reducir el riesgo de sobrescribir traducciones existentes. Esta gestión se puede realizar con la ayuda de algunos conectores de traducción. Consulte [MSM y sitios multilingües](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites) para obtener más información.

* Si el idioma principal tiene variaciones globales, una opción es usar MSM para crear una Live Copy del formato global y utilizarla para la traducción. Por ejemplo, si la creación global se realiza en un formato de inglés de EE. UU., cree un formato de inglés internacional como Live Copy y base para la traducción a otros idiomas.
* Utilice MSM para crear sitios de país a partir de los formatos de idiomas traducidos y para desplegar contenido en sitios que compartan el mismo idioma. Por ejemplo, el formato de francés se puede desplegar en los sitios de Francia, Bélgica y Suiza.
* Planifique, cree prototipos y haga pruebas primero antes de iniciar la implementación.

## Procesos y métodos de traducción {#translation-processes-and-methods}

* Trabaje con un **proveedor de servicios de localización (LSP)** con experiencia en traducción y actividades de localización relacionadas. Los LSP pueden escalar su negocio global al proporcionar una amplia gama de recursos y tecnologías para mejorar la eficiencia y ahorrar costos de traducción:

   * Algunos LSP son proveedores de servicios y de tecnología a la vez. También hay proveedores de tecnología independientes que permiten a muchos LSP participar en sus plataformas de traducción.
   * El **marco de trabajo de traducción de AEM** admite la integración con una variedad de proveedores de tecnología de traducción tanto para la traducción automática como para la humana.
   * Obtenga información sobre cómo [integrar conectores LSP en su sistema AEM](/help/sites-administering/translation.md) para automatizar la traducción de contenido, o cómo crear, exportar e importar manualmente proyectos de traducción para probarlos también en casos en los que no haya ningún proveedor de tecnología LSP o de traducción.

* Elija un **método de traducción** que mejor se adapte al contenido.

   * La **traducción humana** es el método más adecuado para el contenido, donde las expectativas de transmisión del mensaje y de calidad son altas y el contenido estará activo durante un tiempo en el sitio, como en el caso de las páginas de marketing.
   * La **traducción automática** puede ser una buena elección para volúmenes de traducción masivos cuando el tiempo de publicación es crítico, las expectativas de calidad son relajadas o los costos de traducción humana son prohibitivos. La base de conocimiento de soporte y el contenido generado por el usuario suelen traducirse automáticamente.

* Confíe en los conocimientos y experiencia de los proveedores de servicios de localización, los asesores de Adobe y los integradores de sistemas para planificar, crear prototipos y probar la estructura multilingüe de su sitio.
