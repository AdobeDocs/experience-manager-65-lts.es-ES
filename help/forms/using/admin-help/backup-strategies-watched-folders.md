---
title: Estrategias de copia de seguridad para carpetas vigiladas
description: Este documento describe cómo las carpetas vigiladas se ven afectadas por diferentes escenarios de copia de seguridad y recuperación, las limitaciones y los resultados de estos escenarios y cómo minimizar la pérdida de datos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5955deb0-9d1c-4b61-a202-41ef03a23cf8
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 1%

---

# Estrategias de copia de seguridad para carpetas vigiladas {#backup-strategies-for-watched-folders}

Este contenido describe cómo las carpetas vigiladas se ven afectadas por diferentes escenarios de copia de seguridad y recuperación, las limitaciones y los resultados de estos escenarios y cómo minimizar la pérdida de datos.

*La carpeta inspeccionada* es una aplicación basada en el sistema de archivos que invoca operaciones de servicio configuradas que manipulan el archivo en una de las siguientes carpetas de la jerarquía de carpetas inspeccionadas:

* Entrada
* Escenario
* Salida
* Error
* Conservar

Un usuario o una aplicación cliente suelta primero el archivo o la carpeta en la carpeta de entrada. A continuación, la operación de servicio mueve el archivo a la carpeta de fase para su procesamiento. Una vez que el servicio realiza la operación especificada, guarda el archivo modificado en la carpeta de salida. Los archivos de origen procesados correctamente se mueven a la carpeta de conservación y los archivos de procesamiento erróneos se mueven a la carpeta de errores. Cuando el atributo `Preserve On Failure` de la carpeta vigilada está habilitado, los archivos de origen procesados con errores se mueven a la carpeta de conservación. (Consulte [Configuración de puntos finales de carpetas vigiladas](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)).

Puede realizar una copia de seguridad de las carpetas vigiladas realizando una copia de seguridad del sistema de archivos.

>[!NOTE]
>
>Esta copia de seguridad es independiente de la base de datos o del proceso de copia de seguridad y recuperación del almacenamiento de documentos.

## Cómo funcionan las carpetas vigiladas {#how-watched-folders-work}

Este contenido describe el proceso de manipulación de archivos de carpetas inspeccionadas. Es importante comprender este proceso antes de desarrollar un plan de recuperación. En este ejemplo, el atributo `Preserve On Failure` de la carpeta vigilada está habilitado. Los archivos se procesan en el orden en que llegan.

En la tabla siguiente se describe la manipulación de cinco archivos de ejemplo (archivo1, archivo2, archivo3, archivo4, archivo5) a lo largo del proceso. En la tabla, el eje x representa el tiempo, como Tiempo 1 o T1, y el eje y representa las carpetas dentro de la jerarquía de carpetas vigilada, como Entrada.

<table>
 <thead>
  <tr>
   <th><p>Carpeta</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Entrada</p></td>
   <td><p>archivo1, archivo2, archivo3, archivo4</p></td>
   <td><p>archivo2, archivo3, archivo4</p></td>
   <td><p>archivo3, archivo4</p></td>
   <td><p>file4</p></td>
   <td><p>vaciar</p></td>
   <td><p>file5</p></td>
   <td><p>vaciar</p></td>
  </tr>
  <tr>
   <td><p>Escenario</p></td>
   <td><p>vaciar</p></td>
   <td><p>archivo1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>vaciar</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>Salida</p></td>
   <td><p>vaciar</p></td>
   <td><p>vaciar</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Error</p></td>
   <td><p>vaciar</p></td>
   <td><p>vaciar</p></td>
   <td><p>vaciar</p></td>
   <td><p>vaciar</p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
  </tr>
  <tr>
   <td><p>Conservar</p></td>
   <td><p>vaciar</p></td>
   <td><p>vaciar</p></td>
   <td><p>archivo1 </p></td>
   <td><p>archivo1, archivo2 </p></td>
   <td><p>archivo1, archivo2 </p></td>
   <td><p>archivo1, archivo2, archivo4 </p></td>
   <td><p>archivo1, archivo2, archivo4 </p></td>
  </tr>
 </tbody>
</table>

El siguiente texto describe la manipulación de archivos cada vez:

**T1:** Los cuatro archivos de ejemplo se colocan en la carpeta de entrada.

**T2:** La operación de servicio mueve el archivo1 a la carpeta de fase para su manipulación.

**T3:** La operación de servicio mueve file2 a la carpeta de fase para su manipulación. Coloca los resultados de archivo1 en la carpeta de salida y mueve archivo1 a la carpeta de conservación.

**T4:** La operación de servicio coloca file3 en la carpeta de fase para su manipulación. Coloca los resultados de archivo2 en la carpeta de salida y coloca archivo2 en la carpeta de conservación.

**T5:** La operación de servicio coloca file4 en la carpeta de fase para su manipulación. La manipulación del archivo3 falla y la operación de servicio lo coloca en la carpeta de errores.

**T6:** La operación de servicio coloca el archivo5 en la carpeta de entrada. Coloca los resultados de file4 en la carpeta de salida y coloca file4 en la carpeta de conservación.

**T7:** La operación de servicio coloca el archivo5 en la carpeta de fase para su manipulación.

## Copia de seguridad de carpetas vigiladas {#backing-up-watched-folders}

Se recomienda realizar una copia de seguridad de todo el sistema de archivos de carpetas vigiladas en otro sistema de archivos.

## Restauración de carpetas vigiladas {#restoring-watched-folders}

En esta sección se describe cómo restaurar carpetas vigiladas. Las carpetas inspeccionadas suelen invocar procesos de corta duración que se completan en un minuto. En estos casos, restaurar la carpeta vigilada con una copia de seguridad que se realiza cada hora no evita la pérdida de datos.

Por ejemplo, si se realiza una copia de seguridad en el momento T1 y el servidor falla en T7, se manipularán los archivos file1, file2, file3 y file4. La restauración de la carpeta vigilada con una copia de seguridad realizada en T1 no evita la pérdida de datos.

Si se ha realizado una copia de seguridad más reciente, puede restaurar los archivos. Al restaurar los archivos, tenga en cuenta en qué carpeta de jerarquía de carpetas inspeccionada reside el archivo actual:

**Fase:** Los archivos de esta carpeta se procesarán de nuevo una vez restaurada la carpeta vigilada.

**Entrada:** Los archivos de esta carpeta se vuelven a procesar después de restaurar la carpeta vigilada.

**Resultado:** Los archivos de esta carpeta no se procesan.

**Salida:** Los archivos de esta carpeta no se procesan.

**Conservar:** Los archivos de esta carpeta no se procesan.

## Estrategias para minimizar la pérdida de datos {#strategies-to-minimize-data-loss}

Las siguientes estrategias pueden minimizar la pérdida de datos de la carpeta de entrada y salida al restaurar una carpeta vigilada:

* Realice copias de seguridad de las carpetas de resultados y errores con frecuencia, por ejemplo, cada hora, para evitar la pérdida de archivos de resultados y errores.
* Haga una copia de seguridad de los archivos de entrada en una carpeta que no sea la carpeta vigilada. Esto garantiza la disponibilidad del archivo después de la recuperación en caso de que no pueda encontrar los archivos en la carpeta de salida o de error. Asegúrese de que el esquema de nomenclatura de archivos sea coherente.

  Por ejemplo, si está guardando la salida con `%F.`*extensión*, el archivo de salida tendrá el mismo nombre que el archivo de entrada. Esto le ayuda a determinar qué archivos de entrada se manipulan y cuáles se deben volver a enviar. Si sólo ve archivo1_out en la carpeta de resultados y no archivo2_out, archivo3_out y archivo4_out, debe volver a enviar archivo2, archivo3 y archivo4.

* Si la copia de seguridad de la carpeta inspeccionada que está disponible es anterior al tiempo que tarda en procesar el trabajo, debe permitir al sistema crear una carpeta inspeccionada y colocar automáticamente los archivos en la carpeta de entrada.
* Si la última copia de seguridad disponible no es lo suficientemente reciente, el tiempo de copia de seguridad es menor que el tiempo que tarda en procesar los archivos y se restaura la carpeta vigilada, el archivo se manipuló en una de las siguientes fases diferentes:

   * **Fase 1:** en la carpeta de entrada
   * **Fase 2:** Se copió en la carpeta de fase, pero el proceso aún no se ha invocado
   * **Fase 3:** copiado en la carpeta de fase y se invoca el proceso
   * **Fase 4:** manipulación en curso
   * **Fase 5:** resultados devueltos

  Si los archivos se encuentran en la fase 1, se manipularán. Si los archivos se encuentran en las fases 2 o 3, colóquelos en la carpeta de entrada para que la manipulación tenga lugar de nuevo.

  >[!NOTE]
  >
  >Si la manipulación de un archivo se produce más de una vez, se evitará la pérdida de datos, pero los resultados pueden duplicarse.

## Conclusión {#conclusion}

Debido a la naturaleza dinámica y en constante cambio de una carpeta vigilada, la restauración de las carpetas vigiladas debe realizarse con archivos de los que se realiza una copia de seguridad en un día. Una práctica recomendada sería realizar una copia de seguridad de los resultados, almacenar la carpeta de entrada en un servidor y rastrear los archivos de entrada para que pueda volver a enviar el trabajo si se produce un error.
