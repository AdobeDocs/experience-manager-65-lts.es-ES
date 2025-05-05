---
title: Aplicar estilos dentro de la línea a los componentes de un formulario adaptable
description: Aunque puede aplicar estilos personalizados a un formulario adaptable, también puede aplicar propiedades CSS en línea a los componentes individuales de un formulario adaptable.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 99%

---

# Aplicar estilos dentro de la línea a los componentes de un formulario adaptable {#inline-styling-of-adaptive-form-components}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html?lang=es) |
| AEM 6.5 | Este artículo |

Puede definir el aspecto y el estilo generales de un formulario adaptable especificando los estilos mediante el [Editor de temas](../../forms/using/themes.md). Además, puede aplicar estilos CSS en línea a componentes de formulario adaptable individuales y previsualizar los cambios sobre la marcha. Los estilos en línea reemplazan el estilo proporcionado en el tema.

## Aplicar propiedades CSS en línea {#apply-inline-css-properties}

Para añadir estilos en línea a un componente:

1. Abra el formulario en el Editor de formularios y cambie el modo al modo Estilo. Para cambiar el modo al modo de estilo, en la barra de herramientas de la página, seleccione ![canvas-drop-down](assets/canvas-drop-down.png) > **Estilo**.
1. Seleccione un componente de la página y seleccione el botón Editar ![edit-button](assets/edit-button.png). Las propiedades del estilo se abren en la barra lateral.

   También puede seleccionar componentes en el árbol de jerarquía del formulario de la barra lateral. El árbol de jerarquía del formulario está disponible como Objetos del formulario en la barra lateral.

   También puede seleccionar un componente en la barra lateral. En el modo Estilo, puede ver los componentes que aparecen en Objetos de formulario. Sin embargo, la lista Objetos de formulario de la barra lateral muestra componentes como los campos y los paneles. Los campos y los paneles son componentes genéricos que pueden contener otros componentes como, por ejemplo, cuadros de texto y botones de opción.

   Cuando seleccione un componente en la barra lateral, verá una lista de todos los subcomponentes y las propiedades del componente seleccionado. Puede seleccionar un subcomponente específico y aplicarle un estilo.

1. Haga clic en una de las pestañas de la barra lateral para especificar las propiedades CSS. Puede especificar propiedades como las siguientes:

   * Dimensiones y posición (Mostrar configuración, relleno, altura, anchura, margen, posición, índice Z, flotante, borrar, desbordamiento)
   * Texto (Familia de fuentes, grosor, color, tamaño, altura de línea y alineación)
   * Fondo (Imagen y degradado, color de fondo)
   * Borde (Anchura, estilo, color, radio)
   * Efectos (Sombra, Opacidad)
   * Avanzadas (Permite escribir CSS personalizado para el componente)

1. Del mismo modo, puede aplicar estilos a otras partes de un componente, como Widget, Pie de ilustración y Ayuda.
1. Seleccione **Listo** para confirmar los cambios o **Cancelar** para descartarlos.

## Ejemplo: estilos en línea de un componente de campo {#example-inline-styles-for-a-field-component}

Las siguientes imágenes muestran un campo de texto antes y después de que se le apliquen estilos en línea.

![Componente de cuadro de texto antes de aplicar un estilo en línea](assets/no-style.png)

Componente de cuadro de texto antes de aplicar propiedades de estilo en línea

Observe el cambio en el estilo del cuadro de texto después de aplicar las siguientes propiedades CSS, como se muestra en la imagen.

<table>
 <tbody>
  <tr>
   <td><p>Selector</p> </td>
   <td><p>Propiedad CSS</p> </td>
   <td><p>Valor</p> </td>
   <td><p>Efecto</p> </td>
  </tr>
  <tr>
   <td><p>Campo</p> </td>
   <td><p>border</p> </td>
   <td><p>Border width =2px</p> <p>Border style=Solid</p> <p>Border color=#1111</p> </td>
   <td><p>Crea un borde ancho negro de 2 píxeles alrededor del campo</p> </td>
  </tr>
  <tr>
   <td><p>Cuadro de texto</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Cambia el color de fondo a CornflowerBlue (#6495ED)</p> <p>Nota: Puede especificar un nombre de color o su código hexadecimal en el campo del valor.</p> </td>
  </tr>
  <tr>
   <td><p>Etiqueta</p> </td>
   <td><p>Dimensiones y posición &gt; anchura</p> </td>
   <td><p>100px</p> </td>
   <td><p>Fija la anchura en 100 píxeles para la etiqueta</p> </td>
  </tr>
  <tr>
   <td>Icono de ayuda de campo</td>
   <td>Texto &gt; Color de fuente</td>
   <td>#2ECC40</td>
   <td>Cambia el color de la cara del icono de ayuda.</td>
  </tr>
  <tr>
   <td><p>Descripción larga</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Alinea la descripción larga para centrar la ayuda.</p> </td>
  </tr>
 </tbody>
</table>

![Estilo de cuadro de texto después de aplicar un estilo en línea](assets/applied-style.png)

Componente de cuadro de texto después de aplicar propiedades de estilo en línea

Siguiendo los pasos anteriores, puede seleccionar y aplicar estilos a otros componentes, como paneles, botones de envío y botones de opción.

>[!NOTE]
>
>Las propiedades del estilo varían en función del componente que selecciona.
