---
tipo: servicio
estado: borrador
responsable: Joel
---

# Batería y telemetría

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| No | No |

## 1. Responsabilidad

Recibe o simula nivel de batería, última ubicación, kilómetros o número de usos desde la última
revisión.

## 2. Qué NO hace

- No genera órdenes de mantenimiento: lo hace la Lambda de
  [Detección de mantenimiento](../04-lambdas/deteccion-de-mantenimiento.md) o
  [Órdenes de mantenimiento](ordenes-de-mantenimiento.md).
- No registra averías reportadas: [Incidencias](incidencias.md).

## 3. Datos de los que es dueño

Nivel de batería, última ubicación, kilómetros y número de usos desde la última revisión.

> PENDIENTE: definir el modelo de datos y la frecuencia de simulación.

## 4. API

> PENDIENTE: definir endpoints de ingesta o simulación de telemetría y de consulta (p. ej. recursos con batería baja, que pide la app de mantenimiento, §3.2).

## 5. Eventos que publica

`VehicleBatteryLow` ("Detección de batería baja") está relacionado con este servicio.

> PENDIENTE: decidir si `VehicleBatteryLow` lo publica este servicio o la Lambda de detección de mantenimiento.

## 6. Eventos que consume

> PENDIENTE: decidir si consume `RideFinished` u otros eventos para contar usos y kilómetros.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias.

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

- El flujo de mantenimiento empieza cuando "el sistema detecta un recurso con batería baja o
  avería" (§11.2).

> PENDIENTE: decidir si se implementa o si la telemetría se simula dentro de otro componente.

## 10. Relacionado

- [deteccion-de-mantenimiento.md](../04-lambdas/deteccion-de-mantenimiento.md)
- [flujo-mantenimiento.md](../09-flujos/flujo-mantenimiento.md)
