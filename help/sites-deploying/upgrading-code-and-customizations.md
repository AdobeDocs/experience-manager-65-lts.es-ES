---
title: Actualizar código y personalizaciones
description: Obtenga más información sobre la actualización de código y personalizaciones en AEM.
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 6b94caf1-97b7-4430-92f1-4f4d0415aef3
source-git-commit: f983fc1edc613feaa070c4e82a92aabab9d50cbb
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Actualizar código y personalizaciones{#upgrading-code-and-customizations}

Al planificar una actualización, se deben investigar y abordar las siguientes áreas de una implementación.

* [Actualizar la base de código](#upgrade-code-base)
* [Procedimiento de prueba](#testing-procedure)

## Información general {#overview}

1. **AEM Analyzer**: ejecute AEM Analyzer tal como se describe en la planificación de la actualización y se describe en detalle en la página [Evaluación de la complejidad de la actualización con AEM Analyzer](/help/sites-deploying/aem-analyzer.md). Recibirá un informe de AEM Analyzer que contiene más detalles sobre las áreas que deben abordarse, además de las API/paquetes no disponibles en la versión de Target de AEM. El informe de AEM Analyzer le proporciona una indicación de cualquier incompatibilidad en el código. Si no existe, la implementación ya es compatible con 6.5 LTS. Puede optar por realizar un nuevo desarrollo para utilizar la funcionalidad 6.5 LTS, pero no la necesita solo para mantener la compatibilidad.
1. **Desarrollar base de código para 6.5 LTS**- Crear una rama o repositorio dedicado para la base de código para la versión de Target. Utilice la información de Compatibilidad previa a la actualización para planificar las áreas de código que desea actualizar.
1. **Compile con 6.5 LTS Uber jar**- Actualice los POM de base de código para que apunten a 6.5 LTS uber jar y compile el código con él.
1. **Implementar en el entorno 6.5 LTS**: se debe instalar una instancia limpia de AEM 6.5 LTS (Autor + Publicación) en un entorno de desarrollo/control de calidad. Se debe implementar una base de código actualizada y una muestra representativa de contenido (de producción actual).
1. **Validación de control de calidad y corrección de errores**: el control de calidad debe validar la aplicación en las instancias de autor y publicación de 6.5 LTS Cualquier error encontrado debe corregirse y confirmarse con la base de código 6.5 LTS. Repita Dev-Cycle según sea necesario hasta que se corrijan todos los errores.

Antes de continuar con la actualización, debe tener una base de código de aplicación estable que se haya probado exhaustivamente con AEM 6.5 LTS.

## Actualizar la base de código {#upgrade-code-base}

### Crear una rama dedicada para el código LTS 6.5 en el control de versiones {#create-a-dedicated-branch-for-6.5-lts-code-in-version-control}

Todo el código y las configuraciones necesarios para la implementación de AEM deben administrarse mediante algún tipo de control de versiones. Se debe crear una rama dedicada en el control de versiones para administrar los cambios necesarios para el código base en la versión de destino de AEM. En esta rama se gestionan las pruebas iterativas del código base con la versión de destino de AEM y las correcciones de errores subsiguientes.

### Actualice la versión de AEM Uber Jar {#update-the-aem-uber-jar-version}

AEM Uber jar incluye todas las API de AEM como una sola dependencia en `pom.xml` de su proyecto Maven. Siempre es recomendable incluir Uber Jar como una sola dependencia en lugar de incluir dependencias de API de AEM individuales. Al actualizar el código base, cambie la versión de Uber Jar para que apunte a la versión 6.5 LTS de AEM. Actualice las API o los métodos obsoletos para que sean compatibles con la versión de destino de AEM. Recompile el código base con la nueva versión de Uber Jar.

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>Hay una ligera diferencia en la forma en que se empaquetan AEM 6.5 y AEM 6.5 LTS Uber Jars. Consulte la sección siguiente:

**Uber Jars para AEM 6.5**

1. `uber-jar-6.5.x.jar`: contiene todas las API públicas de AEM 6.5.
1. `uber-jar-6.5.x-apis-with-deprecations.jar`: incluye tanto API públicas como API obsoletas de AEM 6.5.

**Uber Jars for AEM 6.5 LTS**

Para AEM 6.5 LTS, hay de nuevo dos tipos de Uber Jars:

1. `uber-jar-6.6.x-apis.jar`: contiene todas las API públicas de AEM 6.5 LTS.
1. `uber-jar-6.6.x-deprecated-apis.jar`: solo incluye las API obsoletas de AEM 6.5 LTS.

**Diferencia clave: AEM 6.5 frente a AEM 6.5 LTS Uber Jars**

* En AEM 6.5, si se necesitan API públicas y obsoletas, puede utilizar incluir un solo jar, `uber-jar-6.5.x-apis-with-deprecations.jar`, en su archivo `pom.xml`.
* En AEM 6.5 LTS, si necesita API públicas y obsoletas, debe incluir dos Jars independientes, `uber-jar-6.6.x-apis.jar` para las API públicas y `uber-jar-6.6.x-deprecated-apis.jar` para las API obsoletas.

**Coordenadas Maven para Jar de API obsoletas**

```
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.0</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

### Notas del desarrollador {#developer-notes}

* AEM 6.5 LTS no incluye la biblioteca de guayaba de Google de forma predeterminada, la versión requerida se puede instalar según los requisitos.
* El paquete Sling XSS ahora utiliza la biblioteca Java HTML Sanitizer, y el uso del método `XSSAPI#filterHTML()` debe usarse para representar el contenido de HTML de forma segura y no para pasar datos a otras API.

## Procedimiento de prueba {#testing-procedure}

Se debe preparar un plan de pruebas completo para probar las actualizaciones. La aplicación y la base de código actualizadas deben probarse primero en entornos más bajos. Los errores encontrados deben corregirse de forma iterativa hasta que la base de código sea estable, solo entonces deben actualizarse los entornos de nivel superior.

### Prueba del procedimiento de actualización {#testing-upgrade-procedure}

El procedimiento de actualización como se describe aquí debe probarse en los entornos de desarrollo y control de calidad, tal como se documenta en su manual de ejecución personalizado (consulte [Planificación de la actualización](/help/sites-deploying/upgrade-planning.md)). El procedimiento de actualización debe repetirse hasta que todos los pasos estén documentados en el manual de ejecución de la actualización y el proceso de actualización sea fluido.

### Áreas de prueba de implementación  {#implementation-test-areas-}

A continuación, se muestran áreas críticas de cualquier implementación de AEM que deben incluirse en el plan de prueba una vez que se haya actualizado el entorno y se haya implementado la base de código actualizada.

<table>
 <tbody>
  <tr>
   <td><strong>Área de prueba funcional</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>Sitios publicados</td>
   <td>Probando la implementación de AEM y el código asociado en el nivel de publicación <br /> a través de Dispatcher. Debe incluir criterios para las actualizaciones de página y <br /> invalidación de caché.</td>
  </tr>
  <tr>
   <td>Creación</td>
   <td>Prueba de la implementación de AEM y del código asociado en el nivel de Author. Debe incluir la creación de páginas, componentes y cuadros de diálogo.</td>
  </tr>
  <tr>
   <td>Integraciones con las soluciones de Experience Cloud</td>
   <td>Validación de integraciones con productos como Analytics.</td>
  </tr>
  <tr>
   <td>Integraciones con sistemas de terceros</td>
   <td>Valide cualquier integración de terceros en los niveles de creación y publicación.</td>
  </tr>
  <tr>
   <td>Autenticación, seguridad y permisos</td>
   <td>Deben validarse todos los mecanismos de autenticación como LDAP/SAML.Los permisos y grupos de <br /> deben probarse en los niveles Author y Publish<br />.</td>
  </tr>
  <tr>
   <td>Consultas</td>
   <td>Los índices y consultas personalizados deben probarse junto con el rendimiento de las consultas.</td>
  </tr>
  <tr>
   <td>Personalizaciones de IU</td>
   <td>Extensiones o personalizaciones de la interfaz de usuario de AEM en el entorno de creación.</td>
  </tr>
  <tr>
   <td>Flujos de trabajo</td>
   <td>Flujos de trabajo y funcionalidad personalizados o listos para usar.</td>
  </tr>
  <tr>
   <td>Pruebas de rendimiento</td>
   <td>Las pruebas de carga deben realizarse en los niveles Author y Publish que simulan escenarios reales.</td>
  </tr>
 </tbody>
</table>

### Documentar el plan y los resultados de prueba {#document-test-plan-and-results}

Debe crearse un plan de pruebas que cubra las áreas de prueba de implementación mencionadas anteriormente. A menudo, tiene sentido separar el plan de prueba por las listas de tareas Autor y Publicar. Este plan de prueba debe ejecutarse en los entornos de desarrollo, control de calidad y ensayo antes de actualizar los entornos de producción. Los resultados de las pruebas y las métricas de rendimiento deben capturarse en entornos inferiores para proporcionar una comparación al actualizar los entornos de ensayo y producción.
