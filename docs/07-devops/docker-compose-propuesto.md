---
tipo: devops
estado: borrador
responsable: Joel
---

# docker-compose.yml propuesto

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

## Relacionado

- [entorno-local.md](entorno-local.md)
