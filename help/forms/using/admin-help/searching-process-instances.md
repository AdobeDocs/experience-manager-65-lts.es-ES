---
title: Buscar instancias de proceso
description: Utilice la página Buscar Proceso para introducir criterios de búsqueda para buscar una instancia de proceso.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: e358ee51-c23f-4737-9dcf-3193ed541bbb
source-git-commit: 51342861dd01e659999c19fbe0274e8d3cbcf8c4
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 1%

---

# Buscar instancias de proceso{#searching-for-process-instances}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Utilice la página Buscar Proceso para introducir criterios de búsqueda para buscar una instancia de proceso. Puede acceder a la página Buscar Proceso desde la página Forms Workflow. O bien, puede hacer clic en **Buscar** en la página Instancia de proceso.

Puede introducir criterios básicos para realizar una búsqueda general, atributos específicos para realizar una búsqueda detallada o una combinación de criterios básicos y atributos específicos para realizar una búsqueda combinada.

## Realizar una búsqueda general {#perform-a-general-search}

La búsqueda general de un proceso es más apropiada si conoce el ID de proceso de la instancia de proceso. O bien, si está buscando un grupo de instancias de proceso relacionadas o si solo se están ejecutando unas pocas instancias de proceso.

Introduzca los criterios básicos para realizar una búsqueda general. Si introduce varios criterios, la búsqueda se realiza con una condición AND implícita.

1. En la consola de administración, haga clic en Servicios > Forms Workflow > Búsqueda de procesos.
1. En la página Buscar proceso, en Búsqueda general, proporcione los siguientes criterios:

   * **Id. de proceso:** El entero positivo que identifica cada instancia de proceso única.
   * **Estado del proceso:** Seleccione un estado de la lista.
   * **Aplicación:** Seleccione una aplicación de la lista. Solo se muestran las aplicaciones implementadas.
   * **Nombre del proceso - Versión:** Seleccione un nombre de proceso en el menú. Solo se muestran los procesos implementados.

1. Haga clic en **Buscar**. Aparecerá la página Instancia de Proceso, que enumera las instancias encontradas.

## Realizar una búsqueda detallada de un proceso {#perform-a-detailed-search-for-a-process}

Puede introducir atributos específicos para realizar una búsqueda detallada. Una búsqueda detallada es más apropiada si tiene muchas instancias de proceso en ejecución y necesita reducir los posibles hallazgos según ciertos criterios.

1. En la consola de administración, haga clic en Servicios > Forms Workflow > Búsqueda de procesos.
1. En la página Buscar proceso, en Búsqueda detallada, especifique el primer conjunto de criterios:

   * En la lista Atributo, seleccione un atributo.
   * En la lista Filtro, seleccione un operador.
   * En el cuadro Valor, escriba un valor apropiado para el atributo seleccionado.

1. Para agregar otra fila, seleccione Más filtros. Aparecerá otro conjunto de listas de atributos, filtros y valores, así como una lista de condiciones.
1. En Condición, seleccione AND u OR. Repita los pasos del 1 al 3 según sea necesario para acotar aún más la búsqueda.
1. Para agregar o quitar filas, haga clic en Más filtros o Menos filtros. Puede tener de una a cuatro filas.
1. Haga clic en **Buscar**. Aparecerá la página Instancia de Proceso, que enumera las instancias encontradas.

Consulte también [Acerca de los estados de instancias de proceso](/help/forms/using/admin-help/processes.md#about-process-instance-statuses).

## Realizar una búsqueda combinada de un proceso {#perform-a-combined-search-for-a-process}

Para crear una búsqueda que utilice criterios generales y detallados, introduzca valores en ambas áreas en la página Buscar Proceso. El sistema aplica un `AND` implícito entre las dos áreas.

Si la búsqueda es demasiado limitada, no se encuentra ninguna instancia.
