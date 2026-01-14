---
title: Etiquetas inteligentes mejoradas
description: Etiquetas inteligentes mejoradas
contentOwner: AG
feature: Smart Tags, Search
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 7a0d5502-8e1a-4396-a517-ea3767e228c2
source-git-commit: ad4c80af0d9aa88837164ba1a8d6be2042b2c0d4
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 1%

---

# Explicación, aplicación y depuración de las etiquetas inteligentes {#enhanced-smart-tags}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=es) |
| AEM 6.5 | Este artículo |

Las organizaciones que trabajan con recursos digitales utilizan cada vez más vocabulario controlado por taxonomía en los metadatos de recursos. Básicamente, incluye una lista de palabras clave que los empleados, socios y clientes suelen utilizar para referirse a recursos digitales de una clase determinada y buscarlos. El etiquetado de recursos con vocabulario controlado por taxonomía garantiza que los recursos se identifiquen y recuperen fácilmente.

En comparación con los vocabularios de lenguajes naturales, el etiquetado de recursos digitales basado en la taxonomía empresarial ayuda a alinearlos con el negocio de una empresa y garantiza que los recursos más relevantes aparezcan en las búsquedas.

Por ejemplo, un fabricante de automóviles puede etiquetar imágenes de automóviles con nombres de modelos para que solo aparezcan imágenes relevantes cuando se busquen imágenes de varios modelos para diseñar una campaña de promoción.

Para que el servicio de contenido inteligente aplique las etiquetas correctas, entréguelo para que reconozca su taxonomía. Para entrenar el servicio, primero depure un conjunto de recursos y etiquetas que describan mejor estos recursos. Para ayudar al servicio a aprender, aplique estas etiquetas en los recursos y ejecute un flujo de trabajo de formación.

Una vez que una etiqueta está preparada y lista, el servicio ahora puede aplicar estas etiquetas a los recursos a través de un flujo de trabajo de etiquetado.

En segundo plano, el servicio de contenido inteligente utiliza el marco de trabajo de Adobe AI para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos.

El servicio de contenido inteligente es un servicio en la nube que está hospedado en [!DNL Adobe Developer Console]. Para usarlo en [!DNL Adobe Experience Manager], el administrador del sistema debe integrar su implementación de [!DNL Experience Manager] con [!DNL Adobe Developer Console].

En resumen, estos son los pasos principales para utilizar el servicio de contenido inteligente:

* Incorporación
* Revisión de recursos y etiquetas (definición de taxonomía)
* Formación del servicio de contenido inteligente
* Etiquetado automático

![Diagrama de flujo](assets/flowchart.gif)

## Requisitos previos y formatos admitidos {#prerequisites}

Antes de usar el servicio de contenido inteligente, asegúrese de lo siguiente para crear una integración en [!DNL Adobe Developer Console]:

* Una cuenta de Adobe ID con privilegios de administrador para la organización.
* Habilite el servicio de contenido inteligente para su organización.
* Para agregar el paquete base de Smart Content Services a una implementación, obtenga la licencia del paquete base [!DNL Adobe Experience Manager Sites] y del complemento [!DNL Assets].

El servicio aplica etiquetas inteligentes a los recursos de los siguientes tipos MIME:

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

El servicio aplica etiquetas inteligentes a las representaciones de recursos de los siguientes tipos MIME:

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## Incorporación {#onboarding}

El servicio de contenido inteligente está disponible para su compra como complemento de [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a [!DNL Adobe I/O].

El administrador puede seguir el vínculo para integrar el servicio de contenido inteligente con [!DNL Experience Manager]. Para integrar el servicio con [!DNL Experience Manager Assets], consulte [Configurar etiquetas inteligentes](config-smart-tagging.md).

El proceso de incorporación se completa cuando el administrador configura el servicio y agrega usuarios en [!DNL Experience Manager].

## Revisión de recursos y etiquetas {#reviewing-assets-and-tags}

Una vez que se haya incorporado, lo primero que debe hacer es identificar un conjunto de etiquetas que describa mejor estas imágenes en el contexto de su negocio.

A continuación, revise las imágenes para identificar el conjunto de imágenes que mejor represente el producto para un requisito empresarial determinado. Asegúrese de que los recursos del conjunto depurado cumplan las [directrices de formación del servicio de contenido inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Agregue los recursos a una carpeta y aplique las etiquetas a cada recurso desde la página de propiedades. A continuación, ejecute el flujo de trabajo de formación en esta carpeta. El conjunto depurado de recursos permite al servicio de contenido inteligente formar de forma eficaz más recursos mediante las definiciones de taxonomía.

>[!NOTE]
>
>1. La formación es un proceso irrevocable. Adobe recomienda revisar las etiquetas del conjunto depurado de recursos mucho antes de entrenar al servicio de contenido inteligente en las etiquetas.
>1. Antes de entrenar una etiqueta, consulte [Directrices de aprendizaje del servicio de contenido inteligente](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Cuando se entrena el servicio de contenido inteligente por primera vez, Adobe recomienda entrenarlo en al menos dos etiquetas distintas.

## Comprender [!DNL Experience Manager] resultados de búsqueda con etiquetas inteligentes {#understandsearch}

De manera predeterminada, la búsqueda [!DNL Experience Manager] combina los términos de búsqueda con una cláusula `AND`. El uso de etiquetas inteligentes no cambia este comportamiento predeterminado. El uso de etiquetas inteligentes agrega una cláusula `OR` adicional para buscar cualquiera de los términos de búsqueda relacionados con las etiquetas inteligentes. Por ejemplo, considere buscar `woman running`. Assets con solo `woman` o solo `running` palabra clave en los metadatos no aparece en los resultados de búsqueda de forma predeterminada. Sin embargo, un recurso etiquetado con `woman` o `running` mediante etiquetas inteligentes aparece en dicha consulta de búsqueda. Por lo tanto, los resultados de búsqueda son una combinación de:

* Assets con palabras clave `woman` y `running` en los metadatos.

* Assets Smart etiquetado con cualquiera de las palabras clave.

Los resultados de búsqueda que coinciden con todos los términos de búsqueda en los campos de metadatos se muestran primero, seguidos de los resultados de búsqueda que coinciden con cualquiera de los términos de búsqueda en las etiquetas inteligentes. En el ejemplo anterior, el orden aproximado de visualización de los resultados de búsqueda es:

1. Coincide con `woman running` en los distintos campos de metadatos.
1. Coincidencias de `woman running` en etiquetas inteligentes.
1. Coincidencias de `woman` o de `running` en etiquetas inteligentes.

>[!CAUTION]
>
>Si la indexación de Lucene se realiza fuera de [!DNL Adobe Experience Manager], la búsqueda basada en etiquetas inteligentes no funciona como se espera.

## Etiquetar recursos automáticamente {#tagging-assets-automatically}

Después de haber formado el servicio de contenido inteligente, puede almacenar en déclencheur el flujo de trabajo de etiquetado para aplicar automáticamente las etiquetas adecuadas a un conjunto diferente de recursos similares.

Puede ejecutar el flujo de trabajo de etiquetado periódicamente o siempre que sea necesario.

>[!NOTE]
>
>El flujo de trabajo de etiquetado se ejecuta tanto en recursos como en carpetas.

### Etiquetado periódico {#periodic-tagging}

Puede habilitar el Servicio de contenido inteligente para que etiquete periódicamente recursos de una carpeta. Abra la página de propiedades de la carpeta de recursos, seleccione **[!UICONTROL Habilitar etiquetas inteligentes]** en la ficha **[!UICONTROL Detalles]** y guarde los cambios.

Una vez seleccionada esta opción para una carpeta, el servicio de contenido inteligente etiqueta automáticamente los recursos de la carpeta. De forma predeterminada, el flujo de trabajo de etiquetado se ejecuta todos los días a las 12:00 a. m.

### Etiquetado bajo demanda {#on-demand-tagging}

Puede almacenar en déclencheur el flujo de trabajo de etiquetado desde la consola de flujo de trabajo o desde la cronología para etiquetar instantáneamente los recursos.

>[!NOTE]
>
>Si ejecuta el flujo de trabajo de etiquetado desde la cronología, puede aplicar etiquetas en un máximo de 15 recursos a la vez.

#### Etiquetado de recursos desde la consola de flujo de trabajo {#tagging-assets-from-the-workflow-console}

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el flujo de trabajo **[!UICONTROL Assets de etiquetas inteligentes DAM]** y, a continuación, haga clic en **[!UICONTROL Iniciar flujo de trabajo]** en la barra de herramientas.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. En el cuadro de diálogo **[!UICONTROL Ejecutar flujo de trabajo]**, vaya a la carpeta de carga útil que contiene los recursos en los que desea aplicar las etiquetas automáticamente.
1. Especifique un título para el flujo de trabajo y un comentario opcional. Haga clic en **[!UICONTROL Ejecutar]**.

   ![cuadro de diálogo_etiquetado](assets/tagging_dialog.png)

   Para comprobar si el servicio de contenido inteligente ha etiquetado correctamente los recursos, vaya a la carpeta de recursos y revise las etiquetas.

#### Etiquetado de recursos de la cronología {#tagging-assets-from-the-timeline}

1. En la interfaz de usuario [!DNL Assets], seleccione la carpeta que contiene los recursos o los recursos específicos a los que desea aplicar las etiquetas inteligentes.
1. En la esquina superior izquierda, abra la **[!UICONTROL cronología]**.
1. Abra acciones desde la parte inferior de la barra lateral izquierda y haga clic en **[!UICONTROL Iniciar flujo de trabajo]**.

   ![start_workflow](assets/start_workflow.png)

1. Seleccione el flujo de trabajo **[!UICONTROL DAM Smart Tag Assets]** y especifique un título para el flujo de trabajo.
1. Haga clic en **[!UICONTROL Iniciar]**. El flujo de trabajo aplica etiquetas a los recursos. para comprobar si el servicio de contenido inteligente ha etiquetado correctamente los recursos, vaya a la carpeta de recursos y revise las etiquetas.

>[!NOTE]
>
>En los ciclos de etiquetado siguientes, solo los recursos modificados se vuelven a etiquetar con etiquetas recién formadas. Sin embargo, incluso los recursos sin modificar se etiquetan si el espacio entre los ciclos de etiquetado último y actual para el flujo de trabajo de etiquetado supera las 24 horas. Para los flujos de trabajo de etiquetado periódicos, los recursos sin modificar se etiquetan cuando el lapso de tiempo supera los seis meses.

## Depurar o moderar las etiquetas inteligentes aplicadas {#manage-smart-tags}

Puede depurar las etiquetas inteligentes para eliminar cualquier etiqueta inexacta asignada a las imágenes de su marca, de modo que solo se muestren las etiquetas más relevantes.

La moderación de las etiquetas inteligentes también ayuda a refinar las búsquedas de imágenes basadas en etiquetas, ya que garantiza que la imagen aparezca en los resultados de búsqueda de las etiquetas más relevantes. Básicamente, ayuda a eliminar las posibilidades de que las imágenes no relacionadas se muestren en los resultados de búsqueda.

También puede asignar una clasificación más alta a una etiqueta para aumentar su relevancia para una imagen. Promocionar una etiqueta para una imagen aumenta las posibilidades de que la imagen aparezca en los resultados de búsqueda cuando se busca la etiqueta en particular.

1. En el cuadro de búsqueda, busque recursos basados en una etiqueta como palabra clave.
1. Para identificar una imagen que no encuentre relevante para la búsqueda, revise los resultados de la búsqueda.
1. Seleccione la imagen y haga clic en **[!UICONTROL Administrar etiquetas]** en la barra de herramientas.
1. En la página **[!UICONTROL Administrar etiquetas]**, revise las etiquetas. Si no desea buscar la imagen según una etiqueta específica, seleccione la etiqueta y haga clic en **[!UICONTROL Eliminar]** en la barra de herramientas. También puede hacer clic en el símbolo `x` que aparece junto a una etiqueta.
1. De manera opcional, para asignar una clasificación más alta a una etiqueta, selecciónela y haga clic en **[!UICONTROL Promocionar]** en la barra de herramientas. La etiqueta que promociones se moverá a la sección **[!UICONTROL Etiquetas]**.
1. Haga clic en **[!UICONTROL Guardar]** y luego en **[!UICONTROL Aceptar]**
1. Vaya a la página **[!UICONTROL Propiedades]** de la imagen. Observe que a la etiqueta promocionada se le asigna más relevancia y aparece antes en los resultados de búsqueda.

## Sugerencias y limitaciones {#tips-best-practices-limitations}

* Para entrenar el modelo, utilice las imágenes más adecuadas. El curso de formación no se puede revertir o el modelo de formación no se puede eliminar. La precisión del etiquetado depende de la formación actual, por lo que debe hacerlo con cuidado.
* El uso de los servicios de contenido inteligente está limitado a un máximo de 2 millones de imágenes etiquetadas al año. Todas las imágenes duplicadas que se procesan y etiquetan se cuentan como imágenes etiquetadas.
* Si ejecuta el flujo de trabajo de etiquetado desde la cronología, puede aplicar etiquetas en un máximo de 15 recursos a la vez.
* Las etiquetas inteligentes solo funcionan para los formatos de imagen PNG y JPG. Por lo tanto, los recursos compatibles que tengan representaciones creadas en estos dos formatos se etiquetan con etiquetas inteligentes.

>[!MORELIKETHIS]
>
>* [Información general y cómo entrenar etiquetas inteligentes](enhanced-smart-tags.md)
>* [Configurar el etiquetado inteligente](config-smart-tagging.md)
>* [Solución de problemas de etiquetas inteligentes para credenciales de OAuth](config-oauth.md)
>* [Tutorial de vídeo sobre etiquetas inteligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=es)
