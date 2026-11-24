# Modelo de datos

> **Estado:** pendiente de diseño y aprobación del equipo. Este documento no define todavía las tablas definitivas.

## 1. Para qué sirve

El modelo de datos describe qué información necesita guardar el gimnasio y cómo se relaciona. El **diagrama entidad-relación (ER)** será el dibujo que represente esa organización antes de crear las tablas en MySQL.

## 2. Entidades que probablemente necesitaremos

Como punto de partida para debatir:

- **Gimnasio:** nombre, dirección y datos de contacto.
- **Socio:** datos personales y de contacto.
- **Plan de membresía:** nombre, duración y precio de la modalidad ofrecida.
- **Membresía:** contratación concreta de un plan por parte de un socio, con fechas y estado.
- **Pago:** pago asociado a una membresía.

Estas entidades se derivan de las funcionalidades iniciales. Sus campos, claves y relaciones deben acordarse en equipo.

## 3. Diferencias importantes

- **Socio:** la persona que utiliza el gimnasio.
- **Plan:** la modalidad que el gimnasio ofrece (por ejemplo, mensual o anual).
- **Membresía:** la contratación concreta de un plan por parte de un socio.
- **Pago:** un movimiento económico asociado a esa contratación.

Un plan no es lo mismo que una membresía. Varios socios pueden contratar el mismo plan, pero cada contratación pertenece a un socio.

## 4. Evolución posterior

Cuando se aborden las siguientes fases, se estudiará cómo incorporar tarjetas o pulseras, registros de acceso, entrenadores, clases, reservas y, si se aprueba, varias sedes.

No se crearán todas esas tablas por adelantado sin conocer las reglas que necesitarán.

## 5. Próximo paso

1. Revisar las entidades propuestas.
2. Identificar qué datos necesita guardar cada una.
3. Decidir identificadores y relaciones.
4. Dibujar el diagrama ER.
5. Revisarlo antes de crear las tablas en MySQL.
