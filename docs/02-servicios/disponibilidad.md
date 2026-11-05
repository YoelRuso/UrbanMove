---
tipo: servicio
estado: borrador
responsable: Sergio
---

# Disponibilidad

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | No |

## 1. Responsabilidad

Mantiene qué recursos pueden reservarse en cada momento, evitando mezclar inventario, reservas
y mantenimiento.

## 2. Qué NO hace

- No registra activos: [Inventario de recursos](inventario-de-recursos.md).
- No crea ni gestiona reservas: [Reservas](reservas.md).
- No gestiona tareas de mantenimiento: [Órdenes de mantenimiento](ordenes-de-mantenimiento.md).

## 3. Datos de los que es dueño

El conjunto de recursos reservables en cada momento, por zona.

> PENDIENTE: decidir si Disponibilidad es el dueño del estado operativo del recurso (ver [estados-recurso.md](../01-arquitectura/estados-recurso.md)).

## 4. API

> PENDIENTE: definir endpoints para consultar recursos disponibles por zona y tipo.

## 5. Eventos que publica

> PENDIENTE: decidir qué eventos publica, si alguno.

## 6. Eventos que consume

Es probable que tenga que reaccionar a eventos que cambian la disponibilidad: `VehicleReserved`,
`ReservationCancelled`, `ReservationExpired`, `RideStarted`, `RideFinished`,
`VehicleBatteryLow`, `VehicleWithdrawnForMaintenance`, `VehicleReturnedToService` y
`VehiclePurchased`. El enunciado no lo indica explícitamente.

> PENDIENTE: decidir qué eventos consume y la transición que provoca cada uno.

## 7. Dependencias de otros servicios

> PENDIENTE: definir si Reservas o Viajes consultan a Disponibilidad de forma síncrona antes de reservar o iniciar un viaje.

## 8. Almacenamiento

PostgreSQL, con una base de datos propia ([acuerdos.md](../10-equipo/acuerdos.md)).

## 9. Decisiones y notas

- Participa en "cómo se evita reservar dos veces el mismo recurso" (§18).

> PENDIENTE: decidir el mecanismo de concurrencia entre Disponibilidad y Reservas.

## 10. Relacionado

- [reservas.md](reservas.md)
- [estados-recurso.md](../01-arquitectura/estados-recurso.md)
- [flujo-usuario.md](../09-flujos/flujo-usuario.md)
