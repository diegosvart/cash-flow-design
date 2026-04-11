# Plantilla Documental de Plan — PRJ-2026-001

> Convención de nombre: `PRJ-2026-001_plan_<tema>_vX_YYYY-MM-DD_<estado>.md`  
> Estados válidos: `draft` | `approved` | `archived`

---

## Encabezado del Plan

| Campo | Valor |
|---|---|
| **ID del plan** | PRJ-2026-001_plan_[tema]_v[N] |
| **Fecha** | YYYY-MM-DD |
| **Estado** | draft / approved / archived |
| **Autor** | [nombre] |
| **Aprobador** | [nombre o PENDIENTE] |
| **Plan previo** | [referencia o NINGUNO] |
| **Entregables vinculados** | [Figma key, repo, doc, etc.] |

---

## 1. Objetivo

Una oración clara y verificable que describe qué se logra cuando el plan esté completo.

---

## 2. Alcance

### Incluye (IN)
- [Ítem 1]

### Excluye (OUT)
- [Ítem 1]

### Supuestos
- [Supuesto 1]

---

## 3. Fases y Tareas

> Cada tarea debe ser atómica y verificable. Indicar dependencias explícitas.

### Fase [N]: [Nombre de la Fase]
**Objetivo de la fase**: [Una oración]

| ID | Tarea | Depende de | Asignado | Estado |
|----|-------|-----------|----------|--------|
| T-01 | [descripción] | — | [rol] | Pendiente |
| T-02 | [descripción] | T-01 | [rol] | Pendiente |

---

## 4. Entregables

| Entregable | Tipo | Criterio de aceptación | Vínculo |
|-----------|------|----------------------|---------|
| [nombre] | [doc/design/code/test] | [criterio verificable] | [URL/ruta] |

---

## 5. Verificación (Checklist de cierre)

- [ ] Todos los entregables listados en §4 están completos y accesibles.
- [ ] Las decisiones relevantes están registradas en `/memories/repo/`.
- [ ] El plan está guardado en memoria de sesión activa.
- [ ] Los planes anteriores marcados como `archived`.
- [ ] El repositorio GitHub refleja el estado actual.

---

## 6. Riesgos

| # | Riesgo | Probabilidad | Impacto | Mitigación |
|----|-------|-------------|---------|-----------|
| R-01 | [descripción] | Alta/Media/Baja | Alto/Medio/Bajo | [acción] |

---

## 7. Decisiones Tomadas

| Decisión | Valor | Rationale |
|----------|-------|-----------|
| [tema] | [valor] | [por qué] |

---

## 8. Recursos y Referencias

- **Figma**: https://www.figma.com/design/n1PBP4Uk3keBmziUSBgSTb
- **GitHub**: https://github.com/[usuario]/cash-flow-design
- **Especificación funcional**: docs/ERT/ERT_PRJ-2026-001_CashFlow_v1.0.md
- **Estructura UI**: docs/task.md
- **Memoria proyecto**: `/memories/repo/project_metadata.md`

---

## 9. Control de versiones del plan

| Versión | Fecha | Autor | Cambio |
|---------|-------|-------|--------|
| v1 | YYYY-MM-DD | [nombre] | Creación inicial |
