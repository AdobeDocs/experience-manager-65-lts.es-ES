---
title: Administración de correspondencia | Administrar datos de usuario
description: Obtenga información sobre Administración de correspondencia y la administración de datos de usuario en un entorno de Adobe Experience Manager Forms.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Form Data Model
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 94%

---

# Administración de correspondencia | Administrar datos de usuario {#correspondence-management-handling-user-data}

Administración de correspondencia de AEM Forms le permite crear, administrar y optimizar las correspondencias seguras y personalizadas de clientes. Proporciona una interfaz de usuario intuitiva para que los usuarios de la empresa creen correspondencias mediante bloques de contenido y elementos multimedia aprobados previamente. Para obtener más información sobre la creación de correspondencias, consulte [Crear correspondencia](/help/forms/using/create-correspondence.md).

Cuando un usuario de la empresa o un agente guarda una correspondencia como borrador o la envía, se guarda una instancia de carta en el repositorio de AEM. La instancia de carta incluye datos de correspondencia y metadatos.

>[!NOTE]
>
>En AEM 6.5 Forms, Administración de correspondencia no está disponible de forma predeterminada. Si actualiza desde una versión anterior de AEM Forms, instale el paquete de compatibilidad y migre los recursos de Administración de correspondencia para poder usarlos en AEM 6.5 Forms. Para obtener más información, consulte [Paquete de compatibilidad](/help/forms/using/compatibility-package.md).

## Almacenamiento de datos y datos de usuarios {#data}

Administración de correspondencia almacena datos para cartas en borrador y enviados en el repositorio de AEM solo si la instancia de publicación está configurada para administrar instancias de carta. Para obtener más información sobre la configuración, consulte [Propiedades de configuración de Administración de correspondencia](/help/forms/using/cm-configuration-properties.md).

Según la persistencia del repositorio de datos configurada para la implementación de AEM, los borradores y los datos de correspondencia enviados se almacenan en las siguientes ubicaciones.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo de persistencia</strong></p> </td>
   <td><p><strong>Almacén de datos</strong></p> </td>
   <td><p><strong>Ubicación</strong></p> </td>
  </tr>
  <tr>
   <td><p>Predeterminado</p> </td>
   <td><p>El repositorio de AEM de instancias de publicación y de autor especificado en la configuración de replicación inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code><br /> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>El repositorio de AEM de la instancia de autor del procesamiento remoto</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

En la ubicación del repositorio de AEM especificada arriba:

* `[yyyy]/[mm]/[dd]` es la estructura del nodo basada en la fecha en la que se creó la instancia de carta
* `[node-id]` es el ID asignado a la carpeta que contiene la carta
* `[letter-instance-name]` es el nombre especificado al guardar o enviar una carta

En el nodo [letter-instance-name], se crea la siguiente estructura de nodos y los datos de cada instancia de carta se almacenan en el repositorio de AEM:

| Nodo | Descripción |
|---|---|
| `extendedProperties` | Almacena las propiedades de metadatos de la instancia de carta. |
| `dataXML` | Almacena un archivo dataXML descargable que contiene los datos de correspondencia en formato binario. |
| `processedXDP` | Incluye los detalles de la plantilla XDP utilizada para crear la carta enviada. Este nodo solo se crea para las correspondencias enviadas. |
| `submittedLetter` | Almacena los datos de la carta enviada en formato binario descargable. Este nodo solo se crea para las correspondencias enviadas. |

## Acceder y eliminar datos de usuario {#access-and-delete-user-data}

Puede acceder a los datos de correspondencia en Borradores y enviados en los repositorios de datos configurados y, si es necesario, eliminarlos.

### Acceder a los datos de usuario {#access-user-data}

Administración de correspondencia proporciona una API que puede utilizar para buscar y acceder a instancias de carta en Borradores y enviados. Con las API, puede encontrar y abrir instancias de carta mediante el ID de instancia de la carta o el usuario que guardó o envió la correspondencia. Para obtener más información, consulte [API para acceder a instancias de carta](/help/forms/using/cm-apis-to-access-letter-instances.md).

También puede navegar a la instancia de carta en el repositorio de AEM mediante CRXDE Lite. Consulte [Almacenamiento de datos y datos de usuarios](/help/forms/using/correspondence-management-handling-user-data.md#data) para obtener información sobre los datos almacenados y la ubicación del repositorio.

### Eliminar los datos de usuario {#delete-user-data}

Para buscar una instancia de carta que contenga los datos de un usuario específico, puede:

* Utilizar las API de Administración de correspondencia si conoce el nombre de la instancia de carta o el usuario que guardó el borrador o envió la correspondencia
* Utilizar la búsqueda del repositorio de AEM con información personal, como el ID de correo electrónico o el nombre, para encontrar el nodo en el que se almacena la información

Para eliminar por completo los datos de usuario de las correspondencias en Borradores y enviados desde sistemas de AEM, debe eliminar manualmente el nodo de instancia de carta de todas las instancias de AEM aplicables.
