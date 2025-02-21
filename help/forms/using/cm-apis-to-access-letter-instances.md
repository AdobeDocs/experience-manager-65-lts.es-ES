---
title: API para acceder a instancias de carta
description: Descubra las API y utilícelas para acceder mediante programación a instancias de carta en el entorno de AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 62%

---

# API para acceder a instancias de carta {#apis-to-access-letter-instances}

## Información general {#overview}

Mediante la IU Crear correspondencia de Administración de correspondencia, puede guardar borradores de instancias de carta en curso y hay instancias de carta enviadas.

Administración de correspondencia proporciona varias API que permiten crear la interfaz del listado para trabajar con instancias de cartas enviadas o borradores. Las API enumeran y abren las instancias de carta en Borradores y enviados de un agente, de modo que el agente pueda trabajar en las instancias de carta en Borradores o enviados.

## Obtener instancias de cartas {#fetching-letter-instances}

Administración de correspondencia expone las API para recuperar instancias de carta a través del servicio LetterInstanceService.

| Método | Descripción |
|--- |--- |
| getAllLetterInstances | Obtiene instancias de cartas basadas en el parámetro de consulta de entrada. Para recuperar todas las instancias de cartas, apruebe el parámetro de consulta como nulo. |
| getLetterInstance | Obtiene la instancia de carta especificada en función del ID de instancia de carta. |
| letterInstanceExists | Comprueba si existe una instancia de carta por el nombre dado. |

>[!NOTE]
>
>LetterInstanceService es un servicio OSGI y su instancia se puede recuperar mediante @Reference en Java™
>Class o sling.getService(LetterInstanceService. Class ) en JSP.

### Usar getAllLetterInstances {#using-nbsp-getallletterinstances}

La siguiente API encuentra las instancias de la carta en función del objeto de consulta (tanto enviados como borradores). Si el objeto de consulta es nulo, devolverá todas las instancias de cartas. Esta API devuelve una lista de [objetos LetterInstanceVO](https://helpx.adobe.com/es/aem-forms/6-2/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html), que pueden utilizarse para extraer información adicional de la instancia de carta.

**Sintaxis**: `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Parámetro</strong></td>
   <td><strong>Descripción</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>El parámetro query se utiliza para buscar/filtrar la instancia Carta. Aquí, la consulta solo admite atributos o propiedades de nivel superior del objeto. Query consiste en instrucciones y el “attributeName” utilizado en el objeto de instrucción debe ser el nombre de la propiedad en el objeto de la instancia Carta.<br /> </td>
  </tr>
 </tbody>
</table>

#### Ejemplo 1: Recupere todas las instancias de cartas del tipo ENVIADO {#example-fetch-all-the-letter-instances-of-type-submitted}

El siguiente código devuelve la lista de instancias de carta enviadas. Para obtener solo borradores, cambie el `LetterInstanceType.COMPLETE.name()` a `LetterInstanceType.DRAFT.name().`

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### Ejemplo 2: Recupere todas las instancias de carta enviadas por un usuario y el tipo de instancia de carta es BORRADOR {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

El siguiente código tiene varias instrucciones en la misma consulta para obtener los resultados filtrados según diferentes criterios, como la instancia de carta enviada (atributo submittedby) por un usuario y el tipo de letterInstanceType es BORRADOR.

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### Usar getLetterInstance {#using-nbsp-getletterinstance}

Recupere la instancia de carta identificada por el ID de instancia de carta dado. Devuelve “null” si no coincide el ID de instancia.

**Sintaxis:** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Comprobar si existe LetterInstance {#verifying-if-letterinstance-exist}

Comprobar si existe una instancia de carta con el nombre dado

**Sintaxis**: `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Parámetro** | **Descripción** |
|---|---|
| letterInstanceName | Nombre de la instancia de carta que desea comprobar si existe. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Abrir instancias de carta {#opening-letter-instances}

La instancia de carta puede ser del tipo Enviado o Borrador. Al abrir ambos tipos de instancias de cartas, se muestran comportamientos diferentes:

* Si hay una instancia de carta Enviada, se abre una PDF que representa la instancia de carta. La instancia de carta enviada que persiste en el servidor también contiene el dataXML y el XDP procesados, que se pueden utilizar para llevar a cabo y utilizar un caso personalizado como la creación de un PDF/A.
* Si hay una instancia de carta Borrador, la interfaz de usuario de Crear correspondencia se vuelve a cargar al estado anterior exacto, tal como estaba durante el momento en que se creó el borrador

### Abrir instancia de carta Borrador  {#opening-draft-letter-instance-nbsp}

La interfaz de usuario de CCR admite el parámetro cmLetterInstanceId, que se puede utilizar para volver a cargar la carta.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>No es necesario especificar cmLetterId o cmLetterName/State/Version al volver a cargar una correspondencia, ya que los datos enviados ya contienen todos los detalles sobre la correspondencia que se recarga. RandomNo se usa para evitar problemas con la caché del explorador, puede usar una marca de tiempo como un número aleatorio.

### Abrir la instancia de la carta enviada {#opening-submitted-letter-instance}

El PDF enviado se puede abrir directamente utilizando el ID de instancia de carta:

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
