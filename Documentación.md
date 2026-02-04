Documentación de GitHub
GitHub Actions/Procedimientos/Implementar/Configura y administra implementaciones/Administrar entornos
Administrar entornos para la implementación
Puede crear entornos y asegurarlos con las reglas de protección de implementación. Un trabajo que haga referencia a un entorno debe seguir cualquier regla de protección para el entorno antes de ejecutar o acceder a los secretos de dicho entorno.

¿Quién puede utilizar esta característica?
Repository owners

Environments, environment secrets, and deployment protection rules are available in public repositories for all current GitHub plans. They are not available on legacy plans, such as Bronze, Silver, or Gold. For access to environments, environment secrets, and deployment branches in private or internal repositories, you must use GitHub Pro, GitHub Team, or GitHub Enterprise. If you are on a GitHub Free, GitHub Pro, or GitHub Team plan, other deployment protection rules, such as a wait timer or required reviewers, are only available for public repositories.

En este artículo
Requisitos previos
Nota:

Los usuarios con planes GitHub Free solo pueden configurar entornos para repositorios públicos. Si conviertes un repositorio de público a privado, cualquier regla de protección o secretos de ambiente que hubieses configurado se ingorarán y no podrás configurar ningún ambiente. Si conviertes tu repositorio en público nuevamente, tendrás acceso a cualquier regla de protección y secreto de ambiente que hubieras configurado previamente.

Las organizaciones con datos GitHub Team y los usuarios con GitHub Pro pueden configurar entornos para repositorios privados. Para más información, consulta Planes de GitHub.

Para obtener información general sobre los entornos, consulta Desplegar con GitHub Actions.
Para obtener información sobre las reglas disponibles, consulta Implementaciones y entornos.
Creación de un entorno
Para configurar un entorno en un repositorio de cuenta personal, debes ser el propietario del repositorio. Para configurar un entorno en el repositorio de una organización, debe tener acceso admin.

Nota:

La creación de un entorno en un repositorio privado está disponible para las organizaciones con GitHub Team y usuarios con GitHub Pro.
Algunas características de los entornos no están disponibles o lo están de forma limitada para los repositorios privados. Si no puedes acceder a una característica descrita en las siguientes instrucciones, consulta la documentación correspondiente en el paso correspondiente para más información sobre disponibilidad.
En GitHub, navegue hasta la página principal del repositorio.

Debajo del nombre del repositorio, haz clic en  Settings. Si no puedes ver la pestaña "Configuración", selecciona el menú desplegable  y, a continuación, haz clic en Configuración.

Captura de pantalla de un encabezado de repositorio en el que se muestran las pestañas. La pestaña "Configuración" está resaltada con un contorno naranja oscuro.
En la barra lateral de la izquierda, haz clic en Entornos.

Haga clic en New environment (Nuevo entorno).

Escriba un nombre para el entorno y, después, haga clic en Configurar entorno. Los nombres de ambiente no distinguen entre mayúsculas y minúsculas. Un nombre de ambiente no deberá exceder los 255 caracteres y deberá ser único dentro del repositorio.

Opcionalmente, personas o equipos específicos deben aprobar los jobs de flujo de trabajo que utilicen este ambiente. Para más información, consulta Implementaciones y entornos.

Seleccione Revisores obligatorios.
Ingresa hasta 6 personas o equipos. Solo uno de los revisores requeridos necesita aprobar el job para que éste pueda proceder.
Opcionalmente, para evitar que los usuarios aprueben las ejecuciones de flujos de trabajo que han desencadenado, selecciona Prevent self-review.
Haga clic en Save protection rules.
Opcionalmente, especifica la cantidad de tiempo a esperar antes de permitir los jobs de flujo de trabajo que utilizan este ambiente para proceder. Para más información, consulta Implementaciones y entornos.

Seleccione Wait timer.
Ingresa la cantidad de minutos a esperar.
Haga clic en Save protection rules.
Opcionalmente, no permita omitir las reglas de protección configuradas. Para más información, consulta Implementaciones y entornos.

Anule la selección de la opción Allow administrators to bypass configured protection rules.
Haga clic en Save protection rules.
Opcionalmente, habilite las reglas de protección de implementación personalizadas que se hayan creado con GitHub Apps. Para más información, consulta Implementaciones y entornos.

Seleccione la regla de protección personalizada que quiere habilitar.
Haga clic en Save protection rules.
Opcionalmente, especifica qué ramas se pueden implementar en este entorno. Para más información, consulta Implementaciones y entornos.

Seleccione la opción deseada en la lista desplegable Deployment branches.

Si has elegido Selected branches and tags, para agregar una nueva regla, haz clic en Add deployment branch or tag rule.

En el menú desplegable "Ref type", haz clic en  Branch o  Tag en función de la regla que quieras aplicar.

Escribe el patrón de nombre de la rama o etiqueta que quieres permitir.

Nota:

Los patrones de nombre deben configurarse para ramas o etiquetas de forma individual.

Haga clic en Agregar regla.

Opcionalmente, agrega secretos de ambiente. Estos secretos solo están disponibles para los jobs de flujos de trabajo que utilicen el ambiente. Adicionalmente, los jobs de flujo de trabajo que utilicen este ambiente solo pueden acceder a estos secretos después de que pase cualquier regla configurada (por ejemplo, los revisores requeridos). Para más información, consulta Implementaciones y entornos.

En Environment secrets, haga clic en Add Secret.
Ingresa el nombre del secreto.
Ingresa el valor del secreto.
Haga clic en Add Secret.
Opcionalmente, agrega variables de entorno. Estas variables solo están disponibles para los trabajos de flujo de trabajo que usan el entorno y solo son accesibles mediante el contexto vars. Para más información, consulta Implementaciones y entornos.

En Variables de entorno, haz clic en Agregar variable.
Establece el nombre de la variable.
Establece el valor de la variable.
Haz clic en Agregar variable.
También puedes crear y configurar ambientes a través de la API de REST. Para más información, consulta Puntos de conexión de la API de REST para entornos de implementación, Puntos de conexión de API de REST para secretos de Acciones de GitHub, Puntos de conexión de API de REST para las variables de las Acciones de GitHub y Puntos de conexión de la API de REST para directivas de rama de implementación.

El ejecutar un flujo de trabajo que referencie un ambiente que no existe creará un ambiente con el nombre referenciado. Si el entorno se crea a partir de la ejecución de compilaciones de página implícitas (por ejemplo, desde una rama u origen de carpeta), la rama de origen se agregará como regla de protección al entorno. De lo contrario, el entorno recién creado no tendrá configurada ninguna regla de protección o secreto. Cualquiera que pueda editar flujos de trabajo en el repositorio podrá crear ambientes a través de un archivo de flujo de trabajo, pero solo los administradoresd e repositorio pueden configurar el ambiente.

Borrar un ambiente
Para configurar un entorno en un repositorio de cuenta personal, debes ser el propietario del repositorio. Para configurar un entorno en el repositorio de una organización, debe tener acceso admin.

El borrar un ambiente borrará todos los secretos y reglas de protección asociadas con éste. Cualquier job que esté actualmente en espera porque depende de las reglas de protección del ambiente que se borró, fallará automáticamente.

En GitHub, navegue hasta la página principal del repositorio.

Debajo del nombre del repositorio, haz clic en  Settings. Si no puedes ver la pestaña "Configuración", selecciona el menú desplegable  y, a continuación, haz clic en Configuración.

Captura de pantalla de un encabezado de repositorio en el que se muestran las pestañas. La pestaña "Configuración" está resaltada con un contorno naranja oscuro.
En la barra lateral de la izquierda, haz clic en Entornos.

Junto al entorno que quieras borrar, haz clic en .

Haga clic en I understand, delete this environment.

También puyedes borrar ambientes a través de la API de REST. Para más información, consulta Puntos de conexión de la API de REST para repositorios.

Cómo se relacionan los ambientes con los desplilegues
Cuando se ejecuta un trabajo de flujo de trabajo que hace referencia a un entorno, crea un objeto de implementación con la propiedad environment establecida en el nombre del entorno. A medida que avanza el flujo de trabajo, también crea objetos de estado de implementación con la propiedad environment establecida en el nombre del entorno, la propiedad environment_url establecida en la URL del entorno (si se ha especificado en el flujo de trabajo) y la propiedad state establecida en el estado del trabajo.

Puedes acceder a estos objetos a través de la API de REST o la API de GraphQL. También puedes suscribirte a estos eventos de webhook. Para obtener más información, consulta Puntos de conexión de la API de REST para repositorios, Objetos (GraphQL API) o Eventos y cargas de webhook.

Pasos siguientes
GitHub Actions proporciona varias características para administrar tus despliegues. Para más información, consulta Desplegar con GitHub Actions.
