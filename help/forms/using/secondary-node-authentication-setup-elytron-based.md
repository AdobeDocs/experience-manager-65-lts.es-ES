---
title: Configuración de autenticación de nodo secundario (basado en Elytron)
description: JBoss EAP 8 utiliza Elytron para habilitar la comunicación segura y el registro de nodos secundarios con el controlador de dominio principal.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# Configuración de autenticación de nodo secundario (basado en Elytron)

## Configuración de la autenticación del nodo secundario mediante Elytron

JBoss EAP 8 usa **Elytron** para autenticar la comunicación entre **nodos primarios y secundarios** en una implementación agrupada. Esta configuración garantiza el registro y la comunicación seguros de los nodos secundarios con el controlador de dominio principal.

Hay dos opciones de configuración disponibles según el entorno y los requisitos de seguridad.

## Requisitos previos

* Se debe crear un **usuario de administración denominado`secondary`** en el **nodo principal**.
* Realice esta configuración **solo en los nodos secundarios**.
* Repita la configuración para **cada nodo secundario** del clúster.
* **JBoss debe estar completamente detenido** tanto en los nodos primarios como en los secundarios.
* Todas las operaciones del almacén de credenciales deben realizarse en **modo sin conexión**.

Para detener JBoss si se está ejecutando:

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

## Elegir una opción de configuración

* **Opción 1: configuración rápida mediante el almacén de credenciales predeterminado**
Recomendado para entornos y pruebas más bajos.

* **Opción 2: Configuración del almacén de credenciales personalizadas**
Recomendado para entornos de producción y seguros.

## Opción 1: configuración rápida mediante el almacén de credenciales predeterminado

**Más indicado para:** escenarios de desarrollo, pruebas y configuración rápida.

### Información general

* Un archivo de almacén de credenciales predeterminado (`cs_secondary_hc.p12`) está preconfigurado.
* La contraseña predeterminada del almacén de credenciales ya está establecida en `domain.conf`.
* Solo es necesario añadir el alias de contraseña de autenticación.

### Pasos de configuración

#### Paso 1: Verificar el almacén de credenciales predeterminado

Confirme que existe el archivo de almacén de credenciales predeterminado:

* **Windows**

  ```
  <JBOSS_HOME>\domain\configuration\cs_secondary_hc.p12
  ```

* **Linux**

  ```
  <JBOSS_HOME>/domain/configuration/cs_secondary_hc.p12
  ```

Si el archivo no existe, use **Opción 2**.

#### Paso 2: Añadir alias de contraseña de autenticación

Ejecute el siguiente comando desde `<JBOSS_HOME>/bin`:

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

> El valor secreto debe coincidir con la contraseña utilizada al crear el usuario `secondary` en el nodo principal.

#### Paso 3: Verificar la configuración de domain.conf

Compruebe que la siguiente entrada ya existe (no se requieren cambios):

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=password"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=password"
  ```

#### Paso 4: Inicio de los nodos

1. Inicie el **nodo principal** y espere a que se inicialice completamente.
2. Inicie el **nodo secundario**.

### de verificación

Compruebe los registros:

* **Nodo principal**

  ```
  <JBOSS_HOME>/domain/log/host-controller.log
  ```

  ```
  Registered remote secondary host "secondary"
  ```

* **Nodo secundario**

  ```
  Connected to primary host controller
  ```

## Opción 2: Configuración del almacén de credenciales personalizadas (producción)

**Más indicado para:** entornos de producción que requieren seguridad mejorada.

### Pasos de configuración

#### Paso 1: Eliminar El Almacén De Credenciales Predeterminado (Si Existe)

Si existe el almacén de credenciales predeterminado, cambie su nombre:

* **Windows**

  ```
  rename cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

* **Linux**

  ```
  mv cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

#### Paso 2: Crear un almacén de credenciales personalizado

De `<JBOSS_HOME>/bin`:

* **Windows**

  ```
  elytron-tool.bat credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

#### Paso 3: Añadir alias de contraseña de autenticación

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

#### Paso 4: Actualizar domain.conf

Actualizar la referencia de contraseña del almacén de credenciales:

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=YourCustomPassword"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=YourCustomPassword"
  ```

#### Paso 5: Verificar la configuración de XML

Asegúrese de que `host-secondary.xml` contiene las entradas de cliente de autenticación y almacén de credenciales configuradas.
No se requiere ningún cambio si la configuración predeterminada está presente.


#### Paso 6: Inicio de los nodos

1. Inicie el **nodo principal** y espere hasta que se inicie por completo.
2. Inicie el **nodo secundario**.

### de verificación

Confirme el registro correcto mediante los registros del controlador de host en ambos nodos.

## Resumen

* **La opción 1** proporciona una configuración rápida mediante un almacén de credenciales preconfigurado.
* **Opción 2** habilita una seguridad más sólida mediante una contraseña personalizada del almacén de credenciales.
* La configuración debe completarse **solo en nodos secundarios**.
* La configuración del nodo principal se reutiliza automáticamente en todo el dominio.

