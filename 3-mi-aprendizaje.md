Antes de realizar esta práctica, mis conocimientos sobre la configuración de herramientas de análisis de código como SonarQube, así como la integración de bases de datos con PostgreSQL en un entorno Docker, eran limitados. Tenía nociones básicas de Docker y de la creación de contenedores, pero no había configurado servicios complejos con dependencias entre ellos ni realizado un healthcheck para monitorear su estado.

Después de realizar la práctica, mis principales aprendizajes fueron:

Integración de servicios en Docker Compose: Aprendí a definir múltiples servicios con dependencias, asignando redes de tipo bridge para que los contenedores se comuniquen de manera segura y eficiente.

Configuración de SonarQube con PostgreSQL: Comprendí cómo establecer las variables de entorno necesarias para que SonarQube se conecte correctamente a su base de datos, así como la importancia de mantener datos persistentes mediante volúmenes.

Healthchecks: Descubrí cómo implementar y configurar healthchecks para asegurar que los servicios estén operativos antes de depender de ellos, lo cual es crucial en entornos de producción.

Gestión de volúmenes y persistencia de datos: Aprendí a separar los datos de configuración, extensiones y la base de datos, garantizando que la información no se pierda al reiniciar los contenedores.

Durante la práctica, surgió un problema al intentar levantar SonarQube: el contenedor no se conectaba a PostgreSQL inicialmente debido a un error en la URL de conexión y credenciales incorrectas. Solucioné este inconveniente verificando los logs del contenedor y corrigiendo las variables de entorno, asegurando que la conexión fuera estable y que SonarQube pudiera iniciar correctamente.

En conclusión, esta práctica fortaleció mi formación profesional al combinar conocimientos de devops, bases de datos, y herramientas de análisis de código, preparándome para enfrentar entornos reales de desarrollo y despliegue de aplicaciones.
