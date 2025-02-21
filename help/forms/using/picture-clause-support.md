---
title: Compatibilidad con cláusula de imagen para formularios HTML5
description: Los formularios HTML5 admiten la cláusula de imagen XFA para el valor de visualización y el valor formateado de símbolos numéricos, texto y fecha.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 96%

---

# Compatibilidad con cláusula de imagen para formularios HTML5 {#picture-clause-support-for-html-forms}

Los formularios HTML5 admiten la cláusula de imagen XFA para el valor de visualización y el valor formateado de símbolos numéricos, texto y fecha. Se admiten las siguientes expresiones de cláusula de imagen:

* category(locale){picture-subscription} | category(locale){picture-subscription} | category(locale){picture-subscription}
* category.subcategory{}

>[!NOTE]
>
>Actualmente, Mobile Forms no admite la cláusula de imagen de edición. Además, no se admiten los símbolos de las cláusulas de imagen de hora y fecha y hora.

## Símbolos de campo de fecha admitidos {#supported-date-field-symbols}

Expresión admitida para la cláusula de imagen de fecha:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{símbolos de la cláusula de imagen de fecha}

>[!NOTE]
>
>El patrón predeterminado de la cláusula de imagen es {MMM D, AAAA}. Si no se aplica ningún patrón, se utiliza el patrón predeterminado.

<table>
 <tbody>
  <tr>
   <th><strong>Símbolo</strong></th>
   <th>Interpretación</th>
  </tr>
  <tr>
   <td>D</td>
   <td>El día del mes expresado con 1 o 2 dígitos (1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>El día del mes expresado con dos dígitos (se rellena con ceros en el caso de los días 1 a 9) (01-31)<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>El mes del año expresado con 1 o 2 dígitos (1-12)<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>El mes del año expresado con 2 dígitos (se rellena con ceros en el caso de los meses 1 a 12)<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>El nombre abreviado del mes de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>El nombre completo del mes de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>El nombre abreviado del día de la semana de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>El nombre completo del día de la semana de la configuración regional actual<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>El año expresado con 2 dígitos, donde 00 = 2000, 29 = 2029, 30 = 1930 y 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>El año expresado con 4 dígitos<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> Según el diseño, el campo Fecha en HTML5 Forms no admite el patrón `MM-YYYY` en formato de edición. Sin embargo, el patrón es compatible con el formato de visualización.

## Cláusula de imagen numérica {#numeric-picture-clause}

Los formularios HTML5 admiten símbolos de imagen numéricos. Sin embargo, existe una diferencia en la compatibilidad entre los formularios PDF y HTML.

En los **formularios PDF**, se da formato a un número independientemente del número de símbolos de la cláusula de imagen.

En los **formularios HTML**, se aplica formato a un número únicamente si tiene un número de dígitos inferior al número de símbolos de la cláusula de imagen.

**Ejemplo**: imagine una cláusula de imagen: num{zzz,zzz,zz9}.

Al número **10000** se le aplica el formato **10 000** tanto en formularios HTML como PDF.

Al número 1000000 se le aplica el formato 1 000 000 en los formularios PDF. Sin embargo, en los formularios HTML, el número sigue sin tener formato y se muestra como 1000000.

Las expresiones compatibles con la cláusula de imagen numérica de los **formularios HTML** son las siguientes:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{símbolos de la cláusula de imagen numérica}

<table>
 <tbody>
  <tr>
   <th><strong>Símbolo</strong></th>
   <th><strong>Interpretación</strong></th>
   <th>Análisis de entrada</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Formato de salida</strong>: un solo dígito, o el dígito cero si los datos de entrada están vacíos o si hay un espacio en la posición correspondiente.<br /> </td>
   <td>Dígito sencillo</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formato de salida</strong>: un solo dígito, o un espacio si los datos de entrada están vacíos o hay un espacio o el dígito cero en la posición correspondiente.<br /> </td>
   <td>Un solo dígito o espacio</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formato de salida</strong>: un solo dígito, o ninguno si los datos de entrada están vacíos o hay un espacio o el dígito cero en la posición correspondiente.<br /> </td>
   <td>Un solo dígito o ninguno</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>Formato de salida</strong>: la parte exponencial de un número de punto flotante que consta del símbolo exponencial (E), seguida de un signo más o menos opcional y seguida del valor exponencial.<br /> </td>
   <td>Igual que el del formato de salida.</td>
  </tr>
  <tr>
   <td>CR o cr<br /> </td>
   <td>El símbolo de crédito (CR) si el número es negativo. En caso contrario, ninguno.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S o s<br /> </td>
   <td>Formato de salida: un signo menos si el número es negativo. De lo contrario, un espacio.<br /> </td>
   <td>Un signo menos si el número es negativo. Un signo más si el número es positivo.</td>
  </tr>
  <tr>
   <td>V</td>
   <td>La base decimal de la configuración regional predominante. Permite para que la base decimal sea implícita al analizar la entrada.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>La base decimal de la configuración regional predominante. Permite que la base decimal sea implícita al analizar la entrada y al dar formato a la salida.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>La base decimal de la configuración regional predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>El separador de agrupación de la configuración regional predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>El símbolo de moneda de la configuración regional predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>El símbolo porcentual de la configuración regional predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>El paréntesis izquierdo si el número es negativo. De lo contrario, espacio.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>El paréntesis derecho si el número es negativo. De lo contrario, espacio.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>El carácter de tabulación</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Cláusula de imagen de texto {#text-picture-clause}

Los formularios HTML5 admiten las siguientes expresiones de cláusula de imagen de texto:

* text{símbolos de la cláusula de imagen de texto}

| **Símbolo** | **Interpretación** |
|---|---|
| A | Carácter alfabético sencillo |
| X | Carácter sencillo |
| O | Carácter alfanumérico sencillo |
| 0 (cero) | Carácter alfanumérico sencillo |
| 9 | Dígito sencillo |
