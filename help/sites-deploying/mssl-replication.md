---
title: Duplicación mediante SSL mutuo
description: Obtenga información sobre cómo configurar AEM para que un agente de replicación en la instancia de autor utilice SSL mutuo (MSSL) para conectarse a la instancia de publicación. Con MSSL, el agente de replicación y el servicio HTTP de la instancia de publicación utilizan certificados para autenticarse mutuamente.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 3%

---

# Duplicación mediante SSL mutuo{#replicating-using-mutual-ssl}

Configure AEM para que un agente de replicación en la instancia de autor utilice SSL mutuo (MSSL) para conectarse a la instancia de publicación. Con MSSL, el agente de replicación y el servicio HTTP de la instancia de publicación utilizan certificados para autenticarse mutuamente.

La configuración de MSSL para la replicación implica realizar los siguientes pasos:

1. Cree o consiga claves y certificados privados para las instancias de autor y publicación.
1. Instale las claves y los certificados en las instancias de autor y publicación:

   * Autor: clave privada del autor y certificado de Publish.
   * Publicar: la clave privada de Publish y el certificado de autor. El certificado está asociado a la cuenta de usuario autenticada con el agente de replicación.

1. Configure el servicio HTTP basado en Jetty en la instancia de publicación.
1. Configure las propiedades de transporte y SSL del agente de replicación.

![chlimage_1-64](assets/chlimage_1-64.png)

Determine qué cuenta de usuario está realizando la replicación. Al instalar el certificado de autor de confianza en la instancia de publicación, el certificado se asocia a esta cuenta de usuario.

## Obtener o crear credenciales para MSSL {#obtaining-or-creating-credentials-for-mssl}

Necesita una clave privada y un certificado público para las instancias de autor y publicación:

* Las claves privadas deben estar contenidas en formato pkcs#12 o JKS.
* Los certificados deben estar en formato pkcs#12 o JKS. Además, el certificado contenido en formato &quot;CER&quot; también se puede añadir a Granite Truststore.
* Los certificados se pueden firmar automáticamente o mediante una CA reconocida.

### Formato JKS {#jks-format}

Genere una clave privada y un certificado en formato JKS. La clave privada se almacena en un archivo KeyStore y el certificado se almacena en un archivo TrustStore. Use [Java `keytool`](https://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html) para crear ambos.

Realice los siguientes pasos utilizando Java `keytool` para crear la clave privada y las credenciales:

1. Genere un par de claves pública y privada en un almacén de claves.
1. Cree o consiga el certificado:

   * Firmado automáticamente: exporte el certificado del almacén de claves.
   * Firmado por la CA: genere una solicitud de certificado y envíela a la CA.

1. Importe el certificado en un almacén de confianza.

Utilice el siguiente procedimiento para crear una clave privada y un certificado autofirmado para las instancias de autor y publicación. Utilice valores diferentes para las opciones de comando según corresponda.

1. Abra una ventana o terminal de la línea de comandos. Para crear el par de claves pública y privada, introduzca el siguiente comando, utilizando los valores de opción de la tabla siguiente:

   ```shell
   keytool -genkeypair -keyalg RSA -validity 3650 -alias alias -keystore keystorename.keystore  -keypass key_password -storepass  store_password -dname "CN=Host Name, OU=Group Name, O=Company Name,L=City Name, S=State, C=Country_ Code"
   ```

   | Opción | Autor | Publicación |
   |---|---|---|
   | -alias | autor | publicación |
   | -keystore | author.keystore | publish.keystore |

1. Para exportar el certificado, introduzca el siguiente comando utilizando los valores de opción de la tabla siguiente:

   ```shell
   keytool -exportcert -alias alias -file cert_file -storetype jks -keystore keystore -storepass store_password
   ```

   | Opción | Autor | Publicación |
   |---|---|---|
   | -alias | autor | publicación |
   | -file | author.cer | publish.cer |
   | -keystore | author.keystore | publish.keystore |

### Formato pkcs#12 {#pkcs-format}

Genere una clave privada y un certificado en formato pkcs#12. Use [openSSL](https://www.openssl.org/) para generarlos. Utilice el siguiente procedimiento para generar una clave privada y una solicitud de certificado. Para obtener el certificado, firme la solicitud con la clave privada (certificado autofirmado) o envíela a una CA. A continuación, genere el archivo pkcs#12 que contiene la clave privada y el certificado.

1. Abra una ventana o terminal de la línea de comandos. Para crear la clave privada, introduzca el siguiente comando, utilizando los valores de opción de la tabla siguiente:

   ```shell
   openssl genrsa -out keyname.key 2048
   ```

   | Opción | Autor | Publicación |
   |---|---|---|
   | -out | author.key | publish.key |

1. Para generar una solicitud de certificado, introduzca el siguiente comando, utilizando los valores de opción de la tabla siguiente:

   ```shell
   openssl req -new -key keyname.key -out key_request.csr
   ```

   | Opción | Autor | Publicación |
   |---|---|---|
   | -key | author.key | publish.key |
   | -out | author_request.csr | publish_request.csr |

   Firme la solicitud de certificado o envíe la solicitud a una CA.

1. Para firmar la solicitud de certificado, introduzca el siguiente comando, utilizando los valores de opción de la siguiente tabla:

   ```shell
   openssl x509 -req -days 3650 -in key_request.csr -signkey keyname.key -out certificate.cer
   ```

   | Opción | Autor | Publicación |
   |---|---|---|
   | -signkey | author.key | publish.key |
   | -in | author_request.csr | publish_request.csr |
   | -out | author.cer | publish.cer |

1. Para añadir la clave privada y el certificado firmado a un archivo pkcs#12, introduzca el siguiente comando, utilizando los valores de opción de la tabla siguiente:

   ```shell
   openssl pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in certificate.cer -inkey keyname.key -out pkcs12_archive.pfx -name "alias"
   ```

   | Opción | Autor | Publicación |
   |---|---|---|
   | -inkey | author.key | publish.key |
   | -out | author.pfx | publish.pfx |
   | -in | author.cer | publish.cer |
   | -name | autor | publicación |

## Instalar la clave privada y TrustStore en Author {#install-the-private-key-and-truststore-on-author}

Instale los siguientes elementos en la instancia de autor:

* La clave privada de la instancia de autor.
* El certificado de la instancia de publicación.

Para realizar el siguiente procedimiento, debe iniciar sesión como administrador de la instancia de autor.

### Instalación de la clave privada del autor {#install-the-author-private-key}

1. Abra la página Administración de usuarios de la instancia de autor. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. Para abrir las propiedades de la cuenta de usuario, haga clic en el nombre de usuario.
1. Si el vínculo Crear almacén de claves aparece en el área Configuración de cuenta, haga clic en el vínculo. Configure una contraseña y haga clic en Aceptar.
1. En el área Configuración de cuenta, haga clic en Administrar almacén de claves.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Haga Clic En Agregar Clave Privada Del Archivo De Almacén De Claves.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Haga clic en Seleccionar archivo de almacén de claves, busque y seleccione el archivo author.keystore o el archivo author.pfx si utiliza pkcs#12 y, a continuación, haga clic en Abrir.
1. Introduzca un alias y la contraseña para el almacén de claves. Introduzca el alias y la contraseña de la clave privada y, a continuación, haga clic en Enviar.
1. Cierre el cuadro de diálogo Administración de almacén de claves.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Instalar el certificado de publicación {#install-the-publish-certificate}

1. Abra la página Administración de usuarios de la instancia de autor. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. Para abrir las propiedades de la cuenta de usuario, haga clic en el nombre de usuario.
1. Si el vínculo Crear almacén de confianza aparece en el área Configuración de cuenta, haga clic en el vínculo, cree una contraseña para el almacén de confianza y haga clic en Aceptar.
1. En el área Configuración de cuenta, haga clic en Administrar almacén de confianza.
1. Haga clic en Agregar certificado del archivo CER.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Desactive la opción Asignar certificado al usuario. Haga clic en Seleccionar archivo de certificado, seleccione publish.cer y haga clic en Abrir.
1. Cierre el cuadro de diálogo Administración de TrustStore.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Instalar Private Key y TrustStore en Publish {#install-private-key-and-truststore-on-publish}

Instale los siguientes elementos en la instancia de publicación:

* La clave privada de la instancia de publicación.
* El certificado de la instancia de autor. Asocie el certificado con el usuario que se utiliza para ejecutar solicitudes de replicación.

Para realizar el siguiente procedimiento, debe iniciar sesión como administrador de la instancia de publicación.

### Instalación de la clave privada de publicación {#install-the-publish-private-key}

1. Abra la página User Management de la instancia de publicación. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. Para abrir las propiedades de la cuenta de usuario, haga clic en el nombre de usuario.
1. Si el vínculo Crear almacén de claves aparece en el área Configuración de cuenta, haga clic en el vínculo. Configure una contraseña y haga clic en Aceptar.
1. En el área Configuración de cuenta, haga clic en Administrar almacén de claves.
1. Haga Clic En Agregar Clave Privada Del Archivo De Almacén De Claves.
1. Haga clic en Seleccionar archivo de almacén de claves, busque y seleccione el archivo publish.keystore o el archivo publish.pfx si utiliza pkcs#12 y, a continuación, haga clic en Abrir.
1. Introduzca un alias y la contraseña para el almacén de claves. Introduzca el alias y la contraseña de la clave privada y, a continuación, haga clic en Enviar.
1. Cierre el cuadro de diálogo Administración de almacén de claves.

### Instalar el certificado de autor {#install-the-author-certificate}

1. Abra la página User Management de la instancia de publicación. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. Si el vínculo Crear almacén de confianza aparece en el área Almacén de confianza global, haga clic en el vínculo, cree una contraseña para el almacén de confianza y haga clic en Aceptar.
1. En el área Configuración de cuenta, haga clic en Administrar almacén de confianza.
1. Haga clic en Agregar certificado del archivo CER.
1. Asegúrese de que la opción Asignar certificado al usuario esté seleccionada. Haga clic en Seleccionar archivo de certificado, seleccione author.cer y haga clic en Abrir.
1. Haga clic en Enviar y cierre el cuadro de diálogo Administración de TrustStore.

## Configuración del servicio HTTP en Publish {#configure-the-http-service-on-publish}

Configure las propiedades del servicio HTTP basado en Apache Felix Jetty en la instancia de publicación para que utilice HTTPS al acceder al repositorio de claves de Granite. El PID del servicio es `org.apache.felix.http`.

En la tabla siguiente se enumeran las propiedades OSGi que debe configurar si utiliza la consola web.

| Nombre de propiedad en la consola web | Nombre de propiedad OSGi | Valor |
|---|---|---|
| Habilitar HTTPS | org.apache.felix.https.enable | true |
| Habilitar HTTPS para utilizar Granite KeyStore | org.apache.felix.https.use.granite.keystore | true |
| Puerto HTTPS | org.osgi.service.http.port.secure | 8443 (u otro puerto deseado) |
| Certificado de cliente | org.apache.felix.https.clientcertificate | &quot;Se busca certificado de cliente&quot; |

## Configuración del agente de replicación en Autor {#configure-the-replication-agent-on-author}

Configure el agente de replicación en la instancia de autor para que utilice el protocolo HTTPS al conectarse a la instancia de publicación. Para obtener información completa sobre la configuración de agentes de replicación, consulte [Configuración de los agentes de replicación](/help/sites-deploying/replication.md#configuring-your-replication-agents).

Para habilitar MSSL, configure las propiedades en la pestaña Transporte según la siguiente tabla:

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>URI</td>
   <td><p>https://server_name:SSL_port/bin/receive?sling:authRequestLogin=1</p> <p>Por ejemplo:</p> <p>http://localhost:8443/bin/receive?sling:authRequestLogin=1</p> </td>
  </tr>
  <tr>
   <td>Usuario</td>
   <td>Sin valor</td>
  </tr>
  <tr>
   <td>Una contraseña</td>
   <td>Sin valor</td>
  </tr>
  <tr>
   <td>SSL</td>
   <td>Autenticación de cliente</td>
  </tr>
 </tbody>
</table>

![chlimage_1-70](assets/chlimage_1-70.png)

Después de configurar el agente de replicación, pruebe la conexión para determinar si MSSL está configurado correctamente.

```xml
29.08.2014 14:02:46 - Create new HttpClient for Default Agent
29.08.2014 14:02:46 - * HTTP Version: 1.1
29.08.2014 14:02:46 - * Using Client Auth SSL configuration *
29.08.2014 14:02:46 - adding header: Action:Test
29.08.2014 14:02:46 - adding header: Path:/content
29.08.2014 14:02:46 - adding header: Handle:/content
29.08.2014 14:02:46 - deserialize content for delivery
29.08.2014 14:02:46 - No message body: Content ReplicationContent.VOID is empty
29.08.2014 14:02:46 - Sending POST request to http://localhost:8443/bin/receive?sling:authRequestLogin=1
29.08.2014 14:02:46 - sent. Response: 200 OK
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Sending message to localhost:8443
29.08.2014 14:02:46 - >> POST /bin/receive HTTP/1.0
29.08.2014 14:02:46 - >> Action: Test
29.08.2014 14:02:46 - >> Path: /content
29.08.2014 14:02:46 - >> Handle: /content
29.08.2014 14:02:46 - >> Referer: about:blank
29.08.2014 14:02:46 - >> Content-Length: 0
29.08.2014 14:02:46 - >> Content-Type: application/octet-stream
29.08.2014 14:02:46 - --
29.08.2014 14:02:46 - << HTTP/1.1 200 OK
29.08.2014 14:02:46 - << Connection: Keep-Alive
29.08.2014 14:02:46 - << Server: Day-Servlet-Engine/4.1.64
29.08.2014 14:02:46 - << Content-Type: text/plain;charset=utf-8
29.08.2014 14:02:46 - << Content-Length: 26
29.08.2014 14:02:46 - << Date: Fri, 29 Aug 2014 18:02:46 GMT
29.08.2014 14:02:46 - << Set-Cookie: login-token=3529326c-1500-4888-a4a3-93d299726f28%3ac8be86c6-04bb-4d18-80d6-91278e08d720_98797d969258a669%3acrx.default; Path=/; HttpOnly; Secure
29.08.2014 14:02:46 - << Set-Cookie: cq-authoring-mode=CLASSIC; Path=/; Secure
29.08.2014 14:02:46 - <<
29.08.2014 14:02:46 - << R
29.08.2014 14:02:46 - << eplicationAction TEST ok.
29.08.2014 14:02:46 - Message sent.
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Replication (TEST) of /content successful.
Replication test succeeded
```
