---
title: Configurar la seguridad
description: Obtenga información sobre cómo establecer la configuración de seguridad. Puede proteger los documentos de PDF limitando el acceso. Puede cifrar, certificar o proteger el documento con contraseña.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator,Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: fee34d9e-6606-40c1-bbbe-e7975ad90a22
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# Configurar la seguridad{#configuring-security-settings}

Puede limitar el acceso a los documentos de PDF estableciendo contraseñas y restringiendo determinadas funciones, como la impresión y la edición. Cuando un documento de PDF tiene funciones restringidas, las herramientas y los elementos de menú relacionados con esas funciones se atenúan. También puede utilizar otros métodos para crear documentos seguros, como cifrar o certificar un documento. Una configuración de seguridad contiene la contraseña y opciones específicas que se deben utilizar para determinadas conversiones de PDF.

En la página Configuración de seguridad, puede realizar las siguientes tareas:

## Crear o editar una configuración de seguridad {#create-or-edit-a-security-setting}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Una configuración de seguridad *1&rbrace; controla la seguridad y los permisos de los archivos convertidos con esa configuración de seguridad.*

1. En la consola de administración, haga clic en Servicios > PDF Generator > Configuración de seguridad.
1. Haga clic en Nuevo o en el nombre de una configuración de seguridad.
1. En la página Nueva/Editar configuración de seguridad, complete la información necesaria para la configuración de seguridad. (Consulte [Configuración del tipo de archivo](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Haga clic en Guardar y, en el cuadro de diálogo que aparece, escriba un nombre para la configuración y, a continuación, haga clic en Aceptar.

### Configuración de seguridad {#security-settings}

Estas opciones configuran la compatibilidad y el cifrado. Para obtener instrucciones sobre cómo obtener acceso a la configuración de fuentes, vea [Crear o editar una configuración de seguridad](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilidad:** Establece el tipo de cifrado para abrir un documento protegido con contraseña. La opción Acrobat 3.0 y posterior utiliza un nivel de cifrado bajo, pero las demás opciones utilizan un nivel de cifrado alto:

**Acrobat 3.0 y posterior:** utiliza cifrado bajo (RC4 de 40 bits).

**Acrobat 5.0 y posterior:** utiliza cifrado alto (RC4 de 128 bits).

**Acrobat 6.0 y posterior:** utiliza cifrado alto (RC4 de 128 bits). Esta opción permite habilitar la búsqueda de metadatos.

**Acrobat 7.0 y posterior:** utiliza cifrado alto (AES de 128 bits). Esta opción permite habilitar los metadatos para buscar y cifrar solo los archivos adjuntos.

**Acrobat 9.0 y posterior:** utiliza cifrado alto (AES de 256 bits). Esta opción permite habilitar los metadatos para buscar y cifrar solo los archivos adjuntos.

Una versión anterior de Acrobat no puede abrir un documento de PDF que tenga una configuración de compatibilidad más alta. Por ejemplo, si selecciona la opción Acrobat 7.0 And later, no podrá abrir el documento en Acrobat 6.0 o anterior.

Asegúrese de que el nivel de compatibilidad es coherente con el nivel de compatibilidad de PDF para la misma fuente. Por ejemplo, si tiene una carpeta vigilada configurada para utilizar la configuración de PDF estándar, que es compatible con Acrobat 5.0 o posterior, su nivel de compatibilidad de seguridad no debe ser superior a Acrobat 5.0.

**Restricción de documento:** Las restricciones de documento disponibles dependen de la opción de compatibilidad seleccionada.

**Sin cifrado:** No cifra ninguna parte del documento.

**Cifrar todo el contenido del documento:** Cifra el documento y los metadatos del documento. Cuando se selecciona esta opción, los motores de búsqueda no pueden acceder a los metadatos del documento.

**Cifrar todo el contenido del documento excepto los metadatos (Acrobat
6 y posterior (compatible):** codifica el contenido de un documento, pero sigue permitiendo a los motores de búsqueda acceder a los metadatos del documento. Esta opción solo está disponible cuando la opción Compatibilidad está establecida en Acrobat 6.0 o posterior, Acrobat 7.0 o posterior, o Acrobat 9.0 o posterior.

**Cifrar Solo Los Archivos Adjuntos (Acrobat 7 Y Posteriores)
Compatible):** Los usuarios pueden abrir el documento sin contraseña, pero deben escribir una contraseña para abrir los archivos adjuntos. Esta opción solo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior, o en Acrobat 9.0 o posterior.

Esta configuración configura la seguridad de contraseña:

>[!NOTE]
>
>Si olvida una contraseña, no se podrá recuperar del documento. Se recomienda almacenar las contraseñas en otra ubicación segura en caso de que las olvide. Además, mantenga una copia de seguridad del documento que no esté protegida con contraseña.

**Requerir Una Contraseña Para Abrir El Documento:** Habilita las opciones de contraseña.

**Contraseña para abrir el documento:** Impide que los usuarios abran el documento a menos que escriban la contraseña especificada. Las contraseñas distinguen entre mayúsculas y minúsculas. Acrobat utiliza el método de seguridad RC4 de RSA Security Inc. para proteger los documentos de PDF con contraseña. Si restringe la impresión y edición, se recomienda agregar una contraseña de apertura de documento para mejorar la seguridad.

**Contraseña para abrir documentos de Retype:** Garantiza que la contraseña para abrir documentos es correcta.

**Requerir Una Contraseña Para Abrir Archivos Adjuntos:** Activa las opciones de contraseña. Esta opción sólo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior, o en Acrobat 9.0 o posterior, y la opción Restricción de documento está establecida en Cifrar sólo archivos adjuntos.

**Contraseña para abrir archivos adjuntos:** Garantiza que se requiere una contraseña para abrir un archivo adjunto. Los usuarios pueden abrir el documento sin contraseña. Esta opción sólo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior, o en Acrobat 9.0 o posterior, y la opción Restricción de documento está establecida en Cifrar sólo archivos adjuntos.

**Archivo adjunto de Retype:** Garantiza que la contraseña sea correcta. Esta opción sólo está disponible cuando la opción Compatibilidad está establecida en Acrobat 7.0 o posterior, o en Acrobat 9.0 o posterior, y la opción Restricción de documento está establecida en Cifrar sólo archivos adjuntos.

Estas opciones configuran los permisos:

**Usar Una Contraseña Para Restringir La Impresión Y Edición De
El documento y su configuración de seguridad:** habilita las restricciones de permisos.

**Contraseña de permisos:** Restringe a los usuarios de la impresión y edición. Los usuarios no pueden cambiar esta configuración de seguridad a menos que escriban la contraseña especificada. No puede utilizar la misma contraseña que se utiliza para Contraseña de apertura de documento. Cuando establece una contraseña de permisos, sólo las personas que escriben esa contraseña pueden cambiar la configuración de seguridad. Si el documento de PDF tiene ambos tipos de contraseñas, cualquiera de ellas la abrirá. Sin embargo, un usuario solo puede establecer o cambiar las funciones restringidas con la contraseña de permisos. Si el documento de PDF sólo tiene la contraseña de permiso o si un usuario abre el documento utilizando la contraseña de apertura del documento, la solicitud de contraseña aparece cuando el usuario intenta cambiar la configuración de seguridad.

**Contraseña de permisos de Retype:** Garantiza que la contraseña de permisos sea correcta.

**Impresión permitida:** Especifica la calidad de impresión del documento de PDF:

**Ninguno:** impide que los usuarios impriman el documento.

**Baja resolución (150 ppp):** Permite a los usuarios imprimir el documento con una resolución no superior a 150 ppp. La impresión puede ser más lenta porque cada página se imprime como imagen de mapa de bits. Esta opción solo está disponible si se selecciona un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Alta resolución:** Permite a los usuarios imprimir a cualquier resolución, dirigiendo la salida vectorial de alta calidad a PostScript y otras impresoras que admiten características de impresión avanzadas de alta calidad.

**Cambios permitidos:** define qué acciones de edición se permiten en el documento de PDF:

**Ninguno:** Impide que los usuarios cambien el documento, incluidos los campos de formulario y de firma.

**Insertar, eliminar y rotar páginas:** Permite a los usuarios insertar, eliminar y rotar páginas y crear marcadores y páginas de miniaturas. Esta opción solo está disponible si se selecciona un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Rellenar Campos De Formulario Y Firmar Firma Existente
Campos:** Permite que los usuarios rellenen formularios y agreguen firmas digitales. Sin embargo, los usuarios no pueden agregar comentarios ni crear campos de formulario. Esta opción solo está disponible si se selecciona un nivel de cifrado alto (Acrobat 5.0, 6.0, 7.0 o 9.0).

**Comentar, Rellenar Campos De Formulario Y Firmar Los Existentes
Campos de firma:** permite a los usuarios rellenar formularios y agregar firmas digitales y comentarios.

**Diseño De Página, Retoque, Rellenado De Campos De Formulario Y Firma
Campos de firma existentes:** permite a los usuarios insertar, rotar o eliminar páginas y crear marcadores o imágenes en miniatura, rellenar formularios y agregar firmas digitales. Esta opción no permite a los usuarios crear campos de formulario. Esta opción solo está disponible si se selecciona un nivel de cifrado bajo (Acrobat 3.0).

**Cualquiera excepto Extraer páginas:** Permite a los usuarios cambiar el documento utilizando cualquier método en la Lista de permitidos Cambios, excepto quitar páginas.

**Habilitar la copia de texto, imágenes y otro contenido:** Permite a los usuarios seleccionar y copiar el contenido del documento de PDF. También permite a las utilidades que necesitan acceder al contenido de un archivo PDF, como Acrobat Catalog, acceder a dicho contenido. Esta opción solo está disponible si se selecciona un nivel de cifrado alto.

**Habilitar El Acceso De Texto De Los Dispositivos Reader De Pantalla Para
Con deficiencias visuales:** permite a los usuarios con deficiencias visuales leer el documento usando lectores de pantalla. Sin embargo, los usuarios no pueden copiar ni extraer el contenido del documento. Esta opción solo está disponible si se selecciona un nivel de cifrado alto.

## Eliminar una configuración de seguridad {#delete-a-security-setting}

Puede eliminar una configuración de seguridad si ya no es necesaria. Sin embargo, no se puede eliminar la configuración de seguridad preconfigurada.

1. En la consola de administración, haga clic en **[!UICONTROL Servicios > PDF Generator > Configuración de seguridad]**.
1. Seleccione la casilla de verificación situada junto a la configuración que desea eliminar. Puede seleccionar varias configuraciones.
1. Haga clic en **[!UICONTROL Eliminar]** y en la página **[!UICONTROL Confirmación de eliminación]**, vuelva a hacer clic en **[!UICONTROL Eliminar]**.
