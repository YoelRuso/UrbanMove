---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Rúbrica (§16)

| Criterio | Peso | Descripción | Dónde se trabaja |
|---|---|---|---|
| Arquitectura | 16 % | Separación clara entre apps, microservicios atómicos, Lambdas, eventos, Data Lake y data marts. Coherencia de responsabilidades, datos propios y contratos. | [01-arquitectura](../01-arquitectura/vision-general.md), [propiedad-de-datos.md](../01-arquitectura/propiedad-de-datos.md) |
| Implementación | 16 % | Servicios funcionales, APIs consistentes, gestión correcta de estados, persistencia y empaquetado reproducible. | [02-servicios](../02-servicios/README.md), [api.md](../06-estandares/api.md), [estados-recurso.md](../01-arquitectura/estados-recurso.md) |
| Eventos y serverless | 12 % | Eventos de dominio bien definidos, consumidores asíncronos, Lambdas integradas y trazabilidad de flujos. | [03-eventos](../03-eventos/README.md), [04-lambdas](../04-lambdas/README.md) |
| Capa analítica | 14 % | Data Lake de eventos, data marts útiles, indicadores de demanda, dashboard operativo y generación razonada de órdenes de recolocación. | [data-lake.md](../05-datos/data-lake.md), [data-marts.md](../05-datos/data-marts.md) |
| Tolerancia a fallos | 10 % | Reintentos, colas, idempotencia, DLQ, degradación funcional y escenarios de fallo probados o simulados. | [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md) |
| Escalabilidad | 9 % | Escalado horizontal, procesamiento paralelo, particionado de datos y separación entre operación y analítica. | [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md), [data-lake.md](../05-datos/data-lake.md) |
| DevOps y despliegue | 10 % | CI/CD, pruebas automáticas, construcción de imágenes o artefactos, despliegue reproducible e infraestructura versionada. | [07-devops](../07-devops/pipeline.md) |
| Observabilidad | 6 % | Logs, métricas, dashboard, evidencias de eventos y capacidad de diagnóstico extremo a extremo. | [logs-y-observabilidad.md](../06-estandares/logs-y-observabilidad.md) |
| Documentación y defensa | 7 % | PDF final, diagramas C4 o equivalentes, contratos, ADRs, reparto equilibrado y defensa técnica de todos los miembros. | [entregables.md](entregables.md), [08-adr](../08-adr/README.md) |

Total: 100 %.

## Preguntas posibles en la defensa (§18)

- ¿Por qué cada microservicio existe como componente independiente?
- ¿Cómo se evita reservar dos veces el mismo recurso?
- ¿Qué ocurre cuando una reserva caduca?
- ¿Cómo llega un evento al Data Lake?
- ¿Qué data mart se usa para decidir una recolocación?
- ¿Cómo se diagnostica un fallo entre microservicios?
- ¿Qué componentes pueden escalar de forma independiente y por qué?
- ¿Qué ocurre si se duplica un evento o si una Lambda falla temporalmente?

> PENDIENTE: preparar la respuesta a cada pregunta, con enlace al fichero o ADR que la respalda.
