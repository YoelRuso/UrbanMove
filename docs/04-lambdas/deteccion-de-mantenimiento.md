---
tipo: lambda
estado: borrador
responsable: PENDIENTE
---

# Lambda: Detección de mantenimiento

**Obligatoria:** PENDIENTE (ver [README](README.md)).

## Qué hace (§4.3)

Genera una orden cuando un recurso queda con batería baja, avería o demasiados usos desde la
última revisión.

## Disparador

> PENDIENTE: decidir el disparador (eventos de telemetría, `VehicleBatteryLow`, `RideFinished`, incidencias, ejecución programada...).

## Entrada

> PENDIENTE: definir los eventos o datos de entrada.

## Salida y efectos

Crea una orden de mantenimiento ([Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md)).

> PENDIENTE: decidir si crea la orden por API o publicando un evento, y si publica `VehicleBatteryLow`.

## Parámetros

> PENDIENTE: fijar los umbrales de batería baja y de "demasiados usos desde la última revisión".

## Idempotencia y errores

> PENDIENTE: definir cómo se evita crear órdenes duplicadas para el mismo recurso.

## Notas

- Es el paso 1-2 del [flujo de mantenimiento](../09-flujos/flujo-mantenimiento.md): "El sistema
  detecta un recurso con batería baja o avería" y "Se genera una orden de mantenimiento".

## Relacionado

- [bateria-y-telemetria.md](../02-servicios/bateria-y-telemetria.md)
- [incidencias.md](../02-servicios/incidencias.md)
