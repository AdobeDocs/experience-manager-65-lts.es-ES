---
title: 'Tutorial: Planificar la comunicación interactiva'
description: Planifique la estructura de la comunicación interactiva
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 98%

---

# Tutorial: Planificar la comunicación interactiva {#tutorial-plan-the-interactive-communication}

Planifique la estructura de la comunicación interactiva

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Este tutorial es un paso en la serie [Crear su primera comunicación interactiva](/help/forms/using/create-your-first-interactive-communication.md). Se recomienda seguir la serie en orden cronológico para comprender, realizar y mostrar el caso de uso del tutorial completo.

El primer paso de la planificación de una comunicación interactiva es finalizar el contenido de la comunicación. Los expertos de áreas como la legal, la de finanzas, la de soporte o la de marketing pueden ayudarle a finalizar el contenido. Una vez finalizado, debe analizarlo para identificar los distintos tipos de recursos necesarios para crear la comunicación interactiva.

## Consideraciones sobre la planificación {#planning-considerations}

Una comunicación interactiva contiene los siguientes elementos:

* El **texto estático** incluye principalmente las partes de la comunicación interactiva que son de naturaleza genérica y se incluyen en las comunicaciones de todos los clientes, como el encabezado, el pie de página, el saludo o las exenciones de responsabilidad legal.
* Los **datos procedentes de un sistema back-end (modelo de datos de formulario)** son específicos del cliente y se combinan dinámicamente con la comunicación interactiva. Por ejemplo, el número de póliza o la dirección pueden obtenerse mediante el modelo de datos de formulario.
* El **diseño o las plantillas** para la versión impresa y web de la comunicación interactiva.
* El **orden** en el que aparecen los distintos párrafos de texto en la comunicación interactiva.
* Los **datos introducidos por el empleado de primera línea (interfaz de usuario del agente)** que está personalizando la comunicación antes de enviarla. Por ejemplo, la fecha de vencimiento del pago.

* Los **datos condicionales** que se rellenan en función de condiciones predefinidas. Por ejemplo, la fecha en la que se genera la comunicación interactiva.
* Las **imágenes almacenadas en un repositorio**, como logotipos e imágenes de firma. Las imágenes como logotipos corporativos aparecerían en la mayoría o en todas las comunicaciones interactivas.
* Las **tablas y los gráficos** son necesarios para simplificar la representación de datos complejos en una comunicación interactiva.

## Estructura de la comunicación interactiva {#anatomy-of-the-interactive-communication}

Una vez finalizado el contenido y los elementos utilizados para crear la comunicación interactiva, puede crear la estructura de la comunicación interactiva. La estructura debe tener los detalles que figuran en la sección [Consideraciones sobre la planificación](/help/forms/using/planning-interactive-communications.md#planning-considerations). Siguiendo con nuestro caso de uso, a continuación encontrará un ejemplo de la estructura de la factura mensual que un operador de telecomunicaciones envía a sus clientes.

La estructura contiene datos con los siguientes modos de entrada:

* Texto estático
* Modelo de datos de formulario
* IU del Agente
* Datos condicionales
* Imágenes

En cada sección, el texto en negrita representa texto estático. La base de datos incluye las tablas de clientes, facturas y llamadas. Un modelo de datos de formulario puede recibir datos de cualquiera de estas tablas. Para obtener más información, consulte [Creación del modelo de datos de formulario](/help/forms/using/create-form-data-model0.md).

La siguiente tabla muestra la fuente de datos de cada uno de los campos de la estructura de la comunicación interactiva:

<table>
 <tbody>
  <tr>
   <td>Sección</td>
   <td>Texto estático</td>
   <td>FDM </td>
   <td>IU del agente</td>
   <td>Imágenes</td>
  </tr>
  <tr>
   <td>Detalles de la factura</td>
   <td><p>N.º de factura</p> <p>Fecha de la factura</p> <p>Período de facturación</p> <p>Su plan</p> </td>
   <td><p>Valor del campo <strong>Su plan </strong></p> <p>Tabla: cliente</p> </td>
   <td><p>Valores de los siguientes campos:</p>
    <ul>
     <li>N.º de factura</li>
     <li>Fecha de la factura</li>
     <li>Período de facturación</li>
    </ul> <p> </p> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Detalles del cliente</td>
   <td><p>Lugar de suministro</p> <p>Código de estado</p> <p>Número de móvil</p> <p>Número de contacto alternativo</p> <p>Número de relación</p> <p>Número de conexiones</p> </td>
   <td><p>Valores de los siguientes campos:</p>
    <ul>
     <li>Nombre</li>
     <li>Dirección</li>
     <li>Número de móvil</li>
     <li>Número de contacto alternativo</li>
     <li>Número de relación</li>
    </ul> <p>Tabla: cliente</p> </td>
   <td><p>Valores de los siguientes campos:</p>
    <ul>
     <li>Lugar de suministro</li>
     <li>Código de estado</li>
     <li>Número de conexiones</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Resumen de la factura</td>
   <td><p>Saldo anterior</p> <p>Pagos</p> <p>Ajustes</p> <p>Cargos del período de facturación actual</p> <p>Importe vencido</p> <p>Fecha de vencimiento</p> </td>
   <td><p>Valor del campo <strong>Cargos del período de facturación actual </strong></p> <p>Tabla: facturas</p> </td>
   <td><p>Valores de los siguientes campos:</p>
    <ul>
     <li>Saldo anterior</li>
     <li>Pagos</li>
     <li>Ajustes</li>
     <li>Importe vencido</li>
     <li>Fecha de vencimiento</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Resumen de cargos</td>
   <td><p>Cargos por llamadas</p> <p>Cargos por llamadas de conferencia</p> <p>Cargos por SMS </p> <p>Cargos por Internet móvil</p> <p>Cargos de itinerancia nacional</p> <p>Cargos de itinerancia internacional</p> <p>Cargos por servicios de valor añadido</p> <p>Cargos totales</p> <p>TOTAL A PAGAR</p> <p>Condición del campo Cargos por servicios de valor añadido</p> </td>
   <td><p>Valores de los siguientes campos:</p>
    <ul>
     <li>Cargos por llamadas</li>
     <li>Cargos por llamadas de conferencia</li>
     <li>Cargos por SMS </li>
     <li>Cargos por Internet móvil</li>
     <li>Cargos de itinerancia nacional</li>
     <li>Cargos de itinerancia internacional</li>
     <li>Cargos por servicios de valor añadido</li>
     <li>Cargos totales (campo calculado de cargos por consumo)</li>
     <li>TOTAL A PAGAR (campo calculado de cargos por consumo)</li>
    </ul> <p>Tabla: facturas</p> </td>
   <td>Sin campos</td>
   <td>--</td>
  </tr>
  <tr>
   <td>Llamadas desglosadas: salientes</td>
   <td><p>Nombres de columna:</p>
    <ul>
     <li>Fecha</li>
     <li>Hora</li>
     <li>Número</li>
     <li>Duración</li>
     <li>Cargos</li>
    </ul> </td>
   <td><p>Todos los valores</p> <p>Tabla: llamadas</p> </td>
   <td>Sin campos</td>
   <td>--</td>
  </tr>
  <tr>
   <td>Pagar ahora</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Servicios de valor agregado</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
