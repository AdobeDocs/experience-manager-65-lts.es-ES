---
title: Palabras clave en formularios adaptables
description: Estas palabras reservadas no se pueden usar como identificadores en los formularios adaptables.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 678e9dfc-2c46-430a-8da9-0329dda80090
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 100%

---

# Palabras clave en formularios adaptables {#adaptive-forms-keywords}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo formulario adaptable](/help/forms/using/create-an-adaptive-form-core-components.md) o [añadir formularios adaptables a páginas de AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Formularios adaptables con componentes de base. </span>

Las palabras clave de los formularios adaptables son identificadores reservados y predefinidos que tienen un significado especial en los formularios adaptables. Estas palabras clave no se pueden usar como identificadores en formularios adaptables. En la siguiente tabla se enumeran todas las palabras clave que son identificadores reservados en formularios adaptables.

<table>
 <tbody>
  <tr>
   <td><p>intialize</p> </td>
   <td><p>getOnOffValues</p> </td>
   <td><p>minOccur</p> </td>
  </tr>
  <tr>
   <td><p>validate</p> </td>
   <td><p>setGuideState</p> </td>
   <td><p>maxOccur</p> </td>
  </tr>
  <tr>
   <td><p>forceElementFocusChange</p> </td>
   <td><p>getGuideState</p> </td>
   <td><p>initialOccur</p> </td>
  </tr>
  <tr>
   <td><p>checkIfNull</p> </td>
   <td><p>initialize</p> </td>
   <td><p>instanceTemplateId</p> </td>
  </tr>
  <tr>
   <td><p>playJson</p> </td>
   <td><p>prepare</p> </td>
   <td><p>instanceCount</p> </td>
  </tr>
  <tr>
   <td><p>resetData</p> </td>
   <td><p>runPendingExpressions</p> </td>
   <td><p>repeatable</p> </td>
  </tr>
  <tr>
   <td><p>calcExp</p> </td>
   <td><p>queueExpressions</p> </td>
   <td><p>instances</p> </td>
  </tr>
  <tr>
   <td><p>title</p> </td>
   <td><p>resolveNode</p> </td>
   <td><p>syncXFAProps</p> </td>
  </tr>
  <tr>
   <td><p>valueCommitScript</p> </td>
   <td><p>autoSaveStart</p> </td>
   <td><p>visit</p> </td>
  </tr>
  <tr>
   <td><p>validateExp</p> </td>
   <td><p>enableAutoSave</p> </td>
   <td><p>getElement</p> </td>
  </tr>
  <tr>
   <td><p>placeholderText</p> </td>
   <td><p>autoSaveStartExpression</p> </td>
   <td><p>children</p> </td>
  </tr>
  <tr>
   <td><p>value</p> </td>
   <td><p>autoSaveInfo</p> </td>
   <td><p>setAttribute</p> </td>
  </tr>
  <tr>
   <td><p>formattedValue</p> </td>
   <td><p>xdpRef</p> </td>
   <td><p>getGuideProp</p> </td>
  </tr>
  <tr>
   <td><p>displayPictureClause</p> </td>
   <td><p>dorTemplateRef</p> </td>
   <td><p>getXFAProp</p> </td>
  </tr>
  <tr>
   <td><p>validatePictureClause</p> </td>
   <td><p>actionType</p> </td>
   <td><p>getAttribute</p> </td>
  </tr>
  <tr>
   <td><p>editPictureClause</p> </td>
   <td><p>xsdRef</p> </td>
   <td><p>name</p> </td>
  </tr>
  <tr>
   <td><p>mandatory</p> </td>
   <td><p>panel</p> </td>
   <td><p>templateId</p> </td>
  </tr>
  <tr>
   <td><p>mandatoryMessage</p> </td>
   <td><p>multiSelect</p> </td>
   <td>&gt;<p>id</p> </td>
  </tr>
  <tr>
   <td><p>validateExpMessage</p> </td>
   <td><p>optionsExp</p> </td>
   <td><p>somExpression</p> </td>
  </tr>
  <tr>
   <td><p>validatePictureClauseMessage</p> </td>
   <td><p>items</p> </td>
   <td><p>nonLocalizedTitle</p> </td>
  </tr>
  <tr>
   <td><p>validationState</p> </td>
   <td><p>multiSelection</p> </td>
   <td><p>viewVisited</p> </td>
  </tr>
  <tr>
   <td><p>width</p> </td>
   <td><p>buttonText</p> </td>
   <td><p>index</p> </td>
  </tr>
  <tr>
   <td><p>height</p> </td>
   <td><p>showComment</p> </td>
   <td><p>visible</p> </td>
  </tr>
  <tr>
   <td><p>cssClassName</p> </td>
   <td><p>fileSizeLimit</p> </td>
   <td><p>enabled</p> </td>
  </tr>
  <tr>
   <td><p>clickExp</p> </td>
   <td><p>fileList</p> </td>
   <td><p>enableLayoutOptimization</p> </td>
  </tr>
  <tr>
   <td><p>navigationChangeExp</p> </td>
   <td><p>handleEvent</p> </td>
   <td><p>dataType</p> </td>
  </tr>
  <tr>
   <td><p>type</p> </td>
   <td><p>addInstance</p> </td>
   <td><p>leadDigits</p> </td>
  </tr>
  <tr>
   <td><p>showLink</p> </td>
   <td><p>insertInstance</p> </td>
   <td><p>fracDigits</p> </td>
  </tr>
  <tr>
   <td><p>clickStatus</p> </td>
   <td><p>removeInstance</p> </td>
   <td><p>maxChars</p> </td>
  </tr>
  <tr>
   <td><p>showAsPopUp</p> </td>
   <td><p>shortDescription</p> </td>
   <td><p>execNavigationChangeExpression</p> </td>
  </tr>
  <tr>
   <td><p>multiLine</p> </td>
   <td><p>longDescription</p> </td>
   <td><p>executeExpression</p> </td>
  </tr>
  <tr>
   <td><p>visibleExp</p> </td>
   <td><p>initScript</p> </td>
   <td><p>enabledExp</p> </td>
  </tr>
  <tr>
   <td><p>execCompletion</p> </td>
   <td><p>sectionId</p> </td>
   <td><p>setFocus</p> </td>
  </tr>
  <tr>
   <td><p>completionExp</p> </td>
   <td><p>sectionTitle</p> </td>
   <td><p>activeInstance</p> </td>
  </tr>
  <tr>
   <td><p>completionExpReq</p> </td>
   <td><p>completionScript</p> </td>
   <td><p>activePart</p> </td>
  </tr>
  <tr>
   <td><p>toolbar</p> </td>
   <td><p>completionBeforeMessage</p> </td>
   <td><p>isLastPart</p> </td>
  </tr>
  <tr>
   <td><p>instanceManager</p> </td>
   <td><p>completionAfterMessage</p> </td>
   <td><p>isFirstPart</p> </td>
  </tr>
  <tr>
   <td><p>instanceIndex</p> </td>
   <td><p>completionSuccessScript</p> </td>
   <td><p>currentActivePart</p> </td>
  </tr>
  <tr>
   <td><p>summary</p> </td>
   <td><p>completionFailureScript</p> </td>
   <td><p>sectionName</p> </td>
  </tr>
  <tr>
   <td><p>submitPassword</p> </td>
   <td><p>initializeChildren</p> </td>
   <td><p>sectionFields</p> </td>
  </tr>
  <tr>
   <td><p>fetchedFromService</p> </td>
   <td><p>repeatablePanelId</p> </td>
   <td><p>getSelectedIndex</p> </td>
  </tr>
  <tr>
   <td><p>repeatablePanelPath</p> </td>
   <td><p>getItemIdentifier</p> </td>
   <td><p>mobileLayout</p> </td>
  </tr>
  <tr>
   <td><p>columnWidth</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Además de las palabras clave enumeradas anteriormente, evite utilizar nombres que sean similares a las [API de JavaScript utilizadas en los formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=es).
