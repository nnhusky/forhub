

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



