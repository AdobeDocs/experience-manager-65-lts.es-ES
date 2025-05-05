---
title: Configurar extremos de correo electrónico
description: Obtenga información sobre cómo configurar los extremos de correo electrónico. Los extremos de correo electrónico permiten invocar un servicio enviando uno o varios documentos a una cuenta de correo electrónico especificada.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 56dac3e2-e330-47c9-a32e-db947272a632
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '3808'
ht-degree: 1%

---

# Configurar extremos de correo electrónico {#configuring-email-endpoints}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

Los extremos de correo electrónico permiten a los usuarios invocar un servicio enviando uno o varios documentos (como archivos adjuntos de correo electrónico) a una cuenta de correo electrónico especificada. La bandeja de entrada del correo electrónico actúa como punto de recopilación de los archivos adjuntos. El servicio supervisa la bandeja de entrada y procesa los archivos adjuntos. Los resultados de la conversión se reenvían al usuario definido en el punto de conexión.

Para un extremo de correo electrónico, los usuarios autorizados pueden invocar un proceso enviando archivos por correo electrónico a la cuenta correspondiente. Los resultados se devuelven al usuario que realiza el envío (de forma predeterminada) o al usuario definido en la configuración del extremo.

Antes de configurar un extremo de correo electrónico, cree una cuenta de correo electrónico POP3 o IMAP para que la utilice el extremo. Configure una cuenta independiente para cada tipo de conversión. Por ejemplo, se puede configurar una cuenta para generar documentos de PDF estándar a partir de archivos adjuntos entrantes y otra cuenta para generar documentos de PDF seguros.

>[!NOTE]
>
>Cada dirección de correo electrónico solo debe asignarse a un extremo de correo electrónico. No puede configurar varios extremos de correo electrónico en una sola dirección de correo electrónico, aunque los extremos de correo electrónico adicionales estén deshabilitados.

Todos los extremos de correo electrónico se configuran con un nombre de usuario y una contraseña autorizados para la bandeja de entrada de correo electrónico, que son necesarios al invocar el servicio. La cuenta de correo electrónico está protegida por el sistema de servidor de correo en el que está configurada.

Si los usuarios envían documentos con caracteres del idioma de Europa occidental en los nombres de ruta de archivo y de conversión, deben utilizar una aplicación de correo electrónico que admita los tipos de codificación requeridos (Latin1 [ISO-8859-1], Europa occidental [Windows] o UTF-8). Para obtener más información, consulte el documento *Instalación e implementación de formularios AEM Forms* para su servidor de aplicaciones.

Antes de configurar un extremo de correo electrónico, configure el servicio de correo electrónico. (Consulte [Configurar las opciones predeterminadas de extremo de correo electrónico](configuring-email-endpoints.md#configure-default-email-endpoint-settings).) Los parámetros de configuración del servicio de correo electrónico tienen dos propósitos:

* Para configurar atributos que son comunes para todos los extremos de correo electrónico
* Para proporcionar valores predeterminados para todos los extremos de correo electrónico

## Configurar SSL para un extremo de correo electrónico {#configure-ssl-for-an-email-endpoint}

Puede configurar POP3, IMAP o SMTP para utilizar Secure Sockets Layer (SSL) en un extremo de correo electrónico.

1. En el servidor de correo electrónico, habilite SSL para POP3, IMAP o SMTP según la documentación del fabricante.
1. Exporte un certificado de cliente desde el servidor de correo electrónico.
1. Utilice el programa keytool para importar el archivo de certificado del cliente al almacén de certificados de la máquina virtual Java (JVM) del servidor de aplicaciones. El procedimiento para este paso dependerá de las rutas de instalación de JVM y cliente.

   Por ejemplo, si está utilizando una instalación predeterminada de Oracle WebLogic Server con JDK 1.5.0 en Microsoft Windows Server® 2003, escriba el siguiente texto en el símbolo del sistema:

   `keytool -import -file client_certificate -alias myalias -keystore BEA_HOME\jdk150_04\jre\security\cacerts`

1. Cuando se le pida, escriba la contraseña (para Java, la contraseña predeterminada es `changeit`). Recibirá un mensaje que indica que el certificado se importó correctamente.
1. Utilice la consola de administración para agregar el extremo de correo electrónico al servicio.
1. Cree el extremo de correo electrónico en la consola de administración. Al configurar los valores del extremo, seleccione POP3/IMAP SSL Enabled para los mensajes entrantes y SMTP SSL Enabled para los mensajes salientes y cambie las propiedades del puerto en consecuencia.

>[!NOTE]
>
>Sugerencia: Si tiene problemas al utilizar SSL, utilice un cliente de correo electrónico como Microsoft Outlook para comprobar si puede acceder al servidor de correo electrónico mediante SSL. Si el cliente de correo electrónico no puede acceder al servidor de correo electrónico, el problema está relacionado con la configuración del certificado o del servidor de correo electrónico.

## Configurar opciones predeterminadas de extremo de correo electrónico {#configure-default-email-endpoint-settings}

Puede usar la página Administración de servicios para configurar atributos que son comunes para todos los extremos de correo electrónico y para proporcionar valores predeterminados para todos los extremos de correo electrónico.

Para que el flujo de trabajo de formularios reciba y administre mensajes de correo electrónico entrantes de los usuarios, debe crear un punto final de correo electrónico para el servicio Tarea completa. Este extremo de correo electrónico requiere una configuración adicional, tal como se describe en [Crear un extremo de correo electrónico para el servicio Tarea completa](configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service).

### Cambiar los valores predeterminados de los extremos de correo electrónico {#change-the-default-values-for-email-endpoints}

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en Correo electrónico: 1.0 (el ID de componente es com.adobe.idp.dsc.provider.service.email.Email).
1. En la pestaña Configuración, especifique la configuración predeterminada del extremo de correo electrónico y, a continuación, haga clic en Guardar.

### Configuración predeterminada de extremo de correo electrónico {#default-email-endpoint-settings}

**Expresión cron:** La expresión cron utilizada por quartz para programar el sondeo del directorio de entrada.

**Intervalo de repetición:** Número de veces que se repite el sondeo de directorios. El intervalo de repetición predeterminado es en segundos si este valor no se especifica en la configuración del extremo. El valor predeterminado es 10. Este valor no puede ser menor que 10.

**Recuento de repeticiones:** El número de veces que se sondea el directorio de entrada. Recuento de repetición predeterminado que se utilizará si este valor no se especifica en la configuración del extremo. El valor -1 indica un análisis indefinido del directorio. El valor predeterminado es -1.

**Retraso al iniciarse el trabajo:** El valor predeterminado, en segundos, para el retraso antes de que el trabajo empiece a analizar el extremo. El valor predeterminado es 0.

**Tamaño de lote:** Número de correos electrónicos que el receptor procesa por análisis para obtener un rendimiento óptimo. El valor -1 indica todos los correos electrónicos. El valor predeterminado es 2.

**Asincrónica:** Identifica el tipo de invocación como asincrónico o sincrónico. Los procesos transitorios y sincrónicos solo se pueden invocar sincrónicamente. El valor predeterminado es asíncrono.

**Patrón de dominio:** Patrón de nombre de dominio que se usa para filtrar correos electrónicos entrantes. Por ejemplo, si se utiliza adobe.com, solo se procesará el correo electrónico de adobe.com; se omitirá el correo electrónico de otros dominios.

**Patrón de archivo:** Patrones de archivos adjuntos entrantes que acepta el proveedor. Esto incluye archivos que tienen extensiones específicas (&ast;.dat, &ast;.xml), nombres específicos (data) y expresiones compuestas en el nombre y la extensión (.[dD][aA]&#39;port&#39;). El valor predeterminado es &ast;.&ast;.

**Destinatarios de trabajo exitosos:** Una o más direcciones de correo electrónico que se usan para enviar correos electrónicos para indicar trabajos exitosos. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente del trabajo inicial. Se admiten hasta 100 destinatarios. Para desactivar esta configuración, deje este campo en blanco.

**Destinatarios del trabajo con errores:** Una o más direcciones de correo electrónico que se utilizan para enviar correos electrónicos para indicar trabajos con errores. De forma predeterminada, siempre se envía un mensaje de trabajo con errores al remitente que envió el trabajo inicial. Se admiten hasta 100 destinatarios. Para desactivar esta configuración, deje este campo en blanco.

**Host de bandeja de entrada:** Nombre de host de bandeja de entrada o Dirección IP para que el proveedor de correo electrónico analice.

**Puerto de bandeja de entrada:** Número de puerto de bandeja de entrada para que el proveedor de correo electrónico lo analice. Si el valor es 0, se utiliza el puerto IMAP o POP3 predeterminado.

**Protocolo de bandeja de entrada:** Protocolo de correo electrónico para que el extremo de correo electrónico se utilice para analizar la bandeja de entrada. Las opciones son IMAP o POP3. El servidor de correo host de bandeja de entrada debe admitir estos protocolos.

**Tiempo de espera de la bandeja de entrada:** Especifica la cantidad de tiempo que el extremo esperará antes de cancelar al intentar conectarse a la bandeja de entrada. Si no se adquiere una conexión antes de que se alcance el valor de tiempo de espera, la bandeja de entrada no se sondea.

**Usuario de bandeja de entrada:** El nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, este nombre solo puede ser la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.

**Contraseña de Bandeja de entrada:** Contraseña del usuario de Bandeja de entrada.

**Habilitado para SSL POP3/IMAP:** Al seleccionarlo, se habilita SSL.

**Host SMTP:** El nombre de host del servidor de correo que el proveedor de correo electrónico utiliza para enviar los resultados y los mensajes de error. Por ejemplo, mail.example.com.

**Puerto SMTP:** El puerto que se usa para conectarse al servidor de correo. El valor predeterminado es 25.

**Usuario SMTP:** Cuenta de usuario que el proveedor de correo electrónico debe usar cuando envíe correo electrónico para obtener resultados y errores.

**Contraseña SMTP:** Contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.

**Enviar desde:** La dirección de correo electrónico (por ejemplo, user@company.com) utilizada para enviar notificaciones por correo electrónico de resultados y errores. Si no especifica un valor Enviar desde, el servidor de correo electrónico intenta determinar la dirección de correo electrónico combinando el valor especificado en la configuración Usuario de SMTP con un dominio predeterminado configurado en el servidor de correo electrónico. Si el servidor de correo electrónico no tiene un dominio predeterminado y no especifica ningún valor para Enviar desde, pueden producirse errores. Para asegurarse de que los mensajes de correo electrónico tengan la dirección remitente correcta, especifique un valor para la configuración Enviar desde.

**SSL SMTP habilitado:** Cuando se selecciona, habilita SSL a través de SMTP.

**Incluir el cuerpo original del correo electrónico como datos adjuntos:** De forma predeterminada, cuando envía un correo electrónico al servidor de Forms, el texto original del mensaje se incluye en el cuerpo del mensaje. Para incluir el texto como datos adjuntos, seleccione esta opción.

**Usar la línea de asunto original para los correos electrónicos de resultados:** De forma predeterminada, el servidor de Forms usa los valores especificados en la configuración Asunto del correo electrónico de éxito y Asunto del correo electrónico de error como línea de asunto al enviar mensajes de correo electrónico de resultados. Para utilizar en su lugar la misma línea de asunto que el correo electrónico original enviado al servidor, seleccione esta opción.

**Asunto del correo electrónico de éxito:** Después de enviar un correo electrónico a un extremo de correo electrónico para iniciar o continuar un proceso, recibirá un mensaje de correo electrónico de retorno del servidor de AEM Forms. Si el correo electrónico se ha enviado correctamente, recibirá un mensaje de correo electrónico con el resultado deseado. Si el correo electrónico falla, recibe un correo electrónico que le informa de por qué ha fallado. Esta configuración le permite especificar la línea de asunto de los mensajes de correo electrónico de éxito enviados para este punto de conexión.

**Cuerpo del mensaje de correo electrónico de éxito:** Permite especificar el texto del cuerpo de los mensajes de correo electrónico de éxito enviados para este extremo.

**Prefijo del asunto del correo electrónico de error:** Permite especificar el texto utilizado al principio de la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo.

**Asunto del correo electrónico de error:** Permite especificar la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo. Este texto se muestra después del prefijo del asunto del correo electrónico de error.

**Cuerpo del mensaje de correo electrónico de error:** Permite especificar la primera línea del texto del cuerpo de los mensajes de correo electrónico de error enviados para este extremo.

**Información de resumen de correo electrónico:** Cada mensaje de éxito o error incluye una sección que contiene el texto original del correo electrónico enviado al servidor de Forms. Esta configuración especifica el texto que aparece encima de esa sección.

**Validar Bandeja de entrada antes de crear o actualizar este extremo:** Cuando se selecciona esta opción, el servidor de Forms comprueba si la configuración de SMTP/POP3 es correcta antes de crear el extremo. Al hacer clic en Agregar, aparece un mensaje que indica si la cuenta de la bandeja de entrada es válida. Si esta opción no está seleccionada, el servidor de AEM Forms crea el extremo sin validar la bandeja de entrada.

**Codificación del conjunto de caracteres:** Formato de codificación que se utilizará para el mensaje de correo electrónico. El valor predeterminado es UTF-8, que usará la mayoría de los usuarios fuera de Japón. Los usuarios en un entorno japonés pueden elegir ISO2022-JP.

**Carpeta de correo electrónico enviado con error:** Especifica un directorio en el que almacenar los resultados si el servidor de correo SMTP no está operativo.

## Configuración de extremo de correo electrónico {#email-endpoint-settings}

Utilice la siguiente configuración para configurar un extremo de correo electrónico.

**Nombre:** Una configuración obligatoria que identifica el extremo. No incluya un carácter &lt; porque trunca el nombre mostrado en Workspace. Si introduce una dirección URL como nombre del extremo, asegúrese de que se ajuste a las reglas de sintaxis especificadas en RFC1738.

**Descripción:** Una descripción del extremo. No incluya un carácter &lt; porque trunca la descripción mostrada en Workspace.

**Expresión cron:** Escriba una expresión cron si el correo electrónico debe programarse mediante una expresión cron.

**Recuento de repeticiones:** Número de veces que el extremo de correo electrónico analiza la carpeta o el directorio. El valor -1 indica un escaneo indefinido. El valor predeterminado es -1.

**Intervalo de repetición:** Velocidad de análisis que utiliza el receptor para comprobar el correo entrante.

**Retraso al iniciarse el trabajo:** Tiempo de espera para analizar después de que se inicie el planificador.

**Tamaño de lote:** Número de correos electrónicos que el receptor procesa por análisis para obtener un rendimiento óptimo. El valor -1 indica todos los correos electrónicos. El valor predeterminado es 2.

**Nombre de usuario:** Una configuración obligatoria, que es el nombre de usuario que se usa al invocar un servicio de destino desde el correo electrónico. El valor predeterminado es SuperAdmin.

**Nombre de dominio:** Una configuración obligatoria, que es el dominio del usuario. El valor predeterminado es DefaultDom.

**Patrón de dominio:** Especifica los patrones de dominio del correo electrónico entrante que acepta el proveedor. Por ejemplo, si se utiliza adobe.com, solo se procesa el correo electrónico de adobe.com; se ignora el correo electrónico de otros dominios.

**Patrón de archivo:** Especifica los patrones de archivos adjuntos entrantes que acepta el proveedor. Esto incluye archivos que tienen extensiones específicas (&ast;.dat, &ast;.xml), nombres específicos (data) o expresiones compuestas en el nombre y la extensión (&ast;).[dD][aA]&#39;port&#39;).

**Destinatarios de trabajo correctos:** Dirección de correo electrónico a la que se envían mensajes para indicar trabajos correctos. De forma predeterminada, siempre se envía un mensaje de trabajo correcto al remitente. Si escribe sender, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, separados por comas (,).

Para desactivar esta configuración, deje el campo en blanco. En algunos casos, desea almacenar en déclencheur un proceso y no desea recibir una notificación del resultado por correo electrónico.

**Destinatarios del trabajo con errores:** Dirección de correo electrónico a la que se envían mensajes para indicar trabajos con errores. De forma predeterminada, siempre se envía un mensaje de trabajo con errores al remitente. Si escribe sender, los resultados del correo electrónico se envían al remitente. Se admiten hasta 100 destinatarios. Especifique destinatarios adicionales con direcciones de correo electrónico, separados por comas (,).

Para desactivar esta configuración, deje el campo en blanco. En algunos casos, desea almacenar en déclencheur un proceso y no desea recibir una notificación del resultado por correo electrónico.

**Host de bandeja de entrada:** Nombre de host de bandeja de entrada o Dirección IP para que el proveedor de correo electrónico analice.

**Puerto de bandeja de entrada:** El puerto que utiliza el servidor de correo electrónico. El valor predeterminado de POP3 es 110 y el de IMAP es 143. Si SSL está habilitado, el valor predeterminado para POP3 es 995 y para IMAP es 993.

**Protocolo de bandeja de entrada:** Protocolo de correo electrónico para que el extremo de correo electrónico se utilice para analizar la bandeja de entrada. Los valores son IMAP o POP3. El servidor de correo host de bandeja de entrada debe admitir estos protocolos.

**Tiempo de espera de la bandeja de entrada:** Tiempo de espera, en segundos, para que el proveedor de correo electrónico espere las respuestas de la bandeja de entrada.

**Usuario de la Bandeja de entrada:** Nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico. Según el servidor de correo electrónico y la configuración, este valor puede ser solo la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.

**Contraseña de la Bandeja de entrada:** Contraseña del usuario de la Bandeja de entrada.

**SSL POP3/IMAP habilitado:** Seleccione esta opción para forzar al proveedor de correo electrónico a usar SSL para analizar la bandeja de entrada. Asegúrese de que el servidor de correo admita SSL.

**Host SMTP:** Nombre de host del servidor de correo que el proveedor de correo electrónico utiliza para enviar resultados y mensajes de error.

**Puerto SMTP:** El valor predeterminado para el puerto SMTP es 25.

**Usuario SMTP:** Cuenta de usuario que el proveedor de correo electrónico debe usar cuando envíe notificaciones por correo electrónico de resultados y errores.

**Contraseña SMTP:** Contraseña de la cuenta SMTP. Algunos servidores de correo no requieren una contraseña SMTP.

**Enviar desde:** La dirección de correo electrónico (por ejemplo, user@company.com) utilizada para enviar notificaciones por correo electrónico de resultados y errores. Si no especifica un valor Enviar desde, el servidor de correo electrónico intenta determinar la dirección de correo electrónico combinando el valor especificado en la configuración Usuario de SMTP con un dominio predeterminado configurado en el servidor de correo electrónico. Si el servidor de correo electrónico no tiene un dominio predeterminado y no especifica ningún valor para Enviar desde, pueden producirse errores. Para asegurarse de que los mensajes de correo electrónico tengan la dirección remitente correcta, especifique un valor para la configuración Enviar desde.

**SSL SMTP habilitado:** Seleccione esta configuración para forzar al proveedor de correo electrónico a usar SSL para analizar la bandeja de entrada. Asegúrese de que el servidor de correo admita SSL.

**Carpeta de correo electrónico enviado con error:** Especifica un directorio en el que almacenar los resultados si el servidor de correo SMTP no está operativo.

**asincrónico:** Cuando se establece en sincrónico, se procesan todos los documentos de entrada y se devuelve una única respuesta. Cuando se establece en asíncrono, se envía una respuesta por cada documento procesado.

Por ejemplo, se crea un extremo de correo electrónico para un servicio que toma un único documento de Word y devuelve ese documento como un archivo de PDF. Se puede enviar un correo electrónico a la bandeja de entrada del extremo que contiene varios (3) documentos de Word. Cuando se procesan los tres documentos, si el punto de conexión está configurado como sincrónico, se envía un único correo electrónico de respuesta con los tres documentos adjuntos. Si el extremo es asincrónico, se envía un mensaje de correo electrónico de respuesta después de convertir cada documento de Word en PDF. El resultado son tres correos electrónicos, cada uno con un solo archivo adjunto de PDF.

El valor predeterminado es asíncrono.

**Incluir el cuerpo original del correo electrónico como datos adjuntos:** De forma predeterminada, cuando envía un correo electrónico al servidor de Forms, el texto original del mensaje se incluye en el cuerpo del mensaje. Para incluir el texto como datos adjuntos, seleccione esta opción.

**Usar la línea de asunto original para los mensajes de correo electrónico con resultados:** De forma predeterminada, el servidor de Forms usa los valores especificados en la configuración Asunto del mensaje de correo electrónico de éxito y Asunto del correo electrónico de error como línea de asunto al enviar mensajes de correo electrónico con resultados. Para utilizar en su lugar la misma línea de asunto que el correo electrónico original enviado al servidor, seleccione esta opción.

**Asunto del correo electrónico de éxito:** Después de enviar un correo electrónico a un extremo de correo electrónico para iniciar o continuar un proceso, recibirá un mensaje de correo electrónico de retorno del servidor de AEM Forms. Si el correo electrónico se ha enviado correctamente, recibirá un mensaje de correo electrónico con el resultado deseado. Si el correo electrónico falla, recibe un correo electrónico que le informa de por qué ha fallado. Esta configuración le permite especificar la línea de asunto de los mensajes de correo electrónico de éxito enviados para este punto de conexión.

**Cuerpo del mensaje de correo electrónico de éxito:** Permite especificar el texto del cuerpo de los mensajes de correo electrónico de éxito enviados para este extremo.

**Prefijo del asunto del correo electrónico de error:** Permite especificar el texto utilizado al principio de la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo.

**Asunto del correo electrónico de error:** Permite especificar la línea de asunto de los mensajes de correo electrónico de error enviados para este extremo. Este texto se muestra después del prefijo del asunto del correo electrónico de error.

**Cuerpo del mensaje de correo electrónico de error:** Permite especificar la primera línea del texto del cuerpo de los mensajes de correo electrónico de error enviados para este extremo.

**Información de resumen de correo electrónico:** Cada mensaje de éxito o error incluye una sección que contiene el texto original del correo electrónico enviado al servidor de Forms. Esta configuración especifica el texto que aparece encima de esa sección.

**Validar Bandeja de entrada antes de crear o actualizar este extremo:** Cuando se selecciona esta opción, el servidor de Forms comprueba si la configuración de SMTP/POP3 es correcta antes de crear el extremo. Al hacer clic en Agregar, aparece un mensaje que indica si la cuenta de la bandeja de entrada es válida. Si esta opción no está seleccionada, el servidor de AEM Forms crea el extremo sin validar la bandeja de entrada.

**Nombre de operación:** Esta configuración es obligatoria. Una lista de operaciones que se pueden asignar al extremo de correo electrónico. La operación que seleccione aquí determina qué campos se muestran en las secciones Asignaciones de parámetros de entrada y Asignaciones de parámetros de salida.

**Asignaciones de parámetros de entrada:** Se usa para configurar la entrada necesaria para procesar el servicio y la operación. Los dos tipos de entrada son literales y variables:

**Literal:** El correo electrónico utiliza el valor introducido en el campo tal como se muestra.

**Variable:** Puede asignar una cadena a partir del asunto, cuerpo, encabezado o dirección de correo electrónico del remitente. Para ello, utilice una de las siguientes palabras clave: %SUBJECT%, %BODY%, %HEADER% o %SENDER%. Por ejemplo, si utiliza %SUBJECT%, el contenido del asunto del correo electrónico se utiliza como parámetro de entrada. Para recoger archivos adjuntos, introduzca un patrón de archivo que el extremo de correo electrónico pueda utilizar para seleccionar los documentos adjuntos. Por ejemplo, al escribir &ast;.pdf se selecciona cualquier documento adjunto que tenga la extensión de nombre de archivo .pdf. Al introducir &ast; se selecciona cualquier documento adjunto. Al introducir example.pdf, se selecciona cualquier documento adjunto denominado example.pdf.

**Asignaciones de parámetros de salida:** Se usó para configurar la salida del servicio y la operación. Los siguientes caracteres de los valores de asignación de parámetros de salida se expanden en el nombre del archivo adjunto:

**%F** Representa el nombre de archivo del archivo de origen (sin incluir una extensión).

**%E** Representa la extensión del archivo de origen.

Cualquier aparición de la barra invertida (\) se reemplaza por %%.

***nota &#x200B;**: si el mensaje de solicitud de servicio incluye varios archivos adjuntos, no puede usar los parámetros %F y %E para la propiedad Asignaciones de parámetros de salida del extremo. Si la respuesta de los servicios devuelve varios archivos adjuntos, no se puede especificar el mismo nombre de archivo para más de un archivo adjunto. Si no sigue estas recomendaciones, el servicio invocado creará los nombres de los archivos devueltos y los nombres no serán predecibles.*

Los valores disponibles son los siguientes:

**Objeto único:** El proveedor de correo electrónico no tiene el destino de la carpeta de origen; los resultados se devuelven como datos adjuntos. El patrón es Result/%F.ps y devuelve Result%%sourcefilename.ps como datos adjuntos del nombre de archivo.

**Lista:** El patrón es Result/%F/ y devuelve Result%%sourcefilename%%file1 como archivo adjunto.

**Mapa:** El patrón es Result/%F/ y el destino de origen es Result%%sourcefilename%%file1 y Result%%sourcefilename%%file2. Si la asignación contiene más de un objeto y el patrón es Result/%F.ps, los archivos adjuntos de respuesta son Result%%sourcefilename1.ps (salida 1) y Result%%sourcefilename2.ps (salida 2).

## Crear un extremo de correo electrónico para el servicio Tarea completa {#create-an-email-endpoint-for-the-complete-task-service}

Para que el flujo de trabajo de formularios reciba y administre mensajes de correo electrónico entrantes de los usuarios, debe crear un punto final de correo electrónico para el servicio Tarea completa.

1. En la consola de administración, haga clic en Servicios > Aplicaciones y servicios > Administración de servicios.
1. En la página Administración de servicios, haga clic en el servicio Completar tarea.
1. En la pestaña Puntos finales, seleccione Correo electrónico en la lista desplegable y haga clic en Agregar.
1. En el cuadro Host de la Bandeja de entrada, escriba el nombre de host o la dirección IP del servidor de correo.
1. En el cuadro Usuario de la bandeja de entrada, escriba el nombre de usuario necesario para iniciar sesión en la cuenta de correo electrónico que ha creado para gestionar los envíos de formularios. Según el servidor de correo electrónico y la configuración, este nombre puede ser solo la parte del nombre de usuario del correo electrónico o puede ser la dirección de correo electrónico completa.
1. En el cuadro Contraseña de la Bandeja de entrada, escriba la contraseña del Usuario de la Bandeja de entrada.
1. En el cuadro Host SMTP, escriba el nombre de host o la dirección IP del servidor de correo desde el que el proveedor de correo electrónico envía los resultados y los mensajes de error.
1. En el cuadro Usuario de SMTP, escriba la cuenta de usuario que el proveedor de correo electrónico utilizará cuando envíe correos electrónicos para obtener resultados y errores. Esta cuenta de usuario puede tener el mismo valor que utilizó para el usuario de la bandeja de entrada.
1. En el cuadro Contraseña SMTP, escriba la contraseña de la cuenta SMTP.
1. En la lista Nombre de operación, seleccione invocar.
1. En la lista attachmentMap, seleccione Variable y escriba `*.*` en el cuadro adyacente. Esto envía todos los archivos adjuntos de los mensajes de correo entrante a una variable de asignación para el proceso de completar tarea.
1. En la lista mailBody, seleccione la variable y escriba `%BODY%` en el cuadro adyacente.
1. En la lista mailFrom, seleccione Variable y escriba `%SENDER%` en el cuadro adyacente. Esto asigna la dirección del remitente a los datos del proceso de la tarea completa.
1. En el cuadro de resultados, escriba `results`. Esto hace que Complete Task o Start Process devuelvan una cadena de resultado.
1. Haga clic en Agregar.
