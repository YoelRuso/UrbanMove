---
tipo: flujo
estado: borrador
responsable: PENDIENTE
---

# Flujo 3: Analítica y recolocación (§11.3)

## Pasos (enunciado)

| # | Paso | Componente responsable | Evento del catálogo relacionado |
|---|---|---|---|
| 1 | Se simulan viajes o reservas en varias zonas. | [Reservas](../02-servicios/reservas.md), [Viajes](../02-servicios/viajes.md) | `VehicleReserved`, `RideStarted`, `RideFinished` |
| 2 | Los eventos se almacenan en el Data Lake. | [Ingesta analítica](../04-lambdas/ingesta-analitica.md), [Data Lake](../05-datos/data-lake.md) | — |
| 3 | Se actualiza al menos un data mart de demanda. | [Construcción de data marts](../04-lambdas/construccion-de-data-marts.md) | — |
| 4 | El sistema detecta déficit de recursos en una zona. | PENDIENTE | `DemandHotspotDetected` |
| 5 | Se crea una orden de recolocación. | [Recolocación](../04-lambdas/recolocacion.md), [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md) | `RelocationOrderCreated` |
| 6 | La app de mantenimiento consulta y completa la orden. | [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md) | `RelocationOrderCompleted` |

## Diagrama de secuencia requerido (§4.2)

Cubre el diagrama obligatorio de **recolocación**.

> PENDIENTE: diagrama de secuencia de recolocación (hueco).

## Detalle técnico

> PENDIENTE: decidir qué componente detecta el déficit (paso 4) y con qué regla (ver [recolocacion.md](../04-lambdas/recolocacion.md)).

> PENDIENTE: decidir cómo se simulan los viajes y las reservas (script, generador de carga...).

## Guion de demostración

> PENDIENTE: definir el escenario (zonas, cantidades) que dispara la regla durante la demo.

## Relacionado

- [data-marts.md](../05-datos/data-marts.md)
- [requisitos-minimos.md](../00-proyecto/requisitos-minimos.md)
