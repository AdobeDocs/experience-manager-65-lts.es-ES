---
title: 'Base de datos de Microsoft SQL Server: Ajustar la configuración'
description: Aprenda a ajustar la configuración de la base de datos de Microsoft SQL Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: dab3ad11-d64a-4a13-a015-379a66e7f29d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 4%

---

# Base de datos de Microsoft SQL Server: Ajustar la configuración {#microsoft-sql-server-database-fine-tuning-the-configuration}

Debe cambiar las opciones de configuración predeterminadas al utilizar Microsoft SQL Server. Haga clic con el botón derecho en el servidor local de Oracle Enterprise Manager para acceder al cuadro de diálogo de propiedades.

## Configuración de memoria {#memory-settings}

Cambie la asignación de memoria mínima al mayor número posible. Si la base de datos se está ejecutando en un equipo independiente, utilice toda la memoria. La configuración predeterminada no asigna memoria de forma agresiva, lo que dificulta el rendimiento en casi cualquier base de datos. Debe ser más agresivo a la hora de asignar memoria en las máquinas de producción.

## Ajustes del procesador {#processor-settings}

Modifique la configuración del procesador y, lo que es más importante, active la casilla de verificación Aumentar prioridad de SQL Server en Windows para que el servidor utilice tantos ciclos como sea posible. La configuración Usar fibras NT es menos importante, pero es posible que también desee seleccionarla.

## Configuración de base de datos {#database-settings}

Cambiar la configuración de la base de datos. La configuración más importante es Intervalo de recuperación, que especifica la cantidad máxima de tiempo que se debe esperar para la recuperación después de un bloqueo. El valor predeterminado es de un minuto. El uso de un valor mayor, de 5 a 15 minutos, mejora el rendimiento porque da al servidor más tiempo para escribir los cambios del registro de base de datos en los archivos de base de datos.

>[!NOTE]
>
>Esta configuración no compromete el comportamiento transaccional porque cambia únicamente la duración de la reproducción del archivo de registro que debe realizarse al inicio.

Establezca el tamaño asignado para el registro y el archivo de datos en un valor mucho mayor que el de la base de datos inicial. Considere cuánto puede crecer la base de datos durante un año. Lo ideal es que los archivos de registro y de datos se asignen en una extensión contigua para que los datos no terminen fragmentados por todo el disco.
