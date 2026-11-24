# Guía de desarrollo del proyecto

> **Estado:** guía inicial. Las decisiones técnicas marcadas como pendientes deben acordarse entre todas las personas antes de iniciar la implementación.

Esta guía está pensada para que cualquier integrante pueda entender qué hay que preparar, qué significa cada término y cómo empezar una historia.

## 1. Orden de trabajo propuesto

### Paso 1. Revisar la propuesta funcional

Leer las historias de usuario y decidir en equipo qué funcionalidades se quieren construir, qué prioridades se mantienen, qué se incluye en la primera entrega y qué historias necesitan aclaraciones.

### Paso 2. Dibujar cómo se organiza la información

Preparar un **diagrama entidad-relación (ER)**: un dibujo que muestra qué tipos de información guardará el sistema, qué datos tiene cada tipo y cómo se relacionan.

Ejemplo: un socio puede contratar una membresía; una membresía corresponde a un plan. El dibujo ayuda a decidir qué tablas necesitaremos.

No es necesario diseñar desde el primer día todas las funcionalidades futuras. El modelo se puede ampliar conforme avance el proyecto.

### Paso 3. Elegir las herramientas

| Elemento | Para qué sirve | Situación propuesta |
|---|---|---|
| Python | Lenguaje con el que programaremos la aplicación | Base de trabajo prevista |
| Framework de API | Herramienta que facilita recibir peticiones y devolver respuestas HTTP | Pendiente de elegir (por ejemplo, FastAPI o Flask) |
| MySQL | Programa que guarda y permite consultar los datos | Propuesta inicial, pendiente de confirmar |
| Docker Desktop | Permite ejecutar programas en contenedores (entornos aislados) | Se propone probarlo para ejecutar MySQL |
| phpMyAdmin | Interfaz web para ver y administrar MySQL desde el navegador | Herramienta de apoyo que ya se ha probado |
| Git y GitHub | Guardar versiones del código y colaborar | Requeridos para el proyecto |

El README del bootcamp permite distintas tecnologías y frameworks; no impone por sí mismo FastAPI, Flask, MySQL o Docker. El equipo debe confirmar sus elecciones.

### Paso 4. Acordar cómo organizaremos el código

La **estructura del proyecto** es la organización de carpetas y archivos donde guardaremos cada parte de la aplicación.

Las **convenciones** son reglas compartidas para escribir nombres y organizar los cambios. Por ejemplo, acordar cómo llamaremos a las tablas, funciones, archivos y ramas.

La estructura definitiva dependerá del framework elegido. No hace falta crear todas las carpetas antes de conocerlo.

### Paso 5. Crear las primeras tablas

Con el diagrama ER acordado, crear en MySQL las tablas necesarias para las primeras historias. Comprobar que las relaciones y claves funcionan.

Docker puede facilitar que todas las personas utilicen una configuración similar de MySQL. Si se usa, habrá que documentar cómo iniciar y detener los contenedores y cómo conservar los datos.

### Paso 6. Desarrollar las historias

Cada persona trabaja en su rama, implementa su funcionalidad y prepara pruebas. Los cambios se integran mediante Pull Request y revisión de otra persona.

## 2. Cómo se comunica la API

Una **API** es una forma organizada para que dos programas se comuniquen. En este proyecto, la API recibirá peticiones y trabajará con la base de datos para devolver respuestas.

Un **endpoint** es una dirección de la API que permite realizar una operación concreta.

Ejemplos:

- `GET /socios/1`: consultar el socio con identificador 1.
- `POST /socios`: registrar un socio nuevo.
- `PUT /socios/1`: modificar los datos del socio 1.
- `DELETE /socios/1`: eliminar el socio 1, si esa operación se contempla y autoriza.

Los nombres y comportamientos definitivos se acordarán al diseñar cada historia.

## 3. Qué es el contrato de una historia

Es el acuerdo que permite que varias personas desarrollen partes compatibles.

Para cada historia se documentará:

- qué operación debe realizar;
- qué datos necesita recibir;
- qué resultado debe devolver;
- qué debe ocurrir si los datos no son válidos o el registro no existe;
- cómo comprobaremos que funciona.

Ejemplo para consultar un socio:

- Petición: `GET /socios/1`.
- Si existe: devolver sus datos.
- Si no existe: devolver un error que indique que no se encontró.
- Pruebas: consultar un socio existente y consultar un identificador inexistente.

Así, quien desarrolla la consulta puede avanzar con datos ficticios aunque el registro de socios todavía esté en desarrollo.

## 4. Convenciones de Git y GitHub

- **Repositorio:** espacio del proyecto en GitHub donde se guardan los archivos y su historial.
- **Rama:** línea de trabajo separada para desarrollar una historia sin modificar directamente la rama principal.
- **Commit:** registro de un conjunto de cambios con un mensaje que explica qué se ha hecho.
- **Pull Request (PR):** solicitud para incorporar los cambios de una rama a otra y revisarlos antes de integrarlos.

El README del bootcamp propone:

- ramas `main` y `develop`;
- una rama por historia, incluyendo su identificador, por ejemplo `feat/US-03-registrar-socio`;
- mensajes de commit con prefijos como `feat:`, `fix:`, `docs:` y `test:`;
- Pull Requests hacia `develop`, revisados por otra persona.

## 5. Glosario básico

| Término | Explicación sencilla |
|---|---|
| API | Medio por el que dos programas se comunican siguiendo unas reglas. |
| API REST | API que utiliza convenciones HTTP para consultar o modificar recursos. |
| Endpoint | Dirección de la API asociada a una operación. |
| HTTP | Protocolo que utilizan clientes y servidores para intercambiar peticiones y respuestas. |
| CRUD | Crear, consultar, modificar y eliminar información. |
| Framework | Conjunto de herramientas y reglas que facilita construir una aplicación. |
| Base de datos | Información organizada para poder guardarla y consultarla. |
| Gestor de base de datos | Programa que administra la base de datos, como MySQL. |
| Contenedor | Entorno aislado donde se ejecuta un programa. |
| Docker | Herramienta para crear y ejecutar contenedores. |
| phpMyAdmin | Interfaz web para administrar bases de datos MySQL. |
| Diagrama ER | Dibujo de las entidades, sus datos y sus relaciones. |
| Commit | Registro de cambios en Git. |
| Rama | Línea independiente de trabajo en Git. |
| Pull Request | Solicitud para revisar e incorporar cambios de una rama. |
| Test | Prueba que comprueba si una parte del programa funciona como se espera. |

## 6. Decisiones que siguen pendientes

- Framework de Python para la API.
- Confirmación de MySQL.
- Forma de utilizar Docker y phpMyAdmin en los equipos.
- Estructura definitiva de carpetas.
- Convenciones de nombres y formato.
- Diseño ER aprobado.
- Contratos y criterios de aceptación de cada historia.
