# Propuesta funcional

> **Estado:** propuesta inicial pendiente de revisión y aprobación del equipo.

## 1. Objetivo

Desarrollar un sistema de gestión para un gimnasio mediante una API REST y una base de datos. El sistema permitirá gestionar la información del gimnasio, sus socios, los planes de membresía y, progresivamente, otras actividades del negocio.

## 2. Alcance inicial

La primera versión se plantea para **un único gimnasio**. La gestión de varias sedes queda como posible ampliación futura.

## 3. Funcionalidades por fases

1. **Configuración y gestión básica:** datos del gimnasio, planes y gestión de socios.
2. **Contratación y pagos:** asignación de planes a socios, pagos y consulta del estado de las membresías.
3. **Control de acceso:** identificación mediante tarjeta o pulsera, comprobación de membresía y registro de entradas.
4. **Funcionalidades complementarias:** entrenadores, clases y reservas.
5. **Expansión a varias sedes:** gestión de diferentes ubicaciones del gimnasio.

El detalle y la prioridad de cada historia se encuentran en [Historias de usuario](historias_usuario.md).

## 4. Qué se propone construir primero

Se propone comenzar con la información básica del gimnasio, los planes y los socios. La primera tanda de trabajo podría centrarse en US-01 a US-04. La US-05 también está marcada como Must y debe incluirse en la planificación de la fase inicial.

## 5. Fuera del alcance inicial

No se propone desarrollar todas las funcionalidades a la vez. El control de acceso, las clases, las reservas y la gestión de varias sedes se incorporarán cuando la base del sistema esté construida y probada.

## 6. Decisiones pendientes

- Confirmar el alcance de la primera entrega.
- Revisar y aprobar las historias y prioridades.
- Confirmar MySQL como gestor de base de datos.
- Elegir el framework de Python para la API.
- Acordar el uso de Docker.
- Definir qué funcionalidades caben en el tiempo disponible.
