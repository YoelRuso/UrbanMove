---
tipo: estandar
estado: borrador
responsable: PENDIENTE
---

# Tests

## Lo que exige el enunciado

- El pipeline ejecuta pruebas automáticas de varios microservicios en cada cambio (§10).
- Todos los miembros participan en las pruebas (§1). El reparto orientativo asigna a cada
  persona las "pruebas asociadas" a sus servicios (§12).
- El PDF documenta las pruebas (§13.2).
- Al menos dos escenarios de fallo probados o simulados (§7.1). Ver
  [errores-y-resiliencia.md](errores-y-resiliencia.md).
- Ampliación: pruebas de carga con Locust sobre reservas o viajes (§15).

## Normas

> PENDIENTE: definir los tipos de prueba obligatorios por servicio (unitarias, integración, contrato, extremo a extremo).

> PENDIENTE: elegir el framework de pruebas según el lenguaje.

> PENDIENTE: decidir si se exige una cobertura mínima.

> PENDIENTE: decidir cómo se prueban las Lambdas y la integración con el bus. Propuesta: pruebas de integración contra LocalStack ([ADR 0001](../08-adr/0001-emulacion-local-de-aws-con-localstack.md)), sin persistencia en el CI.

> PENDIENTE: definir los datos de prueba y las semillas.

> PENDIENTE: definir qué casos críticos deben tener test (p. ej. doble reserva, expiración, transiciones de estado inválidas, evento duplicado).

## Relacionado

- [pipeline.md](../07-devops/pipeline.md)
- [estados-recurso.md](../01-arquitectura/estados-recurso.md)
