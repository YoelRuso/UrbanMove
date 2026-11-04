---
tipo: evento
estado: borrador
responsable: PENDIENTE
---

# Sobre común de los eventos

Todo evento debe tener un identificador, timestamp, origen, tipo, versión de esquema y un
identificador de correlación que permita seguir un flujo completo (§6).

| Campo obligatorio (§6) | Significado | Nombre del campo | Formato |
|---|---|---|---|
| Identificador | Identificador único del evento. Permite la idempotencia al reprocesar. | PENDIENTE | PENDIENTE |
| Timestamp | Momento en que ocurrió el hecho. | PENDIENTE | PENDIENTE |
| Origen | Servicio o Lambda productor. | PENDIENTE | PENDIENTE |
| Tipo | Nombre del evento, tal como figura en el [catálogo](README.md). | PENDIENTE | PENDIENTE |
| Versión de esquema | Versión del contrato del payload. | PENDIENTE | PENDIENTE |
| Identificador de correlación | Mismo valor en todo un flujo: petición de la app, eventos, logs y data marts. | PENDIENTE | PENDIENTE |

> PENDIENTE: fijar los nombres de campo y sus formatos (p. ej. tipo de identificador, zona horaria y formato del timestamp).

> PENDIENTE: decidir si se añaden campos opcionales (p. ej. identificador de causalidad, entidad afectada).

> PENDIENTE: definir dónde va el payload específico de cada evento dentro del sobre.

## Uso del identificador de correlación

- Los logs estructurados lo incluyen (§10). Ver
  [logs-y-observabilidad.md](../06-estandares/logs-y-observabilidad.md).
- El flujo de fallo controlado exige registrar el error con identificador de correlación (§11.5).

> PENDIENTE: decidir quién genera el identificador de correlación (app, gateway o primer servicio) y cómo se propaga en llamadas síncronas.

## Relacionado

- [README.md](README.md)
- [06-estandares/eventos.md](../06-estandares/eventos.md)
