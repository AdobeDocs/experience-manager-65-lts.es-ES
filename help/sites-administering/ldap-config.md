---
title: Configuración de LDAP con AEM 6
description: Aprenda a utilizar y configurar servicios LDAP con AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Configuración de LDAP con AEM 6 {#configuring-ldap-with-aem}

LDAP (el protocolo **L** L **D** irectory **A** ccess **P** rotocol) se usa para acceder a los servicios de directorio centralizados. Ayuda a reducir el esfuerzo necesario para administrar las cuentas de usuario, ya que varias aplicaciones pueden acceder a ellas. Uno de estos servidores LDAP es Active Directory. LDAP se utiliza a menudo para lograr el inicio de sesión único, que permite al usuario acceder a varias aplicaciones después de iniciar sesión una vez.

Las cuentas de usuario se pueden sincronizar entre el servidor LDAP y el repositorio, y los detalles de la cuenta LDAP se guardan en el repositorio. Esta funcionalidad permite asignar las cuentas a grupos de repositorios para asignar los permisos y privilegios necesarios.

El repositorio utiliza la autenticación LDAP para autenticar a estos usuarios, con credenciales que se pasan al servidor LDAP para su validación, que es necesaria antes de permitir el acceso al repositorio. Para mejorar el rendimiento, el repositorio puede almacenar en caché las credenciales validadas correctamente, con un tiempo de espera de caducidad para garantizar que la revalidación se produzca después de un periodo adecuado.

Cuando se quita una cuenta del servidor LDAP, ya no se concede la validación y se deniega el acceso al repositorio. Los detalles de las cuentas LDAP guardadas en el repositorio también se pueden purgar.

El uso de dichas cuentas es transparente para los usuarios. Es decir, no ven ninguna diferencia entre las cuentas de usuario y de grupo creadas a partir de LDAP y las cuentas creadas únicamente en el repositorio.

En AEM 6, la compatibilidad con LDAP viene con una nueva implementación que requiere un tipo de configuración diferente a la de las versiones anteriores.

Todas las configuraciones de LDAP están ahora disponibles como configuraciones de OSGi. Se pueden configurar mediante la consola de administración web en:
`https://serveraddress:4502/system/console/configMgr`

Para que LDAP funcione con AEM, debe crear tres configuraciones OSGi:

1. Un proveedor de identidad LDAP (IDP).
1. Un controlador de sincronización.
1. Un módulo de inicio de sesión externo.

>[!NOTE]
>
>Vea [Módulo de inicio de sesión externo de Oak: autenticación con LDAP y posterior](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html?lang=es) para profundizar en los módulos de inicio de sesión externo.
>
>Para leer un ejemplo de configuración de Experience Manager con Apache DS, consulte [Configuración de Adobe Experience Manager 6.5 para usar el servicio de directorio Apache.](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805?profile.language=es)

## Configuración del proveedor de identidad LDAP {#configuring-the-ldap-identity-provider}

El proveedor de identidad LDAP se utiliza para definir cómo se recuperan los usuarios del servidor LDAP.

Se encuentra en la consola de administración bajo el nombre de **Proveedor de identidad LDAP de Apache Jackrabbit Oak**.

Las siguientes opciones de configuración están disponibles para el proveedor de identidad LDAP:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre de proveedor LDAP</strong></td>
   <td>Nombre de esta configuración de proveedor LDAP.</td>
  </tr>
  <tr>
   <td><strong>Nombre de host del servidor LDAP</strong><br /> </td>
   <td>Nombre de host del servidor LDAP</td>
  </tr>
  <tr>
   <td><strong>Puerto del servidor LDAP</strong></td>
   <td>Puerto del servidor LDAP</td>
  </tr>
  <tr>
   <td><strong>Usar SSL</strong></td>
   <td>Indica si se debe utilizar una conexión SSL (LDAP).</td>
  </tr>
  <tr>
   <td><strong>Usar TLS</strong></td>
   <td>Indica si TLS debe iniciarse en las conexiones.</td>
  </tr>
  <tr>
   <td><strong>Deshabilitar comprobación de certificados</strong></td>
   <td>Indica si la validación de certificados de servidor debe deshabilitarse.</td>
  </tr>
  <tr>
   <td><strong>Enlazar DN</strong></td>
   <td>DN del usuario para la autenticación. Si este campo se deja vacío, se realiza un enlace anónimo.</td>
  </tr>
  <tr>
   <td><strong>Contraseña de enlace</strong></td>
   <td>Contraseña del usuario para la autenticación</td>
  </tr>
  <tr>
   <td><strong>Tiempo de espera de búsqueda</strong></td>
   <td>Tiempo hasta que finaliza la búsqueda</td>
  </tr>
  <tr>
   <td><strong>Grupo de administradores máximo activo</strong></td>
   <td>Tamaño máximo activo del grupo de conexión de administrador.</td>
  </tr>
  <tr>
   <td><strong>Grupo de usuarios máximo activo</strong></td>
   <td>Tamaño máximo activo del grupo de conexión de usuario.</td>
  </tr>
  <tr>
   <td><strong>DN base de usuario</strong></td>
   <td>DN para búsquedas de usuarios</td>
  </tr>
  <tr>
   <td><strong>Clases de objeto de usuario</strong></td>
   <td>La lista de clases de objeto que debe contener una entrada de usuario.</td>
  </tr>
  <tr>
   <td><strong>Atributo de ID de usuario</strong></td>
   <td>Nombre del atributo que contiene el ID de usuario.</td>
  </tr>
  <tr>
   <td><strong>Filtro adicional de usuario</strong></td>
   <td>Filtro LDAP adicional que se utiliza al buscar usuarios. El filtro final tiene el siguiente formato: '(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Rutas DN de usuario</strong></td>
   <td>Controla si el DN debe utilizarse para calcular una parte de la ruta intermedia.</td>
  </tr>
  <tr>
   <td><strong>DN base de grupo</strong></td>
   <td>DN base para búsquedas de grupo.</td>
  </tr>
  <tr>
   <td><strong>Agrupar clases de objeto</strong></td>
   <td>La lista de clases de objeto que debe contener una entrada de grupo.</td>
  </tr>
  <tr>
   <td><strong>Atributo de nombre de grupo</strong></td>
   <td>Nombre del atributo que contiene el nombre del grupo.</td>
  </tr>
  <tr>
   <td><strong>Filtro adicional de grupo</strong></td>
   <td>Filtro LDAP adicional que se utilizará al buscar grupos. El filtro final tiene el siguiente formato: '(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Agrupar rutas DN</strong></td>
   <td>Controla si el DN debe utilizarse para calcular una parte de la ruta intermedia.</td>
  </tr>
  <tr>
   <td><strong>Atributo de miembro de grupo</strong></td>
   <td>Atributo de grupo que contiene uno o varios miembros de un grupo.</td>
  </tr>
 </tbody>
</table>

## Configuración Del Controlador De Sincronización {#configuring-the-synchronization-handler}

El controlador de sincronización define cómo se sincronizan los usuarios y grupos del proveedor de identidad con el repositorio.

Se encuentra bajo el nombre **Apache Jackrabbit Oak Default Sync Handler** en la consola de administración.

Las siguientes opciones de configuración están disponibles para el Controlador de sincronización:

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del controlador de sincronización</strong></td>
   <td>Nombre de la configuración de sincronización.</td>
  </tr>
  <tr>
   <td><strong>Hora de caducidad del usuario</strong></td>
   <td>Duración hasta que caduque un usuario sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Abono automático de usuario</strong></td>
   <td>Lista de grupos a los que se agrega automáticamente un usuario sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Asignación de propiedades de usuario</strong></td>
   <td>Definición de asignación de listas de propiedades locales a partir de propiedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefijo de ruta de usuario</strong></td>
   <td>Prefijo de ruta utilizado al crear usuarios.</td>
  </tr>
  <tr>
   <td><strong>Caducidad de abono de usuario</strong></td>
   <td>Tiempo después del cual caduca la membresía.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profundidad de anidación de pertenencia a usuario</strong></td>
   <td>Devuelve la profundidad máxima de anidamiento de grupos cuando se sincronizan las relaciones de pertenencia. Un valor de 0 deshabilita de forma efectiva la búsqueda de miembros del grupo. El valor 1 solo agrega los grupos directos de un usuario. Este valor no tiene ningún efecto cuando se sincronizan grupos individuales únicamente cuando se sincroniza una ascendencia de pertenencia de usuarios.</td>
  </tr>
  <tr>
   <td><strong>Tiempo de vencimiento del grupo</strong></td>
   <td>Duración hasta que caduque un grupo sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Pertenencia automática al grupo</strong></td>
   <td>Lista de grupos a los que se agrega automáticamente un grupo sincronizado.</td>
  </tr>
  <tr>
   <td><strong>Asignación de propiedades de grupo</strong></td>
   <td>Definición de asignación de listas de propiedades locales a partir de propiedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefijo de ruta de grupo</strong></td>
   <td>Prefijo de ruta utilizado al crear grupos.</td>
  </tr>
 </tbody>
</table>

## El módulo de inicio de sesión externo {#the-external-login-module}

El módulo de inicio de sesión externo se encuentra en **Módulo de inicio de sesión externo de Apache Jackrabbit Oak** en la consola de administración.

>[!NOTE]
>
>El módulo de inicio de sesión externo de Apache Jackrabbit Oak implementa las especificaciones del Servicio de autenticación y autorización de Java™ (JAAS). Consulte la [Guía de referencia de seguridad oficial de Oracle Java™](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) para obtener más información.

Su trabajo es definir qué proveedor de identidad y controlador de sincronización utilizar, enlazando de forma eficaz los dos módulos.

Estas son las opciones de configuración disponibles:

| **Clasificación JAAS** | Especificar la clasificación (es decir, el criterio de ordenación) de esta entrada del módulo de inicio de sesión. Las entradas se ordenan en orden descendente (es decir, las configuraciones con mayor clasificación de valores son las primeras). |
|---|---|
| **Indicador de control de JAAS** | Propiedad que especifica si LoginModule es REQUIRED, REQUISITE, SUFICIENT u OPTIONAL. Consulte la documentación de configuración de JAAS para obtener más información sobre el significado de estos indicadores. |
| **Dominio JAAS** | El nombre de territorio (o nombre de aplicación) con el que está registrado LoginModule. Si no se proporciona ningún nombre de dominio kerberos, LoginModule se registra con un dominio kerberos predeterminado según se ha configurado en la configuración de Felix JAAS. |
| **Nombre del proveedor de identidad** | Nombre del proveedor de identidad. |
| **Nombre del controlador de sincronización** | Nombre del controlador de sincronización. |

>[!NOTE]
>
>Si planea tener más de una configuración LDAP con la instancia de AEM, se deben crear proveedores de identidad y controladores de sincronización independientes para cada configuración.

## Configuración de LDAP sobre SSL {#configure-ldap-over-ssl}

AEM 6 se puede configurar para que se autentique con LDAP a través de SSL siguiendo el siguiente procedimiento:

1. Marque las casillas de verificación **Usar SSL** o **Usar TLS** al configurar el [proveedor de identidad LDAP](#configuring-the-ldap-identity-provider).
1. Configure el controlador de sincronización y el módulo de inicio de sesión externo según la configuración.
1. Instale los certificados SSL en la VM de Java™ si es necesario. Esta instalación se puede realizar utilizando keytool:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Pruebe la conexión con el servidor LDAP.

### Creación de certificados SSL {#creating-ssl-certificates}

Los certificados autofirmados se pueden utilizar al configurar AEM para autenticarse con LDAP a través de SSL. A continuación se muestra un ejemplo de un procedimiento de trabajo para generar certificados para utilizarlos con AEM.

1. Asegúrese de tener una biblioteca SSL instalada y en funcionamiento. Este procedimiento utiliza OpenSSL como ejemplo.

1. Cree un archivo de configuración OpenSSL (cnf) personalizado. Esta configuración se puede realizar copiando el archivo de configuración **openssl.cnf &#x200B;** predeterminado y personalizándolo. En sistemas UNIX®, se encuentra en `/usr/lib/ssl/openssl.cnf`

1. Continúe creando la clave raíz de la CA ejecutando el siguiente comando en un terminal:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. A continuación, cree un certificado autofirmado:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Para asegurarse de que todo está en orden, inspeccione el certificado recién generado:

   `openssl x509 -noout -text -in root-ca.crt`

1. Asegúrese de que existen todas las carpetas especificadas en el archivo de configuración de certificado (.cnf). Si no es así, créelos.
1. Cree una semilla aleatoria ejecutando, por ejemplo:

   `openssl rand -out private/.rand 8192`

1. Mueva los archivos .pem creados a las ubicaciones configuradas en el archivo .cnf.

1. Finalmente, agregue el certificado al repositorio de claves Java™.

## Habilitar el registro de depuración {#enabling-debug-logging}

El registro de depuración se puede habilitar tanto para el proveedor de identidad LDAP como para el módulo de inicio de sesión externo para solucionar los problemas de conexión.

Para habilitar el registro de depuración, debe hacer lo siguiente:

1. Vaya a la consola de administración web.
1. Busque &quot;Configuración del registrador de Apache Sling&quot; y cree dos registradores con las siguientes opciones:

* Nivel de registro: depuración
* Archivo de registro logs/ldap.log
* Patrón de mensaje: &lbrace;0,date,`dd.MM.yyyy` `HH:mm:ss.SSS` &ast;{4}&ast; {2} {3} {5}
* Registrador: org.apache.jackrabbit.oak.security.authentication.ldap

* Nivel de registro: depuración
* Archivo de registro: logs/external.log
* Patrón de mensaje: &lbrace;0,date,`dd.MM.yyyy` `HH:mm:ss.SSS` &ast;{4}&ast; {2} {3} {5}
* Registrador: org.apache.jackrabbit.oak.spi.security.authentication.external

## Una palabra sobre afiliación grupal {#a-word-on-group-affiliation}

Los usuarios sincronizados a través de LDAP pueden formar parte de diferentes grupos en AEM. Estos grupos pueden ser grupos LDAP externos que se agregan a AEM como parte del proceso de sincronización. Sin embargo, también pueden ser grupos que se agregan por separado y que no forman parte del esquema de afiliación de grupo LDAP original.

Por lo general, estos grupos los agrega un administrador local de AEM o cualquier otro proveedor de identidad.

Si se quita un usuario de un grupo en el servidor LDAP, el cambio se refleja en la sincronización del lado de AEM. Sin embargo, todas las demás afiliaciones de grupo del usuario que no fueron agregadas por LDAP permanecen en su lugar.

AEM detecta y administra la depuración de usuarios de grupos externos mediante la propiedad `rep:externalId`. Esta propiedad se agrega automáticamente a cualquier usuario o grupo sincronizado por el controlador de sincronización y contiene información sobre el proveedor de identidad de origen.

Consulte la documentación de Apache Oak sobre la [Sincronización de usuarios y grupos](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemas conocidos {#known-issues}

Si planea utilizar LDAP sobre SSL, asegúrese de que los certificados que está utilizando se crean sin la opción de comentario Netscape. Si esta opción está habilitada, la autenticación falla con un error de protocolo de enlace SSL.
