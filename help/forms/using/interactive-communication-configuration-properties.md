---
title: Propiedades de configuración de comunicaciones interactivas
description: Editar propiedades de configuración predeterminadas para comunicaciones interactivas
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 82%

---

# Propiedades de configuración de comunicaciones interactivas{#interactive-communications-configuration-properties}

Comunicaciones interactivas incluye propiedades que se configuran automáticamente después de instalar el paquete de [complementos de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md). Los autores de comunicaciones interactivas pueden editar estas propiedades de configuración predeterminadas mediante la página **Configuración de la consola web de Adobe Experience Manager**.

Abra la página **Configuración de la consola web de Adobe Experience Manager** con la siguiente URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Entre las propiedades de configuración se incluyen:

* [Configuración de fragmentos de documento](#document-fragments-configuration)
* [Configuración de Crear correspondencia](#create-correspondence-configuration)
* [Configuración del canal web de comunicaciones interactivas y formularios adaptables](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuración del tema del canal web de comunicaciones interactivas y formularios adaptables](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuración de fragmentos de documento {#document-fragments-configuration}

Seleccione **Configuración de fragmentos de documento** en la página **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración de los fragmentos de documento.

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Descripción</td> 
   <td>Predeterminado</td> 
   <td>Valores aceptables</td> 
  </tr> 
  <tr> 
   <td>Formatos de visualización de datos</td> 
   <td>El formato de visualización específico de la configuración regional para los campos, las variables y los elementos del modelo de datos de formulario disponibles al crear una comunicación interactiva para los canales impreso y web.</td> 
   <td> 
    <ul> 
     <li>configuración regional = en_US, de_DE, fr_FR y ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>Sangría</td> 
   <td>La anchura de una unidad de sangría aplicada al texto de los fragmentos de documento de lista.</td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Anchura mínima de los números romanos</td> 
   <td>La anchura mínima que se aplicará al campo de viñeta o número al utilizar números romanos en fragmentos de documento de lista. </td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Anchura mínima de número</td> 
   <td>La anchura mínima que se aplicará a la viñeta o al campo numérico al utilizar listas numeradas separadas por números que no sean números romanos en fragmentos de documento de lista.</td> 
   <td>8,0 mm</td> 
   <td>Número</td> 
  </tr> 
 </tbody> 
</table>

## Configuración de Crear correspondencia {#create-correspondence-configuration}

Seleccione **Crear configuración de correspondencia** en la página **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración de la interfaz de usuario del agente.

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Descripción</td> 
   <td>Predeterminado</td> 
   <td>Valores aceptables</td> 
  </tr> 
  <tr> 
   <td>Mostrar contenido resuelto para editarlo</td> 
   <td>Seleccione la casilla de verificación para mostrar el contenido resuelto (valores reales en lugar de marcadores de posición) mientras edita el módulo de texto de la interfaz de usuario del agente.</td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
  <tr> 
   <td>Aplicar marca de agua durante la vista previa</td> 
   <td>Seleccione la casilla de verificación para aplicar una marca de agua al canal de impresión de una comunicación interactiva en el modo de vista previa.</td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
  <tr> 
   <td>Habilitar incrustación de fuentes en PDF</td> 
   <td><p>Seleccione la casilla de verificación para activar la incrustación de fuentes en los documentos PDF. Después de seleccionar esta opción, puede incrustar nuevas fuentes después de generar o previsualizar los documentos PDF mediante la interfaz de usuario del agente. Utilice el canal de impresión de la comunicación interactiva para generar y previsualizar documentos PDF.</p> <p>La incrustación de fuentes en un documento PDF resulta útil si una fuente está disponible en el equipo que se utiliza para generar el PDF y no está disponible en el equipo cliente que accede a él.</p> <p>Para obtener más información sobre cómo incrustar fuentes, consulte <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizar editor de texto</a>.</p> </td> 
   <td>No seleccionado</td> 
   <td>No aplicable</td> 
  </tr> 
 </tbody> 
</table>

## Configuración del canal web de comunicaciones interactivas y formularios adaptables {#adaptive-form-and-interactive-communication-web-channel-configuration}

Seleccione **Configuración del canal web de comunicaciones interactivas y formularios adaptables** en la página **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración del canal web de comunicaciones interactivas y Forms adaptable. En la siguiente tabla se describen las propiedades relacionadas con Interactive Communications:

| Propiedad | Descripción | Predeterminado | Valores aceptables |
|---|---|---|---|
| Mostrar marcador de posición | Seleccione la casilla de verificación para activar la visualización de los marcadores de posición de los campos incluidos en los formularios adaptables y las comunicaciones interactivas. | Seleccionado | No aplicable |
| Número máximo de entradas de caché | Establezca el número máximo de formularios adaptables y comunicaciones interactivas que se pueden recuperar mediante la memoria caché. | 100 | Número |
| Convertir el nombre de archivo en único | Seleccione la casilla de verificación para asignar un nombre único a los archivos agregados como archivos adjuntos en los formularios adaptables y las comunicaciones interactivas. | No seleccionado | No aplicable |

## Configuración del tema del canal web de comunicaciones interactivas y formularios adaptables {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Seleccione **Configuración del tema del canal web de comunicaciones interactivas y formularios adaptables** en la página **Configuración de la consola web de Adobe Experience Manager** para ver las propiedades de configuración de los temas del canal web de las comunicaciones interactivas y los formularios adaptables Forms.

<table>
 <tbody> 
  <tr> 
   <td>Propiedad</td> 
   <td>Descripción</td> 
   <td>Predeterminado</td> 
   <td>Valores aceptables</td> 
  </tr> 
  <tr> 
   <td>Nombre de la lista de fuentes</td> 
   <td>La lista de fuentes disponibles para usar durante la creación de los formularios adaptables y las comunicaciones interactivas.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impacto</p> <p>Palatino Linotype</p> </td> 
   <td>Todas las fuentes válidas del servidor de Adobe</td> 
  </tr> 
 </tbody> 
</table>
