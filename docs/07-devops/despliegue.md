---
tipo: devops
estado: borrador
responsable: PENDIENTE
---

# Despliegue

## Lo que dice el enunciado

- Puede desplegarse en AWS Academy, AWS real, LocalStack o un entorno local con servicios
  equivalentes. La decisión se justifica en el PDF (§9).
- Entregable: instrucciones de despliegue o de reproducción de la infraestructura (§13.10).
- Ampliación: despliegue por entornos, blue/green simulado o rollback documentado (§15).

## Decisión de plataforma

Hay tres entornos:

| Entorno | Uso | Qué se despliega |
|---|---|---|
| Local | Desarrollo y pruebas automáticas, con Docker Compose y LocalStack ([entorno-local.md](entorno-local.md)). | Todo |
| Sandbox de AWS Academy | Pruebas en AWS al final de cada sprint, con los créditos de la universidad. | Solo las piezas compatibles con el sandbox (ver más abajo) |
| AWS normal | Despliegue para la defensa. | Todo, con el diseño completo |

El mismo Terraform se usa en los tres entornos, con variables por entorno:

- **Endpoint y credenciales:** LocalStack, el sandbox o la cuenta normal.
- **Roles IAM:** en local y en AWS normal, Terraform crea los roles. En el sandbox no puede
  crearlos y usa el ARN de `LabRole`.
- **Piezas activadas:** en el sandbox se desactivan las que usan servicios bloqueados (SQS,
  ECS, ECR, Secrets Manager).

> PENDIENTE: justificar en el PDF la elección del sandbox de AWS Academy y de AWS normal (§9).

> PENDIENTE: decidir cómo se organiza Terraform por entornos (ficheros `.tfvars` por entorno, workspaces o carpetas separadas).

## Restricciones del sandbox de AWS Academy

El entorno de pruebas es **AWS Academy Cloud Foundations – Sandbox**. Según sus
instrucciones, a fecha de 2026-10-27 (las restricciones pueden cambiar):

- **Sesiones efímeras.** Al acabar cada sesión se borran todos los datos y recursos creados.
  Las sesiones duran unas 3 horas (el contador mostraba 2:52 nada más empezar).
- **Región única:** solo `us-east-1`.
- **IAM de solo lectura.** No se pueden crear roles (salvo los vinculados a servicios). Hay
  que usar el rol `LabRole`, también para las Lambdas, y el perfil de instancia
  `LabInstanceProfile` para EC2.
- **Servicios permitidos:**
  - Cómputo: EC2, EC2 Auto Scaling, Elastic Beanstalk, Lambda.
  - Red y contenido: Elastic Load Balancing, CloudFront, Route 53 (sin registrar dominios).
  - Datos: RDS, S3.
  - Mensajería: SNS.
  - Gestión: CloudFormation, CloudWatch, CloudTrail, CloudShell, Systems Manager. KMS solo
    permite listar claves.
- **Límites de EC2:**
  - Tipos `t2`/`t3` hasta `medium`.
  - Máximo 9 instancias a la vez; las que sobren se terminan.
  - Volúmenes EBS `gp2` de hasta 35 GB.
- **Límites de RDS:**
  - PostgreSQL permitido.
  - Sin Multi-AZ y sin monitorización mejorada.
  - Instancias hasta `medium`.
  - Almacenamiento `gp2` de hasta 100 GB.

### Pruebas hechas el 2026-10-27

| Operación | Resultado |
|---|---|
| `sqs:CreateQueue` | ❌ `AccessDenied` |
| `events:PutRule` (programada) y `events:DeleteRule` | ✅ Crear y borrar funciona |
| `scheduler:ListSchedules` | ✅ Lista vacía. Crear no está comprobado |
| `ssm:PutParameter` (`SecureString`) y `ssm:DeleteParameter` | ✅ Crear y borrar funciona |
| `ecs:CreateCluster` | ❌ `AccessDeniedException` (listar sí funciona) |
| `ecr:CreateRepository` | ❌ `AccessDeniedException` (listar sí funciona) |
| `secretsmanager:CreateSecret` | ❌ `AccessDeniedException` (listar sí funciona) |

### Qué se puede probar en el sandbox

| Pieza del diseño | En el sandbox |
|---|---|
| Lambdas (con `LabRole`) | ✅ |
| Tópicos SNS | ✅ |
| Reglas programadas de EventBridge | ✅ |
| RDS PostgreSQL ([ADR 0003](../08-adr/0003-una-instancia-rds-con-una-base-de-datos-por-servicio.md)) | ✅ Compatible con el diseño: instancia pequeña y sin Multi-AZ |
| S3 (Data Lake y apps web con CloudFront) | ✅ |
| Balanceador de carga | ✅ |
| Colas SQS y DLQ ([ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)) | ❌ Solo en local y en AWS normal |
| ECS Fargate y ECR | ❌ Solo en local y en AWS normal |
| Secrets Manager | ❌ Solo en local y en AWS normal |

Además, por ser un entorno efímero:

- **Terraform debe recrear todo** lo compatible en cada sesión con un solo `apply`, incluidas
  las semillas. El estado de Terraform de una sesión anterior ya no sirve.
- **Las credenciales del sandbox son temporales**, así que GitHub Actions no puede desplegar
  automáticamente en él. El despliegue se lanza a mano.
- **`aws login` no funciona** con el sandbox. Las credenciales se copian desde *Details →
  Show → AWS CLI* a `~/.aws/credentials`, y hay que volver a copiarlas en cada sesión.

## Presupuesto

| Cuenta | Presupuesto |
|---|---|
| Sandbox de AWS Academy | Unos 100 € de créditos por miembro, unos 300 € en total |
| AWS normal (defensa) | PENDIENTE |

Reglas para no gastar de más, sobre todo en la cuenta normal:

- El despliegue completo solo se mantiene encendido mientras se usa. Después se destruye con
  `terraform destroy` (ver [limpieza-de-recursos.md](limpieza-de-recursos.md)).
- Antes del primer despliegue en la cuenta normal se crea una alerta de AWS Budgets.
- Se evitan los recursos con coste fijo por hora que no hacen falta (NAT Gateway, RDS
  Multi-AZ, varias instancias RDS).

> PENDIENTE: decidir de quién es la cuenta de AWS normal, quién paga, el presupuesto máximo y si tiene créditos o capa gratuita.

> PENDIENTE: estimar el coste del despliegue completo (Fargate, balanceador de carga, RDS) por día encendido, y decidir cuántos días antes de la defensa se despliega.

## Procedimiento

> PENDIENTE: escribir el procedimiento de despliegue paso a paso cuando exista la infraestructura.

> PENDIENTE: definir el procedimiento de rollback, si se aborda.

## Relacionado

- [infraestructura.md](infraestructura.md)
- [pipeline.md](pipeline.md)
- [limpieza-de-recursos.md](limpieza-de-recursos.md)
