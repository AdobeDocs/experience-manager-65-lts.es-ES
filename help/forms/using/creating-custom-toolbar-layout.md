---
title: Crear un diseño de barra de herramientas personalizado
description: Puede especificar un diseño de la barra de herramientas para el formulario. El diseño de la barra de herramientas define los comandos y el diseño de la barra de herramientas del formulario.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: "Experience Manager, Experience Manager Forms"
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 92%

---

# Crear un diseño de barra de herramientas personalizado{#creating-custom-toolbar-layout}

## Diseños de barra de herramientas {#layout}

Cuando se crea un formulario adaptable, se puede especificar un diseño de la barra de herramientas para el formulario. El diseño de la barra de herramientas define los comandos y el diseño de la barra de herramientas del formulario.

El diseño de la barra de herramientas se basa en gran medida en el procesamiento del lado del cliente impulsado por código complejo CSS y JavaScript. Organizar y optimizar el servicio de este código puede ser un problema complicado. Para ayudar a resolver este problema, AEM proporciona carpetas de biblioteca del lado del cliente, que le permiten almacenar el código del lado del cliente en el repositorio, organizarlo en categorías y definir cuándo y cómo se debe servir cada categoría de código al cliente. A continuación, el sistema de biblioteca del lado del cliente se encarga de producir los vínculos correctos en la página web final para cargar el código correcto. Para obtener información detallada, consulte [Cómo funcionan las bibliotecas del lado del cliente en AEM.](/help/sites-developing/clientlibs.md)

![Diseño de muestra de la barra de herramientas](assets/default_toolbar_layout.png)

Diseño de muestra de la barra de herramientas

Los formularios adaptables proporcionan un conjunto de diseños integrados:

![Diseños de la barra de herramientas disponibles para usar ](assets/toolbar1.png)

Diseños de la barra de herramientas disponibles para usar

Además, puede crear un diseño personalizado de la barra de herramientas.

El siguiente procedimiento detalla los pasos para crear una barra de herramientas personalizada que muestre tres acciones en la barra y las demás acciones en una lista desplegable.

El paquete de contenido adjunto contiene todo el código que se describe a continuación. Después de instalar el paquete de contenido, abra `/content/forms/af/CustomLayoutDemo.html` para ver la demostración del diseño de la barra de herramientas personalizada.

CustomToolbarLayoutDemo.zip

[Obtener archivo](assets/customtoolbarlayoutdemo.zip)
Diseño personalizado de la barra de herramientas 

## Crear un diseño personalizado de la barra de herramientas {#layout-1}

1. Cree una carpeta para guardar los diseños personalizados. Por ejemplo:

   `/apps/customlayout/toolbar`.

   Para crear un diseño personalizado, puede utilizar (y personalizar) uno de los diseños de la barra de herramientas predeterminados disponibles en la siguiente carpeta:

   `/libs/fd/af/layouts/toolbar`

   Por ejemplo, copie el nodo `mobileFixedToolbarLayout` desde la carpeta `/libs/fd/af/layouts/toolbar` a la carpeta `/apps/customlayout/toolbar`.

   Además, copie toolbarCommon.jsp en la carpeta `/apps/customlayout/toolbar`.

   >[!NOTE]
   >
   >La carpeta que cree para mantener los diseños personalizados se puede crear con la carpeta `apps`.

1. Cambie el nombre del nodo copiado. `mobileFixedToolbarLayout`, a `customToolbarLayout.`

   Además, proporcione una descripción relevante para el nodo. Por ejemplo, cambie jcr:description del nodo a **Diseño personalizado para la barra de herramientas**.

   La propiedad `guideComponentType` del nodo determina el tipo de diseño. En este caso, el tipo de diseño es la barra de herramientas, por lo que aparece en la lista desplegable de selección de diseño de la barra de herramientas.

   ![Un nodo con una descripción relevante](assets/toolbar3.png)

   Un nodo con una descripción relevante

   El nuevo diseño personalizado de la barra de herramientas se muestra en la configuración del cuadro de diálogo **Barra de herramientas de formulario adaptable**.

   ![Lista de diseños de barra de herramientas disponibles](assets/toolbar4.png)

   Lista de diseños de barra de herramientas disponibles

   >[!NOTE]
   >
   >La descripción actualizada en el paso anterior se muestra en la lista desplegable Diseño.

1. Seleccione este diseño personalizado de la barra de herramientas y haga clic en Aceptar.

   Agregue clientlib (javascript y css) en el nodo `/etc/customlayout` e incluya la referencia de clientlib en la `customToolbarLayout.jsp`.

   ![Ruta del archivo customToolbarLayout.css](assets/toolbar_3.png)

   Ruta del archivo customToolbarLayout.css

   Muestra `customToolbarLayout.jsp`:

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >Agregue la clase de guía para el diseño. El estilo predeterminado de la barra de herramientas se define con respecto a la clase de guía.

   Muestra `toolBarCommon.jsp`:

   ```jsp
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></code></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></code></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>
   </c:forEach>
   ```

   CSS presente dentro del nodo clientlib:

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;
   }
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;
   }
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;
   }
   
   .mobilecustomToolbar .btn-group {
    vertical-align: super;
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       }
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {
     vertical-align: top;
    }
   
   }
   ```

>[!NOTE]
>
>La descripción actualizada en el paso anterior se muestra en la lista desplegable Diseño.

![Vista de escritorio del diseño personalizado de la barra de herramientas ](assets/toolbar_1.png)

Vista de escritorio del diseño personalizado de la barra de herramientas
