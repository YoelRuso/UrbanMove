---
tipo: servicio
estado: borrador
responsable: Sergio
---

# Viajes

| Obligatorio para aprobar (§14) | Fusión prohibida (§4.1) |
|---|---|
| Sí | **Sí** |

## 1. Responsabilidad

Gestiona el inicio y el fin de uso. Calcula duración, zona de origen, zona de destino y coste
preliminar.

## 2. Qué NO hace

- No crea ni cancela reservas: [Reservas](reservas.md).
- No es el lugar de consulta del histórico: [Historial](historial.md).

## 3. Datos de los que es dueño

Viaje: recurso, usuario, inicio, fin, duración, zona de origen, zona de destino y coste
preliminar.

> PENDIENTE: definir el modelo de datos y la fórmula del coste preliminar.

## 4. API

> PENDIENTE: definir endpoints para iniciar un viaje (con reserva o con recurso disponible, §3.1), finalizarlo indicando la zona de destino y consultarlo.

## 5. Eventos que publica

Eventos del catálogo relacionados con esta responsabilidad: `RideStarted` ("Inicio de uso de un
recurso") y `RideFinished` ("Finalización del viaje y liberación o cambio de estado del recurso").

> PENDIENTE: confirmar que Viajes publica `RideStarted` y `RideFinished`.

## 6. Eventos que consume

> PENDIENTE: definir si consume algún evento.

## 7. Dependencias de otros servicios

> PENDIENTE: definir las dependencias (Reservas, Disponibilidad, Catálogo de zonas) con timeout y comportamiento ante fallo.

## 8. Almacenamiento

> PENDIENTE: elegir la tecnología de almacenamiento.

## 9. Decisiones y notas

- Debe poder escalar horizontalmente (§7.2).
- La analítica de demanda no debe bloquear el inicio ni el fin de viaje (§7.2).
- Ejemplo de degradación funcional: permitir finalizar un viaje aunque el servicio de
  recomendaciones no esté disponible (§7.1).
- Candidato a vista de componentes en el PDF (§4.2) y a diagrama de secuencia de inicio de viaje.
- La sección 2 menciona la "facturación simulada" como posible data mart; aquí solo se calcula
  un coste preliminar.

## 10. Relacionado

- [reservas.md](reservas.md)
- [catalogo-de-zonas.md](catalogo-de-zonas.md)
- [flujo-usuario.md](../09-flujos/flujo-usuario.md)
