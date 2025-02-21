---
title: 'Administración de proyectos: lista de comprobación de prácticas recomendadas'
description: La administración de un proyecto para implementar Adobe Experience Manager (AEM) requiere planificación y comprensión. Las listas de comprobación de proyectos están pensadas como un conjunto de prácticas recomendadas para la entrega de proyectos. Le guían a través de todas las fases del ciclo de vida del proyecto y le proporcionan una monitorización de alto nivel de su estado.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Admin,Architect,Data Architect,Developer,Leader
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3214'
ht-degree: 0%

---

# Administración de proyectos: lista de comprobación de prácticas recomendadas{#managing-projects-best-practices-checklist}

La administración de un proyecto para implementar Adobe Experience Manager (AEM) requiere planificación y comprensión para que esté al tanto de los problemas y las decisiones (relacionadas) que debe realizar, antes y durante la implementación del proyecto.

Para ayudarle, las prácticas recomendadas consisten en:

* [lista de comprobación interactiva](/help/managing/best-practices-checklist.md) que le permite realizar un seguimiento y supervisar su progreso con estas prácticas recomendadas.

   * Define entradas y entregas según la fase, el hito y el perfil.
   * Proporciona descripciones generales automatizadas (calidad, estado y integridad) para indicar el progreso y el estado del proyecto.

* Documentación basada en [lista de comprobación](/help/managing/best-practices-checklist.md) que detalla lo siguiente:

   * Análisis de [Project Heartbeat](#projectheartbeat).
   * Información general sobre [Estado por rol](#status-by-role).
   * [Fases e hitos](#phases-and-milestones).
   * [Persona clave](#persona) y su participación en cada fase (relevante).
   * Un [Glosario](/help/managing/best-practices-glossary.md) de [documentos y entregables requeridos](#required-documents-and-deliverables).

* [Más material de referencia](/help/managing/best-practices-further-reference.md) para proporcionar más detalles sobre áreas específicas.

## Tablero de Heartbeat del proyecto {#project-heartbeat-dashboard}

La hoja de cálculo de **Project Heartbeat** proporciona una descripción general gráfica de las métricas críticas para su proyecto:

* **Calidad de fase**

   * Indica la calidad de [documentos y entregas requeridos](#required-documents-and-deliverables) en todo el proyecto.

* **Estado de fase**

   * Un indicador de estado de alto nivel para su proyecto; útil para resaltar áreas que puedan estar en riesgo.

* **Finalización de fase**

   * En cualquier momento durante el proyecto, esto indica cuánto se ha completado ya para cada fase del proyecto.

## Estado por rol {#status-by-role}

La hoja de cálculo **Estado por rol** muestra un desglose detallado de [**Salud**, **Calidad y **Complejidad**](#projectheartbeat) por **[Fase](#phases-and-milestones)** y **[Persona](#persona)**.

## Fases e hitos {#phases-and-milestones}

El plan del proyecto se divide en distintas fases (alto nivel).

Cada fase contiene sus propios hitos. Para cada [persona](#persona) (o función), se enumeran los hitos relevantes, junto con los documentos necesarios para producir los entregables definidos.

>[!NOTE]
>
>No existe una relación directa 1:1 entre los documentos y las entregas individuales requeridos.

### Preparación {#preparation}

La preparación del proyecto forma la base de todo el proyecto. Defina los requisitos clave junto con objetivos y expectativas claros para:

* **Motivo comercial**

   * Las razones fundamentales y la justificación para emprender el proyecto.

* **Ámbito y horario**

   * Debe haber disponible un ámbito básico y una programación aproximada para definir qué se necesita y en qué plazo; si ayuda a aclarar la situación, también puede definir qué se encuentra fuera del ámbito.

La forma de preparar, planificar y ejecutar el proyecto e implementar la solución se ve afectada por las restricciones en las que está operando. Por ejemplo, presupuesto fijo, plazos fijos, cantidad de contenido, calidad requerida.

Como siempre, ajustar cualquiera de los factores afecta a los demás. Por ejemplo, si reduce el tiempo, pero requiere el mismo nivel de calidad, probablemente aumente el precio y reduzca la cantidad de contenido que puede satisfacer. El presupuesto es a menudo un factor clave por lo que tales relaciones no se pueden olvidar.

Los Cuatro Factores:

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### Hitos {#milestones}

* **Validación**

  En esta fase, debe validar y confirmar los objetivos del proyecto; por ejemplo:

   * ¿Qué desea lograr/proporcionar?
   * ¿Quién se beneficia?
   * ¿Cuál es el ámbito?

      * Si ayuda a aclarar la situación, también puede definir qué se encuentra fuera del ámbito.

   * ¿Cómo se define el éxito?
   * ¿Cómo se mide el éxito?
   * ¿Cuáles son los requisitos, empresariales y técnicos?
   * ¿Hay sistemas heredados que reemplazar y, si es así, hay datos que migrar?
   * ¿Quién está involucrado?
   * ¿Cómo se mide el progreso?
   * ¿Con qué frecuencia revisa el progreso durante la duración del proyecto?

* **Presupuesto**

  Antes de comenzar cualquier proyecto, necesita una estimación fiable y realista de lo que cuesta implementar:

   * Utilice la información del hito de validación como base para las estimaciones.
   * Sea realista en sus estimaciones.
   * Considere y respete las directrices, los procesos o las restricciones de los clientes a los que esté sujeto.
   * Considere los procesos de contingencia y revisión si más adelante se requiere una revisión o un ajuste del presupuesto.
   * Recuerde que los costos vienen en muchas formas, tales como compras, uso de recursos y tarifas, entre otras.

### Planificación {#planning}

La planificación del proyecto consolida la preparación. Aquí debería empezar a convertir los objetivos y expectativas en una hoja de ruta bien definida que consista en tareas concretas, unidas por una comunicación clara, con revisiones estrictas para medir el progreso.

#### Hitos {#milestones-1}

* **Envío**

  Un traspaso limpio garantiza que las personas/grupos adecuados sean conscientes de sus responsabilidades dentro del proyecto.

  Se deben proporcionar/generar detalles completos para garantizar que tengan una comprensión completa de todos los aspectos relevantes, incluida la hoja de ruta, el alcance, los objetivos, los requisitos y los KPI.

* **Evaluación de riesgos**

  Para evitar sorpresas desagradables, utilice la evaluación de riesgos para identificar y cuantificar cualquier riesgo potencial junto con su impacto y probabilidad.

  Esto debe hacerse al principio del ciclo de vida del proyecto para garantizar que se identifiquen y evalúen las vulnerabilidades. En función de los resultados, puede informar a las partes interesadas de si se pueden implementar todos los requisitos y, si es necesario, si es posible planificar las acciones adecuadas que se deben tomar y rastrear.

* **Comunicación**

  La comunicación siempre es clave para el éxito de cualquier proyecto. Comunique de forma clara y eficaz para garantizar que todos:

   * Trabajar para lograr los mismos objetivos básicos
   * Desde la misma base de información
   * Con los mismos canales

* **Inicio**

  La reunión de inicio se utiliza para concienciar sobre el inicio del proyecto. Es una buena oportunidad para:

   * Invitar a todas las partes interesadas (o al menos a los representantes del grupo).
   * Presente datos clave sobre el proyecto.
   * Responda preguntas.
   * Asegúrese de que todos los usuarios tengan la misma base de conocimientos.
   * Consiga el compromiso de todos los que se involucren: esto tendrá que ganarse.

      * Al involucrar a los principales actores (incluidos los posibles autores) al principio del proyecto, aumenta las posibilidades de obtener su compromiso con el proyecto.

### Preparación del desarrollo {#development-preparation}

La planificación del desarrollo es clave para garantizar que el proyecto se basa en un diseño sólido por parte de un equipo que tenga los conocimientos necesarios.

#### Hitos {#milestones-2}

* **Equipo de desarrollo con personal y capacitación**

  Antes de comenzar cualquier proyecto, debe asegurarse de que el equipo de desarrollo tenga el personal adecuado y de que todos los miembros del equipo estén formados para la tarea en cuestión.

* **Arquitectura de contenido**

  La arquitectura de contenido define y describe la arquitectura futura del contenido, lo que incluye:

   * El árbol de contenido; incluidos los recursos
   * Estructuras básicas; incluidas campañas, etc.
   * Estructuras multisitio y en varios idiomas (MSM, traducción, etc.)
   * Contenido de soporte (incluidas etiquetas y conceptos de etiquetado)
   * Estrategias de almacenamiento en caché y reutilización de contenido

* **Arquitectura de sistema**

  La arquitectura del sistema define la vista conceptual del sistema, que incluye (entre otra información):

   * [Estructura del sistema](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) para todos los entornos necesarios
   * Subsistemas
   * Sistemas de terceros
   * Interfaces; hardware, software e interacción humana
   * Servidores para cada entorno; consulte los [Requisitos técnicos](/help/sites-deploying/technical-requirements.md) y las [Directrices de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md)

   * Procesos para cada entorno; por ejemplo, requisitos de implementación y mantenimiento
   * Actividades de mantenimiento (optimización del almacén de datos, TarPM, etc.)
   * Almacenamiento en caché de [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es)
   * [Clúster](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) Publish/Authorshare
   * Rendimiento del lado del cliente (minificación de JS, concat, sprites css, número total de solicitudes http, etc.)

* **Arquitectura de aplicación**

  La arquitectura de la aplicación define y describe el comportamiento de las aplicaciones propuestas.

  Se centra en:

   * Cómo interactúan entre sí y con los usuarios.
   * Los datos que deben consumir y producir las aplicaciones, en lugar de su estructura interna.

  Las definiciones deben abarcar:

   * Estructura de código básica del proyecto
   * Artículos de código (paquetes, paquetes, etc.)
   * Desglose de las plantillas/componentes y sus relaciones
   * Detalles de alto nivel de las personalizaciones necesarias (a continuación se muestran superposiciones específicas)
   * Diseño de los flujos de trabajo requeridos por la solución (por ejemplo, creación de contenido, aprobación, publicación, transformaciones, importaciones y exportaciones)
   * Consideración especial para cualquier módulo complejo, como MSM, Commerce o integración de terceros

* **Integración de sistemas**

  La integración del sistema requiere que planifique (y luego implemente):

   * Cómo se unen todos los subsistemas y las [integraciones de soluciones](/help/sites-administering/integration.md) para funcionar como un sistema coherente
   * Forma en que se integran los sistemas de terceros, junto con cualquier consideración especial, como la gestión sin conexión/en línea, del lado del cliente/del lado del explorador o de la caída de un sistema de terceros cuando éste no funciona

* **Concepto de prueba**

  Antes de comenzar el desarrollo, debe elaborar un concepto detallado y completo de todos los requisitos de [prueba](/help/sites-developing/planning.md) para su proyecto.

  Esto debe incluir (entre otros):

   * Detalles de todas las pruebas a realizar
   * Preparación del contenido necesario para esas pruebas
   * Información sobre las herramientas de ensayo que se utilizarán
   * Indicación de alto nivel de quién participará en las pruebas, especialmente grupos fuera del equipo de control de calidad
   * Detalles de la automatización de pruebas; por ejemplo, con el modo de desarrollador de Selenium o AEM

* **Diseño de experiencia**

  Experience Design (XD) implica diseñar la experiencia del usuario para la solución.

  La experiencia del usuario debe analizarse y desarrollarse tanto para los autores como para los usuarios finales del sitio web.

* **Configuración de soporte**

  Antes del desarrollo, deben establecerse todos los procesos de compatibilidad necesarios para implementar, publicar, probar e informar de problemas.

  Consulte también el [Portal de asistencia de Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home&amp;lang=es#support).

### Planificación de operaciones y operaciones {#operations-planning-and-operations}

Del mismo modo, las operaciones deben planificarse correctamente para garantizar que dispone de los entornos necesarios para todas las etapas del ciclo de vida del proyecto. También necesita los procesos adecuados para mantenerlos.

#### Hitos {#milestones-3}

* **Permisos**

  Debe planificar y, a continuación, implementar un concepto de funciones y derechos para todos los usuarios/grupos que utilizarán la solución.

  Por ejemplo:

   * Una lista de funciones (es decir, grupos) con definiciones de acceso de `read`/ `write` para cada una

   * Definición del uso de privilegios que afectan al entorno de publicación; por ejemplo, `replicate`
   * Para los usuarios con privilegios mínimos, se deben definir los flujos de trabajo
   * Los usuarios del grupo `editor` no deben tener derechos de `admin` ni formar parte del grupo `administrators`

  Para obtener más información, consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md).

* **Supervisión y mantenimiento**

  La monitorización y el mantenimiento son aspectos clave para garantizar el funcionamiento sin problemas de la solución una vez que se ponga en marcha. Para ello, debe definir lo siguiente:

   * Qué necesita monitorización
   * Tareas de mantenimiento; tanto regulares como para casos especiales

  Consulte también [Supervisión y mantenimiento](/help/sites-deploying/monitoring-and-maintaining.md) para obtener más información.

* **Migración**

  Cualquier contenido del sistema heredado debe revisarse y validarse para la migración.

* **Plan de recuperación**

  Asegúrese de que dispone de un plan de recuperación. En caso de emergencia, debe estar disponible para garantizar el uso de AEM en la producción. Esto debe cubrir situaciones como copias de seguridad, restauración, visitas en orden previsto y otras.

### Desarrollo {#development}

El desarrollo es una fase crucial que requiere algo más que codificación.

#### Hitos {#milestones-4}

* **Entorno de desarrollo**

  Planifique y documente su entorno de desarrollo, lo que incluye:

   * Arquitectura
   * [Herramientas de desarrollo](/help/sites-developing/dev-tools.md)

      * Un entorno típico consta de:

         * un sistema de seguimiento de problemas; como Jira
         * un IDE; como Eclipse
         * una herramienta de administración de compilaciones; como Maven
         * una herramienta para la integración continua; como Jenkins
         * una herramienta para el control de versiones; como GIT/SVN
         * un administrador de repositorios de artefactos de compilación; como Archiva/Nexus

   * Integración/dependencias de software de terceros
   * [Integración/dependencias de la solución](/help/sites-administering/integration.md)
   * Cadencia de implementación

* **Sistema de prueba**

  Planifique y documente su entorno de prueba, lo que incluye:

   * Arquitectura
   * Dependencias de las compilaciones de desarrollo, incluidas las compilaciones nocturnas
   * Las posibilidades o limitaciones de probar la integración/dependencias de software de terceros
   * Herramientas de prueba
   * Estrategia de pruebas automatizadas

* **Sistema de producción**

  Planifique y documente su entorno de producción, lo que incluye:

   * Arquitectura
   * Cadencia de implementación
   * Integración/dependencias de software de terceros
   * Configuración de seguridad
   * Rendimiento de línea de base verificado ejecutando [pruebas de día difíciles](/help/sites-developing/tough-day.md) en la configuración de producción
   * Requisitos para pruebas de rendimiento; consulte [Prácticas recomendadas para Assurance de calidad](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **Integración**

  Planifique, documente y pruebe todos los aspectos del sistema y la [integración de soluciones](/help/sites-administering/integration.md), incluidos:

   * Una estrategia de pruebas automatizadas
   * Procesos automatizados para [mover aplicaciones de desarrollo a prueba y después a producción](/help/managing/enterprise-devops.md#code-movement)
   * Procesos automatizados para [mover contenido de producción a prueba y desarrollo](/help/managing/enterprise-devops.md#content-movement)

* **Migración**

  Planifique, documente y pruebe todos los aspectos de la migración de contenido, incluidos los siguientes:

   * Arquitectura de contenido
   * Estrategia de migración

* **Comunicación**

  Asegúrese de que todos los miembros del equipo y el personal del proyecto se mantienen actualizados según sea necesario.

* **Documentación**

  Documente la solución completamente; incluyendo:

   * Manual de operaciones
   * Cualquier personalización que pueda afectar a las actualizaciones
   * Notas de la versión

### Rendimiento y pruebas {#performance-and-testing}

Una vez que la nueva aplicación esté disponible, deberá someterse a rigurosas pruebas, tanto para la funcionalidad como para el [rendimiento](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>Se debe permitir que cualquier equipo de prueba permanezca neutral y entregue los resultados de la prueba.
>
>Es responsabilidad del gestor del proyecto evaluar las implicaciones de los resultados y decidir las acciones apropiadas.

#### Hitos {#milestones-5}

* **Prueba de aceptación de usuario final**

  [Las pruebas de aceptación del usuario](/help/sites-developing/acceptance-signoff.md) (UAT) son cruciales para asegurar que:

   * La solución satisface los requisitos del usuario/cliente
   * El cliente o los usuarios aceptan la solución (función, diseño y rendimiento)

  Debe haber una lista de comprobación formalizada para el traspaso de clientes; idealmente automatizada y ejecutada todas las noches con una instantánea. Los resultados deben enviarse al jefe de proyecto y al equipo de desarrollo

* **Pruebas de rendimiento y carga**

  Las pruebas de rendimiento y carga se utilizan para garantizar que la solución cumpla los niveles de rendimiento requeridos, con cargas medias y máximas.

  Para obtener más información sobre las pruebas de rendimiento, consulte:

   * [Pruebas de rendimiento](/help/sites-deploying/configuring-performance.md)
   * [Planificación y ejecución de pruebas](/help/sites-developing/planning.md)

   * [Directrices básicas de rendimiento](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)

  >[!NOTE]
  >
  >Este proceso debe continuarse durante el uso normal de AEM, pero estas fases iniciales son las más cruciales.

### Despliegue {#rollout}

El despliegue de la nueva aplicación requiere una planificación cuidadosa para garantizar un lanzamiento sin problemas. Esto incluye confirmar un alto nivel de seguridad, entrenar a todos los posibles usuarios y hacer múltiples simulacros para confirmar que todos los problemas se han tratado.

#### Hitos {#milestones-6}

* **Preparación**

  La preparación y la planificación ayudarán a garantizar un despliegue sin problemas.

* **Formación**

  Asegurarse de que todo el personal involucrado haya recibido formación.

  Ver [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) en el catálogo de cursos.

* **Administradores capacitados**

  Asegúrese de que los administradores de su solución tengan:

   * Se ha entrenado
   * Se recibió el material de capacitación apropiado
   * Se ha recibido la documentación adecuada

* **Usuarios capacitados**

  Asegúrese de que los autores tengan:

   * Se ha entrenado
   * Se recibió el material de capacitación apropiado
   * Se recibió la documentación adecuada; por ejemplo, la Guía del usuario

* **Pruebas de penetración**

  Las pruebas de penetración simulan un ataque a un sistema informático para identificar posibles deficiencias de seguridad.

* **Pruebas de penetración/seguridad**

  Para garantizar la seguridad de su solución, realice pruebas de penetración específicas, junto con una gama más amplia de pruebas de seguridad.

  Consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md) para obtener más información.

### Lanzamiento {#go-live}

Desea que el lanzamiento sea lo más fluido posible. De nuevo, los pasos finales deben planificar para una ejecución limpia.

#### Hitos {#milestones-7}

* **Preparación**

  La preparación y planificación ayudarán a garantizar un lanzamiento sin problemas.

* **Seguridad**

  Confirme la seguridad de su solución tanto para usuarios internos como externos, así como para su contenido.

* **Reserva**

  Asegúrese de que todos los sistemas, procedimientos y mecanismos necesarios para la reserva estén implementados antes de activarse.

* **Asistencia**

  Asegúrese de que los servicios de asistencia estén implementados y listos.

* **Transición**

  Planifique y ejecute la transición a su entorno de producción y a los usuarios.

* **Desplegar**

  Prepara y ejecuta tus pruebas de humo.

## Grupo de usuarios {#persona}

Las listas de comprobación están diseñadas por persona. Son las funciones con participación significativa en el ciclo de vida del proyecto.

También hay [otros personajes](#other-persona) que están involucrados en tareas específicas.

### Patrocinador de proyecto {#project-sponsor}

El patrocinador del proyecto es:

* Responsable de proporcionar/presentar el caso empresarial del proyecto.
* Clave para dar forma y definir el ámbito del proyecto; incluye:

   * la definición y los criterios de éxito
   * los KPI principales

* Proporcione los hitos principales en función de la hoja de ruta del cliente.

### Gestor de proyectos {#project-manager}

El jefe de proyecto es:

* Responsable de la entrega general del proyecto en función de los requisitos (por ejemplo, alcance, KPI, criterios de éxito y definición) proporcionados por el patrocinador del proyecto.
* Responsable de definir el presupuesto y dotar de recursos al proyecto en función de dicho presupuesto.
* El principal punto de comunicación para todas las personas involucradas en el proyecto.

### Arquitecto {#architect}

El arquitecto de soluciones:

* Es responsable del diseño de alto nivel de la solución y el sistema.
* Ayuda a definir la estrategia de implementación para AEM. Por ejemplo, si se debe implementar una instalación agrupada, una espera en frío o cuando se necesita una red de entrega de contenido (CDN).
* Defina también la arquitectura de la solución AEM en función de los requisitos del cliente. Esto puede incluir el concepto de funciones de usuario (con derechos relacionados), la relación entre plantillas y componentes o cuándo utilizar la administración de varios sitios.

### Analista empresarial {#business-analyst}

El analista empresarial:

* Es el principal responsable de recopilar y analizar los requisitos de alto nivel, para luego transformarlos en especificaciones:

   * para que el administrador de proyectos lo utilice al planificar el desarrollo
   * para que el equipo de desarrollo trabaje desde durante el diseño y el desarrollo.

* Trabaja en estrecha colaboración con el cliente para analizar los requisitos. Coinciden con estos:

   * La definición de éxito.
   * Los criterios de éxito.
   * KPI (basados tanto en el negocio como en el rendimiento).

### Responsable de desarrollo {#development-lead}

El líder del desarrollo:

* Es responsable de la entrega técnica del proyecto.
* Es responsable de seleccionar una metodología de desarrollo que cumpla con los requisitos del cliente.
* Elabora la estrategia de desarrollo:

   * garantizar que esté alineado con los KPI empresariales y de rendimiento
   * teniendo en cuenta los criterios de éxito y la definición

* Trabaja en estrecha colaboración con el arquitecto (especialmente al diseñar la estrategia de desarrollo para AEM) para definir aspectos como la relación entre plantillas y componentes, la estrategia de integración para aplicaciones de terceros y cualquier funcionalidad especializada.

### Posible cliente de calidad {#quality-lead}

El posible cliente de calidad:

* Es responsable de la calidad del envío; se asegura de que cumpla los criterios de éxito y cualquier KPI definido por el cliente.
* Define las métricas de calidad, se alinea con todas las partes interesadas, elabora los planes de prueba y garantiza que se ejecuten.
* Crea y envía informes a las partes interesadas del proyecto.

### Ingeniero de sistemas {#system-engineer}

El ingeniero de sistemas:

* Es responsable de supervisar la infraestructura del proyecto.
* Es responsable de:

   * la configuración de entornos de prueba y desarrollo internos
   * para hacer coincidir esos sistemas con los sistemas cliente

* Proporciona recomendaciones de hardware, supervisa las distintas implementaciones y proporciona soporte de operaciones tanto antes como después de la activación.

### Responsable de seguridad {#security-lead}

El posible cliente de seguridad:

* Es responsable del concepto de seguridad general de la solución, asegurándose de que esté alineada con cualquier requisito y política del cliente.
* Ofrece un concepto de seguridad, operaciones de seguridad y recomendaciones para cualquier concepto de seguridad basado en hardware; como zonas y cortafuegos.

### Otra persona {#other-persona}

* Partes interesadas

   * Personas (a menudo de la empresa) que tienen interés (participación) en el éxito del proyecto. A menudo contribuyen al presupuesto.

* Oficio

   * Se necesita asesoramiento jurídico cuando se negocian contratos.

* Formadores

   * En función de la escala y la naturaleza del proyecto, se pueden utilizar instructores especializados para preparar y presentar sesiones de capacitación para los grupos pertinentes.

* Escritores técnicos

   * Dependiendo de la escala y la naturaleza del proyecto, se pueden utilizar redactores técnicos especializados para escribir directrices y manuales para grupos específicos. Por ejemplo, un manual de mantenimiento para administradores del sistema o una guía del usuario para autores.

* Administradores del sistema

   * Responsable del funcionamiento continuo del sistema.

* Autores y usuarios finales

   * Las personas que utilizan el sistema para crear y mantener el contenido del sitio web.

## Documentos y entregables requeridos {#required-documents-and-deliverables}

Las listas de comprobación cubren los **documentos necesarios** y **entregables** para cada hito.

* No existe una relación 1:1 entre ellos; por ejemplo, un grupo de documentos requeridos puede dar como resultado un solo resultado.
* Una entrega de una persona puede ser un documento obligatorio para otra persona durante el mismo hito.

### Documentos requeridos {#required-documents}

Los **documentos requeridos** los necesita el usuario apropiado al producir sus entregables.

Para cada **documento requerido**, el personaje debe indicar:

* **S/N**: si se ha recibido.
* **1-3**: una indicación de la calidad del documento recibido.

### Entregables {#deliverables}

Para cada hito, las personas adecuadas son responsables de entregar documentos específicos y, por lo tanto, de cumplir con sus responsabilidades en un hito específico.

Para cada **entrega**, el usuario debe indicar:

* **S/N**: si se ha completado.

Las entregas se utilizan a menudo como **Documentos requeridos** para el hito actual o posterior.

## Prácticas recomendadas relacionadas {#related-best-practices}

Para conocer las prácticas recomendadas sobre la implementación, administración, desarrollo o creación, consulte los siguientes temas:

* Otras prácticas recomendadas y directrices relacionadas con la administración de un proyecto de AEM:
   * [Directrices de tamaño de hardware](/help/managing/hardware-sizing-guidelines.md)
   * [Operaciones de desarrollo empresarial](/help/managing/enterprise-devops.md)
   * [Prácticas recomendadas para la optimización de los motores de búsqueda y administración URL](/help/managing/seo-and-url-management.md)
   * [AEM y las directrices de accesibilidad web](/help/managing/web-accessibility.md)
   * [Reglamento General de Protección de Datos](/help/managing/data-protection-and-privacy.md)* [Prácticas recomendadas de implementación y mantenimiento](/help/sites-deploying/best-practices.md)
* [Prácticas recomendadas de administración](/help/sites-administering/administer-best-practices.md)
* [Desarrollo de prácticas recomendadas](/help/sites-developing/best-practices.md)
* [Prácticas recomendadas de creación](/help/sites-authoring/best-practices.md)

## Áreas clave de documentación {#key-documentation-areas}

* Documentación de AEM
Además, las siguientes secciones de la documentación de AEM son de especial interés (sin embargo, esta lista no es exhaustiva):

   * [Seguridad](/help/sites-developing/security.md)
   * [Implementaciones recomendadas](/help/sites-deploying/recommended-deploys.md)
   * [Operaciones de desarrollo empresarial](/help/managing/enterprise-devops.md)
   * [Tamaño de hardware](/help/managing/hardware-sizing-guidelines.md)
   * Conceptos de AEM:

      * [Desarrollo: conceptos básicos](/help/sites-developing/the-basics.md)
      * [Conceptos de MSM](/help/sites-administering/msm.md)
      * [Lenguaje de plantilla HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=es)

* Documentación relacionada

   * Adobe Experience Cloud - [Planificación de Adobe Experience Cloud](https://experienceleague.adobe.com/docs/core-services/interface/services/core-services.html)
