---
title: Registrar flujos de trabajo de AEM Forms
description: Obtenga información sobre cómo depurar los problemas del flujo de trabajo de AEM Forms y habilitar el registro de depuración para los flujos de trabajo de AEM Forms para ver los registros.
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 77%

---

# Registrar flujos de trabajo de AEM Forms{#logging-in-aem-forms-workflows}

Los pasos de Forms Workflow proporcionan registros detallados para depurar convenientemente los problemas relacionados con los flujos de trabajo. Habilite el registro de depuración de los flujos de trabajo de AEM Forms para ver los registros.

De forma predeterminada, toda la información del registro está disponible en el archivo **error.log** del directorio */crx-repository/logs/*.

Los registros de depuración de los flujos de trabajo de formularios incluyen:

* La entrada de cada paso del flujo de trabajo. Por ejemplo:\
  `[DEBUG] "Executing Invoke DDX Process step"`

* La salida de cada paso del flujo de trabajo. Por ejemplo:\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Mensajes de invocación del servicio. Por ejemplo:\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Mensajes de salida del servicio. Por ejemplo:\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variables leídas desde el mapa de metadatos. Por ejemplo:\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variables escritas en el repositorio JCR. Por ejemplo:

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* Mensajes de excepción con seguimiento de pila completo. Por ejemplo:\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Parámetros de metadatos de paso dinámico. Por ejemplo:

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

El siguiente ejemplo ilustra los registros del paso Firmar documento:

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilice los registros para evaluar lo siguiente:

* Utiliza una configuración correcta de Adobe Sign.
* El servicio de Adobe Sign se cierra después de crear correctamente un acuerdo.
* El paso Firmar documento se cierra con un mensaje de éxito.

Si se produce una excepción, puede ver el seguimiento de pila completo para evaluar la causa del error.

## Habilitar el registro de depuración en flujos de trabajo de AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Haga lo siguiente para poder habilitar el registro de depuración para los flujos de trabajo de AEM Forms:

1. Vaya al Administrador de configuración de la consola web de AEM en:

   https://&#39;[server]:[puerto]&#39;/system/console/configMgr

1. Seleccione **[!UICONTROL Sling]** > **[!UICONTROL Compatibilidad de registros]**.
1. Seleccione **[!UICONTROL Agregar nuevo registrador.]**
1. Seleccione **[!UICONTROL Depuración]** como **[!UICONTROL Nivel de registro]**.
1. Especifique la ubicación del archivo de registro. La ubicación predeterminada para el archivo de registro es *logs\error.log*.
1. Especifique el nombre del paquete como **com.adobe.granite.workflow.core** en la columna **[!UICONTROL Registrador]**.

   La ejecución de estos pasos permite almacenar los registros de depuración del paquete **com.adobe.granite.workflow.core**. Seleccione **[!UICONTROL +]** y agregue los siguientes nombres de paquete a la lista:

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
