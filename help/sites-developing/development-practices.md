---
title: Prácticas de desarrollo
description: Prácticas recomendadas para desarrollar en Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6c0cddc8-44b0-4e75-939f-2a1f735508fc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%
---
# Prácticas de desarrollo{#development-practices}

## Trabajar según una definición de Listo (DoD) {#work-according-to-a-definition-of-done}

Cada equipo tiene una definición diferente de lo que significa &quot;hecho&quot;, pero es importante tener una y asegurarse de que una historia cumpla con los criterios definidos antes de ser aceptada.

Algunos criterios que suelen especificar los equipos son:

* Código revisado para el formato
* Comentarios/Javadoc añadido
* Cumple los niveles de cobertura de prueba requeridos
* Supera las pruebas de unidad e integración
* Validado en el entorno de control de calidad
* Localización implementada

Sin un DoD bien definido, es fácil terminar en una situación en la que muchas cosas están a medio camino y nada está verdaderamente completo.

### Definir y cumplir las convenciones de codificación y formato {#define-and-adhere-to-coding-and-formatting-conventions}

Las cosas como los niveles de sangría y el espacio en blanco pueden no parecer importantes, pero tener un código con el formato correcto contribuye en gran medida a la legibilidad y la capacidad de mantenimiento. Las convenciones deben debatirse y acordarse como un equipo y luego seguirse en el código.

### Objetivo para una alta cobertura de pruebas  {#aim-for-high-test-coverage}

A medida que aumenta el tamaño de la implementación de un proyecto, también lo hace el tiempo necesario para probarlo. Sin una buena cobertura de las pruebas, el equipo de pruebas no puede escalar y los desarrolladores terminan enterrados en errores.

Los desarrolladores deben practicar el desarrollo impulsado por pruebas (TDD) y escribir pruebas unitarias que produzcan errores antes del código de producción que cumpla sus requisitos. El control de calidad debe crear un conjunto automatizado de pruebas de aceptación para garantizar que el sistema funcione según lo esperado desde un alto nivel.

Hay marcos personalizados disponibles, como Jackalope y Prosper, para hacer que burlarse de las API de JCR sea más fácil para garantizar la productividad de los desarrolladores mientras escriben pruebas unitarias.

### Mantén la demostración lista {#stay-demo-ready}

El sistema debe estar disponible para la demostración a la empresa al final de cada iteración. Al mantener el sistema en un estado listo para la demostración, el equipo siempre estará dentro de una iteración de estar listo para la producción y la deuda técnica se puede mantener a un nivel mantenible.

### Implementar un entorno de integración continua y utilizarlo {#implement-a-continuous-integration-environment-and-use-it}

La implementación de un entorno de integración continua permite ejecutar de forma fácil y repetida pruebas unitarias y de integración. También desvincula las implementaciones del equipo de desarrollo, lo que permite que las demás partes del equipo sean más eficientes y lograr implementaciones más estables y predecibles.

### Mantenga el ciclo de desarrollo rápido al mantener los tiempos de compilación bajos {#keep-the-development-cycle-fast-by-keeping-build-times-low}

Si las pruebas unitarias tardan mucho tiempo en ejecutarse, los desarrolladores evitarán ejecutarlas y perderán su valor. Si se tarda mucho tiempo en crear el código e implementarlo, las personas lo harán con menos frecuencia. Hacer que los tiempos de compilación cortos sean una prioridad garantiza que el tiempo que ha invertido en la cobertura de pruebas y en la infraestructura de CI siga haciendo que el equipo sea más productivo.

### Ajuste de Sonar y otras herramientas de análisis de código estático y actúe en función de sus informes {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

Las herramientas de análisis de código pueden ser valiosas, pero solo si sus informes conducen a la acción por parte del equipo de desarrollo. Sin afinar el análisis que proporcionan estas herramientas, las recomendaciones que generan se vuelven irrelevantes y pierden su valor.

### Sigue las reglas de los Boy Scout {#follow-the-boy-scout-rule}

Los Boy Scouts tienen una regla: &quot;Déjalo mejor de lo que lo encontraste&quot;. Mientras todos los miembros del equipo de desarrollo se adhieran a esta regla y limpien algo cuando se encuentren con un lío, el código mejorará constantemente.

### Evitar la implementación de funciones YAGNI {#avoid-implementing-yagni-features}

Las funciones de YAGNI (No lo vas a necesitar) son cosas que se implementan cuando esperamos que necesitemos algo en el futuro, aunque no lo necesitemos ahora. Idealmente, deberíamos implementar lo más simple que funcione hoy en día y utilizar una refactorización continua para garantizar que la arquitectura del sistema evolucione con los requisitos a lo largo del tiempo. Esto nos permite centrarnos en lo que importa y evitar la hinchazón del código y la fluidez de las funciones.
