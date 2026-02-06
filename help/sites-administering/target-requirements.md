---
title: Requisitos previos para la integración con Adobe Target
description: Obtenga información acerca de los requisitos previos para la integración con Adobe Target.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: e1771229-b2ce-406a-95a5-99b11fafbe34
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 7%

---

# Requisitos previos para la integración con Adobe Target{#prerequisites-for-integrating-with-adobe-target}

Como parte de la [integración de AEM y Adobe Target](/help/sites-administering/target.md), debe registrarse en Adobe Target, configurar el agente de replicación y asegurar la configuración de la actividad en el nodo de publicación.

## Registrarse en Adobe Target {#registering-with-adobe-target}

Para integrar AEM con Adobe Target, debe tener una cuenta de Adobe Target válida. Esta cuenta debe tener permisos de nivel **aprobador** como mínimo. Al registrarse en Adobe Target, recibirá un código de cliente. Necesita el código de cliente, el nombre de inicio de sesión de Adobe Target y la contraseña para conectar AEM a Adobe Target.

El código de cliente identifica la cuenta de cliente de Adobe Target al llamar al servidor de Adobe Target.

>[!NOTE]
>
>El equipo de Target debe habilitar su cuenta para utilizar la integración.
>
>Si no es así, comuníquese con el [Servicio de atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/target/using/cmp-resources-and-contact-information).

## Habilitar el agente de replicación de destino {#enabling-the-target-replication-agent}

El agente de replicación [Test and Target](/help/sites-deploying/replication.md) debe estar habilitado en la instancia de autor. Tenga en cuenta que este agente de replicación no está habilitado de forma predeterminada si utilizó el modo de ejecución [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) para instalar AEM. Para obtener más información sobre cómo proteger el entorno de producción, consulte la [Lista de comprobación de seguridad](/help/sites-administering/security-checklist.md).

1. En la página de inicio de AEM, haga clic en **Herramientas** > **Implementación** > **Replicación**.
1. Haga Clic En **Agentes En Autor**.
1. Haga clic en el agente de replicación **Test and Target (test and target)** y, a continuación, haga clic en **Editar**.
1. Seleccione la opción Habilitado y luego haga clic en **Aceptar**.

   >[!NOTE]
   >
   >Al configurar el agente de replicación de Test and Target, en la ficha **Transporte**, el URI se establece de forma predeterminada en `tnt:///`. No reemplace este URI por `https://admin.testandtarget.omniture.com`.
   >
   >Si intenta probar la conexión con `tnt:///`, se mostrará un error, que es el comportamiento esperado. El motivo es que el URI es solo para uso interno. No usar con **Probar conexión**.

## Proteja el nodo de configuración de la actividad {#securing-the-activity-settings-node}

Proteja el nodo de configuración de actividad **cq:ActivitySettings** en la instancia de publicación para que los usuarios normales no puedan obtener acceso a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.

El nodo **cq:ActivitySettings** está disponible en CRXDE Lite en `/content/campaigns/*nameofbrand*`* *en el nodo de actividades `jcr:content`. Por ejemplo, `/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`. Este nodo solo se crea después de establecer como objetivo un componente.

El nodo **cq:ActivitySettings** bajo `jcr:content` de la actividad está protegido por las siguientes ACL:

* Denegar todo para todos.
* Permitir `jcr:read,rep:write` para `target-activity-authors` (el autor es miembro de este grupo de forma predeterminada).
* Permitir `jcr:read,rep:write` para `targetservice`.

Esta configuración garantiza que los usuarios normales no tengan acceso a las propiedades del nodo. Utilice las mismas ACL en autor y en publicación. Consulte [Administración de usuarios y seguridad](/help/sites-administering/security.md) para obtener más información.

## Configuración del externalizador de vínculos de AEM {#configuring-the-aem-link-externalizer}

Al editar una actividad en Adobe Target, la URL apunta a **localhost** a menos que cambie la URL en el nodo de creación de AEM. Puede configurar el externalizador de vínculos de AEM si desea que el contenido exportado apunte a un dominio *publish* específico.

>[!NOTE]
>
>Consulte también [Agregar la configuración de nube](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration).

Para configurar el externalizador de AEM:

>[!NOTE]
>
>Para obtener más información, consulte [Externalización de direcciones URL](/help/sites-developing/externalizer.md).

1. Vaya a la consola web de OSGi en **https://&lt;server>:&lt;port>/system/console/configMgr.**
1. Busque **Day CQ Link Externalizer** e introduzca el dominio para el nodo de creación.

   ![Externalizador de vínculos CQ por día](assets/aem-externalizer-01.png)
