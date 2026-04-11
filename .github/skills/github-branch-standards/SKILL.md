---
name: github-branch-standards
description: "Estandariza ramas GitHub para ejecución de planes y tareas. Úsala cuando: se aprueba o implementa un plan nuevo, se crea una tarea derivada de roadmap, se pide crear branch para trabajo. Invoca automáticamente al detectar: github, branch, rama, plan, implementar plan, tarea nueva, flujo git."
argument-hint: "Indica el identificador del plan y el tema corto (ej: PRJ-2026-001, alta-fidelidad-tabla)."
---

# GitHub Branch Standards Skill

## Objetivo

Forzar un flujo consistente de ramas para que cada tarea implementable se ejecute como una feature dedicada, trazable y alineada con GitFlow del proyecto.

## Cuándo usar esta skill

- Cuando se aprueba un plan y comienza su implementación.
- Cuando un roadmap genera una tarea nueva.
- Cuando el usuario pida explícitamente crear o normalizar ramas GitHub.

## Regla principal

Cada tarea implementable debe tener su propia feature branch antes de cualquier cambio de archivos.

## Modelo Git adoptado

- `main`: rama estable.
- `develop`: rama de integración.
- `feature/*`: trabajo regular por tarea.
- `fix/*`: correcciones sobre una feature ya creada.
- `chore/*`: gobierno, tooling, CI, documentación operativa.
- `hotfix/*`: urgencias que nacen desde `main`.

## Convención de nombres de ramas

Usar siempre para trabajo por tarea:

`feature/prj-2026-001/<tarea-kebab>-v<N>`

Ejemplos:
- `feature/prj-2026-001/mantenedor-registros-v1`
- `feature/prj-2026-001/engram-memory-protocol-v1`

Para otros tipos de trabajo:
- `fix/prj-2026-001/<tema-kebab>-v<N>`
- `chore/prj-2026-001/<tema-kebab>-v<N>`
- `hotfix/prj-2026-001/<tema-kebab>-v<N>`

## Flujo obligatorio

### Paso 1 - Sincronizar base

1. `git checkout develop`
2. `git pull origin develop`

### Paso 2 - Crear rama de la tarea

1. Derivar `<tarea-kebab>` desde la tarea aprobada.
2. Incrementar versión `v<N>` si existe antecedente del mismo tema.
3. Ejecutar:

```bash
git checkout -b feature/prj-2026-001/<tarea-kebab>-v<N>
```

### Paso 3 - Publicar rama remota

```bash
git push -u origin feature/prj-2026-001/<tarea-kebab>-v<N>
```

### Paso 4 - Trazabilidad mínima

Registrar en el plan activo (`/memories/session/plan.md`):
- nombre de rama creada
- fecha de creación
- tarea/feature objetivo de implementación

### Paso 5 - Cierre

1. Abrir PR a `develop` para `feature/*`, `fix/*` y `chore/*`.
2. Abrir PR a `main` sólo para `hotfix/*` o release.
2. Referenciar el plan en la descripción del PR.
3. No reutilizar ramas de planes previos.

## Reglas de calidad

- Una rama por tarea/feature, sin excepciones.
- No trabajar en `main` ni en `develop` directamente.
- Cada tarea del backlog debe mapearse a una `feature/*` independiente.
- Evitar nombres genéricos (`feature/test`, `fix/temp`, etc.).
- Mantener nombres en minúsculas y kebab-case.

## Referencia

Usar plantilla en [./references/branch-template.md](./references/branch-template.md).