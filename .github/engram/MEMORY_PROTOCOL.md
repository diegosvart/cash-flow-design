# Memory Protocol — Engram + VS Code Copilot Integration

**Proyecto**: cash-flow-design  
**Versión**: 1.0  
**Fecha**: 2026-04-11  
**Autor**: GitHub Copilot + Engram MCP  

## 1. Objetivo

Proveer una estrategia de memoria persistente, buscable y coherente para el agente Copilot en VS Code, combinando tres capas:
- **Capa 1 (repo)**: Decisiones y políticas curadas, permanentes.
- **Capa 2 (session)**: Plan activo y contexto efímero por sesión.
- **Capa 3 (Engram)**: Búsqueda persistente, timeline y cross-session discovery.

## 2. Arquitectura de Tres Capas

### Capa 1: `/memories/repo/` (Permanent, Curated)
**Responsabilidad**: Decisiones de gobernanza y arquitectura duraderas.

**Archivos**:
- `project_metadata.md` — Canonical naming, project id, tech stack, contacts
- `planning_policy.md` — GitFlow rules, branch naming, PR targets, memory policies
- `optimization_notes.md` — Lessons learned, performance insights, anti-patterns

**Características**:
- Visible en GitHub (checkeado al repo)
- Editado por: PM/TI managers
- Esperanza de vida: 6+ meses (actualización ocasional)
- Acceso: Copilot lee al iniciar sesión para contexto base

**Ejemplo**: Si se decide cambiar convención de ramas de `feature/*` a `impl/*`, se registra en `planning_policy.md` con razón + fecha de transición.

### Capa 2: `/memories/session/` (Ephemeral, Active Plan)
**Responsabilidad**: Plan ejecutable actual y contexto de sesión.

**Archivos**:
- `plan.md` — Tabla de tareas, entregables, dependencias, estado actual
- `gitflow_analysis.md` — Análisis técnico reciente, hallazgos, decisiones pendientes
- (opcional) `debug_trace.md` — Logs de problemas resueltos esta sesión

**Características**:
- Invisible en GitHub (NO checkeado, local solo)
- Editado por: Copilot automáticamente después de cada sesión
- Esperanza de vida: 1 sesión (reemplazado al abrir nueva sesión)
- Acceso: Copilot carga al iniciar para continuar trabajo previo
- **NO ENVIADO A ENGRAM**: Cada sesión comienza con plan vacío o con referencia a plan anterior via Engram timeline query

### Capa 3: Engram (Persistent, Searchable)
**Responsabilidad**: Búsqueda persistente, timeline y continuidad entre sesiones.

**Capacidades**:
- **FTS5 Semantic Search**: `mem_search("GitFlow decisions")`  → devuelve decisiones relevantes de todas las sesiones
- **Timeline Query**: `mem_timeline("2026-04-01", "2026-04-15")` → devuelve resumen de actividad y cambios
- **Session Summary**: `mem_session_summary()` → resumen automático al final de sesión (Engram lo indexa)
- **Context Injection**: `mem_context(session_id)` → inyecta contexto de sesión anterior en plan nueva

**Características**:
- Backend: SQLite FTS5 en `~/.engram/cash-flow-design/db.sqlite`
- Índices: `project=cash-flow-design` (canonical naming para evitar fragmentación)
- Retenido: Indefinido (aunque prunable por antigüedad vía política)
- Acceso: MCP Server en VS Code (puerto 8765)

**Regla canónica**: Todas las referencias a proyecto usan **exactamente** `cash-flow-design`, NUNCA variantes como `cash-flow`, `CashFlow`, `cash_flow_design`, etc.

## 3. Flujo de Datos entre Capas

```
Sesión N-1 termina
    ↓
`mem_session_summary()` genera resumen de plan ejecutado
    ↓
Resumen enviado a Engram → indexado con FTS (id: sesión N-1, timestamp)
    ↓
Copilot termina sesión (N-1)
---
Sesión N comienza (1 hora después, nuevo terminal)
    ↓
Copilot carga `/memories/repo/` (contexto base: políticas, decisiones)
    ↓
Copilot ejecuta `mem_timeline()` → obtiene resumen de último mes de Engram
    ↓
Copilot lee `/memories/session/plan.md` (vacío o con índice)
    ↓
Copilot puede ejecutar `mem_context(N-1)` → inyecta contexto sesión anterior
    ↓
Copilot continúa trabajo desde checkpoint (o puede abrir PR como en T-10)
```

## 4. Responsabilidades de Capas

| Pregunta | Dónde buscar | Capa |
|----------|--------------|------|
| "¿Cuál es la política de branches?" | `planning_policy.md` Secciones 15-21 | repo (1) |
| "¿Qué se hizo en las últimas 2 semanas?" | `mem_timeline("2026-04-01", "2026-04-15")` en Engram | Engram (3) |
| "¿Cuál es el siguiente paso del plan activo?" | `plan.md` Sección 3, tabla de tareas | session (2) |
| "¿Dónde está el PR de GitFlow?" | `mem_search("PR #3 GitFlow")` en Engram | Engram (3) |
| "¿Quién aprobó Mini-GitFlow?" | `planning_policy.md` + `mem_context(N-1)` | repo (1) + Engram (3) |

## 5. Sync Strategy: Qué entra a Engram

**SÍ sincroniza** (enviado a Engram al final de sesión):
1. `planning_policy.md` cambios (if modified this session)
2. `/memories/session/plan.md` resumen automático (no el plan entero)
3. Figma design asset references (via design context tool)
4. Git commits y PRs (via gh CLI queries)
5. Output de decisiones críticas (risk decisions, architectural choices)

**NO sincroniza** (kept local only):
1. `/memories/session/plan.md` full version (efectivamente, solo resumen)
2. Debug traces, error logs, terminal output
3. Secretos, API keys, credentials
4. IDE state, viewport position, editor selections

**Regla automática**: Al terminar sesión, script de salida ejecuta:
```bash
engram mem_save --project cash-flow-design \
  --tier curation \
  --source planning_policy.md \
  --tags governance,policy
```

## 6. MCP Commands Reference

### `mem_search(query: str) -> List[Result]`
- **Uso**: Buscar en toda la historia de Engram
- **Ejemplo**: `mem_search("GitFlow PR #3 develop")` → devuelve todas las referencias a ese PR en todas las sesiones
- **Índices**: FTS5 sobre proyecto=cash-flow-design
- **Resultado**: Lista de snippets con timestamp, source file, relevancia score

### `mem_save(content: str, tags: List[str], tier: str) -> success`
- **Uso**: Guardar contenido en Engram explícitamente
- **Parámetros**:
  - `content`: texto a guardar
  - `tags`: lista de etiquetas (ej: `["governance", "decision"]`)
  - `tier`: `"curation"` (policy), `"session"` (plan), `"debug"` (temporal)
- **Ejemplo**: Cuando se aprueba decisión crítica, guardar automáticamente

### `mem_context(session_id: str) -> str`
- **Uso**: Inyectar contexto de sesión anterior en sesión actual
- **Ejemplo**: `mem_context("session-20260411-001")` → devuelve resumen de esa sesión para continuidad
- **Resultado**: Párrafo de 100-200 palabras con tareas completadas, pendientes, blockers

### `mem_timeline(start_date: str, end_date: str) -> Timeline`
- **Uso**: Obtener timeline de eventos noticias en rango
- **Ejemplo**: `mem_timeline("2026-04-01", "2026-04-15")` → devuelve hitos, PRs, cambios importantes
- **Resultado**: Timeline markdown con entradas indexadas por fecha

### `mem_session_summary() -> str`
- **Uso**: Generar resumen automático de sesión actual para archivar
- **Invocado**: Al final de sesión, por script de salida
- **Resultado**: Párrafo con tasks completadas, status final, links a artifacts

## 7. Contingencies & Rollback

**Si Engram se corrompe**:
1. Restaurar desde backup (si existe en `~/.engram/backups/`)
2. Re-indexar `/memories/repo/` manualmente: `engram reindex --project cash-flow-design`
3. Caer a búsqueda manual en `/memories/session/` y GitHub issues si es necesario

**Si hay fragmentación (ej: proyecto guardado como `CashFlow` en una sesión)**:
1. Detectar vía `mem_timeline()` — si devuelve resultados con proyecto != `cash-flow-design`
2. Ejecutar: `engram merge-projects --source CashFlow --target cash-flow-design`
3. Validar merge vía query nueva

**Si MCP server de VS Code cae**:
1. Copilot fallback a lectura local `/memories/repo/` + `/memories/session/`
2. Engram queries retornan error → user informed que data no disponible
3. Restart MCP vía: `code --install-extension gentleman-programming.engram`

## 8. Rollout Plan

**Fase 1 (Today)**: 
- ✅ Document Memory Protocol (this file)
- Document MCP config (environment.example.env)

**Fase 2 (Next session)**:
- Install Engram binary on Windows
- Configure MCP in VS Code settings.json
- Create `/memories/session/plan.md` con índice

**Fase 3 (After T-11 PR merged)**:
- Run first `mem_save()` test with planning_policy.md
- Validate FTS search works
- Archive first session summary via `mem_session_summary()`

**Fase 4 (Ongoing)**:
- Every session end: run session summary save script
- Weekly: `mem_timeline()` query to spot patterns
- Monthly: Engram pruning if DB grows too large

## 9. Canonical Naming (Critical)

**RULE**: Every reference to project MUST use exactly:
```
cash-flow-design
```

**NOT**:
- cash-flow (incomplete)
- CashFlow (camelCase)
- Cash_Flow_Design (underscores)
- cash-flow-design-project (verbose)

**Enforcement**:
- Environment: `ENGRAM_PROJECT=cash-flow-design` (set at startup)
- Config: `project_metadata.md` line 1 defines this
- Policy: `planning_policy.md` section on Engram naming
- Validation: MCP rejects `mem_save()` if project not `cash-flow-design`

---

**Document Version**: 1.0  
**Last Updated**: 2026-04-11  
**Next Review**: After Engram installation and first 3 sessions
