---
tipo: flujo
estado: borrador
responsable: PENDIENTE
---

# Flujo 2: Mantenimiento (§11.2)

## Pasos (enunciado)

| # | Paso | Componente responsable (§4.1, §4.3) | Evento del catálogo relacionado |
|---|---|---|---|
| 1 | El sistema detecta un recurso con batería baja o avería. | [Batería y telemetría](../02-servicios/bateria-y-telemetria.md), [Incidencias](../02-servicios/incidencias.md), [Detección de mantenimiento](../04-lambdas/deteccion-de-mantenimiento.md) | `VehicleBatteryLow` |
| 2 | Se genera una orden de mantenimiento. | [Detección de mantenimiento](../04-lambdas/deteccion-de-mantenimiento.md), [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) | — (no hay evento en el catálogo) |
| 3 | La app de mantenimiento retira el recurso. | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) | `VehicleWithdrawnForMaintenance` |
| 4 | Se registra recarga o reparación. | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) | — (no hay evento en el catálogo) |
| 5 | El recurso vuelve a estar disponible. | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) | `VehicleReturnedToService` |
| 6 | El historial y los data marts reflejan el cambio. | [Historial](../02-servicios/historial.md), [data marts](../05-datos/data-marts.md) | — |

## Diagrama de secuencia requerido (§4.2)

Cubre el diagrama obligatorio de **retirada por mantenimiento**.

> PENDIENTE: diagrama de secuencia de retirada por mantenimiento (hueco).

## Detalle técnico

> PENDIENTE: detallar quién detecta, quién crea la orden, las transiciones de estado (LOW_BATTERY, WITHDRAWN, CHARGING/REPAIRING, READY_FOR_SERVICE, AVAILABLE) y los eventos de cada paso.

## Guion de demostración

> PENDIENTE: definir cómo se provoca la batería baja o la avería, qué se muestra y qué data mart se consulta al final.

## Relacionado

- [estados-recurso.md](../01-arquitectura/estados-recurso.md)
- [apps-cliente.md](../01-arquitectura/apps-cliente.md)
