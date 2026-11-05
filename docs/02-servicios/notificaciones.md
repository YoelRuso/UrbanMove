---
tipo: servicio
estado: borrador
responsable: Joel
---

# Notificaciones

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| No | No |

## 1. Responsabilidad

Envía o simula avisos a usuarios, mantenimiento u operaciones ante reservas, incidencias,
órdenes o errores recuperables.

## 2. Qué NO hace

- No genera reservas, incidencias ni órdenes: solo avisa cuando ocurren.

## 3. Datos de los que es dueño

Avisos enviados o simulados.

> PENDIENTE: definir el modelo de datos, o decidir si no persiste nada.

## 4. API

> PENDIENTE: definir si expone API (p. ej. consulta de avisos) o es solo consumidor de eventos.

## 5. Eventos que publica

> PENDIENTE: decidir si publica algún evento.

## 6. Eventos que consume

> PENDIENTE: decidir qué eventos de reservas, incidencias y órdenes consume, y qué es un "error recuperable" notificable.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias y el canal de envío simulado.

## 8. Almacenamiento

PostgreSQL con una base de datos propia, si persiste avisos ([acuerdos.md](../10-equipo/acuerdos.md)). Ver la sección 3.

## 9. Decisiones y notas

- Es un candidato natural a "componente no crítico" para el flujo de fallo controlado (§11.5).

> PENDIENTE: decidir si se implementa.

## 10. Relacionado

- [03-eventos/README.md](../03-eventos/README.md)
- [flujo-fallo-controlado.md](../09-flujos/flujo-fallo-controlado.md)
