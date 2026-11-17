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

Reparto acordado por el grupo el 17 de noviembre de 2026. Sustituye al reparto inicial de la
reunión del 27 de octubre, que solo cubría los servicios para empezar a probar.

| | Joel | Oussama | Sergio |
|---|---|---|---|
| Obligatorios (§14) | [Reservas](../02-servicios/reservas.md), [Viajes](../02-servicios/viajes.md), [Disponibilidad](../02-servicios/disponibilidad.md), [Inventario](../02-servicios/inventario-de-recursos.md) | [Identidad](../02-servicios/identidad.md), [Mantenimiento](../02-servicios/ordenes-de-mantenimiento.md), [Recolocación](../02-servicios/ordenes-de-recolocacion.md) | [Historial](../02-servicios/historial.md), [Analítica](../02-servicios/analitica-operacional.md), [Perfiles](../02-servicios/perfiles-de-usuario.md) |
| Opcionales | [Zonas](../02-servicios/catalogo-de-zonas.md) | [Incidencias](../02-servicios/incidencias.md), [Adquisiciones](../02-servicios/adquisiciones.md) | [Telemetría](../02-servicios/bateria-y-telemetria.md), [Notificaciones](../02-servicios/notificaciones.md) |
| Total de microservicios | 5 | 5 | 5 |
| Lambdas | [Expiración](../04-lambdas/expiracion-de-reservas.md), [Ingesta](../04-lambdas/ingesta-analitica.md) | [Detección](../04-lambdas/deteccion-de-mantenimiento.md), [Recolocación](../04-lambdas/recolocacion.md) | [Data marts](../04-lambdas/construccion-de-data-marts.md) |
| Interfaz | App de usuarios | App de mantenimiento | Dashboard |
| Datos | [Data Lake](../05-datos/data-lake.md) | | [Data marts](../05-datos/data-marts.md) |

Cada responsable de un servicio decide sus detalles; lo que afecta a varios servicios lo decide
el grupo (ver [acuerdos.md](acuerdos.md)).

### Tareas conjuntas

CI/CD, Terraform y despliegue, bus de eventos, observabilidad e informe no tienen responsable
fijo: se reparten rotando según vayan haciendo falta, para que todos toquen un poco de todo.
