Acerca del examen de secretos
GitHub escanea repositorios para encontrar tipos conocidos de secretos para prevenir el uso fraudulento de aquellos que se confirmaron por accidente.

¿Quién puede utilizar esta característica?
Secret scanning está disponible para los tipos de repositorio siguientes:

Repositorios públicos en GitHub.com
Repositorios propiedad de la organización en GitHub Team o GitHub Enterprise Cloud con GitHub Secret Protection habilitado
Repositorios propiedad del usuario para GitHub Enterprise Cloud con Enterprise Managed Users

En este artículo
Acerca de secret scanning
Secret scanning es una característica de seguridad que le permite detectar y evitar la inclusión accidental de información confidencial, como claves de API, contraseñas, tokens y otros secretos en el repositorio. Cuando se habilita, secret scanning examina las confirmaciones en repositorios para ver los tipos conocidos de secretos y administradores del repositorio de alertas tras la detección.

Secret scanning examinará todo el historial de Git en todas las ramas presentes en el repositorio de GitHub para buscar secretos, incluso si el repositorio está archivado. GitHub también ejecutará periódicamente un examen completo de historial de Git para nuevos tipos de secretos del contenido existente en repositorios públicos donde secret scanning está habilitado cuando se agregan los nuevos tipos de secretos compatibles.

Además, secret scanning examina:

Descripciones y comentarios sobre problemas
Títulos, descripciones y comentarios, en propuestas históricas abiertas y cerradas. Se envía una notificación al asociado correspondiente cuando se detecta un patrón de asociado histórico.
Títulos, descripciones y comentarios de la solicitud de cambios
Títulos, descripciones y comentarios en GitHub Discussions
Wikis
Gists secretos. Se envía una notificación al socio relevante cuando se detecta un patrón de socio en un gist secreto.
Sugerencia

Independientemente del estado de habilitación de las características de Advanced Security, las organizaciones de GitHub Team y GitHub Enterprise pueden ejecutar un informe gratuito para examinar el código de la organización en busca de secretos filtrados.

Para generar un informe, abre En la pestaña  Security de tu organización, muestra la página  Assessments y, a continuación, haz clic en Scan your organization..

Cuando se filtra un secreto admitido, GitHub genera una alerta secret scanning. Las alertas se notifican en la pestaña Seguridad de los repositorios en GitHub, donde puede verlas, evaluarlas y resolverlas. Para más información, consulta Administración de alertas de examen de secretos.

Los proveedores de servicio pueden asociarse con GitHub para proporcionar sus formatos de secreto para el escaneo de los mismos. secret scanning se ejecuta automáticamente en patrones de asociado de todos los repositorios públicos y paquetes npm públicos. Para obtener información sobre nuestro programa de asociados, consulta Programa asociado del escaneo de secretos.

Las cadenas que coinciden con los patrones que proporcionaron los asociados del examen de secretos se notifican directamente al asociado correspondiente y no se muestran en GitHub. Para obtener más información sobre los patrones de asociados, consulte Acerca de las alertas de examen de secretos.

Para obtener más información sobre los secretos y proveedores de servicios que admite secret scanning, consulta Patrones de examen de secretos admitidos.

También puedes usar la API de REST para supervisar los resultados de secret scanning en todos los repositorios o en la organización. Para obtener más información sobre los puntos de conexión de API, consulta Puntos de conexión de la API REST para el examen de secretos.

También puedes utilizar el resumen de seguridad para tener una vista a nivel organizacional de los repositorios en los que habilitaste el secret scanning y las alertas que se encontraron. Para más información, consulta Información general sobre seguridad.

Puedes auditar las acciones realizadas en respuesta a las alertas de secret scanning mediante las herramientas de GitHub. Para más información, consulta Auditoría de alertas de seguridad.

Funcionamiento de secret scanning
A continuación, se muestra un flujo de trabajo típico que explica cómo funciona secret scanning:

        **Detección:** Secret scanning examina automáticamente el contenido del repositorio en busca de datos confidenciales, como claves de API, contraseñas, tokens y otros secretos. Busca patrones y heurística que coinciden con tipos conocidos de secretos.
        **Alertas:** cuando se detecta un posible secreto, GitHub genera una alerta y notifica a los usuarios y administradores del repositorio pertinentes. Esta notificación incluye detalles sobre el secreto detectado, como su ubicación en el repositorio. Para obtener más información sobre los tipos de alerta y los detalles, consulte [AUTOTITLE](/code-security/secret-scanning/managing-alerts-from-secret-scanning/about-alerts).
        **Revisión:** cuando se detecta un secreto, deberá revisar los detalles de la alerta proporcionados.
        **Corrección:** después, debe realizar las acciones adecuadas para corregir la exposición. Esto siempre debe incluir la rotación de la credencial afectada para asegurarse de que ya no se puede usar.  También puede incluir la eliminación del secreto del historial del repositorio (mediante herramientas como `git-filter-repo`; consulte [AUTOTITLE](/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository) para obtener más detalles), aunque esto probablemente implicará un gran coste en cuanto a tiempo y esfuerzo, y normalmente no es necesario si se han revocado las credenciales.
        **Supervisión:** se recomienda auditar y supervisar periódicamente los repositorios para asegurarse de que no se exponen otros secretos.
Acerca de las ventajas de secret scanning
        **Seguridad mejorada:** Secret scanning examina los repositorios para obtener información confidencial, como claves de API, contraseñas, tokens y otros secretos. Al detectar estas primeras fases, puede mitigar los posibles riesgos de seguridad antes de que los actores malintencionados los aprovechen.
        **Detección automatizada:** la característica examina de forma automática el código base, incluidas las confirmaciones, las propuestas y las solicitudes de cambios, lo que garantiza la protección continua sin necesidad de intervención manual. Esta automatización le permite mantener la seguridad incluso a medida que evoluciona el repositorio.
        **Alertas en tiempo real:** cuando se detecta un secreto, secret scanning proporciona alertas en tiempo real a los administradores y colaboradores del repositorio. Estos comentarios inmediatos permiten realizar acciones de corrección rápidas.
        **Compatibilidad con patrones personalizados:** las organizaciones pueden definir patrones personalizados para detectar tipos de secretos únicos o de propiedad que pueden no estar cubiertos por los patrones predeterminados. Esta flexibilidad le permite tomar medidas de seguridad específicas y adaptadas a su entorno.
        **Capacidad de detectar patrones que no son de proveedor**: puede expandir la detección para incluir patrones que no sean del proveedor, como cadenas de conexión, encabezados de autenticación y claves privadas, para el repositorio o la organización.
Personalización de secret scanning
Una vez que secret scanning esté habilitado, puede personalizarlo aún más:

Detección de patrones que no son del proveedor
Busque y detecte secretos que no sean específicos de un proveedor de servicios, como claves privadas y claves de API genéricas. Para más información, consulta Habilitación del análisis de secretos para patrones que no son de proveedor.

Realización de comprobaciones de validez
Las comprobaciones de validez te ayudan a priorizar las alertas indicando qué secretos son active o inactive. Para obtener más información, consulta Habilitación de comprobaciones de validez para el repositorio y Evaluación de alertas del análisis de secretos.

Definición de patrones personalizados
Defina sus propios patrones para los secretos que use su organización y que secret scanning pueda buscar y detectar. Para más información, consulta Definición de patrones personalizados para el examen de secretos.

Digitalización secreta de Copilot
        **Detección de secretos genéricos:** aproveche las funcionalidades de IA de secret scanning para detectar secretos no estructurados, como contraseñas, en el repositorio. Para obtener más información, consulte [AUTOTITLE](/code-security/secret-scanning/copilot-secret-scanning/responsible-ai-generic-secrets).
        **Generador de expresiones regulares:** aproveche las funcionalidades de IA de secret scanning para generar expresiones regulares que capturarán todos los patrones personalizados. Para más información, consulta [AUTOTITLE](/code-security/secret-scanning/copilot-secret-scanning/responsible-ai-regex-generator) 
Lectura adicional
        [AUTOTITLE](/code-security/secret-scanning/enabling-secret-scanning-features/enabling-secret-scanning-for-your-repository)
        [AUTOTITLE](/code-security/secret-scanning/introduction/about-push-protection)
        [AUTOTITLE](/code-security/getting-started/best-practices-for-preventing-data-leaks-in-your-organization)
        [AUTOTITLE](/code-security/getting-started/securing-your-repository)
        [AUTOTITLE](/authentication/keeping-your-account-and-data-secure)
