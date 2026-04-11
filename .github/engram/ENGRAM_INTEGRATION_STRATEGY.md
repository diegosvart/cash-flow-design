# Engram Integration Strategy & Migration Plan

**Proyecto**: cash-flow-design  
**Versión**: 1.0  
**Fecha**: 2026-04-11  
**Estado**: Design (Ready for Implementation)  

## 1. Executive Summary

This document defines how Engram integrates with VS Code Copilot to provide persistent, searchable memory for the `cash-flow-design` project, alongside existing `/memories/repo/` and `/memories/session/` layers.

**Goal**: Resolve memory fragmentation, enable cross-session discovery, and maintain decision audit trail without duplicating governance files.

---

## 2. Current State Analysis

### Today (Pre-Engram)

```
Session N-1:
  /memories/repo/ (planning_policy.md, project_metadata.md)
  ↓
  Copilot works on plan...
  ↓
  Session ends, plan.md stored locally (N-1 context lost at next session)

Session N (1 week later):
  /memories/repo/ reloaded (same context as N-1)
  /memories/session/plan.md created fresh (NO continuity)
  ↓
  Copilot must re-read all context from repo/
  ↓
  Search across sessions? IMPOSSIBLE (no temporal index)
```

**Problem**: Each session is isolated. Cross-session patterns invisible. Decision discovery is manual.

### With Engram (Post-Integration)

```
Session N-1:
  /memories/repo/ (planning_policy.md, project_metadata.md)
  /memories/session/plan.md (active plan)
  Engram indexing policy changes (FTS)
  ↓
  Session ends → mem_session_summary() auto-triggers
  ↓
  Summary sent to Engram → indexed with timestamp, project=cash-flow-design

Session N (1 week later):
  /memories/repo/ reloaded
  Engram MCP available via Copilot Chat
  ↓
  Copilot can query: "What did we decide about GitFlow?"
  ↓
  Engram responds: Found in session N-1, timestamp 2026-04-11, snippet + link
  ↓
  Full cross-session discovery + temporal continuity
```

**Benefit**: Persistent searchable memory, temporal patterns, zero manual context loss.

---

## 3. Integration Architecture

### Three-Layer Model

```
┌─────────────────────────────────────────────────────┐
│ GitHub Copilot (VS Code)                            │
│ ↓ @engram command in chat                           │
└─────────────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────────────┐
│ Engram MCP Server (Port 8765)                       │
│ - mem_search (FTS5)                                 │
│ - mem_save (write)                                  │
│ - mem_timeline (temporal query)                     │
│ - mem_context (session inject)                      │
│ - mem_session_summary (archival)                    │
└─────────────────────────────────────────────────────┘
         ↓ (SQLite FTS5)
┌─────────────────────────────────────────────────────┐
│ ~/.engram/cash-flow-design/db.sqlite                │
│ - Index: project=cash-flow-design                   │
│ - Records: decisions, PRs, commits, session summaries
│ - TTL: Indefinite (prunable)                        │
└─────────────────────────────────────────────────────┘

ALONGSIDE (Local Workspace)

┌─────────────────────────────────────────────────────┐
│ /memories/repo/ (GIT VERSIONED)                     │
│ - planning_policy.md (decisions)                    │
│ - project_metadata.md (canonical names)             │
│ - optimization_notes.md (lessons)                   │
│ - TTL: Permanent (updated occasionally)             │
└─────────────────────────────────────────────────────┘
         ↓ (NOT git versioned)
┌─────────────────────────────────────────────────────┐
│ /memories/session/ (EPHEMERAL)                      │
│ - plan.md (active plan table, real-time)            │
│ - gitflow_analysis.md (current findings)            │
│ - TTL: 1 session (replaced next session)            │
└─────────────────────────────────────────────────────┘
```

### Responsibilities

| Layer | Read by | Written by | Scope | Sync to Engram? |
|-------|---------|-----------|-------|-----------------|
| Engram | Copilot (mem_* commands) | Copilot (mem_save) | Cross-session FTS | N/A (itself) |
| /memories/repo/ | Copilot (session init) | PM/TI (manual edits) | Permanent policies | Yes (if changed) |
| /memories/session/ | Copilot (session init) | Copilot (frequent updates) | Active plan only | Resumen only |

---

## 4. Data Flow: Session Lifecycle

### Session N-1: GitFlow Governance

```
[T-10 EXECUTION]

Copilot loads /memories/repo/planning_policy.md
            ↓
Copilot creates feature/prj-2026-001/gitflow-standards-v1
            ↓
Copilot updates SKILL.md, planning.instructions.md, branch-template.md
            ↓
Copilot creates PR #3 → develop
            ↓
Session N-1 DATA: modified files + PR #3 + commits

[SESSION END HOOK]

Copilot runs: mem_session_summary()
             ↓
Output: "GitFlow governance implemented. feature/prj-2026-001/gitflow-standards-v1 created, 
         PR #3 a develop. Cambios: SKILL.md, planning.instructions.md, branch-template.md. 
         Aprob: Pendiente."
             ↓
Engram mem_save(summary, tags=["governance", "gitflow", "pr#3"], tier="curation")
             ↓
Engram FTS indexed:
  project: cash-flow-design
  timestamp: 2026-04-11T14:30:00Z
  text: summary + PR #3 link + commit hashes
  tags: governance, gitflow, pr#3
```

### Session N: Engram Discovery

```
[SESSION START, 1 week later]

Copilot loads /memories/repo/planning_policy.md (same as N-1)
             ↓
Copilot initializes /memories/session/plan.md (fresh, empty or indexed)
             ↓
User: "¿Qué se decidió sobre GitFlow?"
             ↓
Copilot executes: @engram mem_search "GitFlow PR"
             ↓
Engram FTS query:
  project = 'cash-flow-design'
  text MATCH 'GitFlow PR'
  ORDER BY timestamp DESC
             ↓
Results returned:
  - Session N-1 summary (2026-04-11, relevance 95%)
  - planning_policy.md change (timestamp, relevance 87%)
  - GitHub PR #3 metadata (timestamp, relevance 92%)
             ↓
Copilot responds with snippets + session_id reference
```

---

## 5. Implementation Roadmap

### Phase A: Setup (Today)
- ✅ Define Memory Protocol (MEMORY_PROTOCOL.md)
- ✅ Define VS Code MCP config (VS_CODE_MCP_SETUP.md)
- ✅ Create environment template (environment.example.env)
- → Create this strategy document (ENGRAM_INTEGRATION_STRATEGY.md)

### Phase B: Installation (Next 2 Days)
- [ ] Download Engram binary for Windows
- [ ] Copy environment.example.env → ~/.engram/.env
- [ ] Install VS Code extension
- [ ] Test MCP server startup: `engram server start`
- [ ] Verify Copilot can execute @engram commands

### Phase C: First Indexing & Sync (Week of Apr 15)
- [ ] Run `engram reindex --project cash-flow-design` on existing /memories/repo/
- [ ] Execute first `mem_save()` with planning_policy.md to validate FTS
- [ ] Test `mem_search()` queries
- [ ] Create session end hook script (auto-calls mem_session_summary)

### Phase D: Operational (Ongoing)
- [ ] Every session: validate Engram MCP available
- [ ] Weekly: run `mem_timeline()` to detect patterns
- [ ] Monthly: `engram maintenance --project cash-flow-design` (prune old records)
- [ ] Quarterly: review canonical naming (must be `cash-flow-design` always)

---

## 6. Canonical Naming Policy (CRITICAL)

### Rule: Single Name Across All Layers

```
ENGRAM_PROJECT = planning_policy.md section = project_metadata.md line 1 
                = environment.example.env value = GitHub issues label
                = MCP config = Copilot prompt

ALL MUST BE: cash-flow-design
```

### NOT Allowed (Will cause fragmentation)

```
❌ CashFlow
❌ cash-flow
❌ cash_flow_design
❌ cash-flow-design-project
❌ CASH_FLOW_DESIGN
```

### Validation Procedure

At each session init:
```bash
# Check environment
echo $env:ENGRAM_PROJECT
# Expected: cash-flow-design

# Check planning_policy.md exists
grep -i "engram.*canonical" docs/.github/instructions/planning_policy.md

# If mismatch detected: 
# Run: engram rename-project --from OLD --to cash-flow-design
```

---

## 7. Contingency Plans

### If Engram MCP crashes mid-session

**Detection**: Copilot command @engram fails with "connection refused"

**Response**:
1. Copilot falls back to local `/memories/repo/` + `/memories/session/`
2. User can manually restart: `engram server start`
3. Session continues without Engram (degraded mode)
4. At session end, if Engram recovered, `mem_session_summary()` catches up

**Prevention**: 
- Engram runs as background service
- VS Code restart hooks auto-start MCP
- Healthcheck every 10 min (if failed, alert user)

### If Engram database corrupts

**Detection**: `mem_search()` returns no results or errors

**Response**:
1. Backup `/memories/repo/` locally (safe, git-versioned)
2. Stop MCP: `engram server stop`
3. Restore from backup if available: `cp ~/.engram/backups/db.sqlite ~/.engram/cash-flow-design/`
4. Reindex: `engram reindex --project cash-flow-design`
5. Run test query: `mem_search("test")` should work
6. If failed, delete DB and recreate from fresh: `rm ~/.engram/cash-flow-design/db.sqlite && engram init`

**Prevention**:
- Weekly backups: `engram backup --project cash-flow-design`
- Monitor DB size: `ls -lh ~/.engram/cash-flow-design/db.sqlite`

### If project naming fragments (e.g., some records as `CashFlow`, others as `cash-flow-design`)

**Detection**: `mem_timeline()` returns partial results; duplicate content found

**Response**:
1. Query Engram: `SELECT DISTINCT project FROM fts_index LIMIT 10`
2. If multiple projects found: `engram merge-projects --source CashFlow --targets cash-flow-design`
3. Verify merge: `mem_search()` should now return all records
4. Update policy: ensure all configs use `cash-flow-design`

**Prevention**:
- Config validation script: `engram validate-config --project cash-flow-design`
- Enforce in MCP: reject `mem_save()` if project ≠ `cash-flow-design`

---

## 8. Cost & Risk Analysis

| Aspect | Cost | Risk | Mitigation |
|--------|------|------|-----------|
| Installation | 30 min setup | MCP port conflict | Use port 8765 (low-traffic) |
| Learning curve | 2-3 queries to learn syntax | User confusion with mem_* commands | Doc + examples in MEMORY_PROTOCOL.md |
| Storage | ~10MB per 1000 sessions | DB fragmentation/slowness | Weekly `engram maintenance` |
| Naming | One-time mapping | Project fragmentation | Canonical naming + validation script |
| Fallback | Free (local memory always works) | Data loss if MCP crash | Backup strategy (weekly snapshots) |

**Overall Risk Level**: LOW (enhancement, non-blocking)

---

## 9. Success Metrics

At end of Phase D (after 3-4 weeks of operation):

| Metric | Target | How to measure |
|--------|--------|-----------------|
| Engram availability | 99% | Uptime logs in ~/.engram/logs/ |
| Search latency | <500ms | MCP response time in debug logs |
| Index completeness | 100% of planning changes captured | `mem_search("planning_policy")` returns all edits |
| Session continuity | Each session includes prior context | Copilot can answer "What was last week's decision?" |
| Zero fragmentation | All records have project=`cash-flow-design` | Query: SELECT DISTINCT project → returns 1 row |

---

## 10. References

- [MEMORY_PROTOCOL.md](./MEMORY_PROTOCOL.md) — Full Memory Protocol spec
- [VS_CODE_MCP_SETUP.md](./VS_CODE_MCP_SETUP.md) — Detailed setup instructions
- [environment.example.env](./environment.example.env) — Config template
- [GitHub Engram Repo](https://github.com/Gentleman-Programming/engram)
- [planning_policy.md](/memories/repo/planning_policy.md) — Policy decisions

---

**Document Version**: 1.0 (Draft, Ready for Implementation)  
**Last Updated**: 2026-04-11  
**Next Phase Gate**: Phase B approval + Windows Engram binary download
