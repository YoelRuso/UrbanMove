---
tipo: lambda
estado: borrador
responsable: PENDIENTE
---

# Lambda: Construcción de data marts

**Obligatoria:** PENDIENTE (ver [README](README.md)).

## Qué hace (§4.3)

Actualiza tablas agregadas por zona, hora, tipo de recurso o microservicio.

## Disparador

> PENDIENTE: decidir el disparador (programado, llegada de nuevos datos curated, evento...).

## Entrada

Datos de la capa curated del [Data Lake](../05-datos/data-lake.md).

> PENDIENTE: confirmar la capa de entrada.

## Salida y efectos

Actualiza los [data marts](../05-datos/data-marts.md).

> PENDIENTE: decidir qué data marts construye y dónde se almacenan.

## Recálculo

Los data marts deben poder recalcularse de forma incremental o por ventanas temporales (§7.2).

> PENDIENTE: decidir la estrategia (incremental o por ventana) y el tamaño de ventana.

## Idempotencia y errores

> PENDIENTE: definir cómo se reprocesa sin duplicar agregados.

## Notas

- Escenario de fallo de ejemplo: "fallo temporal de la Lambda que actualiza data marts" (§7.1).

## Relacionado

- [data-marts.md](../05-datos/data-marts.md)
- [ingesta-analitica.md](ingesta-analitica.md)
- [flujo-dashboard.md](../09-flujos/flujo-dashboard.md)
