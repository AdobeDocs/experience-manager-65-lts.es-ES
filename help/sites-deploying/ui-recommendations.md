---
title: Recomendaciones de interfaz de usuario para clientes
description: Una lista de recomendaciones relacionadas con las interfaces de usuario clásicas y las optimizadas para dispositivos táctiles.
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: f65f9e94-0837-48d1-a565-cfb880963790
source-git-commit: e7fc1120d12160ba866ceaddd087fc9acdfcd51d
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# Recomendaciones de interfaz de usuario para clientes{#user-interface-recommendations-for-customers}

Adobe Experience Manager incluye dos interfaces de usuario: la IU unificada de Experience Cloud (también conocida como IU táctil) y la IU clásica.

Este documento pretende guiar a los clientes para que elijan qué interfaz de usuario utilizar según su situación.

Términos de interés:

* **IU (o IU estándar)**
Interfaz de usuario moderna introducida en la versión 5.6.0 como vista previa tecnológica y ampliada en versiones posteriores. Se basa en la experiencia de usuario unificada para Adobe Experience Cloud, anteriormente conocida como IU táctil o IU táctil.

* **IU clásica**
Interfaz de usuario basada en la tecnología ExtJS introducida con CQ 5.1 en 2008.

* **Administrador del sitio**
Capacidades para administrar la jerarquía del sitio (mover, activar, gestionar referencias) y crear nuevas páginas.

* **Creación de páginas**
Capacidad para añadir o editar el contenido de una página.

* **Administrador de DAM/Assets**
Funciones para administrar recursos digitales (como imágenes, vídeos, documentos y descargas).

* **ContextHub**
Capacidades para agregar información sobre el visitante y utilizarla para varios fines. Proporciona una interfaz de usuario para simular a las personas que visitan el sitio. A partir de AEM 6.2, ContextHub sustituyó a la tecnología anterior, Client Context.

## General {#general}

En los últimos años, Adobe ha actualizado todas las soluciones de Adobe Experience Cloud con una interfaz de usuario unificada. Los usuarios de las soluciones de Experience Cloud disfrutan de una experiencia coherente con patrones comunes sobre cómo utilizar y utilizar las aplicaciones. Con cada versión, Adobe ha refinado su interfaz de usuario en función de los comentarios de los clientes que trabajan en las distintas soluciones.

La interfaz de usuario original para Adobe Experience Manager (anteriormente conocida como CQ5), presentada en 2008 y utilizada por los clientes que ejecutan las versiones 5.0-5.6.1, está presente en AEM 6.5. Esto garantiza que los clientes puedan actualizar a la versión 6.5 y beneficiarse de una plataforma actualizada con nuevas funciones mientras siguen utilizando la misma interfaz de usuario.

Adobe recomienda a los clientes que planeen cambiar a la nueva interfaz de usuario en 2018/19. Esto se puede hacer durante la actualización a 6.5 o en un proyecto independiente después de la actualización, que incluiría los ajustes necesarios en las personalizaciones y los cuadros de diálogo de componentes.

La IU clásica ha quedado obsoleta con AEM 6.4 y Adobe no tiene previsto realizar más mejoras en ella. Tenga en cuenta que la IU clásica sigue siendo totalmente compatible mientras está en desuso.

### Reglas y recomendaciones {#rules-and-recommendations}

A continuación se muestra una lista de recomendaciones de Administración de productos para Adobe Experience Manager 6.5:

<table>
 <tbody>
  <tr>
   <th>Mi proyecto...</th>
   <th>Recomendaciones</th>
  </tr>
  <tr>
   <td>Acaba de empezar a usar Adobe Experience Manager.</td>
   <td>Utilice la interfaz de usuario predeterminada.</td>
  </tr>
  <tr>
   <td><p>Ha usado AEM durante un tiempo.</p> <p>Ha utilizado la interfaz de usuario predeterminada del producto y ha desarrollado componentes personalizados para los sitios.<br /> </p> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la interfaz de usuario predeterminada para la administración de sitios, recursos, etc. etc.<br /> </li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de IU clásico. Consulte <a href="#selecting-your-ui">Selección de la interfaz de usuario</a>.</li>
    </ol> <p>A continuación, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de componentes para utilizar el formato de diálogo Coral 3. Adobe recomienda usar <a href="/help/sites-developing/modernization-tools.md">Herramientas de modernización de AEM</a> para actualizar los componentes.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Ha creado un sitio que usa ClientContext con integraciones.<br /> </td>
   <td>
    <ol>
     <li>Actualización a 6.5</li>
     <li>Utilice la interfaz de usuario predeterminada para la administración de sitios, recursos, etc. etc.</li>
     <li>Configure la acción "Editar página" para abrir el Editor de páginas de IU clásico. Consulte <a href="#selecting-your-ui">Selección de la interfaz de usuario</a>.</li>
    </ol> <p>A continuación, en una segunda fase:</p>
    <ol>
     <li>Actualice los cuadros de diálogo de componentes para utilizar el formato de diálogo Coral 3. Adobe recomienda usar <a href="/help/sites-developing/modernization-tools.md">Herramientas de modernización de AEM</a> para actualizar los componentes.</li>
     <li>Configure ContextHub (el reemplazo de ClientContext) y actualice las plantillas de página para usar ContextHub. ContextHub tiene un modo de compatibilidad que permite cargar tiendas ClientContext personalizadas.</li>
    </ol> </td>
  </tr>
  <tr>
   <td><p>Ha utilizado CQ/AEM durante muchos años.</p> <p>Ha ampliado la interfaz de usuario del producto (por ejemplo, Administración del sitio) y ha creado componentes con numerosos cuadros de diálogo de edición.</p> </td>
   <td><p>Actualice a 6.5 y configure la IU clásica como la predeterminada para la creación de páginas para todos los usuarios. Consulte <a href="#selecting-your-ui">Selección de la interfaz de usuario</a>.</p> <p>A continuación, inicie un proyecto para aplicar la personalización y optimizar los cuadros de diálogo de componentes en formato Coral 3. Ver <a href="#resources-to-help">recursos para ayudar</a>.<br /> </p> </td>
  </tr>
 </tbody>
</table>

### Selección de la IU {#selecting-your-ui}

Consulte [Selección de la interfaz de usuario](/help/sites-authoring/select-ui.md) para obtener información sobre cómo configurar el sistema según sea necesario.

### Estado de IU táctil {#touch-enabled-ui-status}

Para obtener más información sobre las mejoras realizadas en la IU táctil en AEM 6.5, consulte [Novedades](/help/release-notes/release-notes.md#what-s-new) en las Notas de la versión.


### Recursos de ayuda {#resources-to-help}

Para obtener información básica sobre la manipulación básica:

* [Creación de páginas](/help/sites-authoring/page-authoring.md).

Para obtener información detallada sobre el desarrollo:

* [Arquitectura de IU táctil](/help/sites-developing/touch-ui-concepts.md).
* Use [Herramientas de modernización de AEM](/help/sites-developing/modernization-tools.md) para convertir los cuadros de diálogo de edición de componentes de la IU clásica a la IU táctil.

* [Estructura de la IU táctil](/help/sites-developing/touch-ui-structure.md).

* [Personalización de las consolas en la IU táctil](/help/sites-developing/customizing-consoles-touch.md) (incluye código de ejemplo).

* [Personalización de la creación de páginas en la IU táctil](/help/sites-developing/customizing-page-authoring-touch.md) (incluye código de ejemplo).

* [Documentación de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).
