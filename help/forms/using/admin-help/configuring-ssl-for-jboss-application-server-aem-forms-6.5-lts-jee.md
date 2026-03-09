---
title: Configuración de SSL para el servidor de aplicaciones JBoss (AEM 6.5 LTS JEE)
description: Obtenga información sobre cómo configurar SSL para el servidor de aplicaciones JBoss.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
exl-id: 8a2fbfdc-2b6a-4c9d-beab-1908a9261003
source-git-commit: e48d0604cc8fd1cf745aafa9c70aab17944f4882
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---

# Configuración de SSL para el servidor de aplicaciones JBoss (AEM 6.5 LTS JEE)

## Información general

Para configurar SSL en el servidor de aplicaciones JBoss para Adobe Experience Manager (AEM) 6.5 LTS que se ejecuta en Java EE, debe habilitar la comunicación HTTPS segura. Al habilitar SSL, se cifran los datos intercambiados entre los clientes y el servidor, lo que lo convierte en un requisito de seguridad crítico para cualquier implementación de producción de AEM Forms.

El proceso consta de dos etapas principales:

- **Obtención de una credencial SSL**: ya sea generando un certificado autofirmado o solicitando uno a una entidad emisora de certificados (CA).
- **Habilitación de SSL en JBoss**: uso del subsistema Elytron mediante comandos JBoss CLI.

En esta guía se utilizan los siguientes valores de marcador de posición:

- `[appserver root]`: el directorio principal del servidor de aplicaciones JBoss que ejecuta AEM Forms.
- `[type]`: un nombre de carpeta que varía según el tipo de instalación realizada.
- `[JAVA_HOME]`: el directorio donde está instalado el JDK.

## Parte 1: Crear una credencial SSL (firmada automáticamente)

Si no dispone de un certificado de una CA, puede generar una credencial SSL autofirmada con la utilidad Java `keytool`. Esto es adecuado para entornos de desarrollo o prueba.

### Paso 1: Generación del almacén de claves

Vaya a `[JAVA_HOME]/bin` en un símbolo del sistema y ejecute el siguiente comando, reemplazando los valores por los apropiados para su entorno. El nombre de host debe ser el nombre de dominio completo (FQDN) del servidor de aplicaciones:

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

Cuando se le solicite, escriba `keystore_password`. Tenga en cuenta que la contraseña del almacén de claves y la clave deben ser idénticas.

### Paso 2: Copia del almacén de claves en el directorio de configuración

Copie el repositorio de claves generado en la carpeta de configuración adecuada para su tipo de instalación:

```bash
# Windows Single Server
copy keystorename.keystore [appserver root]\standalone\configuration

# Windows Server Cluster
copy keystorename.keystore [appserver root]\domain\configuration

# Linux Single Server
cp keystorename.keystore [appserver root]/standalone/configuration

# Linux Server Cluster
cp keystorename.keystore [appserver root]/domain/configuration
```

### Paso 3: Exportación del archivo de certificado

Exporte el certificado desde el repositorio de claves mediante uno de los siguientes comandos:

```bash
# Single Server
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/standalone/configuration/keystorename.keystore

# Server Cluster
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/domain/configuration/keystorename.keystore
```

Escriba `keystore_password` cuando se le solicite.

### Paso 4: Copia y verificación del certificado

Copie `AEMForms_cert.cer` al directorio de configuración y, a continuación, compruebe su contenido:

```bash
# Copy (Linux Single Server example)
cp AEMForms_cert.cer [appserver root]/standalone/configuration

# Verify certificate contents (Single Server)
keytool -printcert -v -file [appserver root]/standalone/configuration/AEMForms_cert.cer

# Verify certificate contents (Server Cluster)
keytool -printcert -v -file [appserver root]/domain/configuration/AEMForms_cert.cer
```

### Paso 5: Importación del certificado en Java Truststore

Antes de realizar la importación, asegúrese de que el archivo `cacerts` se pueda escribir:

```bash
# Windows: Right-click cacerts → Properties → deselect Read-only

# Linux:
chmod 777 [JAVA_HOME]/jre/lib/security/cacerts
```

A continuación, importe el certificado:

```bash
keytool -import -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [JAVA_HOME]/jre/lib/security/cacerts
```

Cuando se le pida la contraseña, escriba `changeit` (la contraseña predeterminada del almacén de confianza de Java: consulte con su administrador si se ha modificado). ¿Cuándo se le preguntó **Confiar en este certificado? [no]**, tipo `yes`. Debería ver un mensaje de confirmación: *&quot;Se agregó el certificado al almacén de claves.&quot;*

>[!NOTE]
>
> Si se está conectando a AEM Forms a través de SSL desde Workbench, también debe instalar el certificado en el equipo de Workbench.

## Parte 2: Habilitar SSL en JBoss mediante el subsistema Elytron

Con las credenciales SSL activadas, ahora puede habilitar HTTPS en JBoss mediante su subsistema de seguridad de Elytron a través de la CLI de JBoss. Asegúrese de que el archivo de almacén de claves esté ubicado en el directorio de configuración adecuado antes de continuar.

>[!NOTE]
>
> En Windows, cada comando CLI debe introducirse como una sola línea sin saltos de línea. Reemplace `keystorename.keystore` por su nombre de archivo real y `changeit` por su contraseña de almacén de claves/clave.

### Paso 6a — Creación de un almacén de claves Elytron

```bash
/subsystem=elytron/key-store=aemKeyStore:add(
  path="keystorename.keystore",
  relative-to=jboss.server.config.dir,
  type="JKS",
  credential-reference={clear-text="changeit"})
```

Reemplazar `JKS` por `PKCS12` si el almacén de claves utiliza ese formato.

### Paso 6b — Creación de Elytron Key-Manager

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  credential-reference={clear-text="changeit"})
```

Si el repositorio de claves contiene varias entradas de certificado, especifique explícitamente el alias:

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  alias="AEMForms Cert",
  credential-reference={clear-text="changeit"})
```

### Paso 6c: Actualización del Contexto SSL del Servidor

```bash
/subsystem=elytron/server-ssl-context=applicationSSC:write-attribute(
  name=key-manager,
  value=aemKeyManager)
```

### Paso 6d: Configuración del Listener HTTPS de Undertow

Conecte el contexto SSL en Undertow (el servidor web JBoss) para habilitar el detector de HTTPS:

```bash
/subsystem=undertow/server=default-server/https-listener=https:add(
  socket-binding=https,
  ssl-context=applicationSSC)
```

## Parte 3: Reinicio del servidor de aplicaciones

Después de completar la configuración de Elytron, reinicie JBoss para aplicar los cambios.

### Instalaciones llave en mano (Servicios de Windows)

- Abra **Panel de control de Campaign > Herramientas administrativas > Servicios**.
- Seleccione **JBoss para formularios Adobe Experience Manager**.
- Seleccione **Acción > Detener** y espere a que se detenga el servicio.
- Seleccione **Acción > Iniciar**.

### Instalaciones JBoss preconfiguradas o manuales

Desde un símbolo del sistema, vaya a `[appserver root]/bin`:

```bash
# Stop the server
Windows: shutdown.bat -S
Linux:   ./shutdown.sh -S

# Wait until JBoss fully shuts down, then start the server
Windows: run.bat -c <profile>
Linux:   ./run.sh -c <profile>
```

## Parte 4: Solicitar una credencial de una autoridad certificadora

Para entornos de producción, debe utilizar un certificado emitido por una autoridad de certificación (CA) de confianza. El proceso implica generar un par de claves, crear una Solicitud de firma de certificado (CSR) y, a continuación, importar el certificado firmado por la CA.

### Generación del almacén de claves y creación de una CSR

Vaya a `[JAVA_HOME]/bin` y genere el almacén de claves:

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

A continuación, genere la CSR para enviarla a su CA:

```bash
keytool -certreq -alias "AEMForms Cert" \
  -keystore keystorename.keystore \
  -file AEMFormscertRequest.csr
```

Envíe el archivo de `.csr` a su CA. Una vez que vuelva a recibir el certificado firmado, siga los pasos a continuación.

### Importar el certificado firmado por la CA

Importe primero el certificado raíz de la CA:

```bash
keytool -import -trustcacerts -file rootcert.pem \
  -keystore keystorename.keystore -alias root
```

Si el explorador aún no confía en el certificado raíz, impórtelo allí también. A continuación, importe el certificado firmado por la CA:

```bash
keytool -import -trustcacerts -file CACertificateName.crt \
  -keystore keystorename.keystore
```

>[!NOTE]
>
> El certificado firmado por la CA importado reemplazará cualquier certificado público firmado automáticamente existente si hay uno en el almacén de claves.

Una vez importado el certificado de CA, continúe con **Pasos 6a-6d** en la Parte 2 (Configuración de Elytron), reinicie el servidor (Parte 3) y verifique el acceso SSL.

## Verificar acceso SSL

Después de reiniciar el servidor, compruebe que SSL funciona correctamente accediendo a la consola de administración de AEM Forms a través de HTTPS. El puerto SSL predeterminado para JBoss es `8443`:

```
https://[host name]:8443/adminui
```

Si la consola de administración se carga correctamente en HTTPS, SSL se ha configurado correctamente. Utilice el puerto `8443` para todas las conexiones SSL subsiguientes con AEM Forms.
