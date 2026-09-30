---
title: Importar y exportar archivos de configuración
description: Obtenga información sobre cómo importar y exportar el archivo de configuración para editar las preferencias del servidor o configurar otra instancia de producto de formularios AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 92fdcee3-2007-4bbc-be4b-426d65b8dbc1
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
source-wordcount: '264'
ht-degree: 4%
---
# Importar y exportar archivos de configuración {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Utilice la página Configuración Manual para descargar una copia de los ajustes de configuración en formato XML. La configuración de este archivo controla todas las preferencias del servidor. A continuación, puede editar el archivo y cargarlo de nuevo en el servidor. También puede utilizar el archivo para configurar otra instancia de producto de formularios AEM Forms.

Para evitar riesgos de seguridad, el valor de la contraseña de enlace para el servidor de directorios no se incluye en un archivo de configuración exportado. Actualice la contraseña en el archivo XML antes de importar el archivo a un nuevo sistema.

>[!NOTE]
>
>La importación del archivo de configuración reconfigura los formularios de AEM en función de la información del archivo. Solamente un administrador del sistema o un consultor de servicios profesionales familiarizado con el producto de formularios AEM Forms y el XML debe considerar la posibilidad de modificar el archivo de configuración. Es posible que tengan que editar el archivo de configuración, por ejemplo, para volver a configurar una configuración dañada.

**Exportar la información de configuración**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Exportar. Si utiliza Microsoft Internet Explorer, se le pedirá que especifique una ubicación para guardar el archivo. Si utiliza Firefox, el archivo se guardará en el escritorio.

**Importar la información de configuración**

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo de configuración, haga clic en Importar y, a continuación, haga clic en Aceptar.
