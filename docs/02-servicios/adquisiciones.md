---
tipo: servicio
estado: borrador
responsable: Joel
---

# Adquisiciones

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| No | No |

## 1. Responsabilidad

Registra la compra o incorporación de nuevos recursos y publica eventos para inventario y
analítica.

## 2. Qué NO hace

- No mantiene el registro de activos: [Inventario de recursos](inventario-de-recursos.md), que
  consume sus eventos.

## 3. Datos de los que es dueño

Adquisición: compra o incorporación de uno o varios recursos.

> PENDIENTE: definir el modelo de datos.

## 4. API

> PENDIENTE: definir endpoints para registrar una compra o incorporación (la usa la app de mantenimiento, §3.2).

## 5. Eventos que publica

| Evento | Cuándo |
|---|---|
| `VehiclePurchased` | Incorporación de una bicicleta o patinete nuevo. |

## 6. Eventos que consume

Ninguno indicado en el enunciado.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias.

## 8. Almacenamiento

PostgreSQL, con una base de datos propia ([acuerdos.md](../10-equipo/acuerdos.md)).

## 9. Decisiones y notas

- Consumidores de `VehiclePurchased` según §4.1: inventario y analítica.

> PENDIENTE: decidir si se implementa o si es candidato a fusión de bajo riesgo con Inventario (habría que justificarlo).

## 10. Relacionado

- [inventario-de-recursos.md](inventario-de-recursos.md)
- [03-eventos/README.md](../03-eventos/README.md)
