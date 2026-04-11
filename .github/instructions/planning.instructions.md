---
description: "Use when: creando un nuevo plan, actualizando un plan existente, documentando tareas o fases, preparando un roadmap, handoff operativo o documentación estructurada. Esta instrucción fuerza el uso de las skills context-optimizer y github-branch-standards antes de redactar e implementar cualquier plan. Aplica a todos los archivos del proyecto PRJ-2026-001."
name: "Planificación estructurada con optimización de contexto"
---

# Instrucción: Planificación estructurada

Antes de redactar cualquier plan, roadmap o documentación de fases para PRJ-2026-001:

1. **Carga la skill `context-optimizer`** siguiendo su flujo de 5 pasos (auditar, referenciar, estructurar, persistir, estimar).
2. **Usa siempre** el template en `.github/skills/context-optimizer/references/plan-template.md`.
3. **Carga la skill `github-branch-standards`** cuando el plan pase a implementación.
4. **Crea una rama dedicada por tarea** antes de cualquier cambio de implementación. Cada tarea del plan se ejecuta como una feature independiente derivada de `develop` con formato: `feature/prj-2026-001/<tarea-kebab>-v<N>`.
5. **No repitas** información ya disponible en `/memories/repo/project_metadata.md`.
6. **Guarda** el plan resultante en `/memories/session/plan.md` (reemplaza, no acumula).
7. **Registra** cualquier nueva decisión en `/memories/repo/planning_policy.md`.

## Política GitFlow del proyecto

- `main`: rama estable.
- `develop`: rama de integración.
- `feature/*`, `fix/*`, `chore/*`: derivan de `develop` y vuelven por PR a `develop`.
- `hotfix/*`: deriva de `main` y vuelve por PR a `main`.
- Si un plan tiene varias tareas implementables, no compartir rama: una feature por tarea.

## Convención de nombres para artefactos

```
PRJ-2026-001_plan_<tema>_v<N>_<YYYY-MM-DD>_<estado>.md
```

**Estados**: `draft` | `approved` | `archived`

## Recursos clave del proyecto

- Figma (Wireframe v0.1): `n1PBP4Uk3keBmziUSBgSTb`
- GitHub Repo: `cash-flow-design` (cuenta personal)
- Especificación: `docs/ERT/ERT_PRJ-2026-001_CashFlow_v1.0.md`
- Branch template: `.github/skills/github-branch-standards/references/branch-template.md`
