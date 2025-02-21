---
title: Crear y administrar conjuntos de directivas
description: Los conjuntos de directivas se utilizan para agrupar directivas que tienen un propósito comercial común. Puede crear, editar y eliminar directivas en un conjunto de directivas.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Crear y administrar conjuntos de directivas {#creating-and-managing-policy-sets}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Los conjuntos de directivas se utilizan para agrupar directivas que tienen un propósito comercial común. Los conjuntos de directivas se pueden poner a disposición de un subconjunto de usuarios del sistema.

Cada conjunto de directivas tiene al menos un coordinador asociado. El *coordinador de conjuntos de directivas* es un administrador o un usuario que tiene permisos adicionales. El coordinador del conjunto de políticas suele ser un especialista de la organización que puede crear mejor las políticas en un conjunto de políticas determinado.

Los coordinadores de conjuntos de directivas pueden realizar estas tareas:

* Crear nuevas directivas
* Editar y eliminar cualquier política del conjunto de políticas
* Editar configuración de conjunto de directivas
* Agregar y quitar coordinadores del conjunto de directivas
* Ver los eventos de directivas y documentos de cualquier directiva o documento del conjunto de directivas
* Revocar acceso a documentos
* Cambiar directivas para el documento

Los superusuarios y coordinadores de conjuntos de directivas que tienen permiso para ello crean y eliminan conjuntos de directivas en la interfaz de administrador de Document Security.

Al eliminar un conjunto de directivas, las directivas que formaban parte del conjunto no se pueden aplicar a nuevos documentos. Sin embargo, puede ver la información de la directiva en las páginas web de la consola de administración y del usuario final para las directivas que aún se están utilizando. Puede ver la información de la política desde la página de detalles del documento para cualquier documento protegido por la política. Las directivas que aún se utilizan se pueden editar.

El superusuario o coordinador de conjuntos de directivas agrega los dominios creados en Administración de usuarios al usuario y grupo visibles para cada conjunto de directivas. Esta lista es visible para el coordinador de conjuntos de directivas y se utiliza para establecer límites en los dominios que el coordinador de conjuntos de directivas puede examinar al elegir usuarios para agregarlos a las directivas.

Al crear conjuntos de directivas, se asigna a los usuarios la función de editor de documentos. *editor de documentos* es el usuario que protege el documento con una directiva. De forma predeterminada, este usuario siempre se incluye en una directiva con derechos de acceso completos, incluidas las capacidades de revocación y cambio de directiva. Sin embargo, los administradores pueden cambiar los derechos de acceso del editor del documento para las directivas compartidas. Por ejemplo, el administrador puede deshabilitar el derecho del editor del documento a revocar el acceso al documento o cambiar la directiva. Si un administrador cambia la directiva adjunta al documento, el nombre del publicador se actualizará al nombre del propietario de la última directiva aplicada al documento.

Tras la instalación de Document Security, se crea un conjunto de directivas predeterminado denominado *Conjunto de directivas globales*. Este conjunto de directivas lo administra el administrador que instaló el software o el coordinador de conjuntos de directivas designado para este conjunto de directivas.

## Crear un conjunto de políticas {#create-a-policy-set}

El Conjunto de directivas globales es el único conjunto de directivas predeterminado que se crea durante la instalación. Puede crear conjuntos de directivas adicionales y agregar directivas, usuarios, coordinadores de conjuntos de directivas y editores de documentos. Después de crear un conjunto de directivas, puede crear directivas dentro del conjunto.

Durante la creación del conjunto de directivas, puede utilizar el botón Atrás para volver a la pantalla anterior y el botón Guardar para guardar el conjunto de directivas en cualquier momento.

1. En la página Seguridad de documentos, haga clic en Directivas, en la ficha Conjuntos de directivas y, a continuación, en Nuevo.
1. En el cuadro Nombre, escriba un nombre para el conjunto de directivas, opcionalmente escriba una Descripción y haga clic en Siguiente. El nombre no puede contener dos puntos **:**.

   >[!NOTE]
   >
   >Puede crear un nombre de conjunto de directivas que contenga caracteres extendidos; sin embargo, cuando se realiza una comparación entre dos cadenas, los caracteres acentuados y no acentuados como &quot;e&quot; y &quot;é&quot; se consideran iguales. Cuando alguien crea un conjunto de directivas, se realiza una comparación para comprobar si ya existe uno con el mismo nombre. La comparación no puede distinguir entre nombres que son iguales excepto para caracteres acentuados. Se da por hecho que el conjunto de directivas ya se ha agregado a la base de datos y el nuevo no se ha agregado.

1. (Opcional) Para establecer los dominios visibles para los editores de documentos cuando agregan usuarios a una directiva, haga clic en Agregar dominios, seleccione los dominios en los que puede realizar búsquedas, haga clic en Agregar y, a continuación, haga clic en Aceptar.
1. En la página Agregar usuarios y grupos visibles, haga clic en Siguiente.
1. (Opcional) Para agregar un coordinador de conjuntos de directivas, haga clic en Agregar usuarios y grupos en la página Agregar coordinadores de conjuntos de directivas (paso 3 de 4) y realice las siguientes tareas:

   * En el cuadro Buscar, escriba el nombre o la dirección de correo electrónico.
   * En la lista Utilizando, seleccione la opción adecuada.
   * En la lista Tipo, seleccione Usuario y, en la lista En, seleccione un dominio para buscar.
   * En la lista Mostrar, seleccione el número de resultados que desea mostrar por página y, a continuación, haga clic en Buscar.
   * Seleccione la casilla de verificación del usuario o grupo que desee agregar y haga clic en Siguiente.
   * Seleccione los permisos de coordinador del conjunto de directivas y haga clic en Agregar. Se pueden configurar los siguientes permisos:

      * Ver eventos
      * Administrar documentos (revocar y restablecer el acceso a los documentos y cambiar las directivas de los documentos)
      * Administrar directivas (crear, editar y eliminar directivas)
      * Administrar editores de documentos (agregar y quitar editores de documentos)
      * Delegar (agregar y quitar coordinadores de conjuntos de directivas)

1. Repita el paso 5 para agregar más coordinadores de conjuntos de directivas.
1. Revise la configuración del coordinador de conjuntos de directivas y haga clic en Siguiente.
1. Haga clic en Agregar usuarios y grupos para agregar editores de documentos que puedan utilizar las directivas del conjunto de directivas para proteger documentos.
1. En la página Agregar editores de documentos, realice estas tareas:

   * En el cuadro Buscar, escriba el nombre o la dirección de correo electrónico.
   * En la lista Utilizando, seleccione la opción adecuada.
   * En la lista Tipo, seleccione Usuario y, en la lista En, seleccione un dominio para buscar.
   * En la lista Mostrar, seleccione el número de resultados que desea mostrar por página y, a continuación, haga clic en Buscar.
   * Active las casillas de verificación de los usuarios y grupos que desee agregar, haga clic en Agregar y, a continuación, haga clic en Aceptar.

1. Haga clic en Guardar.

Ahora puede agregar directivas al conjunto de directivas. (Consulte [Creación y edición de directivas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).)

## Editar un conjunto de políticas {#edit-a-policy-set}

1. En la página Seguridad de documentos, haga clic en Directivas, haga clic en la ficha Conjuntos de directivas y, a continuación, haga clic en el conjunto de directivas que desea editar.
1. Haga clic en la pestaña adecuada y edite según sea necesario:

   * **Detalle:** Edite el nombre y la descripción del conjunto de directivas.
   * **Directivas:** Cree, habilite, edite y elimine directivas dentro del conjunto de directivas.
   * **Usuarios y grupos visibles:** Agregue y quite usuarios y grupos visibles que se puedan incluir en una directiva.
   * **Coordinadores de conjuntos de directivas:** Agregue, quite y cambie permisos para los coordinadores.
   * **Publicadores de documentos:** Agregue y quite usuarios que puedan publicar documentos mediante las directivas del conjunto.

1. Para eliminar un usuario o grupo visible, Coordinador de conjuntos de directivas o Editor de documentos, haga clic en la ficha correspondiente, active la casilla de verificación de la entrada, haga clic en Eliminar y, a continuación, haga clic en Aceptar.
1. Para agregar usuarios o grupos visibles, un Coordinador de conjuntos de directivas o Publicadores de documentos, haga clic en la ficha correspondiente, en Agregar usuarios o grupos, busque el usuario o grupo que desee agregar, seleccione la entrada, haga clic en Agregar y, a continuación, haga clic en Aceptar.
1. En la ficha Directivas, busque directivas para agregarlas al conjunto de directivas y cree nuevas directivas:

   * Para buscar una directiva, seleccione ID de directiva o Nombre de directiva, escriba el valor correspondiente, seleccione el número de elementos que desea mostrar y haga clic en Buscar.
   * Para obtener detalles acerca de cómo crear una directiva, vea [Crear y editar directivas](/help/forms/using/admin-help/creating-policies.md#creating-and-editing-policies).

## Eliminar un conjunto de políticas {#delete-a-policy-set}

Al eliminar un conjunto de directivas, las directivas que formaban parte del conjunto no se pueden aplicar a nuevos documentos. Sin embargo, puede ver la información de la directiva en la consola de administración y en las páginas web del usuario final para directivas que aún se están utilizando. Puede ver la información de la política desde la página de detalles del documento para cualquier documento protegido por la política. Las directivas que aún se utilizan se pueden editar.

1. Haga clic en Directivas y en la ficha Conjuntos de directivas.
1. Active la casilla de verificación del conjunto de directivas que desea eliminar.
1. Haga clic en Eliminar y, a continuación, en Aceptar.
