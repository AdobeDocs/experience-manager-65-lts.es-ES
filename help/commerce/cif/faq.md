---
title: Preguntas frecuentes sobre la integración de AEM con Commerce mediante Commerce Integration Framework
description: Preguntas frecuentes sobre la integración de AEM con Commerce mediante Commerce Integration Framework
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 66%

---

# Preguntas frecuentes sobre la integración de AEM con Commerce mediante Commerce Integration Framework

## 1. ¿CIF GraphQL solo se utiliza para fines comerciales o está disponible para consultar contenido creado en JCR de AEM?

Adobe ha adoptado las API GraphQL de Adobe Commerce como sus API comerciales oficiales para todos los datos relacionados con el comercio. Por lo tanto, AEM utiliza GraphQL para intercambiar datos de comercio con Adobe Commerce y con cualquier motor de comercio a través de I/O Runtime. Esta API de GraphQL es independiente de la API GraphQL de AEM para acceder a los fragmentos de contenido.

## 2. ¿Se pueden almacenar los activos de producto (imágenes) y hacer referencia a ellos desde AEM mediante el administrador de Adobe Commerce? ¿Cómo se pueden consumir los activos de Dynamic Media?

No hay AEM Assets oficiales: la integración de Adobe Commerce está disponible. Hay un conector de socio disponible en [Marketplace](https://marketplace.magento.com/partner/bounteous_ecomm).

O bien, como solución alternativa, puede almacenar los recursos de productos (imágenes) en AEM Assets, pero debe almacenar manualmente las direcciones URL de los recursos en Adobe Commerce. Dynamic Media forma parte de los AEM Assets y funciona del mismo modo.

## 3. ¿Importa dónde se implemente la solución de comercio? (Local o en la nube)

No, no importa dónde se implemente su solución de comercio. CIF y la tienda de AEM funcionan independientemente del modelo de implementación. Sin embargo, si la solución se implementa con la arquitectura de referencia E2E recomendada, las pruebas E2E pueden ejecutarse con KPI de rendimiento que representen un perfil de cliente empresarial típico. Este proceso proporciona información adicional que puede utilizarse como referencia.

## 4. ¿Cómo se crean las páginas de catálogo o de producto en AEM? ¿Cómo persisten en AEM?

Las páginas de catálogo y las páginas de producto se crean y almacenan en caché de forma dinámica en AEM según las plantillas de catálogo y de página de producto genéricas. No se importan ni almacenan datos de producto o catálogo en AEM.

## 5. Cuando se actualizan los datos del producto en su solución de comercio, ¿se trata de una inserción a AEM en tiempo real? ¿O es un proceso por lotes?

El complemento de CIF que se utiliza con AEM permite que los datos fluyan de la solución de comercio a AEM bajo demanda. Por lo tanto, este flujo de trabajo no es una inserción en tiempo real ni un proceso por lotes cuando hay una actualización en la solución de comercio.

## 6. ¿Qué tamaño de catálogo admite AEM con CIF?

La compatibilidad con el tamaño del catálogo depende de algunos aspectos adicionales que debe tener en cuenta. ¿Cuál es la proporción de caché de los datos y las páginas del catálogo? ¿Cuántas solicitudes simultáneas espera durante las horas de mayor actividad? ¿En qué medida son escalables las API de sus soluciones de comercio?

## 7. ¿Cómo actúa GIP en este marco?

Los datos de PIM se exponen a AEM y a los clientes a través de solicitudes de GraphQL. La recomendación de Adobe es integrar PIM con el motor de comercio (Adobe Commerce u otros) para que los datos PIM puedan recuperarse del motor de comercio.

## 8. También se almacenan en caché los precios y otros datos a través de Dispatcher. ¿Genera esto un desafío frecuente de invalidación de caché?

Los datos dinámicos, como el precio o el inventario no se almacenan en la caché de Dispatcher. Los datos dinámicos se recuperan del lado del cliente con los componentes web directamente a través de las API de GraphQL. Solo los datos estáticos (como los datos de producto o categoría) se almacenan en la caché de Dispatcher. Si los datos del producto cambian, es necesaria la invalidación de la caché.

## 9. ¿Cómo funciona la invalidación de caché para Dispatcher de AEM con AEM y Commerce?

Adobe recomienda configurar la invalidación de caché basada en TTL para las páginas almacenadas en caché de Dispatcher. Para obtener información dinámica como precio o acciones, Adobe recomienda procesar la fecha del lado del cliente. Para obtener más información sobre la invalidación de caché basada en TTL, consulte [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=es)

## 10. ¿Existe alguna recomendación sobre la búsqueda unificada en los contenidos de AEM con Comercio?

Se proporciona una implementación de referencia de búsqueda de productos, pero no una búsqueda unificada con contenido. Esta función es específica del cliente y se resuelve mejor en un nivel específico del proyecto.

## 11. ¿Cómo funciona la búsqueda con AEM y Commerce mediante CIF?

CIF proporciona los componentes de la barra de búsqueda y el resultado de búsqueda. El componente Barra de búsqueda envía una solicitud de GraphQL con el término buscado a la solución de comercio que, a continuación, devuelve una lista de productos que incluye el nombre del producto, el precio, las anotaciones, etc. A continuación, el componente Resultados de búsqueda muestra los resultados de búsqueda en una vista de galería en una página de resultados de búsqueda creada en AEM. La búsqueda admite la búsqueda básica de texto completo. Utilice la clave SLUG/url para crear una referencia al PDP.

## 12. ¿Cómo se pueden utilizar los datos del producto en MSM o en las traducciones?

Los datos del producto generalmente ya están trasladados en GIP o en Adobe Commerce. La integración AEM y Adobe Commerce admite la conexión a varias tiendas y vistas de tiendas de Adobe Commerce. En una configuración de MSM, normalmente un sitio de AEM está vinculado a una vista de tienda de Adobe Commerce.

## 13. ¿Existe alguna manera de mejorar los datos del producto con texto comercial? En caso afirmativo, ¿dónde se lleva a cabo? ¿En AEM o en la solución de comercio?

Adobe recomienda administrar los datos y el contenido relacionados con el marketing en AEM. Incluya los datos de producto de su solución de comercio y atributos adicionales mediante fragmentos de contenido o cree y vincule fragmentos de experiencias para contenido no estructurado con sus productos.

## 14. ¿Cómo garantiza una empresa la conformidad con PCI al utilizar AEM para toda la capa de presentación?

Adobe recomienda utilizar métodos de pago abstractos. Al hacerlo, el cliente del explorador se pone en comunicación directa con el proveedor de la puerta de enlace de pago para que Adobe no tenga ni pase la fecha del titular de la tarjeta ni las soluciones comerciales. Este enfoque solo requiere un nivel 3 de conformidad con PCI. Sin embargo, hay cosas adicionales que considerar para que sea totalmente compatible con PCI, como por ejemplo cómo los empleados interactúan con el sistema y los datos. Para obtener más información acerca del cumplimiento de PCI Adobe Commerce, consulte [Cumplimiento de PCI](https://business.adobe.com/products/magento/pci-compliance.html?lang=es)

## 15. Si utilizo versiones en la nube de AEM y Adobe Commerce, ¿es compatible esta solución conjunta con PCI?

Sí, el cuestionario de autoevaluación D y la certificación de conformidad están disponibles bajo petición.

## 16. ¿Cómo puedo solicitar una licencia de prueba de I/O Runtime?

Consulte [Obtener acceso](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/) para obtener detalles sobre cómo solicitar una licencia de prueba para usar I/O Runtime.
