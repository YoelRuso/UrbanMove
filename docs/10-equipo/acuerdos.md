---
tipo: equipo
estado: borrador
responsable: PENDIENTE
---

# Acuerdos de trabajo del grupo

## Ya acordado

- El grupo tiene tres integrantes y desarrolla con ayuda de agentes de IA.
- Este vault es la base de información común y la fuente de la documentación del entregable.
- Quien cambia el comportamiento de un componente actualiza su ficha en el mismo cambio (ver
  [README](../README.md)).
- Las decisiones pendientes se marcan con `> PENDIENTE: ...` y no se inventan.
- Forma de trabajo (4 de noviembre de 2026): primero se define la arquitectura de
  microservicios a alto nivel (qué servicios hay, qué hace cada uno, quién se comunica con
  quién y qué app usa qué). Los detalles técnicos (estados, eventos, API, pipeline...) no se
  deciden por adelantado: cada miembro los resuelve en sus servicios a medida que aparecen y
  solo se llevan al grupo las decisiones que afectan a varios. Los agentes de IA no adelantan
  decisiones: ante una duda dan opciones con pros y contras.
- [propuesta-bloqueantes.md](propuesta-bloqueantes.md) está archivada: no es la línea vigente
  y nada de lo que contiene está acordado.

- Stack, ramas y plataforma acordados en la reunión del 27 de octubre de 2026:
  - Microservicios en Java con Spring Boot y Maven. Lambdas en Python.
  - Monorepo con Gitflow y una aprobación por PR.
  - Tres apps React separadas, creadas con Vite.
  - PostgreSQL, con una base de datos por servicio (si la necesita).
  - Docker, GitHub Actions y Terraform.
  - LocalStack (Student Plan) en local.
  - Pruebas parciales en el sandbox de AWS Academy y despliegue completo para la defensa en
    una cuenta de AWS normal.
  - Ver [infraestructura.md](../07-devops/infraestructura.md) y
    [git-y-pull-requests.md](../06-estandares/git-y-pull-requests.md).

## Versiones

Se usan las últimas versiones estables al crear el repositorio y se fijan en él (`pom.xml`,
`package.json`, `required_version` de Terraform, imagen de LocalStack). Solo se actualizan por
PR.

Referencia a fecha de 2026-10-27, que hay que comprobar al crear el repositorio:

| Pieza | Versión |
|---|---|
| Java | 21 (acordado en la reunión). La última LTS es Java 25 |
| Spring Boot | 4.1.x |
| Python (Lambdas) | 3.14, el runtime más reciente de Lambda |
| Terraform | 1.16.x |
| Node.js | La LTS vigente |
| LocalStack | 2026.10.3 |

> PENDIENTE: decidir si se mantiene Java 21 o se pasa a Java 25 (LTS más reciente, compatible con Spring Boot 4.1).

## Calendario

Planificación aproximada en sprints de dos semanas:

| Sprint | Objetivo | Fin |
|---|---|---|
| 1 | Las bases: servicios iniciales, infraestructura local, pipeline e interfaces muy básicas para comprobar que todo funciona | 2026-11-15 |
| 2 | Pulir la base | 2026-11-29 |
| 3 | Interfaces: versiones más completas y cuidadas de las tres apps | 2026-12-13 |
| 4 | Servicios opcionales | 2026-12-27 |

La defensa se espera en enero de 2027.

> PENDIENTE: confirmar la fecha de entrega del PDF y de la defensa.

> PENDIENTE: fijar la fecha de congelación de código y el margen para el PDF y la defensa.

## Por acordar

> PENDIENTE: definir el canal de comunicación y la frecuencia de reuniones o puntos de sincronización.

> PENDIENTE: definir la herramienta de seguimiento de tareas.

> PENDIENTE: definir las normas de uso de agentes de IA (qué ficheros del vault se les pasan, revisión humana obligatoria del código generado).

> PENDIENTE: definir el proceso para tomar decisiones de arquitectura (quién propone, quién aprueba, cuándo se crea un ADR).

> PENDIENTE: definir la "definición de hecho" de una tarea (tests, ficha actualizada, pipeline en verde...).

> PENDIENTE: definir cómo se prepara la defensa individual de cada miembro.

## Relacionado

- [reparto.md](reparto.md)
- [git-y-pull-requests.md](../06-estandares/git-y-pull-requests.md)
