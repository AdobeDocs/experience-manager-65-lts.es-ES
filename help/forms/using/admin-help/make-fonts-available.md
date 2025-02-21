---
title: Hacer que las fuentes estén disponibles
description: Asegúrese de que las fuentes utilizadas en un formulario estén disponibles para su uso en el servidor de aplicaciones J2EE que aloja los formularios AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# Hacer que las fuentes estén disponibles {#make-fonts-available}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Asegúrese de que las fuentes utilizadas en un formulario estén disponibles para su uso en el servidor de aplicaciones J2EE que aloja los formularios AEM. Por ejemplo, imagine el siguiente escenario. Un diseñador de formularios agrega una fuente al directorio de fuentes que utiliza Designer y crea un formulario que utiliza esa fuente en un equipo independiente. Para que el servicio Output utilice la fuente, colóquela en el directorio de fuentes del cliente. Si el directorio de fuentes del cliente no existe, cree un directorio en el servidor de aplicaciones J2EE que aloje formularios AEM.

Para obtener información sobre la configuración de fuentes adicional, consulte [Configuración general de los formularios de AEM](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Especifique la ubicación del directorio de fuentes del cliente**

1. En la consola de administración, haga clic en Configuración > Configuración de sistemas principales > Configuraciones.
1. En el cuadro Ubicación del directorio de fuentes del sistema, escriba la ruta de acceso al directorio de fuentes del cliente. Se pueden agregar varios directorios separados por punto y coma **;**
1. Haga clic en Aceptar.
1. Reinicie el sistema en el que está instalado AEM Forms.

>[!NOTE]
>
>Las fuentes se seleccionan de la caché de fuentes del sistema de Windows y es necesario reiniciar el sistema para actualizar la caché. Después de especificar el directorio de fuentes de cliente, asegúrese de reiniciar el sistema en el que está instalado AEM forms.
