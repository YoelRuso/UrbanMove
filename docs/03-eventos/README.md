---
tipo: evento
estado: borrador
responsable: PENDIENTE
---

# Catálogo de eventos de dominio (§6)

La arquitectura emite eventos de dominio. Alimentan procesos asíncronos, Lambdas, el
historial, el Data Lake y los data marts. Todos los eventos llevan el
[sobre común](sobre-comun.md). Las normas de diseño y versionado están en
[06-estandares/eventos.md](../06-estandares/eventos.md).

La documentación de eventos del entregable debe incluir **nombre, productor, consumidores y
esquema mínimo** (§13.6).

| Evento | Uso esperado (§6) | Productor | Consumidores | Esquema (payload) |
|---|---|---|---|---|
| `UserRegistered` | Alta de usuario y creación de perfil. | PENDIENTE | PENDIENTE | PENDIENTE |
| `VehiclePurchased` | Incorporación de una bicicleta o patinete nuevo. | [Adquisiciones](../02-servicios/adquisiciones.md) (§4.1) | [Inventario](../02-servicios/inventario-de-recursos.md), analítica (§4.1); resto PENDIENTE | PENDIENTE |
| `VehicleReserved` | Reserva creada sobre un recurso disponible. | PENDIENTE | PENDIENTE | PENDIENTE |
| `ReservationCancelled` | Reserva cancelada por el usuario. | PENDIENTE | PENDIENTE | PENDIENTE |
| `ReservationExpired` | Reserva liberada automáticamente por timeout. | PENDIENTE | PENDIENTE | PENDIENTE |
| `RideStarted` | Inicio de uso de un recurso. | PENDIENTE | PENDIENTE | PENDIENTE |
| `RideFinished` | Finalización del viaje y liberación o cambio de estado del recurso. | PENDIENTE | PENDIENTE | PENDIENTE |
| `VehicleBatteryLow` | Detección de batería baja. | PENDIENTE | PENDIENTE | PENDIENTE |
| `VehicleWithdrawnForMaintenance` | Recurso retirado por mantenimiento. | PENDIENTE | PENDIENTE | PENDIENTE |
| `VehicleReturnedToService` | Recurso vuelve a estar disponible. | PENDIENTE | PENDIENTE | PENDIENTE |
| `DemandHotspotDetected` | Zona con demanda superior a la disponibilidad. | PENDIENTE | PENDIENTE | PENDIENTE |
| `RelocationOrderCreated` | Orden creada para mover recursos entre zonas. | PENDIENTE | PENDIENTE | PENDIENTE |
| `RelocationOrderCompleted` | Orden completada por el equipo de mantenimiento. | PENDIENTE | PENDIENTE | PENDIENTE |

Las fichas de servicio y de Lambda indican los productores **candidatos** de cada evento. Al
decidirlo, se actualiza esta tabla y la ficha correspondiente en el mismo cambio.

> PENDIENTE: decidir el productor y los consumidores de cada evento (salvo `VehiclePurchased`, cuyo productor es explícito).

> PENDIENTE: definir el payload mínimo de cada evento.

> PENDIENTE: decidir el formato del contrato (tabla, JSON Schema, AsyncAPI o equivalente, §4.2) y dónde vive en el repositorio.

El bus es SNS + SQS: un tópico por dominio productor y una cola con DLQ por consumidor (ver
[ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)).

> PENDIENTE: fijar el nombre de cada tópico y de cada cola.

## Eventos que faltan en el catálogo del enunciado

El catálogo de §6 no cubre algunas situaciones que el enunciado sí describe:

- Confirmación de reserva (§3.1, §4.3).
- Creación y cambios de estado de órdenes de mantenimiento (§3.2, §11.2).
- Incidencias registradas (§4.1).
- Transiciones a `CHARGING`, `REPAIRING`, `READY_FOR_SERVICE` y `RETIRED` (§5).
- Estados asignada y en curso de las órdenes de recolocación (§3.2).
- Baja lógica de un perfil (§4.1).

> PENDIENTE: decidir qué eventos adicionales se crean. Si se crea alguno, añadirlo a esta tabla.

## Relacionado

- [sobre-comun.md](sobre-comun.md)
- [estados-recurso.md](../01-arquitectura/estados-recurso.md)
- [ingesta-analitica.md](../04-lambdas/ingesta-analitica.md)
