---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Aplicaciones cliente (§3)

Hay al menos tres interfaces diferenciadas. No hace falta una interfaz gráfica sofisticada:
valen apps web sencillas, APIs documentadas, colecciones de peticiones o clientes CLI. Lo
importante es que las responsabilidades estén separadas y que el dashboard muestre
información agregada real del sistema.

La columna "Servicio responsable" se deduce de las responsabilidades de §4.1. Los endpoints
concretos se definen en cada ficha.

## 1. App de usuarios finales (§3.1)

| Funcionalidad | Servicio responsable (§4.1) |
|---|---|
| Registrar o consultar un usuario | [Identidad](../02-servicios/identidad.md), [Perfiles de usuario](../02-servicios/perfiles-de-usuario.md) |
| Ver bicicletas o patinetes disponibles por zona | [Disponibilidad](../02-servicios/disponibilidad.md), [Catálogo de zonas](../02-servicios/catalogo-de-zonas.md) |
| Crear, confirmar o cancelar una reserva | [Reservas](../02-servicios/reservas.md) |
| Iniciar el uso de un recurso reservado o disponible | [Viajes](../02-servicios/viajes.md) |
| Finalizar el viaje indicando zona de destino | [Viajes](../02-servicios/viajes.md) |
| Consultar el historial personal de reservas y viajes | [Historial](../02-servicios/historial.md) |

## 2. App de mantenimiento y operaciones (§3.2)

| Funcionalidad | Servicio responsable (§4.1) |
|---|---|
| Consultar recursos con batería baja, avería o uso anómalo | [Batería y telemetría](../02-servicios/bateria-y-telemetria.md), [Incidencias](../02-servicios/incidencias.md) |
| Retirar un recurso de disponibilidad pública | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) |
| Registrar tareas de recarga, reparación o revisión | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) |
| Volver a poner un recurso en servicio | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) |
| Registrar la compra o incorporación de nuevos recursos | [Adquisiciones](../02-servicios/adquisiciones.md) |
| Consultar órdenes de recolocación generadas por el sistema | [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md) |
| Marcar una orden de recolocación como asignada, en curso o completada | [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md) |

## 3. Dashboard operativo (§3.3)

Permite consultar el estado global del sistema y apoyar decisiones operacionales. Se alimenta
de eventos, data marts, métricas de los microservicios o una combinación justificada de estas
fuentes. Como mínimo muestra:

| Indicador | Fuente |
|---|---|
| Recursos disponibles, reservados, en uso, en carga, en reparación y retirados | PENDIENTE |
| Reservas y viajes por franja horaria, zona y tipo de recurso | PENDIENTE |
| Zonas con déficit o exceso de bicicletas y patinetes | PENDIENTE |
| Órdenes de mantenimiento y recolocación abiertas, en curso y completadas | PENDIENTE |
| Salud del sistema: servicios activos, errores recientes o eventos fallidos | PENDIENTE |

Lo alimenta principalmente [Analítica operacional](../02-servicios/analitica-operacional.md),
o se justifica qué indicadores se calculan en otro componente (§4.1). Debe actualizarse
durante la demostración (§10).

## Decisiones abiertas

Las tres interfaces son apps web React separadas, creadas con Vite:

| App | Responsable |
|---|---|
| Usuarios finales | Oussama |
| Mantenimiento y operaciones | Joel |
| Dashboard operativo | Sergio |

En el sprint 1 se hacen versiones muy básicas para comprobar que todo funciona. En el sprint 3
se completan y se cuida el diseño (ver [acuerdos.md](../10-equipo/acuerdos.md)).

> PENDIENTE: decidir la fuente de cada indicador del dashboard (eventos, data marts, métricas o combinación) y justificarla.

> PENDIENTE: decidir cómo se autentican y se separan los roles de cada app (ver [identidad.md](../02-servicios/identidad.md)).

> PENDIENTE: decidir si las apps llaman directamente a los servicios o a través de un gateway o BFF.

## Relacionado

- [vision-general.md](vision-general.md)
- [09-flujos](../09-flujos/flujo-usuario.md)
