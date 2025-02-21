---
title: Visualizar el avatar del usuario
description: Cómo personalizar AEM Forms Workspace para visualizar la imagen de un usuario que ha iniciado sesión.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%

---

# Visualizar el avatar del usuario {#displaying-the-user-avatar}

El avatar del usuario que haya iniciado sesión se mostrará en la esquina superior derecha de AEM Forms Workspace. Además, los avatares de los informes directos de la jerarquía organizativa se mostrarán en la vista Administrador. Puede configurar AEM Forms Workspace para que elija las imágenes de usuario de la base de datos, por ejemplo, del servidor LDAP.

>[!NOTE]
>
>La relación de aspecto admitida en las imágenes del usuario es de 1:1.

1. Cree un DSC con los detalles mencionados en el siguiente paso. Para obtener más información, consulte el tema “Desarrollar componentes para AEM Forms” en la guía [Programar con AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).
1. En el DSC, defina un nuevo SPI que exponga los métodos getCurrentUserImageUrl y getUserImageUrl para obtener una URL de imagen para un usuario de AEM Forms. A continuación se muestra un ejemplo de un fragmento de código Java™:

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. Cree un archivo component.xml. Asegúrese de que spec-id se muestre en el siguiente fragmento de código.

   El siguiente fragmento de código es un ejemplo. Personalícelo para adaptarlo a sus necesidades específicas.

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Implementar DSC a través de Workbench. Reiniciar el servicio `ProcessManagementClientSessionService`.
1. Es posible que tenga que actualizar su explorador o cerrar la sesión/iniciar sesión con el usuario de nuevo.
