---
title: Arquitectura de software
description: Conozca algunas prácticas recomendadas para crear su software para Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Arquitectura de software{#software-architecture}

## Diseño para actualizaciones {#design-for-upgrades}

Al ampliar los comportamientos predeterminados, es importante tener en cuenta las actualizaciones. Aplique siempre las personalizaciones en el directorio /apps y superponga los nodos correspondientes en el directorio /libs o utilice sling:resourceSuperType para ampliar el comportamiento predeterminado. Aunque pueden ser necesarias algunas modificaciones para admitir una nueva versión de AEM, esta no debe sobrescribir las personalizaciones si se sigue esta práctica.

### Reutilizar plantillas y componentes siempre que sea posible {#reuse-template-and-components-when-possible}

Al hacerlo, el sitio puede mantener una apariencia más coherente y simplificar el mantenimiento del código. Cuando se necesite una plantilla nueva, asegúrese de ampliarla desde una plantilla base compartida para que los requisitos globales, como la inclusión clientlib, se puedan codificar en un solo lugar. Cuando se necesite un nuevo componente, busque oportunidades para ampliarse desde un componente existente.

### Diseñar diseños de plantilla {#design-template-designs}

Al definir qué componentes se pueden incluir en cada parsys de la página, se puede controlar la coherencia de la apariencia del sitio. Al restringir el acceso al diseño en las páginas, se puede permitir a los &quot;superautores&quot; modificar los componentes permitidos por página sin la intervención del desarrollador, siempre que los demás autores sigan los estándares corporativos.

### Desarrollar una arquitectura sólida {#develop-a-solid-architecture}

SOLID es un acrónimo que describe cinco principios arquitectónicos a los que hay que adherirse:

* **S** Principio de responsabilidad único: cada módulo, clase, método, etc., solo debe tener una responsabilidad.
* **O** Principio abierto/Cerrado: los módulos deben estar abiertos para su extensión y cerrados para su modificación.
* **L** principio de sustitución de iskov: los tipos deben ser reemplazables por sus subtipos.
* **I** Principio de segmentación de interfaz: no se debe obligar a ningún cliente a depender de métodos que no utiliza.
* Principio de inversión de dependencia **D** Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambas deberían depender de abstracciones. Las abstracciones no deben depender de los detalles. Los detalles deben depender de las abstracciones.

La lucha por el cumplimiento de estos cinco principios debería dar como resultado un sistema que tenga una estricta separación de intereses.

>[!TIP]
>
>SOLID es un concepto comúnmente utilizado en la programación orientada a objetos y cada elemento es ampliamente discutido en la literatura de la industria.
>
>Esta información es solo un breve resumen presentado para la concienciación y se le anima a familiarizarse con estos conceptos en más profundidad.

### Siga el principio de solidez {#follow-the-robustness-principle}

El Principio de Solidez establece que debes ser conservador en lo que envías, pero ser liberal en lo que aceptas. En otras palabras, al enviar mensajes a un tercero, debe cumplir completamente con las especificaciones. Sin embargo, cuando reciba mensajes de terceros, debe aceptar mensajes no conformes siempre que el significado del mensaje sea claro.

### Implementar picos en sus propios módulos {#implement-spikes-in-their-own-modules}

Los picos y el código de prueba forman parte de cualquier implementación de software de Agile. Sin embargo, debe asegurarse de que no entren en la base del código de producción sin el nivel de supervisión adecuado. Como resultado, se recomienda que los picos se creen en su propio módulo.

### Implementar scripts de migración de datos en su propio módulo {#implement-data-migration-scripts-in-their-own-module}

Los scripts de migración de datos, mientras que el código de producción, se ejecutan solo una vez al primer inicio de un sitio. Por lo tanto, cuando el sitio está activo, los scripts se convierten en código muerto. Para asegurarse de no generar código de implementación que dependa de los scripts de migración, estos deben implementarse en su propio módulo. Al hacerlo, podemos eliminar y retirar este código inmediatamente después del lanzamiento, eliminando el código inactivo del sistema.

### Seguir convenciones de Maven publicadas en archivos POM {#follow-published-maven-conventions-in-pom-files}

Apache ha publicado convenciones de estilo en [https://maven.apache.org/developers/conventions/code.html](https://maven.apache.org/developers/conventions/code.html). Es mejor seguir estas convenciones porque facilita que los nuevos recursos se pongan al día rápidamente.
