---
tipo: devops
estado: borrador
responsable: PENDIENTE
---

# Pipeline CI/CD (§10)

El repositorio debe incluir una práctica DevOps visible y reproducible. No basta con tener
código que funcione manualmente: hay que demostrar cómo se construye, prueba y despliega el
sistema.

## Mínimos del pipeline (§10)

- [ ] Ejecutar pruebas automáticas de varios microservicios en cada cambio.
- [ ] Construir imágenes Docker para los microservicios desplegables o, al menos, para los
      servicios críticos.
- [ ] Validar formato, estilo o análisis estático de código.
- [ ] Empaquetar o desplegar Lambdas mediante comandos versionados.
- [ ] Ejecutar migraciones, semillas de datos o preparación de infraestructura de forma
      documentada.
- [ ] Publicar artefactos, logs de pipeline, capturas o evidencias de ejecución.
- [ ] Evitar imprimir credenciales o secretos en los logs.

Entregable: evidencia de CI/CD funcionando, con ejecución de pruebas, construcción de imágenes
o artefactos y validaciones automáticas (§13.11).

## Decisiones

La plataforma de CI/CD es **GitHub Actions**. Se propone que las pruebas de integración usen LocalStack
con un token de CI guardado como secreto del repositorio, pendiente en
[tests.md](../06-estandares/tests.md)
([ADR 0001](../08-adr/0001-emulacion-local-de-aws-con-localstack.md)).

> PENDIENTE: definir las etapas y disparadores (push, PR, rama principal, etiquetas).

> PENDIENTE: decidir si el pipeline solo construye los servicios que cambian o todos.

> PENDIENTE: elegir el registro de imágenes (ECR es una ampliación valorable, §15).

> PENDIENTE: elegir las herramientas de lint y análisis estático.

> PENDIENTE: definir la gestión de secretos en el pipeline.

> PENDIENTE: decidir si el pipeline despliega automáticamente y a qué entorno.

## Relacionado

- [tests.md](../06-estandares/tests.md)
- [despliegue.md](despliegue.md)
- [11-evidencias/README.md](../11-evidencias/README.md)
