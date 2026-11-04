---
tipo: proyecto
estado: borrador
responsable: PENDIENTE
---

# Resumen de UrbanMove

Proyecto final de **Computación en la Nube** (Grado en Ingeniería Informática, ULPGC).

## Qué es

Un sistema distribuido para una empresa de movilidad urbana que gestiona **bicicletas y
patinetes eléctricos** repartidos por zonas de la ciudad (§1, §2).

- Los usuarios pueden registrarse, consultar recursos cercanos, reservar uno, iniciar un
  viaje, finalizarlo y dejar el recurso en una zona permitida.
- El personal de mantenimiento puede retirar recursos para recarga, reparación o revisión, y
  volver a ponerlos a disposición de los usuarios.
- El sistema recoge eventos de uso y operación en un **Data Lake**. A partir de ellos se
  construyen **data marts** que sirven para analizar patrones de uso y generar **órdenes de
  recolocación**.

El objetivo no es una aplicación comercial completa, sino una arquitectura académica para
practicar microservicios atómicos, Lambdas, comunicación asíncrona, almacenamiento operacional,
Data Lake, data marts, analítica de demanda, tolerancia a fallos, escalabilidad,
observabilidad, documentación arquitectónica y DevOps (§1).

## Piezas principales

| Pieza | Detalle |
|---|---|
| 3 interfaces cliente | [apps-cliente.md](../01-arquitectura/apps-cliente.md) |
| Al menos 10 microservicios atómicos | [02-servicios](../02-servicios/README.md) |
| Al menos 3 Lambdas | [04-lambdas](../04-lambdas/README.md) |
| Eventos de dominio y bus | [03-eventos](../03-eventos/README.md) |
| Data Lake raw/trusted/curated | [data-lake.md](../05-datos/data-lake.md) |
| Al menos 4 data marts | [data-marts.md](../05-datos/data-marts.md) |

## Grupo

Grupos de dos o tres personas; el nuestro tiene **3 integrantes**. Todos deben participar en
código, arquitectura, despliegue, pruebas, documentación y defensa (§1, §12). Ver
[reparto.md](../10-equipo/reparto.md).

## Defensa

Unos 10 minutos por grupo: demostración de los cinco flujos obligatorios, explicación de la
arquitectura y preguntas individuales (§18). Ver [09-flujos](../09-flujos/flujo-usuario.md).

## Plataforma

El enunciado permite AWS Academy, AWS real, LocalStack o un entorno local equivalente, y pide
justificar la decisión en el PDF (§9). El equipo desarrolla en local con LocalStack, prueba en
AWS Academy y despliega para la defensa en AWS real (ver
[despliegue.md](../07-devops/despliegue.md)).

## Relacionado

- [requisitos-minimos.md](requisitos-minimos.md)
- [rubrica.md](rubrica.md)
- [entregables.md](entregables.md)
- [vision-general.md](../01-arquitectura/vision-general.md)
