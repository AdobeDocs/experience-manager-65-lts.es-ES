---
title: Extracción de cadenas para traducir
description: Utilice xgettext-maven-plugin para extraer cadenas del código fuente que necesiten traducción
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 2%

---

# Extracción de cadenas para traducir{#extracting-strings-for-translating}

Utilice xgettext-maven-plugin para extraer cadenas del código fuente que necesiten traducción. El complemento Maven extrae cadenas a un archivo XLIFF que envía para su traducción. Las cadenas se extraen de las siguientes ubicaciones:

* Archivos de origen Java
* Archivos de origen de JavaScript
* Representaciones XML de recursos SVN (nodos JCR)

## Configurar la extracción de cadenas {#configuring-string-extraction}

Configure cómo la herramienta xgettext-maven-plugin extrae cadenas para su proyecto.

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| Sección | Descripción |
|---|---|
| /filter | Identifica los archivos que se analizan. |
| /parsers/vaultxml | Configura el análisis de los archivos de Vault. Identifica los nodos JCR que contienen cadenas externalizadas y sugerencias de localización. También identifica los nodos JCR que se deben ignorar. |
| /parsers/javascript | Identifica las funciones de JavaScript que externalizan cadenas. No es necesario que cambie esta sección. |
| /parsers/regexp | Configura el análisis de archivos de plantilla Java, JSP y ExtJS. No es necesario que cambie esta sección. |
| /potenciales | La fórmula para detectar cadenas que se van a internacionalizar. |

### Identificación de los archivos a analizar {#identifying-the-files-to-parse}

La sección /filter del archivo i18n.any identifica los archivos que analiza la herramienta xgettext-maven-plugin. Añada varias reglas de inclusión y exclusión que identifiquen archivos analizados y omitidos, respectivamente. Debe incluir todos los archivos y luego excluir los archivos que no desee analizar. Normalmente, se excluyen los tipos de archivo que no contribuyen a la interfaz de usuario o los archivos que definen la interfaz de usuario, pero que no se están traduciendo. Las reglas de inclusión y exclusión tienen el siguiente formato:

```
{ /include "pattern" }
{ /exclude "pattern" }
```

La parte de patrón de una regla se utiliza para hacer coincidir los nombres de los archivos que se van a incluir o excluir. El prefijo de patrón indica si coincide con un nodo JCR (su representación en Vault) o con el sistema de archivos.

| Prefijo | Efecto |
|---|---|
| / | Indica una ruta JCR. Por lo tanto, este prefijo coincide con los archivos situados debajo del directorio jcr_root. |
| &ast; | Indica un archivo normal del sistema de archivos. |
| ninguno | Ningún prefijo, o un patrón que comience con un nombre de archivo o carpeta, indica un archivo normal en el sistema de archivos. |

Cuando se utiliza dentro de un patrón, el carácter / indica un subdirectorio y el carácter &ast; coincide con todos. En la tabla siguiente se enumeran varias reglas de ejemplo.

<table>
 <tbody>
  <tr>
   <th>Regla de ejemplo</th>
   <th>Efecto</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>Incluir todos los archivos.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>Excluya todos los archivos de PDF.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>Excluir archivos POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Excluya todos los archivos debajo del nodo /content.</p> <p>Incluya el nodo /content/catalogs/geometrixx/templatepages.</p> <p>Incluya todos los nodos secundarios de /content/catalogs/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Extracción de cadenas  {#extracting-the-strings}

no hay POM:

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Con POM: Agregar esto al POM:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

el comando:

```shell
mvn xgettext:extract
```

### Archivos de salida {#output-files}

* `raw.xliff`: cadenas extraídas
* `warn.log`: advertencias (si las hay), si la API `CQ.I18n.getMessage()` se utiliza incorrectamente. Estos siempre necesitan una corrección y luego una nueva ejecución.

* `parserwarn.log`: advertencias del analizador (si las hay), por ejemplo, problemas con el analizador de js
* `potentials.xliff`: candidatos &quot;potenciales&quot; que no se extraen, pero que podrían ser cadenas legibles por humanos que necesitan traducción (se pueden ignorar, pero que aún producen una gran cantidad de falsos positivos)
* `strings.xliff`: archivo xliff aplanado, que se importará en ALF
* `backrefs.txt`: permite la búsqueda rápida de ubicaciones de código fuente para una cadena determinada
