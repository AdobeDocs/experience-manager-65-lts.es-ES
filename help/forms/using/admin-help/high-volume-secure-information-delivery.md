---
title: Entregar información segura de gran volumen
description: La seguridad de los documentos admite la asociación de licencias a usuarios, en lugar de a documentos en entornos de producción masiva.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 2%

---

# Entregar información segura de gran volumen {#high-volume-secure-information-delivery}

En un entorno de producción masiva, como el que genera facturas mensuales seguras para una empresa de telecomunicaciones, la creación de licencias específicas para cada documento puede convertirse en un proceso que requiera muchos recursos. En estos casos, Document Security admite la asociación de licencias a usuarios, en lugar de a documentos. La licencia generada para un usuario se utiliza para todos los documentos protegidos para ese usuario.

Una ventaja de este enfoque es que el tamaño de la base de datos de seguridad de los documentos no aumenta de forma lineal con los documentos, sino con el número de usuarios. Además, dado que necesita crear la licencia solo una vez para un usuario, la protección posterior de los documentos a través de estas políticas se vuelve más rápida. Las funciones como el acceso sin conexión, la caducidad y la revocación de documentos son compatibles con todos estos documentos.

La seguridad de los documentos también admite directivas abstractas. Las directivas abstractas son plantillas de directiva que contienen todos los atributos de directiva, como la configuración de seguridad de los documentos y los derechos de uso, pero no contienen una lista de principales. Los administradores pueden crear cualquier número de directivas a partir de la directiva abstracta con diferentes entidades principales que deben tener acceso a los documentos. Los cambios realizados en la política abstracta no afectan a las políticas reales que se generan a partir de las políticas abstractas.

Si una empresa de telecomunicaciones genera una factura mensual, se crea una directiva abstracta, se crean usuarios y, a continuación, se generan licencias únicas para cada usuario. Las licencias se aplican posteriormente a los documentos de cada usuario.

La creación de una política abstracta solo es compatible mediante la seguridad de los documentos Java SDK. Sin embargo, puede administrar las directivas que cree a partir de la directiva abstracta de las páginas web de Document Security. Las directivas creadas con este método tienen un comportamiento idéntico al de las páginas web de Document Security.

Consulte [Programar con formularios AEM](https://www.adobe.com/go/learn_aemforms_programming_63) para obtener más información.
