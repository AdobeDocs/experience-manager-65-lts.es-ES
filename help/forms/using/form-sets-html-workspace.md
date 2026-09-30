---
title: Usar conjuntos de formularios en AEM Forms Workspace
description: Un conjunto de formularios es una colección de formularios HTML5 agrupados y presentados como un único conjunto de formularios para los usuarios finales. Aprenda a trabajar con conjuntos de formularios AEM Forms Workspace.
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
exl-id: 4b2c994e-8ca6-42fc-a8b2-96c53e9f9453
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 100%
---
# Usar conjuntos de formularios en AEM Forms Workspace{#working-with-formsets-in-aem-forms-workspace}

Un conjunto de formularios es una colección de formularios HTML5 agrupados y presentados como un único conjunto de formularios para los usuarios finales. Cuando estos empiezan a rellenar un conjunto de formularios, pueden desplazarse de un formulario a otro sin problemas. El conjunto de formularios se puede enviar en un solo clic. Para obtener más información sobre los conjuntos de formularios y cómo configurarlos, consulte [Conjunto de formularios en AEM Forms](../../forms/using/formset-in-aem-forms.md).

AEM Forms Workspace admite conjuntos de formularios. Los conjuntos de formularios permiten agrupar varios formularios relacionados con un servicio o un proceso para automatizar un proceso empresarial y presentarlos a los usuarios finales. En este caso, los usuarios pueden rellenar todo el conjunto como un único formulario, y no es necesario archivar, enviar ni realizar un seguimiento de los formularios o procesos individuales.

## Adjuntar un conjunto de formularios a un punto de inicio en una aplicación de AEM Forms Workspace {#attaching-a-formset-to-startpoint-in-an-aem-forms-workspace-app-br}

1. Cree el flujo de trabajo del proceso empresarial en Workbench. Para obtener más información, consulte [la Ayuda de Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).
1. En las propiedades de proceso del punto de inicio, seleccione **Usar un recurso CRX** en Presentación y datos.

   ![1-3](assets/1-3.png)

1. Haga clic en ![Examinar](assets/browse.png) (Examinar) junto a la ruta del recurso CRX. Aparecerá el cuadro de diálogo Seleccionar recurso de formulario.

   ![2-1](assets/2-1.png)

1. Haga clic en la pestaña **Conjunto de formularios**, seleccione el conjunto de formularios correspondiente en la lista y, a continuación, haga clic en **Aceptar**.

1. Implemente la aplicación después de actualizar otras propiedades de proceso relevantes.

## Uso de conjuntos de formularios en AEM Forms Workspace {#using-formset-in-nbsp-aem-forms-workspace}

Una vez que se adjunta un conjunto de formularios a un punto de inicio, este puede invocarse como cualquier otro punto de inicio desde AEM Forms Workspace.

Las operaciones admitidas en los conjuntos de formularios a través de AEM Forms Workspace son:

* Guardar como borrador
* Bloquear
* Abandonar
* Enviar
* Añadir archivos adjuntos
* Agregar notas
* Desplazarse entre los formularios de un conjunto de formularios utilizando los botones Atrás o Siguiente

![3-1](assets/3-1.png)

>[!NOTE]
>
>Para mejorar el rendimiento durante el desplazamiento entre los formularios de un conjunto de formularios, todos los botones del espacio de trabajo (Atrás, Siguiente, Guardar, Enviar y ... [Más]) se desactivan hasta que el formulario correspondiente termina de procesarse.
