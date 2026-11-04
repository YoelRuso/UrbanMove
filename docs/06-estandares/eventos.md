---
tipo: estandar
estado: borrador
responsable: PENDIENTE
---

# Estándar de eventos

El catálogo está en [03-eventos/README.md](../03-eventos/README.md) y el sobre en
[sobre-comun.md](../03-eventos/sobre-comun.md). Este fichero recoge las **normas** para
diseñar, publicar y consumir eventos.

## Lo que exige el enunciado

- Eventos de dominio bien definidos y consumidores asíncronos (§16).
- Sobre con identificador, timestamp, origen, tipo, versión de esquema y correlación (§6).
- Contratos mediante tabla, JSON Schema, AsyncAPI o equivalente (§4.2). AsyncAPI versionado es
  una ampliación (§15).
- Nombres de eventos en inglés y en pasado, como en el catálogo (`VehicleReserved`, `RideStarted`...).
- Evidencia de eventos enviados y consumidos (§10).

## Normas

> PENDIENTE: definir la convención de nombres para eventos nuevos.

> PENDIENTE: definir la política de versionado de esquemas (cuándo sube la versión y cómo conviven versiones).

Según el [ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md):

- **Entrega al menos una vez.** Todo consumidor es idempotente: guarda el `eventId` y descarta
  los repetidos.
- **Outbox transaccional.** El productor guarda el evento en su base de datos, en la misma
  transacción que el cambio de estado, y lo publica después.
- **Una DLQ por cola de consumidor.** Los mensajes que fallan repetidamente pasan a la DLQ.

> PENDIENTE: fijar el número de reintentos antes de la DLQ y el procedimiento para reprocesarla (ver [errores-y-resiliencia.md](errores-y-resiliencia.md)).

> PENDIENTE: definir el orden de los eventos y si se necesita garantizarlo por recurso.

## Procedimiento para añadir un evento

1. Añadir una fila al [catálogo](../03-eventos/README.md) con productor, consumidores y esquema.
2. Actualizar las fichas del productor y de los consumidores.
3. Si cambia un estado del recurso, actualizar [estados-recurso.md](../01-arquitectura/estados-recurso.md).
4. Comprobar que la [ingesta analítica](../04-lambdas/ingesta-analitica.md) lo trata.
