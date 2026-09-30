---
title: Herramientas de pruebas y seguimiento
description: AEM proporciona un marco de trabajo para probar la interfaz de usuario de los componentes y un mecanismo para probar y depurar componentes
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4aa0f10d-e915-4ad2-a886-080ed8b9b10f
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
source-wordcount: '293'
ht-degree: 5%
---
# Herramientas de pruebas y seguimiento{#testing-and-tracking-tools}

## Pruebas {#testing}

AEM proporciona lo siguiente:

* [un marco de trabajo para probar la IU del componente](/help/sites-developing/hobbes.md).
* [un mecanismo para probar y depurar componentes](/help/sites-developing/developer-mode.md).

Las siguientes son dos herramientas de prueba de Open Source:

**Selenio**

Selenium se utiliza para probar funciones en un navegador con un usuario por actividad. Registra los pasos de prueba (clics) como tablas HTML o clases Java™.

Para obtener más información, consulte [https://www.selenium.dev/](https://www.selenium.dev/).

**JMeter**

JMeter se utiliza para realizar un seguimiento de las solicitudes y puede utilizarse para pruebas funcionales, de rendimiento y de esfuerzo.

Para obtener más información, consulte [https://jmeter.apache.org/](https://jmeter.apache.org/).

También hay muchas herramientas propietarias para automatizar pruebas y administrar planes de prueba.

### Seguimiento {#tracking}

Las siguientes herramientas están disponibles fácilmente. Sin embargo, un problema clave en todos los casos es la disponibilidad de los datos para todos los miembros del equipo del proyecto: socio y cliente.

**Bugzilla**

Un sistema de seguimiento de errores que se puede configurar según sus propios requisitos.

**Hojas de cálculo**

Aunque no se trata específicamente de una herramienta de seguimiento de errores, las hojas de cálculo suelen *error* utilizarse para este fin, ya que son fáciles de entender y la mayoría de los usuarios tienen experiencia con su funcionalidad.

Si estas hojas de cálculo se utilizan para el seguimiento, entonces:

* deben mantenerse simples.
* el número de hojas de cálculo individuales debe reducirse al mínimo.
* deben actualizarse periódicamente.
* solo debe conservarse una copia principal, y todos deben saber dónde se encuentra.
* deben ser accesibles para todos los miembros del proyecto.
* si la seguridad es un problema (a menudo ocurre en grandes empresas) y el acceso común no es posible, entonces las copias pueden distribuirse siempre y cuando todos entiendan que estas hojas de cálculo son copias y no se pueden actualizar.

Una vez más, hay muchas herramientas propietarias para el seguimiento de errores y requisitos de funciones.
