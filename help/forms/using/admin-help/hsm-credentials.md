---
title: Administrar credenciales HSM
description: Obtenga información sobre cómo administrar las credenciales de HSM. Puede administrar HSM desde la página Administración de almacén de confianza. Puede ver, comprobar, actualizar, restablecer y eliminar componentes HSM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 5e9e0371-018a-496f-aad4-04ff21391d51
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 4%

---

# Administrar credenciales HSM {#managing-hsm-credentials}

Desde la página Administración de almacén de confianza, puede administrar las credenciales del Módulo de seguridad de hardware (HSM). Un HSM es un dispositivo PKCS#11 de terceros que puede utilizar para generar y almacenar claves privadas de forma segura. El HSM protege físicamente el acceso a las claves privadas y su uso.

El software cliente es necesario para comunicarse con el HSM. El software cliente HSM debe instalarse y configurarse en el mismo equipo que los formularios AEM.

Las firmas digitales de formularios de AEM pueden utilizar credenciales almacenadas en un HSM para aplicar firmas digitales del lado del servidor. Siga las instrucciones de esta sección para crear un alias para cada credencial HSM que utilizará Firmas digitales. El alias contiene todos los parámetros requeridos por el HSM.

>[!NOTE]
>
>Después de cambiar la configuración de HSM, reinicie AEM Forms Server.

## Crear un alias para una credencial HSM cuando el dispositivo HSM esté en línea {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-online}

>[!NOTE]
> 
> Asegúrese de que el usuario tenga privilegios de administrador para acceder a la consola de administrador.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM y, a continuación, haga clic en Agregar.
1. En el cuadro Nombre del perfil, escriba una cadena utilizada para identificar el alias. Este valor se utiliza como propiedad en algunas operaciones de firmas digitales, como la operación Firmar campo de firma.
1. En el cuadro Biblioteca PKCS11, escriba la ruta de acceso completa de la biblioteca de cliente HSM en el servidor. Por ejemplo, `c:\Program Files\LunaSA\cryptoki.dll`. En un entorno en clúster, esta ruta debe ser idéntica para todos los servidores del clúster.
1. Haga clic en Probar conectividad HSM. Si los formularios AEM Forms pueden conectarse al dispositivo HSM, se muestra un mensaje que indica que el HSM está disponible. Haga clic en Siguiente.
1. Utilice el nombre del token, el ID de ranura o el índice de lista de ranura para identificar dónde se almacenan las credenciales en el HSM.

   * **Nombre de token:** Corresponde al nombre de la partición HSM que se va a usar (por ejemplo, HSMPART1).
   * **Id. de ranura:** El Id. de ranura es un identificador de ranura de tipo de datos de tipo largo.
   * **Índice de lista de ranura:** Si selecciona Índice de lista de ranura, establezca la Información de ranura en un número entero que corresponda a la ranura. Este es un índice basado en 0, lo que significa que si el cliente se registra primero con la partición HSMPART1, se hará referencia a HSMPART1 utilizando el valor 0 de SlotListIndex.

1. En el cuadro Token Pin, escriba la contraseña necesaria para acceder a la clave HSM y haga clic en Siguiente.
1. En el cuadro Credenciales, seleccione una credencial. Haga clic en Guardar.

## Crear un alias para una credencial HSM cuando el dispositivo HSM está sin conexión {#create-an-alias-for-an-hsm-credential-when-the-hsm-device-is-offline}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM y, a continuación, haga clic en Agregar.
1. En el cuadro Nombre del perfil, escriba una cadena utilizada para identificar el alias. Este valor se utiliza como propiedad en algunas operaciones de firmas digitales, como la operación Firmar campo de firma.
1. En el cuadro Biblioteca PKCS11, escriba la ruta de acceso completa de la biblioteca de cliente HSM en el servidor. Por ejemplo, `c:\Program Files\LunaSA\cryptoki.dll`. En un entorno en clúster, esta ruta debe ser idéntica para todos los servidores del clúster.
1. Seleccione la casilla de verificación Creación de perfiles sin conexión. Haga clic en Siguiente.
1. En la lista Dispositivo HSM, seleccione el fabricante del dispositivo HSM donde se almacena la credencial.
1. En la lista Tipo de Ranura, seleccione ID de Ranura, Índice de Ranura o Nombre de Token y especifique un valor en el cuadro Información de Ranura. Los formularios AEM Forms utilizan esta configuración para determinar dónde se almacenan las credenciales en el HSM.

   * **Nombre de token:** Corresponde a un nombre de partición (por ejemplo, HSMPART1).
   * **Id. de ranura:** El Id. de ranura es un número entero que corresponde a la ranura, que a su vez corresponde a una partición. Por ejemplo, el cliente (Forms Server) se registró primero con la partición HSMPART1. Esto asigna la ranura 1 a la partición HSMPART1, para este cliente. Como HSMPART1 es la primera partición registrada, el ID de ranura es 1 y establecería Información de ranura en 1.

     El ID de ranura se establece cliente por cliente. Si registró una segunda máquina en una partición diferente (por ejemplo, HSMPART2 en el mismo dispositivo HSM), entonces la ranura 1 se asociaría con la partición HSMPART2 para ese cliente.

   * **Índice de ranura:** Si selecciona Índice de ranura, establezca la Información de ranura en un número entero que corresponda a la ranura. Este es un índice basado en 0, lo que significa que si el cliente se registra primero con la partición HSMPART1, la ranura 1 se asigna a HSMPART1 para este cliente. Como HSMPART1 es la primera partición registrada, el índice de ranura es 0.

1. Seleccione una de estas opciones y proporcione la ruta:

   * **Certificado**: (No es necesario si usa SHA1) Haga clic en Examinar y busque la ruta de acceso a la clave pública de la credencial que está usando.
   * **Certificado SHA1:** (no obligatorio si se usa un certificado físico) Escriba el valor SHA1 (huella digital) del archivo de clave pública (.cer) de la credencial que está utilizando. Asegúrese de que no haya espacios utilizados en el valor SHA1.

1. En el cuadro Contraseña, escriba la contraseña necesaria para acceder a la clave HSM de la información de ranura especificada y, a continuación, haga clic en Guardar.

## Ver propiedades de alias de credenciales HSM {#view-hsm-credential-alias-properties}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en el nombre de alias del alias de la credencial para ver las propiedades y, a continuación, haga clic en Aceptar.

## Comprobar el estado de una credencial HSM {#check-the-status-of-an-hsm-credential}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en la casilla de verificación situada junto a la credencial que desea comprobar y, a continuación, haga clic en Comprobar estado.

La columna Estado refleja el estado actual de la credencial. Si se produce un error, se muestra una X roja en la columna Estado. Pase el ratón sobre la X para ver la información del objeto que contiene el motivo del error.

## Actualizar propiedades de alias de credenciales HSM {#update-hsm-credential-alias-properties}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en el nombre del alias de la credencial.
1. Haga clic en Actualizar credencial y actualice la configuración según sea necesario.

## Restablecer todas las conexiones HSM {#reset-all-hsm-connections}

Restablezca las conexiones abiertas a un dispositivo HSM después de cualquier interrupción de la sesión de red entre el servidor de Forms y el dispositivo HSM. Por ejemplo, las interrupciones pueden producirse debido a una interrupción de la red o a que el dispositivo HSM se desconecta para una actualización de software. Después de una interrupción, las conexiones existentes están obsoletas y cualquier solicitud de firma contra esas conexiones falla. Al utilizar la opción Restablecer todas las conexiones HSM se borran las conexiones antiguas.

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Haga clic en Restablecer todas las conexiones HSM.

## Eliminar un alias de credencial HSM {#delete-an-hsm-credential-alias}

1. En la consola de administración, haga clic en Configuración > Administración de almacén de confianza > Credenciales de HSM.
1. Seleccione las casillas de verificación de las credenciales de HSM que desee eliminar, haga clic en Eliminar y, a continuación, haga clic en Aceptar.

## Configuración de la compatibilidad remota con HSM {#configure-remote-hsm-support}

Los formularios AEM utilizan un mecanismo IPC/RPC basado en servicios web. Este mecanismo permite que los formularios AEM utilicen un HSM instalado en un equipo remoto. Para utilizar esta funcionalidad, instale el servicio web en el equipo remoto donde esté instalado el HSM. Para obtener más información, consulte [Configuración de la compatibilidad con HSM para formularios AEM Forms ES mediante el uso de Sun JDK en la plataforma Windows de 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html).

Este mecanismo no admite la creación en línea de perfiles HSM o comprobaciones de estado. Sin embargo, hay dos formas de crear perfiles HSM y realizar comprobaciones de estado:

* Cree una credencial de cliente de formularios AEM al pasarle el certificado del firmante. Siga los pasos de [Configuración de la compatibilidad con HSM para formularios AEM ES mediante Sun JDK en la plataforma Windows de 64 bits](https://kb2.adobe.com/cps/808/cpsid_80835.html). La ubicación del servicio web se pasa como una propiedad Credential. También se admiten perfiles HSM sin conexión creados mediante el certificado DER o el certificado SHA-1 hex. Sin embargo, si ha actualizado a formularios AEM Forms desde una versión anterior de formularios AEM, realice cambios en el cliente porque la credencial contenía información de certificados y servicios web.
* La ubicación del servicio Web se especifica en la consola de administración del servicio Signature. (Consulte [Configuración del servicio de firma](/help/forms/using/admin-help/configure-service-settings.md#signature-service-settings).) En este caso, el cliente solo llevaba el alias del perfil HSM en el almacén de confianza. Puede utilizar esta opción sin problemas sin ningún cambio de cliente, incluso si ha actualizado a formularios AEM desde una versión anterior de formularios AEM. Esta opción no admite perfiles HSM que utilicen el certificado SHA-1.
