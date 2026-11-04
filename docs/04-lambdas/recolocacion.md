---
tipo: lambda
estado: borrador
responsable: PENDIENTE
---

# Lambda: Recolocación

**Obligatoria:** PENDIENTE (ver [README](README.md)).

## Qué hace (§4.3)

Propone órdenes para mover recursos desde zonas con exceso a zonas con déficit.

## Disparador

> PENDIENTE: decidir el disparador (programado, actualización del data mart de demanda, `DemandHotspotDetected`...).

## Entrada

Indicadores de demanda (data mart de Demanda, [data-marts.md](../05-datos/data-marts.md)).

> PENDIENTE: decidir qué data mart o indicadores lee.

## Regla

Regla sencilla de ejemplo (§8.3): si una zona tiene menos de tres recursos disponibles y ha
tenido más de diez intentos de reserva o viajes iniciados en la última hora, se genera una
orden para recolocar recursos desde una zona con exceso. La regla puede ser más avanzada
(predicción, clustering de zonas o análisis temporal).

> PENDIENTE: fijar la regla y sus umbrales, y cómo se elige la zona con exceso.

## Salida y efectos

Crea órdenes en [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md).
Relacionados: `DemandHotspotDetected` y `RelocationOrderCreated`.

> PENDIENTE: decidir qué eventos publica esta Lambda y cómo crea la orden (API o evento).

## Idempotencia y errores

> PENDIENTE: definir cómo se evitan órdenes duplicadas para la misma zona y ventana.

## Relacionado

- [ordenes-de-recolocacion.md](../02-servicios/ordenes-de-recolocacion.md)
- [flujo-analitica-y-recolocacion.md](../09-flujos/flujo-analitica-y-recolocacion.md)
