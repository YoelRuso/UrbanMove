---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Estados del recurso

Cada recurso de movilidad tiene un ciclo de vida explícito (§5). Estos son los estados mínimos:

| Estado | Significado (§5) |
|---|---|
| `AVAILABLE` | Disponible para reserva o uso. |
| `RESERVED` | Reservado temporalmente por un usuario. |
| `IN_USE` | En uso durante un viaje. |
| `LOW_BATTERY` | Disponible solo para mantenimiento o pendiente de retirada. |
| `WITHDRAWN` | Retirado de la vía pública. |
| `CHARGING` | En proceso de recarga. |
| `REPAIRING` | En reparación. |
| `READY_FOR_SERVICE` | Listo para volver a la calle. |
| `RETIRED` | Dado de baja definitivamente. |

El grupo debe documentar **qué eventos provocan cada transición** y **qué microservicio es
responsable de validarla** (§5).

## Transiciones

Las filas con evento se deducen del "uso esperado" de los eventos de §6. Las demás no tienen
evento en el enunciado.

| Desde | Hacia | Evento | Servicio que valida |
|---|---|---|---|
| (nuevo) | PENDIENTE | `VehiclePurchased` | PENDIENTE |
| `AVAILABLE` | `RESERVED` | `VehicleReserved` | PENDIENTE |
| `RESERVED` | `AVAILABLE` | `ReservationCancelled` | PENDIENTE |
| `RESERVED` | `AVAILABLE` | `ReservationExpired` | PENDIENTE |
| `RESERVED` | `IN_USE` | `RideStarted` | PENDIENTE |
| `AVAILABLE` | `IN_USE` | `RideStarted` (inicio sin reserva, §3.1) | PENDIENTE |
| `IN_USE` | PENDIENTE | `RideFinished` ("liberación o cambio de estado del recurso") | PENDIENTE |
| PENDIENTE | `LOW_BATTERY` | `VehicleBatteryLow` | PENDIENTE |
| PENDIENTE | `WITHDRAWN` | `VehicleWithdrawnForMaintenance` | PENDIENTE |
| PENDIENTE | `AVAILABLE` | `VehicleReturnedToService` | PENDIENTE |
| `WITHDRAWN` | `CHARGING` | PENDIENTE | PENDIENTE |
| `WITHDRAWN` | `REPAIRING` | PENDIENTE | PENDIENTE |
| PENDIENTE | `READY_FOR_SERVICE` | PENDIENTE | PENDIENTE |
| PENDIENTE | `RETIRED` | PENDIENTE | PENDIENTE |

> PENDIENTE: decidir el estado inicial de un recurso tras `VehiclePurchased`.

> PENDIENTE: decidir a qué estado pasa un recurso tras `RideFinished` (p. ej. según la batería o la zona de destino).

> PENDIENTE: decidir los estados de origen de `LOW_BATTERY`, `WITHDRAWN` y de la vuelta a `AVAILABLE` (¿pasa siempre por `READY_FOR_SERVICE`?).

> PENDIENTE: decidir qué eventos (nuevos o existentes) provocan `CHARGING`, `REPAIRING`, `READY_FOR_SERVICE` y `RETIRED`. Si se crean eventos nuevos, añadirlos a [03-eventos](../03-eventos/README.md).

> PENDIENTE: decidir qué servicio valida cada transición y quién es dueño del estado (ver [propiedad-de-datos.md](propiedad-de-datos.md)).

> PENDIENTE: decidir el mecanismo que impide reservar dos veces un recurso (pregunta de defensa, §18).

> PENDIENTE: diagrama de estados (hueco).

## Estados de otras entidades

El enunciado nombra estados de otras entidades sin formalizarlos:

- Reserva: creada, confirmada, cancelada, expirada (§3.1, §4.1).
- Orden de recolocación: asignada, en curso, completada (§3.2).
- Órdenes de mantenimiento y recolocación en el dashboard: abiertas, en curso, completadas (§3.3).

> PENDIENTE: formalizar los estados de reserva, orden de mantenimiento y orden de recolocación en sus fichas.

## Relacionado

- [03-eventos/README.md](../03-eventos/README.md)
- [disponibilidad.md](../02-servicios/disponibilidad.md)
- [inventario-de-recursos.md](../02-servicios/inventario-de-recursos.md)
