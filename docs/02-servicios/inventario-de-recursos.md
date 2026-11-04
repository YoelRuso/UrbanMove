---
tipo: servicio
estado: borrador
responsable: PENDIENTE
---

# Inventario de recursos

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | No |

## 1. Responsabilidad

Registra bicicletas y patinetes como activos: identificador, tipo, fecha de compra, modelo y
estado administrativo.

## 2. Qué NO hace

- No decide qué recursos pueden reservarse: eso es de [Disponibilidad](disponibilidad.md),
  que existe precisamente para "evitar mezclar inventario, reservas y mantenimiento".
- No registra la compra: [Adquisiciones](adquisiciones.md) la registra y publica eventos
  para inventario.
- No gestiona telemetría: eso es de [Batería y telemetría](bateria-y-telemetria.md).

## 3. Datos de los que es dueño

Activo: identificador, tipo (bicicleta o patinete), fecha de compra, modelo y estado
administrativo.

> PENDIENTE: definir los valores del "estado administrativo" y su relación con los estados de [estados-recurso.md](../01-arquitectura/estados-recurso.md).

## 4. API

> PENDIENTE: definir endpoints de consulta y alta de activos.

## 5. Eventos que publica

> PENDIENTE: decidir si publica eventos (p. ej. al dar de baja un recurso, `RETIRED`).

## 6. Eventos que consume

| Evento | Para qué |
|---|---|
| `VehiclePurchased` | Incorporar un recurso nuevo. Adquisiciones "publica eventos para inventario" (§4.1). |

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias.

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

> PENDIENTE: decidir si Inventario es el dueño del estado `RETIRED` (baja definitiva).

## 10. Relacionado

- [adquisiciones.md](adquisiciones.md)
- [disponibilidad.md](disponibilidad.md)
- [propiedad-de-datos.md](../01-arquitectura/propiedad-de-datos.md)
