# ForoHub

**ForoHub** es una aplicación de foro diseñada para gestionar usuarios, temas, respuestas y cursos de manera eficiente. Este proyecto incluye autenticación de usuarios, manejo de tópicos (temas), y soporte para múltiples roles y perfiles.

## Estructura del Proyecto

El proyecto sigue una estructura modular, organizada de la siguiente manera:

- **clase/**: Contiene las entidades principales del modelo de datos como `Curso`, `Perfil`, `Respuesta`, `Topico`, y `Usuario`.
- **config/**: Configuraciones de seguridad, incluyendo autenticación y autorización.
- **controller/**: Controladores REST para manejar solicitudes HTTP (endpoints).
- **dto/**: Objetos de transferencia de datos para comunicación entre la capa de servicio y la capa de presentación.
- **repository/**: Interfaces que extienden `JpaRepository` para la interacción con la base de datos.
- **resources/db.migration/**: Archivos SQL para la creación y migración de las tablas de la base de datos.

## Tecnologías Utilizadas

- **Java 17**: Lenguaje de programación principal.
- **Spring Boot**:
    - **Spring Security**: Autenticación y autorización.
    - **Spring Web**: Creación de APIs REST.
    - **Spring Data JPA**: Interacción con bases de datos relacionales.
    - **Spring Validation**: Validación de datos de entrada.
- **PostgreSQL**: Base de datos relacional utilizada para el almacenamiento.
- **Flyway**: Herramienta para gestionar migraciones de base de datos.
- **Lombok**: Simplificación del código al generar automáticamente getters, setters y otros métodos comunes.
- **JWT (Json Web Tokens)**: Manejo de autenticación mediante tokens.
- **Maven**: Herramienta para la gestión de dependencias y construcción del proyecto.

## Endpoints Principales

### Autenticación
- `POST /login`: Inicia sesión con credenciales y retorna un token JWT.

### Gestión de Tópicos
- `POST /topicos`: Registra un nuevo tópico.
- `GET /topicos`: Lista tópicos con paginación.
- `GET /topicos/{id}`: Obtiene el detalle de un tópico específico.
- `PUT /topicos/{id}`: Actualiza un tópico existente.
- `DELETE /topicos/{id}`: Elimina un tópico por ID.

## Instalación y Configuración

1. **Clona el repositorio**:
   ```bash
   git clone https://github.com/Miguel-Ghost/ForoHub.git
   cd ForoHub
    ```
2. **Configura la base de datos:** 
    Actualiza el archivo application.properties o application.yml con las credenciales de tu base de datos.

3. **Ejecuta las migraciones:** 
   Spring Boot ejecutará automáticamente los archivos SQL en resources/db.migration/ para crear las tablas necesarias.

4. **Inicia la aplicación:**
    ```bash
    mvn spring-boot:run
    ```
5. **Accede a la API:** 
    La API estará disponible en http://localhost:8080.

## Modelo de Base de Datos

El esquema incluye las siguientes tablas:


- **usuario**: Almacena información de los usuarios.
- **perfil**: Roles asignados a los usuarios.
- **curso**: Información sobre cursos disponibles.
- **topico**: Tópicos del foro.
- **respuesta**: Respuestas asociadas a los tópicos.
- **usuario_perfil**: Relación muchos a muchos entre usuario y perfil.

## Seguridad
- Implementación de autenticación basada en JWT.
- Control de acceso configurado en SecurityConfig.
- Filtros de seguridad definidos en SecurityFilter.

## Ejemplo de Uso

### Autenticación

Para autenticar un usuario, se debe enviar un objeto `DatoLogin` con los siguientes campos:

- `usuario`: Nombre de usuario.
- `clave`: Contraseña.

Ejemplo de solicitud:
```json
{
  "usuario": "miguel.inocente.c@uni.pe",
  "clave": "123456"
}
```

Se le generarán un token JWT que deberá ser incluido en las cabeceras de las solicitudes posteriores.

```json
    {
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJtaWd1ZWwuaW5vY2VudGUuY0B1bmkucGUiLCJpYXQiOjE3MzcyNDgxNDksImV4cCI6MTczNzI1MTc0OX0.ZJaeCWlvWLLdin8Pu9be4soD_xDy0pF13pUBBxvHnGY"
}
```

![img.png](imagenes/img.png)

Luego debera colocarlo en la cabecera de la siguiente manera:

![img_1.png](imagenes/img_1.png)

Esto se debe realizar para cada solicitud posterior.


### Registrar Tópicos

Para registrar un tópico, se debe enviar un json con los siguientes campos:

- `titulo`: Título del tópico.
- `mensaje`: Mensaje del tópico.
- `autorId`: ID del autor del tópico.
- `nombreCurso`: Nombre del curso del tópico.


Ejemplo de solicitud:
```json
{
  "titulo": "Introducción a Java",
  "mensaje": "¿Cómo configuro mi entorno de desarrollo para Java?",
  "autorId": 1,
  "nombreCurso": "Programación en Java"
}
```
![img_6.png](imagenes/img_6.png)

### Listar Tópicos

Para listar tópicos, se puede enviar una solicitud GET a `/topicos` con previa autenticación.

![img_2.png](imagenes/img_2.png)

### Obtener Detalle de Tópico

Para obtener el detalle de un tópico específico, se puede enviar una solicitud GET a `/topicos/{id}` con previa autenticación.

![img_3.png](imagenes/img_3.png)

### Actualizar Tópico


Para actualizar un tópico existente, se puede enviar una solicitud PUT a `/topicos/{id}` con previa autenticación.
Ejecutar la solicitud actualizacion con el siguiente json:

```json
{
  "titulo": "Problemas con CSS y javaScript",
  "mensaje": "No logro centrar un div y relacionar la funcion en el html, ¿alguien puede ayudarme?",
  "estado": "PENDIENTE"
}
```

![img_7.png](imagenes/img_7.png)

Solo se puede actualizar el campo `titulo` , `mensaje` y `estado`(En estado de `PENDIENTE` o `RESOLVIDO`).
Los demás campos aunque le pasen nuevos valores no se actualizaran.

### Eliminar Tópico

Para eliminar un tópico, se puede enviar una solicitud DELETE a `/topicos/{id}` con previa autenticación.

![img_5.png](imagenes/img_5.png)

## Endpoints del API - UNI Foro Hub 

Este proyecto utiliza un API para gestionar tópicos en el foro. Los endpoints han sido configurados y probados en Insomnia.

![img_8.png](imagenes/img_8.png)