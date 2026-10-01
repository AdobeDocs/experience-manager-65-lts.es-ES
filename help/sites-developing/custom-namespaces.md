---
title: Espacios de nombres personalizados
description: Obtenga información sobre cómo definir e implementar áreas de nombres personalizadas en AEM 6.5 LTS.
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
subfeature_v2:
  - id: cd14456d-a492-4b5c-8a82-1fbd4460dbd2
    internal-label: Java Content Repository
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d1f055e0688c24b55f80c7e2be974fe1d28ae8d5
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 3%
---

# Espacios de nombres personalizados{#custom-namespaces}

Obtenga información sobre cómo definir e implementar [áreas de nombres](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/jcr/1.0/4.5_Namespaces.html) personalizadas en AEM 6.5 LTS.

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
