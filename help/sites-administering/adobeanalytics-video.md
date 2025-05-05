---
title: Configuración del seguimiento de vídeo para Adobe Analytics
description: Obtenga información acerca de la configuración del seguimiento de vídeo para SiteCatalyst.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 0%

---

# Configuración del seguimiento de vídeo para Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Hay varios métodos disponibles para el seguimiento de eventos de vídeo, dos de los cuales son opciones heredadas para versiones anteriores de Adobe Analytics. Estas opciones heredadas son: Hitos heredados y Segundos heredados.

>[!NOTE]
>
>Antes de continuar, asegúrese de que ha subido un **vídeo reproducible** en AEM.
>
>Para asegurarse de que los vídeos se reproduzcan en la página, consulte **[este tutorial](/help/sites-authoring/default-components-foundation.md#video)** para obtener información sobre cómo transcodificar archivos de vídeo en AEM.

Utilice el siguiente procedimiento para configurar un marco de trabajo para el seguimiento de vídeo con cada método.

>[!NOTE]
>
>Para nuevas implementaciones, se recomienda que **no use** las opciones heredadas para el seguimiento de vídeo. En su lugar, use el método **Milestones**.

## Pasos comunes {#common-steps}

1. Configure una página web arrastrando un **componente de vídeo** de la barra de tareas y agregando un **vídeo como recurso** que se puede reproducir para el componente

1. [Crear una configuración y un módulo de Adobe Analytics](/help/sites-administering/adobeanalytics.md).

   * Los ejemplos de las secciones siguientes utilizan el nombre **my-sc-configuration** para la configuración y **videofw** para el marco de trabajo.

1. En la página marco de trabajo, seleccione un RSID y establezca el uso en todo. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. En la categoría Componente general de Sidekick, arrastre el componente Vídeo al módulo.
1. Seleccione un método de seguimiento:

   * [Hitos](/help/sites-administering/adobeanalytics.md)
   * [Hitos no heredados](/help/sites-administering/adobeanalytics.md)
   * [Hitos heredados](/help/sites-administering/adobeanalytics.md)
   * [Segundos heredados](/help/sites-administering/adobeanalytics.md)

1. Al seleccionar un método de seguimiento, la lista de variables CQ cambia en consecuencia. Utilice las secciones siguientes para obtener información sobre cómo configurar el componente y asignar las variables CQ con propiedades de Adobe Analytics.

## Hitos {#milestones}

El método Milestones rastrea la mayor cantidad de información sobre el vídeo, es altamente personalizable y fácil de configurar.

Para utilizar el método Milestones, especifique los desplazamientos de seguimiento basados en el tiempo para definir los hitos. Cuando la reproducción de un vídeo supera un hito, la página llama a Adobe Analytics para realizar un seguimiento del evento. Para cada hito que defina, el componente creará una variable de CQ que puede asignar a una propiedad de Adobe Analytics. El nombre de estas variables de CQ utiliza el siguiente formato:

```shell
eventdata.events.milestoneXX
```

El sufijo XX es el desvío de pista que define el hito. Por ejemplo, si se especifican desplazamientos de seguimiento de 4, 8, 16, 20 y 28 segundos, se generan las siguientes variables de CQ:

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

En la tabla siguiente se describen las variables de CQ predeterminadas que se proporcionan para el método Milestones:

<table>
 <tbody>
  <tr>
   <th>Variables CQ</th>
   <th>Propiedades de Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>Las variables asignadas a esto contendrán el <strong>nombre descriptivo</strong> (<strong>Título</strong>) del vídeo si se establece en DAM; si no se establece, se enviará el <strong>nombre de archivo</strong> del vídeo en su lugar. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Las variables asignadas a esta variable contienen el nombre del archivo. Solo se envía junto con eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>Las variables asignadas a esta variable contienen la ruta del archivo en el servidor. Solo se envía junto con eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>Se envía cada vez que se pasa un hito de segmento </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>Cada vez que se activa un hito, se envía junto con este evento el número de segundos que el usuario ha invertido en ver un segmento determinado. por ejemplo, eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>Enviado al inicializar la vista de vídeo</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>Se envió cuando el vídeo terminó de reproducirse<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>Enviado cuando se pase el hito dado, X significa el segundo en que el hito se activa en <br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>Enviado en cada hito; aparece como pev3 en la llamada de Adobe Analytics, normalmente se envía como "vídeo"<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>Exactamente coincide con eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>Contiene información sobre el segmento que se ha visto, por ejemplo, <code>2:O:4-8</code> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede establecer el nombre **fácil de usar** de un vídeo abriendo el vídeo para editarlo en DAM y estableciendo el campo de metadatos **Título** en el nombre deseado.

1. Después de seleccionar Hitos como método de seguimiento, en el cuadro Desplazamiento de seguimiento, escriba una lista de desplazamientos de seguimiento separados por comas en segundos. Por ejemplo, el siguiente valor define hitos a los 4, 8, 16, 20 y 28 segundos después del inicio del vídeo:

   ```xml
   4,8,16,20,24
   ```

   Los valores de desplazamiento deben ser enteros mayores que 0. El valor predeterminado es `10,25,50,75`.

1. Para asignar las variables CQ a las propiedades de Adobe Analytics, arrastre las propiedades de Adobe Analytics desde ContentFinder junto a la variable CQ en el componente.

   Para obtener información sobre cómo optimizar las asignaciones, consulte la guía [Medición de vídeo en Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=es).

1. [Agregar el marco de trabajo](/help/sites-administering/adobeanalytics.md) a la página.
1. Para probar la configuración en **modo de vista previa**, reproduzca el vídeo para obtener llamadas de Adobe Analytics al déclencheur.

Los siguientes ejemplos de datos de seguimiento de Adobe Analytics se aplican al seguimiento de Milestone mediante desplazamientos de seguimiento de 4, 8, 16, 20 y 24, y a las siguientes asignaciones para las variables de CQ:

<table>
 <tbody>
  <tr>
   <th>variable de CQ</th>
   <th>propiedad de Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>evento2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>evento4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>EVAR3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>eVar1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>EVAR2</td>
  </tr>
 </tbody>
</table>

Para este ejemplo, el componente Vídeo aparece de la siguiente manera en la página de marco de trabajo:

![vídeo1](assets/video1.png)

>[!NOTE]
>
>Para ver las llamadas realizadas a Adobe Analytics, utilice una herramienta adecuada, como DigitalPulse Debugger o Fiddler.

Las llamadas a Adobe Analytics que utilicen el ejemplo proporcionado deberían tener este aspecto cuando se visualicen con DigitalPulse Debugger:

![chlimage_1-128](assets/chlimage_1-128.png)

*Esta es la **primera llamada**&#x200B;a Adobe Analytics que contiene los siguientes valores:*

* *prop1 y eVar1 para eventdata.a.media.name,*
* *props2-4, junto con eVar2 y eVar3 que contienen contentType (vídeo) y segmento (1:O:1-4)*
* *event3 asignado a eventdata.events.a.media.view.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Esta es la **tercera llamada**&#x200B;realizada a Adobe Analytics:*

* *prop1 y eVar1 contienen a.media.name;*
* *evento1 porque se ha visto un segmento*
* *evento2 enviado con tiempo de reproducción = 4*
* *evento11 enviado porque se ha alcanzado eventdata.events.milestone8*
* *prop2 a 4 no se envían (ya que eventdata.events.a.media.view no se activó)*

## Hitos no heredados {#non-legacy-milestones}

El método de hitos no heredados es similar al método de hitos, excepto que los hitos se definen mediante porcentajes de la longitud de la pista. Los elementos comunes son los siguientes:

* Cuando la reproducción de un vídeo supera un hito, la página llama a Adobe Analytics para realizar un seguimiento del evento.
* El [conjunto estático de variables CQ](#cqvars) que se definen para su asignación con propiedades Adobe Analytics.
* Para cada hito que defina, el componente creará una variable de CQ que puede asignar a una propiedad de Adobe Analytics.

El nombre de estas variables de CQ utiliza el siguiente formato:

El sufijo XX es el porcentaje de longitud de pista que define el hito. Por ejemplo, si se especifican porcentajes de 10, 25, 50 y 75, se generarán las siguientes variables de CQ:

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. Después de seleccionar Hitos no heredados como método de seguimiento, en el cuadro Desplazamiento de seguimiento, introduzca una lista separada por comas de porcentajes de longitud de seguimiento. Por ejemplo, el siguiente valor predeterminado define hitos en el 10, 25, 50 y 75 por ciento de la longitud de la pista:

   ```xml
   10,25,50,75
   ```

   Los valores de desplazamiento deben ser enteros mayores que 0.

1. Para asignar las variables CQ a las propiedades de Adobe Analytics, arrastre las propiedades de Adobe Analytics desde ContentFinder junto a la variable CQ en el componente.

   Para obtener información sobre cómo optimizar las asignaciones, consulte la guía [Medición de vídeo en Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=es).

1. [Agregar el marco de trabajo](/help/sites-administering/adobeanalytics.md) a la página.
1. Para probar la configuración en **modo de vista previa**, reproduzca el vídeo para obtener llamadas de Adobe Analytics al déclencheur.

## Hitos heredados {#legacy-milestones}

Este método es similar al método Milestones con la diferencia de que los hitos especificados en el campo *Desplazamiento de seguimiento* son porcentajes en lugar de puntos de conjunto dentro del vídeo.

>[!NOTE]
>
>El campo Tracking offset solo acepta una lista separada por comas que contenga números enteros entre 1 y 100.

1. Defina el desplazamiento de pista.

   * por ejemplo,10,50,75,100

   Además, la información enviada a Adobe Analytics es menos personalizable; solo hay 3 variables disponibles para la asignación:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Las variables asignadas a esto contendrán el <strong>nombre descriptivo</strong> (<strong>Título</strong>) del vídeo si se establece en DAM; si no se establece el Título, se enviará el <strong>nombre de archivo</strong> del vídeo en su lugar. Solo se envió una vez, al principio de la reproducción de un vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Las variables asignadas a esta variable contienen el nombre del archivo. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variable asignada a esta ruta contiene la ruta del archivo en el servidor. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede establecer el nombre **fácil de usar** de un vídeo abriendo el vídeo para editarlo en DAM y estableciendo el campo de metadatos **Título** en el nombre deseado. También debe Guardar los cambios realizados cuando termine.

1. Asigne estas variables a las props 1 a 3

   El **resto de la información relevante** en la llamada se enviará concatenado en **una** variable denominada **pev3**.

   **Las llamadas de muestra** a Adobe Analytics que usen el ejemplo proporcionado deberían tener este aspecto cuando se visualicen con DigitalPulse Debugger:

   ![hitos1](assets/lmilestones1.png)

   *La variable **pev3**&#x200B;enviada en la llamada contiene la siguiente información:*

   * *Nombre* - El nombre del archivo de vídeo (*film.avi*)

   * *Longitud* - La longitud del archivo de vídeo, en segundos (*100*)

   * *Nombre del reproductor* - El reproductor de vídeo usado para reproducir el archivo de vídeo (*vídeo de HTML5*)

   * *Segundos totales reproducidos* - El número total de segundos que se reprodujo el vídeo (*25*)

   * *Iniciar marca de tiempo* - Marca de tiempo que identifica cuándo comenzó la reproducción de vídeo (*1331035567*)

   * *Sesión de reproducción*: Los detalles de la sesión de reproducción. Este campo indica cómo interactuó el usuario con el vídeo. Esto puede incluir datos como dónde empezaron a reproducir el vídeo, si usaron el control deslizante de vídeo para avanzar el vídeo y dónde dejaron de reproducirlo (*L10E24S58L58: el vídeo se detuvo a los segundos. 25 de la sección L10, y después se salta a sec. 48*)

## Segundos heredados {#legacy-seconds}

Al utilizar el método **&#x200B; legacy seconds**, las llamadas de Adobe Analytics se activan cada N-ésimo segundo, donde N se especifica en el campo Track offset.

1. Establezca el desplazamiento de pista en cualquier número de segundos,

   * por ejemplo, 6

   >[!NOTE]
   >
   >El campo Desplazamiento de seguimiento solo acepta números enteros superiores a 0

   La información enviada a Adobe Analytics es menos personalizable. Solo hay 3 variables disponibles para la asignación:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Las variables asignadas a esto contendrán el <strong>nombre descriptivo</strong> (<strong>Título</strong>) del vídeo si se establece en DAM; si no se establece el Título, se enviará el <strong>nombre de archivo</strong> del vídeo en su lugar. Solo se envió una vez, al principio de la reproducción de un vídeo.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>La variable asignada a esta acción contiene el nombre del archivo. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variable asignada a esta ruta contiene la ruta del archivo en el servidor. Solo se envía una vez, al principio de la reproducción de un vídeo.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Puede establecer el nombre **fácil de usar** de un vídeo abriendo el vídeo para editarlo en DAM y estableciendo el campo de metadatos **Título** en el nombre deseado. También debe Guardar los cambios realizados cuando termine.

1. Asigne estas variables a prop1, prop2 y prop3

   El **resto de la información relevante** de la llamada se enviará concatenado a la variable **one** denominada **pev3**.

   Las llamadas a Adobe Analytics que utilicen el ejemplo proporcionado deberían tener este aspecto cuando se visualicen con DigitalPulse Debugger:

   ![lseconds](assets/lseconds.png)

   *La llamada es similar a la llamada de hitos heredados anterior. Consulte la información sobre pev3 proporcionada en [Integración con Adobe Analytics](/help/sites-administering/adobeanalytics.md).*

**Referencias utilizadas en este tutorial:**

[0] [https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=es](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=es)
