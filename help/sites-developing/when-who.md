---
title: 'Pruebas: ¿cuándo y con quién?'
description: Se pueden desempeñar diversas funciones en las pruebas y en diversas etapas del desarrollo del proyecto.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 631ca939-81f4-49f5-b29a-f4633f2888aa
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 3%
---
# Pruebas: ¿cuándo y con quién?{#testing-when-and-with-whom}

Se pueden desempeñar diversas funciones en las pruebas y en diversas etapas del desarrollo del proyecto.

<table>
 <tbody>
  <tr>
   <td>Equipo de prueba</td>
   <td>Responsable de... </td>
   <td>Cuando...</td>
  </tr>
  <tr>
   <td>Equipo de desarrollo</td>
   <td>El equipo de desarrollo es responsable de las pruebas unitarias y de algunas pruebas de integración.</td>
   <td>Estas pruebas son las primeras en la cadena, aunque se repiten / se extienden durante el desarrollo.</td>
  </tr>
  <tr>
   <td>Equipo de calidad de Assurance</td>
   <td><p>Necesita un equipo de Quality Assurance (del tamaño que corresponda) para realizar pruebas funcionales y de rendimiento.</p> <p>Estos son probadores neutrales y dedicados; una regla de oro del software siempre establece que un desarrollador nunca debe probar su propio trabajo.</p> <p>Los miembros de este equipo pueden proceder del equipo del proyecto del día, del socio y/o de su equipo de clientes.</p> </td>
   <td><p>La primera versión de la función debe ponerse a disposición de los probadores (cuando sea posible). Aunque una versión provisional anticipada puede generar muchos errores, puede proporcionar comentarios anticipados sobre problemas críticos.</p> </td>
  </tr>
  <tr>
   <td>Equipo de prueba del cliente</td>
   <td><p>Según el modelo de proyecto seleccionado, se puede planificar la participación de miembros del equipo del cliente en las pruebas, en particular autores del sitio del cliente.</p> <p>Esto es ventajoso porque:</p>
    <ul>
     <li><p>Se proporciona al cliente la experiencia del proyecto que se está desarrollando.</p> </li>
     <li><p>Proporciona comentarios anticipados del cliente.</p> </li>
     <li><p>Los usuarios suelen expresar sus requisitos en términos de experiencia previa; involucrar a los clientes en las pruebas lo antes posible aumenta su experiencia del nuevo proyecto en términos de experiencia <i>práctica</i>.</p> </li>
    </ul> </td>
   <td><p>De nuevo, la participación temprana es buena, aunque cualquier versión que utilicen los clientes debería ser estable y tener una funcionalidad razonable.</p> <p>Las primeras impresiones siempre son importantes.</p> </td>
  </tr>
 </tbody>
</table>
