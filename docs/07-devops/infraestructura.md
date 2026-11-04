---
tipo: devops
estado: borrador
responsable: PENDIENTE
---

# Infraestructura

## Opciones que valora el enunciado (§9)

| Pieza | Opciones citadas | Decisión |
|---|---|---|
| Contenedores | ECS, App Runner, Kubernetes, Docker Compose o alternativa justificada | Docker Compose en local. En AWS: propuesta ECS Fargate con imágenes en ECR (pendiente de confirmar) |
| Lambdas | SAM, CDK, Terraform, Serverless Framework o scripts reproducibles | Terraform |
| Eventos | SQS, SNS, EventBridge, Kafka, RabbitMQ o equivalente | SNS + SQS con DLQ por cola, y EventBridge Scheduler para las tareas programadas ([ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)) |
| Data Lake | S3, LocalStack, MinIO o almacenamiento particionado reproducible | S3 (LocalStack en local) |
| Infraestructura como código | Terraform, CloudFormation, SAM, CDK o scripts versionados | Terraform |
| Escalado | Configuración de escalado horizontal, concurrencia o réplicas | PENDIENTE |
| Detección de fallos | Health checks, reinicios automáticos o alarmas | PENDIENTE |
| Bases de datos de los servicios | No especificado | PostgreSQL en una sola instancia RDS, con una base de datos y un usuario por servicio con estado ([ADR 0003](../08-adr/0003-una-instancia-rds-con-una-base-de-datos-por-servicio.md)) |

## Stack acordado

| Pieza | Tecnología |
|---|---|
| Microservicios | Java, Spring Boot, Maven (versiones en [acuerdos.md](../10-equipo/acuerdos.md)) |
| Lambdas | Python |
| Apps cliente | Tres apps React separadas, creadas con Vite |
| Bases de datos | PostgreSQL en RDS, una base de datos por servicio con estado |
| Bus de eventos | SNS + SQS |
| Contenedores | Docker |
| CI/CD | GitHub Actions |
| IaC | Terraform |
| Emulación local de AWS | LocalStack, Student Plan ([ADR 0001](../08-adr/0001-emulacion-local-de-aws-con-localstack.md)) |

Las Lambdas se escriben en Python (ver [04-lambdas](../04-lambdas/README.md)).

## Contenedores en AWS (propuesta)

El equipo aún no lo ha decidido. La propuesta para la cuenta de AWS normal es **ECS Fargate
con imágenes en ECR**. ECS y ECR están bloqueados en el sandbox de AWS Academy (ver
[despliegue.md](despliegue.md)), así que allí no se prueban.

Motivos de la propuesta:

- Es una ampliación valorada (§15).
- No hay servidores que gestionar: cada microservicio es un servicio de ECS que escala con
  réplicas (§7.2).
- ECS reinicia las tareas que fallan el health check (§7.1).

Fargate cobra por hora mientras las tareas están encendidas, así que el despliegue en AWS se
hace solo cuando hace falta (pruebas al final de cada sprint y la defensa) y se destruye
después con `terraform destroy` (ver [limpieza-de-recursos.md](limpieza-de-recursos.md)).

Para no pagar un NAT Gateway, que tiene un coste fijo por hora, las tareas pueden ir en
subredes públicas con IP pública y grupos de seguridad restrictivos.

> PENDIENTE: confirmar ECS Fargate para la cuenta de AWS normal.

> PENDIENTE: estimar el coste diario del despliegue completo (tareas de Fargate, balanceador de carga y RDS) antes del primer despliegue.

Ampliaciones relacionadas (§15): Terraform; ECS con imágenes en ECR; uso de S3, DynamoDB, SQS,
SNS, EventBridge, Lambda y CloudWatch.

> PENDIENTE: decidir cada fila de la tabla y registrar las decisiones relevantes como ADR.

> PENDIENTE: definir la red (VPC, subredes, exposición pública de las APIs), si aplica.

Las restricciones del sandbox de AWS Academy, comprobadas el 2026-10-27, están en
[despliegue.md](despliegue.md).

## Requisito de documentación

- Instrucciones de despliegue o de reproducción de la infraestructura (§13.10). Ver
  [despliegue.md](despliegue.md).
- Vista de contenedores o despliegue en el PDF (§4.2). Ver
  [vision-general.md](../01-arquitectura/vision-general.md).

## Relacionado

- [despliegue.md](despliegue.md)
- [entorno-local.md](entorno-local.md)
- [ADR 0001: emulación local de AWS con LocalStack](../08-adr/0001-emulacion-local-de-aws-con-localstack.md)
- [limpieza-de-recursos.md](limpieza-de-recursos.md)
- [08-adr](../08-adr/README.md)
