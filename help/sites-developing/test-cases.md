---
title: Definición de los casos de prueba
description: Los casos de prueba deben basarse en los casos de uso y en la especificación de requisitos detallada
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Definición de los casos de prueba{#defining-your-test-cases}

Los casos de prueba deben basarse en lo siguiente:

**Casos de uso**

* Definen la funcionalidad necesaria en términos de la interacción entre los actores (funciones que inician determinadas acciones) y el sistema.
* El cliente debe definir los casos de uso.

**Especificación detallada de los requisitos**

* Deben probarse todos los requisitos funcionales y de rendimiento.

Las pruebas deben definir claramente:

* Requisitos previos; pueden cubrir sistemas, configuraciones o experiencia del evaluador específicos.
* Pasos que deben seguirse, con el nivel de detalle adecuado.
* Resultados esperados.
* Borrar criterios para aprobar o suspender.

La perspectiva de automatizar los casos de prueba es atractiva porque elimina las tareas repetitivas.

## Pruebas manuales y automatizadas {#manual-versus-automated-tests}

Sin embargo, automatizar los casos de prueba es una inversión significativa, por lo que se deben considerar ciertos aspectos:

* Requiera tiempo, esfuerzo y experiencia para configurar.
* Si se basa en un explorador, existe un mayor riesgo de problemas cuando se instalan actualizaciones del explorador; se requiere más tiempo para corregir.
* Solo es factible para proyectos grandes.
* Es bueno cuando se generan varias versiones para pruebas o en el plan de versiones a largo plazo.

## Prueba de aspectos específicos {#testing-specific-aspects}

Al probar AEM, algunos detalles específicos son de especial interés:

**Entornos de creación y publicación**

Aunque se trata en [Entornos](/help/sites-developing/the-basics.md#environments), vale la pena destacar un factor decisivo de AEM con respecto a las pruebas.

Considere AEM como dos aplicaciones:

* el entorno *Author*
Esta instancia permite a los autores introducir y publicar contenido.
Tiene un conjunto de usuarios pequeño(a) y predecible, para los que la funcionalidad y el rendimiento específicos son cruciales.

* el entorno *Publish*
Esta instancia presenta el sitio web en su formulario publicado para el acceso de los visitantes.
Esto suele tener un conjunto mayor de usuarios, donde el volumen de tráfico no siempre es 100% predecible. El rendimiento sigue siendo crucial: al responder a las solicitudes. Considere también el almacenamiento en caché y el equilibrio de carga.

Aunque el mismo software como tal, ellos:

* servir para diferentes propósitos
* tienen diferentes requisitos relacionados con la funcionalidad y el rendimiento
* están configuradas de forma diferente
* se sintonizan por separado
* cada uno tiene su propio conjunto de pruebas de aceptación

En otras palabras, deben someterse a pruebas por separado y con casos de prueba diferentes.

**Personalización**

Al probar la personalización, cada caso de uso individual debe repetirse con varias cuentas de usuario para probar el comportamiento.

Compruebe también el comportamiento correcto en el almacenamiento en caché.

**El Dispatcher**

La mayoría de los proyectos instalan Dispatcher para el almacenamiento en caché y el equilibrio de carga.

Las pruebas son difíciles (el almacenamiento en caché se produce en varios niveles y en varias ubicaciones) y deben realizarse en una caja negra. Los aspectos clave para probar son los siguientes:

* **Precisión**
Garantiza que el visitante del sitio web vea las actualizaciones de contenido.

* **Continuidad**
Asegúrese de que el sitio web sigue estando disponible cuando se apaga un servidor.

* **Clústeres**
Se utiliza para proporcionar lo siguiente:

   * **Conmutación por error**
Si falla un servidor, los demás servidores del clúster se harán cargo del procesamiento.

   * **Rendimiento**
Equilibrio de carga con conmutación por error completa aumenta el rendimiento de un clúster.
Cuando se utiliza para un proyecto de cliente, el clúster debe probarse para confirmar el funcionamiento correcto de la configuración.

## Prueba de software de terceros {#testing-third-party-software}

Se hará referencia a cualquier software de terceros conectado a AEM en las especificaciones detalladas de los requisitos.

Se analizarán todos los ensayos necesarios (en función del ámbito de aplicación definido) y se obtendrán ensayos limpios.
