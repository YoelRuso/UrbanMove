---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Glosario

## Dominio

| Término | Significado |
|---|---|
| Recurso | Bicicleta o patinete eléctrico. También se llama "vehículo" (eventos `Vehicle*`) o "activo" (en Inventario). |
| Zona | Área de la ciudad donde hay recursos. Las gestiona [Catálogo de zonas](../02-servicios/catalogo-de-zonas.md): zonas permitidas, restricciones de aparcamiento y áreas de operación. |
| Reserva | Bloqueo temporal de un recurso por parte de un usuario. Se crea, se confirma, se cancela o expira. |
| Confirmación de reserva | Paso que evita que la reserva expire (§4.3, Lambda de expiración). |
| Viaje | Uso de un recurso entre su inicio y su fin. Tiene duración, zona de origen, zona de destino y coste preliminar. |
| Incidencia | Avería, vandalismo, bloqueo, recurso desaparecido o problema reportado por usuarios o por mantenimiento. |
| Orden de mantenimiento | Trabajo de retirada, recarga, reparación, revisión, asignación o reincorporación de un recurso. |
| Orden de recolocación | Orden para mover recursos de una zona con exceso a otra con déficit. Estados mencionados: asignada, en curso, completada (§3.2). |
| Adquisición | Compra o incorporación de nuevos recursos. |
| Zona con déficit / exceso | Zona con menos o más recursos disponibles de los que pide la demanda. |
| Hotspot de demanda | Zona con demanda superior a la disponibilidad (evento `DemandHotspotDetected`). |
| Franja horaria | Ventana temporal para agregar reservas, viajes y demanda. |
| Estado administrativo | Atributo del activo en Inventario (§4.1). Su relación con los estados de §5 no está definida. |
| Estados del recurso | Ver [estados-recurso.md](../01-arquitectura/estados-recurso.md). |

## Técnico

| Término | Significado |
|---|---|
| Microservicio atómico | Servicio con una responsabilidad principal, API clara, almacenamiento propio si tiene estado, despliegue independiente y contratos explícitos (§4.1). |
| Lambda | Función serverless disparada por eventos del sistema (§4.3). |
| Evento de dominio | Hecho de negocio publicado en el bus. Ver [03-eventos](../03-eventos/README.md). |
| Bus de eventos | Cola, tópico o bus para la comunicación asíncrona. |
| Identificador de correlación | Identificador que permite seguir un flujo completo entre servicios, eventos y logs (§6, §10). |
| Data Lake | Almacén de eventos para análisis, auditoría y generación de data marts. No es una base de datos transaccional (§8). |
| Raw / Trusted / Curated | Capas del Data Lake. Ver [data-lake.md](../05-datos/data-lake.md). |
| Data mart | Tabla agregada orientada a un dominio o microservicio. Ver [data-marts.md](../05-datos/data-marts.md). |
| DLQ | Dead-letter queue: almacén de mensajes que fallan, para revisarlos o reprocesarlos. |
| Idempotencia | Propiedad por la que reprocesar un mensaje no crea duplicados. |
| Degradación funcional | Seguir ofreciendo la función principal aunque falle un componente secundario. |
| Health check | Comprobación periódica de que un servicio está vivo. |
| ADR | Architecture Decision Record. Ver [08-adr](../08-adr/README.md). |
| C4 | Modelo de diagramas de contexto, contenedores y componentes, citado en la rúbrica. |
| DevOps / CI/CD | Integración y despliegue continuos. Ver [pipeline.md](../07-devops/pipeline.md). |
