---
title: Crear asignaciones de formularios personalizadas
description: Al crear una tabla personalizada en Adobe Campaign, es posible que desee crear un formulario en AEM que se asigne a esa tabla personalizada
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Crear asignaciones de formularios personalizadas{#creating-custom-form-mappings}

Al crear una tabla personalizada en Adobe Campaign, es posible que desee crear un formulario en AEM que se asigne a esa tabla personalizada.

Este documento describe cómo crear asignaciones de formularios personalizadas. Cuando complete los pasos de este documento, proporcionará a los usuarios una página de evento en la que podrán registrarse en un evento próximo. A continuación, puede realizar un seguimiento con estos usuarios a través de Adobe Campaign.

## Requisitos previos {#prerequisites}

Debe tener instalado lo siguiente:

* Adobe Experience Manager
* Adobe Campaign Classic

Consulte [Integración de AEM con Adobe Campaign Classic](/help/sites-administering/campaignonpremise.md) para obtener más información.

## Crear asignaciones de formularios personalizadas {#creating-custom-form-mappings-2}

Para crear asignaciones de formularios personalizadas, debe seguir estos pasos de alto nivel, que se describen en detalle en las secciones siguientes:

1. Cree una tabla personalizada.
1. Extender la tabla **seed**.
1. Cree una asignación personalizada.
1. Cree una entrega basado en la asignación personalizada.
1. Cree el formulario en AEM, que utilizará el envío creado.
1. Envíe el formulario para probarlo.

### Creación de la tabla personalizada en Adobe Campaign {#creating-the-custom-table-in-adobe-campaign}

Comience creando una tabla personalizada en Adobe Campaign. En este ejemplo, se utiliza la siguiente definición para crear una tabla de eventos:

```xml
<element autopk="true" label="Event" labelSingular="Event" name="event">
 <attribute label="Event Date" name="eventdate" type="date"/>
 <attribute label="Event Name" name="eventname" type="string"/>
 <attribute label="Email" name="email" type="string"/>
 <attribute label="Number of Seats" name="seats" type="long"/>
</element>
```

Después de crear la tabla de eventos, ejecute el **Asistente para actualizar la estructura de la base de datos** para crear la tabla.

### Ampliación de la tabla semilla {#extending-the-seed-table}

En Adobe Campaign, seleccione **Add** para crear una extensión de la tabla **Direcciones semilla (nms)**.

![chlimage_1-194](assets/chlimage_1-194.png)

Ahora, use los campos de la tabla **event** para extender la tabla **seed**:

```xml
<element label="Event" name="custom_cus_event">
 <attribute name="eventname" template="cus:event:event/@eventname"/>
 <attribute name="eventdate" template="cus:event:event/@eventdate"/>
 <attribute name="email" template="cus:event:event/@email"/>
 <attribute name="seats" template="cus:event:event/@seats"/>
 </element>
```

Después de esto, ejecute **Actualizar asistente de base de datos** para aplicar los cambios.

### Creación de asignaciones de destino personalizadas {#creating-custom-target-mapping}

En **Administración/Administración de campañas** t, vaya a **Asignaciones de objetivos** y agregue una nueva asignación de destino de T **t.**

>[!NOTE]
>
>Asegúrese de usar un nombre descriptivo para **Internal name**.

![chlimage_1-195](assets/chlimage_1-195.png)

### Creación de una plantilla de envíos personalizada {#creating-a-custom-delivery-template}

En este paso, está agregando una plantilla de envío que usa la **asignación de destino** creada.

En **Recursos/Plantillas**, vaya a la Plantilla de envíos y duplique el envío de AEM existente. Al hacer clic en **Para**, seleccione crear evento **Asignación de destino**.

![chlimage_1-196](assets/chlimage_1-196.png)

### Creación del formulario en AEM {#building-the-form-in-aem}

En AEM, asegúrese de haber configurado un Cloud Service en **Propiedades de página**.

A continuación, en la pestaña **Adobe Campaign**, seleccione la entrega que se creó en [Creación de una plantilla de entrega personalizada](#creating-a-custom-delivery-template).

![chlimage_1-197](assets/chlimage_1-197.png)

Al configurar los campos, asegúrese de especificar nombres de elemento únicos para los campos de formulario.

Una vez configurados los campos, debe cambiar manualmente la asignación.

En CRXDE-lite, vaya al nodo **jcr:content** (de la página) y cambie el valor **acMapping** por el nombre interno de **Target mapping**.

![chlimage_1-198](assets/chlimage_1-198.png)

En la configuración del formulario, asegúrese de marcar la casilla para crear si no existe

![chlimage_1-199](assets/chlimage_1-199.png)

### Enviar el formulario {#submitting-the-form}

Ahora puede enviar el formulario y validar en Adobe Campaign si los valores se han guardado.

![chlimage_1-200](assets/chlimage_1-200.png)

## Solución de problemas {#troubleshooting}

**&quot;Tipo no válido para el valor &#39;02/02/2015&#39; del elemento &#39;@eventdate&#39; (documento de tipo &#39;Event ([adb:event])&#39;)&quot;**

Al enviar el formulario, este error se registra en **error.log** en AEM.

Esto se debe a un formato no válido para el campo de fecha. La solución consiste en proporcionar **aaaa-mm-dd** como valor.
