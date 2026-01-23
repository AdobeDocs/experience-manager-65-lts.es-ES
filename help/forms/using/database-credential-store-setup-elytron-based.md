---
title: Configuración del almacén de credenciales de base de datos (basado en Elytron)
description: JBoss EAP 8 admite almacenes de credenciales de Elytron para la administración segura de contraseñas de bases de datos en AEM Forms para la configuración del modo de dominio.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: d397e6a51ad2a52da5ccb0a690e1acd3fafcee3c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 2%

---


# Configuración del almacén de credenciales de base de datos (basado en Elytron)

## Configurar el almacén de credenciales de base de datos mediante Elytron

JBoss EAP 8 usa **almacenes de credenciales de Elytron** para administrar de forma segura las contraseñas de base de datos para implementaciones de AEM Forms. Adobe proporciona **scripts automatizados** para simplificar la creación y configuración del almacén de credenciales basado en Elytron en modo de dominio.

Esta configuración debe completarse **antes de iniciar el controlador de dominio de JBoss**.

### Requisitos previos

* El servidor **JBoss debe estar completamente detenido** antes de ejecutar el script de creación del almacén de credenciales.
* La creación del almacén de credenciales debe realizarse solamente en **modo sin conexión**.

Para detener JBoss si se está ejecutando:

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

### Descargar scripts

Descargue la secuencia de comandos adecuada en función de su sistema operativo:

| Nombre de script | Sistema operativo |
| -------------------------------- | ---------------- |
| `create-elytron-cred-domain.bat` | Windows |
| `create-elytron-cred-domain.sh` | Linux/UNIX |

En Linux, convierta el script en ejecutable:

```
chmod +x create-elytron-cred-domain.sh
```

### Pasos de configuración

#### Paso 1: Descargar y colocar el script

Descargue el script adecuado y colóquelo en el siguiente directorio:

```
<JBOSS_HOME>/bin
```

#### Paso 2: Ejecutar la secuencia de comandos

* **Windows**

  ```
  cd <JBOSS_HOME>\bin
  create-elytron-cred-domain.bat
  ```

* **Linux / UNIX**

  ```
  cd <JBOSS_HOME>/bin
  ./create-elytron-cred-domain.sh
  ```

#### Paso 3: Proporcionar la información necesaria

Durante la ejecución, la secuencia de comandos solicita las siguientes entradas:

1. **Ruta JBOSS_HOME**
Introduzca la ruta completa al directorio de instalación de JBoss.

2. **Nombre de archivo de configuración de base de datos**
Introduzca una de las siguientes opciones en función de la base de datos:

   * `domain_oracle.xml`
   * `domain_mysql.xml`
   * `domain_mssql.xml`

3. **Contraseña de almacén de credenciales**
Escriba una contraseña segura para proteger el almacén de credenciales.

   > Esta contraseña se oculta durante la entrada y debe recordarse para pasos posteriores.

4. **Contraseña de base de datos**
Introduzca la contraseña real de la conexión a base de datos.

#### Paso 4: Ejecución y validación de scripts

La secuencia de comandos realiza automáticamente las siguientes acciones:

* Crea `cred-store.p12` en:

  ```
  <JBOSS_HOME>/domain/configuration/
  ```

* Crea los siguientes alias de credenciales:

   * `EncryptDBPassword`
   * `EncryptDBPassword_IDP_DS`
   * `EncryptDBPassword_EDC_DS`
   * `EncryptDBPassword_AEM_DS`
* Comprueba que todos los alias se hayan agregado correctamente

La ejecución correcta confirma la creación del almacén de credenciales y la verificación de alias.

#### Paso 5: Configurar las opciones de JVM

Actualice la configuración de inicio del dominio JBoss para proporcionar la contraseña del almacén de credenciales.

* **Linux**
Editar:

  ```
  <JBOSS_HOME>/bin/domain.conf
  ```

  Agregar:

  ```
  JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourCredStorePassword"
  ```

* **Windows**
Editar:

  ```
  <JBOSS_HOME>/bin/domain.conf.bat
  ```

  Agregar:

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourCredStorePassword"
  ```

Reemplazar `YourCredStorePassword` por la contraseña ingresada durante la creación del almacén de credenciales.

Los archivos de configuración de dominio hacen referencia a este valor mediante la variable `${CS_PASS}`.


#### Paso 6: Verificar la configuración del dominio

Abra el archivo de configuración del dominio de base de datos:

```
<JBOSS_HOME>/domain/configuration/<domain_*.xml>
```

Compruebe que las fuentes de datos hacen referencia al almacén de credenciales de Elytron:

```xml
<security>
    <user-name>your_database_username</user-name>
    <credential-reference store="db-creds" alias="EncryptDBPassword_IDP_DS"/>
</security>
```

Cada origen de datos utiliza un alias específico:

* **IDP_DS:** `EncryptDBPassword_IDP_DS`
* **EDC_DS:** `EncryptDBPassword_EDC_DS`
* **AEM_DS:** `EncryptDBPassword_AEM_DS`
* **DefaultDS / ExampleDS:** `EncryptDBPassword`

Todos los alias hacen referencia a la misma contraseña de base de datos almacenada en el almacén de credenciales.

>[!NOTE]
>
>* Configure el almacén de credenciales solo en el nodo principal.
>* Los nodos secundarios utilizan automáticamente la configuración de dominio sincronizada desde el nodo principal.
