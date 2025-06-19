---
title: Integración de [!DNL Experience Manager Assets] con  [!DNL Adobe Workfront]
description: Introducción a la integración entre  [!DNL Assets] y [!DNL Workfront]
role: Admin,Leader,Architect
feature: Workfront Integrations and Apps
hide: true
solution: Experience Manager, Workfront
exl-id: 5181d278-2e6e-41f7-891e-1067a03de016
source-git-commit: b8576049fba41b3bec16046316938274a5046513
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 4%

---

# Integración de [!DNL Adobe Experience Manager Assets] con [!DNL Adobe Workfront] {#assets-integration-overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/integrations/workfront-integrations.html?lang=es) |
| AEM 6.5 | Este artículo |

[!DNL Adobe Workfront] es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad del contenido y el tiempo de salida al mercado, conectando intrínsecamente el trabajo con la administración de recursos digitales. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios.

[!DNL Workfront for Experience Manager enhanced connector] habilita procesos empresariales mejorados con flujos de trabajo de un extremo a otro, y proporciona experiencias de cliente de un extremo a otro personalizadas y almacenamiento central. Adobe ofrece un conector estándar y un conector mejorado para integrar las dos soluciones. Vea las funciones admitidas a continuación para ver una comparación y vea [las novedades de [!DNL enhanced connector]](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

[!DNL Workfront for Experience Manage enhanced connector] permite a su organización:

* Cree automáticamente carpetas de Experience Manager vinculadas en Workfront y organice las carpetas en función de Portafolios, Programas y Proyectos de Workfront.
* Sincronice los metadatos de proyecto de Workfront con las carpetas de Experience Manager vinculadas.
* Experience Manager actualiza los metadatos con nuevas versiones.
* Establezca los estados de objetos de Workfront en función de condiciones configurables mediante flujos de trabajo de Experience Manager.
* Publique recursos en el entorno de publicación de Experience Manager o en Brand Portal.

Consulte los [requisitos previos y compatibilidad con la plataforma para el conector mejorado](https://one.workfront.com/s/csh?context=2467&pubname=the-new-workfront-experience).

>[!IMPORTANT]
>
>* Adobe requiere la implementación y configuración de [!DNL Adobe Workfront for Experience Manager enhanced connector] solo a través de socios certificados o [!DNL Adobe Professional Services]. Si se implementa y se configura sin un socio certificado o [!DNL Adobe Professional Services], no es compatible con Adobe.
>
>* Adobe puede publicar actualizaciones para [!DNL Adobe Workfront] y [!DNL Adobe Experience Manager] que hagan redundante este conector; si esto sucede, es posible que los clientes deban realizar la transición desde el uso de este conector.
>
>* Adobe admite las versiones 1.7.4 y posteriores del conector mejorado. No se admiten versiones preliminares ni versiones personalizadas anteriores. Para comprobar la versión mejorada del conector, vaya al grupo `digital.hoodoo` disponible en el panel izquierdo de [Administrador de paquetes](/help/sites-administering/package-manager.md).
>
>* Consulte [Examen de certificación de socio para el conector mejorado de Workfront para Experience Manager Assets](https://solutionpartners.adobe.com/solution-partners/home/applications/experience_cloud/workfront/journey/dev_core.html). Para obtener información sobre el examen, consulte [Guía para exámenes](https://express.adobe.com/page/Tc7Mq6zLbPFy8/).

## Comparar diferentes integraciones entre [!DNL Assets] y [!DNL Workfront] {#feature-parity-matrix}

A continuación se muestran los detalles de las funcionalidades disponibles a través de varios tipos de integraciones entre [!DNL Assets] y [!DNL Workfront].

| Función | Descripción | [!DNL Workfront] y [!DNL Assets Essentials] *Sin conector (predeterminado)* | [!DNL Workfront for Experience Manager enhanced connector] *Requiere Conector* | Workfront y [!DNL Experience Manager as a Cloud Service] *Sin conector (predeterminado)* |
|----|----|----|-----|-----|
| Métodos de implementación | Apropiado para la oferta [!DNL Assets]. | Assets Essentials | Adobe Managed Services, On-Premise | Cloud Service |
| **General** |
| Enviar archivos digitales de [!DNL Workfront] a [!DNL Assets] | La última versión de un documento WF se puede cargar a los AEM Assets, que está vinculado como una nueva versión del documento. | ✓ | ✓ | ✓ |
| Vincular manualmente carpetas de AEM a objetos de Workfront | Las carpetas de AEM existentes se pueden vincular como una carpeta de Workfront y sus recursos secundarios se vinculan como nuevos documentos de Workfront. | ✓ | ✓ | ✓ |
| Vincular [!DNL Assets] a objetos de Workfront | Los recursos existentes en AEM se pueden vincular a un nuevo documento de Workfront o como una nueva versión de un documento existente. | ✓ | ✓ | ✓ |
| Los Assets agregados a las carpetas vinculadas se envían automáticamente a AEM | Si se agrega el documento a una carpeta vinculada, el recurso asociado se cargará automáticamente en AEM Assets como un nuevo recurso. | ✓ | ✓ | ✓ |
| Descarga de AEM Assets vinculados desde Workfront | Cuando un recurso está vinculado en Workfront, el usuario puede descargar los bytes del recurso. | ✓ | ✓ | ✓ |
| Buscar AEM Assets desde Workfront | El selector AEM Assets de Workfront permite búsquedas de texto completo para recursos. | ✓ | ✓ | ✓ |
| Buscar carpetas de AEM desde Workfront | El selector de AEM Assets de Workfront permite búsquedas de texto completo en carpetas. | ✓ | ✓ | ✓ |
| Ver y navegar por la jerarquía de carpetas de AEM desde Workfront | El selector AEM Assets de Workfront permite explorar la jerarquía de AEM Assets limitada por el   los controles de acceso y permisos asociados del usuario establecidos en AEM. | ✓ | ✓ | ✓ |
| Seguimiento de versiones de recursos en cronologías de AEM | Mantener el historial de versiones del documento entre Workfront y AEM. | ✓ | ✓ | ✓ |
| Desvincular Assets de los AEM Assets en Workfront | Un recurso vinculado existente de AEM se puede desvincular del documento de Workfront asociado. Esto no elimina el recurso original dentro de AEM. | ✓ | ✓ | ✓ |
| Añadir recursos de las últimas versiones a los AEM Assets desde Workfront | Cuando se agrega una versión recién agregada a un documento en Workfront, un usuario puede enviar la nueva versión a AEM para reemplazar la versión existente. | ✓ | ✓ | ✓ |
| Assets se vinculó en Workfront al hacer clic en el usuario directo en AEM | Los usuarios se dirigen a AEM para obtener una vista previa de un recurso vinculado desde Workfront. | ✓ | ✓ | Próximamente |
| Crear automáticamente carpetas de AEM vinculadas en Workfront | Cree automáticamente carpetas de AEM vinculadas en Workfront mediante los estados de proyecto. Configure automáticamente carpetas de AEM basadas en Portafolios, Programas y Proyectos de Workfront. | No | ✓ | No |
| Vaya directamente a los repositorios de AEM desde Workfront | Permite que los usuarios naveguen a repositorios de AEM disponibles configurados en Workfront. | ✓ | No | ✓ |
| Creación de carpetas de AEM vinculadas en Workfront | Cree manualmente carpetas de AEM vinculadas en Workfront mediante la opción disponible en la pestaña Documentos. | ✓ | No | ✓ |
| Sincronización de comentarios | Sincronizar automáticamente los comentarios de los recursos de [!DNL Workfront] a [!DNL Assets] | No | ✓ | No |
| Admitir varios entornos de Workfront que se conecten a un solo entorno de AEM | Los usuarios de varios entornos de Workfront pueden conectarse a un único entorno de AEM. | ✓ | No | ✓ |
| Admitir varios entornos de AEM que se conecten a un solo entorno de Workfront | Los usuarios dentro de un solo entorno de Workfront pueden enviar o vincular recursos entre varios entornos de AEM. | ✓ | ✓ | ✓ |
| **Metadatos** |
| Asignación de metadatos de recursos Workfront a los AEM Assets | Las propiedades de objeto de Workfront y formulario personalizado se pueden asignar a las propiedades de metadatos de recursos de AEM. Los valores se insertan en la carga o el vínculo inicial. | ✓ | ✓ | ✓ |
| Crear automáticamente un documento de Forms personalizado en Workfront | Adjuntar formularios personalizados a documentos, tareas y problemas de Workfront mediante flujos de trabajo de AEM. | No | ✓ | No |
| Actualización automática bidireccional de metadatos entre AEM Assets y Workfront | Actualizar automáticamente los metadatos entre AEM Assets y Workfront. El recurso debe insertarse inicialmente desde Workfront a AEM y los metadatos del recurso de Workfront deben asignarse a los recursos de AEM para que las actualizaciones de metadatos bidireccionales funcionen correctamente. | No | ✓ | No |
| Vista en tiempo real en Workfront para metadatos asignados a AEM | Vea los metadatos asignados actualizados a AEM en los paneles Detalles del documento de Workfront y Resumen del documento. | ✓ | No | ✓ |
| Inserción en tiempo real de metadatos de Workfront actualizados en AEM | Actualice automáticamente los metadatos de Workfront asignados a AEM sin volver a cargar un recurso o una nueva versión de un recurso. | ✓ | No | ✓ |
| Asignar metadatos de Workfront a las carpetas de los AEM Assets | Sincronizar metadatos de proyecto de Workfront con carpetas de AEM vinculadas. | No | ✓ | ✓ |
| Actualizaciones de metadatos de AEM con nuevas versiones | Se puede realizar una configuración en AEM para determinar si un recurso con una nueva versión en Workfront también inserta cambios en sus metadatos. | No | ✓ | No |
| Actualizar automáticamente metadatos de AEM sobre los cambios en Forms personalizado en Workfront | AEM permite suscribirse a las actualizaciones de los formularios de documentos en Workfront. Como resultado, cualquier actualización de los metadatos de formulario personalizados del documento de Workfront edita los valores de los campos de metadatos de AEM asignados. | No | ✓ | No |
| **Flujos de trabajo (predeterminados)** |
| Crear nueva versión de revisión en Assets vinculado | Al vincular un recurso en Workfront, se puede generar una prueba automáticamente. | No | Personalizado | No |
| Definir estado en objetos de Workfront | Definición de estados de objetos de Workfront basados en condiciones configurables mediante flujos de trabajo de AEM | No | ✓ | Próximamente |
| Publicar Assets en el entorno de publicación de AEM o Brand Portal | Dé a los usuarios de Workfront la opción de publicar automáticamente los recursos vinculados en un entorno de publicación de AEM o Brand Portal. | No | ✓ | Próximamente |
