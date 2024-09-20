#  AppConfig Java Sample

## Descripción general

Este proyecto es una demostración de un microservicio en Java basado en Java 1.8, que muestra una lista de películas gratis del mes. La configuración de las películas se gestiona mediante **AWS AppConfig** utilizando el SDK de AWS. El código original se publicó en 2020 y emplea versiones antiguas de bibliotecas como **Spring Boot 2.x**, **Log4j 2.13.x**, y **Junit 4**.

**Amazon Q Developer Agent** puede actualizar automáticamente el código de Java 8 o 11 a Java 17 en tu entorno de desarrollo (JetBrains o Visual Studio Code).

## Instrucciones de instalación

### Local (usando Docker)

1. Clona el repositorio y navega a la carpeta del proyecto.
2. Construye la imagen Docker ejecutando:
   ```bash
   docker build -t movie-service .

3. Inicia el contenedor con: docker run -p 8080:8080 movie-service
4. Abre un navegador y ve a http://localhost:8080/movies/getMovies para ver la lista de películas.

## Despliegue en AWS (usando CloudFormation)

### Paso 1: Crear la infraestructura en AWS usando CloudFormation

1. Abre la consola de AWS CloudFormation.
2. Crea una nueva pila (stack) seleccionando "Con nuevos recursos".
3. Sube la plantilla ecs-cluster.yml del repositorio para crear un clúster de Amazon ECS.
4. Asigna un nombre a la pila, como ECSCluster-dev, y completa los parámetros solicitados.
5. Una vez creada la pila, sube la plantilla fargate-task.yml para crear una tarea de Fargate que ejecutará el contenedor con la aplicación.
6. Proporciona la URL de la imagen Docker generada en Amazon ECR como parámetro para la tarea de Fargate.

### Paso 2: Desplegar el microservicio

1. Verifica el URL externo del balanceador de carga creado por la tarea de Fargate (en la pestaña de Outputs de la consola de CloudFormation).
2. Accede a http://ExternalUrl/movies/getMovies para ver la lista de películas configuradas.

### Paso 3: Actualizar la configuración en AppConfig 
### Nota: los recursos para configurar AppConfig se pueden ejecutar mediante el repositorio de IaC en Terraform: https://github.com/julianisaza/terraform_appconfig_iac

1. Modifica el JSON de configuración en AWS AppConfig para cambiar la lista de películas.
2. Inicia un nuevo despliegue de la configuración para aplicar los cambios.
3. Los cambios se verán reflejados inmediatamente sin necesidad de reiniciar el contenedor.

## Limpieza

Elimina los recursos creados en AWS AppConfig y las pilas de CloudFormation para evitar costos adicionales.

## Licencia

Este código de muestra está licenciado bajo la licencia MIT-0. Consulta el archivo LICENSE.

