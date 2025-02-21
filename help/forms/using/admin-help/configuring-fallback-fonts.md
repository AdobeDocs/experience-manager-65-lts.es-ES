---
title: Configurar fuentes de reserva
description: Obtenga información sobre cómo configurar fuentes de reserva para AEM Forms. Puede utilizar el archivo FontManagerResources.properties para asignar manualmente las fuentes predeterminadas a las fuentes de reserva.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 2%

---

# Configurar fuentes de reserva {#configuring-fallback-fonts}

Puede configurar manualmente el archivo FontManagerResources.properties para asignar las fuentes predeterminadas de los formularios AEM Forms a una alternativa (o un sustituto) si las fuentes predeterminadas no están disponibles en el servidor. Este archivo de propiedades se encuentra en el archivo adobe-fontmanager.jar.

>[!NOTE]
>
>La configuración de fuentes de reserva también se aplica al servicio de ensamblador.

1. Vaya al archivo adobe-livecycle-*`[appserver]`*.ear en el directorio *`[aem-forms root]`*/configurationManager/export, haga una copia de seguridad y desempaquete el original.
1. Busque el archivo adobe-fontmanager.jar y desempaquételo.
1. Busque el archivo FontManagerResources.properties y ábralo en un editor de texto.
1. Modifique las ubicaciones y los nombres de las fuentes genéricas y de reserva según sea necesario y guarde el archivo.

   Las entradas de fuente del archivo FontManagerResources.properties son relativas al directorio *`[aem-forms root]`*/fonts. Si especifica fuentes que no son fuentes predeterminadas de formularios AEM Forms, debe instalarlas dentro de esta estructura de directorios (en un directorio existente o en uno recién creado).

   >[!NOTE]
   >
   >Si la fuente especificada o la fuente predeterminada no contiene un carácter Unicode específico o si no está disponible, el carácter se toma de una fuente de reserva según la siguiente prioridad:

   * Fuente específica de la configuración regional
   * Fuente ROOT si no se ha definido la configuración regional
   * Fuente genérica, buscada por orden establecido en la tabla de reserva

1. Vuelva a empaquetar el archivo adobe-fontmanager.jar.
1. Vuelva a empaquetar el archivo adobe-livecycle-*`[appserver]`*.ear y, a continuación, vuelva a implementarlo manualmente o ejecutando el Administrador de configuración.

>[!NOTE]
>
>No utilice el Administrador de configuración para volver a empaquetar el archivo adobe-livecycle-`[appserver]`.ear, ya que sobrescribirá las modificaciones con los valores predeterminados de los formularios de AEM.
