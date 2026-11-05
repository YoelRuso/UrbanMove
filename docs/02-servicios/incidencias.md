---
tipo: servicio
estado: borrador
responsable: Joel
---

# Incidencias

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| No | No |

## 1. Responsabilidad

Registra averías, vandalismo, bloqueos, recursos desaparecidos o incidencias reportadas por
usuarios y mantenimiento.

## 2. Qué NO hace

- No gestiona la retirada ni la reparación: [Órdenes de mantenimiento](ordenes-de-mantenimiento.md).

## 3. Datos de los que es dueño

Incidencia: tipo (avería, vandalismo, bloqueo, desaparecido u otra), recurso, quién la reporta
(usuario o mantenimiento) y estado.

> PENDIENTE: definir el modelo de datos y los estados de una incidencia.

## 4. API

> PENDIENTE: definir endpoints para reportar y consultar incidencias.

## 5. Eventos que publica

El catálogo de §6 no incluye ningún evento de incidencias.

> PENDIENTE: decidir si se añade un evento de incidencia (necesario, por ejemplo, para que Historial y la detección de mantenimiento la conozcan).

## 6. Eventos que consume

> PENDIENTE: definir si consume algún evento.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias.

## 8. Almacenamiento

PostgreSQL, con una base de datos propia ([acuerdos.md](../10-equipo/acuerdos.md)).

## 9. Decisiones y notas

- Historial debe permitir consultar las incidencias (§4.1).
- La app de mantenimiento consulta recursos con avería o uso anómalo (§3.2).

> PENDIENTE: decidir si se implementa.

## 10. Relacionado

- [ordenes-de-mantenimiento.md](ordenes-de-mantenimiento.md)
- [historial.md](historial.md)
