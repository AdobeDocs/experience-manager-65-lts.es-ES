---
title: Listado de formularios en una página web mediante API
description: Consulte Forms Manager mediante programación para recuperar una lista filtrada de formularios y mostrarla en sus propias páginas web.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
solution: Experience Manager, Experience Manager Forms
feature: Forms Portal
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 100%

---

# Listado de formularios en una página web mediante API {#listing-forms-on-a-web-page-using-apis}

AEM Forms proporciona una API de búsqueda basada en REST que los desarrolladores web pueden utilizar para consultar y recuperar un conjunto de formularios que cumplan los criterios de búsqueda. Las API se pueden usar para buscar formularios basados en distintos filtros. El objeto response contiene atributos de formulario, propiedades y extremos de procesamiento de formularios.

Para buscar formularios utilizando la API de REST, envíe una petición GET al servidor de `https://'[server]:[port]'/libs/fd/fm/content/manage.json` con los parámetros de consulta que se describen a continuación.

## Parámetros de consulta {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nombre del atributo<br /> </strong></td>
   <td><strong>Descripción<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>Especifica la función a la que se va a llamar. Para buscar formularios, establezca el valor del atributo <code>func </code> en <code>searchForms</code>.</p> <p>Por ejemplo, <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>Nota:</strong> <em>Este parámetro es obligatorio.</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>Especifica la ruta de la aplicación para buscar formularios. De forma predeterminada, el atributo appPath busca todas las aplicaciones disponibles en el nivel del nodo raíz.<br /> </p> <p>Puede especificar varias rutas de aplicación en una sola consulta de búsqueda. Separe las diferentes rutas con el carácter de barra vertical (|). </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>Especifica las propiedades que se recuperarán con los recursos. Puede usar un asterisco (*) para recuperar todas las propiedades a la vez. Utilice el operador de barra vertical (|) para especificar varias propiedades. </p> <p>Por ejemplo, <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>Nota</strong>: </p>
    <ul>
     <li><em>Las propiedades como id, path y name se recuperan siempre. </em></li>
     <li><em>Cada recurso tiene un conjunto diferente de propiedades. Las propiedades como formUrl, pdfUrl y guideUrl no dependen del atributo cutpoints. Estas propiedades dependen del tipo de recurso y se recuperan según corresponda. </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>Especifica los recursos relacionados que se recuperarán junto con los resultados de búsqueda. Puede elegir una de las siguientes opciones para recuperar recursos relacionados:
    <ul>
     <li><strong>NO_RELATION</strong>: no recupere recursos relacionados.</li>
     <li><strong>IMMEDIATE</strong>: recupera recursos que están directamente relacionados con los resultados de búsqueda.</li>
     <li><strong>ALL</strong>: recupere recursos relacionados directa e indirectamente.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>Especifica el número máximo de formularios que se van a recuperar.</td>
  </tr>
  <tr>
   <td>offset</td>
   <td>Especifica el número de formularios que se omitirán desde el inicio.</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>Especifica si se devuelven o no los resultados de búsqueda que coinciden con el criterio dado. </td>
  </tr>
  <tr>
   <td>statements</td>
   <td><p>Especifica la lista de instrucciones. Las consultas se ejecutan en la lista de las instrucciones especificadas en el formato JSON. </p> <p>Por ejemplo,</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>En el ejemplo anterior, </p>
    <ul>
     <li><strong>name</strong>: especifica el nombre de la propiedad que se va a buscar.</li>
     <li><strong>value</strong>: especifica el valor de la propiedad que se va a buscar.</li>
     <li><strong>operator</strong>: especifica el operador que se aplicará durante la búsqueda. Se admiten los siguientes operadores:
      <ul>
       <li>EQ: igual a </li>
       <li>NEQ: no igual a</li>
       <li>GT: mayor que</li>
       <li>LT: menor que</li>
       <li>GTEQ: mayor o igual que</li>
       <li>LTEQ: menor o igual que</li>
       <li>CONTAINS: A contiene B si B es parte de A</li>
       <li>FULLTEXT: búsqueda de texto completo</li>
       <li>STARTSWITH: A comienza con B si B es la parte inicial de A</li>
       <li>ENDSWITH: A termina con B si B es la parte final de A</li>
       <li>LIKE: implementa el operador LIKE</li>
       <li>AND: combina varias instrucciones</li>
      </ul> <p><strong>Nota:</strong> <em>Los operadores GT, LT, GTEQ y LTEQ se aplican a propiedades de tipo lineal como LONG, DOUBLE y DATE.</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>orderings<br /> </td>
   <td><p>Especifica los criterios de ordenación para los resultados de búsqueda. Los criterios se definen en el formato JSON. Puede ordenar los resultados de búsqueda en más de un campo. Los resultados se ordenan en el orden en el que aparecen los campos en la consulta.</p> <p>Por ejemplo,</p> <p>Para recuperar los resultados de consulta ordenados por la propiedad title en orden ascendente, agregue el siguiente parámetro: </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>name</strong>: especifica el nombre de la propiedad que se utiliza para ordenar los resultados de búsqueda.</li>
     <li><strong>criteria</strong>: especifica el orden de los resultados. El atributo order acepta los siguientes valores:
      <ul>
       <li>ASC: utilice ASC para organizar los resultados en orden ascendente.<br /> </li>
       <li>DES: utilice DES para organizar los resultados en orden descendente.</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>Especifica si se recupera el contenido binario o no. El atributo <code>includeXdp</code> es aplicable a los recursos de tipo <code>FORM</code>, <code>PDFFORM</code> y <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>Especifica los tipos de recurso que se recuperarán de todos los recursos publicados. Utilice el operador de barra vertical (|) para especificar varios tipos de recursos. Los tipos de recursos válidos son FORM, PDFFORM, PRINTFORM, RESOURCE y GUIDE.</td>
  </tr>
 </tbody>
</table>

## Solicitud de ejemplo {#sample-request}

```json
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :"lastModifiedDate":"order":"ASC"}]
```

## Respuesta de ejemplo {#sample-response}

```json
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## Artículos relacionados

* [Habilitar componentes del portal de formularios](/help/forms/using/enabling-forms-portal-components.md)
* [Creación de una página del portal de formularios](/help/forms/using/creating-form-portal-page.md)
* [Enumerar formularios en una página web mediante API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar el componente Borradores y envíos](/help/forms/using/draft-submission-component.md)
* [Personalizar el almacenamiento de borradores y formularios enviados](/help/forms/using/draft-submission-component.md)
* [Ejemplo para integrar el componente Borradores y envíos con la base de datos](/help/forms/using/integrate-draft-submission-database.md)
* [Personalizar plantillas para componentes del portal de formularios](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introducción a la publicación de formularios en un portal](/help/forms/using/introduction-publishing-forms.md)
