# Microservicio REST

**Nombre del servicio**

`authentication-service`

**Puerto**

`8081`

**Objetivo**

Servicio responsable de la generación y validación de Tokens utilizando JWT

**Pasos para ejecutar el servicio**

* `mvn clean install`

*  Crear Base de Datos mysql: cloudx

*  Ejecutar request para registrar uno o más usuarios, ya que solo se podrá generar tokens con usuarios que se 
hayan registrado previamente en el sistema, cabe señalar que dicha contraseña se almacenará encriptada en la BD.

*  Ejecutar request para generar token, se pasarán como parámetros de entrada en el body un usuario y una contraseña registrados anteriormente

* Ejecutar request para validar token, se pasará como parámetro un token generado, dicho token tendrá un tiempo de expiración de 30 min

* `mvn spring-boot:run`

**Ejemplo de peticiones**

* **Petición para registrar usuario**

````
    curl --location 'http://localhost:8081/auth/register' \
        --header 'Content-Type: application/json' \
        --data-raw '{
            "name": "pepe",
            "email": "pepe@resolvit.com",
            "password": 123
        }'
````   

* **Petición para generar token**

````
    curl --location 'http://localhost:8081/auth/token' \
        --header 'Content-Type: application/json' \
        --data '{
            "username": "pepe",
            "password": "123"
        }'
````   

* **Petición validar token**

````
    curl --location 'http://localhost:8081/auth/validate
        ?token=eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJwZXBlIiwiaWF0IjoxNjkzOTY2NjQyLCJleHAiOjE2OTM5Njg0NDJ9.XjBJw0N9BOO55k_3HuF7SGsaXrv_AjC1qlm3-1dAlUk'
````  