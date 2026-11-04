---
tipo: devops
estado: borrador
responsable: Joel
---

# Entorno local

## Lo que exige el enunciado

- El README del repositorio debe permitir levantar una versión local con un único flujo
  razonable de comandos, por ejemplo `docker compose up`, scripts de inicialización y comandos
  de prueba (§10).
- Entregable: instrucciones de ejecución local (§13.9).
- Las migraciones, las semillas de datos y la preparación de infraestructura se ejecutan de
  forma documentada (§10).

## Decisiones

- **Orquestación local:** Docker Compose.
- **Emulación de AWS:** [LocalStack](https://localstack.cloud) con el Student Plan y la
  versión fijada `2026.10.3`. Expone todos los servicios en `http://localhost:4566`. Ver
  [ADR 0001](../08-adr/0001-emulacion-local-de-aws-con-localstack.md).
- **Endpoint configurable:** todo el código lee `AWS_ENDPOINT_URL`. En local apunta a
  LocalStack y en AWS no se define.
- **IaC:** Terraform. Ver [infraestructura.md](infraestructura.md).

> PENDIENTE: definir los scripts de inicialización y las semillas (zonas, recursos, usuarios de prueba).

- **PostgreSQL:** se usa el RDS de LocalStack, creado con el mismo Terraform que en AWS. Es
  una instancia con una base de datos por servicio
  ([ADR 0003](../08-adr/0003-una-instancia-rds-con-una-base-de-datos-por-servicio.md)).
  LocalStack arranca un contenedor PostgreSQL real a través del socket de Docker.

## Requisitos previos

- Docker Desktop (Windows o macOS) o Docker Engine con el plugin Compose v2 (Linux).
- Cuenta de LocalStack con el **Student Plan** activado. Hay que estar verificado en GitHub
  Education.
- Java y Maven, para los microservicios Spring Boot.
- Python, para las Lambdas.
- Node.js, para las tres apps React con Vite.
- Terraform.
- AWS CLI v2, para inspeccionar recursos en local.

Las versiones son las últimas estables al crear el repositorio (ver
[acuerdos.md](../10-equipo/acuerdos.md)).

## Configuración del token

Cada miembro crea un fichero `.env` en la raíz del repositorio, que está en el `.gitignore`:

```bash
LOCALSTACK_AUTH_TOKEN=<token personal de app.localstack.cloud>
```

El repositorio incluye un `.env.example` con la misma clave y el valor vacío. En GitHub
Actions, el token de CI se guarda como secreto y se pasa como variable de entorno.

## docker-compose.yml propuesto

Fichero en la raíz del repositorio. Por ahora solo incluye LocalStack. Cada microservicio se
añade como un servicio más, siguiendo el ejemplo comentado.

```yaml
name: urbanmove

services:
  localstack:
    image: localstack/localstack:2026.10.3   # versión fijada; se actualiza por PR
    container_name: localstack
    ports:
      - "4566:4566"
    environment:
      LOCALSTACK_AUTH_TOKEN: ${LOCALSTACK_AUTH_TOKEN:?Falta LOCALSTACK_AUTH_TOKEN en .env}
      LOCALSTACK_HOST: localstack:4566      # URLs que devuelve LocalStack (p. ej. colas SQS) resolubles desde otros contenedores
      PERSISTENCE: 1                        # conserva el estado entre reinicios; en CI se omite
      LAMBDA_DOCKER_NETWORK: urbanmove      # las Lambdas se ejecutan en la misma red que los servicios
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock   # Lambda, RDS y ECS arrancan contenedores reales
      - localstack-data:/var/lib/localstack
    networks:
      - urbanmove

  # Ejemplo de microservicio (plantilla):
  # reservas:
  #   build: ./services/reservas
  #   environment:
  #     AWS_ENDPOINT_URL: http://localstack:4566
  #     AWS_REGION: us-east-1
  #     AWS_ACCESS_KEY_ID: test          # LocalStack no valida las credenciales
  #     AWS_SECRET_ACCESS_KEY: test
  #   depends_on:
  #     - localstack
  #   networks:
  #     - urbanmove

volumes:
  localstack-data:

networks:
  urbanmove:
    name: urbanmove                   # nombre fijo para que coincida con LAMBDA_DOCKER_NETWORK
```

Notas:

- **Credenciales:** `test`/`test` no son secretas. Las únicas credenciales reales del entorno
  local son el token de LocalStack, que va en `.env`. Nunca se ponen credenciales de AWS en
  este fichero.
- **Borrar el estado:** `docker compose down -v` elimina el volumen `localstack-data` y deja
  LocalStack vacío.
- **Arranque:** `depends_on` solo espera a que el contenedor arranque, no a que LocalStack esté
  listo. Los servicios deben reintentar la conexión al arrancar (ver
  [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md)).

> PENDIENTE: decidir si se añade un `healthcheck` al servicio localstack para usar `depends_on: condition: service_healthy`.

## Pasos para levantar el sistema

Secuencia prevista. Se concretará cuando exista el repositorio.

1. Crear `.env` a partir de `.env.example` y poner el token.

2. Levantar el emulador y los servicios:

   ```bash
   docker compose up -d
   ```

3. Comprobar que LocalStack responde y que la licencia está activa:

   ```bash
   curl http://localhost:4566/_localstack/health
   ```

4. Crear la infraestructura (tópicos SNS, colas SQS, buckets del Data Lake, Lambdas) con
   Terraform, apuntando a LocalStack:

   ```bash
   AWS_ENDPOINT_URL=http://localhost:4566 AWS_ACCESS_KEY_ID=test AWS_SECRET_ACCESS_KEY=test terraform -chdir=infra apply -auto-approve
   ```

   > PENDIENTE: confirmar la carpeta de Terraform (`infra/` es provisional) y si se separan entornos (local, Academy, AWS real).

5. Cargar las semillas.

   > PENDIENTE: script de semillas.

6. Ejecutar las pruebas.

   > PENDIENTE: comando de pruebas (probablemente `mvn verify` por servicio).

7. Inspeccionar recursos con la AWS CLI (opcional):

   ```bash
   aws --endpoint-url http://localhost:4566 sqs list-queues
   ```

## Diferencias con AWS que hay que tener presentes

- **IAM y servicios bloqueados:** en local no se reproducen el rol `LabRole` ni los servicios
  que bloquea el sandbox de AWS Academy (SQS, ECS, ECR, Secrets Manager). Ver
  [despliegue.md](despliegue.md).
- **Fidelidad:** LocalStack es muy fiel, pero no es AWS. Los tiempos, los límites de servicio
  y los costes reales solo se ven en AWS.

## Relacionado

- [ADR 0001: emulación local de AWS con LocalStack](../08-adr/0001-emulacion-local-de-aws-con-localstack.md)
- [infraestructura.md](infraestructura.md)
- [pipeline.md](pipeline.md)
- [despliegue.md](despliegue.md)
- [tests.md](../06-estandares/tests.md)
