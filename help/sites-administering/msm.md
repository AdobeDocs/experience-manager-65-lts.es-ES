---
title: 'Reutilización del contenido: administrador de varios sitios y Live Copy'
description: Obtenga información sobre cómo reutilizar contenido con Live Copies y el Administrador de varios sitios.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Multi Site Manager
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '2665'
ht-degree: 19%

---

# Reutilización del contenido: administrador de varios sitios y Live Copy{#reusing-content-multi-site-manager-and-live-copy}

Administrador de varios sitios (MSM) le permite utilizar el mismo contenido del sitio en varias ubicaciones. MSM utiliza su funcionalidad de Live Copy para lograr lo siguiente:

* Con MSM puede lograr lo siguiente:

   * Crear contenido una vez y después
   * Copie este contenido y reúna este contenido en otras áreas ([Live Copies](#live-copies)) del mismo sitio u otros.

* A continuación, MSM mantiene las relaciones (activas) entre el contenido de origen y sus Live Copies para lo siguiente:

   * Al cambiar el contenido de origen, el origen y las Live Copies se sincronizan (para aplicar estos cambios a las Live Copies también).
   * Puede ajustar el contenido de las Live Copies desconectando la relación activa para subpáginas individuales, componentes o ambos. Al hacerlo, los cambios en el origen ya no se aplican a la Live Copy.

Esta y las siguientes páginas tratan sobre los problemas relacionados:

* [Creación y sincronización de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Información general de Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuración de la sincronización de Live Copy](/help/sites-administering/msm-sync.md)
* [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md)
* [Prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md)

## Posibles escenarios {#possible-scenarios}

Existen muchos casos de uso para MSM y Live Copies, algunos de los cuales incluyen:

* **Multinacionales: empresa global a local**

  Un caso de uso típico que admite MSM es reutilizar contenido en varios sitios multinacionales en el mismo idioma. Esto permite reutilizar el contenido principal, aunque admite variaciones nacionales.

  Por ejemplo, la sección en inglés de la muestra del sitio de referencia de We.Retail se crea para los clientes de EE. UU. La mayor parte del contenido de este sitio también puede utilizarse para otros sitios de We.Retail que atienden a clientes de habla inglesa de diferentes países y culturas. El contenido principal sigue siendo el mismo en todos los sitios, mientras que se pueden llevar a cabo ajustes regionales.

  La siguiente estructura se puede utilizar para sitios de Estados Unidos, Reino Unido, Canadá y Australia:

  ```xml
  /content
      |- we.retail
          |- language-masters
              |- en
      |- we.retail
          |- us
              |- en
      |- we.retail
          |- gb
              |- en
      |- we.retail
          |- ca
              |- en
      |- we.retail
          |- au
              |- en
  ```

  >[!NOTE]
  >
  >MSM no traduce el contenido. Se utiliza para crear la estructura necesaria e implementar el contenido.
  >
  >
  >Consulte [Traducción de contenido para sitios multilingües](/help/sites-administering/translation.md) si desea ampliar un ejemplo de este tipo.

* **Nacional: de la sede central a las subdivisiones regionales**

  Alternativamente, una empresa con una red de distribuidores podría querer sitios web separados para sus concesionarios individuales, cada uno de los cuales es una variación del sitio principal proporcionado por la sede central. Esto podría ser para una sola empresa con múltiples oficinas regionales, o un sistema nacional de franquicias compuesto por un franquiciador central y múltiples franquicias locales.

  La sede central puede proporcionar la información básica, mientras que las entidades regionales pueden añadir información local, como detalles de contacto, horarios de apertura y eventos.

  ```xml
  /content
      |- head-office-Berlin
      |- branch-Hamburg
      |- branch-Stuttgart
      |- branch-Munich
      |- branch-Frankfurt
  ```

* **Varias versiones**

  O puede utilizar MSM para crear versiones de una subrama específica. Por ejemplo, un subsitio de asistencia que contiene detalles de las distintas versiones de un producto específico, donde la información base permanece constante y solo se deben cambiar las funciones actualizadas:

  ```xml
  /content
      |- support
          |- product X
              |- v5.0
              |- v4.0
              |- v3.0
              |- v2.0
              |- v1.0
  ```

  >[!NOTE]
  >
  >En este caso, debe decidir si realizar una copia directa o utilizar Live Copies.
  >
  >Hay un equilibrio de:
  >
  >  * La cantidad de contenido principal que debe actualizarse en las distintas versiones.
  >
  >Frente a:
  >
  >  * La cantidad de copias individuales que deben ajustarse.

## MSM desde la IU {#msm-from-the-ui}

Se puede acceder directamente a MSM desde la IU mediante varias opciones desde la consola adecuada. Para proporcionar una introducción, a continuación se enumeran las ubicaciones principales:

* **Crear sitio** (**Sitios**)

   * MSM le ayuda a administrar varios sitios web que comparten contenido común. Por ejemplo: los sitios web suelen estar destinados a audiencias internacionales, de modo que la mayor parte del contenido es común en todos los países, con un subconjunto del contenido específico de cada país. MSM le permite [crear Live Copies que actualicen automáticamente uno o más sitios según su sitio de origen](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Esto también le ayuda a aplicar una estructura base común, utilizar el contenido común en varios sitios, mantener un aspecto y un enfoque comunes y enfocar los esfuerzos en administrar el contenido que difiere entre los sitios.
   * Requiere una configuración de modelo predefinida para especificar el origen.
   * Crea una Live Copy del origen (predefinido).
   * Proporciona al usuario el botón **Despliegue**.

* **Creación de Live Copy** (**Sites**)

   * MSM le permite [crear una Live Copy ad-hoc (única) de una página o subrama individual de un sitio web](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page); por ejemplo, duplicar una subrama para proporcionar información sobre una versión nueva o actualizada de un producto.
   * Crea una Live Copy ad-hoc (no se requiere configuración de modelo).
   * Se puede utilizar para crear (inmediatamente) una Live Copy de cualquier página o rama.
   * Requiere **Sincronizar** (no proporciona el botón **Despliegue**).

* **Ver propiedades** (**Sitios**)

   * Si corresponde, esta opción le ayuda a [monitorizar Live Copy](/help/sites-administering/msm-livecopy.md#monitoring-your-live-copy) al proporcionar información sobre **Live Copy** y o **modelo** relacionados.

* **Referencias** (**Sitios**)

   * El carril [Referencias](/help/sites-authoring/basic-handling.md#references) proporciona información sobre **Live Copies** junto con el acceso a las acciones adecuadas.

* **Información general de Live Copy** (**Sites**)

   * Esta consola le permite [ver y administrar su modelo y sus Live Copies](/help/sites-administering/msm-livecopy-overview.md).

* **Modelos** (**Herramientas** - **Sites**)

   * Esta consola le permite [crear y administrar sus configuraciones de modelo](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration).

>[!NOTE]
>
>MSM se puede usar con ambas páginas y [Fragmentos de experiencias](/help/sites-authoring/experience-fragments.md), ya que estos fragmentos son parte de una experiencia (página).

>[!NOTE]
>
>Los aspectos de la funcionalidad de MSM se utilizan en varias otras funciones de Adobe Experience Manager (AEM) (por ejemplo, Inicios, Catálogo); en estos casos, esa función administra Live Copy.

### Términos utilizados {#terms-used}

Como introducción, la siguiente tabla proporciona una descripción general de los términos principales utilizados con MSM; se tratan con más detalle en las secciones y páginas siguientes:

<table>
 <tbody>
  <tr>
   <td><strong>Término</strong></td>
   <td><strong>Definición</strong></td>
   <td><strong>Más información</strong></td>
  </tr>
  <tr>
   <td><strong>Origen</strong></td>
   <td>Las páginas originales.</td>
   <td>Sinónimo de páginas de modelos o modelos.</td>
  </tr>
  <tr>
   <td><strong>Live Copy</strong></td>
   <td>La copia (del origen), mantenida mediante acciones de sincronización definidas según las configuraciones de despliegue. </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configuración de Live Copy</strong></td>
   <td>Definición de los detalles de configuración de una Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Relación activa</strong><br /> </td>
   <td>Definición efectiva de la herencia para un recurso determinado; las conexiones entre el origen y Live Copies.<br /> </td>
   <td>Garantiza que los cambios en el origen se puedan sincronizar con la Live Copy.</td>
  </tr>
  <tr>
   <td><strong>Modelo</strong></td>
   <td>Sinónimo de Source.</td>
   <td>Se puede definir mediante una configuración de modelo.</td>
  </tr>
  <tr>
   <td><strong>Configuración del modelo</strong></td>
   <td>Configuración predefinida que especifica una ruta de origen.</td>
   <td>Cuando se hace referencia a una página de modelo en una configuración de modelo, el comando Despliegue está disponible.</td>
  </tr>
  <tr>
   <td><strong>Sincronización</strong></td>
   <td>Término genérico para la sincronización de contenido entre el origen y las Live Copies (por <strong>Despliegue</strong> y <strong>Sincronizar</strong>).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Despliegue</strong><br /> </td>
   <td>Sincroniza desde el origen a la Live Copy.<br />: se puede activar mediante un autor (en una página de modelo) o mediante un evento del sistema (tal como se define en la configuración de despliegue).</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Configuración de despliegue</strong></td>
   <td>Reglas que determinan qué propiedades se sincronizan, cómo y cuándo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Sincronizar</strong></td>
   <td>Solicitud manual de sincronización, realizada desde las páginas de Live Copy.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Herencia</strong></td>
   <td>Una página o componente de Live Copy hereda contenido de su página o componente de origen cuando se produce la sincronización.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Suspender</strong></td>
   <td>Elimina temporalmente la relación activa entre una Live Copy y su página de modelo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Desasociar</strong></td>
   <td>Elimina permanentemente la relación activa entre una Live Copy y su página de modelo.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Restablecer</strong></td>
   <td><p>Restablecer una página de Live Copy a:</p>
    <ul>
     <li>Quitar todas las cancelaciones de herencia y <br /> </li>
     <li>Devuelva la página al mismo estado que la página de origen.</li>
    </ul> <p>Restablecer afecta a los cambios realizados en las propiedades de la página, el sistema de párrafos y los componentes.</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Superficial</strong></td>
   <td>Una Live Copy de una sola página.</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Profundo</strong></td>
   <td>Una Live Copy de una página, junto con sus páginas secundarias.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Consulte [Información general de la API de Java™](/help/sites-developing/extending-msm.md#overview-of-the-java-api) para ver los nombres de los objetos.

## Live Copies {#live-copies}

Una Live Copy de MSM es una copia de contenido de un sitio específico que mantiene una relación activa con el origen:

* La Live Copy hereda el contenido de su origen.
* La sincronización realiza la transferencia real de contenido cuando se realizan cambios en el origen.
* Una Live Copy puede considerarse como lo siguiente:

   * Superficial: una sola página
   * Profundo: la página, junto con sus páginas secundarias

* Las reglas de sincronización denominadas configuraciones de despliegue determinan qué propiedades se sincronizan y cuándo se produce la sincronización.

En el ejemplo anterior, `/content/we-retail/language-masters/en` es la ubicación maestra global en inglés. Para reutilizar el contenido de este sitio, se crean Live Copies de MSM:

* El contenido siguiente `/content/we-retail/language-masters/en` es el origen.

* El contenido siguiente a `/content/we-retail/language-masters/en` se copia debajo de los nodos `/content/we-retail/us/en/`, `/content/we-retail/gb/en`, `/content/we-retail/ca/en` y `/content/we-retail/au/en`. Estas son las Live Copies.

* Los autores pueden cambiar de página por debajo de `/content/we-retail/language-masters/en`.
* Cuando se activa, MSM sincroniza estos cambios con las Live Copies.

### Live Copies: composición {#live-copies-composition}

>[!NOTE]
>
>Los diagramas y las descripciones de esta sección representan instantáneas de posibles Live Copies. No son exhaustivas, pero ofrecen una descripción general para resaltar características específicas.

Cuando crea una Live Copy, las páginas de origen seleccionadas se reflejan en 1:1 en Live Copy. Después de esto, también se pueden crear nuevos recursos (páginas o párrafos) directamente dentro de la Live Copy, por lo que es útil tener en cuenta estas variaciones y cómo afectan a la sincronización. Las posibles composiciones incluyen las siguientes:

* [Live Copy con páginas que no sean de Live Copy](#live-copy-with-non-live-copy-pages)
* [Live Copies anidadas](#nested-live-copies)

La forma básica de Live Copy tiene lo siguiente:

* Páginas de Live Copy que reflejen las páginas de origen seleccionadas de forma individual.
* Una definición de configuración.
* Una relación activa definida para cada recurso:

   * Vincule el recurso de Live Copy con su modelo u origen.
   * Se utiliza para realizar la herencia y el despliegue.

* Los cambios se pueden [sincronizar](/help/sites-administering/msm-livecopy.md#synchronizing-your-live-copy) según los requisitos.

![Sincronizar](assets/chlimage_1-367.png)

#### Live Copy con páginas que no sean de Live Copy {#live-copy-with-non-live-copy-pages}

Cuando crea una Live Copy en AEM, puede ver y navegar por la rama de Live Copy y utilizar la funcionalidad normal de AEM en la rama de Live Copy. Esto significa que usted (o un proceso) puede crear recursos (páginas, párrafos o ambos) dentro de la rama de Live Copy. Por ejemplo, `myCanadaOnlyProduct`.

* Estos recursos no tienen relación activa con las páginas de origen/modelo y no se sincronizan.
* Pueden producirse escenarios que el MSM gestione como casos especiales. Por ejemplo, cuando usted (o un proceso) crea una página con la misma posición y el mismo nombre en las ramas de origen/modelo y Live Copy. Para estas situaciones, consulte [Conflictos de despliegue de MSM](/help/sites-administering/msm-rollout-conflicts.md) para obtener más información.

![Conflictos de despliegue](assets/chlimage_1-368.png)

#### Live Copies anidadas {#nested-live-copies}

Cuando usted (o un proceso) crea una página [dentro de una Live Copy existente](#live-copy-with-non-live-copy-pages), esta nueva página también se puede configurar como una Live Copy de un modelo diferente. Esto se conoce como Live Copy anidada, donde el comportamiento de la segunda Live Copy (interna) se ve afectado por la primera Live Copy (externa) de la siguiente manera:

* Se puede continuar con un despliegue profundo activado para Live Copy de nivel superior en la Live Copy anidada (por ejemplo, si el déclencheur coincide).
* Cualquier vínculo entre los orígenes se reescribe dentro de las Live Copies.

  Por ejemplo, los vínculos del segundo al primer modelo se reescriben como vínculos de la Live Copy anidada/segunda a la primera Live Copy.

![Vínculos entre orígenes](assets/chlimage_1-369.png)

>[!NOTE]
>
>Si mueve o cambia el nombre de una página dentro de la rama de Live Copy, esto se trata (internamente) como una Live Copy anidada para permitir que AEM rastree las relaciones.

#### Copias activas apiladas {#stacked-live-copies}

Una Live Copy se conoce como Live Copy apilada cuando se crea como el elemento secundario de una Live Copy superficial. Se comporta de la misma manera que una [Live Copy anidada](#nested-live-copies).

### Configuraciones de Source, modelos y modelos {#source-blueprints-and-blueprint-configurations}

Cualquier página o rama de páginas puede utilizarse como origen de una Live Copy.

Sin embargo, MSM también le permite definir una configuración de modelo que especifica una ruta de origen. Los beneficios de utilizar una configuración de modelo son los siguientes:

* Permiten que el autor use la opción **Despliegue** en un modelo para insertar (explícitamente) modificaciones en Live Copies que hereden de este modelo.
* Permitir que el autor use **Crear sitio**; esto permite al usuario seleccionar idiomas fácilmente y configurar la estructura de la Live Copy.
* Defina una configuración de despliegue predeterminada para Live Copies que tengan una relación con el modelo.

El origen de una Live Copy pueden ser tanto páginas normales como páginas incluidas en una configuración de modelo; ambos son casos de uso válidos.

El origen forma el modelo para la Live Copy. El modelo se define al:

* [Crear una configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration)

  La configuración define (por adelantado) las páginas que se utilizarán para crear la Live Copy.

* [Crear una Live Copy de una página](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

  Las páginas utilizadas para crear la Live Copy (las páginas de origen) son las páginas de modelo.

  Una configuración de modelo puede hacer referencia a la página de origen o no.

### Desplegar y sincronizar {#rollout-and-synchronize}

Un despliegue es la acción central de MSM que sincroniza Live Copies con su origen. Puede realizar despliegues manualmente o pueden producirse automáticamente:

* Una [configuración de despliegue](#rollout-configurations) puede definirse de modo que [eventos](/help/sites-administering/msm-sync.md#rollout-triggers) específicos puedan provocar un despliegue automáticamente.
* Al crear una página de modelo, puede usar el comando [Despliegue](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) para insertar cambios en la Live Copy.

  **El comando Despliegue** está disponible en una página de modelo a la que hace referencia una configuración de modelo.

  ![Despliegue](assets/chlimage_1-370.png)

* Al crear una página de Live Copy, puede usar el comando [Sincronizar](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) para extraer cambios del origen a la Live Copy.

  El comando **Sincronizar** siempre está disponible en la página de Live Copy (independientemente de si la página de origen/modelo está incluida en una configuración de modelo).

  ![Sincronizar](assets/chlimage_1-371.png)

### Opciones de configuración del lanzamiento {#rollout-configurations}

Una configuración de despliegue define cuándo y cómo se sincroniza una Live Copy con el contenido de origen. Una configuración de despliegue consta de un activador y una o más acciones de sincronización:

* **Déclencheur**

  Un déclencheur es un evento que hace que se produzca la acción de sincronización dinámica, como la activación de una página de origen. MSM define los activadores que puede utilizar.

* **Acciones de sincronización**

  Se realiza en la Live Copy para sincronizarla con el origen. Algunas acciones de ejemplo son copiar contenido, ordenar nodos secundarios y activar la página de Live Copy. MSM proporciona varias acciones de sincronización.

  >[!NOTE]
  >
  >Puede crear acciones personalizadas para su instancia mediante la API de Java™.

Las configuraciones de despliegue se pueden reutilizar, de modo que más de una Live Copy pueda utilizar la misma configuración de despliegue. Varias [configuraciones de despliegue](/help/sites-administering/msm-sync.md#installed-rollout-configurations) se incluyen en una instalación estándar.

### Despliegue de conflictos {#rollout-conflicts}

Los despliegues se pueden complicar, especialmente cuando los autores editan contenido tanto en el origen como en la Live Copy, por lo que es útil tener en cuenta cómo AEM gestiona los [conflictos que pueden producirse durante el despliegue](/help/sites-administering/msm-rollout-conflicts.md).

### Suspender y cancelar la herencia y sincronización {#suspending-and-cancelling-inheritance-and-synchronization}

Cada página y componente de una Live Copy está asociado con su página de origen y componente a través de una relación dinámica. La relación dinámica configura la sincronización de contenido de Live Copy desde el origen.

Puede **Suspender** la herencia de Live Copy de una página de Live Copy para poder cambiar las propiedades y los componentes de la página. Al suspender la herencia, las propiedades y los componentes de la página ya no se sincronizan con el origen.

Al editar una página individual, los autores pueden **Cancelar la herencia** de un componente. Cuando se cancela la herencia, la relación dinámica se suspende y la sincronización no se produce para ese componente. Cancelar la herencia y la sincronización resulta útil cuando se deben personalizar las subsecciones del contenido.

### Desasociación de una Live Copy {#detaching-a-live-copy}

También puede [desasociar una Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) de su modelo para eliminar todas las conexiones.

>[!CAUTION]
>
>La acción Desasociar es permanente e irreversible.

La opción Desasociar elimina permanentemente la relación activa entre una Live Copy y su página de modelo. Todas las propiedades relevantes para MSM se eliminan de la Live Copy y las páginas de Live Copy se convierten en una copia independiente.

>[!NOTE]
>
>Consulte [Desasociar una Live Copy](/help/sites-administering/msm-livecopy.md#detaching-a-live-copy) para obtener información detallada; incluido el impacto relacionado en las páginas principales y secundarias.

## Pasos estándar para usar MSM {#standard-steps-for-using-msm}

Los siguientes pasos describen el procedimiento estándar para utilizar MSM para reutilizar contenido y sincronizar cambios en Live Copies.

1. Desarrollar el contenido del sitio de origen.
1. Determine la configuración de despliegue que desea utilizar.

   1. MSM [instala varias configuraciones de despliegue](/help/sites-administering/msm-sync.md#installed-rollout-configurations) que pueden satisfacer varios casos de uso.
   1. Opcionalmente, puede [crear una configuración de despliegue](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) si es necesario.

1. Determine dónde debe [especificar las configuraciones de despliegue que se usarán](/help/sites-administering/msm-sync.md#specifying-the-rollout-configurations-to-use) y configúrelas según sea necesario.
1. Si es necesario, [cree una configuración de modelo](/help/sites-administering/msm-livecopy.md#creating-a-blueprint-configuration) que identifique el contenido de origen de Live Copy.
1. [Crear una Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy).
1. Cambie el contenido de origen según sea necesario. Utilice el proceso normal de revisión y aprobación de contenido que ha establecido su organización.
1. [Despliegue](/help/sites-administering/msm-livecopy.md#rolling-out-a-blueprint) el modelo o [sincronice la Live Copy](/help/sites-administering/msm-livecopy.md#synchronizing-a-live-copy) con los cambios.

## Personalización de MSM {#customizing-msm}

MSM proporciona herramientas para que su implementación se pueda adaptar a las complejidades excepcionales que pueden existir al compartir contenido:

* **Configuraciones de despliegue personalizadas**
  [Crear una configuración de despliegue](/help/sites-administering/msm-sync.md#creating-a-rollout-configuration) cuando las configuraciones de despliegue instaladas no cumplan con sus requisitos. Puede utilizar cualquier activador de despliegue y acción de sincronización disponible.

* **Acciones de sincronización personalizadas**
  [Cree una acción de sincronización personalizada](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) cuando las acciones instaladas no cumplan los requisitos específicos de la aplicación. MSM proporciona una API de Java™ para crear acciones de sincronización personalizadas.

## Prácticas recomendadas {#best-practices}

La página [Prácticas recomendadas de MSM](/help/sites-administering/msm-best-practices.md) contiene información importante sobre la implementación.
