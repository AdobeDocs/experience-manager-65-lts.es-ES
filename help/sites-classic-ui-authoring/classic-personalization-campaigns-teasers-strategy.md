---
title: Teasers and Strategies
description: Las campañas suelen utilizar teasers como mecanismo para atraer a un segmento específico de la población de visitantes a contenido centrado en sus intereses. Uno o más teasers están definidos para una campaña específica.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1202'
ht-degree: 2%

---

# Teasers and Strategies{#teasers-and-strategies}

Las campañas suelen utilizar teasers como mecanismo para atraer a un segmento específico de la población de visitantes a contenido centrado en sus intereses. Uno o más teasers están definidos para una campaña específica.

>[!NOTE]
>
>El componente Teaser ya no se utiliza en AEM 6.2. En su lugar, utilice [Target component](/help/sites-authoring/content-targeting-touch.md).

* **Las páginas de marca** se almacenan en la sección Campañas del sitio web. Una marca contiene las campañas individuales.
* **Las páginas de campaña** se almacenan en la sección Campañas del sitio web. Cada campaña tiene una página individual, en la que se muestran las definiciones del teaser. El contenedor, o página de información general, también contiene cierta información y estadísticas relacionadas con las páginas de teaser individuales.

Los teasers de AEM están compuestos por varias partes:

* **Las páginas teaser** se almacenan en la página de campaña adecuada y contienen las definiciones de los párrafos de teaser disponibles para cada campaña específica. Estas definiciones se utilizan para mostrar los párrafos de teaser; incluidas las variaciones de contenido, el segmento que se utilizará para seleccionar una variación y el factor de ampliación.
* El **componente Teaser** está disponible de forma predeterminada y le permite crear una instancia de su párrafo de teaser específico en una página de contenido. Puede arrastrar el componente Teaser de la barra de tareas y, a continuación, especificar la definición del teaser para crear su propio párrafo de teaser. **Nota:** El componente Teaser ya no se utiliza en AEM 6.2. En su lugar, utilice [Target component](/help/sites-authoring/content-targeting-touch.md).
* **Los párrafos de teaser** son instancias reales del teaser dentro de una página de contenido. Esto atrae a un segmento de visitantes a través del contenido centrado en sus intereses.
* Páginas que contienen contenido de la campaña centrado en un segmento de visitante específico. Normalmente, los párrafos de teaser dirigen al visitante a dichas páginas.

## Estrategias {#strategies}

Al agregar un párrafo de teaser a una página, debe definir la **estrategia**.

Esto es así en el caso de que haya varios teasers disponibles para su selección, ya que todos sus segmentos asignados se resuelven correctamente. La **estrategia** especifica un criterio adicional usado para seleccionar el teaser que se muestra:

* **Puntuación del flujo de navegación**, se basa en las etiquetas y las visitas de etiquetas relacionadas que se mantienen dentro del contexto de cliente del visitante (muestran la frecuencia con la que un visitante ha hecho clic en páginas que contienen la etiqueta correspondiente). Se comparan las tasas de visitas de las etiquetas definidas en la página de teaser.
* **Aleatorio**, para la selección &quot;aleatoria&quot;; utiliza el factor aleatorio generado para una página; esto se puede ver con el [contexto de cliente](/help/sites-administering/client-context.md).
* **Primero** en la lista de segmentos resueltos. El orden es el de los teasers de la página contenedora de la campaña.

El [factor de ampliación](/help/sites-administering/campaign-segmentation.md#boost-factor) del segmento también afecta a la selección. Se trata de un factor de ponderación añadido a una definición de segmento para aumentar/disminuir la probabilidad relativa de que se seleccione.

El proceso y las interrelaciones de los distintos criterios de selección se ilustran mejor con un ejemplo (un método que también se puede utilizar para garantizar que los teasers lleguen a la audiencia requerida).

Si ya se han creado los siguientes segmentos y se les ha asignado su respectivo factor de ampliación:

| Segmento | Factor de ampliación |
|---|---|
| S1 | 0 |
| S2 | 0 |
| S3 | 10 |
| S4 | 30 |
| S5 | 0 |
| S6 | 100 |

Y usamos las siguientes definiciones de teaser:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Segmentos asignados</td>
   <td>Etiquetas asignadas </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Negocios, Marketing</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Empresa<br /> </td>
  </tr>
 </tbody>
</table>

Entonces, si aplicamos esto a un visitante donde:

* **S1**, **S2 y **S6** se resolvieron correctamente

* la etiqueta **marketing** tiene tres visitas
* la etiqueta **business** tiene seis visitas

Podemos ver el resultado:

* coincidencia correcta: ¿alguno de los segmentos asignados al teaser se resuelve correctamente para el visitante actual?
* factor de ampliación: el factor de ampliación más alto de todos los segmentos aplicables
* puntuación del flujo de navegación: el total acumulado de todas las visitas de etiquetas aplicables

que se calculan antes de aplicar la estrategia adecuada:

<table>
 <tbody>
  <tr>
   <td>Campaign</td>
   <td>Teaser</td>
   <td>Segmentos asignados</td>
   <td>Etiquetas </td>
   <td>¿Coincidencia correcta?</td>
   <td>Factor de ampliación resultante</td>
   <td>Puntuación del flujo de navegación resultante </td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T1</td>
   <td>S1, S2</td>
   <td>Negocios, Marketing</td>
   <td>Sí</td>
   <td>0</td>
   <td>9</td>
  </tr>
  <tr>
   <td>C1</td>
   <td>T2 </td>
   <td>S1</td>
   <td><br /> </td>
   <td>Sí</td>
   <td>0</td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T3</td>
   <td>S3, S4</td>
   <td><br /> </td>
   <td>No</td>
   <td><br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T4</td>
   <td>S2, S5</td>
   <td><br /> </td>
   <td>Sí<br /> </td>
   <td>0<br /> </td>
   <td><br /> </td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T5</td>
   <td>S1, S2, S6</td>
   <td>Marketing</td>
   <td>Sí</td>
   <td>100</td>
   <td>3</td>
  </tr>
  <tr>
   <td>C1 </td>
   <td>T6</td>
   <td>S6</td>
   <td>Negocios</td>
   <td>Sí</td>
   <td>100</td>
   <td>6 </td>
  </tr>
 </tbody>
</table>

Estos valores se usan para determinar los teasers que verá el visitante, según la **estrategia** aplicada al párrafo de teaser:

<table>
 <tbody>
  <tr>
   <td>Estrategia</td>
   <td>Teaser resultante</td>
   <td>Comentarios</td>
  </tr>
  <tr>
   <td>Primero</td>
   <td>T5</td>
   <td>Solo T5 y T6 se consideran como sus segmentos resuelven <i>y</i> tienen el factor de ampliación más alto. La lista devuelta está en el orden T5, T6; por lo tanto, T5 se selecciona y se muestra.</td>
  </tr>
  <tr>
   <td>Aleatorio</td>
   <td>T5 o T6</td>
   <td>Ambos teasers tienen segmentos que se resuelven y tienen el mismo factor de ampliación. Por lo tanto, los dos teasers se muestran en igual proporción.</td>
  </tr>
  <tr>
   <td>Puntuación del flujo de navegación</td>
   <td>T6</td>
   <td><p>Los segmentos para T1, T4, T5 y T6 se resuelven para el visitante. Los factores de impulso más altos de T5 y T6 excluyen entonces T1 y T4. Finalmente, la mayor puntuación del flujo de navegación de T6 hace que se seleccione esta opción.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si, después de las técnicas de resolución anteriores, hay varios teasers disponibles para seleccionarlos, una selección interna (aleatoria) seleccionará un único teaser para mostrarlo.
>
>Por ejemplo, si la estrategia era Puntuación del flujo de navegación y T5 tenía la misma puntuación del flujo de navegación que T6 (es decir, seis en lugar de tres), se utilizaría la selección interna (aleatoria) para seleccionar uno de estos dos.

Las páginas teaser o los párrafos se utilizan para dirigir segmentos específicos de visitantes a contenido centrado en sus intereses. Pueden presentar una serie de opciones para que el visitante elija, o mostrar solo un párrafo de teaser basado en el segmento del visitante específico. Por ejemplo, el párrafo de teaser que se muestra puede depender de la edad del visitante.

Normalmente, una página de teaser es una acción temporal que dura un período de tiempo específico, hasta que se reemplaza por la siguiente página de teaser.

Después de crear la marca y la campaña, puede crear y configurar la experiencia de teaser.

### Creación de un punto de contacto para el teaser {#creating-a-touchpoint-for-your-teaser}

>[!NOTE]
>
>El componente Teaser ya no se utiliza en AEM 6.2. En su lugar, utilice [Target component](/help/sites-authoring/content-targeting-touch.md).

1. Vaya a la página de contenido en la que desee colocar el párrafo de teaser que lleva a la página de la campaña.
1. Agregue un componente **Teaser** (disponible en la sección **Personalization** de la barra de tareas) en la posición requerida. Cuando se cree por primera vez, mostrará que la ruta de campaña aún no está configurada:

   ![chlimage_1](assets/chlimage_1.png)

1. Edite el componente teaser para añadir lo siguiente:

   * **Ruta de campaña**
Ruta a la página de campaña que contiene la página de teaser individual; los segmentos determinan exactamente qué teaser se muestra.

   * **[Estrategia](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md#strategies)**
Método utilizado para la selección cuando varios segmentos se resuelven correctamente.

   ![chlimage_1-1](assets/chlimage_1-1.png)

1. Haga clic en **Aceptar** para guardar. Según los segmentos que haya configurado en el teaser y el perfil del usuario con el que haya iniciado sesión, se mostrará el contenido apropiado:

   ![chlimage_1-2](assets/chlimage_1-2.png)

1. Pase el ratón sobre el párrafo de teaser para mostrar el icono del signo de interrogación (esquina inferior derecha del componente). Haga clic aquí para ver los segmentos aplicados y si se resuelven actualmente.

   ![chlimage_1-3](assets/chlimage_1-3.png)

### Información general sobre teaser {#teaser-overview}

Además de la vista de campaña en el MCM, la página de campaña también proporciona información sobre los teasers conectados a ella:

1. Desde la consola **Sitios web**, abra la página de campaña; por ejemplo:

   `https://localhost:4502/content/campaigns/geometrixx-outdoors/storefront/summer.html`

   Esto muestra una descripción general de las definiciones de teaser y las estadísticas de visualización:

   ![chlimage_1-4](assets/chlimage_1-4.png)
