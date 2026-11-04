---
tipo: estandar
estado: borrador
responsable: PENDIENTE
---

# Estándar de APIs

## Lo que exige el enunciado

- Cada microservicio tiene una API clara y contratos explícitos (§4.1).
- Contratos de APIs REST o equivalentes, mediante OpenAPI, README estructurado o colección de
  peticiones (§4.2).
- La documentación de APIs incluye endpoints, métodos, payloads y códigos de respuesta
  principales (§13.5).
- La rúbrica valora "APIs consistentes" (§16).
- Ampliación: contratos OpenAPI versionados (§15).

## Convenciones

> PENDIENTE: elegir el estilo de API (REST u otro) y el formato del contrato (OpenAPI, README o colección).

> PENDIENTE: definir las convenciones de rutas, nombres de recursos y versionado de la API.

> PENDIENTE: definir el formato común de errores y los códigos HTTP por tipo de error.

> PENDIENTE: definir la paginación y los filtros de las consultas.

> PENDIENTE: definir la autenticación en las llamadas (cabecera, formato del token) y la autorización por rol.

> PENDIENTE: definir la propagación del identificador de correlación en cabeceras.

> PENDIENTE: definir el endpoint de health check (§7.1, §9).

> PENDIENTE: definir la idempotencia de las operaciones de escritura sensibles (p. ej. crear reserva).

> PENDIENTE: decidir dónde viven los contratos en el repositorio y cómo se validan en el pipeline.

## Relacionado

- [02-servicios](../02-servicios/README.md)
- [errores-y-resiliencia.md](errores-y-resiliencia.md)
- [logs-y-observabilidad.md](logs-y-observabilidad.md)
