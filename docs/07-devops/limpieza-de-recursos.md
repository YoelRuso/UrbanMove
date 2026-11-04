---
tipo: devops
estado: borrador
responsable: PENDIENTE
---

# Seguridad y limpieza de recursos (§17)

No deben incluirse credenciales, tokens, claves privadas ni identificadores sensibles en el
repositorio ni en el PDF. Si se usan servicios cloud reales, el informe debe indicar qué
recursos se han creado, cuáles se han eliminado y si queda alguno activo.

## Sección obligatoria del PDF

### Recursos creados

| Recurso | Tipo | Región | Creado por | Fecha |
|---|---|---|---|---|

> PENDIENTE: rellenar a medida que se creen recursos.

### Recursos eliminados

| Recurso | Fecha de eliminación | Cómo se eliminó |
|---|---|---|

> PENDIENTE: rellenar al limpiar.

### Recursos que quedan activos

> PENDIENTE: listar los recursos activos al entregar, si los hay, y por qué.

### Coste esperado

> PENDIENTE: estimar el coste o explicar por qué no existe (p. ej. créditos de AWS Academy, LocalStack).

### Medidas para no exponer credenciales

> PENDIENTE: documentar las medidas adoptadas (gestión de secretos, gitignore, escaneo, logs sin secretos).

## Procedimiento de limpieza

> PENDIENTE: definir el procedimiento o script de destrucción de la infraestructura (p. ej. `terraform destroy`) y su verificación.

## Relacionado

- [infraestructura.md](infraestructura.md)
- [entregables.md](../00-proyecto/entregables.md)
