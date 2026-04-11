# Plantilla de branch por tarea/feature

## Inputs

- Proyecto: `PRJ-2026-001`
- Tarea o feature: `<tarea-kebab>`
- Versión: `v<N>`

## Nombre final

`feature/prj-2026-001/<tarea-kebab>-v<N>`

## Comandos estándar

```bash
git checkout develop
git pull origin develop
git checkout -b feature/prj-2026-001/<tarea-kebab>-v<N>
git push -u origin feature/prj-2026-001/<tarea-kebab>-v<N>
```

## Registro en plan

Agregar al plan activo:

```md
## Feature de implementación
- branch: feature/prj-2026-001/<tarea-kebab>-v<N>
- creada: <YYYY-MM-DD>
- alcance: <tarea concreta y verificable>
```