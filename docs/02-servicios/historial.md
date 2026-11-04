---
tipo: servicio
estado: borrador
responsable: Joel
---

# Historial

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí (y como microservicio independiente) | **Sí** |

## 1. Responsabilidad

Servicio independiente para consultar el histórico de reservas, viajes, incidencias,
mantenimiento y operaciones relevantes. No debe ser una tabla secundaria dentro de otro
microservicio.

## 2. Qué NO hace

- No es dueño de las reservas, los viajes ni las órdenes originales: solo mantiene su histórico
  consultable.
- No es el Data Lake ni los data marts (capa analítica separada, §8).

## 3. Datos de los que es dueño

Histórico consultable de reservas, viajes, incidencias, mantenimiento y operaciones relevantes.

> PENDIENTE: definir el modelo de datos del histórico.

## 4. API

> PENDIENTE: definir endpoints de consulta, incluido el historial personal de reservas y viajes de un usuario (§3.1).

## 5. Eventos que publica

> PENDIENTE: decidir si publica algún evento.

## 6. Eventos que consume

Los eventos de dominio alimentan el historial (§6).

> PENDIENTE: decidir qué eventos del catálogo consume.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias.

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

- Escenario de fallo de ejemplo: "caída del servicio de historial" (§7.1). Su caída no debe
  romper reservas ni viajes.
- Flujo de usuario: "Se genera historial" (§11.1). Flujo de mantenimiento: "El historial y los
  data marts reflejan el cambio" (§11.2).
- Ejemplo de carpeta de repositorio: `services/history` (§10).

> PENDIENTE: decidir cómo se recupera el historial tras una caída (reprocesado de eventos, DLQ...).

## 10. Relacionado

- [03-eventos/README.md](../03-eventos/README.md)
- [flujo-fallo-controlado.md](../09-flujos/flujo-fallo-controlado.md)
