---
title: Espacios de nombres personalizados
description: Obtenga información sobre cómo definir e implementar áreas de nombres personalizadas en AEM 6.5 LTS.
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 475a77e8e4ff0ecd19a939fd3b3c9294adf24997
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 8%

---


# Espacios de nombres personalizados{#custom-namespaces}

Obtenga información sobre cómo definir e implementar [áreas de nombres](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/4.5_Namespaces.html?lang=es) personalizadas en AEM 6.5 LTS.

Las áreas de nombres personalizadas son la parte opcional de una propiedad JCR que precede a `:`. AEM utiliza varias áreas de nombres como:

+ `jcr` para propiedades del sistema JCR
+ `cq` para propiedades de AEM (anteriormente conocidas como Adobe CQ)
+ `dam` para propiedades de AEM específicas de recursos DAM
+ `dc` para propiedades principales de Dublín

... y muchos otros.

Las áreas de nombres se pueden utilizar para denotar el ámbito y la intención de una propiedad. La creación de un área de nombres personalizada, a menudo el nombre de su empresa, ayuda a identificar claramente los nodos o las propiedades específicas de su implementación de AEM y contienen datos específicos de su empresa.

Las áreas de nombres personalizadas se administran en [scripts de inicialización de repositorio de Sling (repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html) e implementan como configuraciones OSGi en el paquete de configuración del proyecto (por ejemplo, `ui.config`).

## Recursos {#resources}

+ [Documentación de inicialización del repositorio de Sling (repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)

## Código {#code}

El siguiente código se usa para configurar un área de nombres `wknd`.

### Configuración OSGi de RepositoryInitializer

`/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~wknd-examples-namespaces.cfg.json`

```json
{
    "scripts": [
        "register namespace (wknd) https://site.wknd/1.0"
    ]
}
```

Esto permite utilizar en AEM las propiedades personalizadas que usan el espacio de nombres `wknd`, como indica el primer parámetro después de la instrucción `register namespace`. Para obtener definiciones de scripts más avanzadas, consulte los ejemplos de la [documentación de inicialización del repositorio de Sling (repoinit)](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios).
