---
title: Crear componentes de diseño personalizados para formularios adaptables
description: Procedimiento para crear componentes de diseño personalizados para formularios adaptables.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 100%

---

# Crear componentes de diseño personalizados para formularios adaptables{#creating-custom-layout-components-for-adaptive-forms}

## Requisitos previos {#prerequisite}

Conocimiento de los diseños, que le permite crear/utilizar un diseño personalizado. Consulte [Cambiar el diseño del panel](../../forms/using/layout-capabilities-adaptive-forms.md).

## Componente Diseño del panel de formulario adaptable {#adaptive-form-panel-layout-component}

El componente Diseño del panel de formulario adaptable controla el modo en que se presentan los componentes de los formularios adaptables en un panel en relación con la interfaz de usuario.

## Crear un diseño de panel personalizado {#creating-a-custom-panel-layout}

1. Navegue hasta la ubicación requerida `/crx/de`.
1. Copie un diseño de panel de la ubicación `/libs/fd/af/layouts/panel` (por ejemplo, `tabbedPanelLayout`) a `/apps` (por ejemplo, `/apps/af-custom-layout`).
1. Cambie el nombre del diseño que ha copiado a `customPanelLayout`. Cambie las propiedades de los nodos `qtip` y `jcr:description`. Por ejemplo, cambie a `Custom layout - Toggle tabs`.

qtip

![Diseño de paneles personalizados: captura de imagen de CRX DE](assets/custom_layout_new.png)

>[!NOTE]
>
>Configurar la propiedad `guideComponentType` al valor `fd/af/layouts/panel` determina que el diseño es un diseño de panel.

1. Cambiar el nombre del archivo `tabbedPanelLayout.jsp` en el nuevo diseño a customPanelLayout.jsp.
1. Para introducir estilos y comportamientos nuevos, cree una biblioteca de cliente en el nodo `etc`. Por ejemplo, en la ubicación /etc/af-custom-layout-clientlib, cree el nodo client-library. Permita que el nodo tenga la propiedad de categorías af.panel.custom. Tiene los siguientes archivos .css y .js:

   ```css
   /** CSS defining new styles used by custom layout **/
   
   .menu-nav {
       background-color: rgb(198, 38, 76);
       height: 30px;
    width: 30px;
    font-size: 2em;
    color: white;
       -webkit-transition: -webkit-transform 1s;  /* For Safari 3.1 to 6.0 */
    transition: transform 1s;
   }
   
   .tab-content {
    border: 1px solid #08b1cf;
   }
   
   .custom-navigation {
       -webkit-transition: width 1s, height 1s, -webkit-transform 1s;  /* For Safari 3.1 to 6.0 */
    transition: width 1s, height 1s, transform 1s;
   }
   
   .panel-name {
       padding-left: 30px;
       font-size: 20px;
   }
   
   @media (min-width: 992px) {
    .nav-close {
     width: 0px;
       }
   }
   
   @media (min-width: 768px) and (max-width: 991px) {
    .nav-close {
     height: 0px;
       }
   }
   
   @media (max-width: 767px) {
    .menu-nav, .custom-navigation {
        display: none;
       }
   }
   ```

   ```javascript
   /** function for toggling the navigators **/
   var toggleNav = function () {
   
       var nav = $('.custom-navigation');
       if (nav) {
           nav.toggleClass('nav-close');
       }
   }
   
   /** function to populate the panel title **/
   $(window).on('load', function() {
       if (window.guideBridge) {
           window.guideBridge.on("elementNavigationChanged",
           function (evntName, evnt) {
                       var activePanelSom = evnt.newText,
                           activePanel = window.guideBridge._guideView.getView(activePanelSom);
                       $('.panel-name').html(activePanel.$itemNav.find('a').html());
                   }
           );
       }
   });
   ```

1. Para mejorar el aspecto y el comportamiento, puede incluir un `client library`.

   Además, actualice las rutas de los scripts incluidos en los archivos .jsp. Por ejemplo, actualice el archivo `customPanelLayout.jsp` como se indica a continuación:

   ```html
   <%-- jsp encapsulating navigator container and panel container divs --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   <cq:includeClientLib categories="af.panel.custom"/>
   <div>
       <div class="row">
           <div class="col-md-2 col-sm-2 hidden-xs menu-nav glyphicon glyphicon-align-justify" onclick="toggleNav();"></div>
           <div class="col-md-10 col-sm-10 hidden-xs panel-name"></div>
       </div>
       <div class="row">
           <div class="col-md-2 hidden-xs guide-tab-stamp-list custom-navigation">
               <cq:include script = "/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp" />
           </div>
           <div  class="col-md-10">
               <c:if test="${fn:length(guidePanel.description) > 0}">
                   <div class="<%=GuideConstants.GUIDE_PANEL_DESCRIPTION%>">
                       ${guide:encodeForHtml(guidePanel.description,xssAPI)}
                           <cq:include script="/libs/fd/af/components/panel/longDescription.jsp"/>
                   </div>
               </c:if>
               <cq:include script = "/apps/af-custom-layout/customPanelLayout/panelContainer.jsp"/>
           </div>
       </div>
   </div>
   ```

   El archivo `/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp`:

   ```html
   <%-- jsp governing the navigation part --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   <%@ page import="com.adobe.aemds.guide.utils.StyleUtils" %>
   <%-- navigation tabs --%>
   <ul id="${guidePanel.id}_guide-item-nav-container" class="tab-navigators tab-navigators-vertical in"
       data-guide-panel-edit="reorderItems" role="tablist">
       <c:forEach items="${guidePanel.items}" var="panelItem">
           <c:set var="isNestedLayout" value="${guide:hasNestablePanelLayout(guidePanel,panelItem)}"/>
           <li id="${panelItem.id}_guide-item-nav" title="${guide:encodeForHtmlAttr(panelItem.navTitle,xssAPI)}" data-path="${panelItem.path}" role="tab" aria-controls="${panelItem.id}_guide-item">
               <c:set var="panelItemCss" value="${panelItem.cssClassName}"/>
               <% String panelItemCss = (String) pageContext.getAttribute("panelItemCss");%>
               <a data-guide-toggle="tab" class="<%= StyleUtils.addPostfixToClasses(panelItemCss, "_nav") %> guideNavIcon nested_${isNestedLayout}">${guide:encodeForHtml(panelItem.navTitle,xssAPI)}</a>
               <c:if test="${isNestedLayout}">
                   <guide:initializeBean name="guidePanel" className="com.adobe.aemds.guide.common.GuidePanel"
                       resourcePath="${panelItem.path}" restoreOnExit="true">
                       <sling:include path="${panelItem.path}"
                                      resourceType="/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp"/>
                   </guide:initializeBean>
               </c:if>
               <em></em>
           </li>
       </c:forEach>
   </ul>
   ```

   El `/apps/af-custom-layout/customPanelLayout/panelContainer.jsp` actualizado:

   ```html
   <%-- jsp governing the panel content --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   
   <div id="${guidePanel.id}_guide-item-container" class="tab-content">
       <c:if test="${guidePanel.hasToolbar && (guidePanel.toolbarPosition == 'Top') }">
           <sling:include path="${guidePanel.toolbar.path}"/>
       </c:if>
   
   <c:forEach items="${guidePanel.items}" var="panelItem">
       <div class="tab-pane" id="${panelItem.id}_guide-item" role="tabpanel">
           <c:set var="isNestedLayout" value="${guide:hasNestablePanelLayout(guidePanel,panelItem)}"/>
           <c:if test="${isNestedLayout}">
               <c:set var="guidePanelResourceType" value="/apps/af-custom-layout/customPanelLayout/panelContainer.jsp" scope="request"/>
           </c:if>
           <sling:include path="${panelItem.path}" resourceType="${panelItem.resourceType}"/>
       </div>
   </c:forEach>
   <c:if test="${guidePanel.hasToolbar && (guidePanel.toolbarPosition == 'Bottom')}">
       <sling:include path="${guidePanel.toolbar.path}"/>
   </c:if>
   </div>
   ```

1. Abra un formulario adaptable en modo de autor. El diseño del panel que haya definido se agregará a la lista para configurar los diseños del panel.

   ![El diseño del panel personalizado aparece en la lista de diseño del panel](assets/auth-layt.png) ![Captura de pantalla de un formulario adaptable, con diseño de panel personalizado](assets/s1.png) ![Captura de pantalla que muestra la funcionalidad de alternar del diseño personalizado](assets/s2.png)

Ejemplo de ZIP para un diseño de panel personalizado y un formulario adaptable que lo utilice.

[Obtener archivo](assets/af-custom-layout.zip)
