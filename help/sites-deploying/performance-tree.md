---
title: Árbol de rendimiento
description: Obtenga información acerca de los pasos que se deben seguir para solucionar problemas de rendimiento en AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: c83fcf96-cc45-40a0-9a50-c60406096de1
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 9%

---

# Árbol de rendimiento{#performance-tree}

## Ámbito {#scope}

El diagrama siguiente tiene por objeto proporcionar instrucciones sobre los pasos que se deben seguir para solucionar los problemas de rendimiento. Se divide en cinco secciones para facilitar la lectura.

Cada paso del diagrama está vinculado a un recurso de documentación o a una recomendación.

## Requisitos previos y suposiciones {#prerequisites-and-assumptions}

Se supone que se observa un problema de rendimiento en una página determinada (una consola de AEM o una página web) y que se puede reproducir de forma coherente. Tener una forma de probar o monitorear el rendimiento es un requisito previo antes de comenzar la investigación.

El análisis comienza en el paso 0. El objetivo es determinar qué entidad (Dispatcher, host externo o AEM) es responsable del problema de rendimiento y luego determinar qué área (servidor o red) debe investigarse.

### Sección 1 {#section}

![chlimage_1-103](assets/chlimage_1-103.png)

### Sección 2 {#section-1}

![chlimage_1-104](assets/chlimage_1-104.png)

### Sección 3 {#section-2}

![chlimage_1-105](assets/chlimage_1-105.png)

### Sección 4 {#section-3}

![chlimage_1-106](assets/chlimage_1-106.png)

### Sección 5 {#section-4}

![chlimage_1-107](assets/chlimage_1-107.png)

## Vínculos de referencia {#reference-links}

<table>
 <tbody>
  <tr>
   <td><strong>Paso</strong></td>
   <td><strong>Título</strong></td>
   <td><strong>Recursos</strong></td>
  </tr>
  <tr>
   <td><strong>Etapa 0</strong></td>
   <td>Analizar flujo de solicitudes</td>
   <td><p>Puede utilizar el análisis de solicitud HTTP estándar en el explorador para analizar el flujo de solicitud. Para obtener más información acerca de cómo realizar este análisis en Chrome, vea:<br /> </p> <p><a href="https://developers.google.com/web/tools/chrome-devtools/profile/network-performance/resource-loading">https://developer.chrome.com/docs/devtools/</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 2</strong></td>
   <td>¿Las solicitudes provienen de hosts externos?</td>
   <td>Puede utilizar el análisis de solicitud HTTP estándar en el explorador para analizar el flujo de solicitud. Consulte los vínculos anteriores sobre cómo realizar este análisis en Chrome.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 3</strong></td>
   <td>¿Se pueden almacenar en caché las solicitudes?</td>
   <td>Para obtener más información sobre solicitudes almacenables en caché y consejos generales sobre optimización del rendimiento de Dispatcher, consulte <a href="/help/sites-deploying/configuring-performance.md#optimizing-performance-when-using-the-dispatcher">Optimización del rendimiento de Dispatcher</a>.</td>
  </tr>
  <tr>
   <td><strong>Etapa 4</strong></td>
   <td>¿Las solicitudes provienen de Dispatcher?</td>
   <td><p>Para ver si las solicitudes se almacenan en la caché correctamente, consulte la <a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#debugging">documentación de depuración de Dispatcher</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 5</strong></td>
   <td>¿Dispatcher está intentando autenticar cada solicitud a través de AEM?</td>
   <td>Compruebe si Dispatcher envía <code>HEAD</code> solicitudes a AEM para la autenticación antes de enviar el recurso en caché. Busque <code>HEAD</code> solicitudes en AEM <code>access.log</code>. Para obtener más información, consulte <a href="/help/sites-deploying/configure-logging.md">Registro</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 6</strong></td>
   <td>¿La ubicación geográfica de Dispatcher está lejos de los usuarios?</td>
   <td>Acerca Dispatcher a los usuarios.</td>
  </tr>
  <tr>
   <td><strong>Etapa 7</strong></td>
   <td>¿Es correcta la capa de red de Dispatcher?</td>
   <td><br /> Investigue la capa de red para ver si hay problemas de saturación y latencia.<p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 8</strong></td>
   <td>¿La lentitud es reproducible con una instancia local?</td>
   <td><br /> <p>Use <a href="/help/sites-developing/tough-day.md">Día difícil</a> para replicar las condiciones "reales" de las instancias de producción. Si este escenario no es realista para el espacio de desarrollo, asegúrese de probar la instancia de producción (o una instancia de ensayo idéntica) en un contexto de red diferente.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 9</strong></td>
   <td>¿La ubicación geográfica del servidor está lejos de los usuarios?</td>
   <td>Acerque el servidor a los usuarios.</td>
  </tr>
  <tr>
   <td><strong>Pasos 10 y 29</strong></td>
   <td>Investigar la capa de red</td>
   <td><p>Investigue la capa de red para ver si hay problemas de saturación y latencia.</p> <p>Para el nivel de creación, se recomienda que la latencia no supere los 100 milisegundos.</p> <p>Para obtener más información acerca de sugerencias de optimización de rendimiento, vea <a href="https://helpx.adobe.com/es/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">esta página</a>.</p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 11</strong></td>
   <td>Acercar el servidor o agregar uno por región</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 12</strong></td>
   <td>Solucionar problemas del servidor de AEM</td>
   <td>Consulte los siguientes pasos secundarios en el diagrama para obtener más información.</td>
  </tr>
  <tr>
   <td><strong>Etapa 13</strong></td>
   <td>Compruebe los requisitos de hardware</td>
   <td>Consulte la documentación sobre <a href="/help/managing/hardware-sizing-guidelines.md">Directrices de tamaño de hardware</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 14</strong></td>
   <td>Buscar causas frecuentes de problemas de rendimiento</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 15</strong></td>
   <td>Buscar solicitudes lentas</td>
   <td><p>Puede comprobar las solicitudes lentas analizando <code>request.log</code> o utilizando <code>rlog.jar</code>.</p> <p>Para obtener más información sobre el uso de rlog.jar, consulte esta página.</p> <p>Ver <a href="/help/sites-deploying/monitoring-and-maintaining.md#using-rlog-jar-to-find-requests-with-long-duration-times">Buscar solicitudes con tiempos de duración largos mediante rlog.jar</a>.<br /> </p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 16</strong></td>
   <td>Servidor de perfiles</td>
   <td><p>Para obtener información acerca de las herramientas de generación de perfiles que se pueden usar con AEM, vea <a href="/help/sites-deploying/monitoring-and-maintaining.md#tools-for-monitoring-and-analyzing-performance">Herramientas para supervisar y analizar el rendimiento</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 17</strong></td>
   <td>Buscar métodos lentos en la creación de perfiles</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 18</strong></td>
   <td>Situaciones comunes de creación de perfiles</td>
   <td>Consulte <a href="/help/sites-deploying/monitoring-and-maintaining.md#analyzing-specific-scenarios">Análisis de escenarios específicos</a> en la sección Optimización de rendimiento.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 19</strong></td>
   <td>100 % CPU</td>
   <td>Ver <a href="/help/sites-deploying/monitoring-and-maintaining.md#cpu-at">CPU al 100%</a></td>
  </tr>
  <tr>
   <td><strong>Etapa 20</strong></td>
   <td>Memoria insuficiente</td>
   <td><br />
    <ol>
     <li><a href="/help/sites-deploying/monitoring-and-maintaining.md#out-of-memory">Memoria insuficiente</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=es">Analizar problemas de memoria.</a><br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 21</strong></td>
   <td>E/S de disco</td>
   <td><p>Consulte la sección <a href="/help/sites-deploying/monitoring-and-maintaining.md#disk-i-o">E/S de disco</a> en la documentación de supervisión y mantenimiento.</p> </td>
  </tr>
  <tr>
   <td><strong>Pasos 22 y 22.1</strong></td>
   <td>Proporción de caché</td>
   <td>Ver <a href="/help/sites-deploying/configuring-performance.md#calculating-the-dispatcher-cache-ratio">Cálculo de la proporción de caché de Dispatcher</a>.<br /> <br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 23</strong></td>
   <td>Consultas lentas</td>
   <td><a href="/help/sites-deploying/best-practices-for-queries-and-indexing.md">Prácticas recomendadas para consultas e indexación</a></td>
  </tr>
  <tr>
   <td><strong>Etapa 24</strong></td>
   <td>Ajuste del repositorio</td>
   <td>
    <ul>
     <li><a href="https://helpx.adobe.com/es/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">Consejos de ajuste de rendimiento</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configuring-for-performance">Configurar para el rendimiento</a></li>
     <li><a href="https://www.slideshare.net/jukka/repository-performance-tuning">Ajuste del rendimiento del repositorio</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Etapa 25</strong></td>
   <td>Flujos de trabajo en ejecución</td>
   <td>
    <ul>
     <li><a href="/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing">Procesamiento de flujo de trabajo simultáneo</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#configure-the-queue-for-a-specific-workflow">Configurar la cola para un flujo de trabajo específico</a></li>
     <li><a href="/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances">Depuración regular de instancias de flujo de trabajo</a></li>
     <li><a href="/help/sites-developing/workflows.md#transient-workflows">Flujos de trabajo transitorios</a><br /> </li>
    </ul> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 26</strong></td>
   <td>Infraestructura de MSM</td>
   <td><p><a href="/help/sites-administering/msm-best-practices.md">Prácticas recomendadas para el administrador de varios sitios</a><br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 27</strong></td>
   <td>Ajuste de Assets</td>
   <td>
    <ol>
     <li><a href="/help/sites-deploying/configuring-performance.md#cq-dam-asset-synchronization-service">Servicio de sincronización de Assets</a></li>
     <li><a href="/help/sites-deploying/configuring-performance.md#multiple-dam-instances">Varias instancias de DAM</a></li>
     <li>Artículo de sugerencias de optimización de rendimiento <a href="https://helpx.adobe.com/es/customer-care-office-hours/aem/6x-performance-tuning-best-practices.html">aquí</a>.<br /> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 28</strong></td>
   <td>Sesiones sin cerrar</td>
   <td><p> </p> <p><a href="/help/sites-administering/troubleshoot.md#checking-for-unclosed-jcr-sessions">Comprobación de sesiones JCR sin cerrar</a></p> <p> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 30</strong></td>
   <td>¿Desea acercar Dispatcher (añada uno por "región"?)</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Etapa 31</strong></td>
   <td>Usar CDN delante de Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es#using-dispatcher-with-a-cdn">Uso de Dispatcher con una red de distribución de contenido (CDN)</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 32</strong></td>
   <td>Para descargar el servidor de AEM, utilice la administración de sesiones en el nivel de Dispatcher</td>
   <td><p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#enabling-secure-sessions-sessionmanagement">Activar sesiones seguras</a></p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 33</strong></td>
   <td>Hacer que las solicitudes sean almacenables en caché</td>
   <td>
    <ol>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=es">Configuración general de Dispatcher</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#configuring-the-dispatcher-cache-cache">Configuración de la caché de Dispatcher</a></li>
    </ol> <p>Cómo mejorar la proporción de caché; hacer que las solicitudes puedan almacenarse en caché (prácticas recomendadas de Dispatcher)</p> <p>Además, considere la siguiente configuración para optimizar las configuraciones de almacenamiento en caché<br /> </p>
    <ol>
     <li>Establezca una regla sin caché para la solicitud HTTP que no sea GET</li>
     <li>Configurar las cadenas de consulta para que no se puedan almacenar en caché</li>
     <li>No almacenar en caché las direcciones URL con extensiones faltantes</li>
     <li>Encabezados de autenticación en caché (posible desde la versión 4.1.10 de Dispatcher)</li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 34</strong></td>
   <td>Actualizar la versión de Dispatcher</td>
   <td><p>Puede descargar la versión más reciente de Dispatcher en esta ubicación:</p> <p><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=es">Seguir vínculo</a></p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 35</strong></td>
   <td>Configurar Dispatcher</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es">Configuración de Dispatcher</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 36</strong></td>
   <td>Comprobar invalidación de caché</td>
   <td><br />
    <ul>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=es#invalidating-dispatcher-cache-from-the-authoring-environment">Invalidación de caché para el nivel de Author;</a></li>
     <li><a href="https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=es#invalidating-dispatcher-cache-from-a-publishing-instance">Invalidación de caché para el nivel de publicación.</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>Pasos 37 y 38</strong></td>
   <td>Carga diferida</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=es">Ver la sesión de Gem sobre el rendimiento web de AEM.</a><br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 39</strong></td>
   <td>Utilice la preconexión para reducir la sobrecarga de conexión</td>
   <td>Consulte la sesión de Gem anterior. Además, documentación adicional previa a la conexión en W3c:<a href="https://html.spec.whatwg.org/#linkTypes"> https://html.spec.whatwg.org/#linkTypes</a></td>
  </tr>
  <tr>
   <td><strong>Pasos 40 y 41</strong><br /> </td>
   <td>Latencia y tiempo de respuesta de hosts externos</td>
   <td>Investigue la latencia y el tiempo de respuesta de los hosts externos.</td>
  </tr>
  <tr>
   <td><strong>Pasos 45<br /> y 47</strong><br /> </td>
   <td>Uso de HTTP/2</td>
   <td>Consulte la sesión de Gem para ver los pasos 37, 38 y 39.<br /> </td>
  </tr>
  <tr>
   <td><strong>Etapa 49</strong></td>
   <td>Reducir tamaño de carga útil</td>
   <td><a href="/help/sites-deploying/osgi-configuration-settings.md">Habilitar Gzip</a> y <a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=es">reducir el tamaño de la imagen</a>.<br /> </td>
  </tr>
  <tr>
   <td><strong>Pasos 42 y 43</strong></td>
   <td>Keep-Alive</td>
   <td><p>¿Está el encabezado <code>Keep-Alive</code> presente en las diferentes solicitudes para reutilizar conexiones? De lo contrario, significaría que cada solicitud conduce a otro establecimiento de conexión, lo que introduce gastos generales innecesarios. (Análisis de solicitudes HTTP estándar en el explorador)</p> <p>Puede comprobar la <a href="/help/sites-administering/proxy-jar.md">herramienta Servidor proxy</a> para buscar conexiones de conexión persistente.<br /> </p> </td>
  </tr>
  <tr>
   <td><strong>Etapa 44</strong></td>
   <td>¿Cuántas solicitudes se realizan?</td>
   <td>Realizar análisis de solicitudes HTTP estándar en el explorador.</td>
  </tr>
  <tr>
   <td><strong>Etapa 46</strong></td>
   <td>Reducción del número de solicitudes</td>
   <td>
    <ol>
     <li>Concatenar recursos (imágenes, sprites CSS, JSON)<br /> </li>
     <li>Incrustar Clientlibs:
      <ol>
       <li><a href="/help/sites-developing/clientlibs.md#creating-client-library-folders">Creando carpetas de biblioteca de cliente</a> - vea el encabezado Usar la incrustación para minimizar las solicitudes</li>
      </ol> </li>
    </ol> </td>
  </tr>
  <tr>
   <td><strong>Etapa 48</strong></td>
   <td>¿Cuál es el tamaño de la carga útil?</td>
   <td>Análisis de solicitudes HTTP estándar en el explorador</td>
  </tr>
  <tr>
   <td><strong>Pasos 50 y 51</strong></td>
   <td>Bloqueo de código JS</td>
   <td><a href="https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=es">https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2016/aem-web-performance.html?lang=es</a></td>
  </tr>
 </tbody>
</table>
