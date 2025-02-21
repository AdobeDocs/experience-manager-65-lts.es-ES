---
title: Protección y seguridad de AEM Forms en el entorno OSGi
description: Conozca las recomendaciones y las prácticas recomendadas para proteger AEM Forms en el servidor OSGi.
topic-tags: Security
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 98%

---

# Protección y seguridad de AEM Forms en el entorno OSGi {#hardening-and-securing-aem-forms-on-osgi-environment}

Conozca las recomendaciones y las prácticas recomendadas para proteger AEM Forms en el servidor OSGi.

La seguridad de un entorno de servidor es fundamental para una organización. Este artículo contiene recomendaciones y prácticas recomendadas para proteger los servidores que ejecutan AEM Forms. El objetivo de este documento no es proporcionar una guía completa sobre cómo proteger el host del sistema operativo. En su lugar, este artículo describe una serie de configuraciones para proteger la seguridad que debe implementar para mejorar la seguridad de la aplicación implementada. Sin embargo, para garantizar que los servidores de aplicaciones siguen siendo seguros, también debe implementar procedimientos de monitorización, detección y respuesta de seguridad, así como las recomendaciones incluidas en este artículo. El documento contiene asimismo prácticas recomendadas y directrices para proteger la información de identificación personal (PII).

El artículo está dirigido a consultores, especialistas en seguridad, arquitectos de sistemas y profesionales de TI responsables de planificar la aplicación o el desarrollo de la infraestructura y la implementación de AEM Forms. Entre estas funciones se incluyen las siguientes funciones comunes:

* Los ingenieros de TI y de operaciones encargados de implementar aplicaciones y servidores web seguros en su propia organización o en las organizaciones de sus clientes.
* Los arquitectos y los planeadores responsables de planificar el esfuerzo arquitectónico de las organizaciones de sus clientes.
* Los especialistas en seguridad de TI que se encargan de proporcionar la seguridad de todas las plataformas de su organización.
* Los consultores de Adobe y partners que necesitan recursos detallados para sus clientes y sus asociados.

La siguiente imagen muestra los componentes y los protocolos utilizados en una implementación típica de AEM Forms, incluida la topología indicada para el cortafuegos:

![arquitectura-típica](assets/typical-architecture.png)

AEM Forms ofrece un alto grado de personalización y es compatible con un gran número de entornos diferentes. Es posible que algunas de las recomendaciones no sean aplicables a su organización.

## Capa de transporte segura {#secure-transport-layer}

Las vulnerabilidades de seguridad de la capa de transporte están entre las principales amenazas a las que está expuesto un servidor de aplicaciones orientado a Internet o a la intranet. Esta sección describe el proceso de protección de los hosts de la red frente a este tipo de vulnerabilidades. Aborda la segmentación de red, la protección de pila del Protocolo de control de transmisión/Protocolo Internet (TCP/IP) y el uso de cortafuegos para la protección del host.

### Límite de extremos abiertos  {#limit-open-endpoints}

Una organización puede tener un cortafuegos externo para restringir el acceso entre un usuario final y la granja de servidores de publicación de AEM Forms. La organización también puede disponer de un cortafuegos interno para limitar el acceso entre una granja de servidores de publicación y los servidores de el resto de elementos de la organización (por ejemplo, la instancia de autor, la instancia de procesamiento y las bases de datos). Permita que los cortafuegos permitan el acceso a un número limitado de URL de AEM Forms para usuarios finales y dentro de los elementos de la organización:

#### Configuración de un cortafuegos externo  {#configure-external-firewall}

Puede configurar un cortafuegos externo para permitir que determinadas URL de AEM Forms accedan a Internet. Se requiere acceso a estas URL para rellenar o enviar un formulario adaptable, HTML5 o una carta de Administración de correspondencia, o para iniciar sesión en un servidor de AEM Forms:

<table> 
 <tbody>
  <tr>
   <td>Componente</td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Formularios adaptables</td> 
   <td>
    <ul> 
     <li>/content/dam/formsanddocuments/AF_PATH/jcr:content</li> 
     <li>/etc/clientlibs/fd/</li> 
     <li>/content/forms/af/AF_PATH</li> 
     <li>/libs/granite/csrf/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Formularios HTML5</td> 
   <td>
    <ul> 
     <li>/content/forms/formsets/profiles/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Administración de correspondencia </td> 
   <td>
    <ul> 
     <li>/aem/forms/createcorrespondence* </li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>Portal de Forms </td> 
   <td>
    <ul> 
     <li>/content/forms/portal/</li> 
     <li>/libs/cq/ui/widgets*</li> 
     <li>/libs/cq/security/</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td> Aplicación de AEM Forms</td> 
   <td>
    <ul> 
     <li>/j_security_check*</li> 
     <li>/soap/services/AuthenticationManagerService</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

#### Configuración del cortafuegos interno  {#configure-internal-firewall}

Puede configurar el cortafuegos interno para permitir que ciertos componentes de AEM Forms (por ejemplo, la instancia de autor, la instancia de procesamiento o las bases de datos) se comuniquen con la granja de servidores de publicación y con otros componentes internos mencionados en el diagrama de topología:

<table> 
 <tbody>
  <tr>
   <td>Host<br /> </td> 
   <td>URI</td> 
  </tr>
  <tr>
   <td>Publicar granja (nodos de publicación)</td> 
   <td>/bin/receive</td> 
  </tr>
  <tr>
   <td>Servidor de procesamiento</td> 
   <td>/content/forms/fp/*</td> 
  </tr>
  <tr>
   <td>Servidor de complementos de Forms Workflow (servidor de AEM Forms en JEE)</td> 
   <td>/soap/sdk</td> 
  </tr>
 </tbody>
</table>

#### Configuración de permisos del repositorio y listas de control de acceso (ACL) {#setup-repository-permissions-and-access-control-lists-acls}

De forma predeterminada, los recursos disponibles en los nodos de publicación son accesibles para todos. El acceso de solo lectura está habilitado para todos los recursos. Es necesario para habilitar el acceso anónimo. Si planea restringir la vista de Forms y enviar el acceso solo a usuarios autenticados, utilice un grupo común para permitir que solo los usuarios autenticados tengan acceso de solo lectura a los recursos disponibles en los nodos de publicación. Las siguientes ubicaciones/directorios contienen recursos de Forms que requieren protección (acceso de solo lectura para usuarios autenticados):

* /content/&amp;ast;
* /etc.clientlibs/fd/&amp;ast;
* /libs/fd/&amp;ast;

## Administrar de forma segura los datos de Forms  {#securely-handle-forms-data}

AEM Forms almacena datos en ubicaciones predefinidas y carpetas temporales. Debe proteger los datos para evitar su uso no autorizado.

### Configuración de la limpieza periódica de la carpeta temporal {#setup-periodic-cleanup-of-temporary-folder}

Cuando se configuran formularios para archivos adjuntos y se verifican o se previsualizan componentes, los datos correspondientes se almacenan en los nodos de publicación en /tmp/fd/. Los datos se depuran periódicamente. Puede modificar el trabajo de depuración de datos predeterminado para que sea más agresivo. Para modificar el trabajo programado para depurar datos, abra la consola web de AEM, luego abra Tarea de limpieza del almacenamiento temporal de AEM Forms y modifique la expresión Cron.

En las situaciones mencionadas anteriormente, los datos solo se guardan para los usuarios autenticados. Además, los datos están protegidos mediante listas de control de acceso (ACL). Por lo tanto, modificar la depuración de datos es un paso adicional para proteger la información.

### Proteger los datos guardados mediante la acción de envío del portal de formularios {#secure-data-saved-by-forms-portal-submit-action}

De forma predeterminada, la acción de envío de los formularios adaptables del portal de formularios guarda los datos en el repositorio local del nodo de publicación. Los datos se guardan en /content/forms/fp. **No se recomienda almacenar los datos en instancias de publicación.**

Puede configurar el servicio de almacenamiento para que transmita datos al clúster de procesamiento sin guardar nada de forma local en el nodo de publicación. El clúster de procesamiento reside en una zona segura detrás del cortafuegos privado, y los datos siguen siendo seguros.

Utilice las credenciales del servidor de procesamiento para el servicio de configuración de AEM DS para publicar datos del nodo de publicación en el servidor de procesamiento. Utilice las credenciales de un usuario no administrativo restringido con acceso de lectura y escritura al repositorio del servidor de procesamiento. Para obtener más información, consulte [Configuración de servicios de almacenamiento para borradores y envíos](/help/forms/using/configuring-draft-submission-storage.md).

### Proteger datos administrados por el modelo de datos de formulario (FDM) {#secure-data-handled-by-form-data-model-fdm}

Utilice cuentas de usuario con los privilegios mínimos requeridos para configurar las fuentes de datos del modelo de datos de formulario (FDM). El uso de cuentas administrativas puede proporcionar acceso abierto a entidades de esquema y metadatos a usuarios no autorizados.\
La integración de datos también proporciona métodos para autorizar solicitudes de servicio de FDM. Puede insertar mecanismos de autorización antes y después de la ejecución para validar una solicitud. Las solicitudes de servicio se generan al rellenar previamente un formulario, al enviarlo y al invocar servicios a través de una regla.

**Autorización previa al proceso:** puede utilizar la autorización previa al proceso para validar la autenticidad de una solicitud antes de ejecutarla. Puede utilizar entradas, servicios y detalles de solicitud para permitir o detener la ejecución de la solicitud. Puede devolver una excepción de integración de datos OPERATION_ACCESS_DENIED si se detiene la ejecución. También puede modificar la solicitud del cliente antes de enviarla para su ejecución. Por ejemplo, puede cambiar la entrada y agregar información adicional.

**Autorización posterior al proceso:** puede utilizar la autorización posterior al proceso para validar y controlar los resultados antes de devolver los resultados al solicitante. También puede filtrar, recortar e insertar datos adicionales en los resultados.

### Limitar el acceso de los usuarios {#limit-user-access}

Se requiere un conjunto diferente de perfiles de usuario para las instancias de autor, publicación y procesamiento. No ejecute ninguna instancia con credenciales de administrador.

**En una instancia de publicación:**

* Solo los usuarios del grupo forms-users pueden obtener una vista previa, crear borradores y enviar formularios.
* Solo los usuarios del grupo cm-user-agent pueden obtener una vista previa de las cartas de Administración de correspondencia.
* Desactive todos los accesos anónimos no esenciales.

**En una instancia de autor:**

* Hay un conjunto diferente de grupos predefinidos con privilegios específicos para cada perfil. Asigne usuarios al grupo.

   * Un usuario del grupo forms-user:

      * Puede crear, rellenar, publicar y enviar un formulario.
      * No puede crear un formulario adaptable basado en XDP.
      * No tiene permisos para escribir scripts para formularios adaptables.
      * No puede importar XDP ni ningún paquete que contenga XDP.

   * Un usuario del grupo forms-power-user puede crear, cumplimentar, publicar y enviar todo tipo de formularios, escribir scripts para formularios adaptables e importar paquetes que contengan XDP.
   * Un usuario de template-authors y template-power-user puede previsualizar y crear una plantilla.
   * Un usuario de fdm-authors puede crear y modificar un modelo de datos de formulario.
   * Un usuario del grupo cm-user-agent puede crear, previsualizar y publicar cartas de Administración de correspondencia.
   * Un usuario del grupo workflow-editors puede crear una aplicación de bandeja de entrada y un modelo de flujo de trabajo.

**En autor de procesamiento:**

* Para los casos de uso de almacenamiento y envío remotos, puede crear un usuario con permisos de lectura, creación y modificación en la ruta content/form/fp del repositorio CRX.
* Agregue un usuario al grupo workflow-user para permitir que utilice las aplicaciones de la Bandeja de entrada AEM.

## Proteger los elementos de intranet de un entorno de AEM Forms {#secure-intranet-elements-of-an-aem-forms-environment}

En general, los clústeres de procesamiento y el complemento de Forms Workflow (AEM Forms en JEE) se ejecutan detrás de un cortafuegos. Por ello, se consideran seguros. No obstante, hay algunos pasos que puede llevar a cabo para proteger estos entornos:

### Protección del clúster de procesamiento {#secure-processing-cluster}

Un clúster de procesamiento se ejecuta en modo de autor. Sin embargo, no lo utilice en actividades de desarrollo. No permita que se incluya a un usuario normal en los grupos content-authors y form-users de un clúster de procesamiento.

### Use las prácticas recomendadas de AEM para proteger un entorno de AEM Forms {#use-aem-best-practices-to-secure-an-aem-forms-environment}

Este documento contiene instrucciones específicas para el entorno de AEM Forms. Asegúrese de que la instalación de AEM subyacente sea segura cuando la implemente. Para obtener instrucciones detalladas, consulte la documentación [Lista de comprobación de seguridad de AEM](/help/sites-administering/security-checklist.md).
