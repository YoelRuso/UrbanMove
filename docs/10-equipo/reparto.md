---
tipo: equipo
estado: borrador
responsable: PENDIENTE
---

# Reparto de trabajo (§12)

El reparto debe estar equilibrado. Todos los miembros participan en la implementación, la
documentación y la defensa, y el reparto se documenta en el informe final (§1, §12).

## Reparto orientativo del enunciado

| Persona | Responsabilidades orientativas |
|---|---|
| A | App de usuarios, [Identidad](../02-servicios/identidad.md), [Perfiles](../02-servicios/perfiles-de-usuario.md), [Reservas](../02-servicios/reservas.md), [Viajes](../02-servicios/viajes.md) y pruebas asociadas. |
| B | App de mantenimiento, [Inventario](../02-servicios/inventario-de-recursos.md), [Disponibilidad](../02-servicios/disponibilidad.md), [Incidencias](../02-servicios/incidencias.md), [Mantenimiento](../02-servicios/ordenes-de-mantenimiento.md), [Recolocación](../02-servicios/ordenes-de-recolocacion.md) y Lambdas asociadas. |
| C (grupos de tres) | [Historial](../02-servicios/historial.md), [Data Lake](../05-datos/data-lake.md), [data marts](../05-datos/data-marts.md), [Analítica operacional](../02-servicios/analitica-operacional.md) y dashboard. |
| Conjunto | Arquitectura, contratos, eventos, CI/CD, despliegue, pruebas, observabilidad, informe y defensa. |

El reparto orientativo no asigna Catálogo de zonas, Batería y telemetría, Adquisiciones ni
Notificaciones.

## Reparto real

Reparto inicial acordado en la reunión del 27 de octubre de 2026. Solo cubre los servicios
para empezar a probar; el resto se repartirá más adelante.

| Miembro | Servicios iniciales | Interfaz | Opcionales | Lambdas | Otros |
|---|---|---|---|---|---|
| Joel | [Historial](../02-servicios/historial.md), [Reservas](../02-servicios/reservas.md) | App de mantenimiento y operaciones | [Catálogo de zonas](../02-servicios/catalogo-de-zonas.md), [Batería y telemetría](../02-servicios/bateria-y-telemetria.md), [Incidencias](../02-servicios/incidencias.md), [Adquisiciones](../02-servicios/adquisiciones.md), [Notificaciones](../02-servicios/notificaciones.md) | PENDIENTE | Lo más complejo, cuando se reparta |
| Oussama | [Identidad](../02-servicios/identidad.md), [Perfiles de usuario](../02-servicios/perfiles-de-usuario.md) | App de usuarios finales | — | PENDIENTE | PENDIENTE |
| Sergio | [Viajes](../02-servicios/viajes.md), [Disponibilidad](../02-servicios/disponibilidad.md) | Dashboard operativo | — | PENDIENTE | PENDIENTE |

### Pendiente de repartir

Obligatorios (§14) sin responsable todavía:

- [Inventario de recursos](../02-servicios/inventario-de-recursos.md)
- [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md)
- [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md)
- [Analítica operacional](../02-servicios/analitica-operacional.md)

Piezas no asociadas a un servicio:

- [Lambdas](../04-lambdas/README.md) (al menos tres).
- [Data Lake](../05-datos/data-lake.md) y [data marts](../05-datos/data-marts.md) (al menos
  cuatro).
- Tareas conjuntas: bus de eventos, Terraform y despliegue, CI/CD, observabilidad e informe.
  Se repartirán de forma equitativa.

Criterio acordado: Joel se encarga de las piezas más complejas y el resto se reparte entre
Oussama y Sergio.

> PENDIENTE: asignar los cuatro servicios obligatorios restantes, las Lambdas y los data marts.

> PENDIENTE: repartir las tareas conjuntas con un responsable principal cada una.

> PENDIENTE: revisar que el reparto final quede equilibrado (§12, rúbrica): con los cinco opcionales y las piezas complejas, Joel acumula mucha más carga que los demás.

> PENDIENTE: actualizar el campo `responsable` del frontmatter de cada fichero del vault.
