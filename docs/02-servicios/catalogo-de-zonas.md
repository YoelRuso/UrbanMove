---
tipo: servicio
estado: borrador
responsable: Joel
---

# Catálogo de zonas

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| No | No |

## 1. Responsabilidad

Mantiene zonas permitidas, restricciones de aparcamiento, áreas de operación y metadatos
geográficos simplificados.

## 2. Qué NO hace

- No dice qué recursos hay ni cuáles están disponibles en una zona: eso es de
  [Disponibilidad](disponibilidad.md).
- No calcula déficit ni exceso por zona: eso es de la capa analítica
  ([data-marts.md](../05-datos/data-marts.md)).

## 3. Datos de los que es dueño

Zonas, restricciones de aparcamiento, áreas de operación y metadatos geográficos simplificados.

> PENDIENTE: definir el modelo de zona y el nivel de simplificación geográfica.

## 4. API

> PENDIENTE: definir endpoints de consulta de zonas y validación de zona permitida.

## 5. Eventos que publica

El enunciado no asocia ningún evento a este servicio.

> PENDIENTE: decidir si publica eventos (p. ej. cambios de zona).

## 6. Eventos que consume

> PENDIENTE: definir si consume algún evento.

## 7. Dependencias de otros servicios

> PENDIENTE: definir qué servicios lo consultan (p. ej. Viajes para validar la zona de destino).

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

- El usuario debe dejar el recurso "en una zona permitida" (§2).

> PENDIENTE: decidir si se implementa o si las zonas se gestionan como datos estáticos o semilla.

## 10. Relacionado

- [disponibilidad.md](disponibilidad.md)
- [viajes.md](viajes.md)
