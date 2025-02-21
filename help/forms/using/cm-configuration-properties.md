---
title: Propiedades de configuración de Administración de correspondencia
description: En este tema se explica cómo modificar el Compositor de recursos con configuraciones específicas de la solución. En este tema se detallan las propiedades que puede editar, con su descripción, los valores predeterminados y los valores aceptables.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 100%

---

# Propiedades de configuración de Administración de correspondencia {#correspondence-management-configuration-properties}

Para configurar estas propiedades, abra la siguiente URL en un explorador: `https://<server>:<port>/<contextPath>/system/console/configMgr` y seleccione **Configuraciones de Administración de correspondencia**.

Administración de correspondencia tiene las siguientes propiedades de configuración:

<table>
 <tbody>
  <tr>
   <th><p><strong>Propiedad</strong></p> </th>
   <th><p><strong>Descripción</strong></p> </th>
   <th><p><strong>Predeterminado</strong></p> </th>
   <th><p><strong>Valores aceptables</strong></p> </th>
  </tr>
  <tr>
   <td><p>Sangría</p> </td>
   <td>Sangría en módulos<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Cualquier número</p> </td>
  </tr>
  <tr>
   <td>Anchura mínima de número</td>
   <td>Ancho mínimo que se aplicará en el campo viñeta/número, al utilizar listas numeradas separadas de números romanos</td>
   <td>8,0 mm</td>
   <td>Cualquier número</td>
  </tr>
  <tr>
   <td><p>Anchura mínima de los números romanos</p> </td>
   <td><p>Anchura mínima que se aplicará en el campo viñeta/número, al utilizar números romanos</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Cualquier número</p> </td>
  </tr>
  <tr>
   <td>Tipo de representación</td>
   <td>El tipo de representación que utiliza la aplicación Crear correspondencia para obtener la vista previa de la carta. </td>
   <td>Representación del HTML</td>
   <td>Representación del HTML/Representación del PDF</td>
  </tr>
  <tr>
   <td><p>Habilitar resaltado de PDF CCR</p> </td>
   <td><p>Habilita el resaltado del PDF en la aplicación Crear correspondencia</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de resaltado de destino</p> </td>
   <td><p>Tipo de resaltado de destino en la aplicación Crear correspondencia</p> </td>
   <td><p>border</p> </td>
   <td><p>border / fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Color de resaltado de destino</p> </td>
   <td><p>Color de resaltado de destino en la aplicación Crear correspondencia</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Cualquier color RGB en el formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de resaltado de contenido</p> </td>
   <td><p>Tipo de resaltado de contenido en la aplicación Crear correspondencia</p> </td>
   <td><p>Relleno</p> </td>
   <td><p>border / fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Color de resaltado de contenido</p> </td>
   <td><p>Color de resaltado de contenido en la aplicación Crear correspondencia</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Cualquier color RGB en el formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de resaltado de campo</p> </td>
   <td><p>Tipo de resaltado de campo en la aplicación Crear correspondencia</p> </td>
   <td><p>fill</p> </td>
   <td><p>border / fill / none</p> </td>
  </tr>
  <tr>
   <td><p>Color de resaltado de campo</p> </td>
   <td><p>Color de resaltado de campo en la aplicación Crear correspondencia</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Cualquier color RGB en el formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tiempo de espera de la aplicación</p> </td>
   <td><p>Tiempo de espera de la aplicación en segundos</p> </td>
   <td><p>1200</p> </td>
   <td><p>Cualquier número</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro del documento PDF</p> </td>
   <td><p>Nombre del parámetro del documento PDF en el proceso posterior</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro de datos XML</p> </td>
   <td><p>Nombre del parámetro para el documento XML (datos) en el proceso posterior</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro del documento XDP</p> </td>
   <td><p>Nombre del parámetro para el documento XDP enviado al proceso posterior</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro de la URL de redireccionamiento</p> </td>
   <td><p>Nombre del parámetro para la URL de redireccionamiento enviada desde el proceso de publicación. Este valor puede ser cualquier nombre de variable de cadena</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de envío PDF</p> </td>
   <td><p>Tipo de envío PDF (tipo de PDF generado al realizar el envío desde la aplicación Crear correspondencia)</p> </td>
   <td><p>nonInteractive</p> </td>
   <td><p>Interactivo / no interactivo</p> </td>
  </tr>
  <tr>
   <td><p>Optimizar instancia del diccionario de datos</p> </td>
   <td><p>Habilita la transferencia optimizada de la instancia del diccionario de datos entre el servidor y el cliente</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Incoherencias de corrección automática </p> </td>
   <td><p>Cuando está habilitado, administra automáticamente las posibles incoherencias en las asignaciones de cartas</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Usar formatos de datos configurados</p> </td>
   <td><p>Controla si se deben usar formatos de edición de datos configurados y de visualización de datos</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Formatos de visualización de datos</p> </td>
   <td><p>Especifica el formato de visualización específico de la configuración regional para los datos</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>--</p> </td>
  </tr>
  <tr>
   <td><p>Formato de edición de datos</p> </td>
   <td><p>Editar formato para los datos. Se utiliza al escribir datos como String o al analizar datos de String</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>--<p> </p> </td>
  </tr>
  <tr>
   <td><p>Administrar instancias de carta en publicación</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad Administrar carta (aplicable solo para el servidor de publicación)</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría. Si es false, los registros de auditoría de todas las acciones se deshabilitarán</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Leer auditoría</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para lecturas de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Crear auditoría</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la creación de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de actualización</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la actualización de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar la auditoría de reversión</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la reversión de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de publicación</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para la publicación de recursos</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría Guardar como borrador</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para guardar borradores de cartas</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de envío</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para el envío de cartas</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de correo electrónico</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para enviar cartas por correo electrónico</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de impresión</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para imprimir cartas</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoría de entrega personalizada</p> </td>
   <td><p>Habilitar/deshabilitar la funcionalidad de auditoría para el envío personalizado de cartas</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Nombre del parámetro de documentos adjuntos</p> </td>
   <td><p>Nombre del parámetro para los documentos adjuntos enviados al proceso posterior</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Cualquier nombre de variable de cadena</p> </td>
  </tr>
  <tr>
   <td><p>Raíz del usuario de CM</p> </td>
   <td><p>URL de la carpeta que contiene todos los recursos de usuario de Administración de correspondencia</p> </td>
   <td><p>--</p> </td>
   <td><p>Ubicación de carpeta válida</p> </td>
  </tr>
  <tr>
   <td><p>Tamaño de la memoria caché Cartas</p> </td>
   <td><p>Especifique el número máximo de cartas que se guardarán en la memoria caché.</p> <p>Si se cambia este valor, se limpiará <code>in-memory</code> la memoria caché.</p> </td>
   <td><p>100</p> </td>
   <td><p>Cualquier valor numérico</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar memoria caché de Cartas</p> </td>
   <td><p>Habilitar/Deshabilitar la memoria caché de Cartas.</p> <p>Si se cambia este valor, se limpiará <code>in-memory </code> la memoria caché.</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Solicitud de elementos de datos</p> </td>
   <td><p>Mantiene el orden de los elementos de datos en la interfaz de creación de correspondencia según su secuencia en Cartas</p> </td>
   <td><p>true</p> </td>
   <td><p>true / false</p> </td>
  </tr>
  <tr>
   <td><p>Compatibilidad de Recargas</p> </td>
   <td><p>Habilitar/Deshabilitar la compatibilidad de Recargas en cartas representadas en el lado del servidor.</p> <p>Deshabilitar esto mejorará el rendimiento del procesamiento de cartas.</p> </td>
   <td><p>false</p> </td>
   <td><p>true / false</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Carpeta Temporal</td>
   <td>Ubicación de la carpeta temporal.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Guardado remoto</td>
   <td>Guarda las instancias de carta en el autor de procesamiento especificado.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Opciones de compatibilidad</td>
   <td>Opciones de compatibilidad del formato configname:configvalue separadas por una coma.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Directorio de depuración </p> <p> </p> </td>
   <td>Ubicación de la carpeta del sistema de archivos para la depuración. Si el directorio no <code>exists</code>, no se generarán volcados de depuración.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
