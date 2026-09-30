---
title: Uso de registros
description: Obtenga información sobre cómo solucionar problemas de AEM trabajando con registros.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: f286ca06-e567-4d77-a0ff-6786a8bbf32a
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 5%
---
# Uso de registros{#working-with-logs}

Esta sección incluye información detallada sobre los registros disponibles para ayudarle a solucionar problemas.

>[!NOTE]
>
>Para obtener más información sobre los registros, consulte:
>
>* [Mantenimiento del registro de auditoría en AEM](/help/sites-administering/operations-audit-log.md)
>* [Trabajando con registros de auditoría y archivos de registro](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)

CRX registra los registros detallados. Después de desempaquetar e iniciar Quickstart, puede encontrar registros en las siguientes ubicaciones:

* crx-quickstart/launchpad/logs
* crx-quickstart/server/logs
* crx-quickstart/logs

## Activación del nivel de registro de depuración {#activating-the-debug-log-level}

El nivel de registro predeterminado es INFO, es decir, los mensajes de DEPURACIÓN no se registran.

Para activar el nivel de registro DEBUG, utilice el explorador de CRX para establecer el

```xml
/libs/sling/config/org.apache.sling.commons.log.LogManager/org.apache.sling.commons.log.level
```

propiedad para depurar. No deje el registro en el nivel de registro DEBUG más tiempo del necesario, ya que genera numerosos registros.

Una línea del archivo de depuración suele comenzar con DEBUG y, a continuación, proporciona el nivel de registro, la acción del instalador y el mensaje de registro. Por ejemplo:

```xml
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

Los niveles de registro son los siguientes:

| 0 | Error grave | La acción ha fallado y el instalador no puede continuar. |
|---|---|---|
| 1 | Error | La acción ha fallado. La instalación continúa, pero una parte de CRX no se instaló correctamente y no funcionará. |
| 2 | Advertencia | La acción se realizó correctamente pero se encontraron problemas. Es posible que CRX funcione o no correctamente. |
| 3 | Información | La acción se ha realizado correctamente. |

## Opción detallada utilizada para la resolución de problemas {#verbose-option-used-for-troubleshooting}

Al iniciar CRX, puede agregar la opción -v (detallada) a la línea de comandos como en:

` java -jar crx-<*version*>-<*edition*>.jar -v`

Utilice la opción detallada para la resolución de problemas, ya que esta opción muestra algunos de los resultados del registro de inicio rápido en la consola.
