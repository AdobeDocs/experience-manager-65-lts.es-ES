---
title: Umbral máximo de cursores abiertos de la base de datos de Oracle
description: Obtenga información acerca de la configuración de un valor máximo para cursores abiertos en Oracle.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 98663f16-6c05-4485-9bf2-a2de9d1975c8
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 14%

---

# Umbral máximo de cursores abiertos de la base de datos de Oracle {#oracle-database-maximum-open-cursors-threshold}

Para configurar un valor máximo para cursores abiertos en Oracle, es posible que tenga que ajustar este valor a un número que sea apropiado para su aplicación. Es evidente que bajo una carga moderada, el promedio de cursores abiertos fue de 2700. Se recomienda comenzar con un límite superior de 3000. Para obtener más información, ve a [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
