---
tipo: servicio
estado: borrador
responsable: Oussama
---

# Perfiles de usuario

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | No |

## 1. Responsabilidad

Gestiona datos de usuario, preferencias, validación básica y baja lógica.

## 2. Qué NO hace

- No debe emitir tokens ni controlar sesiones: eso es de [Identidad](identidad.md).

## 3. Datos de los que es dueño

Datos de usuario y preferencias, incluido el estado de baja lógica.

> PENDIENTE: definir el modelo de datos del perfil.

## 4. API

> PENDIENTE: definir endpoints para consultar, crear, actualizar y dar de baja un perfil (métodos, payloads y códigos).

## 5. Eventos que publica

`UserRegistered` ("Alta de usuario y creación de perfil") está relacionado con este servicio.

> PENDIENTE: decidir si `UserRegistered` lo publica Perfiles o Identidad, y si la baja lógica emite un evento.

## 6. Eventos que consume

> PENDIENTE: decidir si el perfil se crea consumiendo `UserRegistered` o con una llamada síncrona.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias (p. ej. con Identidad para autorizar).

## 8. Almacenamiento

PostgreSQL, con una base de datos propia ([acuerdos.md](../10-equipo/acuerdos.md)).

## 9. Decisiones y notas

- Alimenta el data mart de Usuarios ("¿Cuántos usuarios activos hay por período?"), ver
  [data-marts.md](../05-datos/data-marts.md).

## 10. Relacionado

- [identidad.md](identidad.md)
- [historial.md](historial.md)
