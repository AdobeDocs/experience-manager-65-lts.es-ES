---
title: Configurar puntos finales remotos
description: Obtenga información sobre cómo configurar extremos remotos. En este documento se explica cómo habilitar la aplicación creada con Flex para invocar el servicio mediante la comunicación remota de formularios de AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: d19b7265-42cc-41d9-9897-e7b044c4529c
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 4%

---

# Configurar puntos finales remotos {#configuring-remoting-endpoints}

Un extremo remoto permite que una aplicación creada con Flex invoque el servicio mediante (obsoleto para formularios AEM) AEM Forms Remoting. Se crea automáticamente un extremo remoto para cada servicio activado. Se crea un destino de Flex con el mismo nombre que el extremo y los clientes de Flex pueden crear objetos remotos que apunten a este destino para invocar operaciones en el servicio correspondiente.

## Configuración del extremo remoto {#remoting-endpoint-settings}

**Método de autenticación de cliente de Flex:** Determina el tipo de respuesta que el servidor devuelve al cliente cuando el servicio invocado está habilitado para la seguridad, la operación invocada no admite invocaciones anónimas y el cliente pasa credenciales no válidas.
