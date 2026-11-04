---
tipo: datos
estado: borrador
responsable: PENDIENTE
---

# Data marts (§8.2)

Hay que construir **al menos cuatro data marts**. Cada uno tiene una finalidad clara y está
asociado a un dominio o microservicio. Se valora incluir más si se integran con decisiones
reales del sistema.

| Data mart | Preguntas que debe responder (§8.2) | Dominio asociado | Lo consumen | Se construye |
|---|---|---|---|---|
| Usuarios | ¿Cuántos usuarios activos hay por período? ¿Qué usuarios tienen más viajes o cancelaciones? | Perfiles, Reservas, Viajes | PENDIENTE | PENDIENTE |
| Reservas | ¿Cuántas reservas caducan? ¿En qué zonas se reservan recursos que luego no se usan? | [Reservas](../02-servicios/reservas.md) | PENDIENTE | PENDIENTE |
| Viajes | ¿Cuáles son los orígenes y destinos más frecuentes? ¿Qué duración media tienen los viajes? | [Viajes](../02-servicios/viajes.md) | PENDIENTE | PENDIENTE |
| Flota | ¿Cuántos recursos están disponibles, en uso, en carga o en reparación por zona? | Inventario, Disponibilidad | PENDIENTE | PENDIENTE |
| Mantenimiento | ¿Qué recursos requieren recarga o reparación? ¿Cuánto tiempo pasan fuera de servicio? | [Órdenes de mantenimiento](../02-servicios/ordenes-de-mantenimiento.md) | PENDIENTE | PENDIENTE |
| Operaciones | ¿Qué órdenes de recolocación se crean? ¿Cuántas se completan y con qué retraso? | [Órdenes de recolocación](../02-servicios/ordenes-de-recolocacion.md) | PENDIENTE | PENDIENTE |
| Demanda | ¿Qué zonas tienen déficit o exceso de recursos según franja horaria y tipo de vehículo? | Analítica / recolocación | [Recolocación](../04-lambdas/recolocacion.md), dashboard | PENDIENTE |

La sección 2 menciona también como ejemplos de dominio la **facturación simulada** y la
**demanda por zona**. La facturación simulada no aparece en la tabla de §8.2.

> PENDIENTE: elegir los cuatro (o más) data marts que se construyen.

> PENDIENTE: definir el esquema de cada data mart (dimensiones: zona, hora o franja, tipo de recurso, microservicio; y métricas).

> PENDIENTE: decidir dónde se almacenan los data marts y con qué motor se consultan (p. ej. Athena, una base de datos, ficheros curated).

> PENDIENTE: escribir ejemplos de consultas o indicadores de cada data mart (entregable §13.7).

## Restricciones

- El data mart de **Demanda** está implícito en los mínimos: el flujo de analítica exige
  actualizar "al menos un data mart de demanda" (§11.3) y las órdenes de recolocación se
  generan a partir de datos de demanda (§14).
- Deben poder recalcularse de forma incremental o por ventanas temporales (§7.2).
- La analítica de demanda no debe bloquear la reserva ni el inicio o fin de viaje (§7.2).
- La observabilidad exige una consulta o captura de algún data mart generado (§10).
- Pregunta de defensa: "¿Qué data mart se usa para decidir una recolocación?" (§18).

## Relacionado

- [data-lake.md](data-lake.md)
- [construccion-de-data-marts.md](../04-lambdas/construccion-de-data-marts.md)
- [analitica-operacional.md](../02-servicios/analitica-operacional.md)
- [apps-cliente.md](../01-arquitectura/apps-cliente.md)
