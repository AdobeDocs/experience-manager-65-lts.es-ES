---
title: Actualizar el tipo de licencia para la implementación
description: Actualice el tipo de licencia para la implementación mediante la página Cambiar licencia en la consola de administración.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/get_started_with_administering_aem_forms_on_jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 4%

---

# Actualizar el tipo de licencia para la implementación {#update-the-license-type-for-the-deployment}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Como parte del proceso de instalación de los formularios AEM Forms, utilizó el Administrador de configuración para configurar e implementar los módulos de formularios AEM Forms que necesita. De forma predeterminada, estos módulos se configuran con una licencia de evaluación de 60 días. Utilice la página Cambiar licencia de la consola de administración para cambiar el tipo de licencia de la implementación. Los módulos implementados actualmente se muestran en la página Cambiar licencia.

La página Cambiar licencia muestra información sobre la licencia:

* El tipo de licencia actual
* La fecha y hora de la última actualización de la licencia
* Quién realizó la última actualización
* El estado actual de la licencia
* La fecha en la que se instalaron los formularios AEM
* La fecha en la que caducará la licencia actual

>[!NOTE]
>
>El cambio de licencia se aplica a todos los módulos implementados. Antes de cambiar el tipo de licencia, anule la implementación de los módulos sin licencia. No seleccione el tipo de licencia de producción si la lista de módulos implementados contiene módulos distintos de los adquiridos en Adobe.

## Actualizar el tipo de licencia {#update-the-license-type}

1. En la consola de administración, haga clic en Licencias.
1. Lea el acuerdo de licencia para el usuario final de AEM forms, seleccione Acepto si está de acuerdo con los términos del acuerdo y, a continuación, haga clic en Siguiente.
1. En la página Cambiar licencia, seleccione un tipo de licencia:

   * **EVAL:** licencia de evaluación de 60 días
   * **DEV:** Licencia de desarrollo permanente
   * **NFR:** licencia de evaluación de 2 años
   * **IDEV:** suscripción de 1 año al programa Adobe Developer
   * **Producción:** Licencia perpetua

1. Seleccione Sí, El Cambio De Licencia Es Válido Para Todos Los Módulos Implementados.
1. Haga clic en Confirmar cambio de licencia. Aparece un mensaje que indica que la licencia se ha actualizado correctamente.
