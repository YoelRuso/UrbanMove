---
tipo: adr
estado: borrador
responsable: PENDIENTE
---

# Decisiones arquitectónicas (ADR)

El PDF debe incluir **al menos dos** decisiones arquitectónicas documentadas como ADR breve:
problema, alternativas, decisión y consecuencias (§4.2). Los ADR forman parte de la
documentación arquitectónica completa (§13.3).

## Convención

- Fichero: `NNNN-titulo-en-kebab-case.md` (p. ej. `0001-...md`), copiado de
  [_plantilla.md](_plantilla.md).
- Un ADR aceptado no se edita: si cambia la decisión, se crea uno nuevo que lo sustituye.
- Las fichas afectadas enlazan el ADR en su sección "Decisiones y notas".

## Índice

| Nº | Título | Estado | Fecha |
|---|---|---|---|
| 0001 | [Emulación local de AWS con LocalStack (Student Plan)](0001-emulacion-local-de-aws-con-localstack.md) | propuesto | 2026-10-27 |
| 0002 | [Bus de eventos con SNS y SQS](0002-bus-de-eventos-con-sns-y-sqs.md) | propuesto | 2026-10-27 |
| 0003 | [Una instancia RDS con una base de datos por servicio](0003-una-instancia-rds-con-una-base-de-datos-por-servicio.md) | propuesto | 2026-10-27 |

Con los tres ADR propuestos ya se cubre el mínimo de dos. Para que cuenten, deben pasar a
"aceptado".

> PENDIENTE: revisar los ADR 0001, 0002 y 0003 con el equipo y marcarlos como aceptados.

## Decisiones abiertas en el vault que podrían convertirse en ADR

Lista de referencia (no decidida), tomada de las marcas PENDIENTE:

- Plataforma de despliegue: [despliegue.md](../07-devops/despliegue.md).
- Servicio dueño del estado del recurso: [propiedad-de-datos.md](../01-arquitectura/propiedad-de-datos.md).
- Mecanismo contra la doble reserva: [reservas.md](../02-servicios/reservas.md).
- Elección de las tres Lambdas obligatorias: [04-lambdas](../04-lambdas/README.md).
- Fuente de datos del dashboard: [apps-cliente.md](../01-arquitectura/apps-cliente.md).
- Fusión de servicios de bajo riesgo, si se hace: [02-servicios](../02-servicios/README.md).
- Plataforma de contenedores en AWS: [infraestructura.md](../07-devops/infraestructura.md).
