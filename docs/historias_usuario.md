# Historias de usuario

> **Estado:** propuesta pendiente de revisión del equipo. Los identificadores, descripciones, prioridades y fases se han trasladado del Excel actualizado.

Las historias describen funcionalidades desde el punto de vista de quien las necesita. Las prioridades se conservan tal como aparecen en el Excel.

## Fase 1 · Configuración y gestión básica

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-01 | Como administrador del gimnasio, quiero registrar los datos del gimnasio (nombre, dirección y datos de contacto) para configurar el sistema de gestión. | Must |
| US-02 | Como administrador, quiero crear planes de membresía con nombre, duración y precio para ofrecer distintas modalidades de acceso al gimnasio. | Must |
| US-03 | Como recepcionista, quiero registrar nuevos socios con sus datos personales y de contacto para mantener una base de datos de clientes. | Must |
| US-04 | Como recepcionista, quiero consultar los datos de un socio para comprobar su información y situación en el gimnasio. | Must |
| US-05 | Como recepcionista, quiero modificar los datos de un socio para mantener actualizada su información. | Must |
| US-06 | Como administrador, quiero consultar el listado de socios para conocer la cantidad de clientes registrados en el gimnasio. | Should |

## Fase 2 · Contratación y pagos

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-07 | Como recepcionista, quiero asignar un plan de membresía a un socio para registrar su contratación y fecha de vigencia. | Must |
| US-08 | Como administrador, quiero registrar los pagos de los socios asociados a sus membresías para llevar un control de los ingresos del gimnasio. | Must |
| US-09 | Como recepcionista, quiero consultar el estado de la membresía de un socio para saber si está activa, vencida o pendiente. | Must |
| US-10 | Como recepcionista, quiero consultar el historial de pagos de un socio para comprobar las cuotas que ha abonado. | Should |

## Fase 3 · Control de acceso

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-11 | Como administrador, quiero registrar una tarjeta o pulsera de acceso y asociarla a un socio para permitir su identificación en el gimnasio. | Should |
| US-12 | Como sistema de control de acceso, quiero comprobar que la membresía del socio está activa antes de autorizar la entrada para evitar accesos no permitidos. | Should |
| US-13 | Como socio, quiero acceder al gimnasio utilizando mi tarjeta o pulsera identificativa para entrar de forma rápida y sencilla. | Should |
| US-14 | Como sistema de control de acceso, quiero registrar la fecha y hora de cada entrada para mantener un historial de asistencia. | Should |
| US-15 | Como administrador, quiero desactivar una tarjeta o pulsera extraviada para impedir que pueda utilizarse para acceder al gimnasio. | Could |
| US-16 | Como administrador, quiero consultar el historial de accesos de los socios para conocer su asistencia al gimnasio. | Could |

## Fase 4 · Funcionalidades complementarias

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-17 | Como administrador, quiero registrar entrenadores con sus datos profesionales para gestionar el personal del gimnasio. | Could |
| US-18 | Como administrador, quiero crear clases y actividades asignándoles un horario y un entrenador para organizar la oferta del gimnasio. | Could |
| US-19 | Como socio, quiero reservar una plaza en una clase para asegurar mi participación en la actividad. | Could |

## Fase 5 · Expansión a varias sedes

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-20 | Como administrador, quiero registrar diferentes sedes del gimnasio con su dirección y ciudad para poder gestionar una cadena de gimnasios desde un mismo sistema. | Futuro |

## Revisión del backlog

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-21 | Como recepcionista, quiero registrar la entrada de un socio para llevar un control de la asistencia al gimnasio. | Por revisar |

**Nota sobre US-21:** revisar si se refiere a registrar manualmente una entrada desde recepción o si duplica el registro automático de accesos de US-14. Si son procesos diferentes, conviene explicitar esa diferencia.

## Cómo interpretar las prioridades

- **Must:** prioridad Must asignada en el backlog.
- **Should:** prioridad Should asignada en el backlog.
- **Could:** prioridad Could asignada en el backlog.
- **Futuro:** posible ampliación posterior.
- **Por revisar:** requiere aclaración antes de planificarla.

El equipo debe confirmar el significado y la aplicación de estas prioridades al alcance del proyecto.
