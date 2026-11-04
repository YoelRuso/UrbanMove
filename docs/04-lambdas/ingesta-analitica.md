---
tipo: lambda
estado: borrador
responsable: PENDIENTE
---

# Lambda: Ingesta analítica

**Obligatoria:** PENDIENTE (ver [README](README.md)).

## Qué hace (§4.3)

Copia o transforma eventos hacia el Data Lake y actualiza particiones o metadatos.

## Disparador

> PENDIENTE: decidir el disparador (suscripción al bus, cola, lotes...).

## Entrada

Eventos de dominio del [catálogo](../03-eventos/README.md).

> PENDIENTE: decidir si ingiere todos los eventos o un subconjunto.

## Salida y efectos

Escribe en las capas del [Data Lake](../05-datos/data-lake.md) (raw, y posiblemente trusted) y
actualiza particiones o metadatos.

> PENDIENTE: decidir qué capas escribe esta Lambda y qué componente promueve los datos de raw a trusted y de trusted a curated.

> PENDIENTE: decidir el catálogo de metadatos, si se usa alguno (p. ej. Glue).

## Idempotencia y errores

> PENDIENTE: definir cómo se evitan duplicados en el Data Lake y qué se hace con los eventos inválidos (DLQ, carpeta de rechazados...).

## Notas

- Pregunta de defensa: "¿Cómo llega un evento al Data Lake?" (§18).
- Debe poder procesar eventos en paralelo (§7.2).

## Relacionado

- [data-lake.md](../05-datos/data-lake.md)
- [construccion-de-data-marts.md](construccion-de-data-marts.md)
