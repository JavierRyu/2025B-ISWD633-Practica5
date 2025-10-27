# Ejercicio
Configurar SonarQube utilizando Docker Compose, para esto necesitas dos servicios:
- Servicio: SonarQube
- Desde el host es necesario acceder a SonarQube por lo que necesitas mapear el puerto correspondiente.
- Servicio: PostgreSQL (existen otras opciones: Microsoft SQL Server, Oracle)
- Coloca un healtcheck para cada uno de los servicios.
- Los dos servicios deben pertenecer a una red de tipo bridge
- Investiga cuáles son los volúmenes necesarios para cada servicio
- Investiga cuáles son las variables de entorno para que los servicios funcionen de manera adecuada.
docker-compose.yml para SonarQube + PostgreSQL
version: '3.9'

services:
  sonarqube:
    image: sonarqube:latest
    container_name: sonarqube
    depends_on:
      - db
    ports:
      - "9000:9000" # Acceso desde el host a SonarQube
    environment:
      SONAR_JDBC_URL: jdbc:postgresql://db:5432/sonarqube
      SONAR_JDBC_USERNAME: sonar
      SONAR_JDBC_PASSWORD: sonarpass
    volumes:
      - sonarqube_data:/opt/sonarqube/data
      - sonarqube_extensions:/opt/sonarqube/extensions
    networks:
      - sonarnet
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:9000 || exit 1"]
      interval: 30s
      timeout: 10s
      retries: 5

  db:
    image: postgres:15
    container_name: sonarqube_db
    environment:
      POSTGRES_USER: sonar
      POSTGRES_PASSWORD: sonarpass
      POSTGRES_DB: sonarqube
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - sonarnet
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U sonar"]
      interval: 30s
      timeout: 10s
      retries: 5

volumes:
  sonarqube_data:
  sonarqube_extensions:
  postgres_data:

networks:
  sonarnet:
    driver: bridge

Explicación paso a paso

Servicios:

SonarQube: Se expone en el puerto 9000 para poder acceder desde el navegador (http://localhost:9000).

PostgreSQL: Base de datos para SonarQube. La contraseña y usuario se configuran con variables de entorno.

Healthchecks:

SonarQube: Se hace un curl al puerto 9000 dentro del contenedor para verificar si está activo.

PostgreSQL: pg_isready verifica si la base de datos está lista para conexiones.

Redes:

Ambos contenedores están en la misma red bridge llamada sonarnet.

Volúmenes:

sonarqube_data: Guarda los datos de SonarQube persistentes.

sonarqube_extensions: Guarda los plugins o extensiones instaladas.

postgres_data: Guarda la base de datos PostgreSQL de forma persistente.

Variables de entorno:

SonarQube:
SONAR_JDBC_URL → URL de conexión a la base de datos
SONAR_JDBC_USERNAME → Usuario de la DB
SONAR_JDBC_PASSWORD → Contraseña de la DB

PostgreSQL:
POSTGRES_USER, POSTGRES_PASSWORD, POSTGRES_DB para inicializar la base de datos.
# Una vez creado tu archivo .yaml realiza la respectiva prueba 
# <img width="971" height="507" alt="image" src="https://github.com/user-attachments/assets/ffe7dc83-5f53-41c5-a03b-9a4ac775e106" />
# ACCEDER A LOCALHOST:puertoDefinido para ingresar a SonarQube
