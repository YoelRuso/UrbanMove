---
tipo: estandar
estado: borrador
responsable: PENDIENTE
---

# Errores, tolerancia a fallos y escalabilidad (§7)

El diseño debe explicar cómo se comporta el sistema ante fallos parciales. No se espera una
solución perfecta, pero sí decisiones conscientes.

## Mecanismos de tolerancia a fallos (§7.1)

Hay que incorporar **al menos cuatro**:

| Mecanismo | ¿Se usa? | Dónde |
|---|---|---|
| Reintentos controlados para llamadas o procesamiento de eventos | Sí | Reentrega de SQS a cada consumidor antes de pasar a la DLQ ([ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)) |
| Colas o tópicos para desacoplar microservicios y evitar pérdida de eventos | Sí | Tópicos SNS por dominio y una cola SQS por consumidor ([ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)) |
| Dead-letter queue o almacenamiento de eventos fallidos para su revisión | Sí | Una DLQ por cola de consumidor ([ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)) |
| Operaciones idempotentes para evitar duplicados al reprocesar mensajes | Sí | Consumidores que descartan `eventId` repetidos ([ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)) |
| Timeouts y gestión explícita de errores entre microservicios | PENDIENTE | PENDIENTE |
| Degradación funcional (p. ej. finalizar un viaje aunque el servicio de recomendaciones no esté disponible) | PENDIENTE | PENDIENTE |
| Health checks en microservicios y reinicio automático de contenedores | PENDIENTE | PENDIENTE |
| Persistencia de eventos críticos antes de ejecutar procesamiento secundario | Sí | Outbox transaccional en los productores ([ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)) |

Con los cinco mecanismos marcados ya se cubre el mínimo de cuatro.

> PENDIENTE: decidir si se aplican también timeouts, degradación funcional y health checks, e indicar dónde.

## Escenarios de fallo (§7.1, §11.5)

El informe incluye **al menos dos** escenarios de fallo probados o simulados. Ejemplos del
enunciado: caída del servicio de historial, error al procesar una orden de mantenimiento, o
fallo temporal de la Lambda que actualiza data marts.

| Escenario | Componente | Comportamiento esperado | Evidencia |
|---|---|---|---|
| PENDIENTE | PENDIENTE | PENDIENTE | PENDIENTE |
| PENDIENTE | PENDIENTE | PENDIENTE | PENDIENTE |

> PENDIENTE: elegir los dos (o más) escenarios de fallo. Uno se demuestra en el [flujo de fallo controlado](../09-flujos/flujo-fallo-controlado.md).

## Escalabilidad (§7.2)

Hay que justificar cómo escalan las partes con más carga:

- La app de usuarios y los servicios de reservas y viajes deben poder escalar horizontalmente.
- Las Lambdas deben poder procesar eventos en paralelo.
- El Data Lake debe almacenar eventos particionados para crecer por volumen y tiempo.
- Los data marts deben poder recalcularse de forma incremental o por ventanas temporales.
- La analítica de demanda no debe bloquear las operaciones principales de reserva, inicio o fin
  de viaje.

> PENDIENTE: definir cómo se configura el escalado horizontal (réplicas, autoescalado, concurrencia de Lambdas).

## Cuellos de botella (§7.2)

Hay que identificar **al menos dos** cuellos de botella probables y proponer una estrategia
concreta para mitigarlos.

| Cuello de botella | Estrategia de mitigación |
|---|---|
| PENDIENTE | PENDIENTE |
| PENDIENTE | PENDIENTE |

> PENDIENTE: identificar los dos cuellos de botella y su mitigación.

## Normas de gestión de errores

> PENDIENTE: definir los valores por defecto de timeouts, número de reintentos y backoff.

> PENDIENTE: definir cómo se reprocesa un evento desde la DLQ.

## Relacionado

- [logs-y-observabilidad.md](logs-y-observabilidad.md)
- [06-estandares/eventos.md](eventos.md)
- [rubrica.md](../00-proyecto/rubrica.md)
