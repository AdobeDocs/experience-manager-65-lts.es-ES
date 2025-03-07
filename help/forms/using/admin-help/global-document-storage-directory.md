---
title: Directorio global de almacenamiento de documentos
description: El directorio de almacenamiento global de documentos (GDS) es un directorio que se utiliza para almacenar archivos de larga duración que se utilizan en un proceso.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 9a93b8f9-33cb-4aec-81e0-a1146bba955a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 3%

---

# Directorio global de almacenamiento de documentos{#global-document-storage-directory}

El directorio *Global Document Storage (GDS)* es un directorio usado para almacenar archivos de larga duración que se usan en un proceso. Estos archivos incluyen PDF, directivas y plantillas de formulario. Los archivos de larga duración son una parte esencial del estado general de muchas implementaciones de formularios AEM Forms. Si se pierden o dañan algunos o todos los documentos de larga duración, el servidor de Forms puede volverse inestable. Los documentos de entrada para invocaciones de trabajo asincrónicas también se almacenan en el directorio GDS y deben estar disponibles para procesar solicitudes. Es importante tener en cuenta la fiabilidad del sistema de archivos que aloja el directorio GDS. Utilice una cabina redundante de discos independientes (RAID) u otra tecnología adecuada para sus necesidades de calidad y nivel de servicio.

Los archivos de larga duración pueden contener información confidencial del usuario. Esta información puede requerir credenciales especiales cuando se accede a ella mediante las API de formularios AEM Forms o las interfaces de usuario. Es importante que el directorio GDS esté protegido correctamente a través del sistema operativo. Solo la cuenta de administrador utilizada para ejecutar el servidor de aplicaciones debe tener acceso de lectura y escritura al directorio GDS.

Además de seleccionar un directorio seguro y de alta disponibilidad para GDS, también puede optar por habilitar el almacenamiento de documentos en la base de datos. Tenga en cuenta que incluso con el uso de la base de datos de formularios de AEM para el almacenamiento de documentos, los formularios de AEM siguen necesitando el directorio GDS. (Vea [Opciones de copia de seguridad cuando se usa la base de datos para el almacenamiento de documentos](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)).

Los datos de la aplicación de formularios de AEM residen en el directorio GDS y en la base de datos de formularios de AEM. En la tabla siguiente se describen los datos y sus ubicaciones.

<table>
 <thead>
  <tr>
   <th><p>Datos de formularios AEM</p></th>
   <th><p>Base de datos</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Datos de aplicación (usuarios, funciones, procesos, directivas, extremos, eventos, etc.)</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Contenedores de servicio implementados</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Administrador de documentos </p></td>
   <td><p>No</p></td>
   <td><p>Sí</p></td>
  </tr>
  <tr>
   <td><p>Repositorio de Forms</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Configuración del sistema</p></td>
   <td><p>Sí</p></td>
   <td><p>No</p></td>
  </tr>
  <tr>
   <td><p>Carpetas inspeccionadas</p></td>
   <td><p>No</p></td>
   <td><p>Sí</p></td>
  </tr>
 </tbody>
</table>

## Configuración del directorio GDS {#configuring-the-gds-directory}

La ubicación del directorio GDS se puede configurar manualmente durante el proceso de instalación de los formularios AEM Forms. Si la configuración de ubicación permanece vacía durante la instalación, la ubicación predeterminada es un directorio en la instalación del servidor de aplicaciones de la siguiente manera:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Cambiar la ubicación predeterminada de GDS {#change-the-default-gds-location}

Puede cambiar la ubicación de GDS en la consola de administración una vez completada la instalación de los formularios AEM Forms. Reubicar manualmente los datos para completar el proceso.

>[!NOTE]
>
>* Migre los datos de la siguiente manera o se perderán datos.
>* Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. Inicie sesión en la consola de administración y haga clic en Configuración > Configuración del sistema principal > Configuraciones.
1. En el cuadro Directorio global de almacenamiento de documentos, escriba la ruta de acceso completa al nuevo directorio GDS y, a continuación, haga clic en Aceptar.
1. Cierre inmediatamente el servidor de aplicaciones.
1. Mueva todos los archivos del directorio GDS antiguo a la nueva ubicación, conservando la estructura de directorios interna.
1. Reinicie el servidor de aplicaciones.

## Acerca de los archivos de implementación {#about-deployment-files}

Los formularios de AEM constan de dos tipos de archivos de implementación, los contenedores de servicio y los archivos EAR de Java 2 Platform, Enterprise Edition (J2EE). Los archivos EAR constan de paquetes de aplicaciones J2EE estándar que contienen la funcionalidad principal de los formularios AEM Forms. Los archivos EAR específicos del servidor de aplicaciones son los siguientes:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

La implementación de formularios AEM implica implementar los archivos EAR ensamblados y los archivos auxiliares en el servidor de aplicaciones donde planea ejecutar la solución de formularios AEM. Si ha configurado y ensamblado varios módulos, los módulos implementables se empaquetan dentro de los archivos EAR implementables. Para implementar estos archivos, cópielos en el directorio *[appserver home]*\server\all\deploy.

Los módulos y los archivos de archivo de formularios AEM se empaquetan en archivos JAR. Como no son archivos de tipo J2EE, no se implementan en el servidor de aplicaciones. En su lugar, se copian en el directorio GDS y se almacena una referencia a su ubicación en la base de datos de formularios AEM Forms. Por este motivo, el directorio GDS debe compartirse entre todos los nodos del clúster. Todos los nodos deben tener acceso al directorio de almacenamiento central de los DSC.

>[!NOTE]
>
>Antes de implementar los contenedores de servicio, asegúrese de crear y configurar el directorio GDS. (Consulte [Configuración del directorio GDS](global-document-storage-directory.md#configuring-the-gds-directory))
