---
title: Configuración del marco de trabajo de integración de traducción
description: Obtenga información sobre cómo configurar el marco de trabajo de integración de traducciones en Adobe Experience Manager.
contentOwner: Guillaume Carlino
feature: Language Copy
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 17898ee854df1141272b207f96cebe69c325f12c
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 44%

---

# Configuración del marco de trabajo de integración de traducción{#configuring-the-translation-integration-framework}

El marco de trabajo de integración de traducciones se integra con los servicios de traducción de terceros para organizar la traducción de contenido de AEM.

* Conéctese a su proveedor de servicios de traducción.
* Cree una configuración del marco de trabajo de integración de traducción.
* Asocie las configuraciones de nube con sus páginas.

Para obtener una descripción general de las funciones de traducción de contenido de AEM, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md).

## Conexión a un proveedor de servicios de traducción {#connecting-to-a-translation-service-provider}

Cree una configuración en la nube que conecte AEM con su proveedor de servicios de traducción.

AEM incluye la capacidad de [conectarse a Microsoft® Translator](/help/sites-administering/tc-msconf.md) de forma predeterminada. Otros proveedores de tecnología de traducción con conectores de AEM que son miembros del programa de socios de Adobe Exchange se encuentran [aquí](https://exchange.adobe.com/apps/browse/ec?page=1&partnerLevel=All&product=AEM&q=experience+manager+translation&sort=RELEVANCE).

Después de instalar un paquete de conector, puede crear una configuración de la nube para él. Normalmente, debe proporcionar sus credenciales para autenticarse en el servicio de traducción. Para obtener información acerca de cómo añadir una configuración de la nube para el conector de Microsoft Translator, consulte [Integración con Microsoft Translator](/help/sites-administering/tc-msconf.md).

Si es necesario, puede crear varias configuraciones de nube para el mismo conector. Por ejemplo, cree una configuración para cada una de las cuentas o proyectos que tenga con el mismo proveedor.

Después de configurar una conexión, puede crear la configuración del marco de trabajo de integración de traducciones que la utiliza.

## Creación de una configuración de integración de traducción {#creating-a-translation-integration-configuration}

Cree una configuración del marco de trabajo de integración de traducciones para especificar cómo traducir el contenido. La configuración incluye la siguiente información:

* Qué proveedor de servicios de traducción utilizar.
* Si se va a realizar una traducción humana o automática.
* Si se debe traducir otro contenido asociado a una página o recurso, como etiquetas.

Después de crear una configuración de marco de trabajo, asocia la configuración de la nube con las páginas que desea traducir según la configuración. Cuando se inicia el proceso de traducción, el flujo de trabajo de traducción se ejecuta según la configuración del marco de trabajo asociada.

Cuando las diferentes secciones del sitio web tengan distintos requisitos de traducción, cree varias configuraciones de marco de trabajo según corresponda. Por ejemplo, un sitio web multilingüe incluye copias en inglés, español y japonés. El propietario del sitio utiliza dos proveedores de servicios de traducción diferentes para las traducciones al español y al japonés. Por lo tanto, se establecen dos configuraciones del marco de trabajo. Cada configuración utiliza un proveedor de servicios de traducción diferente.

Después de configurar un marco de trabajo de integración de traducciones, puede [asociarlo a las páginas](/help/sites-administering/tc-prep.md) que lo usan.

**Nota:** Para obtener una descripción general de las características de traducción de contenido de AEM, consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md).

Una sola configuración del marco de trabajo controla cómo traducir contenido de página y recursos.
![chlimage_1-386](assets/translation-config-65.jpg)

### Propiedades de configuración de sitios {#sites-configuration-properties}

Las propiedades de Sites controlan cómo se traduce el contenido de la página.

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Flujo de trabajo de traducción</td>
   <td><p>Seleccione el método de traducción que el marco de trabajo aplica al contenido del sitio:</p>
    <ul>
     <li>Traducción automática: el proveedor de traducción realiza la traducción mediante traducción automática en tiempo real.</li>
     <li>Traducción humana: el contenido se envía al proveedor de traducción para que lo traduzcan traductores. </li>
     <li>No traducir: el contenido no se envía para su traducción. Esto sirve para omitir ciertas divisiones de contenido que no se traducen, pero que podrían actualizarse con el contenido más reciente.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Proveedor de traducciones</td>
   <td>Seleccione el proveedor de traducción para llevar a cabo la traducción. Cuando se instala su conector correspondiente, aparece un proveedor en la lista.</td>
  </tr>
  <tr>
   <td>Categoría de contenido</td>
   <td>(Solo traducción automática) Una categoría que describe el contenido que está traduciendo. La categoría puede afectar a la elección de la terminología y el estilo al traducir el contenido.</td>
  </tr>
  <tr>
   <td>Traducir cadenas de componentes</td>
   <td>Seleccione esta opción para traducir las cadenas de componentes asociados a la página.</td>
  </tr>
  <tr>
   <td>Traducir etiquetas</td>
   <td>Seleccione para traducir las etiquetas asociadas con la página.</td>
  </tr>
  <tr>
   <td>Traducir recursos de la página</td>
   <td><p>Seleccione cómo traducir recursos que se añaden a componentes del sistema de archivos o a los que se hace referencia desde Assets:</p>
    <ul>
     <li>No traducir: los recursos de la página no se traducen.</li>
     <li>Uso del flujo de trabajo de traducción de sitios: Assets se gestiona según las propiedades de configuración de la pestaña Sitios.</li>
     <li>Uso del flujo de trabajo de traducción de Assets: Assets se gestiona según la configuración de las propiedades de la pestaña Assets.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Ejecutar traducción automáticamente</td>
   <td>Seleccione esta opción para ejecutar los trabajos de traducción automáticamente después de crear los proyectos. Cuando selecciona esta opción, no tiene la oportunidad de revisar y ampliar el ámbito del trabajo de traducción.</td>
  </tr>
 </tbody>
</table>

### Propiedades de configuración de recursos {#assets-configuration-properties}

Las propiedades de recursos controlan cómo se configuran los recursos. Para obtener más información acerca de la traducción de recursos, consulte [Creación de copias de idioma para los recursos](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>Propiedad</th>
   <th>Descripción</th>
  </tr>
  <tr>
   <td>Flujo de trabajo de traducción</td>
   <td><p>Seleccione el tipo de traducción que el marco de trabajo realiza para los recursos:</p>
    <ul>
     <li>Traducción automática: el proveedor de traducción realiza la traducción inmediatamente mediante traducción automática.</li>
     <li>Traducción humana: el contenido se envía automáticamente al proveedor de traducción para que lo traduzcan traductores. </li>
     <li>No traducir: Assets no se envía para su traducción.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Proveedor de traducciones</td>
   <td>Seleccione el proveedor de traducción para llevar a cabo la traducción. Cuando se instala su conector correspondiente, aparece un proveedor en la lista.</td>
  </tr>
  <tr>
   <td>Categoría de contenido</td>
   <td>(Solo traducción automática) Una categoría que describe el contenido que está traduciendo. La categoría puede afectar a la elección de la terminología y el estilo al traducir el contenido.</td>
  </tr>
  <tr>
   <td>Traducir recursos</td>
   <td>Seleccione esta opción para incluir recursos en el proyecto de traducción. </td>
  </tr>
  <tr>
   <td>Traducir metadatos</td>
   <td>Seleccione para traducir metadatos de recursos.</td>
  </tr>
  <tr>
   <td>Traducir etiquetas</td>
   <td>Seleccione esta opción para traducir las etiquetas asociadas al recurso.</td>
  </tr>
  <tr>
   <td>Ejecutar traducción automáticamente</td>
   <td>Seleccione esta opción para ejecutar los trabajos de traducción automáticamente después de crear los proyectos. Cuando selecciona esta opción, no tiene la oportunidad de revisar o ampliar el ámbito del trabajo de traducción.</td>
  </tr>
 </tbody>
</table>

1. En la barra lateral, haga clic en Herramientas > Operaciones > Cloud > Cloud Services.
1. En el área Integración de traducción, si se ha creado alguna configuración, determina qué vínculo aparece:

   * Si no se ha creado ninguna configuración, haga clic en Configurar ahora.
   * Si ya existen configuraciones, haga clic en Mostrar configuraciones y, a continuación, en el vínculo + que aparece junto a Configuraciones disponibles.

1. Escriba un nombre para la configuración y haga clic en Crear.
1. Configure las propiedades en la ficha Sitios y Assets y, a continuación, haga clic en Aceptar.

## Configuración de páginas para su traducción {#configuring-pages-for-translation}

Para configurar la traducción de las páginas de origen a otros idiomas, asócielas con las siguientes configuraciones de la nube:

* La configuración en la nube que conecta AEM con su proveedor de traducción.
* El marco de trabajo de integración de traducciones que configura los detalles de la traducción.

La configuración de nube del marco de trabajo de integración de traducciones identifica la configuración de nube que se utilizará para la conexión con el proveedor de servicios. Cuando asocia una página de origen con una configuración de nube de marco de trabajo, la página debe asociarse a la configuración de nube del proveedor de servicios que utiliza la configuración de nube de marco trabajo.

Cuando asocia una página con una configuración de nube, los descendientes de la página heredan la asociación. Por ejemplo, si asocia la página /content/geometrixx/en/products con un marco de trabajo de integración de traducciones, la página Products y todas las páginas por debajo se traducen según el marco de trabajo.

Si es necesario, puede anular la asociación en una página descendiente. Por ejemplo, el contenido de un sitio web se refiere principalmente a la ropa. Sin embargo, una rama de páginas describe la compañía. La página raíz del sitio está asociada a un marco de trabajo de integración de traducción que especifica la traducción automática mediante la categoría Ropa. La rama que describe la compañía utiliza un marco de trabajo que realiza la traducción automática mediante la categoría General.

### Asociación de una página con un proveedor de traducción {#associating-a-page-with-a-translation-provider}

Asocie una página al proveedor de traducción que esté utilizando para traducir la página y las páginas descendientes.

1. En la consola Sitios, seleccione la página que desea configurar y haga clic en Ver propiedades.
1. Haga clic en Editar y luego en la pestaña Cloud Services.
1. Haga clic en Agregar configuración > Integración de traducción.
1. Seleccione el proveedor de traducción que desee utilizar y, a continuación, haga clic en Listo.

### Asociación de páginas a un marco de trabajo integración de traducción {#associating-pages-with-a-translation-integration-framework}

Asocie una página al marco de trabajo de integración de traducción que define cómo desea realizar la traducción de la página y de las páginas descendientes.

1. En la consola Sitios, seleccione la página que desea configurar y haga clic en Ver propiedades.
1. Haga clic en Editar y luego en la pestaña Cloud Services.
1. Haga clic en Agregar configuración > Integración de traducción.
1. Seleccione el marco de trabajo de integración de traducciones que desea utilizar y haga clic en Listo.
