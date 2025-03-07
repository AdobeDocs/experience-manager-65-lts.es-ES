---
title: Especificar las opciones de configuración XCI
description: Obtenga información sobre cómo especificar las opciones de configuración de XCI. Puede especificar valores de archivo XCI personalizados para el formulario adaptable, de modo que se pueda utilizar durante el procesamiento del formulario.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5fb6e6cc-6af7-4cf5-804b-bb3030079383
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%

---

# Especificar las opciones de configuración XCI {#specify-xci-configuration-options}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

La salida permite especificar un archivo XCI personalizado que utiliza para el procesamiento. Consulte [Especificar ubicaciones de archivos para la salida](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

De forma predeterminada, Output anula algunas de las opciones especificadas en el archivo XCI, incluidas las siguientes:

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Puede seleccionar opciones que cancelen la anulación de las opciones enumeradas anteriormente, en cuyo caso la salida utiliza los valores especificados en el archivo XCI personalizado.

1. En la consola de administración, haga clic en **Servicios** > resultado.
1. Seleccione o anule la selección de la casilla de verificación Usar opciones XCI predeterminadas del sistema. Cuando se selecciona esta opción, Output utiliza sus valores predeterminados para la configuración de paquetes, creator, producer y compressObjectStream. Cuando esta opción no está seleccionada, la salida utiliza los valores especificados en el archivo XCI personalizado.
1. Haga clic en **Guardar**.
