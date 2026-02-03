---
title: Guía de configuración del almacén de credenciales de base de datos (modo independiente)
description: Busque la configuración del almacén de credenciales de base de datos para AEM Forms JEE en JBoss/Red Hat EAP en modo independiente.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---


# Guía de configuración del almacén de credenciales de base de datos (modo independiente)

## Información general

Esta guía describe la **configuración del almacén de credenciales de la base de datos** para AEM Forms JEE en JBoss/Red Hat EAP en **modo independiente**. Esto es necesario cuando se realiza una instalación manual.

**Esta guía describe:**

- Creando el almacén de credenciales de la base de datos (`cred-store.p12`)
- Añadir alias de contraseña de base de datos de forma segura
- Configurar JBoss para que utilice el almacén de credenciales

**ESENCIAL:** Estos scripts operan en **MODO SIN CONEXIÓN SOLAMENTE**. JBoss debe detenerse antes de ejecutar estos scripts. Los scripts utilizan el modo `embed-server`, que requiere que se detenga el servidor.

**Nota:** Esta es **no** una guía de instalación independiente completa. Este documento supone lo siguiente:

- JBoss ya está instalado
- Los archivos de configuración independientes (`lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`) ya están configurados
- La base de datos está configurada y accesible

Si necesita instrucciones de instalación independientes completas, consulte la guía de instalación principal.

## Requisitos previos

Antes de ejecutar estos scripts, asegúrese de lo siguiente:

1. **DEBE detenerse JBoss**
   - Estos scripts funcionan en **MODO SIN CONEXIÓN SOLAMENTE**
   - Los scripts utilizan `embed-server`, lo que requiere que se detenga el servidor
   - Si JBoss se está ejecutando, los scripts fallarán
   - Compruebe si JBoss se está ejecutando:
      - Windows: comprobar el Administrador de tareas para el proceso `java.exe`
      - Linux: `ps aux | grep jboss` o `ps aux | grep java`
   - Detener JBoss si se ejecuta:
      - Pulse `Ctrl+C` en el terminal donde se está ejecutando JBoss
      - O matar el proceso manualmente

2. **Tiene lista la contraseña de la base de datos**

3. **Ha elegido una contraseña segura para el almacén de credenciales**

4. **Sabe qué archivo de configuración de base de datos está utilizando:**
   - `lc_oracle.xml` (para base de datos de Oracle)
   - `lc_mysql.xml` (para la base de datos MySQL)
   - `lc_mssql.xml` (para la base de datos de Microsoft SQL Server)

## Pasos de configuración

### Paso 1: Crear almacén de credenciales de base de datos

Utilice los scripts proporcionados para crear el almacén de credenciales de la base de datos y agregar todos los alias de contraseña necesarios.

#### En Windows:

**Ubicación del script:** `create-elytron-cred-standalone.bat`

`batch cd path\to\script\location create-elytron-cred-standalone.bat`

**El script le pedirá:**
1. **Ruta JBOSS_HOME** (por ejemplo, `C:\Adobe\Adobe_Experience_Manager_Forms\jboss`)
2. **Nombre del archivo de configuración** (por ejemplo: `lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`)
3. **Contraseña del almacén de credenciales** (protege el archivo del almacén de claves; recuerde esta contraseña)
4. **Contraseña de base de datos** (su contraseña real de base de datos)

**Lo que hace el script:**

- Crea un almacén de credenciales en: `JBOSS_HOME\standalone\configuration\cred-store.p12`
- Modifica temporalmente el archivo de configuración para habilitar la creación del almacén de credenciales
- Agrega los siguientes alias con la contraseña de la base de datos:
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- Restaura el archivo de configuración a su estado original
- Comprueba que todos los alias se hayan agregado correctamente

#### En Linux:

**Ubicación del script:** `create-elytron-cred-standalone.sh`

`bash cd /path/to/script/location chmod +x create-elytron-cred-standalone.sh./create-elytron-cred-standalone.sh`

**El script le pedirá:**

1. **Ruta JBOSS_HOME** (por ejemplo, `/opt/Adobe/Adobe_Experience_Manager_Forms/jboss`)
2. **Nombre del archivo de configuración** (por ejemplo: `lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`)
3. **Contraseña del almacén de credenciales** (protege el archivo del almacén de claves; recuerde esta contraseña)
4. **Contraseña de base de datos** (su contraseña real de base de datos)

**Lo que hace el script:**

- Crea un almacén de credenciales en: `JBOSS_HOME/standalone/configuration/cred-store.p12`
- Modifica temporalmente el archivo de configuración para habilitar la creación del almacén de credenciales
- Agrega los siguientes alias con la contraseña de la base de datos:
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- Restaura el archivo de configuración a su estado original
- Comprueba que todos los alias se hayan agregado correctamente

**Salida esperada:**

```
=== JBoss Elytron Credential Store Setup ===
Enter JBOSS_HOME path (e.g. /opt/jboss): /opt/Adobe/Adobe_Experience_Manager_Forms/jboss
Enter configuration file name (e.g. lc_oracle.xml): lc_oracle.xml
Enter credential store password: ********
Confirm credential store password: ********
Enter database password: ********
Creating credential store using JBoss CLI...
Adding aliases to credential store...
Verifying credential store aliases...

All 4 aliases verified successfully!
- EncryptDBPassword
- EncryptDBPassword_IDP_DS
- EncryptDBPassword_EDC_DS
- EncryptDBPassword_AEM_DS

Credential store setup completed successfully!
```

### Paso 2: Actualización del archivo de configuración independiente

Después de ejecutar el script, debe configurar JBoss para leer la contraseña del almacén de credenciales al inicio.

#### En Windows:

**Ubicación de archivo:** `<JBOSS_HOME>\bin\standalone.conf.bat`

Ejemplo: `C:\Adobe\Adobe_Experience_Manager_Forms\jboss\bin\standalone.conf.bat`

Añada o actualice la línea siguiente:

```batch
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourActualPassword123"
```

Reemplace `YourActualPassword123` con la **contraseña del almacén de credenciales** que utilizó en el paso 1.

#### En Linux:

**Ubicación de archivo:** `<JBOSS_HOME>/bin/standalone.conf`

Ejemplo: `/opt/Adobe/Adobe_Experience_Manager_Forms/jboss/bin/standalone.conf`

Añada o actualice la línea siguiente:

```bash
JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourActualPassword123"
```

Reemplace `YourActualPassword123` con la **contraseña del almacén de credenciales** que utilizó en el paso 1.

### Paso 3: Inicio de JBoss

Después de completar la instalación del almacén de credenciales, inicie JBoss con el archivo de configuración adecuado.

**Nota:** Para conocer los comandos y procedimientos de inicio exactos para iniciar JBoss en modo independiente, consulte la **guía de instalación principal**. Los comandos de inicio pueden variar según la configuración específica y el tipo de base de datos (`lc_oracle.xml`, `lc_mysql.xml` o `lc_mssql.xml`).

## de verificación

### Comprobar registros del servidor

**Ubicación de registro:**

- Windows: `<JBOSS_HOME>\standalone\log\server.log`
- Linux: `<JBOSS_HOME>/standalone/log/server.log`

**Buscar mensajes de inicio correctos:**

```
INFO  [org.jboss.as.server] WFLYSRV0025: JBoss EAP started
INFO  [org.jboss.as.connector.deployers.jdbc] Bound data source [java:/AdobeDataSource]
```

**No hay errores relacionados con:**

- Cargando almacén de credenciales
- Conexión de base de datos
- Faltan alias

## Resolución de problemas

### Problema 1: Almacén de credenciales no encontrado

**Mensaje de error:**

```
ERROR Unable to load credential store
```

**Solución:**

1. Compruebe que el archivo del almacén de credenciales existe:
   - Windows: `dir <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `ls -l <JBOSS_HOME>/standalone/configuration/cred-store.p12`
2. Si falta, vuelva a ejecutar el script de creación del almacén de credenciales (paso 1)

### Problema 2: Contraseña de almacén de credenciales incorrecta

**Mensaje de error:**

```
ERROR Unable to load credential store - Invalid password
```

**Solución:**
Compruebe que la contraseña de `standalone.conf.bat` / `standalone.conf` (Paso 2) coincide con la contraseña utilizada al crear el almacén de credenciales (Paso 1).

**Para corregir:**
Edite `standalone.conf.bat` / `standalone.conf` y actualice la contraseña:

```
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=CorrectPassword"
```

### Problema 3: Error de conexión a base de datos

**Mensaje de error:**

```
ERROR Failed to obtain connection
```

**Solución:**

1. Compruebe que la contraseña de la base de datos utilizada en el almacén de credenciales es correcta
2. Compruebe que la configuración de la fuente de datos hace referencia al alias correcto
3. Comprobar la conectividad de red con el servidor de base de datos

**Para Volver A Crear El Almacén De Credenciales:**

1. Detener JBoss
2. Eliminar el almacén de credenciales existente:
   - Windows: `del <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `rm <JBOSS_HOME>/standalone/configuration/cred-store.p12`
3. Vuelva a ejecutar el script de creación del almacén de credenciales con la contraseña de base de datos correcta

### Problema 4: El script falla durante la ejecución

**Mensaje de error:**

```
ERROR: jboss-cli.bat is not found
```

**Solución:**
Compruebe que la ruta JBOSS_HOME es correcta y señala al directorio de instalación de JBoss.

**Mensaje de error:**

```
ERROR: Configuration file not found
```

**Solución:**

1. Compruebe que el nombre del archivo de configuración es correcto
2. Compruebe que el archivo existe en el directorio `JBOSS_HOME\standalone\configuration\`
3. Asegúrese de utilizar el archivo de configuración específico de la base de datos correcto

## Referencia rápida

### Almacén de credenciales de base de datos (modo independiente)

**Propósito:** Almacenar contraseñas de base de datos de forma segura

**Script:**

- Windows: `create-elytron-cred-standalone.bat`
- Linux: `create-elytron-cred-standalone.sh`

**Crea:**

- Archivo: `standalone/configuration/cred-store.p12`
- Alias: `EncryptDBPassword`, `EncryptDBPassword_IDP_DS`, `EncryptDBPassword_EDC_DS`, `EncryptDBPassword_AEM_DS`

**Configuración:**

- Variable: `-DCS_PASS=password`
- Archivo: `standalone.conf.bat` (Windows) o `standalone.conf` (Linux)

