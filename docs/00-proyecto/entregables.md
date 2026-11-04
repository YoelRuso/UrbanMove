---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Entregables

## Lista de entregables (§13)

- [ ] 1. Repositorio GitHub con todo el código fuente.
- [ ] 2. Documento PDF final que explique el trabajo realizado, la arquitectura, las decisiones
      técnicas, el reparto, las pruebas, las evidencias, los problemas encontrados y la
      limpieza de recursos.
- [ ] 3. Documentación arquitectónica completa: contexto, contenedores o despliegue,
      componentes de servicios críticos, secuencias, propiedad de datos y ADRs.
- [ ] 4. Diagrama de arquitectura con apps cliente, dashboard, microservicios atómicos,
      Lambdas, bus de eventos, Data Lake y data marts.
- [ ] 5. Documentación de APIs: endpoints, métodos, payloads y códigos de respuesta principales.
- [ ] 6. Documentación de eventos: nombre, productor, consumidores y esquema mínimo.
- [ ] 7. Descripción de los data marts construidos, con ejemplos de consultas o indicadores.
- [ ] 8. Dashboard operativo, con capturas o evidencia de ejecución explicadas.
- [ ] 9. Instrucciones de ejecución local.
- [ ] 10. Instrucciones de despliegue o de reproducción de la infraestructura.
- [ ] 11. Evidencia de CI/CD funcionando: ejecución de pruebas, construcción de imágenes o
      artefactos, y validaciones automáticas.
- [ ] 12. Evidencia de observabilidad: logs, métricas, trazas, paneles o capturas explicadas.

## Contenido mínimo del PDF final

| Apartado | Origen en el enunciado | Fuente en el vault |
|---|---|---|
| Trabajo realizado y decisiones técnicas | §13.2 | [08-adr](../08-adr/README.md) |
| Justificación de la plataforma de despliegue | §9 | [despliegue.md](../07-devops/despliegue.md) |
| Vista de contexto: actores, apps cliente, sistemas externos simulados y límites del sistema | §4.2 | [vision-general.md](../01-arquitectura/vision-general.md) |
| Vista de contenedores o despliegue: microservicios, Lambdas, BBDD, bus, Data Lake y data marts | §4.2 | [vision-general.md](../01-arquitectura/vision-general.md) |
| Vista de componentes de al menos dos microservicios críticos (p. ej. reservas y viajes) | §4.2 | [reservas.md](../02-servicios/reservas.md), [viajes.md](../02-servicios/viajes.md) |
| Diagramas de secuencia: reserva, inicio de viaje, retirada por mantenimiento y recolocación | §4.2 | [09-flujos](../09-flujos/flujo-usuario.md) |
| Tabla de propiedad de datos | §4.2 | [propiedad-de-datos.md](../01-arquitectura/propiedad-de-datos.md) |
| Contratos de APIs (OpenAPI, README estructurado o colección de peticiones) | §4.2 | [api.md](../06-estandares/api.md) y fichas de servicio |
| Contratos de eventos (tabla, JSON Schema, AsyncAPI o equivalente) | §4.2 | [03-eventos](../03-eventos/README.md) |
| Al menos dos ADR breves | §4.2 | [08-adr](../08-adr/README.md) |
| Transiciones de estado: evento y servicio validador | §5 | [estados-recurso.md](../01-arquitectura/estados-recurso.md) |
| Justificación si se fusionan dos servicios de bajo riesgo | §4.1 | [02-servicios](../02-servicios/README.md) |
| Al menos dos escenarios de fallo probados o simulados | §7.1 | [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md) |
| Escalabilidad, más dos cuellos de botella con su mitigación | §7.2 | [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md) |
| Justificación de usar varios repositorios, si se hace | §10 | [git-y-pull-requests.md](../06-estandares/git-y-pull-requests.md) |
| Reparto de tareas | §1, §12 | [reparto.md](../10-equipo/reparto.md) |
| Pruebas y evidencias | §13.2 | [tests.md](../06-estandares/tests.md), [11-evidencias](../11-evidencias/README.md) |
| Problemas encontrados | §13.2 | — |
| Seguridad y limpieza de recursos | §17 | [limpieza-de-recursos.md](../07-devops/limpieza-de-recursos.md) |

> PENDIENTE: decidir la herramienta y la plantilla del PDF, y quién lo ensambla.

> PENDIENTE: definir dónde se registran los "problemas encontrados" durante el proyecto.

## Restricción de seguridad

No deben incluirse credenciales, tokens, claves privadas ni identificadores sensibles en el
repositorio ni en el PDF (§17).
