---
tipo: adr
estado: borrador
responsable: Joel
---

# ADR 0001: Emulación local de AWS con LocalStack (Student Plan)

- **Estado:** propuesto
- **Fecha:** 2026-10-27
- **Autores:** Joel

## Problema

El sistema usa servicios gestionados de AWS: SNS y SQS para los eventos, Lambdas, Data Lake en
S3 y bases de datos PostgreSQL. Las pruebas se hacen en AWS Academy y la defensa se despliega
en AWS normal ([despliegue.md](../07-devops/despliegue.md)). El enunciado exige además levantar
el sistema en local con un único flujo de comandos (§10) y ejecutar pruebas automáticas en el
pipeline.

Hay que decidir cómo se emulan esos servicios en las máquinas del equipo y en el CI. Se quiere
usar muchos servicios de AWS, así que el emulador no debe obligar a renunciar a ninguno
por no poder ejecutarlo en local. Desarrollar directamente contra AWS no es viable: las
sesiones de AWS Academy caducan y tienen límites, y AWS normal tiene coste.

## Alternativas

1. **LocalStack, plan Hobby (gratuito)**: herramienta madura y citada en el enunciado (§9).
   Inconveniente: deja fuera RDS, ECS, ECR, Athena, Glue, Cognito y API Gateway HTTP.
2. **LocalStack, Student Plan** (GitHub Student Developer Pack): gratuito para estudiantes
   verificados. En cuanto a servicios, equivale al plan Ultimate: incluye todos los servicios
   emulados y las pruebas en CI. Inconvenientes: cada miembro necesita cuenta y token propios,
   y el CI necesita un token como secreto.
3. **floci**: emulador con licencia MIT, sin cuenta ni token y compatible con LocalStack.
   Inconvenientes: proyecto joven, con menos documentación y ejemplos, y algunos servicios
   simulados.
4. **Desarrollar directamente en AWS**: máxima fidelidad. Inconvenientes: coste, sesiones que
   caducan, imposibilidad de trabajar sin conexión y CI lento.

## Decisión

Usar **LocalStack con el Student Plan** en local y en el CI, con estas reglas:

- **Versión fijada** de la imagen (`localstack/localstack:2026.10.3`), nunca `latest`. Se
  actualiza mediante un PR que pase la batería de pruebas.
- **Tokens fuera del repositorio.** Cada miembro guarda su `LOCALSTACK_AUTH_TOKEN` en un
  `.env` local, que está en el `.gitignore`. El CI usa un token de CI guardado como secreto
  de GitHub Actions.
- **Código independiente del emulador.** Microservicios, Lambdas y Terraform leen el endpoint
  de `AWS_ENDPOINT_URL`. En local apunta a LocalStack y en AWS no se define.
- **AWS como referencia final.**
  - Al final de cada sprint se valida en el sandbox de AWS Academy lo que este permite
    (Lambda, SNS, RDS, S3, EventBridge).
  - Antes de la defensa se valida el despliegue completo en la cuenta de AWS normal. Ver
    [despliegue.md](../07-devops/despliegue.md).
- **Plan B:** si falla la licencia o se pierde el acceso, se cambia la imagen por floci, que
  acepta la configuración de LocalStack.

Motivo principal: cubre todos los servicios que se quieren usar sin renunciar a ninguno, es la
herramienta más madura y documentada, y el enunciado la menciona expresamente.

## Consecuencias

- **Positivas:**
  - `docker compose up` arranca el emulador y el mismo Terraform crea en él la infraestructura de AWS.
  - Se pueden usar RDS, ECS/ECR, Athena y Glue en local, lo que encaja con las ampliaciones
    de §15.
  - El mismo Terraform sirve para local, AWS Academy y AWS normal.
  - El CI puede probar la integración con SNS/SQS, las Lambdas y el Data Lake.
- **Negativas o riesgos:**
  - **Los tres miembros** deben estar verificados en GitHub Education y activar el Student
    Plan. Las licencias son individuales.
  - **El CI depende de un token válido.** Si caduca, el pipeline falla. La documentación del
    plan no indica límites de uso en CI, así que hay que vigilarlo.
  - **Telemetría:** el plan la tiene activada por defecto. Se puede desactivar.
  - **Diferencias con AWS:**
    - LocalStack no aplica los permisos IAM como AWS.
    - LocalStack no bloquea los servicios que el sandbox de Academy sí bloquea (SQS, ECS,
      ECR, Secrets Manager).
    - Por eso hay que validar en AWS: en el sandbox cada sprint y en la cuenta normal antes
      de la defensa.
- **Ficheros del vault afectados:**
  - [entorno-local.md](../07-devops/entorno-local.md)
  - [infraestructura.md](../07-devops/infraestructura.md)
  - [tests.md](../06-estandares/tests.md)
  - [pipeline.md](../07-devops/pipeline.md)
