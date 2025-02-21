---
title: Crear lanzamientos
description: Puede crear un lanzamiento para poder actualizar las páginas web existentes a una versión nueva que se activará más adelante.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Launches
role: User,Admin,Architect,Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 77%

---

# Crear lanzamientos{#creating-launches}

Cree un lanzamiento para poder actualizar las páginas web existentes a la versión nueva que se activará más adelante. Al crear un lanzamiento, especificará un título y la página de origen:

* El título aparece en el carril [Referencias](/help/sites-authoring/author-environment-tools.md#references); desde allí, los autores pueden acceder al título y trabajar con él.
* Las páginas secundarias de la página de origen se incluyen en el lanzamiento de forma predeterminada. Si lo desea, puede utilizar únicamente la página de origen.
* De forma predeterminada, [Live Copy](/help/sites-administering/msm.md) actualiza automáticamente las páginas de lanzamiento a medida que cambian las páginas de origen. Puede especificar que se cree una copia estática para evitar cambios automáticos.

De forma opcional, puede especificar la **fecha de lanzamiento** (y hora) para establecer cuándo se promocionarán y activarán las páginas. Sin embargo, la **fecha de lanzamiento** solo funciona en combinación con el indicador **Producción lista** (consulte [Edición de la configuración de un lanzamiento](/help/sites-authoring/launches-editing.md#editing-a-launch-configuration)); para que las acciones se produzcan de forma automática, se deben configurar ambas.

## Creación de un lanzamiento {#creating-a-launch}

Puede crear un lanzamiento desde la consola Sites o Lanzamientos:

1. Abra cualquiera de las consolas **Sites** o **Lanzamientos**.

   >[!NOTE]
   >
   >Al usar la consola **Sites** es habitual desplazarse a la ubicación de la página de origen, pero esto no es obligatorio, ya que puede navegar al seleccionar el **Origen de lanzamiento** en el asistente.

1. Según la consola que utilice:

   * **Lanzamientos**:

      1. Seleccione **Crear lanzamiento** en la barra de herramientas para abrir el asistente.

   * **Sites**:

      1. Seleccione **Crear** en la barra de herramientas para abrir el cuadro de selección.
      1. A continuación, seleccione **Crear lanzamiento** para abrir el asistente.

   >[!NOTE]
   >
   >En la consola de **Sites** también puede utilizar el [modo de selección](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources) para seleccionar una página antes de hace clic en **Crear**.
   >
   >La página seleccionada se utilizará como página de origen inicial.

1. En el paso **Seleccionar origen**, debe **Añadir páginas**. Puede seleccionar varias páginas, pero debe especificar la ruta de acceso de cada una de ellas:

   * Vaya a la ubicación requerida.
   * Seleccione las páginas de origen y confirme (marca de verificación).

   Repita el proceso tantas veces como sea necesario.

   ![Seleccionar origen y agregar páginas](assets/chlimage_1-225.png)

   >[!NOTE]
   >
   >Las páginas o ramas que se deseen añadir a un lanzamiento deben estar dentro de un sitio; es decir, por debajo de una raíz de nivel superior común.
   >
   >Si un sitio contiene raíces de idioma por debajo del nivel superior, las páginas y ramas de un lanzamiento deben estar por debajo de una raíz de idioma común.
   >
   >Si intenta crear un lanzamiento con una página principal o secundaria en la ruta de origen, se producirá un error y se devolverá el error &quot;El destino ya existe en :ruta de acceso a la página&quot;.

1. Para cada entrada, puede especificar lo siguiente:

   * **Incluir páginas secundarias**:

      * Especifique si desea crear un lanzamiento con o sin las páginas secundarias.  De forma predeterminada, se incluyen estas subpáginas.

   Continúe con **Siguiente**.

   ![Especifique si desea incluir las páginas](assets/chlimage_1-226.png)

1. En el paso **Propiedades** del asistente, puede especificar lo siguiente:

   * **Título del lanzamiento**: el nombre del lanzamiento. El nombre debe ser significativo para los autores.
   * **Con contenido existente**: el contenido original se utiliza para crear el lanzamiento.
   * **utilice una plantilla nueva para sustituir la página**: consulte [Creación de un lanzamiento con una plantilla nueva](#create-launch-with-new-template) para obtener más información.
   * **Heredar los datos publicados de la página de origen**: seleccione esta opción para actualizar automáticamente el contenido de las páginas de lanzamiento cuando cambien las páginas de origen. Para conseguirlo, esta opción convierte el lanzamiento en [live copy](/help/sites-administering/msm.md).

     Esta opción está seleccionada de forma predeterminada.

   * **Fecha del lanzamiento**: la fecha y hora en que la copia de lanzamiento se debe activar (depende del indicador **Producción lista**; consulte [Lanzamientos: orden de los eventos](/help/sites-authoring/launches.md#launches-the-order-of-events)).

   ![Especificar propiedades](assets/chlimage_1-227.png)

1. Utilice **Crear** para completar el proceso y crear el nuevo lanzamiento. El cuadro de diálogo de confirmación le preguntará si desea abrir el lanzamiento inmediatamente.

   Si devuelve la consola (con **Listo**) puede ver (y acceder) al lanzamiento desde las ubicaciones siguientes:

   * la consola [**Lanzamientos**](/help/sites-authoring/launches.md#the-launches-console)
   * las [**referencias** en la consola **Sitios**](/help/sites-authoring/launches.md#launches-in-references-sites-console)

### Creación de un lanzamiento con una plantilla nueva {#create-launch-with-new-template}

Al [crear un lanzamiento](/help/sites-authoring/launches-creating.md#create-launch-with-new-template), puede seleccionar si desea utilizar una plantilla nueva con la opción: **usar una plantilla nueva para reemplazar la página**

>[!CAUTION]
>
>Esta opción solo está disponible al crear un lanzamiento desde la consola **Sitios**. No está disponible al crear un lanzamiento desde la consola **Lanzamientos**.

![Use una plantilla nueva para reemplazar la página](assets/chlimage_1-228.png)

Al seleccionar esto, ocurrirá lo siguiente:

* actualizar las demás opciones disponibles,
* incluya un nuevo paso en el que puede seleccionar la plantilla requerida.

![Seleccionar plantilla](assets/chlimage_1-229.png)

>[!CAUTION]
>
>Como se utiliza una plantilla diferente, la nueva página estará vacía. Debido a la diferente estructura de la página, no se copia ningún contenido.
>
>Este mecanismo se puede utilizar para cambiar la plantilla de una [página existente](/help/sites-authoring/managing-pages.md#creating-a-new-page): sin embargo, debe tenerse en cuenta la pérdida de contenido.

### Creación de un lanzamiento anidado {#creating-a-nested-launch}

Crear un lanzamiento anidado (un lanzamiento dentro de otro lanzamiento) le ofrece la posibilidad de crear un lanzamiento a partir de un lanzamiento existente, de modo que los autores pueden aprovechar los cambios que ya se hayan realizado, en lugar de tener que realizar los mismos cambios varias veces en cada lanzamiento.

>[!NOTE]
>
>Consulte también [Promoción de un lanzamiento anidado](/help/sites-authoring/launches-promoting.md#promoting-a-nested-launch).

#### Creación de un lanzamiento anidado: consola Lanzamientos {#creating-a-nested-launch-launches-console}

Crear un lanzamiento anidado desde la consola **Lanzamientos** es básicamente lo mismo que crear cualquier otra forma de lanzamiento, con la excepción de que debe desplazarse a la rama de lanzamientos `/content/launches`:

1. En la consola **Lanzamientos**, seleccione **Crear**.
1. Seleccione **Agregar páginas** y, a continuación, vaya a la rama de lanzamientos especificando `/content/launches` en el filtro. Seleccione el lanzamiento necesario y confirme con la opción **Seleccionar**:

   ![Seleccionar lanzamiento](assets/chlimage_1-230.png)

1. Continúe con **Siguiente** y complete las **Propiedades** como con cualquier otro lanzamiento.

   ![Especificar propiedades](assets/chlimage_1-231.png)

#### Creación de un lanzamiento anidado: consola Sites {#creating-a-nested-launch-sites-console}

Para crear un lanzamiento anidado desde la consola **Sites** basado en un lanzamiento existente:

1. Acceda a [Lanzamiento desde las referencias (consola Sites)](/help/sites-authoring/launches.md#launches-in-references-sites-console) para mostrar las acciones disponibles.
1. Seleccione **Crear lanzamiento** para abrir el asistente (como el origen ya se ha seleccionado, se omitirá el paso **Seleccionar origen**).

1. Introduzca el **título del lanzamiento** y cualquier otra información necesaria (como con un lanzamiento normal).

1. Utilice **Crear** para completar el proceso y crear el nuevo lanzamiento. El cuadro de diálogo de confirmación le preguntará si desea abrir el lanzamiento inmediatamente.

   Si selecciona **Listo**, volverá al carril **Referencias** de la **consola de Sites**, si selecciona la página adecuada en la que se muestra el nuevo lanzamiento.

### Clonación de un lanzamiento {#cloning-a-launch}

Puede clonar un lanzamiento desde la [consola de lanzamientos](/help/sites-authoring/launches.md#the-launches-console):

* Para seleccionar el lanzamiento, toque o haga clic en la miniatura.
* Aparecerá la barra de herramientas. Seleccione Clonar.
   * El clon se crea y se muestra en la consola.
   * El **Título de lanzamiento** indicará que es un clon. Puede actualizar el título editando la [Configuración de lanzamiento](/help/sites-authoring/launches-editing.md#editing-a-launch-configuration) (**Propiedades**).

## Eliminación de un lanzamiento {#deleting-a-launch}

Puede eliminar un lanzamiento desde la [consola de lanzamientos](/help/sites-authoring/launches.md#the-launches-console):

* Para seleccionar el lanzamiento, toque o haga clic en la miniatura.
* Se mostrará la barra de herramientas: seleccione Eliminar.
* Confirme la acción.

>[!CAUTION]
>
>Al eliminar un lanzamiento, se quitarán el lanzamiento en sí y todos los lanzamientos anidados descendentes.
