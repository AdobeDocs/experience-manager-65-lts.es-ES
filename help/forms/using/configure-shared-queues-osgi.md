---
title: Configurar colas compartidas
description: Aprenda a utilizar colas compartidas en flujos de trabajo centrados en formularios en AEM Forms en OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on OSGi
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 100%

---

# Compartir y solicitar acceso a los elementos de la bandeja de entrada de un usuario {#share-and-request-access}

Una cola es una lista de elementos de la Bandeja de entrada de AEM de un usuario. Pueden ser elementos asignados a un usuario o elementos compartidos con el grupo al que pertenece un usuario. Puede acceder a la Bandeja de entrada para ver y realizar acciones con un elemento de la Bandeja de entrada. Por ejemplo, compartir un elemento con otro usuario.

También puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario tiene acceso a los elementos de la Bandeja de entrada, ese usuario puede reclamar y realizar las acciones adecuadas con los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada de otros usuarios.

## Requisitos previos {#pre-requisites}

El usuario que ha iniciado sesión debe ser miembro del grupo `workflow-users`. El usuario solo puede compartir elementos o solicitar acceso a elementos de usuarios en los que el usuario que ha iniciado sesión tiene permisos de lectura o usuarios que han habilitado el perfil público.

## Compartir uno o todos los elementos de la Bandeja de entrada con otro usuario

La bandeja de entrada AEM permite compartir uno o todos los elementos de la bandeja de entrada con otro usuario.

### Compartir todos los elementos de la Bandeja de entrada

Siga estos pasos para compartir todos los elementos de una Bandeja de entrada con otro usuario:

1. Inicie sesión en la instancia de AEM. Seleccione el icono ![Bandeja de entrada](assets/bell.svg) y luego seleccione **[!UICONTROL Ver todo]**. Aparecerá una lista de los elementos de la Bandeja de entrada.
1. Seleccione ![Selector de vista](assets/viewlist.svg) o el icono ![Selector de vista](assets/calendar.svg) junto al botón **[!UICONTROL Crear]** y luego seleccione **[!UICONTROL Configuración]**.  Aparece el cuadro de diálogo Configuración.
1. Abra la pestaña **[!UICONTROL Compartir]** en el cuadro de diálogo Configuración.
1. Introduzca el nombre de un usuario en el cuadro de texto **[!UICONTROL Conceder acceso a los elementos de la Bandeja de entrada]** y seleccione **[!UICONTROL Conceder]**. Repita el paso para agregar más usuarios. Todos los usuarios con acceso a sus elementos aparecen en la sección **Nombre de usuario**.
1. Seleccione **[!UICONTROL Guardar]**.

>[!NOTE]
>
>(Solo para elementos de los flujos de trabajo centrados en formularios) Active la opción **[Permitir que el usuario asignado comparta elementos a través del uso compartido de la Bandeja de entrada](aem-forms-workflow-step-reference.md)** del paso **Asignar tarea** del flujo de trabajo. Solo se mostrarán a los demás usuarios los elementos que tengan la opción mencionada activada.

### Compartir elementos individuales

Realice los siguientes pasos para compartir un elemento de la Bandeja de entrada con otro usuario:

1. Inicie sesión en la instancia de AEM. Seleccione el icono ![Bandeja de entrada](assets/bell.svg) y luego seleccione **[!UICONTROL Ver todo]**. Aparecerá una lista de los elementos de la Bandeja de entrada.
1. Seleccione un elemento y seleccione **[!UICONTROL Compartir]**. Aparecerá un cuadro de diálogo.
1. Escriba el nombre de un usuario en el cuadro de texto Agregar usuarios para compartir este elemento y seleccione **[!UICONTROL Agregar]**. Repita el paso para agregar más usuarios. Todos los usuarios con acceso a sus elementos aparecen en la sección **[!UICONTROL Nombre de usuario]**.
1. Seleccione **[!UICONTROL Guardar]**.


>[!NOTE]
>
>(Solo para elementos de los flujos de trabajo centrados en formularios) Active la opción **[Permitir que el usuario asignado comparta explícitamente elementos en la Bandeja de entrada](aem-forms-workflow-step-reference.md)** del paso **Asignar tarea** del flujo de trabajo. Solo se mostrarán a los demás usuarios los elementos que tengan la opción mencionada activada.

## Solicitar acceso a los elementos de la bandeja de entrada {#request-access}

Puede solicitar acceso a los elementos de la Bandeja de entrada de otro usuario. Una vez concedido el acceso, podrá visualizar, reclamar y realizar las acciones adecuadas con los elementos compartidos. Realice los siguientes pasos para solicitar acceso a los elementos de la Bandeja de entrada de otro usuario:

1. Inicie sesión en la instancia de AEM. Seleccione el icono ![Selector de vista](assets/bell.svg) y luego seleccione **[!UICONTROL Ver todo]**.
1. Seleccione ![Selector de vista](assets/viewlist.svg) o el icono ![Selector de vista](assets/calendar.svg) junto al botón **[!UICONTROL Crear]** y luego seleccione **[!UICONTROL Configuración]**. Aparece el cuadro de diálogo Configuración.
1. Introduzca el nombre de un usuario en el cuadro de texto **[!UICONTROL Solicitar acceso a los elementos de la Bandeja de entrada del usuario]** y luego seleccione **[!UICONTROL Solicitar]**. Se enviará una solicitud al usuario, y el estado de la misma se mostrará junto al nombre de dicho usuario. Repita el paso para agregar más usuarios.
1. Seleccione **[!UICONTROL Guardar]**. La solicitud se envía a los usuarios como un elemento de la Bandeja de entrada. El usuario puede seleccionar el elemento y seleccionar Aprobar o Rechazar para conceder o rechazar el acceso.


## Reclamar elementos compartidos por otros usuarios {#claim-items}

Solo puede empezar a trabajar en un elemento compartido una vez que lo ha reclamado. Esto evita que varios usuarios puedan trabajar en el mismo elemento. Realice los siguientes pasos para reclamar un elemento:

1. Inicie sesión en la instancia de AEM. Seleccione el icono Bandeja de entrada ![Bandeja de entrada](assets/bell.svg) y luego seleccione **[!UICONTROL Ver todo]**.
1. Seleccione el icono ![Solo contenido](assets/railleft.svg) para abrir el selector de filtros.
1. ©Seleccione la lista desplegable **[!UICONTROL Seleccionar usuario asignado]** para ver y seleccionar los usuarios que han compartido los elementos de su Bandeja de entrada con usted.
1. Seleccione un elemento y seleccione **[!UICONTROL Reclamar]**. El elemento se agregará a la Bandeja de entrada.

## Liberar elementos reclamados {#release-items}

Solo puede trabajar en un elemento compartido una vez que lo ha reclamado. El resto de los usuarios no pueden ver los elementos que ha reclamado ni trabajar en ellos. Si no puede continuar trabajando en un elemento, puede volver a liberarlo en el grupo. Una vez liberado, otros usuarios podrán reclamarlo y trabajar con él:

Realice los siguientes pasos para liberar un elemento:

1. Inicie sesión en la instancia de AEM. Seleccione el icono Bandeja de entrada ![Bandeja de entrada](assets/bell.svg) y luego seleccione **[!UICONTROL Ver todo]**.  Aparecerá una lista de los elementos de la Bandeja de entrada.
1. Seleccione el elemento que desea liberar y seleccione **[!UICONTROL Anular reclamación]**. El elemento volverá a agregarse al grupo. Ahora otros podrán reclamar el elemento.

## Restricciones {#limitations}

* No se admite el uso compartido de elementos con un grupo.
* No se admite el uso compartido de tareas de proyecto.
