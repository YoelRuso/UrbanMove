---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# UrbanMove: vault de contexto del proyecto

Este vault es la base de información compartida del grupo y de los agentes de IA, y la
fuente de la documentación del entregable final. La única fuente de verdad es el enunciado:
[urbanmove.pdf](urbanmove.pdf). Las referencias con la forma "§N" remiten a sus secciones.

## Mapa del vault

| Carpeta | Contenido |
|---|---|
| [00-proyecto](00-proyecto/resumen.md) | Qué es UrbanMove, mínimos, rúbrica, ampliaciones, entregables y glosario |
| [01-arquitectura](01-arquitectura/vision-general.md) | Visión general, propiedad de datos, estados del recurso y apps cliente |
| [02-servicios](02-servicios/README.md) | Una ficha por microservicio |
| [03-eventos](03-eventos/README.md) | Catálogo de eventos de dominio y sobre común |
| [04-lambdas](04-lambdas/README.md) | Una ficha por función Lambda |
| [05-datos](05-datos/data-lake.md) | Data Lake (capas y particionado) y data marts |
| [06-estandares](06-estandares/api.md) | Normas de API, eventos, logs, resiliencia, tests y git |
| [07-devops](07-devops/pipeline.md) | Entorno local, pipeline, infraestructura, despliegue y limpieza |
| [08-adr](08-adr/README.md) | Decisiones arquitectónicas (ADR) |
| [09-flujos](09-flujos/flujo-usuario.md) | Los cinco flujos obligatorios de la demostración |
| [10-equipo](10-equipo/reparto.md) | Reparto de trabajo y acuerdos del grupo |
| [11-evidencias](11-evidencias/README.md) | Evidencias que pide el enunciado y dónde guardarlas |

## Qué leer según la tarea

| Tarea | Ficheros (en este orden) |
|---|---|
| Implementar o modificar un microservicio | Su ficha en [02-servicios](02-servicios/README.md), [api.md](06-estandares/api.md), [propiedad-de-datos.md](01-arquitectura/propiedad-de-datos.md), [errores-y-resiliencia.md](06-estandares/errores-y-resiliencia.md) |
| Tocar el ciclo de vida de un recurso | [estados-recurso.md](01-arquitectura/estados-recurso.md), [03-eventos/README.md](03-eventos/README.md), ficha del servicio que valida la transición |
| Crear una Lambda | Su ficha en [04-lambdas](04-lambdas/README.md), [03-eventos/README.md](03-eventos/README.md), [errores-y-resiliencia.md](06-estandares/errores-y-resiliencia.md), [pipeline.md](07-devops/pipeline.md) |
| Añadir o cambiar un evento | [03-eventos/README.md](03-eventos/README.md), [sobre-comun.md](03-eventos/sobre-comun.md), [06-estandares/eventos.md](06-estandares/eventos.md), fichas del productor y de los consumidores |
| Trabajar en Data Lake o data marts | [data-lake.md](05-datos/data-lake.md), [data-marts.md](05-datos/data-marts.md), [ingesta-analitica.md](04-lambdas/ingesta-analitica.md), [construccion-de-data-marts.md](04-lambdas/construccion-de-data-marts.md) |
| Trabajar en el dashboard | [apps-cliente.md](01-arquitectura/apps-cliente.md), [analitica-operacional.md](02-servicios/analitica-operacional.md), [data-marts.md](05-datos/data-marts.md), [flujo-dashboard.md](09-flujos/flujo-dashboard.md) |
| Tocar el pipeline CI/CD | [pipeline.md](07-devops/pipeline.md), [tests.md](06-estandares/tests.md), [git-y-pull-requests.md](06-estandares/git-y-pull-requests.md) |
| Desplegar o crear infraestructura | [infraestructura.md](07-devops/infraestructura.md), [despliegue.md](07-devops/despliegue.md), [limpieza-de-recursos.md](07-devops/limpieza-de-recursos.md) |
| Levantar el sistema en local | [entorno-local.md](07-devops/entorno-local.md) |
| Registrar una decisión arquitectónica | [08-adr/README.md](08-adr/README.md), [_plantilla.md](08-adr/_plantilla.md) |
| Preparar la demo o la defensa | [09-flujos](09-flujos/flujo-usuario.md), [rubrica.md](00-proyecto/rubrica.md), [requisitos-minimos.md](00-proyecto/requisitos-minimos.md), [11-evidencias/README.md](11-evidencias/README.md) |
| Redactar el PDF final | [entregables.md](00-proyecto/entregables.md), [11-evidencias/README.md](11-evidencias/README.md), [reparto.md](10-equipo/reparto.md) |

## Reglas para mantener el vault

1. **Quien cambia el comportamiento de un servicio actualiza su ficha en el mismo cambio**
   (API, eventos, almacenamiento y dependencias). Lo mismo vale para Lambdas, eventos y estados.
2. Una decisión de equipo se registra sustituyendo la marca `> PENDIENTE: ...` por el valor
   decidido. Si la decisión es arquitectónica, se crea además un ADR en [08-adr](08-adr/README.md)
   y se enlaza desde la ficha.
3. No se duplica información: se enlaza el fichero que ya la contiene.
4. Un tema por fichero, con un máximo de unas 150 líneas. Si crece, se divide.
5. Nombres de fichero en kebab-case, sin tildes ni espacios. Enlaces Markdown relativos, sin
   wikilinks ni sintaxis de plugins.
6. Nombres de eventos y estados en inglés, tal como aparecen en el enunciado.
7. Todo fichero lleva el frontmatter `tipo`, `estado` y `responsable`. Al revisarlo, `estado`
   pasa de `borrador` a `revisado`.
8. No se guardan credenciales, tokens ni identificadores sensibles en el vault (§17).
