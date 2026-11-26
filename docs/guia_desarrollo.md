# Guía de desarrollo del proyecto

> **Estado:** guía inicial. Las decisiones técnicas marcadas como pendientes deben acordarse entre todas las personas antes de iniciar la implementación.

Esta guía está pensada para que cualquier integrante pueda entender qué hay que preparar, qué significa cada término y cómo empezar una historia. También recoge el flujo de colaboración mediante Git y GitHub acordado para el repositorio.

## 1. Orden de trabajo propuesto

### Paso 1. Revisar la propuesta funcional

Leer las historias de usuario y decidir en equipo qué funcionalidades se quieren construir, qué prioridades se mantienen, qué se incluye en la primera entrega y qué historias necesitan aclaraciones.

La aprobación conjunta de las historias de usuario es un punto previo importante: permite compartir una misma definición del alcance antes de diseñar la solución técnica y repartir el trabajo.

### Paso 2. Dibujar cómo se organiza la información

Preparar un **diagrama entidad-relación (ER)**: un dibujo que muestra qué tipos de información guardará el sistema, qué datos tiene cada tipo y cómo se relacionan.

Ejemplo: un socio puede contratar una membresía; una membresía corresponde a un plan. El dibujo ayuda a decidir qué tablas necesitaremos.

No es necesario diseñar desde el primer día todas las funcionalidades futuras. El modelo se puede ampliar conforme avance el proyecto.

El diseño del modelo de datos debe responder a las historias de usuario que el equipo haya acordado. Si se modifican las historias o su alcance, puede ser necesario revisar el diagrama.

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

### Paso 6. Definir el reparto del trabajo y desarrollar las historias

Una vez aprobadas las historias de usuario y acordados los principales criterios de diseño, el equipo podrá decidir cómo dividir el trabajo. El reparto dependerá de las funcionalidades, sus dependencias y del diseño que finalmente se acuerde; por eso no se fija de antemano en esta guía.

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

### 4.1. Ramas principales

| Rama | Función |
|---|---|
| `main` | Rama principal. Contiene la versión estable y recibe las integraciones finales revisadas por el equipo. |
| `develop` | Rama de integración. Recibe el trabajo de las ramas de funcionalidad después de su revisión mediante Pull Request. |

El trabajo habitual se desarrolla a partir de `develop`, no directamente desde `main`.

### 4.2. Ramas de funcionalidad

Cada integrante crea una rama para la historia o tarea asignada. Estas ramas deben partir de `develop`.

Ejemplo: `feat/US-03-registrar-socio`.

Prefijos recomendados:

- `feat/`: nueva funcionalidad.
- `fix/`: corrección de un error.
- `docs/`: cambios en documentación.
- `test/`: incorporación o modificación de pruebas.

### 4.3. Flujo de trabajo acordado

1. Actualizar la copia local de `develop`.
2. Crear una rama de funcionalidad a partir de `develop`.
3. Realizar los cambios y pruebas en esa rama.
4. Registrar los cambios mediante commits.
5. Publicar la rama en GitHub.
6. Abrir un Pull Request con destino `develop`.
7. Solicitar la revisión de otra persona del equipo.
8. Incorporar los cambios cuando se cumplan las condiciones de protección.
9. Cuando `develop` esté preparado para una versión estable, abrir un Pull Request con destino `main`.
10. Revisar esa integración final y realizar el merge cuando esté aprobada.

Representación simplificada:

```text
main
  └── develop
        ├── feat/US-03-registrar-socio ── PR → develop
        ├── feat/US-04-consultar-socio ── PR → develop
        └── PR develop → main (versión estable)
```

Las ramas de funcionalidad no deben crearse desde `main`, sino desde `develop`.

### 4.4. Clonar el repositorio y trabajar desde develop

Para clonar inicialmente solo la rama `develop`:

```bash
git clone --branch develop --single-branch https://github.com/tania-herrera/gymnasio_crud.git
```

También se puede clonar el repositorio completo y cambiar después a `develop`:

```bash
git clone https://github.com/tania-herrera/gymnasio_crud.git
cd gymnasio_crud
git switch develop
git pull origin develop
```

Para crear una rama de funcionalidad:

```bash
git switch develop
git pull origin develop
git switch -c feat/US-03-registrar-socio
```

Para publicarla por primera vez en GitHub:

```bash
git push -u origin feat/US-03-registrar-socio
```

Los comandos se ejecutan desde la carpeta local del repositorio. Antes de empezar una historia, conviene actualizar `develop` para partir de su versión más reciente.

**Importante:** `--single-branch` limita las ramas que se descargan inicialmente; no es una medida de seguridad ni impide que una persona con acceso al repositorio consulte o descargue `main` posteriormente.

### 4.5. Protección de main y develop

El repositorio tiene un Ruleset activo llamado **Protección estándar de ramas - PR y revisión obligatoria**. Se aplica a `develop` y a la rama predeterminada del repositorio (`main`).

| Protección | Qué implica |
|---|---|
| Pull Request obligatorio | Para incorporar cambios se debe abrir un Pull Request; no se permite hacerlo mediante push directo. |
| Una aprobación como mínimo | El Pull Request necesita al menos una aprobación antes de integrarse. |
| Sin excepciones para omitir las reglas | Las protecciones también se aplican a la persona administradora. |
| Bloqueo de eliminación | No se permite eliminar las ramas protegidas. |
| Bloqueo de force push | No se permite reescribir el historial de las ramas protegidas mediante force push. |
| Aprobación de la última modificación revisable | Si se realizan nuevos cambios después de una aprobación, otra persona debe revisarlos y aprobarlos antes de integrar el Pull Request. |

Estas protecciones controlan **cómo se modifican** `main` y `develop`; no ocultan las ramas ni restringen la lectura o clonación del repositorio.

El repositorio es público. Cualquier persona puede consultar y clonar su contenido, pero eso no le concede permisos para modificar el repositorio original. La protección de ramas tampoco cambia la visibilidad ni los permisos de acceso.

### 4.6. Revisión y responsabilidades

- Cada integrante prueba sus cambios antes de abrir un Pull Request.
- Otra persona del equipo revisa el Pull Request y comprueba que los cambios cumplen lo esperado.
- La persona que desarrolla no debe aprobar su propio trabajo.
- Los Pull Requests de funcionalidades se dirigen a `develop`.
- La integración final de `develop` en `main` debe recibir una revisión y aprobación de otra persona colaboradora. La persona responsable de la integración final realiza el merge cuando se cumplen las condiciones.
- Los cambios que afecten a la documentación general o a los acuerdos de trabajo del equipo deben comunicarse a todos los integrantes, por ejemplo, mediante el foro del proyecto. Cuando sea conveniente, se podrá solicitar la revisión de todos, aunque no sea necesaria la aprobación de todos para integrar los cambios.

### 4.7. Mensajes de commit

Se utilizarán mensajes breves que indiquen el tipo de cambio. Por ejemplo:

- `feat: add member registration`
- `fix: validate member email`
- `docs: update development guide`
- `test: add member endpoint tests`

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
| Clonar | Crear una copia local de un repositorio remoto. |
| Approval | Aprobación formal de una revisión de Pull Request en GitHub. |
| Ruleset | Conjunto de reglas de GitHub que se aplica a determinadas ramas o etiquetas. |

## 6. Decisiones que siguen pendientes

- Aprobación conjunta de las historias de usuario y confirmación del alcance.
- Framework de Python para la API.
- Confirmación de MySQL.
- Forma de utilizar Docker y phpMyAdmin en los equipos.
- Estructura definitiva de carpetas.
- Convenciones de nombres y formato.
- Diseño ER aprobado.
- Contratos y criterios de aceptación de cada historia.
- Reparto del trabajo, una vez aprobadas las historias y acordado el diseño.
- Acordar quién revisará los Pull Requests de cada integrante y quién participará en la revisión final hacia `main`.
