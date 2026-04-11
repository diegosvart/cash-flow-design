---
name: context-optimizer
description: 'Optimiza el uso de tokens y contexto antes de crear un plan, planificación, roadmap, handoff o documentación de tareas. Úsala cuando: estés a punto de redactar un nuevo plan, necesites reducir tokens redundantes, quieras estructurar un plan como documentación reutilizable, o debas registrar decisiones clave en memoria. Invoca automáticamente al detectar: plan, planificación, roadmap, tareas, handoff, optimizar contexto, documentación de fases.'
argument-hint: 'Describe brevemente el plan que vas a crear (ej: plan diseño alta fidelidad, plan integración GitHub)'
---

# Context Optimizer Skill

## Cuándo usar esta skill

Esta skill se activa automáticamente cuando el agente detecta que el usuario va a:
- Escribir un nuevo plan o actualizar uno existente
- Crear documentación de tareas o fases de un proyecto
- Preparar un handoff operativo
- Organizar un roadmap técnico o de producto

## Flujo obligatorio antes de redactar un plan

### Paso 1 — Auditar contexto activo (< 30 seg)
1. Revisar `/memories/session/` y listar archivos existentes.
2. Revisar `/memories/repo/` y listar archivos existentes.
3. Identificar qué información ya existe y puede reutilizarse sin recargar.
4. Eliminar archivos de sesión obsoletos (planes cerrados, checklists completados).

### Paso 2 — Referenciar, no repetir
- Reutilizar datos de `/memories/repo/project_metadata.md` para contexto del proyecto.
- Citar IDs, keys y URLs desde la memoria en vez de incluirlas en el cuerpo del plan.
- Si existe un plan previo en sesión, resumirlo en una línea antes de reemplazarlo.

### Paso 3 — Estructurar el plan para documentación
Usar siempre el template de [./references/plan-template.md](./references/plan-template.md).

### Paso 4 — Persistir en memoria
1. Guardar el plan nuevo en `/memories/session/plan.md` (reemplaza el anterior).
2. Actualizar `/memories/repo/planning_policy.md` si hay nuevas decisiones estructurales.
3. Registrar en `/memories/repo/project_metadata.md` cualquier recurso nuevo generado.

### Paso 5 — Estimar tokens antes de ejecutar
Proporcionar una estimación rápida:
- Tokens esperados para el plan: N
- Tokens disponibles estimados: N
- Fases recomendadas para no exceder el límite: N

## Reglas de economía de tokens

| Regla | Acción |
|-------|--------|
| No repetir el plan anterior al actualizar | Indicar solo el delta (qué cambió) |
| No recargar task.md completo | Citar líneas específicas si son necesarias |
| No repetir decisiones ya tomadas | Referenciar `/memories/repo/` |
| No incluir historia del chat | Solo el estado actual, no cómo llegamos aquí |
| No generar documentación no solicitada | Solo lo explícitamente pedido |

## Referencias

- [Template de plan](./references/plan-template.md)
- [Metadatos del proyecto](../../../../memories/repo/project_metadata.md)
- [Política de planificación](../../../../memories/repo/planning_policy.md)
