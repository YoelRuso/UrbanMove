---
tipo: servicio
estado: borrador
responsable: Oussama
---

# Identidad

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | No |

## 1. Responsabilidad

Gestiona autenticación, sesiones, tokens y roles básicos. Debe separar usuarios finales,
mantenimiento y administración.

## 2. Qué NO hace

- No gestiona datos de usuario, preferencias ni baja lógica: eso es de
  [Perfiles de usuario](perfiles-de-usuario.md), que a su vez no emite tokens ni controla
  sesiones.

## 3. Datos de los que es dueño

Credenciales, sesiones, tokens y roles (usuario final, mantenimiento, administración).

> PENDIENTE: definir el modelo de datos.

## 4. API

> PENDIENTE: definir endpoints de registro, inicio de sesión, validación de token y gestión de roles (métodos, payloads y códigos).

## 5. Eventos que publica

`UserRegistered` ("Alta de usuario y creación de perfil") está relacionado con este servicio.

> PENDIENTE: decidir si `UserRegistered` lo publica Identidad o Perfiles de usuario.

## 6. Eventos que consume

> PENDIENTE: definir si consume algún evento.

## 7. Dependencias de otros servicios

> PENDIENTE: definir cómo validan los demás servicios los tokens y si Identidad llama a Perfiles al registrar.

## 8. Almacenamiento

PostgreSQL, con una base de datos propia ([acuerdos.md](../10-equipo/acuerdos.md)).

## 9. Decisiones y notas

- Los "roles separados para usuarios y mantenimiento" figuran también como ampliación valorable
  (§15), aunque la responsabilidad de §4.1 ya pide separar los tres tipos de usuario.

> PENDIENTE: decidir el mecanismo de autenticación (propio, Cognito u otro) y el formato del token.

## 10. Relacionado

- [perfiles-de-usuario.md](perfiles-de-usuario.md)
- [apps-cliente.md](../01-arquitectura/apps-cliente.md)
- [flujo-usuario.md](../09-flujos/flujo-usuario.md)
