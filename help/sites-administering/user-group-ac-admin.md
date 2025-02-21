---
title: Administración de derechos de usuario, grupo y acceso
description: Obtenga información sobre la administración de derechos de usuario, grupo y acceso en Adobe Experience Manager.
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 29391c8e3042a8a04c64165663a228bb4886afb5
workflow-type: tm+mt
source-wordcount: '3073'
ht-degree: 0%

---

# Administración de derechos de usuario, grupo y acceso{#user-group-and-access-rights-administration}

La activación del acceso a un repositorio de CRX implica varios temas:

* [Derechos de acceso](#how-access-rights-are-evaluated): los conceptos de cómo se definen y evalúan
* [Administración de usuarios](#user-administration) - administrar las cuentas individuales usadas para el acceso
* [Administración de grupos](#group-administration): simplifique la administración de usuarios formando grupos
* [Administración de derechos de acceso](#access-right-management) - definiendo directivas que controlan cómo estos usuarios y grupos pueden acceder a los recursos

Los elementos básicos son:

**Cuentas de usuario**: CRX autentica el acceso identificando y verificando a un usuario (por esa persona u otra aplicación) según los detalles que contenga la cuenta de usuario.

En CRX, cada cuenta de usuario es un nodo en el espacio de trabajo. Una cuenta de usuario de CRX tiene las siguientes propiedades:

* Representa a un usuario de CRX.
* Contiene un nombre de usuario y una contraseña.
* Aplicable para ese espacio de trabajo.
* No puede tener subusuarios. Para los derechos de acceso jerárquicos, debe utilizar grupos.

* Puede especificar derechos de acceso para la cuenta de usuario.

  Sin embargo, para simplificar la administración, Adobe recomienda que (en la mayoría de los casos) asigne derechos de acceso a las cuentas de grupo. La asignación de derechos de acceso a cada usuario individual se vuelve rápidamente difícil de administrar (las excepciones son determinados usuarios del sistema cuando solo existen una o dos instancias).

**Cuentas de grupo**: las cuentas de grupo son colecciones de usuarios u otros grupos. Se utilizan para simplificar la administración, ya que un cambio en los derechos de acceso asignados a un grupo se aplica automáticamente a todos los usuarios de ese grupo. Un usuario no tiene que pertenecer a ningún grupo, pero a menudo pertenece a varios.

En CRX, un grupo tiene las siguientes propiedades:

* Representa un grupo de usuarios con derechos de acceso comunes. Por ejemplo, autores o desarrolladores.
* Aplicable para ese espacio de trabajo.
* Puede tener miembros; pueden ser usuarios individuales u otros grupos.
* La agrupación jerárquica se puede lograr con relaciones de miembros. No puede colocar un grupo directamente debajo de otro grupo en el repositorio.
* Puede definir los derechos de acceso para todos los miembros del grupo.

**Derechos de acceso**: CRX utiliza derechos de acceso para controlar el acceso a áreas específicas del repositorio.

Esto se realiza asignando privilegios para permitir o denegar el acceso a un recurso (nodo o ruta) en el repositorio. Dado que se pueden asignar varios privilegios, estos deben evaluarse para determinar qué combinación es aplicable a la solicitud actual.

CRX permite configurar los derechos de acceso para las cuentas de usuario y de grupo. Los mismos principios básicos de evaluación se aplican a ambos.

## Cómo se evalúan los derechos de acceso {#how-access-rights-are-evaluated}

>[!NOTE]
>
>CRX implementa [control de acceso según lo definido por JSR-283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html).
>
>Una instalación estándar de un repositorio de CRX está configurada para utilizar listas de control de acceso basadas en recursos. Esta es una posible implementación del control de acceso JSR-283 y una de las implementaciones presentes con Jackrabbit.

### Sujetos y principales {#subjects-and-principals}

CRX utiliza dos conceptos clave al evaluar los derechos de acceso:

* **principal** es una entidad que cuenta con derechos de acceso. Las entidades principales incluyen:

   * Una cuenta de usuario
   * Una cuenta de grupo

     Si una cuenta de usuario pertenece a uno o más grupos, también se asocia a cada una de esas entidades de seguridad de grupo.

* Se usa un **asunto** para representar el origen de una solicitud.

  Se utiliza para consolidar los derechos de acceso aplicables a esa solicitud. Estas se toman de:

   * Principal de usuario

     Los derechos que asigna directamente a la cuenta de usuario.

   * Todas las entidades de seguridad de grupo asociadas a ese usuario

     Todos los derechos se asignan a cualquiera de los grupos a los que pertenece el usuario.

  A continuación, el resultado se utiliza para permitir o denegar el acceso al recurso solicitado.

#### Compilación de la lista de derechos de acceso para un asunto {#compiling-the-list-of-access-rights-for-a-subject}

En CRX, el asunto depende de lo siguiente:

* principal de usuario
* todas las entidades de seguridad de grupo asociadas a ese usuario

La lista de derechos de acceso aplicables al sujeto de ensayo se elabora a partir de:

* los derechos que asigna directamente a la cuenta de usuario
* además de todos los derechos asignados a cualquiera de los grupos a los que pertenece el usuario

![chlimage_1-56](assets/chlimage_1-56.png)

>[!NOTE]
>
>* CRX no tiene en cuenta ninguna jerarquía de usuarios cuando compila la lista.
>* CRX utiliza una jerarquía de grupos únicamente cuando se incluye un grupo como miembro de otro grupo. No hay herencia automática de permisos de grupo.
>* El orden en que se especifican los grupos no afecta a los derechos de acceso.
>

### Resolver solicitudes y derechos de acceso {#resolving-request-and-access-rights}

Cuando CRX administra la solicitud, compara la solicitud de acceso del asunto con la lista de control de acceso del nodo del repositorio:

Por lo tanto, si Linda solicita actualizar el nodo `/features` en la siguiente estructura de repositorio:

![chlimage_1-57](assets/chlimage_1-57.png)

### Orden de prioridad {#order-of-precedence}

Los derechos de acceso en CRX se evalúan de la siguiente manera:

* Las entidades de seguridad de usuario siempre tienen prioridad sobre las de grupo, independientemente de:

   * su orden en la lista de control de acceso
   * su posición en la jerarquía del nodo

* Para un principal determinado, existe (como máximo) una entrada denegada y 1 permitida en un nodo determinado. La implementación siempre borra las entradas redundantes y se asegura de que el mismo privilegio no aparezca en las entradas de permiso y de denegación.

>[!NOTE]
>
>Este proceso de evaluación es adecuado para el control de acceso basado en recursos de una instalación estándar de CRX.

Tomando dos ejemplos en los que el usuario `aUser` es miembro del grupo `aGroup`:

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
       + grandChildNode
```

En el caso anterior:

* `aUser` no tiene permiso de escritura para `grandChildNode`.

```xml
   + parentNode
     + acl
       + ace: aUser - deny - write
     + childNode
       + acl
         + ace: aGroup - allow - write
         + ace: aUser - deny - write
       + grandChildNode
```

En este caso:

* `aUser` no tiene permiso de escritura para `grandChildNode`.
* La segunda ACE de `aUser` es redundante.

Los derechos de acceso de varios principales de grupo se evalúan en función de su orden, tanto dentro de la jerarquía como dentro de una sola lista de control de acceso.

### Prácticas recomendadas {#best-practices}

En la tabla siguiente se enumeran algunas recomendaciones y prácticas recomendadas:

<table>
 <tbody>
  <tr>
   <td>Recomendación...</td>
   <td>Motivo...</td>
  </tr>
  <tr>
   <td><i>Usar grupos</i></td>
   <td><p>Evite asignar derechos de acceso usuario por usuario. Esto se debe a varios motivos:</p>
    <ul>
     <li>Hay muchos más usuarios que grupos, por lo que los grupos simplifican la estructura.</li>
     <li>Los grupos ayudan a proporcionar una visión general de todas las cuentas.</li>
     <li>La herencia es más sencilla con los grupos.</li>
     <li>Los usuarios van y vienen. Los grupos son a largo plazo.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><i>Sea positivo</i></td>
   <td><p>Utilice siempre las instrucciones Allow para especificar los derechos de acceso del principal del grupo (siempre que sea posible). Evite utilizar una instrucción Deny.</p> <p>Las entidades de seguridad de grupo se evalúan en orden, tanto dentro de la jerarquía como en orden dentro de una sola lista de control de acceso.</p> </td>
  </tr>
  <tr>
   <td><i>Manténgalo simple</i></td>
   <td><p>Invertir algo de tiempo y reflexión en la configuración de una nueva instalación está bien remunerado.</p> <p>La aplicación de una estructura clara simplifica el mantenimiento y la administración continuos, lo que garantiza que tanto sus compañeros actuales como los sucesores futuros puedan comprender fácilmente qué se está implementando.</p> </td>
  </tr>
  <tr>
   <td><i>Prueba</i></td>
   <td>Utilice una instalación de prueba para practicar y asegurarse de que comprende las relaciones entre los distintos usuarios y grupos.</td>
  </tr>
  <tr>
   <td><i>Usuarios/grupos predeterminados</i></td>
   <td>Actualice siempre Usuarios y grupos predeterminados inmediatamente después de la instalación para evitar problemas de seguridad.</td>
  </tr>
 </tbody>
</table>

## Administración de usuarios {#user-administration}

Se usa un cuadro de diálogo estándar para **Administración de usuarios**.

Debe haber iniciado sesión en el espacio de trabajo adecuado. A continuación, puede acceder al cuadro de diálogo desde los dos:

* el vínculo **Administración de usuarios** en la consola principal de CRX
* el menú **Seguridad** del Explorador de CRX

![chlimage_1-58](assets/chlimage_1-58.png)

**Propiedades**

* **Id. de usuario**

  El nombre abreviado de la cuenta se utiliza al acceder a CRX.

* **Nombre principal**

  Un nombre de texto completo para la cuenta.

* **Contraseña**

  Necesario al acceder a CRX con esta cuenta.

* **ntlmhash**

  Se asigna automáticamente a cada cuenta nueva y se actualiza cuando se cambia la contraseña.

* Puede agregar nuevas propiedades definiendo un nombre, tipo y valor. Haga clic en Guardar (símbolo de verificación verde) para cada nueva propiedad.

**Pertenencia a grupo**

Muestra todos los grupos a los que pertenece la cuenta. La columna Heredado indica la pertenencia que se ha heredado como resultado de la pertenencia a otro grupo.

Al hacer clic en un GroupID (cuando está disponible), se abre [Administración de grupos](#group-administration) para ese grupo.

**Suplantadores**

Con la funcionalidad Suplantar, un usuario puede trabajar en nombre de otro usuario.

Esto significa que una cuenta de usuario puede especificar otras cuentas (usuario o grupo) que pueden funcionar con su cuenta. En otras palabras, si el usuario B puede suplantar al usuario A, el usuario B puede actuar utilizando los detalles completos de la cuenta del usuario A (incluidos el ID, el nombre y los derechos de acceso).

Esto permite a las cuentas de suplantación completar tareas como si estuvieran utilizando la cuenta que están suplantando; por ejemplo, durante una ausencia o para compartir una carga excesiva a corto plazo.

Si una cuenta suplanta a otra, es difícil verla. Los archivos de registro no contienen información sobre el hecho de que se haya producido una suplantación en los eventos. Por lo tanto, si el usuario B se hace pasar por el usuario A, todos los eventos pueden parecer realizados por el usuario A personalmente.

### Creación de una cuenta de usuario {#creating-a-user-account}

1. Abra el cuadro de diálogo **Administración de usuarios**.
1. Haga clic en **Crear usuario**.
1. A continuación, puede introducir las propiedades:

   * **UserID** se usa como nombre de cuenta.
   * Se necesita **contraseña** al iniciar sesión.
   * **Nombre principal** para proporcionar un nombre de texto completo.
   * **Ruta intermedia** que se puede usar para formar una estructura de árbol.

1. Haga clic en Guardar (símbolo de marca verde).
1. El cuadro de diálogo se expande para que pueda hacer lo siguiente:

   1. Configurar **propiedades**.
   1. Consulte **Pertenencia a grupo**.
   1. Definir **suplantadores**.

>[!NOTE]
>
>A veces se puede observar una pérdida de rendimiento al registrar nuevos usuarios en instalaciones que tienen un número elevado de ambos:
>
>* usuarios
>* grupos con muchos miembros
>

### Actualización de una cuenta de usuario {#updating-a-user-account}

1. Con el cuadro de diálogo **Administración de usuarios**, abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Haga clic en la cuenta requerida para poder abrirla y editarla.
1. Realice un cambio y, a continuación, haga clic en Guardar (símbolo de marca de verificación verde) para esa entrada.
1. Haga clic en **Cerrar** para finalizar o en **Lista...** para regresar a la lista de todas las cuentas de usuario.

### Eliminación de una cuenta de usuario {#removing-a-user-account}

1. Con el cuadro de diálogo **Administración de usuarios**, abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Seleccione la cuenta requerida y haga clic en **Quitar usuario**; la cuenta se eliminará inmediatamente.

>[!NOTE]
>
>Esto elimina el nodo de esta entidad de seguridad del repositorio.
>
>Las entradas de derechos de acceso no se eliminan. Esto garantiza la integridad histórica.

### Definición de propiedades {#defining-properties}

Puede definir **Propiedades** para cuentas nuevas o existentes:

1. Abra el cuadro de diálogo **Administración de usuarios** para la cuenta correspondiente.
1. Defina un nombre de **propiedad**.
1. Seleccione **Type** en la lista desplegable.
1. Defina **Value**.
1. Haga clic en Guardar (símbolo de clic verde) para la nueva propiedad.

Las propiedades existentes se pueden eliminar con el símbolo de papelera.

Excepto por la contraseña, las propiedades no se pueden editar, se deben eliminar y volver a crear.

#### Cambio de la contraseña {#changing-the-password}

La **Contraseña** es una propiedad especial que se puede cambiar haciendo clic en el vínculo **Cambiar contraseña**.

También puede cambiar la contraseña a su propia cuenta de usuario desde el menú **Seguridad** del Explorador de CRX.

### Definición de un suplantador {#defining-an-impersonator}

Puede definir suplantadores para cuentas nuevas o existentes:

1. Abra el cuadro de diálogo **Administración de usuarios** para la cuenta correspondiente.
1. Especifique la cuenta que puede suplantar a esa cuenta.

   Puede usar Examinar... para seleccionar una cuenta existente.

1. Haga clic en Guardar (símbolo de verificación verde) para la nueva propiedad.

## Administración de grupos {#group-administration}

Se usa un cuadro de diálogo estándar para **Administración de grupos**.

Debe haber iniciado sesión en el espacio de trabajo adecuado. A continuación, puede acceder al cuadro de diálogo desde los dos:

* el vínculo **Administración de grupos** en la consola principal de CRX
* el menú **Seguridad** del Explorador de CRX

![chlimage_1-8](assets/chlimage_1-8.jpeg)

**Propiedades**

* **Id. de grupo**

  Nombre abreviado de la cuenta de grupo.

* **Nombre principal**

  Un nombre de texto completo para la cuenta de grupo.

* Puede agregar nuevas propiedades definiendo un nombre, tipo y valor. Haga clic en Guardar (símbolo de verificación verde) para cada nueva propiedad.

* **Miembros**

  Puede agregar usuarios u otros grupos como miembros de este grupo.

**Pertenencia a grupo**

Muestra todos los grupos a los que pertenece la cuenta de grupo actual. La columna Heredado indica la pertenencia que se ha heredado como resultado de la pertenencia a otro grupo.

Al hacer clic en un Id. de grupo, se abre el cuadro de diálogo correspondiente a ese grupo.

**Miembros**

Enumera todas las cuentas (usuarios o grupos) que son miembros del grupo actual.

La columna **Heredado** indica la pertenencia que se ha heredado como resultado de la pertenencia a otro grupo.

>[!NOTE]
>
>Cuando se asigna la función Propietario, Editor o Visualizador a un usuario de cualquier carpeta de recursos, se crea un nuevo grupo. El nombre del grupo tiene el formato `mac-default-<foldername>` para cada carpeta en la que se definen los roles.

### Crear una cuenta de grupo {#creating-a-group-account}

1. Abra el cuadro de diálogo **Administración de grupos**.
1. Haga clic en **Crear grupo**.
1. A continuación, puede introducir las propiedades:

   * **Nombre principal** para proporcionar un nombre de texto completo.
   * **Ruta intermedia** que se puede usar para formar una estructura de árbol.

1. Haga clic en Guardar (símbolo de marca verde).
1. El cuadro de diálogo se expande para que pueda:

   1. Configurar **propiedades**.
   1. Consulte **Pertenencia a grupo**.
   1. Administrar **Miembros**.

### Actualización de una Cuenta de Grupo {#updating-a-group-account}

1. Con el cuadro de diálogo **Administración de grupos**, abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Haga clic en la cuenta requerida para poder abrirla y editarla.
1. Realice un cambio y, a continuación, haga clic en Guardar (símbolo de marca de verificación verde) para esa entrada.
1. Haga clic en **Cerrar** para finalizar o en **Lista...** para regresar a la lista de todas las cuentas de grupo.

### Eliminación de una cuenta de grupo {#removing-a-group-account}

1. Con el cuadro de diálogo **Administración de grupos**, abra la vista de lista de todas las cuentas.
1. Desplácese por la estructura de árbol.
1. Seleccione la cuenta requerida y haga clic en **Quitar grupo**; la cuenta se eliminará inmediatamente.

>[!NOTE]
>
>Esto elimina el nodo de esta entidad de seguridad del repositorio.
>
>Las entradas de derechos de acceso no se eliminan. Esto garantiza la integridad histórica.

### Definición de propiedades {#defining-properties-1}

Puede definir Propiedades para cuentas nuevas o existentes:

1. Abra el cuadro de diálogo **Administración de grupos** para la cuenta correspondiente.
1. Defina un nombre de **propiedad**.
1. Seleccione **Type** en la lista desplegable.
1. Defina **Value**.
1. Haga clic en Guardar (símbolo de verificación verde) para la nueva propiedad.

Las propiedades existentes se pueden eliminar con el símbolo de papelera.

### Miembros {#members}

Puede agregar miembros al grupo actual:

1. Abra el cuadro de diálogo **Administración de grupos** para la cuenta correspondiente.
1. O bien, haga lo siguiente:

   * Introduzca el nombre del miembro requerido (cuenta de usuario o de grupo).
   * O use **Examinar...** para buscar y seleccionar el principal (cuenta de usuario o de grupo) que desee agregar.

1. Haga clic en Guardar (símbolo de verificación verde) para la nueva propiedad.

O elimine un miembro existente con el símbolo de papelera.

## Administración de derechos de acceso {#access-right-management}

Con la ficha **Control de acceso** de CRXDE Lite, puede definir las directivas de control de acceso y asignar los privilegios relacionados.

Por ejemplo, para **Ruta actual**, seleccione el recurso necesario en el panel izquierdo, en la ficha Control de acceso del panel inferior derecho:

![crx_accesscontrol_tab](assets/crx_accesscontrol_tab.png)

Las directivas se clasifican de acuerdo con:

* **Directivas de control de acceso aplicables**

  Estas políticas se pueden aplicar.

  Son directivas que están disponibles para crear una directiva local. Al seleccionar y agregar una directiva aplicable, esta se convierte en una directiva local.

* **Directivas de control de acceso local**

  Son directivas de control de acceso que ha aplicado. A continuación, puede actualizarlas, pedirlas o eliminarlas.

  Una directiva local anula las directivas heredadas del elemento principal.

* **Directivas efectivas de control de acceso**

  Estas son las políticas de control de acceso que ahora están en vigor para cualquier solicitud de acceso. Muestran las directivas agregadas derivadas tanto de las directivas locales como de las heredadas del elemento principal.

### Selección de directiva {#policy-selection}

Se pueden seleccionar las políticas para:

* **Ruta actual**

  Como en el ejemplo anterior, seleccione un recurso dentro del repositorio. Se muestran las políticas para esta &quot;ruta actual&quot;.

* **Repositorio**

  Selecciona el control de acceso de nivel de repositorio. Por ejemplo, al establecer el privilegio `jcr:namespaceManagement`, que solo es relevante para el repositorio, no para un nodo.

* **Principal**

  Un principal registrado en el repositorio.

  Puede escribir el nombre de **Principal** o hacer clic en el icono a la derecha del campo para abrir el cuadro de diálogo **Seleccionar principal**.

  Esto le permite **buscar** un **usuario** o **grupo**. Seleccione el principal requerido de la lista resultante y, a continuación, haga clic en **Aceptar** para volver a llevar el valor al cuadro de diálogo anterior.

![crx_accesscontrol_selectprincipal](assets/crx_accesscontrol_selectprincipal.png)

>[!NOTE]
>
>Para simplificar la administración, Adobe recomienda que asigne derechos de acceso a las cuentas de grupo, no a las cuentas de usuario individuales.
>
>Es más fácil administrar algunos grupos que varias cuentas de usuario.

### Privilegios {#privileges}

Los siguientes privilegios están disponibles para seleccionarlos al agregar una entrada de control de acceso (consulte la [API de seguridad](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/security/Privilege.html) para obtener información detallada):

<table>
 <tbody>
  <tr>
   <th><strong>Nombre de privilegio</strong></th>
   <th><strong>Lo que controla el privilegio de...</strong></th>
  </tr>
  <tr>
   <td><code>jcr:read</code></td>
   <td>Recupere un nodo y lea sus propiedades y sus valores.</td>
  </tr>
  <tr>
   <td><code>rep:write</code></td>
   <td>Se trata de un privilegio agregado específico de Jackrabbit de jcr:write y jcr:nodeTypeManagement.<br /> </td>
  </tr>
  <tr>
   <td><code>jcr:all</code></td>
   <td>Es un privilegio agregado que contiene todos los demás privilegios predefinidos.</td>
  </tr>
  <tr>
   <td><strong>Avanzado </strong></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>crx:replicate</code></td>
   <td>Realice la replicación de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:addChildNodes</code></td>
   <td>Crear nodos secundarios de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:lifecycleManagement</code></td>
   <td>Realizar operaciones del ciclo vital en un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:lockManagement</code></td>
   <td>Bloquear y desbloquear un nodo; actualizar un bloqueo.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyAccessControl</code></td>
   <td>Modificar las directivas de control de acceso de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:modifyProperties</code></td>
   <td>Crear, modificar y quitar las propiedades de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:namespaceManagement</code></td>
   <td>Registrar, cancelar el registro y modificar definiciones de área de nombres.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeDefinitionManagement</code></td>
   <td>Importe definiciones de tipo de nodo al repositorio.</td>
  </tr>
  <tr>
   <td><code>jcr:nodeTypeManagement</code></td>
   <td>Añada y elimine tipos de nodos de mezcla y cambie el tipo de nodo principal de un nodo. Esto también incluye cualquier llamada a los métodos de importación Node.addNode y XML donde el tipo mixin o principal del nuevo nodo se especifica explícitamente.</td>
  </tr>
  <tr>
   <td><code>jcr:readAccessControl</code></td>
   <td>Leer la directiva de control de acceso de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:removeChildNodes</code></td>
   <td>Quitar nodos secundarios de un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:removeNode</code></td>
   <td>Elimine un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:retentionManagement</code></td>
   <td>Realizar operaciones de administración de retención en un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:versionManagement</code></td>
   <td>Realizar operaciones de versiones en un nodo.</td>
  </tr>
  <tr>
   <td><code>jcr:workspaceManagement</code></td>
   <td>Creación y eliminación de espacios de trabajo mediante la API JCR.</td>
  </tr>
  <tr>
   <td><code>jcr:write</code></td>
   <td>Este es un privilegio agregado que contiene:<br /> - jcr:modifyProperties<br /> - jcr:addChildNodes<br /> - jcr:removeNode<br /> - jcr:removeChildNodes</td>
  </tr>
  <tr>
   <td><code>rep:privilegeManagement</code></td>
   <td>Registre un nuevo privilegio.</td>
  </tr>
 </tbody>
</table>

### Registro de nuevos privilegios {#registering-new-privileges}

También puede registrar nuevos privilegios:

1. En la barra de herramientas, seleccione **Herramientas** y, a continuación, **Privilegios** para mostrar los privilegios registrados actualmente.

   ![ac_privilegios](assets/ac_privileges.png)

1. Use el icono **Registrar privilegio** (**+**) para definir un privilegio:

   ![ac_privilegieregister](assets/ac_privilegeregister.png)

1. Haga clic en **Aceptar** para guardar. El privilegio ya está disponible para su selección.

### Agregar una entrada de control de acceso {#adding-an-access-control-entry}

1. Seleccione su recurso y abra la ficha **Control de acceso**.

1. Para agregar **Directivas de control de acceso local**, haga clic en el icono **+** a la derecha de la lista **Directiva de control de acceso aplicable**:

   ![crx_accesscontrol_apply](assets/crx_accesscontrol_applicable.png)

1. Aparece una nueva entrada en **Directivas de control de acceso local:**

   ![crx_accesscontrol_newlocal](assets/crx_accesscontrol_newlocal.png)

1. Haga clic en el icono **+** para agregar una entrada:

   ![crx_accesscontrol_addentry](assets/crx_accesscontrol_addentry.png)

   >[!NOTE]
   >
   >Actualmente, se necesita una solución para especificar una cadena vacía.
   >
   >Para esto, debe usar `""`.

1. Defina la directiva de control de acceso y haga clic en **Aceptar** para guardar. La nueva directiva es:

   * enumerados en **Directiva de control de acceso local**
   * Los cambios se reflejan en las **Directivas efectivas de control de acceso**.

CRX valida la selección; para una entidad de seguridad determinada existe (como máximo) una entrada denegada y una entrada permitida en un nodo determinado. La implementación siempre borra las entradas redundantes y se asegura de que el mismo privilegio no aparezca en las entradas de permiso y de denegación.

### Ordenación de directivas de control de acceso local {#ordering-local-access-control-policies}

El orden en la lista indica el orden en que se aplican las directivas.

1. En la tabla de **Directivas de control de acceso local**, seleccione la entrada requerida y arrástrela a la nueva posición de la tabla.

   ![crx_accesscontrol_reorder](assets/crx_accesscontrol_reorder.png)

1. Los cambios se muestran en las tablas de **Local** y **Directivas efectivas de control de acceso**.

### Eliminación de una directiva de control de acceso {#removing-an-access-control-policy}

1. En la tabla de **Directivas de control de acceso local**, haga clic en el icono rojo (-) a la derecha de la entrada.
1. La entrada se ha eliminado de las tablas de **Local** y de **Directivas efectivas de control de acceso**.

### Probar una directiva de control de acceso {#testing-an-access-control-policy}

1. En la barra de herramientas de CRXDE Lite, seleccione **Herramientas**, luego **Probar control de acceso...**.
1. Se abrirá un nuevo cuadro de diálogo en el panel superior derecho. Seleccione la **ruta** o el **principal** que desee probar.
1. Haga clic en **Prueba** para ver los resultados de su selección:

   ![crx_accesscontrol_test](assets/crx_accesscontrol_test.png)
