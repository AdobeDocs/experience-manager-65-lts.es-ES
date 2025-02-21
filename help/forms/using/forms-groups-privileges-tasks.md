---
title: AEM Forms en grupos y privilegios de OSGi
description: Asignar usuarios a grupos para administrar Adobe Experience Manager (AEM) Forms en OSGi
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 56%

---

# AEM Forms en grupos y privilegios de OSGi{#aem-forms-on-osgi-groups-and-privileges}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html?lang=es) |
| AEM 6.5 | Este artículo |

Puede [crear grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) y asignar directivas y [usuarios](/help/sites-administering/user-group-ac-admin.md#user-administration) a los grupos de Adobe Experience Manager (AEM). Estas políticas controlan los privilegios de los usuarios que forman parte del grupo.

Después de instalar el [paquete de complementos de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), los grupos mencionados en este artículo, como forms-users y forms-power-user, estarán disponibles automáticamente para su asignación. En la tabla siguiente se enumeran las tareas que un usuario puede realizar para AEM Forms en OSGi en función de las asignaciones de grupo:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Tareas</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Crear, previsualizar, publicar y enviar formularios adaptables</li> 
     <li>Crear, previsualizar y publicar comunicaciones interactivas y fragmentos de documentos</li> 
     <li>Cargar recursos en una instancia de AEM</li> 
     <li>Crear temáticas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>Crear, previsualizar, publicar y enviar formularios adaptables</li> 
     <li>Crear, previsualizar y publicar comunicaciones interactivas y fragmentos de documentos</li> 
     <li>Crear scripts para formularios adaptables mediante un editor de código</li> 
     <li>Cargar recursos, incluidos scripts</li> 
     <li>Crear temáticas</li> 
     <li>Importar paquetes que contengan XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Revisar envíos</li> 
     <li>Aprobar o rechazar envíos</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Crear y previsualizar formularios adaptables o plantillas de comunicaciones interactivas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>Crear y modificar un modelo de datos de formulario</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Acceder a cartas de Administración de correspondencia o Interactive Communications mediante la interfaz de usuario del agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>Crear una aplicación de la bandeja de entrada</li> 
     <li>Crear un modelo del flujo de trabajo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>Usar las aplicaciones de la Bandeja de entrada AEM<br /> <strong>Nota: </strong>Debe tener asignaciones de los grupos cm-agent-users y workflow-users para acceder a la interfaz de usuario del agente de comunicaciones interactivas en la Bandeja de entrada AEM.</li> 
     <li>Administrar instancias de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>Configurar PDF Generator</li> 
     <li>Configurar la carpeta inspeccionada</li> 
     <li>Administrar aplicaciones de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. El usuario con privilegios del grupo forms-users no puede escribir scripts para formularios adaptables.
1. El usuario con privilegios del grupo de autores de plantillas no puede escribir scripts para plantillas.
