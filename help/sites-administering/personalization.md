---
title: Personalización
description: Obtenga información acerca de la personalización en Adobe Experience Manager para proporcionar al usuario un entorno personalizado que muestre contenido dinámico.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
exl-id: 558cf29b-34f4-4ead-b8d6-67ef8aaa5dc5
source-git-commit: abda4a719676f45388e91bbdec1421152433fce8
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 2%

---

# Personalización {#personalization}

## ¿Qué es Personalization? {#what-is-personalization}

Hoy en día, hay un volumen de contenido cada vez mayor disponible, ya sea en sitios web de Internet, extranet o intranet.

Personalization se centra en proporcionar al usuario un entorno personalizado que muestre el contenido dinámico seleccionado según sus necesidades específicas; esto puede realizarse en función de perfiles predefinidos, selección de usuarios o comportamiento interactivo del usuario.

La personalización consta de tres elementos principales:

### Usuarios {#users}

* Tienen perfiles, tanto individuales como grupales. Estos perfiles contienen características (como la descripción del trabajo, la ubicación, los intereses) que se pueden utilizar para personalizar el contenido que pueden ver.
* Realice acciones. A continuación, se pueden analizar y comparar con las reglas de comportamiento para adaptar el contenido que ven.

### Contenido {#content}

* Es lo que el usuario quiere ver. Preferiblemente contenido de interés, y uso, a ellos para el cumplimiento de sus tareas.
* Pueden clasificarse y, por lo tanto, ponerse a disposición de los usuarios según reglas predefinidas.
* Debe ser dinámico.

En otras palabras, el contenido debe, de alguna manera, depender del usuario. Si todos los usuarios ven el mismo contenido, la personalización es redundante.

### Reglas {#rules}

* Defina cómo se produce realmente la personalización: qué contenido puede ver el usuario y cuándo.

Personalization puede ser:

#### Explícito {#explicit}

* Personalización: el usuario realiza selecciones entre una selección de fuentes de contenido.

#### Implícito {#implicit}

* Basado en reglas: los administradores empresariales definen reglas específicas para las acciones en función de perfiles o comportamientos específicos.
* Filtrado simple: las selecciones se realizan sobre la base de perfiles predefinidos a nivel de usuario o grupo.
* Filtrado colaborativo/de recomendaciones: el comportamiento del usuario se registra de acuerdo con reglas predefinidas. Estas reglas se basan en el comportamiento observado con individuos de ideas similares. La información recopilada se utiliza para adaptar la información mostrada al usuario, especialmente en forma de recomendaciones.

## ¿Cómo y cuándo se puede utilizar Personalization? {#how-and-when-can-personalization-be-used}

Personalization se puede utilizar en muchos casos, por ejemplo:

### Páginas de intranet {#intranet-pages}

* El contenido se puede ofrecer en función de la ubicación, el departamento o la función de un usuario, ya definidos dentro de una red interna.
* Según la opción disponible, el usuario puede realizar más selecciones.

### Grupos de usuarios de destino específicos, limitados: redes externas {#extranets}

* Los usuarios requieren un inicio de sesión para la autorización; esto se vincula a un perfil que proporciona la información necesaria para la personalización; posiblemente detalles como su ubicación, relación con el producto, historial de uso, responsabilidades presupuestarias, etc.
* Estas instancias pueden variar entre sitios como:
* Empresas que proporcionan sitios web a una sección altamente especializada de su mercado, por ejemplo, una empresa farmacéutica que proporciona un sitio web especializado para los médicos.
* Compañías que proporcionan sitios web que permiten a sus clientes ver la información actual de cuenta y facturación; por ejemplo, proveedores de telefonía.

### Sitio web de ventas y distribución {#sales-site}

* Los sitios web de ventas y distribución, como Amazon, pueden combinar un perfil de usuario, el historial de ventas del usuario y el historial de navegación para hacer sugerencias sobre lo que podría interesar al usuario a continuación.

### Buscar sitios web {#search-site}

* Muchos de los principales sitios web de motores de búsqueda tienen herramientas analíticas muy poderosas que registran el comportamiento de los usuarios, los términos de búsqueda que utilizan y los sitios web que realmente visitan. A continuación, se utiliza para personalizar el contenido proporcionado, especialmente en lo que respecta a la visualización de anuncios.

### Puntos fuertes de Personalization y puntos a considerar {#strengths-of-personalization-and-points-to-consider}

Las siguientes son las razones por las que se debe utilizar la personalización:

* Un usuario puede experimentar un sitio web cómodo y centrado.
* Personalization se puede utilizar para propagar automáticamente el acceso a la última versión del contenido.
* Las funciones de colaboración social están disponibles para que los usuarios se comuniquen entre sí, ya que se pueden identificar mediante sus perfiles.
* Se puede proporcionar al usuario el contenido necesario para realizar una tarea determinada. Dentro de la intranet de una empresa, esto puede proporcionar una herramienta inestimable para la difusión de información.
* Se puede proporcionar al usuario el contenido que necesita/desea, lo que reduce el tiempo que necesita para realizar operaciones de búsqueda.
* El proveedor de contenido puede dirigir el contenido para que lo vean categorías específicas de usuarios.
* Se pueden definir reglas para entregar contenido en función de combinaciones de características de usuario y comportamiento. Esto proporciona un mecanismo sofisticado para personalizar su experiencia web.

Al utilizar la personalización, tenga en cuenta lo siguiente:

#### Rendimiento {#performance}

* Naturalmente, el análisis y la evaluación adicionales tienen un impacto en el rendimiento. Sin embargo, los métodos utilizados son muy sofisticados y pueden optimizarse para minimizar el impacto.

#### Autorización {#authorization}

* Personalization requiere un mecanismo de inicio de sesión, ya que el sitio web debe poder identificar al usuario.

#### Almacenamiento en caché {#caching}

* El almacenamiento en caché es un aspecto que el usuario verá en términos de rendimiento y precisión: la rapidez con la que el sitio web ofrece contenido personalizado y siempre está actualizado.
* El almacenamiento en caché es una consideración clave al configurar la personalización y se debe tardar en utilizar la implementación correcta.

>[!TIP]
>
>El efecto de Personalization en el rendimiento y los temas relacionados con el almacenamiento en caché se tratan con más detalle en el documento [Optimización del rendimiento.](/help/sites-deploying/configuring-performance.md)

#### Precisión de las reglas {#accuracy}

* La Personalization que se obtiene realizando un seguimiento del comportamiento del usuario o estableciendo reglas basadas en el perfil del usuario debe ser precisa y lógica.
* No hay nada más frustrante para el usuario que tener contenido forzado o denegado debido a la lógica inexacta de una regla.
* Por lo tanto, las reglas deben estar bien pensadas, con los requisitos del usuario en primer plano. Esto puede requerir mucho esfuerzo y no se debe subestimar; definir las reglas empresariales a menudo supera el esfuerzo técnico al implementar la personalización.

#### Cuándo usarlas {#when-to-use}

* Al igual que muchas funciones de la web, la personalización debe utilizarse con cuidado. ¿Beneficiará realmente al usuario su uso? Siempre debe ser la primera consideración, o si el objetivo deseado se puede lograr con menos esfuerzo por otro método. Personalization puede correr el riesgo de ser una función que los usuarios configuran una vez (para ver cómo funciona) y solo una vez, ya que no les aporta ventajas reales.
* Personalization solo es significativo cuando el contenido es dinámico: depende del usuario de alguna manera. Si todos los usuarios ven el mismo contenido, la personalización es redundante.

#### Confidencialidad {#confidentiality}

* Muchos usuarios están preocupados por la protección de datos y la seguridad. En particular, los datos recuperados al rastrear su comportamiento al navegar por la web.

## Personalization y Access {#personalization-and-access}

Personalization debe considerarse por separado del control de acceso, pero no se interrelacionan.

Personalization no crea ninguna forma de control de acceso. Es simplemente un método para controlar lo que el usuario ve; no restringe el acceso del usuario a otro contenido y, como con cualquier contenido, necesita tener asignados los controles de acceso correctos.

Sin embargo, el control de acceso se puede utilizar para crear una forma de personalización. Si permite o deniega a un usuario el acceso al contenido, esto inevitablemente afecta a la elección del contenido que tiene disponible, personalizando así su experiencia web.

## Componentes disponibles para Personalization {#components-available-for-personalization}

Con AEM se proporcionan varios componentes para la personalización. Algunos permiten a los usuarios iniciar sesión y editar sus perfiles, mientras que otros (como Mis gadgets) permiten a los usuarios configurar una página específica:

| Título en Sidekick | Función |
|---|---|
| Campo de contraseña activado | Solicita la contraseña y la confirmación de la misma. |
| Registro de inicio de sesión combinado | Permite al usuario iniciar sesión en una cuenta existente o registrarse para obtener una nueva cuenta. |
| Campo de dirección de Forms | Campo complejo que permite la entrada de una dirección internacional. |
| Forms Begin | Inicia una definición de formulario |
| Captcha de Forms | Campo formado por una palabra alfanumérica que se actualiza automáticamente. El componente captcha protege los sitios web contra los bots. |
| Grupo de casillas de verificación Forms | Varios elementos organizados en una lista y precedidos de casillas de verificación. Los usuarios pueden seleccionar varias casillas de verificación. |
| Lista desplegable de Forms | Varios elementos organizados en una lista desplegable. El modificador Selección múltiple especifica si se pueden seleccionar varios elementos de la lista. |
| Fin de Forms | Termina la definición del formulario. |
| Carga de archivo de Forms | Elemento de carga que permite al usuario cargar un archivo en el servidor. |
| Campo oculto de Forms | Este campo no se muestra al usuario. Se puede utilizar para transportar un valor al cliente y de vuelta al servidor. Este campo no debe tener restricciones. |
| Botón de imagen de Forms | Botón de envío adicional para el formulario que se procesa como imagen. |
| Campo de contraseña de Forms | Es igual que el campo de texto, pero solo se permite una línea y la entrada de texto del usuario no es visible en el campo. |
| Grupo de radio de Forms | Varios elementos organizados en una lista precedida por un botón de opción. Los usuarios solo deben seleccionar un botón de opción. |
| Botón Enviar de Forms | Botón de envío adicional para el formulario en el que el título se muestra como texto en el botón. |
| Campo de texto de Forms | Campo de texto que permite a los usuarios introducir información. |
| My Gadgets | Permite incluir uno de una selección de gadgets disponibles. |
| Fotografía de avatar de perfil | Permite la entrada de una fotografía de avatar. |
| Nombre detallado de perfil | Entrada de detalles del nombre, incluidos elementos como título, segundo nombre y sufijo si es necesario. |
| Nombre para mostrar en el perfil | Nombre para mostrar. |
| Correo electrónico del perfil | Introducción de una dirección de correo electrónico. |
| Género de perfil | Permite la entrada del sexo. |
| Número de teléfono principal del perfil | Permite introducir un número de teléfono. |
| URL principal del perfil | Permite introducir una dirección URL. |
| Propiedad Texto general de perfil | Propiedades del perfil. |
| Inicio de sesión | Permite enviar un nombre de usuario y una contraseña al iniciar sesión. |
| Cerrar sesión | Indica el usuario que ha iniciado sesión actualmente y le proporciona un vínculo para cerrar la sesión. |
| Nube de etiquetas | Una nube de etiquetas para mostrar una selección de etiquetas presentada gráficamente dentro del sitio web |
| Teaser | Un fragmento de contenido (normalmente una imagen) que se muestra en una página principal para &quot;provocar&quot; a los usuarios el acceso al contenido subyacente. |
