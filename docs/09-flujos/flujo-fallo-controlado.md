---
tipo: flujo
estado: borrador
responsable: PENDIENTE
---

# Flujo 5: Fallo controlado (§11.5)

## Pasos (enunciado)

| # | Paso |
|---|---|
| 1 | Se provoca o simula la indisponibilidad temporal de un componente no crítico. |
| 2 | El sistema registra el error con identificador de correlación. |
| 3 | Los eventos críticos no se pierden. |
| 4 | El sistema se recupera o permite reprocesar el evento. |
| 5 | El grupo explica qué parte de la arquitectura evita que el fallo se propague. |

Ejemplos de escenario del enunciado (§7.1): caída del servicio de historial, error al procesar
una orden de mantenimiento, o fallo temporal de la Lambda que actualiza data marts.

## Decisiones

> PENDIENTE: elegir el componente no crítico que se tumba en la demo.

> PENDIENTE: describir los mecanismos que lo protegen (cola, DLQ, reintentos, idempotencia...). Ver [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md).

> PENDIENTE: definir cómo se demuestra que no se pierden eventos y cómo se reprocesan.

## Guion de demostración

> PENDIENTE: escribir los comandos para provocar el fallo y recuperarse, y qué logs o métricas se muestran.

## Relacionado

- [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md)
- [logs-y-observabilidad.md](../06-estandares/logs-y-observabilidad.md)
- [historial.md](../02-servicios/historial.md)
