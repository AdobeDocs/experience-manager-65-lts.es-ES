---
title: Metadatos de C2PA [!DNL Experience Manager Assets]
description: Descubra cómo [!DNL Experience Manager Assets] detecta los metadatos de C2PA en los recursos cargados, los marca en la interfaz de usuario y firma las representaciones que genera para los recursos de IA general.
role: User, Admin, Developer
feature: Asset Management, Metadata, Renditions, Workflow, Asset Processing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 042eab9c4b25b320556da14c45408f91014bd2ff
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 6%
---

# Metadatos de C2PA en [!DNL Experience Manager Assets] {#c2pa-metadata}

Las marcas están más preocupadas que nunca por la transparencia del contenido, la divulgación de la inteligencia artificial y la prevención de la manipulación de activos. Content Authenticity Initiative (CAI) en Adobe crea herramientas compatibles con el estándar técnico [Content Provenance and Authenticity](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) (C2PA). Los metadatos C2PA, un nuevo tipo de metadatos a prueba de manipulaciones, ayudan a los espectadores a comprender el linaje del contenido y garantizan la integridad de los activos de la marca. Pueden incluir una amplia gama de datos de procedencia que ofrecen información del historial de un recurso digital.

Esta información incluye lo siguiente:

* **Emisor o firmante:** Información acerca de la entidad o compañía que emitió la firma digital del recurso.
* **Fecha del problema:** Fecha en la que se aplicaron los metadatos de C2PA al recurso.
* **Proceso:** registra las ediciones o modificaciones realizadas en el recurso.
* **Detalles del dispositivo:** información sobre la aplicación o el dispositivo usado para crear o editar el recurso.
* **Herramienta de IA utilizada:** Si se utilizó IA generativa para editar o crear el recurso, se incluye el nombre del modelo utilizado.
* **Otra información relevante:** Datos adicionales que ofrecen más contexto sobre el historial de un recurso.

Para obtener más información sobre el historial de un recurso, consulte [Verificar](https://contentcredentials.org/verify).

[!DNL Adobe Experience Manager Assets] detecta los metadatos de C2PA cuando se carga o actualiza un recurso, marca esos recursos en la interfaz de usuario de [!DNL Assets] y mantiene intacta la información de inteligencia artificial aplicada a la generación en las representaciones que genera [!DNL Experience Manager]. Cada vez que [!DNL Experience Manager] crea o modifica una representación de un recurso de IA general, como una miniatura, una representación web, una copia con marca de agua o una transcodificación de vídeo, [!DNL Experience Manager] firma esa representación con nuevos metadatos de C2PA que hacen referencia al recurso original como su principal. Las representaciones que descargue, publique o comparta conservan su procedencia.

## Requisitos previos {#Prerequisites}

La compatibilidad con Content Credentials requiere el paquete de servicio [!DNL Adobe Experience Manager] 6.5 LTS. En el Service Pack 6.5.3.LTS, instale [AEM 6.5 LTS SP3 - revisión de compatibilidad con C2PA GenAI](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.3-hotfix-ASSETS-75868-1.0.zip).

## Formatos y plataformas compatibles {#supported-formats}

### Formatos {#formats}

[!DNL Experience Manager] firma representaciones en los formatos que [especificación C2PA](https://c2pa.org/specifications/specifications/2.2/specs/C2PA_Specification.html) admite para manifiestos incrustados.

| Tipo | Formatos | Tipos MIME |
|---|---|---|
| Imagen | JPEG, PNG, GIF, TIFF, DNG, WebP, JPEG XL, AVIF, HEIC/HEIF, SVG | `image/jpeg`, `image/png`, `image/gif`, `image/tiff`, `image/x-adobe-dng`, `image/webp`, `image/jxl`, `image/avif`, `image/heic`, `image/heif`, `image/svg+xml` |
| Vídeo | MP4, MOV, AVI | `video/mp4`, `video/quicktime`, `video/x-msvideo` |
| Audio | MP3, M4A, WAV, FLAC | `audio/mpeg`, `audio/mp4`, `audio/wav`, `audio/flac` |

[!DNL Experience Manager] también reconoce alias comunes, como `image/jpg`, `image/pjpeg`, `image/x-png` y `video/mov`. [!DNL Experience Manager] comprueba si hay un manifiesto en todos los recursos cargados, independientemente del formato de archivo. Las representaciones en otros formatos, como PSD o EPS, no están firmadas.

### Plataformas {#platforms}

La compatibilidad con los metadatos de C2PA se basa en un componente nativo de C2PA que se envía dentro del paquete `cq-dam-core`, con una compilación para cada plataforma admitida. Cuando se inicia el servicio, [!DNL Experience Manager] extrae la compilación para la plataforma (`adobe_c2patool` o `adobe_c2patool.exe` en Windows) en la carpeta de datos privada del paquete, comprueba la suma de comprobación SHA-256 y la ejecuta como un proceso independiente. No necesita instalar nada ni cambiar `PATH`.

| Sistema operativo | Arquitectura |
|---|---|
| Linux (glibc 2.28 o posterior, incluido Red Hat Enterprise Linux 8) | `x86_64`, `aarch64` |
| macOS | `x86_64`, `aarch64` (silicio de Apple) |
| Windows | `x86_64` |

Esto funciona igual en [!DNL Adobe Managed Services] y en implementaciones locales. Asegúrese de que el proceso [!DNL Experience Manager] pueda iniciar este ejecutable. Si usa `noexec` montajes, antivirus o software de seguridad de extremos, permita que `adobe_c2patool` se ejecute desde la carpeta `crx-quickstart`. De lo contrario, la compatibilidad con metadatos C2PA no se inicia.

## Funcionamiento de los metadatos de C2PA {#how-c2pa-metadata-works}

La compatibilidad con metadatos de C2PA consta de dos partes: detección cuando se carga o actualiza un recurso y nueva firma cada vez que [!DNL Experience Manager] genera o modifica una representación.

### Configuración de flujo de trabajo {#workflow}

El paso **[!UICONTROL Detectar credencial de C2PA]** que se muestra en [Detectar metadatos de C2PA](#detect) es parte del modelo de flujo de trabajo predeterminado de **[!UICONTROL Recurso de actualización DAM]**. Si utiliza una copia personalizada de ese modelo, agregue el paso usted mismo:

1. En la interfaz de [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]** y abra el modelo en el modo ![Editar icono](assets/edit.svg) **[!UICONTROL Editar]**.
1. Agregue el paso **[!UICONTROL Detectar credencial de C2PA]** después de **[!UICONTROL Procesador de metadatos]**, antes de que cualquier paso genere las representaciones.
1. Seleccione **[!UICONTROL Sincronizar]** para guardar el modelo.

Los pasos de representación firman su salida solo si la detección ya se ha ejecutado en el recurso. Si la detección se ejecuta después de ellos, sus representaciones permanecen sin firmar hasta que se vuelve a ejecutar el flujo de trabajo.

### Detectar metadatos de C2PA {#detect}

El flujo de trabajo **[!UICONTROL Recurso de actualización DAM]** incluye un paso **[!UICONTROL Detectar credencial de C2PA]** que se ejecuta después del paso **[!UICONTROL Procesador de metadatos]**, como se muestra en la figura siguiente. Lee el binario original del recurso y registra el resultado en el nodo de metadatos del recurso `jcr:content/metadata`.

![Flujo de trabajo](assets/workflow.png)

En la tabla siguiente se enumeran las propiedades de metadatos clave del flujo de trabajo de metadatos de C2PA.

| Propiedad | Tipo | Descripción |
|---|---|---|
| `dam:hasC2PAManifest` | `boolean` | `true`, si el binario original tiene un manifiesto C2PA incrustado. Siempre está escrito. |
| `dam:isAiGenerated` | `boolean` | `true`, si el manifiesto coloca el recurso en el ámbito del etiquetado de IA general. Solo se escribe cuando hay un manifiesto. |
| `dam:c2paValidationState` | `string` | Describe el estado de validación del manifiesto: `TRUSTED`, `VALID`, `INVALID` o `UNKNOWN`. Solo se escribe cuando hay un manifiesto. |

Cuando hay un manifiesto, [!DNL Experience Manager] también lo almacena como la representación de `c2pa-manifest.json` (`application/json`).

Si reemplaza el recurso original por un archivo binario sin manifiesto, la siguiente ejecución del flujo de trabajo establece `dam:hasC2PAManifest` en `false` y quita `dam:isAiGenerated`, `dam:c2paValidationState` y la representación `c2pa-manifest.json`.

>[!NOTE]
>
>Un error de detección nunca bloquea la ingesta de recursos. Si al leer el manifiesto se agota el tiempo de espera o falla, [!DNL Experience Manager] registra el error, deja los metadatos sin cambios y continúa con el resto del flujo de trabajo.

### Ver metadatos de C2PA en la interfaz de usuario [!DNL Assets] {#view-c2pa-metadata}

Los Assets que llevan metadatos de C2PA muestran el distintivo **cr** (metadatos de C2PA) en la interfaz de usuario [!DNL Assets]. Vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]** y busque el distintivo en la esquina inferior izquierda de:

* La miniatura del recurso en **[!UICONTROL Vista de tarjeta]**.
* La miniatura del recurso en **[!UICONTROL Vista de columna]**. Seleccione el recurso para mostrar su miniatura.
* El área de vista previa de la página de detalles del recurso.

El distintivo **cr** que se muestra en la siguiente ilustración indica si un recurso contiene metadatos de C2PA. No muestra el manifiesto en sí. Para ver el manifiesto completo, descargue el recurso y ábralo en [Verify](https://contentcredentials.org/verify).

![distintivo cr](assets/cr.png)

[!DNL Experience Manager] almacena el manifiesto detectado como una representación `c2pa-manifest.json` en el recurso. Esta representación es interna. No aparece en el panel **[!UICONTROL Representaciones]** de la página de detalles del recurso ni en el selector de representaciones.

### Firmar representaciones {#sign-renditions}

Una representación es un nuevo archivo binario, por lo que el manifiesto incrustado en el recurso original no lo cubre. Para mantener intacta la divulgación de la inteligencia artificial aplicada a la generación, [!DNL Experience Manager] firma cada representación apta como el último paso del proceso que la produce. Los nuevos metadatos de C2PA:

* Hace referencia al recurso original como su ingrediente **principal**.
* Registra cómo se derivó la representación del recurso original, como una de las acciones de C2PA `c2pa.resized`, `c2pa.transcoded` o `c2pa.edited`.
* Nombra a `Adobe Experience Manager` como agente de software.

[!DNL Experience Manager] firma una representación solamente cuando todas las siguientes `true`:

* El recurso de origen tiene `dam:isAiGenerated` establecido en `true`. Las Assets que llevan un manifiesto pero que no se generan mediante IA siguen mostrando el distintivo **cr**, pero [!DNL Experience Manager] no vuelve a firmar sus representaciones.
* El manifiesto de origen es legible y su estado de validación no es `INVALID`. [!DNL Experience Manager] nunca encadena una nueva firma a un manifiesto en el que se produjo un error en la validación, por ejemplo, después de que se manipulara el recurso.
* El formato de representación admite un manifiesto de C2PA incrustado. Para obtener más información, consulte [Formatos compatibles](#supported-formats). [!DNL Experience Manager] omite los formatos no compatibles sin un error.

Los siguientes pasos del flujo de trabajo **[!UICONTROL Flujo de trabajo del recurso de actualización DAM completado]** que se muestra en [Detectar metadatos de C2PA](#detect) firman su resultado.

| Paso de flujo de trabajo | Representaciones firmadas | Acción de C2PA registrada |
|---|---|---|
| **[!UICONTROL Miniaturas de procesos]** | Representaciones de miniaturas e imagen habilitada para web. | `c2pa.resized` y `c2pa.transcoded` cuando cambia el formato. |
| **[!UICONTROL miniaturas de EPS (con tecnología de ImageMagick)]** | Resultado principal, miniaturas derivadas y representaciones web. | `c2pa.resized`, `c2pa.transcoded` o `c2pa.edited`; |
| **[!UICONTROL Miniaturas FFmpeg]** | Fotogramas y miniaturas de póster de vídeo. | `c2pa.resized` y `c2pa.transcoded` |
| **[!UICONTROL Transcodificación FFmpeg]** | Codificaciones de vídeo. | `c2pa.transcoded` |
| **[!UICONTROL Rasterizar la representación de vista previa de imágenes de PDF/AI]** | Previsualizar representación. (`cqdam.preview.png`) | `c2pa.transcoded` |

Los siguientes procesos de flujo de trabajo también firman su resultado cuando los utiliza en el flujo de trabajo **[!UICONTROL Flujo de trabajo de recursos de actualización DAM completado]**, en otro flujo de trabajo o en un modelo de flujo de trabajo personalizado. Selecciónelas en la lista **[!UICONTROL Miniaturas de procesos]** de un paso del flujo de trabajo como se muestra en [Detectar metadatos de C2PA](#detect).

| Proceso de flujo | Representaciones firmadas | Acción de C2PA registrada |
|---|---|---|
| **[!UICONTROL Crear miniatura]** | Representaciones de miniaturas. | `c2pa.resized` y `c2pa.transcoded` cuando cambia el formato. |
| **[!UICONTROL Crear imagen Web]** | Representaciones web. | `c2pa.resized` y `c2pa.transcoded` cuando cambia el formato. |
| **[!UICONTROL Línea de comandos]**, por ejemplo, con [!DNL ImageMagick] | Resultado principal, miniaturas derivadas y representaciones web. | `c2pa.resized`, `c2pa.transcoded` o `c2pa.edited`; |
| **[!UICONTROL Proceso de marca de agua de imagen]** | Representación con filigrana o la representación original cuando se establece la filigrana. Para obtener más información, vea [Aplicar marcas de agua a los recursos](/help/assets/watermarking.md). | `c2pa.edited` |
| **[!UICONTROL Crear guión gráfico de vídeo]** | Fotogramas clave del guión gráfico. | `c2pa.transcoded` |
| **[!UICONTROL reescritura de XMP]** | Representación original, después de volver a escribir los metadatos. Para obtener más información, consulte [reescritura de XMP en representaciones](/help/assets/xmp-writeback.md). | `c2pa.edited` |

### Proteger el binario original durante la reescritura en XMP {#xmp-writeback}

La reescritura de XMP reescribe el binario original, que rompe su manifiesto incrustado. Para los recursos con `dam:hasC2PAManifest` establecido en `true`, [!DNL Experience Manager] cambia el comportamiento del paso **[!UICONTROL Proceso de reescritura de XMP]** del flujo de trabajo **[!UICONTROL reescritura de metadatos DAM]** de la siguiente manera:

* **Recursos de IA genérica** (`dam:isAiGenerated` es `true`): [!DNL Experience Manager] escribe el XMP y vuelve a firmar el binario original, con el binario de preescritura como principal. Guarda juntos la reescritura y la nueva firma. Si la refirma falla, descarta y falla en el paso.
* **Otros recursos que contienen un manifiesto**: [!DNL Experience Manager] omite la reescritura de XMP y registra el motivo. El binario original y su manifiesto permanecen inalterados.

### Modo de firma {#signing-mode}

[!DNL Experience Manager] firma las representaciones localmente, en la instancia que las produce, con un certificado efímero y autofirmado que genera. La firma no necesita acceso a la red ni configuración de certificado o clave privada.

>[!NOTE]
>
>No puede configurar su propio certificado de firma. Los validadores como [Verify](https://contentcredentials.org/verify) muestran la divulgación de IA general de la representación y el vínculo al original, pero no identifican a su organización como el firmante.

## Configuración de metadatos de C2PA {#configure}

La compatibilidad con metadatos C2PA está habilitada de forma predeterminada. No es necesario instalar ni configurar nada.

### Configuración de OSGi {#osgi-configuration}

Para cambiar la configuración predeterminada, configure el **[!UICONTROL Servicio C2PA de CQ DAM por día]** (PID `com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl`) en el Administrador de configuración en `https://[aem_server]:[port]/system/console/configMgr`como se muestra en la figura siguiente, o agregue una configuración OSGi a su proyecto. Para obtener más información, consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md).

![Configuración de OSGi](assets/OSGi.png)

En la tabla siguiente se enumeran las propiedades de la configuración OSGi del proyecto.

| Propiedad | Nombre en el Administrador de configuración | Predeterminado | Descripción |
|---|---|---|---|
| `enabled` | **[!UICONTROL Habilitado]** | `true` | Activa o desactiva la compatibilidad con metadatos de C2PA. Cuando está desactivado, [!DNL Experience Manager] no detecta manifiestos ni firma representaciones. |
| `timeoutMillis` | **[!UICONTROL Tiempo de espera de CLI (ms)]** | `30000` | Especifica el tiempo máximo, en milisegundos, que [!DNL Experience Manager] espera una única operación de lectura o firma en un archivo antes de tratarlo como con tiempo de espera agotado. Aumente este valor para vídeo de gran tamaño o archivos de imagen de alta resolución. |

Por ejemplo, agregue una configuración OSGi en `/apps/<your-project>/config/com.day.cq.dam.core.impl.c2pa.C2PAServiceImpl.config`.

```text
enabled=B"true"
timeoutMillis=L"60000"
```

### Desactivar compatibilidad con metadatos de C2PA {#disable}

En la configuración **[!UICONTROL Servicio C2PA de CQ DAM por día]** que se muestra en [Configuración de OSGi](#osgi-configuration), deshabilite la opción **[!UICONTROL Habilitado]** y, a continuación, guarde los cambios. El cambio surte efecto inmediatamente sin reiniciar:

* El paso **[!UICONTROL Detectar credencial de C2PA]** que se muestra en [Detectar metadatos de C2PA](#detect) deja de ser operativo.
* Los pasos del flujo de trabajo crean representaciones sin firmarlas.
* Assets procesado anteriormente conservó su propiedad `dam:hasC2PAManifest` y aún muestra el distintivo **cr**.

>[!CAUTION]
>
>Después de deshabilitar la opción **[!UICONTROL Enabled]**, las representaciones de los recursos de IA general no llevan metadatos de C2PA. Si desea cumplir con las regulaciones de divulgación de la inteligencia artificial aplicada a la generación, habilite la opción **[!UICONTROL Enabled]**.

## Personalización de la canalización de procesamiento {#customize}

Para agregar, quitar o reordenar los pasos del **[!UICONTROL recurso de actualización DAM]** y mantener intacta la divulgación de inteligencia artificial aplicada a la generación, siga estas reglas:

* **Ejecute primero la detección.** Mantenga **[!UICONTROL Detectar credencial de C2PA]** antes de cada paso que cree o modifique las representaciones.
* **Firmar el último.** Cualquier cambio en un binario después de la firma invalida su firma. No ejecute pasos que modifiquen una representación después del paso que la firmó.
* **Use pasos que firmen.** Los pasos integrados enumerados en [Firmar representaciones](#sign-renditions) firman su salida. Los pasos personalizados y las herramientas de terceros que se ejecutan a través de cualquier otro proceso que no sea la **[!UICONTROL Línea de comandos]** no firman su resultado a menos que se agregue explícitamente la firma. Para obtener más información, consulte [Procesar recursos mediante controladores de medios y flujos de trabajo](/help/assets/media-handlers.md).
* **No modifique el original en contexto** a menos que el paso lo vuelva a firmar, como lo hacen **[!UICONTROL XMP Writeback]** y **[!UICONTROL Image Watermark Process]**.

### Firmar representaciones desde un paso de flujo de trabajo personalizado {#custom-step}

Los pasos personalizados del flujo de trabajo que producen representaciones pueden firmarlas a través del servicio OSGi `com.day.cq.dam.api.c2pa.C2PASigner`. Aplica las mismas reglas de elegibilidad que los pasos integrados pero en su lugar informa el resultado como `C2PASigningOutcome`.

```java
import java.util.Collections;

import org.osgi.service.component.annotations.Reference;
import org.osgi.service.component.annotations.ReferenceCardinality;
import org.osgi.service.component.annotations.ReferencePolicy;

import com.day.cq.dam.api.Asset;
import com.day.cq.dam.api.Rendition;
import com.day.cq.dam.api.c2pa.C2PAAction;
import com.day.cq.dam.api.c2pa.C2PAConstants;
import com.day.cq.dam.api.c2pa.C2PASigner;
import com.day.cq.dam.api.c2pa.C2PASigningOutcome;

// Inside your WorkflowProcess implementation:

@Reference(cardinality = ReferenceCardinality.OPTIONAL, policy = ReferencePolicy.DYNAMIC)
private volatile C2PASigner c2paSigner;

private void signRendition(Asset asset, Rendition rendition) {
    C2PASigner signer = c2paSigner;
    if (signer == null) {
        return;
    }
    C2PASigningOutcome outcome = signer.signIfEligible(asset, rendition,
            Collections.singletonList(
                    new C2PAAction(C2PAConstants.ACTION_RESIZED, C2PAConstants.SOFTWARE_AGENT, null)));
    if (outcome == C2PASigningOutcome.FAILED) {
        // Log, retry, or alert an operator.
    }
}
```

Llame a `signIfEligible` solo después de que su paso haya terminado de escribir la representación. El servicio OSGi proporciona los métodos enumerados en la tabla siguiente.

| Método | Úselo para lo siguiente |
|---|---|
| `signIfEligible(Asset, Rendition, List<C2PAAction>)` | Firme una nueva representación, con el recurso de origen como su principal. |
| `signIfEligible(Asset, Map<Rendition, List<C2PAAction>>)` | Firmar varias representaciones derivadas del mismo recurso. Este método lee el manifiesto de origen una vez. |
| `captureResignState(Asset)` | Tome una imagen del recurso original antes de que el paso lo modifique en su lugar. Este método devuelve `null` si el recurso no es elegible. |
| `resign(Asset, Rendition, List<C2PAAction>)` | Vuelva a firmar el recurso original después de un cambio local, con la imagen como su principal. |
| `discardResignState(Rendition)` | Coloque una imagen que haya tomado pero que no vaya a usar, por ejemplo, porque el cambio falló. |

Los valores de `C2PASigningOutcome` se mencionan en la siguiente tabla.

| Resultado | Descripción |
|---|---|
| `SIGNED` | [!DNL Experience Manager] firmó la representación. |
| `SKIPPED_SOURCE_NOT_AI_GENERATED` | El recurso de origen no está marcado como un recurso generado por IA. |
| `SKIPPED_FORMAT_NOT_ELIGIBLE` | El formato de representación no admite el manifiesto de C2PA incrustado. |
| `SKIPPED_MANIFEST_UNREADABLE` | [!DNL Experience Manager] no encontró ningún manifiesto en el recurso de origen. |
| `SKIPPED_MANIFEST_NOT_VALID` | Error de validación del manifiesto de origen. |
| `SKIPPED_SERVICE_UNAVAILABLE` | La compatibilidad con metadatos C2PA está desactivada o no está disponible. |
| `FAILED` | Error al leer el manifiesto de origen o al firmar la representación. |

Para comprobar la idoneidad antes de generar una representación costosa, llame a `C2PASupportedFormats.isEligible(...)`.

## Resolución de problemas {#troubleshooting}

Cuando solucione problemas, establezca los siguientes registradores en `DEBUG` en **[!UICONTROL Configuración del registrador de Apache Sling]**.

* `com.day.cq.dam.core.impl.c2pa`: extracción del componente nativo de C2PA, lecturas de manifiesto y firma.
* `com.day.cq.dam.core.process.DetectC2PACredentialProcess`: detección.

| Síntoma | Posible causa | Resolución |
|---|---|---|
| Ningún recurso muestra el distintivo **cr**. | La compatibilidad con metadatos C2PA está desactivada o el modelo de flujo de trabajo no incluye el paso de detección. | Compruebe que **[!UICONTROL Enabled]** esté habilitado en la configuración de **[!UICONTROL Day CQ DAM C2PA Service]** y que su modelo **[!UICONTROL DAM Update Asset]** incluya **[!UICONTROL Detectar credencial de C2PA]**. |
| Un recurso que sabe que tiene un manifiesto pero no muestra distintivo. | El recurso se cargó antes de que la función estuviera disponible. | Ejecute de nuevo el flujo de trabajo **[!UICONTROL DAM Update Asset]** en el recurso, por ejemplo, desde **[!UICONTROL Cronología]** > **[!UICONTROL Iniciar flujo de trabajo]**. |
| El servicio no se inicia. El registro de errores informa de que `adobe_c2patool` no se puede extraer ni marcar como ejecutable. | No existe ningún binario para el sistema operativo o la arquitectura, o bien el sistema de archivos bloquea los ejecutables. | Utilice una plataforma compatible. Permitir que el proceso [!DNL Experience Manager] ejecute los ejecutables desde su carpeta `crx-quickstart`. |
| El registro de errores informa de `GLIBC_2.xx not found`. | El host de Linux ejecuta una versión glibc anterior a la 2.28. | Actualice el sistema operativo del host. |
| Se agotó el tiempo de espera de detección o firma. | Los archivos grandes tardan más tiempo que el tiempo de espera predeterminado de 30 segundos. | Aumentar **[!UICONTROL tiempo de espera de CLI (ms)]**. |
| Las representaciones de un recurso de IA general no están firmadas. | El formato no es compatible, el manifiesto es `INVALID` o la detección se ejecutó después del paso de representación. | Compruebe `dam:c2paValidationState` y el formato de representación. Adelantar **[!UICONTROL Detectar credencial de C2PA]** a los pasos de representación. |
| La reescritura de XMP no actualiza un recurso. | El recurso lleva un manifiesto, pero no se genera mediante IA, por lo que [!DNL Experience Manager] mantiene su original sin cambios. | Este es un comportamiento esperado. Para obtener más información, consulte [Proteger el original durante la reescritura en XMP](#xmp-writeback). |

## Limitaciones {#limitations}

* La interfaz de usuario [!DNL Assets] solo muestra si hay metadatos de C2PA. No tiene panel para los detalles del manifiesto.
* [!DNL Experience Manager] vuelve a firmar representaciones solo para los recursos generados a través de IA. Las representaciones de otros recursos que llevan un manifiesto se crean sin metadatos de C2PA.
* [!DNL Experience Manager] firma con un certificado efímero y autofirmado. No se admiten certificados de firma personalizados o específicos de la organización.


>[!MORELIKETHIS]
>
>* [Metadatos de C2PA en la vista de Assets de [!DNL Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/assets-view/c2pa-metadata-assets-view)
>* [Metadatos de C2PA en [!DNL Experience Manager Assets Essentials]](https://experienceleague.adobe.com/es/docs/experience-manager-assets-essentials/help/content-credentials)
>* [Metadatos de C2PA en [!DNL Dynamic Media]](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/c2pa-metadata)
>* [reescritura de XMP en representaciones](/help/assets/xmp-writeback.md)
>* [Marca de agua de tus recursos](/help/assets/watermarking.md)
>* [Content Authenticity Initiative](https://contentauthenticity.org/)
>* [Verificar](https://contentcredentials.org/verify)
