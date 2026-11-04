---
tipo: lambda
estado: borrador
responsable: PENDIENTE
---

# Lambda: Expiración de reservas

**Obligatoria:** PENDIENTE (ver [README](README.md)).

## Qué hace (§4.3)

Libera un recurso si una reserva no se confirma en el tiempo establecido.

## Disparador

> PENDIENTE: decidir el disparador (programado, retraso en cola, TTL de base de datos, evento `VehicleReserved`...).

## Entrada

> PENDIENTE: definir los eventos o datos de entrada.

## Salida y efectos

`ReservationExpired` ("Reserva liberada automáticamente por timeout") está relacionado.

> PENDIENTE: decidir si la Lambda publica `ReservationExpired`, llama a Reservas para que expire la reserva, o ambas cosas.

## Parámetros

> PENDIENTE: fijar el tiempo de expiración de una reserva no confirmada.

## Idempotencia y errores

> PENDIENTE: definir cómo se evita expirar una reserva ya confirmada o ya usada (condición de carrera con la confirmación o con `RideStarted`).

## Notas

- Pregunta de defensa: "¿Qué ocurre cuando una reserva caduca?" (§18).

## Relacionado

- [reservas.md](../02-servicios/reservas.md)
- [disponibilidad.md](../02-servicios/disponibilidad.md)
- [estados-recurso.md](../01-arquitectura/estados-recurso.md)
