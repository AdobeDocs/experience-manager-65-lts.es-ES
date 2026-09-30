---
title: No se puede iniciar el controlador de dominio JBoss
description: En implementaciones de clúster LTS de AEM Forms 6.5.1 mediante JBoss EAP 8, el archivo de configuración puede contener una etiqueta duplicada.
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: f24e7245-7b43-4b1c-ba7a-162344ef545c
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%
---
# No se puede iniciar el controlador de dominio JBoss

## Problema

En **AEM Forms 6.5.1 LTS** implementaciones de clúster usando **JBoss EAP 8**, el archivo de configuración
`<JBOSS_HOME>/domain/configuration/domain_oracle.xml` (y las variantes específicas de la base de datos) pueden contener **una etiqueta `<security>` de apertura** duplicada.

Esto causa una **configuración XML no válida**, lo que da como resultado **error al iniciar el controlador de dominio JBoss** e impide que la inicialización del clúster se realice correctamente.

## Aplicable a

* **Producto:** AEM Forms 6.5.1 LTS
* **Tipo de implementación:** clúster
* **Servidor de aplicaciones:** JBoss EAP 8.x
* **Archivos de configuración:**

  * `<JBOSS_HOME>/domain/configuration/domain_oracle.xml`
  * `<JBOSS_HOME>/domain/configuration/domain_mysql.xml`
  * `<JBOSS_HOME>/domain/configuration/domain_mssql.xml`

## Pasos para solucionar problemas

1. Durante el inicio del controlador de dominio, pueden observarse los siguientes errores:

   * `WFLYCTL0198: Unexpected element 'security'`
   * `IJ010061: Unexpected element: security`

2. Abra el archivo de configuración correspondiente:

   ```
   <JBOSS_HOME>/domain/configuration/domain_oracle.xml
   (or domain_mysql.xml / domain_mssql.xml)
   ```

3. Busque la etiqueta de apertura `<security>` duplicada.

   **Configuración incorrecta:**

   ```xml
   <security>
       <security>
           <user-name>adobe</user-name>
           <credential-reference store="db-creds" alias="EncryptDBPassword"/>
       </security>
   ```

4. Quite la etiqueta de apertura extra `<security>` para corregir la configuración como se muestra a continuación:

   **Configuración correcta:**

   ```xml
   <security>
       <user-name>adobe</user-name>
       <credential-reference store="db-creds" alias="EncryptDBPassword"/>
   </security>
   ```

5. Guarde el archivo e inicie el controlador de dominio JBoss.

6. Asegúrese de que la misma configuración validada se aplica de forma coherente en todos los nodos del clúster.
