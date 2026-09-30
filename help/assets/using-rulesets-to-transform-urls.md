---
title: Uso de conjuntos de reglas para transformar URL
description: Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritas en un lenguaje de script (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin,Developer
feature: Configuration,Rulesets
solution: Experience Manager, Experience Manager Assets
exl-id: 8f005ada-275a-444f-9883-64d847fd9959
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: 9e13e2c2-3788-53ff-a622-b0cb8a3a3622
    internal-label: Rulesets
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%
---
# Uso de conjuntos de reglas para transformar direcciones URL {#using-rulesets-to-transform-urls}

Puede implementar conjuntos de reglas en Dynamic Media para transformar direcciones URL. Los conjuntos de reglas son conjuntos de instrucciones escritas en un lenguaje de script (como JavaScript) que evalúan los datos XML y realizan determinadas acciones si dichos datos cumplen determinadas condiciones. Cada regla consta de al menos una condición y una acción. Una regla evalúa los datos XML con respecto a las condiciones y, si se cumple una condición, toma la acción adecuada. Algunos ejemplos de conjuntos de reglas son los siguientes:

* Agregar un sufijo de tipo MIME. Muchos servicios y sitios web requieren sufijos de imagen, como agregar `.jpg` a una dirección URL.
* Creación de una ruta de carpeta a la URL con fines de optimización del motor de búsqueda.

  Ver [Cómo Adobe Dynamic Media Classic admite SEO](/help/assets/assets/s7_seo.pdf).

* Añadir metadatos a la URL con fines de SEO (optimización del motor de búsqueda).

  Ver [Cómo Adobe Dynamic Media Classic admite SEO](/help/assets/assets/s7_seo.pdf).

* Configuración de la disposición de contenido para almacenar en déclencheur una descarga.
* Simplifique las direcciones URL de plantilla del servicio de imágenes para la personalización. Por ejemplo, convierta `rgb{XX,YY,ZZ}` en el `\redXX\greenYY\blueZZ` listo para RTF

* Solicite la codificación de ciertos caracteres, como `$`, `{` y `}`, y de ciertos caracteres, para su descodificación hacia ImageServer. Por ejemplo, Facebook no funciona bien con direcciones URL que contienen caracteres especiales.

En el contexto de Dynamic Media, los sitios web que utilizan un sistema basado en XML para administrar la información de los recursos pueden cargar archivos XML en Dynamic Media. Puede designar uno de estos archivos como el archivo del conjunto de reglas de preprocesamiento para el servicio de recursos de Dynamic Media. Este archivo reestructura el formato de protocolo de URL estándar para satisfacer la lógica empresarial de los sistemas que se integran con Dynamic Media. Especifique un archivo XML que sirva como ruta de acceso del archivo de definiciones del conjunto de reglas.

>[!CAUTION]
>
>Tenga cuidado al utilizar conjuntos de reglas; pueden evitar que el contenido de Dynamic Media se muestre en el sitio web.

Hay conjuntos de reglas de ejemplo disponibles que pueden ayudarle a crear su propio conjunto de reglas.
Consulte [Referencia del conjunto de reglas](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html).

Al igual que con toda la creación de conjuntos de reglas, asegúrese de que el archivo XML es válido antes de cargarlo mediante un programa de validación XML como xmlvalid.

Además, asegúrese de probar primero el conjunto de reglas en un entorno de ensayo que no afecte al entorno de producción en directo.
Los entornos de producción y los entornos de ensayo suelen requerir distintos inicios de sesión.

Consulte la [aplicación de escritorio de Adobe Dynamic Media Classic para obtener información de inicio de sesión](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

<!--
OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)
-->

**Para implementar conjuntos de reglas XML:**

1. Inicie sesión en [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Adobe proporcionó sus credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con Asistencia al cliente de Adobe.

1. Cargue el archivo del conjunto de reglas haciendo lo siguiente:

   * En la barra de navegación global, seleccione **[!UICONTROL Cargar]**.
   * En la página **[!UICONTROL Cargar]**, cerca de la esquina superior izquierda, seleccione **[!UICONTROL Examinar]**.
   * En el cuadro de diálogo **[!UICONTROL Abrir]**, busque el archivo de conjunto de reglas (XML).
   * Seleccione el archivo y luego seleccione **[!UICONTROL Abrir]**.
   * En el lado derecho de la página **[!UICONTROL Cargar]**, seleccione una carpeta de destino para el archivo del conjunto de reglas.
   * Cerca de la parte inferior de la página, asegúrese de marcar **[!UICONTROL Publicar después de cargar]**.
   * En la esquina inferior derecha de la página, seleccione **[!UICONTROL Cargar envío]**.
   * En la barra de navegación global, seleccione **[!UICONTROL Jobs]** para comprobar el estado del trabajo de carga. Cuando la columna **[!UICONTROL Estado]** de la página **[!UICONTROL Trabajo]** indique Carga finalizada, continúe con los siguientes pasos.

1. En la barra de navegación cerca de la parte superior de la página, seleccione **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**.
1. En la página **[!UICONTROL Servidor de imágenes: publicar]**, en el grupo **[!UICONTROL Administración de catálogos]**, busque **[!UICONTROL Ruta del archivo de definición de conjunto de reglas]** y, a continuación, seleccione **[!UICONTROL Seleccionar]**.
1. En la página **[!UICONTROL Seleccionar archivo de definición de conjunto de reglas (XML)]**, busque el archivo de conjunto de reglas y, en la esquina inferior derecha de la página, seleccione **[!UICONTROL Seleccionar]**.
1. En la esquina inferior derecha de la página Configuración, seleccione **[!UICONTROL Cerrar]**.
1. Ejecute un trabajo de publicación del servidor de imágenes.

   Las condiciones del conjunto de reglas se aplican a las solicitudes enviadas a los servidores de imágenes de Dynamic Media activos.

   Si cambia el archivo del conjunto de reglas, los cambios se aplican inmediatamente al volver a cargar y publicar el archivo del conjunto de reglas actualizado.
