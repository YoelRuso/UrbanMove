---
tipo: estandar
estado: borrador
responsable: PENDIENTE
---

# Logs y observabilidad (§10)

La observabilidad debe permitir diagnosticar un flujo completo desde la app de usuarios o de
mantenimiento hasta los eventos y los data marts.

## Mínimos (§10)

- [ ] Logs estructurados con identificador de correlación.
- [ ] Métricas de reservas, viajes, recursos disponibles y órdenes de mantenimiento.
- [ ] Evidencia de eventos enviados y consumidos.
- [ ] Consulta o captura de algún data mart generado.
- [ ] Dashboard operativo con indicadores funcionales y técnicos, actualizados durante la
      demostración.

## Requisitos relacionados

- El dashboard muestra indicadores de salud: servicios activos, errores recientes o eventos
  fallidos (§3.3).
- Health checks, reinicios automáticos o alarmas para detectar fallos (§9).
- En el fallo controlado, el sistema registra el error con identificador de correlación (§11.5).
- No se imprimen credenciales ni secretos en los logs (§10).
- Entregable: evidencia de observabilidad con logs, métricas, trazas, paneles o capturas
  explicadas (§13.12).
- Pregunta de defensa: "¿Cómo se diagnostica un fallo entre microservicios?" (§18).

## Normas

> PENDIENTE: definir el formato de log estructurado (campos obligatorios: timestamp, nivel, servicio, correlación...).

> PENDIENTE: elegir la herramienta de logs y métricas (CloudWatch u otra) y decidir si hay trazas distribuidas.

> PENDIENTE: definir los nombres y dimensiones de las métricas mínimas.

> PENDIENTE: definir alarmas, si las hay.

> PENDIENTE: definir cómo se evidencian los eventos enviados y consumidos.

## Relacionado

- [sobre-comun.md](../03-eventos/sobre-comun.md)
- [apps-cliente.md](../01-arquitectura/apps-cliente.md)
- [11-evidencias/README.md](../11-evidencias/README.md)
