---
title: Creación de un nuevo componente de campo de IU de Granite
description: La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios, denominados campos
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Creación de un nuevo componente de campo de IU de Granite{#creating-a-new-granite-ui-field-component}

La interfaz de usuario de Granite proporciona una serie de componentes diseñados para utilizarse en formularios; estos se denominan *campos* en el vocabulario de la interfaz de usuario de Granite. Los componentes de formulario estándar de Granite están disponibles en:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>Estos campos de formulario de la interfaz de usuario de Granite son de particular interés ya que se utilizan para [cuadros de diálogo de componentes](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Para obtener información detallada sobre los campos, consulte la [documentación de Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Utilice el marco de trabajo Granite UI Foundation para desarrollar o ampliar componentes de Granite. Tiene dos elementos:

* del lado del servidor:

   * una colección de componentes de base

      * base: modular, componible, capas, reutilizable
      * componentes: componentes de Sling

   * ayudantes para el desarrollo de aplicaciones

* lado del cliente:

   * una colección de clientlibs que proporciona cierto vocabulario (es decir, extensión del lenguaje HTML) para lograr patrones de interacción genéricos a través de una interfaz de usuario impulsada por hipermedia.

El componente genérico de Granite UI `field` está compuesto por dos archivos de interés:

* `init.jsp`: administra el procesamiento genérico; el etiquetado, la descripción y proporciona el valor de formulario que necesita al procesar el campo.
* `render.jsp`: aquí es donde se realiza la representación real del campo, que debe anularse para el campo personalizado; incluido por `init.jsp`.

Consulte la [documentación de Granite UI - Campo](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) para obtener detalles.

Para ver ejemplos, consulte:

* `cqgems/customizingfield/components/colorpicker`

   * proporcionado por [Ejemplo de código](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>Como este mecanismo utiliza JSP, i18n y XSS no se proporcionan listas para usar. Esto significa que debe internacionalizarse y escapar de sus cadenas. El siguiente directorio contiene los campos genéricos de una instancia estándar, que puede utilizar como referencia:
>
>`/libs/granite/ui/components/foundation/form` directorio

## Creación del script del lado del servidor para el componente {#creating-the-server-side-script-for-the-component}

El campo personalizado solo debe invalidar el script `render.jsp`, donde se proporciona el marcado para el componente. Puede considerar JSP (es decir, el script de procesamiento) como un envoltorio para el marcado.

1. Cree un componente que use la propiedad `sling:resourceSuperType` para heredar de:

   `/libs/granite/ui/components/foundation/form/field`

1. Anule la secuencia de comandos:

   `render.jsp`

   En este script, genere el marcado hipermedia (es decir, marcado enriquecido, que contiene la asequibilidad de hipermedia) para que el cliente sepa cómo interactuar con el elemento generado. Esto debe seguir el estilo de codificación del lado del servidor de Granite UI.

   Al personalizar, el único contrato que *debe* cumplir es leer el valor del formulario (inicializado en `init.jsp`) de la solicitud mediante:

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   Para obtener más información, consulte la implementación de los campos predeterminados de Granite UI; por ejemplo, `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >Por el momento, JSP es el método de script preferido, ya que pasar información de un componente a otro (que es frecuente en el contexto de formularios/campos) no se logra fácilmente en HTL.

## Creación de la biblioteca de cliente para el componente {#creating-the-client-library-for-the-component}

Para agregar un comportamiento específico del lado del cliente al componente:

1. Cree una clientlib de categoría `cq.authoring.dialog`.
1. Cree una clientlib de categoría `cq.authoring.dialog` y defina su `JS`/ `CSS` dentro de ella.

   Defina su `JS`/ `CSS` dentro de clientlib.

   >[!NOTE]
   >
   >Por el momento, la interfaz de usuario de Granite no proporciona escuchas o enlaces predeterminados que pueda utilizar directamente para agregar el comportamiento de JS. Por lo tanto, para agregar un comportamiento JS adicional al componente, debe implementar un vínculo JS a una clase personalizada que luego asigne al componente durante la generación de marcado.
