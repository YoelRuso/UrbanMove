---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Visión general de la arquitectura

## Principios exigidos (§4)

- La solución está formada por **microservicios independientes**, **funciones Lambda** y una
  **capa analítica basada en eventos**.
- Servicios pequeños, con bajo acoplamiento y una responsabilidad principal por servicio. La
  cantidad exacta de componentes puede variar, pero la separación de responsabilidades debe
  ser clara.
- **Tolerante a fallos**: el fallo temporal de un componente no debe romper todo el sistema.
- **Escalable**: los componentes con más carga deben poder crecer de forma independiente.
- La capa analítica está separada de los microservicios operacionales. Los microservicios no
  usan el Data Lake como base de datos transaccional (§8).

## Componentes

| Capa | Componentes | Detalle |
|---|---|---|
| Clientes | App de usuarios finales, app de mantenimiento y operaciones, dashboard operativo | [apps-cliente.md](apps-cliente.md) |
| Microservicios | 15 servicios descritos en §4.1 (mínimo 10) | [02-servicios](../02-servicios/README.md) |
| Mensajería | Bus, cola o tópico de eventos de dominio | [03-eventos](../03-eventos/README.md) |
| Serverless | 5 Lambdas descritas en §4.3 (mínimo 3) | [04-lambdas](../04-lambdas/README.md) |
| Analítica | Data Lake (raw/trusted/curated) y data marts | [data-lake.md](../05-datos/data-lake.md), [data-marts.md](../05-datos/data-marts.md) |

## Cómo se relacionan (según el enunciado)

1. Las apps cliente consumen las APIs de los microservicios.
2. Los microservicios emiten **eventos de dominio**. Esos eventos alimentan procesos
   asíncronos, Lambdas, el historial, el Data Lake y los data marts (§6).
3. La Lambda de ingesta copia o transforma eventos hacia el Data Lake (§4.3).
4. La Lambda de construcción de data marts actualiza tablas agregadas (§4.3).
5. Analítica operacional expone consultas agregadas a partir de los data marts y alimenta el
   dashboard (§4.1).
6. Los indicadores de demanda generan órdenes de recolocación, que la app de mantenimiento
   consulta y completa (§8.3, §11.3).
7. Historial es un servicio independiente que consulta el histórico de reservas, viajes,
   incidencias, mantenimiento y operaciones (§4.1).

## Decisiones abiertas

El bus de eventos es SNS + SQS (ver [ADR 0002](../08-adr/0002-bus-de-eventos-con-sns-y-sqs.md)).

> PENDIENTE: decidir si existe un API Gateway o un BFF delante de los microservicios.

> PENDIENTE: decidir la comunicación entre servicios (síncrona, asíncrona o mixta) en cada interacción.

> PENDIENTE: decidir qué sistemas externos simulados existen (p. ej. pagos o facturación simulada, telemetría) y sus límites.

Los microservicios se escriben en Java con Spring Boot y Maven, y las Lambdas en Python. Cada
servicio con estado tiene su propia base de datos PostgreSQL dentro de una instancia RDS
compartida
([ADR 0003](../08-adr/0003-una-instancia-rds-con-una-base-de-datos-por-servicio.md)). Ver
[infraestructura.md](../07-devops/infraestructura.md).

## Diagramas requeridos (§4.2, §13)

- Vista de contexto: actores, apps cliente, sistemas externos simulados y límites del sistema.

  > PENDIENTE: diagrama de contexto (hueco).

- Vista de contenedores o despliegue: microservicios, Lambdas, bases de datos, bus de
  eventos, Data Lake y data marts.

  > PENDIENTE: diagrama de contenedores o despliegue (hueco).

- Diagrama de arquitectura con apps cliente, dashboard, microservicios atómicos, Lambdas, bus
  de eventos, Data Lake y data marts (§13.4).

  > PENDIENTE: diagrama de arquitectura general (hueco).

## Relacionado

- [propiedad-de-datos.md](propiedad-de-datos.md)
- [estados-recurso.md](estados-recurso.md)
- [infraestructura.md](../07-devops/infraestructura.md)
- [08-adr](../08-adr/README.md)
