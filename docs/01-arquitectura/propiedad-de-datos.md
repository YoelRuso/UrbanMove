---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Propiedad de datos

El enunciado exige una tabla que diga qué servicio es dueño de cada entidad o tabla principal
(§4.2). Cada microservicio con estado tiene su propia base de datos o almacenamiento (§4.1).
Ningún servicio escribe en los datos de otro.

La tabla recoge las entidades que se desprenden de la responsabilidad de cada servicio en
§4.1. Los nombres de tablas y los modelos concretos son decisión del equipo.

| Entidad | Servicio dueño | Base en el enunciado | Tabla / almacén |
|---|---|---|---|
| Credenciales, sesiones, tokens, roles | [Identidad](../02-servicios/identidad.md) | §4.1 | PENDIENTE |
| Datos de usuario y preferencias | [Perfiles de usuario](../02-servicios/perfiles-de-usuario.md) | §4.1 | PENDIENTE |
| Zonas, restricciones de aparcamiento, áreas de operación, metadatos geográficos | [Catálogo de zonas](../02-servicios/catalogo-de-zonas.md) | §4.1 | PENDIENTE |
| Activo (identificador, tipo, fecha de compra, modelo, estado administrativo) | [Inventario de recursos](../02-servicios/inventario-de-recursos.md) | §4.1 | PENDIENTE |
| Qué recursos pueden reservarse en cada momento | [Disponibilidad](../02-servicios/disponibilidad.md) | §4.1 | PENDIENTE |
| Batería, última ubicación, kilómetros y usos desde la última revisión | [Batería y telemetría](../02-servicios/bateria-y-telemetria.md) | §4.1 | PENDIENTE |
| Reserva | [Reservas](../02-servicios/reservas.md) | §4.1 | PENDIENTE |
| Viaje (inicio, fin, duración, zonas de origen y destino, coste preliminar) | [Viajes](../02-servicios/viajes.md) | §4.1 | PENDIENTE |
| Incidencia | [Incidencias](../02-servicios/incidencias.md) | §4.1 | PENDIENTE |
| Orden de mantenimiento | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) | §4.1 | PENDIENTE |
| Orden de recolocación | [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md) | §4.1 | PENDIENTE |
| Adquisición (compra o incorporación) | [Adquisiciones](../02-servicios/adquisiciones.md) | §4.1 | PENDIENTE |
| Histórico consultable de reservas, viajes, incidencias, mantenimiento y operaciones | [Historial](../02-servicios/historial.md) | §4.1 | PENDIENTE |
| Avisos enviados o simulados | [Notificaciones](../02-servicios/notificaciones.md) | §4.1 | PENDIENTE |
| Eventos raw/trusted/curated | Capa analítica ([Data Lake](../05-datos/data-lake.md)) | §8.1 | PENDIENTE |
| Data marts | Capa analítica ([data-marts.md](../05-datos/data-marts.md)) | §8.2 | PENDIENTE |

> PENDIENTE: decidir qué servicio es dueño del **estado operativo del recurso** (AVAILABLE, RESERVED, IN_USE...). El enunciado reparte información sobre el recurso entre Inventario ("estado administrativo"), Disponibilidad ("qué recursos pueden reservarse") y Órdenes de mantenimiento, sin decir cuál manda. Ver [estados-recurso.md](estados-recurso.md).

Cada servicio con estado tiene su propia base de datos PostgreSQL y un usuario que solo tiene
permisos sobre ella, dentro de una instancia RDS compartida
([ADR 0003](../08-adr/0003-una-instancia-rds-con-una-base-de-datos-por-servicio.md)).

> PENDIENTE: completar la columna "Tabla / almacén" con el nombre de la base de datos y las tablas principales de cada servicio.

> PENDIENTE: decidir qué copias locales (proyecciones) de datos ajenos mantiene cada servicio, alimentadas por eventos.

## Relacionado

- [vision-general.md](vision-general.md)
- [02-servicios](../02-servicios/README.md)
