---
title: Preparar y enviar comunicaciones interactivas mediante la interfaz de usuario del agente
description: La interfaz de usuario del agente permite a los agentes preparar y enviar una comunicación interactiva al proceso de publicación. El agente realiza las modificaciones necesarias según lo permitido y envía la comunicación interactiva a un proceso de publicación, como el correo electrónico o la impresión.
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 85%

---

# Preparar y enviar comunicaciones interactivas mediante la interfaz de usuario del agente {#prepare-and-send-interactive-communication-using-the-agent-ui}

La interfaz de usuario del agente permite a los agentes preparar y enviar una comunicación interactiva al proceso de publicación. El agente realiza las modificaciones necesarias según lo permitido y envía la comunicación interactiva a un proceso de publicación, como el correo electrónico o la impresión.

## Información general {#overview}

Una vez creada una comunicación interactiva, el agente puede abrirla en la interfaz de usuario del agente y preparar una copia específica para el destinatario introduciendo datos y administrando el contenido y los archivos adjuntos. Por último, puede enviar la comunicación interactiva a un proceso de publicación.

Cuando prepara la comunicación interactiva mediante la interfaz de usuario del agente, este administra los siguientes aspectos de la comunicación interactiva en la interfaz de usuario antes de enviarla a un proceso de publicación:

* **Datos**: la pestaña Datos de la interfaz de usuario del agente muestra todas las variables editables por el agente y las propiedades del modelo de datos de formulario desbloqueadas en la comunicación interactiva. Estas variables o propiedades se crean al editar o crear los fragmentos de documento incluidos en la comunicación interactiva. La pestaña Datos incluye también todos los campos creados en la plantilla del canal de impresión o XDP. La pestaña Datos aparece únicamente cuando el agente puede editar alguna variable, propiedad del modelo de datos de formulario o campo de la comunicación interactiva.
* **Contenido**: en la pestaña Contenido, el agente administra el contenido de la comunicación interactiva, como los fragmentos de documento y las variables de contenido. El agente puede realizar los cambios en el fragmento de documento según lo permitido en las propiedades de esos fragmentos de documento al crear la comunicación interactiva. El agente también puede reordenar, agregar o quitar un fragmento de documento y añadir saltos de página, si se le permite.
* **Archivos adjuntos**: la pestaña Archivos adjuntos aparece en la interfaz de usuario del agente únicamente si la comunicación interactiva tiene archivos adjuntos o si el agente tiene acceso a la biblioteca. El agente puede poseer los permisos necesarios para cambiar o editar los archivos adjuntos, o carecer de ellos.

## Preparación de la comunicación interactiva mediante la interfaz de usuario del agente {#prepare-interactive-communication-using-the-agent-ui}

1. Seleccione **[!UICONTROL Forms]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione la comunicación interactiva adecuada y seleccione **[!UICONTROL Abrir la interfaz de usuario del agente]**.

   >[!NOTE]
   >
   >La interfaz de usuario del agente solo está disponible si la comunicación interactiva seleccionada contiene un canal de impresión.

   ![abrir_iu_del_agente](assets/openagentiui.png)

   En función del contenido y de las propiedades de la comunicación interactiva, la interfaz de usuario del agente aparece con las tres pestañas siguientes: Datos, Contenido y Archivos adjuntos.

   ![pestañas_iu_del_agente](assets/agentuitabs.png)

   Comience a introducir los datos y a administrar el contenido y los archivos adjuntos.

### Introducir datos {#enter-data}

1. En la pestaña Datos, introduzca los datos de las variables, las propiedades del modelo de datos de formulario y los campos de la plantilla de impresión (XDP), según los requisitos. Complete todos los campos obligatorios marcados con un asterisco (*) para habilitar el botón **Enviar**.

   Seleccione un valor de campo de datos en la vista previa de la comunicación interactiva para resaltar el campo de datos correspondiente en la pestaña Datos o a la inversa.

### Administrar contenido {#manage-content}

En la pestaña Contenido, administre el contenido de la comunicación interactiva, como los fragmentos de documento y las variables de contenido.

1. Seleccione **[!UICONTROL Contenido]**. Aparece la pestaña Contenido de la comunicación interactiva.

   ![pestaña_contenido_iu_agente](assets/agentuicontenttab.png)

1. Edite los fragmentos de documento según los requisitos en la pestaña Contenido. Para establecer el enfoque en el fragmento relevante en la jerarquía de contenido, puede seleccionar la línea o el párrafo correspondiente en la vista previa de la comunicación interactiva o seleccionar el fragmento directamente en la jerarquía de contenido.

   Por ejemplo, el fragmento de documento con la línea &quot;Realizar un pago en línea ahora ...&quot; está seleccionado en la vista previa del gráfico que aparece a continuación, y se ha seleccionado el mismo fragmento de documento en la pestaña Contenido

   ![enfoque_módulo_contenido](assets/contentmodulefocus.png)

   Si pulsa Resaltar los módulos seleccionados en el contenido ( ![ccr_resaltar_módulos_seleccionados_en_contenido](assets/highlightselectedmodulesincontentccr.png)) en la parte superior izquierda de la vista previa de las pestañas Contenido o Datos, puede deshabilitar o habilitar la funcionalidad para ir al fragmento de documento pulsando o seleccionando el texto, el párrafo o el campo de datos relevantes en la vista previa.

   Los fragmentos que el agente puede editar al crear la comunicación interactiva incluyen el icono Editar contenido seleccionado ( ![iconeditselectedcontent](assets/iconeditselectedcontent.png)). Seleccione el icono Editar contenido seleccionado para iniciar el fragmento en modo de edición y realizar cambios en él. Utilice las siguientes opciones para dar formato y administrar el texto:

   * [Opciones de formato](#formattingtext)

      * [Copiar y pegar texto con formato de otras aplicaciones](#pasteformattedtext)
      * [Resaltar fragmentos del texto](#highlightemphasize)

   * [Caracteres especiales](#specialcharacters)
   * [Métodos abreviados de teclado](/help/forms/using/keyboard-shortcuts.md)

   Para obtener más información sobre las acciones disponibles en los diferentes fragmentos de documento de la interfaz de usuario del agente, consulte [Acciones e información disponible en la interfaz de usuario del agente](#actionsagentui).

1. Para añadir un salto de página a la salida de impresión de la comunicación interactiva, coloque el cursor en el punto en el que desea insertar un salto de página y seleccione Salto de página antes o Salto de página después ( ![salto_de_página_antes_después](assets/pagebreakbeforeafter.png)).

   En la comunicación interactiva se inserta un marcador de posición de salto de página explícito. Para ver cómo afectan los saltos de página explícitos a la comunicación interactiva, consulte la vista previa de impresión.

   ![salto_de_página_explícito](assets/explicitpagebreak.png)

   Continúe administrando los archivos adjuntos de la comunicación interactiva.

### Administrar archivos adjuntos {#manage-attachments}

1. Seleccione **[!UICONTROL Archivo adjunto]**. La interfaz de usuario del agente muestra los archivos adjuntos disponibles tal como están configurados al crear la comunicación interactiva.

   Puede optar por no enviar un archivo adjunto junto con la comunicación interactiva tocando el icono Ver y puede seleccionar la cruz del archivo adjunto para eliminarlo (si el agente puede eliminar u ocultar el archivo adjunto) de la comunicación interactiva. Los iconos Ver y Eliminar están desactivados en los archivos adjuntos especificados como obligatorios al crear la comunicación interactiva.

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. Seleccione el icono Acceder a la biblioteca (![libraryaccess](assets/libraryaccess.png)) para acceder a la biblioteca de contenido e insertar recursos DAM como archivos adjuntos.

   >[!NOTE]
   >
   >El icono Acceder a la biblioteca solo está disponible si el acceso a la biblioteca estaba habilitado al crear la comunicación interactiva (en las propiedades del contenedor de documentos del canal de impresión).

1. Si el orden de los archivos adjuntos no estaba bloqueado al crear la comunicación interactiva, puede reordenarlos seleccionando un archivo y pulsando las flechas abajo y arriba.
1. Utilice las opciones Vista previa en la web y Vista previa de impresión para ver si las dos salidas se ajustan a sus necesidades.

   Si encuentra que las vistas previas son satisfactorias, seleccione **[!UICONTROL Enviar]** para enviar la comunicación interactiva a un proceso de publicación. Si desea realizar cambios, salga de la vista previa para llevarlos a cabo.

## Aplicar formato al texto {#formattingtext}

Al editar un fragmento de texto en la interfaz de usuario del agente, la barra de herramientas cambia según el tipo de ediciones que decida realizar: Fuente, Párrafo o Lista.

![tipo_de_formato_barra_herramientas](assets/typeofformattingtoolbar.png) ![Barra de herramientas Fuente](do-not-localize/fonttoolbar.png)

Barra de herramientas Fuente

![Barra de herramientas Párrafo](do-not-localize/paragraphtoolbar.png)

Barra de herramientas Párrafo

![Barra de herramientas Lista](do-not-localize/listtoolbar.png)

Barra de herramientas Lista

### Resaltar partes del texto {#highlightemphasize}

Para resaltar fragmentos de texto en un fragmento editable, seleccione el texto y elija Color de resaltado.

![highlighttextagentui](assets/highlighttextagentui.png)

### Pegar texto con formato {#pasteformattedtext}

![pastedtext](assets/pastedtext.png)

### Insertar caracteres especiales en el texto {#specialcharacters}

La interfaz de usuario del agente ha incorporado la compatibilidad con 210 caracteres especiales. El administrador puede [agregar compatibilidad con caracteres especiales adicionales o personalizados usando la personalización](/help/forms/using/custom-special-characters.md).

#### Envío de archivos adjuntos {#attachmentdelivery}

* Cuando la comunicación interactiva se procesa mediante API del lado del servidor como un PDF interactivo o no interactivo, el PDF procesado contiene archivos adjuntos como archivos adjuntos del PDF.
* Cuando se carga un proceso de publicación asociado a una comunicación interactiva como parte de la opción Enviar mediante la interfaz de usuario del agente, los archivos adjuntos se pasan como el parámetro List&lt;com.adobe.idp.Document> inAttachmentDocs.
* Los flujos de trabajo del mecanismo de envío, como el correo electrónico y la impresión, también proporcionan archivos adjuntos con la versión PDF de la comunicación interactiva.

## Acciones e información disponible en la interfaz de usuario del agente {#actionsagentui}

### Fragmentos de documento {#document-fragments}

![&#x200B; &#x200B;](do-not-localize/contentoptionsdocfragments.png)

* **Flechas arriba/abajo**: permiten mover fragmentos de documento hacia arriba o hacia abajo en la comunicación interactiva.
* **Eliminar**: si dispone de los permisos necesarios, elimina el fragmento del documento de la comunicación interactiva.
* **Salto de página antes** (aplicable a los fragmentos secundarios del área de destino): inserta un salto de página antes del fragmento de documento.
* **Sangría**: aumenta o disminuye la sangría de un fragmento de documento.
* **Salto de página después** (aplicable a los fragmentos secundarios del área de destino): inserta un salto de página después del fragmento de documento.

![opciones_fragmento_documento](assets/docfragoptions.png)

* Editar (solo fragmentos de texto): abre el editor de texto enriquecido para editar el fragmento de documento de texto. Para obtener más información, consulte [Formato del texto](#formattingtext).

* Selección (icono en forma de ojo): incluye o excluye el fragmento de documento de la comunicación interactiva.
* Valores no rellenados (información): indica el número de variables no rellenadas del fragmento de documento.

### Fragmentos de documento de lista {#list-document-fragments}

![opciones_lista](assets/listoptions.png)

* Insertar línea en blanco: inserta una nueva línea en blanco.
* Selección (icono en forma de ojo): incluye o excluye el fragmento de documento de la comunicación interactiva.
* Omitir viñetas/numeraciones: active esta opción si desea omitir las viñetas o la numeración en el fragmento de documento de lista.
* Valores no rellenados (información): indica el número de variables no rellenadas del fragmento de documento.

## Guardar comunicaciones interactivas como borrador {#save-as-draft}

Puede utilizar la interfaz de usuario del agente para guardar uno o más borradores de cada comunicación interactiva y recuperar los borradores más tarde para seguir trabajando en ellos. Puede especificar un nombre diferente para cada borrador para identificarlo.

Adobe recomienda ejecutar estas instrucciones de forma secuencial para guardar correctamente una comunicación interactiva como borrador.

### Habilitar la función Guardar como borrador {#before-save-as-draft}

La función Guardar como borrador no está activada de forma predeterminada. Siga los siguientes pasos para habilitar la función:

1. Implemente la interfaz de proveedor de servicios (SPI) de [ccrDocumentInstance](https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html).

   La SPI permite guardar la versión de borrador de la comunicación interactiva en la base de datos con un ID de borrador como identificador único. Estas instrucciones dar por sentado que tiene conocimientos previos sobre cómo construir un paquete OSGi usando un proyecto Maven.

   Para ver la implementación de la SPI de ejemplo, consulte [Ejemplo de implementación de la SPI de ccrDocumentInstance](#sample-ccrDocumentInstance-spi).
1. Abra `http://<hostname>:<port>/ system/console/bundles` y seleccione **[!UICONTROL Instalar/actualizar]** para cargar el paquete OSGi. Compruebe que el estado del paquete cargado se muestra como **Activo**. Reinicie el servidor si el estado del paquete no se muestra como **Activo**.
1. Vaya a `https://'[server]:[port]'/system/console/configMgr`.
1. Seleccione **[!UICONTROL Crear configuración de correspondencia]**.
1. Seleccione **[!UICONTROL Habilitar Guardar usando CCRDocumentInstanceService]** y seleccione **[!UICONTROL Guardar]**.

### Guardar una comunicación interactiva como borrador {#save-as-draft-agent-ui}

Realice los siguientes pasos para guardar una comunicación interactiva como borrador:

1. Seleccione una comunicación interactiva en Forms Manager y seleccione **[!UICONTROL Abrir la interfaz de usuario del agente]**.

1. Realice los cambios correspondientes en la interfaz de usuario del agente y seleccione **[!UICONTROL Guardar como borrador]**.

1. Especifique el nombre del borrador en el campo **[!UICONTROL Nombre]** y seleccione **[!UICONTROL Listo]**.

Una vez guardada la comunicación interactiva como borrador, seleccione **[!UICONTROL Guardar cambios]** para guardar cualquier cambio adicional que haya realizado en el borrador.

### Recuperar el borrador de una comunicación interactiva {#retrieve-draft}

Después de guardar una comunicación interactiva como borrador, puede recuperarla para continuar trabajando en ella. Recupere la comunicación interactiva de la siguiente forma:

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[reclutid] hace referencia al identificador único de la versión de borrador que se genera después de guardar una comunicación interactiva como borrador.

### Ejemplo de implementación de la SPI de ccrDocumentInstance SPI {#sample-ccrDocumentInstance-spi}

Implemente la SPI de `ccrDocumentInstance` para guardar una comunicación interactiva como borrador. A continuación, se muestra una implementación de ejemplo de la SPI de `ccrDocumentInstance`.

```javascript
package Implementation;

import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.exception.CCRDocumentException;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.model.CCRDocumentInstance;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.services.CCRDocumentInstanceService;
import org.apache.commons.lang3.StringUtils;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.*;


@Component(service = CCRDocumentInstanceService.class, immediate = true)
public class CCRDraftService implements CCRDocumentInstanceService {

    private static final Logger logger = LoggerFactory.getLogger(CCRDraftService.class);

    private HashMap<String, Object> draftDataMap = new HashMap<>();

    @Override
    public String save(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", ccrDocumentInstance.getName());
            if (!CCRDocumentInstance.Status.SUBMIT.equals(ccrDocumentInstance.getStatus())) {
                ccrDocumentInstance = mySQLDataBaseServiceCRUD(ccrDocumentInstance,null, "SAVE");
            }
        } else {
            logger.error("Could not save data as draft name is empty");
        }
        return ccrDocumentInstance.getId();
    }

    @Override
    public void update(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", documentInstanceName);
            mySQLDataBaseServiceCRUD(ccrDocumentInstance, ccrDocumentInstance.getId(), "UPDATE");
        } else {
            logger.error("Could not save data as draft Name is empty");
        }
    }

    @Override
    public CCRDocumentInstance get(String id) throws CCRDocumentException {
        CCRDocumentInstance cCRDocumentInstance;
        if (StringUtils.isEmpty(id)) {
            logger.error("Could not retrieve data as draftId is empty");
            cCRDocumentInstance = null;
        } else {
            cCRDocumentInstance = mySQLDataBaseServiceCRUD(null, id,"GET");
        }
        return cCRDocumentInstance;
    }

    @Override
    public List<CCRDocumentInstance> getAll(String userId, Date creationTime, Date updateTime,
                                            Map<String, Object> optionsParams) throws CCRDocumentException {
        List<CCRDocumentInstance> ccrDocumentInstancesList = new ArrayList<>();

        HashMap<String, Object> allSavedDraft = mySQLGetALLData();
        for (String key : allSavedDraft.keySet()) {
            ccrDocumentInstancesList.add((CCRDocumentInstance) allSavedDraft.get(key));
        }
        return ccrDocumentInstancesList;
    }

    //The APIs call the service in the database using the following section.
    private CCRDocumentInstance mySQLDataBaseServiceCRUD(CCRDocumentInstance ccrDocumentInstance,String draftId, String method){
        if(method.equals("SAVE")){

            String autoGenerateId = draftDataMap.size() + 1 +"";
            ccrDocumentInstance.setId(autoGenerateId);
            draftDataMap.put(autoGenerateId, ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if (method.equals("UPDATE")){

            draftDataMap.put(ccrDocumentInstance.getId(), ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if(method.equals("GET")){

            return (CCRDocumentInstance) draftDataMap.get(draftId);

        }
        return null;
    }

    private HashMap<String, Object> mySQLGetALLData(){
        return draftDataMap;
    }
}
```

Las operaciones `save`, `update`, `get` y `getAll` llaman al servicio de base de datos para guardar una comunicación interactiva como borrador, actualizarla, recuperar datos de la base de datos y recuperar datos de todas las comunicaciones interactivas disponibles en ella. Este ejemplo utiliza `mySQLDataBaseServiceCRUD` como nombre del servicio de base de datos.

La siguiente tabla explica la implementación de ejemplo de la SPI de `ccrDocumentInstance`. Muestra cómo las operaciones `save`, `update`, `get` y `getAll` llaman al servicio de base de datos en la implementación de ejemplo.

<table> 
 <tbody>
 <tr>
  <td><p><strong>Operación</strong></p></td>
  <td><p><strong>Ejemplos del servicio de base de datos</strong></p></td> 
   </tr>
  <tr>
   <td><p>Puede crear el borrador de una comunicación interactiva o enviarla directamente. La API para la operación de guardado comprueba si la comunicación interactiva se envía como borrador y si incluye un nombre de borrador. A continuación, llama al servicio mySQLDataBaseServiceCRUD con Guardar como método de entrada.</p></br><img src="assets/save-as-draft-save-operation.png"/></td>
   <td><p>El servicio mySQLDataBaseServiceCRUD verifica Guardar como método de entrada, genera de forma automática un ID de borrador y lo devuelve a AEM. La lógica para generar un ID de borrador puede variar según la base de datos.</p></br><img src="assets/save-operation-service.png"/></td>
   </tr>
  <tr>
   <td><p>La API para la operación de actualización recupera el estado del borrador de la comunicación interactiva y comprueba si esta contiene un nombre de borrador. La API llama al servicio mySQLDataBaseServiceCRUD para actualizar ese estado en la base de datos.</p></br><img src="assets/save-as-draft-update-operation.png"/></td>
   <td><p>El servicio mySQLDataBaseServiceCRUD verifica Actualizar como método de entrada y guarda el estado del borrador de la comunicación en la base de datos.</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>La API para la operación GET comprueba si la comunicación interactiva contiene un ID de borrador. A continuación, llama al servicio mySQLDataBaseServiceCRUD con Get como método de entrada para recuperar los datos de la comunicación.</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>El servicio mySQLDataBaseServiceCRUD verifica Get como método de entrada y recupera los datos de la comunicación interactiva en función del ID de borrador.</p></br><img src="assets/get-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>La API para la operación getAll llama al servicio mySQLGetALLData para recuperar los datos de todas las comunicaciones interactivas guardadas en la base de datos.</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>El servicio mySQLGetALLData recupera los datos de todas las comunicaciones interactivas guardadas en la base de datos.</p></br><img src="assets/getall-operation-service.png"/></td>
   </tr>
  </tbody>
</table>

El siguiente es un ejemplo del archivo `pom.xml` que forma parte de la implementación:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
         xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.adobe.livecycle</groupId>
    <artifactId>draft-sample</artifactId>
    <version>2.0.0-SNAPSHOT</version>

    <name>Interact</name>
    <packaging>bundle</packaging>

    <dependencies>
        <dependency>
            <groupId>com.adobe.aemfd</groupId>
            <artifactId>aemfd-client-sdk</artifactId>
            <version>6.0.160</version>
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
                <version>3.3.0</version>
                <extensions>true</extensions>
                <executions>
                    <!--Configure extra execution of 'manifest' in process-classes phase to make sure SCR metadata is generated before unit test runs-->
                    <execution>
                        <id>scr-metadata</id>
                        <goals>
                            <goal>manifest</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <exportScr>true</exportScr>
                    <instructions>
                        <!-- Enable processing of OSGI DS component annotations -->
                        <_dsannotations>*</_dsannotations>
                        <!-- Enable processing of OSGI metatype annotations -->
                        <_metatypeannotations>*</_metatypeannotations>
                        <Bundle-SymbolicName>${project.groupId}-${project.artifactId}</Bundle-SymbolicName>
                    </instructions>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>autoInstall</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.sling</groupId>
                        <artifactId>maven-sling-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>install-bundle</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>install</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>

</project>
```

>[!NOTE]
>
>Asegúrese de actualizar la dependencia `aemfd-client-sdk` a la versión 6.0.160 en el archivo `pom.xml`.
