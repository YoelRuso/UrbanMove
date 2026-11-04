---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Mínimos para aprobar (§14)

Para superar el proyecto deben cumplirse **todos** estos requisitos.

- [ ] Tres interfaces diferenciadas: usuarios finales, mantenimiento/operaciones y dashboard
      operativo. → [apps-cliente.md](../01-arquitectura/apps-cliente.md)
- [ ] Al menos diez microservicios atómicos, incluyendo obligatoriamente:
  - [ ] [Identidad](../02-servicios/identidad.md)
  - [ ] [Perfiles de usuario](../02-servicios/perfiles-de-usuario.md)
  - [ ] [Inventario de recursos](../02-servicios/inventario-de-recursos.md)
  - [ ] [Disponibilidad](../02-servicios/disponibilidad.md)
  - [ ] [Reservas](../02-servicios/reservas.md)
  - [ ] [Viajes](../02-servicios/viajes.md)
  - [ ] [Historial](../02-servicios/historial.md)
  - [ ] [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md)
  - [ ] [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md)
  - [ ] [Analítica operacional](../02-servicios/analitica-operacional.md)
- [ ] El historial está implementado como microservicio independiente.
- [ ] Documentación arquitectónica con diagramas, contratos de APIs, contratos de eventos,
      propiedad de datos y al menos dos ADRs. → [entregables.md](entregables.md), [08-adr](../08-adr/README.md)
- [ ] Al menos tres Lambdas o funciones serverless equivalentes. → [04-lambdas](../04-lambdas/README.md)
- [ ] Al menos un bus, cola o tópico para comunicación asíncrona. → [03-eventos](../03-eventos/README.md)
- [ ] Data Lake de eventos con separación raw, trusted o curated, aunque sea simplificada.
      → [data-lake.md](../05-datos/data-lake.md)
- [ ] Al menos cuatro data marts asociados a dominios o microservicios.
      → [data-marts.md](../05-datos/data-marts.md)
- [ ] Generación de órdenes de recolocación a partir de datos de demanda.
      → [flujo-analitica-y-recolocacion.md](../09-flujos/flujo-analitica-y-recolocacion.md)
- [ ] Dashboard con indicadores de flota, reservas, viajes, mantenimiento, recolocación y salud
      básica del sistema. → [apps-cliente.md](../01-arquitectura/apps-cliente.md)
- [ ] Mecanismos explícitos de tolerancia a fallos y al menos dos fallos simulados o probados.
      → [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md)
- [ ] Justificación de escalabilidad horizontal o por eventos en los componentes de mayor carga.
      → [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md)
- [ ] Pipeline DevOps con pruebas automáticas, construcción de artefactos o imágenes, y
      evidencias de ejecución. → [pipeline.md](../07-devops/pipeline.md)
- [ ] PDF final y defensa técnica por parte de todos los miembros.
      → [entregables.md](entregables.md)

## Otros requisitos obligatorios repartidos por el enunciado

No aparecen en §14, pero el enunciado los formula como obligatorios:

- [ ] Al menos cuatro de los mecanismos de tolerancia a fallos de §7.1.
- [ ] Al menos dos cuellos de botella identificados, con estrategia de mitigación (§7.2).
- [ ] La analítica alimenta al menos una decisión operacional (§8.3).
- [ ] Cada evento tiene identificador, timestamp, origen, tipo, versión de esquema e
      identificador de correlación (§6). → [sobre-comun.md](../03-eventos/sobre-comun.md)
- [ ] Transiciones de estado documentadas con el evento que las provoca y el servicio que las
      valida (§5). → [estados-recurso.md](../01-arquitectura/estados-recurso.md)
- [ ] Mínimos de pipeline de §10. → [pipeline.md](../07-devops/pipeline.md)
- [ ] Mínimos de observabilidad de §10. → [logs-y-observabilidad.md](../06-estandares/logs-y-observabilidad.md)
- [ ] Sección de seguridad y limpieza de recursos en el PDF (§17).
      → [limpieza-de-recursos.md](../07-devops/limpieza-de-recursos.md)
- [ ] Demostración de los cinco flujos (§11, §18). → [09-flujos](../09-flujos/flujo-usuario.md)
