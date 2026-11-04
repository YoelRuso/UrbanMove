---
tipo: servicio
estado: borrador
responsable: PENDIENTE
---

# Órdenes de recolocación

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | No |

## 1. Responsabilidad

Gestiona la redistribución de recursos entre zonas a partir de reglas o indicadores de demanda.

## 2. Qué NO hace

- No calcula los data marts de demanda: los construye la capa analítica
  ([data-marts.md](../05-datos/data-marts.md)).
- No gestiona reparaciones ni recargas: [Órdenes de mantenimiento](ordenes-de-mantenimiento.md).

## 3. Datos de los que es dueño

Orden de recolocación: zona de origen (con exceso), zona de destino (con déficit), recursos y
estado (asignada, en curso o completada, §3.2).

> PENDIENTE: definir el modelo de datos y el estado inicial de la orden.

## 4. API

> PENDIENTE: definir endpoints para consultar órdenes y marcarlas como asignada, en curso o completada.

## 5. Eventos que publica

Eventos del catálogo relacionados con esta responsabilidad: `RelocationOrderCreated` ("Orden
creada para mover recursos entre zonas") y `RelocationOrderCompleted` ("Orden completada por el
equipo de mantenimiento").

> PENDIENTE: confirmar que este servicio publica ambos eventos y decidir si los estados asignada y en curso emiten evento.

## 6. Eventos que consume

`DemandHotspotDetected` ("Zona con demanda superior a la disponibilidad") está relacionado.

> PENDIENTE: decidir si las órdenes se crean consumiendo `DemandHotspotDetected` o por llamada de la Lambda de recolocación.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias.

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

- Mínimo para aprobar: "Generación de órdenes de recolocación a partir de datos de demanda" (§14).
- Regla de ejemplo (§8.3): si una zona tiene menos de tres recursos disponibles y ha tenido más
  de diez intentos de reserva o viajes iniciados en la última hora, se genera una orden para
  recolocar recursos desde una zona con exceso.
- Diagrama de secuencia obligatorio de "recolocación" (§4.2).

> PENDIENTE: decidir la regla de recolocación definitiva y quién la evalúa.

## 10. Relacionado

- [recolocacion.md](../04-lambdas/recolocacion.md)
- [data-marts.md](../05-datos/data-marts.md)
- [flujo-analitica-y-recolocacion.md](../09-flujos/flujo-analitica-y-recolocacion.md)
