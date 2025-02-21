---
title: Seguimiento de correos electrónicos rechazados
description: Cuando envía una newsletter a muchos usuarios, suele haber algunas direcciones de correo electrónico no válidas en la lista. El envío de boletines a esas direcciones se recupera. AEM puede administrar esas devoluciones y puede dejar de enviar boletines informativos a esas direcciones después de superar el contador de devoluciones configurado.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Personalization
role: User
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Seguimiento de correos electrónicos rechazados{#tracking-bounced-emails}

>[!NOTE]
>
>Adobe no planea mejorar aún más el seguimiento de los correos electrónicos abiertos/rechazados enviados por el servicio SMTP de AEM.
>
>Se recomienda [usar Adobe Campaign y su integración con AEM](/help/sites-administering/campaign.md).

Cuando envía una newsletter a muchos usuarios, suele haber algunas direcciones de correo electrónico no válidas en la lista. El envío de boletines a esas direcciones se recupera. AEM puede administrar esas devoluciones y puede dejar de enviar boletines informativos a esas direcciones después de superar el contador de devoluciones configurado. De forma predeterminada, la tasa de salida hacia otro sitio se establece en 3, pero se puede configurar.

Para configurar AEM para que rastree los correos electrónicos rechazados, configure AEM para sondear un buzón existente en el que se reciben los correos electrónicos rechazados. Normalmente, esta ubicación es la dirección de correo electrónico de origen que especifica dónde envía la newsletter. AEM sondea esta bandeja de entrada e importa todos los correos electrónicos por debajo de la ruta especificada en la configuración de sondeo. A continuación, se activa un flujo de trabajo para buscar las direcciones de correo electrónico rechazadas dentro de los usuarios y se actualiza el valor de la propiedad bounceCounter del usuario en consecuencia. Una vez superados los rebotes máximos configurados, el usuario se elimina de la lista del boletín informativo.

## Configuración del importador de fuentes {#configuring-the-feed-importer}

El importador de fuentes le permite importar repetidamente contenido de fuentes externas al repositorio. Con esta configuración del importador de fuentes, AEM comprueba el buzón del remitente para ver si hay correos electrónicos rechazados.

Para configurar el importador de fuentes para el seguimiento de correos electrónicos rechazados, haga lo siguiente:

1. En **Herramientas**, seleccione el Importador de fuentes.

1. Haga clic en **Agregar** para crear una configuración.

   ![chlimage_1](assets/chlimage_1a.png)

1. Añada una configuración seleccionando el tipo y añadiendo información a la URL de sondeo para que pueda configurar el host y el puerto. Además, agregue algunos parámetros de correo electrónico y específicos del protocolo a la consulta de URL. Establezca la configuración para sondear al menos una vez al día.

   Todas las configuraciones necesitan información sobre lo siguiente en la dirección URL de sondeo:

   `username`: nombre de usuario utilizado para la conexión

   `password`: la contraseña utilizada para la conexión

   Además, según el protocolo, puede configurar ciertas opciones.

   **Propiedades de configuración POP3:**

   `pop3.leave.on.server`: define si se deben dejar los mensajes en el servidor o no. Si se establece en true, los mensajes se dejarán en el servidor; en caso contrario, en false. El valor predeterminado es True.

   **ejemplos POP3:**

   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret | Uso de pop3 sobre SSL para conectarse a GMail en el puerto 995 con usuario/secreto, dejando los mensajes en el servidor de forma predeterminada |
   |---|---|
   | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false | pop3s://pop.gmail.com:995/INBOX?username=user&amp;password=secret&amp;pop3.leave.on.server=false |

   **Propiedades de configuración de IMAP:**

   Permite establecer marcas para buscar.

   `imap.flag.SEEN`: establecer falso para mensaje nuevo/no visto, verdadero para mensajes ya leídos

   Consulte [https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html](https://javaee.github.io/javamail/docs/api/index.html?javax/mail/Flags.Flag.html) para obtener la lista completa de indicadores.

   **ejemplos de IMAP:**

   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret | Uso de IMAP sobre SSL para conectarse a GMail en el puerto 993 con usuario/secreto. Recibir mensajes nuevos solo de forma predeterminada. |
   |---|---|
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true | Utilizando IMAP sobre SSL para conectarse a GMail 993 con usuario/secreto, solo recibiendo mensaje ya visto. |
   | imaps://imap.gmail.com:993/inbox?username=user&amp;password=secret&amp;imap.flag.SEEN=true&amp;imap.flag.SEEN=false | Utilizando IMAP sobre SSL para conectarse a GMail 993 con usuario/secreto, recibiendo mensajes leídos o nuevos. |

1. Guarde la configuración.

## Configuración del componente de servicio de newsletter {#configuring-the-newsletter-service-component}

Después de configurar el importador de fuentes, configure la Dirección de origen y el contador de devoluciones.

Para configurar el servicio del boletín informativo:

1. En la consola de OSGi, en `<host>:<port>/system/console/configMgr`, vaya a **Boletín de MCM**.

1. Configure el servicio y guarde los cambios cuando termine.

   ![chlimage_1-1](assets/chlimage_1-1a.png)

   Se pueden configurar las siguientes configuraciones para ajustar el comportamiento:

   | Contador de rechazos máximo (max.bounce.count) | Define el número de devoluciones hasta que se omite un usuario al enviar un boletín informativo. Si este valor se establece en 0, la comprobación de devoluciones se desactiva por completo. |
   |---|---|
   | Actividad sin caché (sent.activity.nocache) | Define la configuración de caché que se utilizará para la actividad de envío de newsletter |

   Una vez guardado, el servicio MCM del boletín informativo realiza las siguientes acciones:

   * Escribe una actividad en el flujo oculto de usuarios tras el envío correcto de un boletín informativo.
   * Escribe una actividad si se detecta una devolución y cambia el contador de devoluciones de los usuarios.
