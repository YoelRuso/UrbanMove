---
tipo: servicio
estado: borrador
responsable: PENDIENTE
---

# Órdenes de mantenimiento

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | **Sí** ("mantenimiento") |

## 1. Responsabilidad

Gestiona la retirada, recarga, reparación, revisión, asignación y reincorporación de recursos.

## 2. Qué NO hace

- No registra la avería o el reporte original: [Incidencias](incidencias.md).
- No mide la batería: [Batería y telemetría](bateria-y-telemetria.md).
- No gestiona la redistribución entre zonas: [Órdenes de recolocación](ordenes-de-recolocacion.md).

## 3. Datos de los que es dueño

Orden de mantenimiento: recurso, tipo (retirada, recarga, reparación o revisión), asignación y
estado (abierta, en curso o completada, según el dashboard de §3.3).

> PENDIENTE: definir el modelo de datos y los estados formales de la orden.

## 4. API

> PENDIENTE: definir endpoints para retirar un recurso, registrar recarga, reparación o revisión, reincorporarlo y consultar órdenes.

## 5. Eventos que publica

Eventos del catálogo relacionados con esta responsabilidad: `VehicleWithdrawnForMaintenance`
("Recurso retirado por mantenimiento") y `VehicleReturnedToService` ("Recurso vuelve a estar
disponible").

> PENDIENTE: confirmar que este servicio publica ambos eventos y decidir si hacen falta eventos para recarga, reparación, `READY_FOR_SERVICE` y creación de orden.

## 6. Eventos que consume

> PENDIENTE: decidir si consume `VehicleBatteryLow` o un evento de incidencia para crear órdenes, o si las crea la Lambda de detección de mantenimiento.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias.

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

- Diagrama de secuencia obligatorio de "retirada por mantenimiento" (§4.2).
- Escenario de fallo de ejemplo: "error al procesar una orden de mantenimiento" (§7.1).

## 10. Relacionado

- [deteccion-de-mantenimiento.md](../04-lambdas/deteccion-de-mantenimiento.md)
- [estados-recurso.md](../01-arquitectura/estados-recurso.md)
- [flujo-mantenimiento.md](../09-flujos/flujo-mantenimiento.md)
