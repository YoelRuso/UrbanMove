---
tipo: adr
estado: borrador
responsable: Joel
---

# ADR 0002: Bus de eventos con SNS y SQS

- **Estado:** propuesto
- **Fecha:** 2026-10-27
- **Autores:** Joel

## Problema

Los microservicios emiten eventos de dominio que consumen otros servicios, las Lambdas, el
historial y el Data Lake (§6). Hace falta al menos un bus, cola o tópico (§14) y al menos cuatro
mecanismos de tolerancia a fallos (§7.1). El objetivo del equipo es una arquitectura robusta:
un consumidor caído o lento no debe perder eventos ni frenar a los demás.

## Alternativas

1. **SNS + SQS**: un tópico SNS por dominio, y una cola SQS por consumidor suscrita al tópico.
   - Ventajas: fan-out nativo, cada consumidor tiene su propia cola con reintentos y DLQ, y se
     integra directamente con Lambda. Coste muy bajo, buen soporte en Spring Cloud AWS y en
     LocalStack.
   - Inconvenientes: más recursos que configurar (tópicos, colas, suscripciones, DLQ).
2. **EventBridge**: un bus con reglas que enrutan cada evento a sus destinos.
   - Ventajas: enrutado por contenido muy flexible y registro de esquemas.
   - Inconvenientes: para tener reintentos por consumidor y DLQ hay que poner igualmente una
     cola SQS detrás de cada regla.
3. **Kafka (Amazon MSK) o RabbitMQ (Amazon MQ)**: brókers clásicos.
   - Ventajas: Kafka permite reprocesar el histórico y garantiza el orden por partición.
   - Inconvenientes: coste fijo alto aunque no haya tráfico (incompatible con los créditos
     disponibles) y más operación.

## Decisión

Usar **SNS + SQS** como bus de eventos, con estas reglas:

- **Topología:**
  - Un tópico SNS por dominio productor (p. ej. `reservas`, `viajes`, `mantenimiento`).
  - Una cola SQS por consumidor, suscrita a los tópicos que le interesan. Una política de
    filtro por tipo de evento evita recibir lo que no necesita.
  - La Lambda de ingesta analítica tiene su propia cola, suscrita a todos los tópicos, y
    escribe en la capa raw del Data Lake.
- **DLQ por cola.** Cada cola tiene su dead-letter queue. Un mensaje que falla varias veces
  pasa a la DLQ para revisarlo y reprocesarlo, en lugar de perderse o bloquear la cola.
- **Entrega al menos una vez y consumidores idempotentes.** SQS puede entregar un mensaje más
  de una vez. Cada consumidor guarda el `eventId` del [sobre común](../03-eventos/sobre-comun.md)
  y descarta los repetidos.
- **Outbox transaccional en los productores.** El servicio guarda el evento en su propia base de
  datos, en la misma transacción que el cambio de estado. Un proceso aparte lo publica en SNS.
  Si SNS no está disponible, el evento no se pierde: se publica al recuperarse.
- **Tareas programadas con EventBridge Scheduler.** Las Lambdas que se ejecutan por tiempo
  (construcción de data marts, recolocación) no dependen del bus de eventos.

Motivo principal: con servicios gestionados y baratos se cubren cinco de los mecanismos de §7.1:
colas, reintentos, DLQ, idempotencia y persistencia previa de eventos críticos.

## Consecuencias

- **Positivas:**
  - Un consumidor caído no afecta a los demás: sus mensajes esperan en su cola.
  - Las Lambdas escalan en paralelo leyendo de su cola (§7.2).
  - El fallo de un consumidor se puede demostrar fácilmente en el flujo de fallo controlado: se
    para el consumidor, se acumulan mensajes y se procesan al volver.
- **Negativas o riesgos:**
  - **Más infraestructura:** hay que mantener muchos recursos en Terraform. Conviene un módulo
    reutilizable de "cola con DLQ suscrita a tópicos".
  - **Sin orden garantizado:** SNS y SQS estándar no garantizan el orden. Si algún flujo lo
    necesita por recurso, hay que usar tópicos y colas FIFO con el identificador del recurso
    como grupo de mensajes.
  - **Outbox:** cada servicio productor necesita una tabla de outbox y un publicador.
- **Ficheros del vault afectados:**
  - [03-eventos/README.md](../03-eventos/README.md)
  - [06-estandares/eventos.md](../06-estandares/eventos.md)
  - [errores-y-resiliencia.md](../06-estandares/errores-y-resiliencia.md)
  - [infraestructura.md](../07-devops/infraestructura.md)

> PENDIENTE: decidir qué flujos necesitan orden por recurso (y por tanto FIFO).

> PENDIENTE: decidir el disparador de la expiración de reservas: una programación puntual de EventBridge Scheduler por reserva, o una cola SQS con retardo (máximo 15 minutos).

> PENDIENTE: fijar el número de reintentos antes de pasar a la DLQ (`maxReceiveCount`) y el tiempo de visibilidad.
