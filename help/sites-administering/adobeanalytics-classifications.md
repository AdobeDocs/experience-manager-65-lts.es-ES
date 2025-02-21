---
title: Clasificaciones de Adobe
description: Aprenda a utilizar las clasificaciones de Adobe para exportar datos de clasificaciones a Adobe Analytics.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Clasificaciones de Adobe{#adobe-classifications}

Clasificaciones de Adobe exporta datos de clasificaciones a [Adobe Analytics](/help/sites-administering/adobeanalytics.md) de forma programada. El exportador es una implementación de **com.adobe.cq.scheduled.exporter.Exporter**.

Para configurar esto:

1. Usando **Navegación**, seleccione **Herramientas**, **Cloud Services** y después **Cloud Services heredados**.
1. Desplácese a **Adobe Analytics** y seleccione **Mostrar configuraciones**.
1. Haga clic en el vínculo **[+]** junto a la configuración de Adobe Analytics.

1. En el cuadro de diálogo **Crear módulo**:

   * Especifique un **Título**.
   * Opcionalmente, puede especificar **Name**, para el nodo que almacena los detalles del marco de trabajo en el repositorio.
   * Seleccionar **clasificaciones de Adobe Analytics**

   Y haga clic en **Crear**.

   ![Cuadro de diálogo Crear marco](assets/aa-25.png)

1. Se abre el cuadro de diálogo **Configuración de clasificaciones** para editarlo.

   ![Cuadro de diálogo Configuración de clasificaciones](assets/aa-classifications-settings.png)

   Las propiedades incluyen lo siguiente:

   | **Campo** | **Descripción** |
   |---|---|
   | Habilitado | Seleccione **Sí** para habilitar la configuración de las clasificaciones de Adobe. |
   | Sobrescribir en caso de conflicto | Seleccione **Sí** para sobrescribir los conflictos de datos. De manera predeterminada, se establece en **No**. |
   | Eliminar procesados | Si se establece en **Yes**, elimina los nodos procesados una vez exportados. El valor predeterminado es **False**. |
   | Descripción del trabajo de exportación | Introduzca una descripción para el trabajo de clasificaciones de Adobe. |
   | Correo electrónico de notificación | Introduzca una dirección de correo electrónico para la notificación de clasificaciones de Adobe. |
   | Grupo de informes | Introduzca el grupo de informes para el que se ejecutará el trabajo de importación. |
   | Conjunto de datos | Introduzca el ID de relación del conjunto de datos para el que se ejecutará el trabajo de importación. |
   | Transformador | En el menú desplegable, seleccione una implementación de transformador. |
   | Fuente de datos | Vaya a la ruta del contenedor de datos. |
   | Programación de exportación | Seleccione la programación de la exportación. El valor predeterminado es cada 30 minutos. |

1. Haz clic en **Aceptar** para guardar la configuración.

## Modificación del tamaño de página {#modifying-page-size}

Los registros se procesan en páginas. De forma predeterminada, Clasificaciones de Adobe crea páginas con un tamaño de página de 1000.

Una página puede tener 25000 tamaño máximo por definición en las clasificaciones de Adobe y puede modificarse desde la consola Felix. Durante la exportación, Clasificaciones de Adobe bloquea el nodo de origen para evitar modificaciones simultáneas. El nodo se desbloquea después de la exportación, por error o cuando se cierra la sesión.

Para cambiar el tamaño de la página:

1. Vaya a la consola OSGI en **https://&lt;host>:&lt;port>/system/console/configMgr** y seleccione **Exportador de clasificaciones de Adobe AEM**.

   ![aa-26](assets/aa-26.png)

1. Actualice **Exportar tamaño de página** según sea necesario y, a continuación, haga clic en **Guardar**.

## SAINTefaultTransformer {#saintdefaulttransformer}

>[!NOTE]
>
>Las clasificaciones de Adobe se conocían anteriormente como Exportador de SAINT.

Un exportador puede utilizar un transformador para transformar los datos de exportación a un formato específico. Para las clasificaciones de Adobe, se ha proporcionado una subinterfaz `SAINTTransformer<String[]>` que implementa la interfaz del transformador. Esta interfaz se usa para restringir el tipo de datos a `String[]`, que usa la API de SAINT, y para tener una interfaz de marcador que busque estos servicios para seleccionarlos.

En la implementación predeterminada SAINTDefaultTransformer, los recursos secundarios del origen del exportador se tratan como registros con nombres de propiedad como claves y valores de propiedad como valores. La columna **Key** se agrega automáticamente como primera columna; su valor será el nombre del nodo. No se tienen en cuenta las propiedades de espacio de nombres (que contienen `:`).

*Estructura del nodo:*

* clasificación de id `nt:unstructured`

   * 1 `nt:unstructured`

      * Product = Mi nombre de producto (String)
      * Price = 120.90 (String)
      * Tamaño = M (Cadena)
      * Color = negro (String)
      * Color^Código = 101 (Cadena)

**Encabezado y registro de SAINT:**

| **Clave** | **Producto** | **Precio** | **Tamaño** | **Color** | **Color^Código** |
|---|---|---|---|---|---|
| 1 | Mi nombre de producto | 120,90 | M | black | 101 |

Las propiedades incluyen lo siguiente:

<table>
 <tbody>
  <tr>
   <td><strong>Ruta de propiedad</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>transformador</td>
   <td>Un nombre de clase de una implementación de SAINTransformer</td>
  </tr>
  <tr>
   <td>correo electrónico</td>
   <td>Dirección de correo electrónico de notificación.</td>
  </tr>
  <tr>
   <td>grupos de informes</td>
   <td>ID del grupo de informes para los que se ejecutará el trabajo de importación. </td>
  </tr>
  <tr>
   <td>conjunto de datos</td>
   <td>ID de relación del conjunto de datos para el que se ejecutará el trabajo de importación. </td>
  </tr>
  <tr>
   <td>descripción</td>
   <td>Descripción del trabajo. <br /> </td>
  </tr>
  <tr>
   <td>sobrescribir</td>
   <td>Indicador para sobrescribir los conflictos de datos. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
  <tr>
   <td>divisiones de comprobación</td>
   <td>Marcar para comprobar la compatibilidad de los grupos de informes. El valor predeterminado es <strong>true</strong>.</td>
  </tr>
  <tr>
   <td>deleteprocessed</td>
   <td>Indicador para eliminar los nodos procesados después de la exportación. El valor predeterminado es <strong>false</strong>.</td>
  </tr>
 </tbody>
</table>

## Automatización de la exportación de clasificaciones de Adobe {#automating-adobe-classifications-export}

Puede crear su propio flujo de trabajo para que las nuevas importaciones inicien el flujo de trabajo y creen los datos correspondientes y correctamente estructurados en **/var/export/** para que se puedan exportar a las clasificaciones de Adobe.
