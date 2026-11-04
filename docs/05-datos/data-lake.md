---
tipo: datos
estado: borrador
responsable: PENDIENTE
---

# Data Lake de eventos (§8, §8.1)

El proyecto incluye una capa analítica separada de los microservicios operacionales. Los
microservicios **no** usan el Data Lake como base de datos transaccional. El Data Lake recoge
eventos para análisis, auditoría y generación de data marts.

Puede implementarse con S3, LocalStack, MinIO, ficheros particionados o una alternativa
justificada.

> PENDIENTE: elegir la tecnología del Data Lake (el equipo ha indicado AWS, lo que apunta a S3, pero falta confirmarlo).

## Capas

| Capa | Contenido (§8.1) | Quién escribe | Formato |
|---|---|---|---|
| Raw | Eventos tal como llegan desde los microservicios o el bus de eventos. | PENDIENTE | PENDIENTE |
| Trusted | Eventos validados, normalizados y con esquema conocido. | PENDIENTE | PENDIENTE |
| Curated | Datos preparados para consumo analítico y construcción de data marts. | PENDIENTE | PENDIENTE |

El mínimo para aprobar exige separación "raw, trusted o curated, aunque sea simplificada" (§14).

> PENDIENTE: decidir el formato de fichero de cada capa (JSON, Parquet...) y qué componente promueve los datos entre capas.

## Particionado

Se recomienda particionar por **fecha, tipo de evento y microservicio productor**. Ejemplos
del enunciado:

```
s3://urbanmove-datalake/raw/year=2026/month=09/day=10/source=rides/
s3://urbanmove-datalake/trusted/event_type=RideFinished/
s3://urbanmove-datalake/curated/domain=demand/
```

El Data Lake debe almacenar eventos particionados para crecer por volumen y tiempo (§7.2).

> PENDIENTE: fijar el esquema de particionado definitivo de cada capa y el nombre del bucket o la ruta raíz.

## Requisitos relacionados

- La ingesta la hace la Lambda [Ingesta analítica](../04-lambdas/ingesta-analitica.md), si se
  elige como obligatoria.
- El flujo de analítica pide que "los eventos se almacenen en el Data Lake" (§11.3).
- El flujo de usuario termina con "Se genera historial y eventos para el Data Lake" (§11.1).

> PENDIENTE: decidir la retención de datos y el tratamiento de datos personales en el Data Lake.

## Relacionado

- [data-marts.md](data-marts.md)
- [03-eventos/README.md](../03-eventos/README.md)
- [infraestructura.md](../07-devops/infraestructura.md)
