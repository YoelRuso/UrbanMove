---
tipo: flujo
estado: borrador
responsable: PENDIENTE
---

# Flujo 1: Usuario (§11.1)

Primero de los cinco flujos obligatorios de la demostración.

## Pasos (enunciado)

| # | Paso | Servicio responsable (§4.1) | Evento del catálogo relacionado |
|---|---|---|---|
| 1 | El usuario se registra o inicia sesión. | [Identidad](../02-servicios/identidad.md), [Perfiles](../02-servicios/perfiles-de-usuario.md) | `UserRegistered` (en el registro) |
| 2 | Consulta bicicletas o patinetes disponibles en una zona. | [Disponibilidad](../02-servicios/disponibilidad.md) | — |
| 3 | Reserva un recurso. | [Reservas](../02-servicios/reservas.md) | `VehicleReserved` |
| 4 | Inicia el viaje. | [Viajes](../02-servicios/viajes.md) | `RideStarted` |
| 5 | Finaliza el viaje en otra zona. | [Viajes](../02-servicios/viajes.md) | `RideFinished` |
| 6 | Se genera historial y eventos para el Data Lake. | [Historial](../02-servicios/historial.md), [Ingesta analítica](../04-lambdas/ingesta-analitica.md) | — |

## Diagramas de secuencia requeridos (§4.2)

Este flujo cubre dos de los diagramas obligatorios: **reserva** e **inicio de viaje**.

> PENDIENTE: diagrama de secuencia de reserva (hueco).

> PENDIENTE: diagrama de secuencia de inicio de viaje (hueco).

## Detalle técnico

> PENDIENTE: detallar las llamadas síncronas, los eventos publicados y consumidos, y las transiciones de estado de cada paso.

## Guion de demostración

> PENDIENTE: definir los datos de partida, los comandos o pantallas y qué se enseña como evidencia (logs con correlación, eventos, Data Lake).

## Relacionado

- [apps-cliente.md](../01-arquitectura/apps-cliente.md)
- [estados-recurso.md](../01-arquitectura/estados-recurso.md)
