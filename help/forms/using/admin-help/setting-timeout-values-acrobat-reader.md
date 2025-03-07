---
title: Configurar valores de tiempo de espera para usarlos con extensiones de Acrobat Reader DC
description: Obtenga información sobre cómo establecer valores de tiempo de espera para utilizarlos con extensiones de Acrobat Reader DC.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: c2f96686-15e3-4d92-acfe-f971c5849de4
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Configurar valores de tiempo de espera para usarlos con extensiones de Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Cuando trabaje con muchos archivos PDF en extensiones de Acrobat Reader DC, asegúrese de que los siguientes valores de tiempo de espera estén correctamente configurados para evitar que los trabajos agoten el tiempo de espera y produzcan errores:

**Tiempo de espera de eliminación de documento**

Este valor se puede establecer en la consola de administración. Haga clic en Configuración > Configuración del sistema principal > Configuraciones y especifique un valor para Tiempo de espera de eliminación de documentos predeterminado.

**Tiempo de espera de formularios AEM del administrador de usuarios:** Este valor se puede establecer editando el archivo config.xml. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración y, a continuación, haga clic en Exportar. Abra el archivo config.xml exportado y edite las siguientes líneas:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Guarde y vuelva a importar el archivo config.xml en la consola de administración.

**Tiempo de espera de sesión del servidor de aplicaciones:** Este valor se puede establecer en el servidor de aplicaciones. Para obtener más información, consulte la documentación proporcionada con el servidor de aplicaciones.
