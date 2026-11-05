---
tipo: estandar
estado: borrador
responsable: Joel
---

# Git y pull requests

## Lo que dice el enunciado

- Se entrega un repositorio GitHub con todo el código fuente (§13.1).
- Se recomienda un **monorepo** con carpetas independientes por servicio, por ejemplo
  `services/reservations`, `services/rides`, `services/history`, `lambdas/`, `infra/` y `docs/`
  (§10).
- Si el grupo usa varios repositorios, debe justificarlo y documentar cómo se versionan
  conjuntamente (§10).
- No deben incluirse credenciales, tokens, claves privadas ni identificadores sensibles en el
  repositorio (§17).
- El reparto de trabajo debe estar documentado (§1). El historial de git sirve como evidencia de
  participación.

## Repositorio: monorepo

Repositorio privado: <https://github.com/YoelRuso/UrbanMove>.

Un único repositorio GitHub con esta estructura (provisional):

```text
urbanmove/
├── services/            # un proyecto Spring Boot (Maven) por microservicio
│   ├── reservas/
│   ├── viajes/
│   └── ...
├── lambdas/             # una carpeta por Lambda (Python)
├── apps/
│   ├── usuarios/        # React + Vite
│   ├── mantenimiento/
│   └── dashboard/
├── infra/               # Terraform
├── docs/                # este vault
├── docker-compose.yml
├── .env.example
└── .github/workflows/   # GitHub Actions
```

> PENDIENTE: decidir si hay un `pom.xml` agregador en la raíz o cada servicio se construye por separado.

> PENDIENTE: decidir dónde viven los contratos compartidos (JSON Schema de eventos, OpenAPI), p. ej. una carpeta `contracts/`.

## Modelo de ramas: Gitflow

| Rama | Sale de | Se fusiona en | Uso |
|---|---|---|---|
| `main` | — | — | Versión entregable. Solo recibe fusiones de `release/*` y `hotfix/*`. Cada fusión lleva una etiqueta de versión. |
| `develop` | `main` | — | Integración del trabajo en curso. |
| `feat/<descripcion>` | `develop` | `develop` | Una funcionalidad o tarea. |
| `fix/<descripcion>` | `develop` | `develop` | Corrección de un error que todavía no está en `main`. |
| `release/<version>` | `develop` | `main` y `develop` | Preparación de una versión al final de cada sprint. |
| `hotfix/<version>` | `main` | `main` y `develop` | Corrección urgente de un error que ya está en `main`. |

Ni `main` ni `develop` reciben commits directos: todo entra por pull request.

## Versiones

Se usa versionado semántico, con una sola versión para todo el monorepo:

| Momento | Versión |
|---|---|
| Fin del sprint 1 | `v0.1.0` |
| Fin del sprint 2 | `v0.2.0` |
| Fin del sprint 3 | `v0.3.0` |
| Fin del sprint 4 | `v0.4.0` |
| Versión de la defensa | `v1.0.0` |
| Hotfix sobre una versión | Sube el último número (`v0.2.0` → `v0.2.1`) |

Las imágenes Docker que publica el pipeline usan la misma etiqueta.

## Cómo se hace una release

Al cerrar cada sprint:

1. **Crear la rama** desde `develop` actualizado:

   ```bash
   git switch develop
   git pull
   git switch -c release/0.1.0
   git push -u origin release/0.1.0
   ```

2. **Estabilizar.** En la rama `release/*` solo entran correcciones, mediante PR contra
   `release/0.1.0`. Las funcionalidades nuevas siguen entrando en `develop`, para el sprint
   siguiente.
3. **Fusionar en `main`.** Se abre un PR de `release/0.1.0` a `main`. Se fusiona con
   *merge commit*, no con *squash*, para que `main` y `develop` compartan historial.
4. **Etiquetar** el commit de fusión de `main` y publicar la release en GitHub:

   ```bash
   git switch main
   git pull
   git tag -a v0.1.0 -m "Sprint 1"
   git push origin v0.1.0
   ```

   En GitHub: *Releases* → *Draft a new release* → elegir `v0.1.0` → *Generate release notes*.
   Las notas generadas y las evidencias del pipeline sirven para el PDF.
5. **Devolver las correcciones a `develop`.** Se abre un PR de `release/0.1.0` a `develop`.
6. **Borrar la rama** `release/0.1.0`.

Un **hotfix** sigue el mismo camino, pero sale de `main` (`hotfix/0.1.1`), se fusiona en `main`
con su etiqueta y después se devuelve a `develop`.

## Pull requests

- **Aprobaciones:** al menos una, de alguien distinto del autor.
- **Checks obligatorios:** el pipeline debe pasar antes de fusionar.
- **Protección de ramas:** `main` y `develop` están protegidas en GitHub: exigen PR y una
  aprobación, y no admiten force push ni borrado. El pipeline en verde se exigirá cuando exista.
- **Estrategia de fusión:**
  - `feat/*` y `fix/*` → `develop`: *squash*, un commit por tarea.
  - `release/*` y `hotfix/*` → `main` y `develop`: *merge commit*.

> PENDIENTE: definir la plantilla de PR (qué se cambia, cómo se ha probado, fichas del vault actualizadas).

> PENDIENTE: confirmar la convención de mensajes de commit. Propuesta: Conventional Commits (`feat: ...`, `fix: ...`, `docs: ...`), coherente con los nombres de rama.

> PENDIENTE: decidir si se añade escaneo de secretos. `.gitignore` ya excluye `.env`, y `.env.example` está en el repositorio.

## Regla del vault

Todo PR que cambie el comportamiento de un servicio, una Lambda, un evento o un estado
actualiza su ficha en este vault en el mismo PR. Ver [README](../README.md).

## Relacionado

- [pipeline.md](../07-devops/pipeline.md)
- [acuerdos.md](../10-equipo/acuerdos.md)
