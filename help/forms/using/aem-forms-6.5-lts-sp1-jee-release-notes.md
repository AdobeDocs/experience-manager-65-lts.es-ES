---
title: Notas de la versión para  [!DNL Adobe Experience Manager] 6.5 LTS SP1
description: Encuentre información de la versión, novedades, instrucciones de instalación y una lista de cambios detallada para  [!DNL Adobe Experience Manager] 6.5 LTS SP1
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 811fccbc-6f63-4309-93c8-13b7ace07925
source-git-commit: c13c6c3d5511a5355570e999e378e4bdf0d7a88f
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 3%

---


# Notas de la versión de Adobe Experience Manager (AEM) Forms 6.5 LTS SP1 en JEE

## Información de la versión

| **Producto** | Adobe Experience Manager Forms |
| -------------------- | ------------------------------------ |
| **Versión** | SP1 DE 6,5 LTS |
| **Tipo** | Paquete de servicio de soporte a largo plazo (JEE) |
| **Categoría de versión** | Versión de actualización |
| **URL de descarga** | Distribución de software |

## Qué se incluye en [!DNL Experience Manager] 6.5 LTS SP1 {#what-is-included-in-aem-65ltssp1}

Adobe Experience Manager (AEM) Forms **6.5 LTS SP1 en JEE** ofrece nuevas características, actualizaciones clave de la plataforma solicitadas por el cliente y correcciones generales de errores, con un fuerte enfoque en la estabilidad del producto y soporte a largo plazo.

## Qué se incluye en AEM Forms 6.5 LTS SP1

### &#x200B;1. Actualizaciones de soporte de Java

Se ha introducido la compatibilidad con las versiones más recientes de Java:

* **Java™ 17**
* **Java™ 21**

### &#x200B;2. Actualizaciones de soporte del servidor de aplicaciones

#### Compatibilidad con JBoss EAP 8

* Se ha agregado compatibilidad con **JBoss EAP 8**.
* Se ha eliminado el marco de seguridad heredado **PicketBox**.
* **Ahora se admiten almacenes de credenciales basados en Elytron** para la administración segura de credenciales.

##### Configuración: almacén de credenciales (basado en Elytron)

AEM Forms en JBoss EAP 8 usa Elytron para administrar credenciales seguras. Los clientes deben configurar un almacén de credenciales basado en Elytron para garantizar el inicio correcto del servidor y la autenticación segura de la base de datos.

Para obtener más información, consulte la guía de instalación y configuración.

### &#x200B;3. Cambios de plataforma y compatibilidad

#### Compatibilidad con especificaciones de servlet

* Compatibilidad con **Especificación de servlet 5+**
* Basado en el cumplimiento de **Jakarta EE 9**

#### Requisito de migración del área de nombres

* Jakarta EE 9 introduce un cambio de área de nombres de `javax.*` a `jakarta.*`
* Todos los **DSC personalizados** deben migrarse al área de nombres `jakarta.*`
* AEM Forms 6.5 LTS SP1 solo admite **servidores de aplicaciones basados en Jakarta EE 9+**

Para obtener más información, consulte **Migración de javax a jakarta Namespace**.

## Actualizar

Para obtener instrucciones de actualización detalladas, consulte la [Guía de actualización para AEM Forms 6.5 LTS SP1 en JEE](https://experienceleague.adobe.com/en/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)

## Instalación

Para ver los pasos y requisitos previos de la instalación, consulte la **Guía de instalación de AEM Forms 6.5 LTS SP1 (JEE)**.

## Plataformas compatibles

Para obtener la lista completa de plataformas compatibles, sistemas operativos, bases de datos y servidores de aplicaciones, consulte:

**Matriz de plataformas admitidas - AEM Forms 6.5 LTS SP1 (JEE)**

## Funciones en desuso y eliminadas

* Se ha eliminado la compatibilidad con **RDBMK** para la persistencia del repositorio de CRX.
* Para entornos agrupados, **solo MongoMK** es compatible con la persistencia del repositorio.

## Migración de javax a yakarta Namespace

### Migración de `javax` a `jakarta` área de nombres

A partir de **AEM Forms 6.5 LTS SP1**, solo se admiten los servidores de aplicaciones que implementan **Jakarta Servlet API 5/6**. Con **Jakarta EE 9 y versiones posteriores**, todas las API pasaron del área de nombres `javax.{}` a `jakarta.`.

Como resultado, **todos los DSC personalizados deben usar el espacio de nombres `jakarta`**. Los componentes personalizados creados con las API `javax.{}` son **no compatibles** con los servidores de aplicaciones compatibles.

### Opciones de migración para DSC personalizados

Puede migrar los DSC personalizados existentes mediante uno de los siguientes métodos:

#### Opción 1: Migración De Código Source (Recomendada)

* Actualizar todas las instrucciones de importación de `javax.{}` a `jakarta.`
* Reconstruir y volver a compilar los proyectos de DSC personalizados
* Volver a implementar los componentes actualizados en el servidor de aplicaciones

**Ventajas:**

* Garantiza la compatibilidad a largo plazo con Jakarta EE 9+
* Más adecuado para proyectos mantenidos activamente

#### Opción 2: Migración Binaria Mediante El Transformador Eclipse

* Use la herramienta **Transformador Eclipse** para convertir binarios compilados (`.jar`, `.war`) de `javax` a `jakarta`
* No se requieren cambios ni recompilación del código fuente
* Volver a implementar los binarios transformados en el servidor de aplicaciones

>[!NOTE]
>
> La transformación binaria se realiza en el **nivel de código de bytes**.

Asignaciones de importación de muestra

A continuación, se muestran ejemplos comunes de cambios en el área de nombres necesarios durante la migración:

Antes (javax)    Después (yakarta)
javax.servlet.*    jakarta.servlet.*
javax.servlet.http.*    jakarta.servlet.http.*

### Asignaciones de importación de muestra

La tabla siguiente muestra los cambios comunes de área de nombres necesarios al migrar de `javax` a `jakarta`:

| Antes de (`javax`) | Después de (`jakarta`) |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

Utilice estas asignaciones como referencia al actualizar el código fuente DSC personalizado o al validar binarios transformados.

