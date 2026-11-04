---
tipo: servicio
estado: borrador
responsable: PENDIENTE
---

# Analítica operacional

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | **Sí** ("analítica") |

## 1. Responsabilidad

Expone consultas agregadas de demanda, ocupación, disponibilidad y rendimiento operacional a
partir de data marts. Debe alimentar el dashboard o justificar qué indicadores se calculan en
otro componente.

## 2. Qué NO hace

- No construye los data marts: lo hace la Lambda de
  [Construcción de data marts](../04-lambdas/construccion-de-data-marts.md) u otro componente.
- No es una base de datos transaccional, y los microservicios no usan el Data Lake como tal (§8).
- No debe bloquear las operaciones principales de reserva, inicio o fin de viaje (§7.2).

## 3. Datos de los que es dueño

No queda claro si es dueño de los data marts o solo los lee.

> PENDIENTE: decidir si Analítica operacional es dueño de los data marts o solo los consulta.

## 4. API

> PENDIENTE: definir endpoints de consulta agregada para el dashboard (ver los indicadores en [apps-cliente.md](../01-arquitectura/apps-cliente.md)).

## 5. Eventos que publica

`DemandHotspotDetected` ("Zona con demanda superior a la disponibilidad") está relacionado con la
analítica de demanda.

> PENDIENTE: decidir si `DemandHotspotDetected` lo publica este servicio, la Lambda de recolocación u otro componente.

## 6. Eventos que consume

> PENDIENTE: decidir si consume eventos directamente o solo lee data marts.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias (data marts, métricas de servicios).

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de consulta sobre los data marts.

## 9. Decisiones y notas

- Pregunta de defensa: qué data mart se usa para decidir una recolocación (§18).

## 10. Relacionado

- [data-marts.md](../05-datos/data-marts.md)
- [apps-cliente.md](../01-arquitectura/apps-cliente.md)
- [flujo-dashboard.md](../09-flujos/flujo-dashboard.md)
