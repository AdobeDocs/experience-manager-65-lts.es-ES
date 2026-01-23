---
title: La ejecución de scripts falla en AEM Forms 6.5 LTS con JBoss EAP 8 (Linux)
description: Al configurar JBoss EAP 8.0 en un entorno Linux, puede encontrar ciertos errores al ejecutar scripts de shell o archivos de inicio
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: d397e6a51ad2a52da5ccb0a690e1acd3fafcee3c
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---


# La ejecución de scripts falla en AEM Forms 6.5 LTS con JBoss EAP 8 (Linux)

## Problema

Al configurar **JBoss EAP 8.0 (AEM Forms 6.5.1 LTS)** en un entorno **Linux**, puede encontrar uno de los siguientes errores al ejecutar scripts de shell o archivos de inicio:

```text
/bin/sh^M: bad interpreter
$'\r': command not found
```

Estos errores se producen cuando se crean o editan scripts de shell o archivos de configuración en un sistema **Windows** y contienen **finales de línea CRLF (Carriage Return + Line Feed)**.
Los sistemas Linux solo admiten **LF (Fuente de línea)** finales de línea, y los finales de línea del estilo de Windows provocan errores de ejecución de scripts.

## Aplicable a

* **JBoss EAP 8.0**
* **Sistemas operativos basados en Linux/UNIX**

## Pasos para solucionar problemas

1. **Identificar el archivo afectado**

   * Revise el resultado del error para identificar el script `.sh` o el archivo de configuración que causa el error.

2. **Convertir el archivo al formato Unix**

   * Utilice la utilidad `dos2unix` para convertir los extremos de línea del estilo de Windows al formato Unix:

     ```bash
     dos2unix <file_name>
     ```

   * Reemplazar `<file_name>` por el script o archivo de configuración real que genera el error.

3. **Repetir si es necesario**

   * Si hay varios scripts afectados, repita la conversión de todos los archivos `.sh` relevantes (por ejemplo, scripts de inicio del instalador, LCM o JBoss).

4. **Vuelva a ejecutar el script**

   * Después de la conversión, vuelva a ejecutar la secuencia de comandos para confirmar que se ha resuelto el problema.

Después de convertir los archivos a finales de línea Unix (LF), se resuelven los errores `/bin/sh^M` y `$'\r': command not found`, y los scripts JBoss se ejecutan correctamente en Linux.
