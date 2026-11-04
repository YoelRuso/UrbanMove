---
tipo: servicio
estado: borrador
responsable: Joel
---

# Reservas

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | **Sí** |

## 1. Responsabilidad

Crea, confirma, cancela y expira reservas. Controla que un recurso no se reserve dos veces.

## 2. Qué NO hace

- No gestiona el uso del recurso (inicio y fin): [Viajes](viajes.md).
- No decide de forma global qué recursos son reservables: [Disponibilidad](disponibilidad.md).
- No es el lugar de consulta del histórico: [Historial](historial.md).

## 3. Datos de los que es dueño

Reserva: usuario, recurso, estado (creada, confirmada, cancelada, expirada) y tiempos.

> PENDIENTE: definir el modelo de datos de la reserva y sus estados formales.

## 4. API

> PENDIENTE: definir endpoints para crear, confirmar, cancelar y consultar reservas.

## 5. Eventos que publica

Eventos del catálogo relacionados con esta responsabilidad: `VehicleReserved`,
`ReservationCancelled` y `ReservationExpired`.

> PENDIENTE: confirmar qué eventos publica Reservas. En concreto, decidir si `ReservationExpired` lo publica Reservas o la Lambda de expiración.

> PENDIENTE: decidir si la confirmación de una reserva emite evento (no existe en el catálogo).

## 6. Eventos que consume

> PENDIENTE: decidir si consume `RideStarted` (para cerrar la reserva) u otros eventos.

## 7. Dependencias de otros servicios

> PENDIENTE: definir la dependencia con Disponibilidad y su comportamiento ante fallo o timeout.

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

- Debe poder escalar horizontalmente (§7.2).
- Candidato a vista de componentes en el PDF (§4.2) y a diagrama de secuencia de reserva.
- La expiración la ejecuta la Lambda [Expiración de reservas](../04-lambdas/expiracion-de-reservas.md)
  si se elige como obligatoria.
- Preguntas de defensa: cómo se evita la doble reserva y qué ocurre cuando una reserva caduca
  (§18).

> PENDIENTE: decidir el mecanismo contra la doble reserva y el tiempo de expiración.

## 10. Relacionado

- [disponibilidad.md](disponibilidad.md)
- [viajes.md](viajes.md)
- [expiracion-de-reservas.md](../04-lambdas/expiracion-de-reservas.md)
- [flujo-usuario.md](../09-flujos/flujo-usuario.md)
