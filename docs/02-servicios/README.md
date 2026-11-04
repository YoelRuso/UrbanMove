---
tipo: servicio
estado: borrador
responsable: PENDIENTE
---

# Microservicios

El enunciado describe 15 microservicios atómicos (§4.1). Hay que implementar **al menos
diez**, entre ellos los diez obligatorios de §14. Se valora que cada microservicio sea
atómico: una API clara, una base de datos o almacenamiento propio cuando tenga estado,
despliegue independiente y contratos explícitos.

**Fusiones (§4.1):** se permite fusionar dos servicios de bajo riesgo si se justifica en el
PDF, pero **no se pueden fusionar** reservas, viajes, historial, mantenimiento ni analítica.

| Servicio | Obligatorio (§14) | Fusión prohibida | Responsabilidad resumida | Ficha |
|---|---|---|---|---|
| Identidad | Sí | No | Autenticación, sesiones, tokens y roles | [identidad.md](identidad.md) |
| Perfiles de usuario | Sí | No | Datos de usuario, preferencias, validación y baja lógica | [perfiles-de-usuario.md](perfiles-de-usuario.md) |
| Catálogo de zonas | No | No | Zonas permitidas, aparcamiento, áreas de operación | [catalogo-de-zonas.md](catalogo-de-zonas.md) |
| Inventario de recursos | Sí | No | Registro de recursos como activos | [inventario-de-recursos.md](inventario-de-recursos.md) |
| Disponibilidad | Sí | No | Qué recursos pueden reservarse en cada momento | [disponibilidad.md](disponibilidad.md) |
| Batería y telemetría | No | No | Batería, ubicación, km y usos desde la última revisión | [bateria-y-telemetria.md](bateria-y-telemetria.md) |
| Reservas | Sí | **Sí** | Crear, confirmar, cancelar y expirar reservas | [reservas.md](reservas.md) |
| Viajes | Sí | **Sí** | Inicio y fin de uso, duración, zonas y coste preliminar | [viajes.md](viajes.md) |
| Incidencias | No | No | Averías, vandalismo, bloqueos, desaparecidos | [incidencias.md](incidencias.md) |
| Órdenes de mantenimiento | Sí | **Sí** | Retirada, recarga, reparación, revisión y reincorporación | [ordenes-de-mantenimiento.md](ordenes-de-mantenimiento.md) |
| Órdenes de recolocación | Sí | No | Redistribución de recursos entre zonas | [ordenes-de-recolocacion.md](ordenes-de-recolocacion.md) |
| Adquisiciones | No | No | Compra o incorporación de recursos | [adquisiciones.md](adquisiciones.md) |
| Historial | Sí | **Sí** | Consulta de histórico, como servicio independiente | [historial.md](historial.md) |
| Notificaciones | No | No | Avisos a usuarios, mantenimiento u operaciones | [notificaciones.md](notificaciones.md) |
| Analítica operacional | Sí | **Sí** | Consultas agregadas sobre data marts para el dashboard | [analitica-operacional.md](analitica-operacional.md) |

Los diez obligatorios ya cumplen el mínimo de diez microservicios.

Se implementan también los cinco servicios no obligatorios (Catálogo de zonas, Batería y
telemetría, Incidencias, Adquisiciones y Notificaciones), previstos para el sprint 4. Ver
[reparto.md](../10-equipo/reparto.md).

> PENDIENTE: decidir si se fusiona algún par de servicios de bajo riesgo y justificarlo en un ADR.

> PENDIENTE: elegir los dos microservicios críticos que tendrán vista de componentes en el PDF (el enunciado sugiere reservas y viajes, §4.2).

Para crear una ficha nueva se copia [_plantilla.md](_plantilla.md).
