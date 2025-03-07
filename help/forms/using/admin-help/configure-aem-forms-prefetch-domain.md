---
title: Configuración de formularios AEM para recuperar previamente información de dominio
description: Configure los formularios de AEM para recuperar previamente información de dominio si experimenta un tiempo de respuesta más lento debido a grupos profundamente anidados o si es miembro de muchos grupos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 61328a32-d014-4a90-b142-169f4f73b35f
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Configuración de formularios AEM para recuperar previamente información de dominio {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Los usuarios pueden experimentar un tiempo de respuesta más lento si pertenecen a muchos grupos (por ejemplo, 500 o más) o si los grupos están profundamente anidados (por ejemplo, 30 niveles). Si tiene este problema, puede configurar los formularios de AEM para que recuperen previamente información de ciertos dominios.

1. En la consola de administración, haga clic en **[!UICONTROL Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración]**.
1. Para exportar la configuración actual a un archivo, haga clic en **[!UICONTROL Exportar]** y guarde el archivo de configuración en otra ubicación.
1. Añada el siguiente nodo (marcado en negrita):

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   En este ejemplo, se configuran varios dominios para la recuperación previa. Los nombres de dominio están separados por &quot;/&quot;. Esto se muestra en el ejemplo anterior con *Domain_Name1*, *Domain_Name2* y *Domain_Name3*.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en **[!UICONTROL Configuración > Importar y exportar archivos de configuración]**.
1. Haga clic en **[!UICONTROL Examinar]** para buscar el archivo, haga clic en Importar y, a continuación, en **[!UICONTROL Aceptar]**.
