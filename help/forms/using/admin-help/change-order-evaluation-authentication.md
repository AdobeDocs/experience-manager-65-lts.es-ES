---
title: Cambiar el orden de evaluación para la autenticación
description: Puede cambiar el orden en que los formularios AEM Forms evalúan varios proveedores de autenticación.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 8%

---

# Cambiar el orden de evaluación para la autenticación {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Si ha configurado varios proveedores de autenticación, puede cambiar el orden en que los formularios AEM Forms los evalúan para la autenticación. El orden de los proveedores de autenticación que se enumeran en el archivo config.xml determina el orden de evaluación para la autenticación.

1. En la consola de administración, haga clic en Configuración > Administración de usuarios > Configuración > Importar y exportar archivos de configuración.
1. Para exportar la configuración actual a un archivo, haga clic en Exportar y guarde el archivo de configuración en otra ubicación.
1. Busque el siguiente nodo en el archivo:

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   En `<entry key="order" value="3" />`, edite el valor de cada nodo para establecer el orden de la evaluación de autenticación.

1. Para importar el archivo actualizado, en Administración de usuarios, haga clic en Configuración > Importar y exportar archivos de configuración.
1. Haga clic en Examinar para buscar el archivo, en Importar y, a continuación, en Aceptar.
