---
title: Prácticas recomendadas para plantillas de correo electrónico
description: Encuentre prácticas recomendadas sobre la creación de plantillas de correo electrónico en AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration, best-practices
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 1%

---


# Prácticas recomendadas para plantillas de correo electrónico {#best-practices-for-email-templates}

>[!CAUTION]
>
>Este artículo se aplica a los componentes de base obsoletos basados en los componentes de correo electrónico de AEM.
>
>Se recomienda a los usuarios utilizar los [componentes principales y componentes de correo electrónico modernos.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/email/introduction.html)

Este documento describe algunas de las prácticas recomendadas en cuanto al diseño de correos electrónicos, lo que da como resultado una plantilla de campaña de correo electrónico bien desarrollada.

La campaña de demostración disponible en AEM sigue todas estas prácticas recomendadas. Se describe cómo se implementan las prácticas recomendadas en la campaña de demostración para cada práctica recomendada.

Siga estas prácticas recomendadas al crear su propia newsletter.

>[!NOTE]
>
>Todo el contenido de la campaña debe crearse en una página de `master` de tipo `cq/personalization/components/ambitpage`.
>
>Por ejemplo, si la estructura de la campaña planificada es similar a
>
>`/content/campaigns/teasers/en/campaign-promotion-global`
>
>Asegúrese de que reside en una página de `master`
>
>`/content/campaigns/teasers/master/en/campaign-promotion-global`

>[!NOTE]
>
>Al crear una plantilla de correo electrónico para Adobe Campaign, debe incluir la propiedad **acMapping** con el valor **mapRecipient** en el nodo **jcr:content** de la plantilla. Si no lo hace, no podrá seleccionar la plantilla Adobe Campaign en **Propiedades de página** de Experience Manager (el campo está deshabilitado).

## Componente de plantilla/página {#template-page-component}

***/libs/mcm/campaign/components/campaign_newsletterpage***

<table>
 <tbody>
  <tr>
   <td><strong>Práctica recomendada</strong></td>
   <td><strong>Implementación</strong></td>
  </tr>
  <tr>
   <td><p>Especifique el tipo de documento para garantizar una representación coherente.</p> <p>Agregar DOCTYPE al principio (HTML o XHTML)</p> </td>
   <td><p>Se puede configurar por diseño cambiando la propiedad <i>cq:doctype</i> en <i>"/etc/designs/default/jcr:content/campaign_newsletterpage"</i></p> <p>El valor predeterminado es "XHTML":</p> <p>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 transition/EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;</p> <p>Se puede cambiar a "HTML_5":</p> <p>&lt;!DOCTYPE HTML&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Especifique la definición de caracteres para garantizar la correcta representación de los caracteres especiales.</p> <p>Agregue la declaración CHARSET (por ejemplo, iso-8859-15, UTF-8) a &lt;head&gt;</p> </td>
   <td><p>Se establece en UTF-8.</p> <p>&lt;meta http-equiv="content-type" content="text/html; charset=UTF-8"&gt;</p> </td>
  </tr>
  <tr>
   <td><p>Codifique toda la estructura utilizando el elemento &lt;table&gt;. Para diseños más complicados, debe anidar tablas para crear estructuras complejas.</p> <p>El correo electrónico debería verse bien incluso sin css.</p> </td>
   <td><p>Las tablas se utilizan en toda la plantilla para estructurar el contenido. Actualmente se utiliza un máximo de cuatro tablas anidadas (1 tabla base + máx. 3 niveles de anidación)</p> <p>Las etiquetas &lt;div&gt; solo se utilizan en el modo de autor para garantizar la correcta edición de los componentes.</p> </td>
  </tr>
  <tr>
   <td>Utilice atributos de elemento (como relleno de celda, validación y anchura) para establecer las dimensiones de la tabla. Este método fuerza una estructura de modelo de cuadro.</td>
   <td><p>Todas las tablas contienen atributos necesarios como <i>border</i>, <i>cellpadding</i>, <i>cellspacing</i> y <i>width</i>.</p> <p>Para armonizar la colocación de elementos dentro de las tablas, todas las celdas de la tabla tienen establecido el atributo <i>valign="top"</i>.</p> </td>
  </tr>
  <tr>
   <td><p>Tenga en cuenta la compatibilidad con dispositivos móviles, si es posible. Utilice consultas de medios para aumentar el tamaño del texto en pantallas pequeñas y proporcione áreas de visita en miniatura para los vínculos.</p> <p>Hacer que un correo electrónico sea adaptable si el diseño lo permite.</p> </td>
   <td>En la medida en que los estilos CSS se utilizan para ilustrar el diseño de demostración, las consultas de medios se utilizan para ofrecer una versión compatible con dispositivos móviles.</td>
  </tr>
  <tr>
   <td>CSS en línea es mejor que colocar todo el CSS al principio.</td>
   <td><p>Para mostrar mejor la estructura subyacente de HTML y facilitar la posibilidad de personalizar la estructura del boletín, solo se han insertado algunas definiciones CSS.</p> <p>Los estilos base y las variaciones de plantilla se han extraído a un bloque de estilo en el &lt;head&gt; de la página. Al enviar la newsletter final, estas definiciones de CSS se insertan en HTML. Se ha planificado un mecanismo de inline automático, pero actualmente no está disponible.</p> </td>
  </tr>
  <tr>
   <td>Simplifique el código CSS. Evite las declaraciones de estilos compuestos, el código abreviado, las propiedades de diseño CSS, los selectores complejos y los pseudoelementos.</td>
   <td>En cuanto a los estilos CSS que se utilizan para ilustrar el diseño de demostración, se siguen las recomendaciones CSS.</td>
  </tr>
  <tr>
   <td>Los correos electrónicos deben tener una anchura máxima de 600-800 píxeles. Este tamaño hace que se comporten mejor dentro del tamaño del panel de vista previa proporcionado por muchos clientes.</td>
   <td>La <i>anchura</i> de la tabla de contenido está limitada a 600 píxeles en el diseño de demostración.</td>
  </tr>
 </tbody>
</table>

### Imágenes {#images}

/libs/mcm/campaign/components/image

| **Prácticas recomendadas** | **Implementación** |
|---|---|
| Agregar atributos *alt* a imágenes | El atributo *alt* se ha definido como obligatorio para el componente de imagen. |
| Usar *jpg* en lugar del formato *png* para imágenes | El componente de imagen siempre sirve las imágenes como JPG. |
| Utilice el elemento `<img>` en lugar de imágenes de fondo en una tabla. | No se utilizan datos de imagen de fondo en las plantillas. |
| Añadir el atributo style=&quot;display block&quot; en las imágenes. Al hacerlo, se muestran bien en Gmail. | Todas las imágenes contienen de forma predeterminada el atributo *style=&quot;display block&quot;*. |

### Texto y vínculos {#text-and-links}

/libs/mcm/campaign/components/heading, /libs/mcm/campaign/components/textimage

<table>
 <tbody>
  <tr>
   <td><strong>Práctica recomendada</strong></td>
   <td><strong>Implementación</strong></td>
  </tr>
  <tr>
   <td>Utilice html &lt;font&gt; en lugar de estilo en CSS (font-family)</td>
   <td>RichTextEditor (por ejemplo, en el componente textimage) ahora admite la selección y aplicación de familias de fuentes y tamaños de fuente a textos seleccionados. Se representan como etiquetas &lt;font&gt;.</td>
  </tr>
  <tr>
   <td>Utilice fuentes básicas en varias plataformas, como <i>Arial®, Verdana, Georgia</i> y <i>Times New Roman®</i>.</td>
   <td><p>Depende del diseño de la newsletter.</p> <p>Para el diseño de demostración, se utiliza la fuente "Helvetica®", pero vuelve a una fuente sans-serif genérica, si no está presente.</p> </td>
  </tr>
 </tbody>
</table>

### Genérica {#generic}

| **Prácticas recomendadas** | **Implementación** |
|---|---|
| Utilice el validador W3C para corregir el código HTML. Asegúrese de que todas las etiquetas abiertas estén correctamente cerradas. | Se ha validado el código. Solo para el tipo de documento transitorio XHTML, falta el atributo xmlns que falta para el elemento `<html>`. |
| Evite utilizar JavaScript o Flash: estas tecnologías suelen ser incompatibles con los clientes de correo electrónico. | JavaScript o Flash no se utilizan en la plantilla del boletín informativo. |
| Añada una versión de texto sin formato para el envío de varias partes. | Se ha incorporado un nuevo widget en las propiedades de la página para extraer fácilmente una versión de texto sin formato del contenido de la página. Puede utilizarlo como punto de partida para la versión final de texto sin formato. |

## Plantillas y ejemplos de newsletter de Campaign {#campaign-newsletter-templates-and-examples}

AEM incluye varias plantillas y componentes predeterminados para que pueda crear boletines de campaña. Puede utilizar estas plantillas y componentes para crear sus boletines personalizados.

### Plantillas {#templates}

Para ofrecer una base sólida y ampliar la variedad de posibilidades de flujo de contenido, hay tres tipos de plantillas ligeramente diferentes disponibles de forma predeterminada. Puede utilizar fácilmente estos tres tipos para crear un boletín informativo personalizado.

Todos tienen una sección **header**, **footer** y **body**. Debajo de la sección del cuerpo, cada plantilla difiere en **diseño de columna** (una, dos o tres columnas).

![Variantes de posibles boletines](assets/chlimage_1-69.png)

### Componentes {#components}

Actualmente hay [siete componentes disponibles para usar en plantillas de campaña](/help/sites-authoring/adobe-campaign-components.md). Todos estos componentes se basan en el lenguaje de marcado Adobe **HTL**.

| **Nombre del componente** | **Ruta del componente** |
|---|---|
| Encabezado | /libs/mcm/campaign/components/heading |
| Imagen | /libs/mcm/campaign/components/image |
| Text&amp;Personalization | /libs/mcm/campaign/components/personalization |
| Textimage | /libs/mcm/campaign/components/textimage |
| Vínculo | /libs/mcm/campaign/components/reference |
| Plantilla de imagen de Dynamic Media Classic (anteriormente Scene7) | /libs/mcm/campaign/s7image |
| Referencia de destino | /libs/mcm/campaign/components/reference |

>[!NOTE]
>
>Estos componentes están optimizados para el contenido del correo; es decir, se adhieren a las prácticas recomendadas descritas en este documento. El uso de otros componentes listos para usar generalmente infringe estas reglas.

Estos componentes se describen detalladamente en [componentes de Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md).
