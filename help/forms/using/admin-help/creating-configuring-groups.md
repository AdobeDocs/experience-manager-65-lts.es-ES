---
title: Crear y configurar grupos
description: Obtenga información sobre cómo crear grupos de forma manual o dinámica, editar un grupo, ver detalles sobre un grupo o eliminarlo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
hidefromtoc: true
exl-id: e8824453-8891-40e0-9948-c0c0f0fdce62
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1585'
ht-degree: 1%

---

# Crear y configurar grupos{#creating-and-configuring-groups}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

La creación de grupos de usuarios permite asignar funciones al grupo en lugar de a usuarios individuales.

Hay dos tipos diferentes de grupos disponibles. Puede crear manualmente un grupo y agregarle usuarios y otros grupos. También puede crear grupos dinámicos que incluyan automáticamente a todos los usuarios que cumplan un conjunto especificado de reglas.

Los usuarios pueden experimentar un tiempo de respuesta más lento si pertenecen a muchos grupos (por ejemplo, 500 o más) o si los grupos están profundamente anidados (por ejemplo, 30 niveles). Si tiene este problema, puede configurar los formularios de AEM para que recuperen previamente información de ciertos dominios. (Consulte [Configuración de formularios de AEM para recuperar previamente información de dominio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information)).

## Crear un grupo manualmente {#create-a-group-manually}

Cuando crea manualmente un grupo, puede agregarle usuarios y otros grupos y asignarle funciones. También puede asociar el grupo con un grupo principal.

Si utiliza Content Services (obsoleto), puede seleccionar la opción Seleccionar esta opción para insertar usuarios y grupos en proveedores de almacenamiento de principales externos registrados en la página Administración de dominios para insertar la información de cualquier nuevo usuario o grupo que cree en Content Services (obsoleto).

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos y, a continuación, haga clic en Nuevo grupo.
1. Complete la sección Configuración general y haga clic en Siguiente. El nombre canónico y el nombre de grupo son atributos obligatorios.

   El nombre canónico es un identificador único para el grupo. Cada grupo y usuario de un dominio debe tener un nombre canónico único. Seleccione la casilla de verificación Generado por el sistema para permitir que la Administración de usuarios asigne un valor único o desmarque la casilla de verificación y especifique un valor personalizado para el Nombre canónico.

   Evite utilizar caracteres de subrayado (_) en nombres canónicos, por ejemplo, `sample_group`. Al buscar grupos en función de su nombre canónico, no se devuelven los que contienen caracteres de guion bajo.

1. Para agregar usuarios y grupos a este nuevo grupo, haga clic en Buscar usuarios/grupos y realice las siguientes tareas:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * En la lista En, seleccione Usuarios, Grupos o Usuarios y grupos.
   * En la lista Utilizando, seleccione Nombre, Correo electrónico o ID de usuario.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de búsqueda, active las casillas de verificación de los usuarios y grupos que desee agregar a este nuevo grupo y haga clic en Aceptar.

1. Haga clic en Siguiente.
1. Para agregar este nuevo grupo a otros grupos existentes, haga clic en Buscar grupos y realice las siguientes tareas:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de la búsqueda, active las casillas de verificación de los grupos a los que pertenece el nuevo grupo y haga clic en Aceptar.

1. Haga clic en Siguiente.
1. Para asignar funciones al grupo, haga clic en Buscar funciones, active las casillas de verificación de cada función que desee asignar al grupo y haga clic en Aceptar. Los usuarios del grupo heredan las funciones asignadas en el nivel de grupo.
1. Haga clic en Finish.

## Creación de un grupo dinámico {#create-a-dynamic-group}

En un grupo dinámico, no selecciona individualmente los usuarios que pertenecen al grupo. En su lugar, debe especificar un conjunto de reglas y todos los usuarios que cumplan dichas reglas se añadirán automáticamente al grupo dinámico.

Utilice una de estas dos formas de crear grupos dinámicos:

* Habilite la creación automática de grupos dinámicos basados en dominios de correo electrónico, como @adobe.com. Al habilitar esta función, Administración de usuarios crea un grupo dinámico para cada dominio de correo electrónico único en la base de datos de formularios de AEM. Utilice una expresión CRON para especificar la frecuencia con la que Administración de usuarios busca nuevos dominios de correo electrónico en la base de datos de formularios AEM Forms. Estos grupos dinámicos se agregan al dominio local DefaultDom y se denominan &quot;Todos los usuarios con un ID de correo *`[email domain]`*&quot;.
* Cree un grupo dinámico en función de criterios especificados, incluidos el dominio de correo electrónico, la descripción, el nombre canónico y el nombre de dominio del usuario. Para pertenecer al grupo dinámico, un usuario debe cumplir todos los criterios especificados. Para configurar una condición &quot;o&quot;, cree dos grupos dinámicos independientes y agréguelos a un grupo local. Por ejemplo, utilice ese método para crear un grupo de usuarios que pertenezcan al dominio de correo electrónico @adobe.com o cuyo nombre canónico contenga ou=adobe.com. Sin embargo, los usuarios no necesariamente tienen que cumplir ambas condiciones.

Un grupo dinámico contiene sólo usuarios. No puede contener otros grupos. Sin embargo, un grupo dinámico puede pertenecer a un grupo principal.

### Crear automáticamente grupos dinámicos basados en dominios de correo electrónico {#automatically-create-dynamic-groups-based-on-email-domains}

1. Haga clic en Configuración > Administración de usuarios > Configuración > Configurar atributos avanzados del sistema.
1. En Creación automática de grupo dinámico, active la casilla de verificación.
1. Especifique cuándo el administrador de usuarios comprueba los nuevos dominios de correo electrónico. Este tiempo debe ser posterior al tiempo de sincronización del dominio porque la creación de grupos dinámicos es lógica sólo si se ha completado la sincronización del dominio.

   * Para habilitar la sincronización automática diariamente, escriba la hora en formato de 24 horas en el cuadro Se produce a diario a las. Al guardar la configuración, este valor se convierte en una expresión cron, que se muestra en el cuadro siguiente.
   * Para programar la sincronización en un día concreto de la semana o del mes, o en un mes concreto, seleccione la expresión cron adecuada en el cuadro. El valor predeterminado es `0 00 4 ? * *` (lo que significa comprobar a las 4 a. m. todos los días).

     El uso de expresiones cron se basa en el sistema de programación de trabajos de código abierto Quartz, versión 1.4.0.

1. Haga clic en Guardar.

### Crear un grupo dinámico basado en criterios especificados {#create-a-dynamic-group-based-on-specified-criteria}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Haga clic en Nuevo grupo dinámico.
1. Complete la sección Configuración general. El nombre de grupo es un atributo obligatorio. Puede asignar el grupo a cualquier dominio configurado.
1. En Criterios de grupo dinámico, especifique uno o varios atributos utilizados para rellenar el grupo dinámico.

   >[!NOTE]
   >
   >Los atributos Correo electrónico, Descripción y Nombre canónico distinguen entre mayúsculas y minúsculas al utilizar el operador Igual. No distinguen entre mayúsculas y minúsculas con los operadores Comienza con, Finaliza con o Contiene.

   **Correo electrónico:** Dominio de correo electrónico del usuario, como `@adobe.com`.

   **Descripción:** Descripción del usuario, como &quot;Científico informático&quot;

   **Nombre canónico:** Nombre canónico del usuario, como `ou=adobe.com`

   **Nombre de dominio:** El nombre del dominio al que pertenece el usuario, como `DefaultDom`. El atributo Domain Name distingue entre mayúsculas y minúsculas al utilizar el operador Contains. No distingue entre mayúsculas y minúsculas con los operadores Comienza con, Finaliza con o Es igual a.

1. Haga clic en Probar. Una página Prueba muestra los 200 primeros usuarios que cumplen los criterios definidos. Haga clic en Cerrar.
1. Si la prueba arrojó los resultados esperados, haga clic en Siguiente. De lo contrario, edite los criterios del grupo dinámico y vuelva a realizar la prueba.
1. Para agregar el grupo dinámico a un grupo principal, haga clic en Buscar grupos y realice las siguientes tareas:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de la búsqueda, active las casillas de verificación de los grupos a los que pertenece el grupo dinámico y haga clic en Aceptar.

1. Haga clic en Siguiente.
1. Para asignar funciones al grupo dinámico, haga clic en Buscar funciones, active las casillas de verificación de cada función que desee asignar al grupo y, a continuación, haga clic en Aceptar. Los usuarios del grupo heredan las funciones asignadas en el nivel de grupo.
1. Haga clic en Finish.

## Ver detalles de un grupo {#view-details-about-a-group}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. En la lista En, seleccione Grupo y, a continuación, haga clic en Buscar. Los resultados de la búsqueda se muestran en la parte inferior de la página. Puede ordenar la lista haciendo clic en cualquiera de los encabezados de columna.
1. Haga clic en el nombre del grupo sobre el que desea mostrar detalles. Aparecerá la página Detalles del Grupo.
1. Para ver los miembros directos del grupo, haga clic en Identidades secundarias.

## Editar un grupo {#edit-a-group}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. Para buscar el grupo que desea editar, realice estas tareas:

   * En el cuadro Buscar, escriba los criterios de búsqueda.
   * En la lista Utilizando, seleccione Nombre o Correo electrónico.
   * En la lista En, seleccione Grupos.
   * Seleccione el dominio, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * En los resultados de búsqueda, haga clic en el nombre del grupo que desea editar.

1. En la pestaña Detalles, edite la configuración general y haga clic en Guardar.
1. Para editar los grupos asociados, haga clic en la pestaña Grupos principales y realice las siguientes tareas:

   * Para buscar grupos que agregar a la asociación, haga clic en Buscar grupos y complete la información de búsqueda.
   * Para agregar grupos, active la casilla de verificación de los grupos que desea agregar, haga clic en Aceptar y, a continuación, haga clic en Guardar.
   * Para eliminar un grupo asociado, active la casilla de verificación del grupo que desea eliminar, haga clic en Eliminar, en Aceptar y, a continuación, en Guardar.

1. Para editar los usuarios y grupos del grupo, haga clic en la pestaña Identidades secundarias y realice las siguientes tareas:

   * Para buscar usuarios y grupos que agregar, haga clic en Buscar usuarios/grupos y complete la información de búsqueda.
   * Para agregar un usuario o grupo, active la casilla correspondiente, haga clic en Aceptar y, a continuación, en Guardar.
   * Para eliminar un usuario o grupo, active la casilla de verificación del usuario o grupo, haga clic en Eliminar, en Aceptar y, a continuación, en Guardar.

1. Para editar asignaciones de roles, haga clic en la ficha Asignaciones de roles y realice las siguientes tareas:

   * Para buscar roles que asignar al grupo, haga clic en Buscar roles.
   * Para agregar un rol, active la casilla correspondiente, haga clic en Aceptar y, a continuación, en Guardar.
   * Para anular la asignación de un rol, active la casilla correspondiente, haga clic en Anular asignación y, a continuación, en Guardar.

## Eliminar un grupo {#delete-a-group}

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Usuarios y grupos.
1. En la lista Buscar, seleccione Grupos y, a continuación, haga clic en Buscar.
1. Active la casilla de verificación del grupo que desea eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.
