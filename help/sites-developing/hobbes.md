---
title: Prueba de la IU
description: AEM proporciona un marco para automatizar pruebas para la interfaz de usuario de AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components, testing
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 73a3a6386a857eae1b7392d0fdf943b9b6799b33
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 1%

---

# Prueba de la IU{#testing-your-ui}

>[!NOTE]
>
>A partir de AEM 6.5, el marco de prueba de la interfaz de usuario de hobbes.js quedará obsoleto. Adobe no planea realizar más mejoras en él y recomienda a los clientes utilizar la automatización de Selenium.
>

AEM proporciona un marco para automatizar pruebas para la interfaz de usuario de AEM. Con el marco de trabajo, puede escribir y ejecutar pruebas de interfaz de usuario directamente en un explorador web. El marco de trabajo proporciona una API de JavaScript para crear pruebas.

El marco de prueba de AEM utiliza Hobbes.js, una biblioteca de prueba escrita en JavaScript. El marco de Hobbes.js se desarrolló para probar AEM como parte del proceso de desarrollo. El marco de trabajo ya está disponible para uso público para probar las aplicaciones de AEM.

>[!NOTE]
>
>Consulte la [documentación](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html) de Hobbes.js para obtener información detallada sobre la API.

## Estructura de las pruebas {#structure-of-tests}

Al utilizar pruebas automatizadas en AEM, es importante comprender los siguientes términos:

| Acción | Una **acción** es una actividad específica de una página web, como hacer clic en un vínculo o en un botón. |
|---|---|
| Caso de prueba | Un **caso de prueba** es una situación específica que puede estar compuesta por una o más **acciones**. |
| Grupo de pruebas | Un **grupo de pruebas** es un grupo de **casos de prueba** relacionados que juntos prueban un caso de uso específico. |

## Ejecución de pruebas {#executing-tests}

### Visualización de grupos de pruebas {#viewing-test-suites}

Abra la consola de pruebas para ver los grupos de pruebas registrados. El panel Pruebas contiene una lista de los grupos de pruebas y sus casos de prueba.

Vaya a la consola Herramientas mediante **Navegación global > Herramientas > Operaciones > Pruebas**.

![chlimage_1-63](assets/chlimage_1-63.png)

Al abrir la consola, los grupos de pruebas se muestran a la izquierda junto con una opción para ejecutarlos todos secuencialmente. El espacio a la derecha que se muestra con un fondo a cuadros es un marcador de posición para mostrar el contenido de la página mientras se ejecutan las pruebas.

![chlimage_1-64](assets/chlimage_1-64.png)

### Ejecutar un único grupo de pruebas {#running-a-single-test-suite}

Los grupos de pruebas se pueden ejecutar individualmente. Al ejecutar un grupo de pruebas, la página cambia a medida que se ejecutan los casos de prueba y sus acciones, y los resultados aparecen después de finalizar la prueba. Los iconos indican los resultados.

Un icono de marca de verificación indica que la prueba se ha superado:

![Icono de marca de verificación.](do-not-localize/chlimage_1-2.png)

El icono &quot;X&quot; indica que la prueba ha fallado:

![Icono de prueba con error indicado por una X dentro de un círculo.](do-not-localize/chlimage_1-3.png)

Para ejecutar un grupo de pruebas:

1. En el panel Pruebas, haga clic en el nombre del caso de prueba que desea ejecutar para expandir los detalles de las acciones.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Haga clic en **Ejecutar prueba**.

   ![Imagen del botón Ejecutar pruebas, indicada por un puntero orientado a la derecha dentro de un círculo.](do-not-localize/chlimage_1-4.png)

1. El marcador de posición se reemplaza por el contenido de la página mientras se ejecuta la prueba.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Revise los resultados del caso de prueba tocando o haciendo clic en la descripción para abrir el panel **Resultado**. Al tocar o hacer clic en el nombre del caso de prueba en el panel **Resultado**, se muestran todos los detalles.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Ejecución de varias pruebas {#running-multiple-tests}

Los grupos de pruebas se ejecutan secuencialmente en el orden en que aparecen en la consola. Puede explorar en profundidad una prueba para ver los resultados detallados.

![chlimage_1-68](assets/chlimage_1-68.png)

1. En el panel Pruebas, haga clic en el botón **Ejecutar todas las pruebas** o en el botón **Ejecutar pruebas** situado debajo del título del grupo de pruebas que desee ejecutar.

   ![Imagen del botón Ejecutar todas las pruebas y del botón Ejecutar pruebas, indicados por un puntero derecho dentro de un círculo.](do-not-localize/chlimage_1-5.png)

1. Para ver los resultados de cada caso de prueba, haga clic en el título del caso de prueba. Al hacer clic en el nombre de la prueba en el panel **Result**, se muestran todos los detalles.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Crear y usar un grupo de pruebas simple {#creating-and-using-a-simple-test-suite}

El siguiente procedimiento lo guía durante la creación y ejecución de un grupo de pruebas con [contenido de We.Retail](/help/sites-developing/we-retail.md), pero puede modificar fácilmente la prueba para que utilice una página web diferente.

Para obtener información detallada sobre cómo crear sus propios grupos de pruebas, consulte la [documentación de la API de Hobbes.js](https://developer.adobe.com/experience-manager/reference-materials/6-5/test-api/index.html).

1. Abra CRXDE Lite. ([https://localhost:4502/crx/de](https://localhost:4502/crx/de))
1. Haga clic con el botón derecho en la carpeta `/etc/clientlibs` y haga clic en **Crear > Crear carpeta**. Escriba `myTests` para el nombre y haga clic en **Aceptar**.
1. Haga clic con el botón derecho en la carpeta `/etc/clientlibs/myTests` y haga clic en **Crear > Crear nodo**. Use los siguientes valores de propiedad y haga clic en **Aceptar**:

   * Nombre: `myFirstTest`
   * Tipo: `cq:ClientLibraryFolder`

1. Agregue las siguientes propiedades al nodo myFirstTest:

   | Nombre | Tipo | Valor  |
   |---|---|---|
   | `categories` | Cadena [] | `granite.testing.hobbes.tests` |
   | `dependencies` | Cadena [] | `granite.testing.hobbes.testrunner` |

   >[!NOTE]
   >
   >**Solo AEM Forms**
   >
   >
   >Para probar los formularios adaptables, agregue los siguientes valores a las categorías y dependencias. Por ejemplo:
   >
   >
   >**categorías**: `granite.testing.hobbes.tests, granite.testing.hobbes.af.commons`
   >
   >
   >**dependencias**: `granite.testing.hobbes.testrunner, granite.testing.hobbes.af`

1. Haga clic en **Guardar todo**.
1. Haga clic con el botón derecho en el nodo `myFirstTest` y haga clic en **Crear > Crear archivo**. Asigne un nombre al archivo `js.txt` y haga clic en **Aceptar**.
1. En el archivo `js.txt`, escriba el siguiente texto:

   ```
   #base=.
   myTestSuite.js
   ```

1. Haga clic en **Guardar todo** y, a continuación, cierre el archivo `js.txt`.
1. Haga clic con el botón derecho en el nodo `myFirstTest` y haga clic en **Crear > Crear archivo**. Asigne un nombre al archivo `myTestSuite.js` y haga clic en **Aceptar**.
1. Copie el siguiente código en el archivo `myTestSuite.js` y, a continuación, guarde el archivo:

   ```
   new hobs.TestSuite("Experience Content Test Suite", {path:"/etc/clientlibs/myTests/myFirstTest/myTestSuite.js"})
      .addTestCase(new hobs.TestCase("Navigate to Experience Content")
         .navigateTo("/content/we-retail/us/en/experience/arctic-surfing-in-lofoten.html")
      )
      .addTestCase(new hobs.TestCase("Hover Over Topnav")
         .mouseover("li.visible-xs")
      )
      .addTestCase(new hobs.TestCase("Click Topnav Link")
         .click("li.active a")
   );
   ```

1. Vaya a la consola **Pruebas** para probar el grupo de pruebas.
