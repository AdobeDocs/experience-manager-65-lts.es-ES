---
title: Instalar y configurar Designer
description: Designer está disponible como programa de instalación independiente y se integra con Workbench. Aprenda a instalar Designer de forma independiente.
role: Admin, User, Developer
feature: Forms Designer,Designer
solution: Experience Manager, Experience Manager Forms
source-git-commit: 1444b0fc0811cbb187d2a4d83b626444e44ef73f
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 23%

---

# Instalar y configurar Designer{#installing-and-configuring-designer}

## Requisitos previos {#pre-requisites}

+++ Para AEM Forms Designer de 64 bits (recomendado)

* Instale la versión de 64 bits de [Visual C++ 2019 redistribuible (x64)](https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación.
* Un usuario con derechos de administrador para instalar o desinstalar AEM Forms Designer.

+++

+++ Para AEM Forms Designer de 32 bits

* Instale la versión de 32 bits de [Visual C++ 2019 redistribuible (x64)](https://learn.microsoft.com/es-es/cpp/windows/latest-supported-vc-redist?view=msvc-170). Asegúrese de que los paquetes de ejecución redistribuibles anteriores estén instalados antes de iniciar la instalación.
* Un usuario con derechos de administrador para instalar o desinstalar AEM Forms Designer.

+++

>[!NOTE]
>
>* La versión de 64 bits del diseñador se introdujo con AEM 6.5 Forms Service Pack 19 (6.5.19.0).
>* La versión de 32 bits del diseñador está obsoleta desde el lanzamiento de [AEM Forms Service Pack 21 (6.5.21.0)](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).
> * Las plataformas compatibles con Forms Designer se alinean con las plataformas compatibles con AEM Forms. Para obtener más información sobre las plataformas compatibles con Forms Designer, [haga clic aquí](/help/forms/using/aem-forms-jee-supported-platforms.md).

Para obtener más información sobre la instalación de Forms Designer, visite [Preguntas más frecuentes](#fandq).

## Instalación de AEM Forms Designer {#install-designer}

Designer está disponible como programa de instalación independiente y se integra con Workbench. Si utiliza un programa de instalación independiente para AEM Forms Designer, realice los siguientes pasos:

1. Desinstale la versión anterior de AEM Forms Designer, si ya está instalada.
1. Descargue AEM Forms Designer de 64 bits (recomendado) o AEM Forms Designer de 32 bits según sus necesidades.

   >[!NOTE]
   > 
   >* Forms Designer de 32 bits está programado para dejar de utilizarse con AEM 6.5 Forms Service Packs 20 (6.5.20.0). Adobe recomienda actualizar a Forms Designer de 64 bits.
   >* Forms Designer de 64 bits solo está disponible para AEM 6.5 Forms Service Packs 19 (6.5.19.0) o versiones posteriores.
   >* Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0) y versiones posteriores Forms Designer también incluye la versión Service Pack. Por ejemplo, para el paquete de servicio 15 el número de versión es 6.5.15.20221112.1.0. En este ejemplo, 6.5.15 es la versión del paquete de servicio.

1. Inicie el programa de instalación de AEM Forms Designer haciendo doble clic en setup.exe.
1. Continúe y proporcione sus detalles y el número de serie en la pantalla de Personalization.

   >[!NOTE]
   >
   >* Obtenga su clave de licencia de Forms Designer en [Sitio web de licencias de Adobe](https://licensing.adobe.com/).

1. Si acepta el acuerdo de licencia, haga clic en Siguiente para continuar.
1. (Opcional) Si desea instalar Designer en una ubicación de su elección, modifique la ruta de instalación. Haga clic en Siguiente.
1. Haga clic en Atrás para cambiar las preferencias. Para instalar Designer, haga clic en Instalar.
1. Haga clic en Finalizar cuando finalice la instalación.

Como alternativa, puede instalar AEM Forms Designer a través de la línea de comandos utilizando el modo pasivo o silencioso.

* Instalación pasiva desde la línea de comandos: el programa de instalación muestra una barra de progreso que indica que la instalación está en curso, pero que no se muestran avisos ni mensajes de error. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Instalación silenciosa desde la línea de comandos: el programa de instalación ejecuta la instalación sin mostrar una interfaz de usuario. No se muestran avisos, mensajes ni cuadros de diálogo. Una vez iniciada, no puede cancelar la instalación.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## Actualizar AEM Forms Designer {#update-forms-designer}

Hay dos casos al actualizar la última versión de AEM Forms Designer 6.5.16.0:

* **Caso 1**: Cuando el usuario tiene una versión de AEM Forms Designer anterior a 6.5.15.0.
* **Caso 2**: Cuando el usuario tiene 6.5.15.0 versión de AEM Forms Designer.

+++**Cuando el usuario tiene una versión de AEM Forms Designer anterior a 6.5.15.0.**

Si utiliza un programa de instalación independiente para AEM Forms Designer, realice los siguientes pasos:

1. Antes de instalar **AEM Forms Designer6.5.16.0**, los usuarios deben desinstalar todas las versiones anteriores.
1. Descargue e instale [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) desde la página Versiones de formularios de AEM.
1. Después de instalar correctamente **AEM Forms Designer6.5.15.0**, descargue e instale [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es) haciendo doble clic en el archivo de instalación descargado

+++

+++**Cuando el usuario tiene 6.5.15.0 AEM Forms Designer versión**

Si utiliza un programa de instalación independiente para AEM Forms Designer, realice los siguientes pasos:
1. Descargue la versión más reciente de AEM Forms Designer desde el [Portal de distribución de software](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=es).
1. Instale la última versión de AEM Forms Designer haciendo doble clic en el archivo de instalación descargado.

+++

## Preguntas frecuentes {#fandq}

* **¿Puede un usuario actualizar o instalar directamente el diseñador de 64 bits?**
   * Sí, los usuarios pueden actualizar o instalar directamente Designer de 64 bits. Para actualizar, instale el programa de instalación completo del diseñador [SP19](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/Designer-Patch/sp19_x64/aemforms_designer_6_5_0_wwe_win.zip) y aplique la versión posterior del parche del diseñador sobre eso.

     >[!NOTE]
     > Antes de actualizar a Designer de 64 bits, desinstale primero Designer de 32 bits, si existe.

* **¿Pueden los usuarios mantener instalados en el sistema tanto los de 32 bits como los de 64 bits?**
   * No, la instalación de 32 y 64 bits no funcionará en el mismo equipo. El usuario puede tener un diseñador de 32 bits o uno de 64 bits.

* **¿Cómo comprueba si un usuario tiene un diseñador de 64 bits o de 32 bits?**
   * Existen dos formas de comprobar la versión de Forms Designer:

      1. Abra Designer, vaya a la Ayuda, haga clic en Acerca de Designer y verá información sobre la versión del diseñador junto con la información de bits. Por ejemplo, verá que 64 bits está escrito al final de la versión, como se muestra a continuación:
         `6.5.21.20240522.1.161 | 64 bit`
      1. Abra Designer, en la parte superior izquierda verá un icono de marca que contiene información de 64 bits con el nombre del producto.

