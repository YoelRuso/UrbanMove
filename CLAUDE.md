# UrbanMove

Proyecto final de Computación en la Nube (ULPGC) de un grupo de 3 personas: sistema distribuido de
movilidad urbana con microservicios, Lambdas, eventos, Data Lake y data marts. Cada miembro debe
poder explicar y defender cualquier parte del trabajo en una pregunta individual.

## Dónde está la información

El vault `docs/` es la base de información del proyecto y lo que hay que leer antes de trabajar.

1. Abre `docs/README.md` y lee los ficheros que su tabla "Qué leer según la tarea" indique.
2. Si dos fuentes se contradicen, manda el enunciado (`docs/urbanmove.pdf`, citado como "§N"), luego
   `docs/10-equipo/acuerdos.md`, luego los ADR de `docs/08-adr/` y por último las fichas.
3. No uses `archivo/propuesta-bloqueantes.md`: está archivada.

No copies aquí el stack, las versiones ni las normas: están en el vault.

## Cómo trabaja el equipo

- **No adelantes decisiones.** Primero la arquitectura a alto nivel; los detalles se resuelven cuando
  surgen. Ante una duda, da opciones con pros y contras.
- **Una marca `> PENDIENTE: ...` es una decisión abierta, no un hueco que rellenar.** Sustitúyela solo
  si te dicen que el equipo ya lo ha decidido.
- **Lo que afecta a un servicio** lo resuelve su responsable. **Lo que afecta a varios** lo decide el
  grupo.
- **Quien cambia un comportamiento actualiza su ficha en el mismo cambio.** Las reglas del vault están
  en `docs/README.md`.

## Límites

- Nunca escribas ni muestres credenciales o tokens, ni leas `.env` (§17).
- No hagas commit, push ni PR sin que te lo pidan. Todo entra por PR, con la aprobación de una persona
  distinta del autor: ver `docs/06-estandares/git-y-pull-requests.md`.
- En commits, PR, ramas y etiquetas no añadas `Co-authored-by` ni menciones a Claude o a agentes de IA,
  ni uses "Claude" como autor.
- No ejecutes `terraform apply` o `destroy` contra AWS ni despliegues sin que te lo pidan e indiquen el
  entorno. Los recursos activos cuestan dinero: ver `docs/07-devops/limpieza-de-recursos.md`.
- Di siempre lo que no se ha podido comprobar.

## Subagentes y skills

Se lanzan solo cuando alguien lo pide (`.claude/agents/`):

| Subagente | Para qué |
|---|---|
| `aws-microservices-architect` | Dudas de arquitectura: da opciones, no decide |
| `urbanmove-implementer` | Implementar una tarea acotada con pruebas y ficha |
| `urbanmove-reviewer` | Revisar un cambio de forma independiente, sin aprobarlo |

Las skills de `.claude/skills/` son guías genéricas y están fijadas en `skills-lock.json`. Si
contradicen el vault, manda el vault. Revisa el contenido de una skill antes de añadirla.

En Windows, las skills de `aws/agent-toolkit-for-aws` solo se instalan con rutas largas activadas:

```bash
GIT_CONFIG_COUNT=1 GIT_CONFIG_KEY_0=core.longpaths GIT_CONFIG_VALUE_0=true npx skills add aws/agent-toolkit-for-aws --skill <skill> -a claude-code --copy -y
```
