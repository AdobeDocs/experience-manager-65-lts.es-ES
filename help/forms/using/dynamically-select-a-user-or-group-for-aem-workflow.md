---
title: Seleccionar dinámicamente un usuario o un grupo para los pasos de los flujos de trabajo centrados en AEM Forms
description: Obtenga información sobre cómo seleccionar un usuario o un grupo para un flujo de trabajo de AEM Forms en tiempo de ejecución.
content-type: troubleshooting
topic-tags: publish
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Document Services
exl-id: b3b3567f-df0a-4a24-849c-dcc0b745de63
source-git-commit: 5995dda0aac101e6c0d506ac5bba786674b0735b
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 60%

---

# Seleccionar dinámicamente un usuario o un grupo para los pasos de los flujos de trabajo centrados en AEM Forms {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

Obtenga información sobre cómo seleccionar un usuario o un grupo para un flujo de trabajo de AEM Forms en tiempo de ejecución.

En las organizaciones grandes, hay requisitos para seleccionar usuarios de forma dinámica para un proceso. por ejemplo, cuando se selecciona un agente de campo para servir a un cliente en función de la proximidad de ese agente al cliente. En este tipo de escenarios, el agente se selecciona dinámicamente.

Asignar tareas y pasos de Adobe Sign de [flujos de trabajo centrados en Forms en OSGi](/help/forms/using/aem-forms-workflow.md) proporciona opciones para seleccionar un usuario de forma dinámica. Puede utilizar paquetes ECMAScript u OSGi para seleccionar un usuario asignado de forma dinámica para el paso Asignar tarea o para seleccionar firmantes para el paso Firmar documento.

## Utilizar ECMAScript para seleccionar un usuario o un grupo de forma dinámica {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript es un lenguaje de script. Se utiliza para scripts del lado del cliente y aplicaciones de servidor. Realice los siguientes pasos para seleccionar un usuario o un grupo de forma dinámica mediante ECMAScript:

1. Abra CRXDE Lite. La URL es `https://'[server]:[port]'/crx/de/index.jsp`. 
1. Cree un archivo con la extensión .ecma en la siguiente ruta. Si la ruta (estructura de nodos) no existe, créela:

   * (Ruta para el paso Asignar tarea) `/apps/fd/dashboard/scripts/participantChooser`
   * (Ruta para el Paso de firma) `/apps/fd/workflow/scripts/adobesign`

1. Agregue ECMAScript que tenga la lógica de seleccionar un usuario dinámicamente al archivo `.ecma`. Haga clic en **[!UICONTROL Guardar todo]**.

   Para ver los scripts de ejemplo, consulte [ECMAScripts de ejemplo para seleccionar dinámicamente un usuario o un grupo](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. Añada el nombre para mostrar del script. Este nombre se muestra en los pasos del flujo de trabajo. Para especificar el nombre:

   1. Expanda el nodo del script, haga clic con el botón secundario en el nodo **`jcr:content`** y haga clic en **[!UICONTROL Mixins]**.
   1. Agregue la propiedad `mix:title` en el cuadro de diálogo Editar mixins y haga clic en **Aceptar**.
   1. Agregue la siguiente propiedad al nodo `jcr:content` del script:

      | Nombre | Tipo | Valor  |
      |--- |--- |--- |
      | `jcr:title` | Cadena | Especifique el nombre del script; por ejemplo, Seleccionar el agente de campo más cercano. Este nombre se muestra en los pasos `Assign Task` y Firmar documento. |

   1. Haga clic en **Guardar todo**. El script está disponible para su selección en los componentes del flujo de trabajo de AEM.

      ![script](assets/script.png)

### ECMAScripts de ejemplo para elegir un usuario o un grupo de forma dinámica {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

El siguiente ejemplo de ECMAScript selecciona dinámicamente un usuario asignado para el paso Asignar tarea. En este script, se selecciona un usuario en función de la ruta de la carga útil. Antes de usar este script, asegúrese de que todos los usuarios mencionados en este existen en AEM. Si los usuarios mencionados en el script no existen en AEM, puede producirse un error durante el proceso relacionado.

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

El siguiente ejemplo de ECMAScript selecciona dinámicamente un usuario asignado para el paso de Adobe Sign. Antes de utilizar el siguiente script, asegúrese de que la información de los usuarios (direcciones de correo electrónico y números de teléfono) que se menciona en este es correcta. Si la información de los usuarios que se menciona en el script es incorrecta, puede producirse un error durante el proceso relacionado.

>[!NOTE]
>
>A la hora de usar ECMAScript para Adobe Sign, el script debe estar en crx-repository en /apps/fd/workflow/scripts/adobesign/ y debe tener una función denominada getAdobeSignRecipients para devolver una lista de usuarios.

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## Usar la interfaz de Java para elegir un usuario o un grupo de forma dinámica {#use-java-interface-to-dynamically-choose-a-user-or-group}

Puede usar la interfaz de Java [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) para elegir un usuario o un grupo de forma dinámica para los pasos de Adobe Sign y Asignar tarea. Puede crear un paquete OSGi que use la interfaz Java [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) e implementarlo en el servidor de AEM Forms. Esto le permitirá seleccionar la opción en los componentes `Assign Task` y Adobe Sign del flujo de trabajo de AEM.

Necesitará los archivos jar del [AEM Forms Client SDK](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases#) y [granite](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) para compilar el código de ejemplo que se muestra a continuación. Agregue estos archivos jar como dependencias externas al proyecto del paquete OSGi. Puede utilizar cualquier IDE de Java para crear un paquete OSGi. El siguiente procedimiento proporciona los pasos para utilizar Eclipse para crear un paquete OSGi:

1. Abra Eclipse IDE. Vaya a **[!UICONTROL Archivo]** > **[!UICONTROL Nuevo proyecto]**.
1. En la pantalla Seleccionar un asistente, seleccione **[!UICONTROL Proyecto Maven]** y haga clic en **[!UICONTROL Siguiente]**.
1. En este nuevo proyecto llamado Maven, mantenga los valores predeterminados y haga clic en **[!UICONTROL Siguiente]**. Seleccione un arquetipo y haga clic en **[!UICONTROL Siguiente]**; por ejemplo, maven-archetype-quickstart. Especifique el **[!UICONTROL ID de grupo]**, el **[!UICONTROL ID de artefacto]**, la **[!UICONTROL versión]** y el **[!UICONTROL paquete]** del proyecto y haga clic en **[!UICONTROL Finalizar]**. El proyecto se ha creado.
1. Abra el archivo pom.xml para editarlo y reemplace todo el contenido del archivo por lo siguiente:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. Agregue código fuente que use la interfaz de Java [RecipientInfoSpecifier](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) para elegir dinámicamente un usuario o un grupo para el paso Asignar tarea. Para ver el código de ejemplo, consulte [Ejemplo para elegir dinámicamente un usuario o un grupo mediante una interfaz Java](#-sample-scripts-for).
1. Abra un símbolo del sistema y vaya al directorio que contiene el proyecto del paquete OSGi. Utilice el siguiente comando para crear el paquete OSGi:

   `mvn clean install`

1. Cargue el paquete en un servidor de AEM Forms. Puede utilizar el Administrador de paquetes de AEM para importar el paquete en el servidor de AEM Forms.

Una vez importado el paquete, la opción de elegir la interfaz de Java para seleccionar dinámicamente un usuario o un grupo estará disponible para los pasos de Adobe Sign y Asignar tarea.

### Código Java de ejemplo para elegir un usuario o un grupo de forma dinámica {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

El siguiente código de ejemplo elige dinámicamente un usuario asignado para el paso de Adobe Sign. Este código se utiliza en un paquete OSGi. Antes de usar el código que se muestra a continuación, asegúrese de que la información de los usuarios (direcciones de correo electrónico y números de teléfono) que se menciona en este es correcta. Si la información de los usuarios mencionada en el código es incorrecta, puede producirse un error durante el proceso relacionado.

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```
