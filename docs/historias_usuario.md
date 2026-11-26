# Historias de usuario

> **Estado:** propuesta pendiente de revisión y aprobación del equipo.

## Criterios generales del modelo

- Cada entidad tendrá un identificador interno propio (`socio_id`, `sede_id`, `plan_cuota_id`, etc.), que se utilizará para establecer las relaciones entre tablas.
- Los identificadores funcionales, como el NIF/NIE, podrán utilizarse para buscar registros. El NIF/NIE del socio será único.
- Las relaciones entre entidades se establecerán mediante claves foráneas, evitando duplicar datos personales o información que ya esté registrada en otra entidad.
- En la primera versión se trabajará con una sede por socio y por entrenador. El diseño deberá permitir ampliar estas relaciones en el futuro.
- Los planes de cuotas serán comunes a todas las sedes.
- Las entradas deberán registrar la sede en la que se producen, independientemente de la sede de referencia del socio.

## Fase 1 · Configuración y gestión de socios

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-01 | Como administrador, quiero registrar y gestionar las sedes del gimnasio para configurar el sistema y permitir la gestión de una o varias ubicaciones. **Datos:** `sede_id` (identificador interno), nombre, dirección, ciudad y datos de contacto. **Relaciones:** la sede podrá estar relacionada con socios, entrenadores, contrataciones, clases y registros de entrada. Cada relación utilizará `sede_id` como referencia. **Operaciones:** registrar, consultar, modificar y gestionar las sedes existentes. | Must |
| US-02 | Como administrador, quiero crear y gestionar planes de cuotas para ofrecer distintas modalidades de acceso al gimnasio. **Datos:** `plan_cuota_id`, nombre, duración y precio. **Relaciones:** cada contratación utilizará el `plan_cuota_id` del plan seleccionado. Los planes serán comunes a todas las sedes, por lo que no tendrán una relación directa con `sede_id`. **Operaciones:** crear, consultar y modificar planes de cuotas. | Must |
| US-03 | Como recepcionista, quiero registrar nuevos socios para mantener una base de datos con su información personal y de contacto. **Datos:** `socio_id`, nombre, apellidos, NIF/NIE, fecha de nacimiento, teléfono, correo electrónico y dirección. El NIF/NIE será único y permitirá localizar al socio. **Relaciones:** cada socio estará asociado a una única sede mediante `sede_id` en esta primera versión. La relación utilizará el identificador interno del socio (`socio_id`), no su NIF/NIE. | Must |
| US-04 | Como recepcionista, quiero consultar los datos de un socio para comprobar su información y situación en el gimnasio. **Búsqueda:** el socio podrá localizarse mediante su NIF/NIE. **Información:** se mostrarán sus datos personales y de contacto, sede de referencia, contrataciones y estado de sus cuotas. La información de contrataciones y cuotas se obtendrá de sus registros relacionados, sin duplicarla en la ficha del socio. | Must |
| US-05 | Como recepcionista, quiero modificar los datos de un socio para mantener actualizada su información. **Datos modificables:** nombre, apellidos, NIF/NIE, fecha de nacimiento, teléfono, correo electrónico, dirección y sede de referencia. El NIF/NIE deberá mantener su condición de único. El `socio_id` no cambiará al actualizar los datos, de manera que se conserven las relaciones con contrataciones, pagos, tarjetas, entradas y reservas. | Must |
| US-06 | Como administrador, quiero consultar y filtrar el listado de socios para conocer la cantidad de socios registrados y su situación en el gimnasio. **Información:** identificador, nombre, apellidos, NIF/NIE, sede y situación de sus cuotas. **Búsqueda y filtros propuestos:** por NIF/NIE, nombre, apellidos, sede y estado de las cuotas. La información de las cuotas se obtendrá de las contrataciones relacionadas con cada socio. | Should |

## Fase 2 · Cuotas y pagos

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-07 | Como recepcionista, quiero asignar un plan de cuotas a un socio para registrar su contratación y establecer su periodo de vigencia. **Datos de la contratación:** `contratacion_id`, `socio_id`, `plan_cuota_id`, fecha de contratación, fecha de inicio y fecha de fin de la vigencia, y estado. **Relaciones:** la contratación debe estar asociada a un socio existente y a un plan de cuotas existente. También se registrará la sede donde se formaliza la contratación mediante `sede_contratacion_id`. El socio y el plan se referenciarán mediante sus identificadores internos, sin duplicar sus datos. **Estado inicial:** pendiente de pago. | Must |
| US-08 | Como administrador, quiero registrar el pago de una cuota para que, una vez confirmado el pago correspondiente y cumplidas las condiciones de vigencia, la contratación pase a estar activa. **Datos del pago:** `pago_id`, `contratacion_id`, importe abonado y fecha del pago. **Relaciones:** cada pago estará asociado a una contratación existente mediante `contratacion_id`. El socio se identificará a través de esa contratación. **Comportamiento:** al confirmar el pago, se actualizará el estado de la contratación cuando corresponda según sus condiciones de vigencia. | Must |
| US-09 | Como recepcionista, quiero consultar el estado de las cuotas de un socio para saber si están activas, vencidas, pendientes de pago o canceladas. **Información:** plan contratado, fecha de contratación, periodo de vigencia, estado y pagos asociados. **Relaciones:** se consultarán las contrataciones vinculadas al socio mediante `socio_id` y los pagos asociados a cada contratación mediante `contratacion_id`. | Must |
| US-10 | Como recepcionista, quiero consultar el historial de pagos de un socio para comprobar los pagos realizados por sus cuotas. **Información:** fecha del pago, importe abonado y contratación a la que corresponde. **Relaciones:** el historial se obtendrá a partir de las contrataciones del socio y los pagos relacionados con cada una. Se conservará el registro histórico de los pagos. | Should |
| US-21 | Como administrador, quiero cancelar una cuota para finalizar una contratación concreta, conservando el historial del socio y de los pagos asociados. **Relaciones:** se identificará la contratación que se desea cancelar mediante `contratacion_id`. **Comportamiento:** la cancelación afectará únicamente a esa contratación y actualizará su estado a cancelada. Se conservarán la contratación y los pagos relacionados, sin eliminarlos del historial. | Must |
| US-22 | Como administrador, quiero dar de baja a un socio para indicar que ya no pertenece al gimnasio, conservando su registro y su historial de actividad. **Datos:** se actualizará la situación del socio mediante un estado o indicador de baja. **Relaciones:** se conservarán las relaciones con sus contrataciones, pagos, tarjetas, entradas y reservas. No se eliminarán los registros históricos del socio. | Must |

## Fase 3 · Control de acceso y asistencia

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-11 | Como administrador, quiero registrar una tarjeta o pulsera de acceso y asociarla a un socio para permitir su identificación en el gimnasio. **Datos:** `tarjeta_id`, identificador de la tarjeta o pulsera y estado. **Relaciones:** cada tarjeta o pulsera estará asociada a un socio existente mediante `socio_id`. El identificador de la tarjeta o pulsera deberá permitir distinguirla de las demás. No se vinculará directamente a una sede, para permitir una posible ampliación del acceso entre sedes. | Should |
| US-12 | Como sistema de control de acceso, quiero comprobar que el socio tiene una cuota activa y vigente antes de autorizar la entrada para evitar accesos no permitidos. **Datos consultados:** socio identificado, contrataciones asociadas, estado de la contratación y periodo de vigencia. **Relaciones:** se consultará el socio mediante `socio_id` y sus contrataciones mediante la relación con `socio_id`. **Comportamiento:** se autorizará el acceso cuando se cumplan las condiciones de actividad y vigencia de la cuota. | Should |
| US-13 | Como socio, quiero acceder al gimnasio utilizando mi tarjeta o pulsera identificativa para entrar de forma rápida y sencilla. **Comportamiento:** el sistema identificará al socio mediante la tarjeta o pulsera asociada a su registro y comprobará las condiciones de acceso definidas en US-12 antes de autorizar la entrada. | Should |
| US-14 | Como recepcionista, quiero buscar a un socio en el sistema mediante su NIF/NIE y registrar su entrada, previa comprobación de sus condiciones de acceso, para llevar un control de su asistencia al gimnasio. **Datos de la entrada:** `entrada_id`, `socio_id`, fecha y hora de entrada y `sede_id` donde se produce. **Relaciones:** la entrada estará asociada al socio y a la sede correspondiente. **Comportamiento:** antes de registrar la entrada, se comprobarán las condiciones de acceso de US-12. | Should |
| US-15 | Como administrador, quiero desactivar una tarjeta o pulsera extraviada para impedir que pueda utilizarse para acceder al gimnasio. **Relaciones:** se identificará la tarjeta o pulsera mediante `tarjeta_id`. **Comportamiento:** se actualizará su estado para impedir que vuelva a utilizarse para identificar al socio. Se conservará el registro de la tarjeta o pulsera desactivada. | Could |
| US-16 | Como administrador, quiero consultar el historial de accesos de los socios para conocer su asistencia al gimnasio. **Información:** socio, fecha y hora de entrada y sede en la que se produjo. **Relaciones:** se consultarán los registros de entrada asociados al socio mediante `socio_id` y a la sede mediante `sede_id`. Se conservará el historial de entradas. | Could |

**Nota sobre US-14:** el registro manual de entradas desde recepción constituye la funcionalidad básica de control de acceso. La integración física con lectores de tarjetas o pulseras se abordará si el alcance y el tiempo disponible lo permiten.

## Fase 4 · Entrenadores, clases y reservas

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-17 | Como administrador, quiero registrar entrenadores con sus datos personales y profesionales para gestionar el personal del gimnasio. **Datos propuestos:** `entrenador_id`, nombre, apellidos, NIF/NIE, teléfono, correo electrónico y especialidad o titulación profesional. **Relaciones:** cada entrenador estará asociado a una sede mediante `sede_id` en la primera versión. Esta relación podrá ampliarse en el futuro para permitir que un entrenador trabaje en varias sedes. | Could |
| US-18 | Como administrador, quiero crear clases y actividades asignándoles un horario, una duración, un aforo y un entrenador para organizar la oferta del gimnasio. **Datos:** `clase_id`, nombre de la clase, fecha y hora, duración, aforo y `entrenador_id` del entrenador asignado. **Relaciones:** cada clase estará asociada a un entrenador existente y a una sede mediante `sede_id`, para identificar dónde se imparte. | Could |
| US-19 | Como socio, quiero reservar una plaza en una clase para asegurar mi participación en la actividad. **Datos:** `reserva_id`, `socio_id`, `clase_id` y fecha de la reserva. **Relaciones:** cada reserva estará asociada a un socio existente y a una clase existente. El sistema conservará la relación entre ambos registros para poder consultar las reservas realizadas por cada socio y las plazas reservadas en cada clase. | Could |

## Fase 5 · Gestión de varias sedes

| ID | Historia de usuario | Prioridad |
|---|---|---|
| US-20 | Como administrador, quiero gestionar diferentes sedes del gimnasio con sus datos de identificación, dirección y ciudad para poder administrar una cadena de gimnasios desde un mismo sistema. **Datos:** `sede_id`, nombre, dirección, ciudad y datos de contacto. **Relaciones:** las sedes estarán relacionadas con los socios, entrenadores, contrataciones, clases y entradas correspondientes. Esta funcionalidad permitirá ampliar la gestión a varias ubicaciones desde un mismo sistema. | Future |

## Consideraciones pendientes de validación del equipo

Los siguientes puntos deben acordarse antes de implementar las historias correspondientes. No se consideran requisitos aprobados todavía.

1. **Datos de socios:** determinar qué campos son obligatorios y cuáles opcionales. Confirmar también si se permitirá modificar el NIF/NIE.
2. **Datos de entrenadores:** validar los campos personales y profesionales propuestos y decidir si se necesita registrar más información.
3. **Sedes y socios:** en la primera versión cada socio tendrá una única sede de referencia. En una futura ampliación podrá acceder a otras sedes sin necesidad de cambiar su sede de referencia.
4. **Sedes y entrenadores:** en la primera versión cada entrenador tendrá una única sede. Si se amplía el modelo, se podrá sustituir esa relación por una relación muchos a muchos mediante una tabla intermedia.
5. **Planes de cuotas:** serán comunes a todas las sedes. No se asociarán directamente a una sede.
6. **Contrataciones:** se conservará la sede donde se formalizó cada contratación. Confirmar si esta información es necesaria desde la primera versión.
7. **Pagos:** confirmar si se admitirán pagos parciales, varios pagos para una misma contratación o devoluciones. La historia actual solo contempla registrar el importe abonado y la fecha.
8. **Estados de las cuotas:** definir las condiciones exactas para pasar de pendiente de pago a activa, de activa a vencida y a cancelada.
9. **Baja de socios:** decidir qué ocurre con las contrataciones activas y las reservas cuando se da de baja a un socio.
10. **Control de acceso:** definir si un socio puede tener varias tarjetas o pulseras activas y qué ocurre cuando se desactiva una.
11. **Acceso entre sedes:** en una futura ampliación se deberá permitir comprobar las condiciones de acceso independientemente de la sede de referencia del socio.
12. **Reservas:** definir si un socio puede reservar varias plazas, si puede cancelar una reserva y qué ocurre cuando se alcanza el aforo máximo.
13. **Sedes y clases:** cada clase estará asociada a una sede. La asignación de entrenadores a varias sedes podrá incorporarse cuando se amplíe el modelo.