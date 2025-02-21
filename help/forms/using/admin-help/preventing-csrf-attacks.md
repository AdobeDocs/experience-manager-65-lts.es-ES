---
title: Prevenir ataques CSRF
description: Aprenda a evitar ataques de falsificación de solicitudes entre sitios (CSRF) y a salvaguardar los datos de usuario de verse comprometidos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 2%

---

# Prevenir ataques CSRF {#preventing-csrf-attacks}

## Cómo funcionan los ataques CSRF {#how-csrf-attacks-work}

La falsificación de solicitudes entre sitios (CSRF) es una vulnerabilidad del sitio web en la que se utiliza el explorador de un usuario válido para enviar una solicitud maliciosa, posiblemente a través de un iFrame. Dado que el explorador envía cookies por dominio, si el usuario ha iniciado sesión en una aplicación, los datos del usuario pueden verse comprometidos.

Por ejemplo, imagine un escenario en el que ha iniciado sesión en la consola de administración en un explorador. Recibirá un mensaje de correo electrónico que contiene un vínculo. Hace clic en el vínculo, que abre una nueva pestaña en el explorador. La página que ha abierto contiene un iFrame oculto que realiza una solicitud malintencionada al servidor de Forms mediante la cookie de la sesión de formularios autenticados de AEM. Como Administración de usuarios recibe una cookie válida, pasa la solicitud.

## Términos relacionados con CSRF {#csrf-related-terms}

**Referente:** Dirección de la página de origen de la que proviene una solicitud. Por ejemplo, una página web en site1.com contiene un vínculo a site2.com. Al hacer clic en el vínculo, se publica una solicitud en site2.com. El referente de esta solicitud es site1.com porque la solicitud se realiza desde una página cuyo origen es site1.com.

**URI Incluidos en la lista de permitidos:** URI que identifican los recursos del servidor de Forms que se solicitan, por ejemplo, /adminui o /contentspace. Algunos recursos pueden permitir que una solicitud entre en la aplicación desde sitios externos. Estos recursos se consideran URI incluidos en la lista de permitidos. El servidor de Forms nunca realiza una comprobación de referente a partir de URI incluidos en la lista de permitidos.

**Referente nulo:** Al abrir una nueva ventana o ficha del explorador, escribir una dirección y presionar Entrar, el referente es nulo. La solicitud es completamente nueva y no se origina desde una página web principal; por lo tanto, no hay ningún referente para la solicitud. El servidor de Forms puede recibir un referente nulo de:

* solicitudes realizadas en puntos finales SOAP o REST desde Acrobat
* cualquier cliente de escritorio que realice una solicitud HTTP en un extremo SOAP o REST de formularios AEM
* cuando se abre una nueva ventana del explorador y se introduce la dirección URL de cualquier página de inicio de sesión de la aplicación web de AEM forms

Permitir referente nulo en puntos finales SOAP y REST. También permita un referente nulo en todas las páginas de inicio de sesión de URI como /adminui y /contentspace y sus recursos asignados correspondientes. Por ejemplo, el servlet asignado para /contentspace es /contentspace/faces/jsp/login.jsp, que debería ser una excepción de referente nulo. Esta excepción solo es necesaria si habilita el filtrado de GET para la aplicación web. Las aplicaciones pueden especificar si se permiten referentes nulos. Consulte &quot;Protección frente a ataques de falsificación de solicitud en sitios múltiples&quot; en [Protección y seguridad para formularios AEM](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html).

**Excepción de referente permitido:** La excepción de referente permitido es una sublista de la lista de referentes permitidos, desde la cual se bloquean las solicitudes. Las excepciones de referencia permitidas son específicas de una aplicación web. Si no se debe permitir que un subconjunto de los referentes permitidos invoque una aplicación web determinada, se pueden realizar listas de bloqueados de los referentes mediante Excepciones de referentes permitidos. Las excepciones de referentes permitidos se especifican en el archivo web.xml de la aplicación. (Consulte &quot;Protección frente a ataques de falsificación de solicitud en sitios múltiples&quot; en Protección y seguridad para formularios AEM en la página Ayuda y tutoriales).

## Funcionamiento de los referentes permitidos {#how-allowed-referers-work}

AEM Forms proporciona filtrado de referentes, que puede ayudar a evitar ataques de CSRF. Así funciona el filtrado de referentes:

1. El servidor de Forms comprueba el método HTTP utilizado para la invocación:

   * Si es POST, el servidor de Forms realiza la comprobación del encabezado de referente.
   * Si es GET, Forms Server omite la comprobación del referente, a menos que CSRF_CHECK_GETS esté establecido en true, en cuyo caso realiza la comprobación del encabezado del referente. CSRF_CHECK_GETS se especifica en el archivo web.xml de la aplicación. (Consulte &quot;Protección frente a ataques de falsificación de solicitud en sitios múltiples&quot; en [Guía de protección y seguridad](https://help.adobe.com/en_US/livecycle/11.0/HardeningSecurity/index.html)).

1. El servidor de Forms comprueba si el URI solicitado está incluido en la lista de permitidos:

   * Si el URI está incluido en la lista de permitidos, el servidor pasa la solicitud.
   * Si el URI solicitado no está incluido en la lista de permitidos, el servidor recupera el referente de la solicitud.

1. Si hay un referente en la solicitud, el servidor comprueba si es un referente permitido. Si está permitido, el servidor comprueba la existencia de una excepción de referente:

   * Si existe una excepción, la solicitud se bloquea.
   * Si hay ninguna excepción, se pasa la solicitud.

1. Si no hay ningún referente en la solicitud, el servidor comprueba si se permite un referente nulo.

   * Si se permite un referente nulo, se pasa la solicitud.
   * Si no se permite un referente nulo, el servidor comprueba si el URI solicitado es una excepción para el referente nulo y gestiona la solicitud en consecuencia.

## Configuración de referentes permitidos {#configure-allowed-referers}

Al ejecutar el Administrador de configuración, el host predeterminado y la dirección IP o el servidor de Forms se agregan a la lista Referentes permitidos. Puede editar esta lista en la consola de administración.

1. En la consola de administración, haga clic en Configuración > User Management > Configuración > Configurar direcciones URL de referentes permitidos. La lista Referentes permitidos aparece en la parte inferior de la página.
1. Para agregar un referente permitido:

   * Escriba un nombre de host o una dirección IP en el cuadro Referentes permitidos. Para agregar varios referentes permitidos a la vez, escriba cada nombre de host o dirección IP en una nueva línea.
   * En los cuadros Puerto HTTP y Puertos HTTPS, especifique qué puertos permiten HTTP, HTTPS o ambos. Si deja esas casillas vacías, se usan los puertos predeterminados (puerto 80 para HTTP y puerto 443 para HTTPS). Si escribe `0` (cero) en los cuadros, se habilitarán todos los puertos de ese servidor. También puede especificar un número de puerto específico para habilitar sólo ese puerto.
   * Haga clic en Agregar.

1. Para quitar una entrada de la lista Referentes permitidos, seleccione el elemento de la lista y haga clic en Eliminar.

   Si la Lista de referentes permitidos está vacía, la función CSRF deja de funcionar y el sistema se vuelve inseguro.

1. Después de cambiar la lista Referentes permitidos, reinicie AEM Forms Server.
