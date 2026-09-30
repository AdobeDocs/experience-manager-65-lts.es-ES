---
title: Configuración del conector para IBM&reg; Content Manager
description: Configure el conector para IBM&reg; Content Manager para permitir la comunicación entre los formularios de AEM y IBM&reg; Content Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 106f01a2-39fb-474b-8c58-5ab08666b918
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%
---
# Configuración del conector para el administrador de contenido de IBM®{#configuring-connector-for-ibm-content-manager}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

El conector para el administrador de contenido de IBM® permite la comunicación entre los formularios de AEM y el administrador de contenido de IBM®. Para obtener información adicional, consulte &quot;Conectores para ECM&quot; en [Referencia de servicios](https://www.adobe.com/go/learn_aemforms_services_63).

## Configuración de la conexión de IBM® Content Manager {#configure-the-ibm-content-manager-connection}

1. En la consola de administración, haga clic en Servicios > Conector para IBM® Content Manager.
1. En el cuadro Nombre del almacén de datos, escriba el nombre del almacén de datos de IBM® Content Manager al que desea conectarse. Si la base de datos es local, escriba el nombre de la base de datos. Si la base de datos es remota, escriba su nombre de alias.
1. En el cuadro Nombre de usuario, escriba el ID de usuario de un usuario que se va a conectar al almacén de datos de IBM® Content Manager.
1. En el cuadro Contraseña, escriba la contraseña del usuario.
1. (Opcional) En el cuadro Cadena de conexión de alias, escriba argumentos de conexión adicionales. Normalmente, esta casilla debe estar vacía. Para obtener más información, consulte la documentación de IBM®.
1. Haga clic en Guardar.

## Validación de la configuración del servicio {#validation-of-service-settings}

Si introduce un alias, un nombre de usuario o una contraseña de dataStore incorrectos, obtendrá los siguientes resultados, en función de si se está ejecutando el servicio Conector del repositorio de contenido para IBM® Content Manager:

* Si el servicio está detenido, al guardar la información de configuración del servicio, no aparece ningún error. Sin embargo, la próxima vez que inicie el servicio, se producirá una excepción y el servicio no se iniciará.
* Si se inicia el servicio, al guardar la información de configuración del servicio, el servicio intenta validar la información de credenciales inmediatamente. En este caso, se produce un error y la información de configuración no se guarda.
