---
title: Migración de contenido de AEM 6.5 a AEM 6.5 LTS mediante la actualización a Oak
description: Obtenga información sobre cómo migrar contenido de AEM 6.5 a AEM 6.5 LTS mediante la herramienta de actualización de oak
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 8c4ffb0e-b4dc-4a81-ac43-723754cbc0de
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Migración de contenido de AEM 6.5 a AEM 6.5 LTS mediante la actualización a Oak {#aem-65-to-aem-65lts-content-migration-using-oak-upgrade}

Este documento proporciona una guía completa para actualizar Adobe Experience Manager de la versión **6.5** a **6.5 LTS**, centrándose en la migración del repositorio de contenido mediante la herramienta de actualización de oak, una potente utilidad para transferir contenido entre diferentes repositorios con precisión y control.

## Requisitos previos {#prerequisites}

Antes de iniciar la migración, asegúrese de que se cumplen los siguientes requisitos:

1. Compatibilidad con Java: AEM 6.5 LTS debe instalarse y configurarse para ejecutarse con Java™ 17. Una vez configurada, inicie la instancia de AEM y compruebe que todos los paquetes estén activos y en ejecución sin problemas
1. Recursos del sistema: Asegúrese de que haya suficiente espacio en disco y memoria disponibles para gestionar ambos repositorios durante el proceso de migración
1. Herramienta de actualización de Oak: Descargue el JAR `oak-upgrade` del [repositorio oficial de Maven](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade). Asegúrese de que la versión coincida con la versión de oak-core utilizada en AEM 6.5 LTS. La herramienta de actualización de Oak se ejecuta en Oracle® Java™ 11 o posterior

## Proceso de migración paso a paso {#step-by-step-migration-process}

### Detención de AEM 6.5 y AEM 6.5 LTS {#stopping-aem65-and-aem65lts}

Antes de iniciar la migración, detenga las instancias de AEM 6.5 y AEM 6.5 LTS. Esto garantiza que el repositorio esté en un estado estable y que no se produzcan escrituras adicionales durante la migración.

### Copia de seguridad de la instancia de AEM 6.5 {#backing-up-the-aem65-instance}

Realice una copia de seguridad completa de su instancia de AEM 6.5 si no lo ha hecho ya.

### Uso de la herramienta de actualización de Oak para la migración de contenido {#using-the-oak-upgrade-tool-for-content-migration}

La herramienta Oak-Upgrade se ejecuta a través de la línea de comandos, como se muestra a continuación:

```
java -jar oak-upgrade-*.jar [options] /path/to/source/repository /path/to/destination/repository 
```

A continuación se muestran los comandos y las opciones esenciales:

**Opciones de clave**

* `--include-paths`: especifique los subárboles que desea incluir en la migración. Consulte este ejemplo para el uso del comando:

  ```
  java -jar oak-upgrade-*.jar --include-paths=/content/site /old/repository /new/repository
  ```

* `--exclude-paths`: excluir rutas específicas de la migración. Tenga cuidado al utilizar esta opción: si la ruta existe en el sistema de destino, se eliminará. Consulte este ejemplo para el uso del comando:

  ```
  java -jar oak-upgrade-*.jar --exclude-paths=/content/old_site /old/repository /new/repository 
  ```

* `--copy-binaries`: de forma predeterminada, oak-upgrade migra solo referencias a binarios, dejando los archivos reales en el blob/almacén de datos original. Como resultado, el nuevo repositorio sigue dependiendo del almacén de origen para los binarios. Para migrar binarios junto con el contenido del repositorio, utilice el parámetro `--copy-binaries` para copiar todos los datos binarios en el nuevo almacén, como se muestra a continuación:

  ```
  java -jar oak-upgrade-*.jar \
  --copy-binaries \
  --src-datastore=/old/repository/datastore \
  --datastore=/new/repository/datastore \
  /old/repository \
  /new/repository 
  ```

### Migración de puntos de comprobación {#migratiing-checkpoints}

Al migrar un repositorio antiguo de SegmentMK (anterior a Oak 1.6) a un nuevo SegmentMK (versión de Oak mayor o igual a 1.6), también se migran los puntos de comprobación. Esto permite evitar la reindexación cuando Oak se ejecuta por primera vez en el nuevo repositorio. Sin embargo, los puntos de comprobación no se migrarán en los siguientes casos:

1. Se especifican rutas de inclusión, exclusión o combinación personalizadas o
1. Los binarios se copian mediante referencias, no se especifica ningún almacén de datos de origen y dos puntos de comprobación diferentes contienen un binario diferente en la misma ruta.

En el segundo caso, oak-upgrade emite la siguiente advertencia y se interrumpe:

```
Checkpoints won't be copied, because no external datastore has been specified. This will result in the full repository reindexing on the first start. Use --skip-checkpoints to force the migration or see https://jackrabbit.apache.org/oak/docs/migration.html#Checkpoints_migration for more info. 
```

La forma más sencilla de solucionar este problema es especificar el almacén de datos de origen en las opciones de la línea de comandos (por ejemplo, `--src-datastore` o `--src-s3datastore`).

La advertencia también se puede ignorar, pero en este caso el repositorio se reindexará completamente en el primer inicio. Puede ser un proceso largo, especialmente para la gran instancia. El repositorio no se podrá utilizar hasta que se haya completado el proceso de reindexación. Utilice la opción `--skip-checkpoints` para suprimir la advertencia.

También puede reindexar el repositorio sin conexión antes de iniciar AEM usando [reindexación sin conexión](/help/sites-deploying/upgrade-offline-reindexing.md) para evitar la reindexación completa al primer inicio.
