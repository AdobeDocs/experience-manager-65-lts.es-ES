---
title: Técnicas para probar la accesibilidad de los formularios
description: Obtenga información sobre las técnicas para probar la accesibilidad de los formularios en Forms Designer
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
exl-id: 06d05a33-82bd-420c-89b4-3d93dbcd4589
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 1af3c3d4-88d7-5e0f-813c-eb70824bfcdd
    internal-label: Forms Designer
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 2%
---
# Técnicas para probar la accesibilidad de los formularios

Para garantizar que los formularios sean accesibles para una amplia variedad de usuarios, debe probarlos con una variedad de tecnologías de asistencia. Puede probar los formularios de forma sencilla y económica mediante las técnicas descritas en esta sección.
Asegúrese de que el formulario se pueda rellenar utilizando solo el teclado. Asegúrese de rellenar todo el formulario y probar todos los campos y botones. A medida que complete el formulario, determine si es necesario realizar mejoras en función de sus respuestas a las siguientes preguntas:

* ¿Hay alguna operación que no se pueda realizar?
* ¿Hay alguna operación incómoda o difícil de realizar?
* ¿Están bien documentados los mecanismos del teclado?
* ¿Todos los controles y elementos de menú tienen teclas de acceso subrayadas?

Las versiones de demostración del software de lector de pantalla se pueden descargar gratis a través de Internet. Para probar los resultados del lector de pantalla, apague el monitor y utilice únicamente el lector de pantalla para desplazarse por el formulario y rellenarlo. Si es el autor del formulario, su familiaridad con el formulario puede dificultar la determinación de si la información leída por el lector de pantalla es suficiente y tiene sentido. Si es posible, pida a otra persona que pruebe el formulario de esta manera.

Las versiones de demostración del software de ampliación de pantalla también están disponibles para probarlas en Internet.

El software de conversión de voz a texto, disponible a un coste nominal, se puede utilizar para probar el formulario utilizando únicamente la entrada de voz.
Muchos usuarios con deficiencias visuales dependen del alto contraste entre el texto y el fondo para leer el formulario. Microsoft Windows tiene un esquema de colores de alto contraste que proporciona una visualización similar a la que muchos usuarios con deficiencias visuales utilizarán para completar el formulario. Para establecer la pantalla en modo de alto contraste, habilite la característica mediante Opciones de accesibilidad en el Panel de control de Campaign de Windows. A medida que complete el formulario en este modo, determine si es necesario realizar mejoras en función de sus respuestas a las siguientes preguntas:

* ¿Las partes del formulario se vuelven invisibles, irreconocibles o difíciles de usar?
* ¿Siguen apareciendo áreas negras sobre un fondo blanco?
* ¿Hay algún elemento cuyo tamaño o truncado sean incorrectos?
