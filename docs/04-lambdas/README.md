---
tipo: lambda
estado: borrador
responsable: PENDIENTE
---

# Funciones Lambda (§4.3)

El sistema debe incluir **al menos tres funciones Lambda** o funciones serverless equivalentes,
conectadas a eventos reales del sistema. El enunciado describe cinco: **tres son obligatorias y
el resto son ampliaciones valorables**, pero no dice cuáles son las obligatorias.

| Lambda | Descripción (§4.3) | Obligatoria | Ficha |
|---|---|---|---|
| Expiración de reservas | Libera un recurso si una reserva no se confirma en el tiempo establecido. | PENDIENTE | [expiracion-de-reservas.md](expiracion-de-reservas.md) |
| Detección de mantenimiento | Genera una orden cuando un recurso queda con batería baja, avería o demasiados usos desde la última revisión. | PENDIENTE | [deteccion-de-mantenimiento.md](deteccion-de-mantenimiento.md) |
| Ingesta analítica | Copia o transforma eventos hacia el Data Lake y actualiza particiones o metadatos. | PENDIENTE | [ingesta-analitica.md](ingesta-analitica.md) |
| Construcción de data marts | Actualiza tablas agregadas por zona, hora, tipo de recurso o microservicio. | PENDIENTE | [construccion-de-data-marts.md](construccion-de-data-marts.md) |
| Recolocación | Propone órdenes para mover recursos desde zonas con exceso a zonas con déficit. | PENDIENTE | [recolocacion.md](recolocacion.md) |

> PENDIENTE: elegir las tres Lambdas obligatorias. Otros mínimos dependen de funciones que aparecen aquí: el Data Lake (§14), la generación de órdenes de recolocación (§14) y la expiración de reservas (pregunta de defensa, §18). Si no las hace una Lambda, las tiene que hacer otro componente.

- **Lenguaje:** Python, con el runtime más reciente que soporta Lambda (`python3.14` a fecha
  de 2026-10-27).
- **Empaquetado y despliegue:** Terraform, como el resto de la infraestructura (ver
  [infraestructura.md](../07-devops/infraestructura.md)).
- **Disparadores:** pendientes en cada ficha. El [ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md), sin aceptar,
  propone colas SQS y EventBridge Scheduler para las tareas programadas. En el sandbox solo se ha
  probado crear reglas programadas de EventBridge ([despliegue.md](../07-devops/despliegue.md)).

> PENDIENTE: comprobar que LocalStack ejecuta el runtime `python3.14`; si no, usar `python3.13`.

> PENDIENTE: definir cómo se comparten con las Lambdas los esquemas de eventos que también usan los servicios en Java (p. ej. JSON Schema común).

## Requisitos comunes

- Conectadas a eventos reales del sistema (§4.3).
- Deben poder procesar eventos en paralelo (§7.2).
- Se empaquetan o despliegan mediante comandos versionados en el pipeline (§10).
- Pregunta de defensa: qué ocurre si se duplica un evento o si una Lambda falla temporalmente
  (§18). Ver [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md).
- Ejemplo de carpeta de repositorio: `lambdas/` (§10).
