---
title: Actualización de AEM 6.5 LTS en JBoss EAP 8 (Windows)
description: Esta guía proporciona instrucciones paso a paso para actualizar una instalación existente de Adobe Experience Manager (AEM) 6.5 LTS de JBoss EAP 7.4 a JBoss EAP 8 en Windows, mediante JDK 21.
source-git-commit: 835530039678bc16a6de87b8d580be91a2026f94
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 3%

---

# Actualización de AEM 6.5 LTS en JBoss EAP 8 (Windows)

## Información general

Esta guía proporciona instrucciones paso a paso para actualizar una instalación existente de Adobe Experience Manager (AEM) 6.5 LTS de JBoss EAP 7.4 a JBoss EAP 8 en Windows, mediante JDK 21.

**Ruta de actualización:** JBoss EAP 7.4 (JDK 11) → JBoss EAP 8 (JDK 21)

## Avisos importantes

>[!NOTE]
>
>Este es un procedimiento de actualización esencial. Realice siempre primero esta actualización en un entorno que no sea de producción y realice copias de seguridad completas.
>
> **&#x200B; REQUISITOS PREVIOS:** Es obligatorio realizar una copia de seguridad completa del sistema y un plan de reversión documentado antes de continuar.

## Requisitos previos a la actualización

### Requisitos del sistema

| Componente | Requisito |
|-----------|-------------|
| Sistema operativo | Windows Server 2016 o posterior (64 bits) |
| Entorno de Source | JBoss EAP 7.4 con AEM 6.5 LTS |
| Entorno de destino | JBoss EAP 8.x |
| Java Development Kit | JDK 21 (Oracle o OpenJDK) |
| Versión de AEM | Paquete de servicio de AEM 6.5 (recomendado más reciente) |
| Espacio en disco | Espacio libre mínimo de 50 GB para el proceso de actualización |

### Descargas requeridas

Antes de comenzar la actualización, obtenga lo siguiente:

1. **Distribución EAP 8.0 de JBoss**\
   Descargar de: [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. **Instalador de JDK 21**\
   Descargar Oracle JDK 21 u OpenJDK 21 para Windows (64 bits)

3. **Archivo WAR DE AEM 6.5 LTS**\
   Obtenga la última versión de AEM 6.5 Service Pack WAR de Adobe Software Distribution

## Paso 1: Crear Copia De Seguridad Completa

>[!IMPORTANT]
>
> Realice copias de seguridad completas antes de continuar.

### Lista de comprobación de copia

- [ ] Copia de seguridad completa del directorio de instalación de JBoss EAP 7.4 existente
- [ ] copia de seguridad de `crx-repository` carpeta
- [ ] copia de seguridad de `crx-quickstart` carpeta
- [ ] exportación de todas las configuraciones personalizadas
- [ Copia de seguridad de la base de datos ] (si usa una base de datos externa)
- [ ]: documenta el estado y las configuraciones actuales del sistema.

### Crear copia de seguridad

```cmd
# Example backup location
C:\AEM-Backups\Pre-Upgrade-<date>

# Copy entire JBoss 7.4 directory
xcopy "C:\jboss-eap-7.4" "C:\AEM-Backups\Pre-Upgrade-<date>\jboss-eap-7.4" /E /I /H
```

**Recomendado:** Almacenar copias de seguridad en una unidad o ubicación de red independiente.

## Paso 2: Instalar JBoss EAP 8

### Extraer JBoss EAP 8

1. Extraiga la distribución JBoss EAP 8 ZIP en el directorio de instalación de Target:

   ```
   C:\jboss-eap-8.0
   ```

2. Tenga en cuenta esta ruta de acceso de directorio como `<JBOSS_HOME>` para su uso en esta guía.

### Replicar estructura de directorio

Asegúrese de que la nueva instalación de JBoss EAP 8 tenga la misma estructura de directorio personalizada que la instalación de JBoss EAP 7.4 anterior, en particular:

- Directorios de implementación personalizados
- Carpetas de configuración externa
- Ubicaciones de archivos de registro
- Cualquier módulo o biblioteca personalizada

## Paso 3: Migrar datos de repositorio

### Copiar repositorio de CRX

1. Vaya a la instalación existente de JBoss EAP 7.4:

   ```
   <OLD_JBOSS_HOME>\bin\crx-repository
   ```

2. Copie toda la carpeta `crx-repository` en la nueva instalación de JBoss EAP 8:

   ```cmd
   xcopy "C:\jboss-eap-7.4\bin\crx-repository" "C:\jboss-eap-8.0\bin\crx-repository" /E /I /H
   ```

**Importante:** Esta carpeta contiene su repositorio de contenido y debe transferirse por completo.

### Verificar copia del repositorio

Después de copiar, compruebe que el tamaño y la estructura del repositorio coinciden con el origen:

```cmd
dir "C:\jboss-eap-8.0\bin\crx-repository" /s
```

## Paso 4: Detener la instancia de AEM

Antes de realizar cualquier cambio, asegúrese de que AEM esté completamente detenido.

### Detener mediante Servicios de Windows

1. Abrir **Servicios** (Ejecutar: `services.msc`)
2. Localice el servicio AEM/JBoss
3. Haga clic con el botón derecho y seleccione **Detener**
4. Espere a que el servicio se detenga por completo

### Detener a través de la línea de comandos

Si AEM se inició manualmente:

1. Vaya a la ventana de la consola JBoss
2. Presione `Ctrl+C`
3. Esperar a que se complete el cierre correcto

### Verificar apagado

Asegúrese de que el proceso de Java ya no se esté ejecutando:

```cmd
tasklist | findstr java
```

## Paso 5: Limpieza De Archivos De AEM Heredados

Quite los archivos obsoletos del directorio `crx-quickstart` para garantizar una actualización limpia.

>[!CAUTION]
>
> Eliminar solo los archivos y carpetas específicos que se enumeran a continuación. No elimine ningún otro archivo de configuración, código personalizado o datos del repositorio.

### 5.1 Eliminar la carpeta de inicio de Launchpad

**Ubicación:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\startup
```

**Acción:**

```cmd
rd /s /q "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\startup"
```

**Propósito:** Esta carpeta contiene paquetes OSGi antiguos que se regenerarán durante la actualización.

### 5.2 Eliminar archivo JAR base

**Ubicación:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar
```

**Acción:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar"
```

**Propósito:** Este JAR se reemplazará con la versión del nuevo archivo WAR.

### 5.3 Eliminar archivo de comandos de Bootstrap

**Ubicación:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt
```

**Acción:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt"
```

**Propósito:** los comandos de Bootstrap se regenerarán para el nuevo entorno.

### 5.4 Eliminar archivo sling.options

**Ubicación:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file
```

**Acción:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file"
```

### 5.5 Eliminar archivo sling_bootstrap.txt

**Ubicación:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt
```

**Acción:**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt"
```

### 5.6 Copia de seguridad y eliminación del archivo sling.properties

Este archivo contiene configuraciones específicas del entorno que pueden ser necesarias para combinarse más adelante.

**Ubicación:**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
```

**Acción:**

1. **Crear copia de seguridad:**

   ```cmd
   copy "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties" "C:\AEM-Backups\sling.properties.backup"
   ```

2. **Eliminar original:**

   ```cmd
   del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties"
   ```

**Propósito:** Se generará un nuevo(a) `sling.properties`. Revise la copia de seguridad para restaurar cualquier configuración personalizada después de la actualización.

## Paso 6: Instalación y configuración de JDK 21

### Instalación de JDK 21

1. Ejecute el instalador de JDK 21 para Windows
2. Instale en una ubicación estándar (por ejemplo, `C:\Program Files\Java\jdk-21`)
3. Completar el asistente de instalación

### Configurar variables de entorno

#### Establecer JAVA_HOME

1. Abrir **Propiedades del sistema** → **Avanzadas** → **Variables de entorno**
2. En **Variables del sistema**, haga clic en **Nuevo**
3. Establecer:
   - Nombre de variable: `JAVA_HOME`
   - Valor de variable: `C:\Program Files\Java\jdk-21`
4. Haga clic en **Aceptar**

#### Actualizar variable PATH

1. En **Variables del sistema**, seleccione `Path` y haga clic en **Editar**
2. Agregar nueva entrada:

   ```
   %JAVA_HOME%\bin
   ```

3. Mueva esta entrada al principio de la lista para asegurarse de que JDK 21 tenga prioridad
4. Haga clic en **Aceptar** en todos los cuadros de diálogo

### Verificar instalación de Java

1. Abra un símbolo del sistema **new** (para cargar variables de entorno actualizadas)
2. Verifique la versión de Java:

   ```cmd
   java -version
   ```

   Resultado esperado:

   ```
   java version "21.0.x"
   Java(TM) SE Runtime Environment (build 21.0.x+...)
   Java HotSpot(TM) 64-Bit Server VM (build 21.0.x+..., mixed mode, sharing)
   ```

3. Verificar JAVA_HOME:

   ```cmd
   echo %JAVA_HOME%
   ```

## Paso 7: Configuración de JVM

Antes de implementar AEM, configure las opciones de memoria JVM adecuadas para el uso en producción.

### Editar standalone.conf.bat

1. Vaya a:

   ```
   <JBOSS_HOME>\bin
   ```

2. Abrir `standalone.conf.bat` en un editor de texto (como administrador)

3. Busque o agregue la configuración `JAVA_OPTS`:

   ```batch
   rem # AEM Production JVM Settings
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=768m"
   set "JAVA_OPTS=%JAVA_OPTS% -Djava.net.preferIPv4Stack=true"
   set "JAVA_OPTS=%JAVA_OPTS% -Dfile.encoding=UTF-8"
   set "JAVA_OPTS=%JAVA_OPTS% -server"
   ```

4. Guarde y cierre el archivo

**Configuración recomendada:**

| Parámetro | Valor recomendado | Descripción |
|-----------|-------------------|-------------|
| `-Xms` | 4096 m - 8192 m | Tamaño inicial de la pila |
| `-Xmx` | 4096 m - 8192 m | Tamaño máximo de pila |
| `-XX:MaxMetaspaceSize` | 768 m - 1024 m | Límite de metaespacio |

**Nota:** Ajuste los valores en función de la memoria disponible y los requisitos de carga de trabajo del servidor.

## Paso 8: Implementar AEM 6.5 LTS WAR

### Preparar archivo WAR

Asegúrese de que el archivo AEM WAR esté configurado correctamente según la guía de implementación:

- `jboss-deployment-structure.xml` está presente
- `web.xml` incluye la configuración multipart-config
- WAR se vuelve a empaquetar si se realizó alguna modificación

### Implementar en JBoss

1. Copie el archivo WAR de AEM 6.5 LTS en el directorio de implementaciones:

   ```cmd
   copy "C:\AEM-Downloads\cq-quickstart-6.5.xx.war" "C:\jboss-eap-8.0\standalone\deployments\cq-quickstart.war"
   ```

**Importante:** Asegúrese de que el nombre de archivo WAR coincida con la ruta de acceso de contexto de URL deseada.

## Paso 9: Iniciar JBoss EAP 8 con AEM

### Inicie el servidor

1. Abrir **Símbolo del sistema** como **Administrador**

2. Vaya al directorio bin de JBoss:

   ```cmd
   cd C:\jboss-eap-8.0\bin
   ```

3. Iniciar JBoss EAP 8:

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

### Supervisar inicio inicial

Observe la salida de la consola en busca de:

1. **Implementación de WAR:**

   ```
   Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
   ```

2. **Mensajes de inicialización de AEM:**

   ```
   Apache Sling Application Launcher
   Sling Home: crx-repository/crx-quickstart
   ```

3. **Actualización del repositorio (si corresponde):**

   ```
   Performing repository migration...
   ```

**Tiempo de inicio esperado:** de 5 a 15 minutos, según el tamaño del repositorio y los recursos del sistema.

## Paso 10: Verificar el éxito de la actualización

### Comprobar inicio de AEM

Monitorice la consola JBoss para ver el mensaje de inicio final:

```
**** AEM started successfully ****
```

### Acceso a la interfaz de AEM

1. Apertura de un explorador web
2. Vaya a:

   ```
   http://localhost:8080/cq-quickstart
   ```

3. Inicie sesión con credenciales de administrador:
   - Nombre de usuario: `admin`
   - Contraseña: `admin` (o su contraseña personalizada)

### Verificar información del sistema

1. Vaya a **Herramientas** → **Operaciones** → **Consola web**

   ```
   http://localhost:8080/cq-quickstart/system/console
   ```

2. Haga clic en **Información del sistema**

3. Verificar:

   - **Versión de JVM:** debe mostrar Java 21
   - **Versión de JBoss:** debe mostrar EAP 8.x
   - **Versión de AEM:** debería mostrar 6.5.xx

### Comprobar el estado del sistema

Vaya a **Herramientas** → **Operaciones** → **Diagnóstico** para ejecutar las comprobaciones de estado:

- Estado del paquete: todos los paquetes deben estar &quot;activos&quot;
- Resolución de recursos: Debe mostrar un estado correcto
- Rendimiento de la consulta: revisar cualquier degradación

## Tareas posteriores a la actualización

### Restaurar configuraciones personalizadas

1. Revisar el archivo de copia de seguridad `sling.properties`
2. Restaure los modos de ejecución o configuraciones personalizados en el nuevo archivo:

   ```
   <JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
   ```

3. Reinicie AEM si se han cambiado las configuraciones

### Actualizar agentes de replicación

1. Vaya a **Herramientas** → **Implementación** → **Replicación** → **Agentes en Autor**
2. Revisar y probar todos los agentes de replicación
3. Actualizar cualquier referencia codificada a rutas de servidor antiguas

### Prueba de funcionalidad crítica

- [ ] Creación y publicación de contenido
- [ ] Carga y procesamiento de recursos
- [ ] ejecución de flujo de trabajo
- [ Autenticación de usuario ]
- [ ] extremos de integración
- [ ] componentes y plantillas personalizados

### Optimización de rendimiento

1. Revisar y borrar cualquier caché temporal
2. Monitorización del rendimiento del sistema durante el uso inicial
3. Ajuste la configuración de JVM si es necesario en función de los patrones de uso reales

## Solución de problemas

### Problemas comunes

| Problema | Causa posible | Solución |
|-------|---------------|----------|
| AEM no se puede iniciar | Versión de Java incorrecta | Verificar `JAVA_HOME` puntos para JDK 21 |
| Errores de corrupción de repositorios | Copia de repositorio incompleta | Restaurar desde el repositorio de copia de seguridad y volver a copiar |
| OutOfMemoryError | Memoria insuficiente | Aumentar `-Xmx` en `standalone.conf.bat` |
| Paquetes en estado &quot;Instalado&quot; | Faltan dependencias | Comprobación de dependencias del paquete en la consola web |
| El puerto 8080 ya está en uso | Otro servicio que utiliza el puerto | Detener el servicio en conflicto o cambiar el puerto JBoss |

### Ubicaciones de archivos de registro

- **Registro del servidor JBoss:**\
  `<JBOSS_HOME>\standalone\log\server.log`

- **Registro de errores de AEM:**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\error.log`

- **Registro de acceso de AEM:**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\access.log`

### Procedimiento de reversión

Si la actualización falla y no se puede resolver:

1. Detener JBoss EAP 8
2. Restaurar la copia de seguridad completa de JBoss EAP 7.4
3. Restaurar la carpeta `crx-repository`
4. Verificar `JAVA_HOME` puntos para JDK 11 (si se revierte)
5. Iniciar el entorno anterior

## Prácticas recomendadas

### Antes de la implementación de producción

- [ ] Probar el proceso de actualización completo en un entorno de desarrollo
- [ ]: prueba en un entorno de ensayo con datos de producción
- [ ] Documentar todas las configuraciones e integraciones personalizadas
- [ ]: crear un plan de reversión detallado
- [ ] Programar actualización durante la ventana de mantenimiento
- [ ]: notificar a todos los interesados del tiempo de inactividad planificado

### Tras la actualización correcta

- [ ] Supervisar los registros del sistema durante 48 a 72 horas
- [ ] Realizar prueba de carga para identificar problemas de rendimiento
- [ ] Actualizar documentación del sistema
- [ ] Entrenar equipo en cualquier diferencia de JBoss EAP 8
- [ ] Archivar toda la documentación de actualización y las copias de seguridad

## Documentación relacionada

- [Guía de migración de JBoss EAP 8](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0/html/migration_guide/)
- [Guía de actualización de Adobe Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html?lang=es)
- [AEM está instalando Service Packs](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=es)

## Información del documento

| Campo | Valor |
|-------|-------|
| Versión del documento | 1.0 |
| Última actualización | Febrero de 2026 |
| Versión de AEM | 6.5 LTS |
| Plataforma de Source | JBoss EAP 7.4 / JDK 11 |
| Plataforma de Target | JBoss EAP 8.x/JDK 21 |
| Sistema operativo | Windows Server |

**Aviso legal:** Adobe, Adobe Experience Manager y AEM son marcas comerciales registradas de Adobe Inc. JBoss y Red Hat son marcas comerciales registradas de Red Hat, Inc.
