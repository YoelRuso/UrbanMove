---
tipo: proyecto
estado: borrador
responsable: Joel
---

# Arquitecturas alternativas

**Son opciones para debatir, no decisiones.** Ninguna sustituye a lo que dicen las fichas, los ADR ni
las marcas `> PENDIENTE: ...` del vault.

Cada diagrama es una página HTML que se abre en el navegador, con sus pros y contras debajo. Hay que
abrirla en local: GitHub muestra el código del fichero, no la página, y Obsidian no la muestra en el
vault.

| Alternativa | Decisión que plantea | Idea |
|---|---|---|
| [A. Núcleo consistente](alternativa-a-nucleo-consistente.html) | Quién manda sobre el estado del recurso | Disponibilidad decide el estado; tomar un recurso es síncrono y el resto va por eventos |
| [B. Todo por eventos](alternativa-b-todo-por-eventos.html) | Cómo se comunican los servicios | Ningún servicio llama a otro; el sistema converge por eventos |
| [C. Una puerta por app](alternativa-c-una-puerta-por-app.html) | Cómo entran las apps | Cada app tiene su propio backend (BFF), que coordina los casos de uso |

Los pros, los contras y las valoraciones son una propuesta del agente de arquitectura, generada el
2026-11-04, para que el equipo los revise.

## Relacionado

- [vision-general.md](../vision-general.md)
- [propiedad-de-datos.md](../propiedad-de-datos.md)
- [08-adr](../../08-adr/README.md)
