# Validation Checklist for GitFlow + Engram Integration

**Proyecto**: cash-flow-design PRJ-2026-001  
**Plan**: GitFlow + Engram governance & memory  
**Checklist Complete**: T-12 final deliverable  
**Fecha**: 2026-04-11  

## Pre-Implementation Verification (Before Merging PR #3 + PR #4)

### Git Branches & Tags
- [ ] `main` branch exists and is protected
- [ ] `develop` branch created and exists at origin
- [ ] Feature branches follow naming: `feature/prj-2026-001/<task>-v<N>`
- [ ] No legacy `plan/*` branches remain in active use
- [ ] Branch protection rules documented (will be implemented in follow-up PR)

**Check**:
```bash
git branch -r | grep develop
git branch -r | grep "feature/prj-2026-001"
```

### GitHub / Pull Requests
- [ ] PR #3 targets `develop` (not `main`)
- [ ] PR #3 title: "PRJ-2026-001: GitHub standards y GitFlow governance"
- [ ] PR #3 includes SKILL.md, planning.instructions.md, branch-template.md
- [ ] PR #4 targets `develop` (not `main`)
- [ ] PR #4 title: "PRJ-2026-001: Engram MCP integration design for VS Code"
- [ ] PR #4 includes MEMORY_PROTOCOL.md, VS_CODE_MCP_SETUP.md, etc.

**Check**:
```bash
gh pr view 3 --json baseRefName,headRefName,title
gh pr view 4 --json baseRefName,headRefName,title
```

### Memory Files & Policies
- [ ] `/memories/repo/planning_policy.md` contains GitFlow rules (§15-21)
- [ ] `/memories/repo/planning_policy.md` contains Engram canonical naming (§Engram section)
- [ ] `/memories/repo/project_metadata.md` exists and lists canonical names
- [ ] `/memories/session/plan.md` exists and reflects plan state (T-00 through T-11 ✅, T-12 pending)
- [ ] No contradictions between SKILL.md and planning_policy.md on branch naming

**Check**:
```bash
grep -n "develop\|feature/prj-2026-001" docs/.github/skills/github-branch-standards/SKILL.md
grep -n "cash-flow-design" /memories/repo/planning_policy.md
```

### Figma Design (Mantenedor v3)
- [ ] Frame "Mantenedor - Registros v3 (Single Screen)" exists in Figma
- [ ] Header component instance (real, not replicated) id = 41:33
- [ ] Footer component instance (real, not replicated) id = 41:34
- [ ] Registros tab is only active content tab (others are placeholder)
- [ ] v2 legacy frames marked and displaced in canvas

**Check**: Via Figma MCP get_metadata on fileKey for mantenedor design

---

## Post-PR-Merge Verification (After PR #3 and PR #4 accepted into `develop`)

### Branches Updated in develop
- [ ] Execute `git checkout develop && git pull origin develop`
- [ ] Confirm `.github/` directory exists with subdirectories: skills/, instructions/, engram/
- [ ] Confirm SKILL.md and planning.instructions.md reflect GitFlow (git diff against main)
- [ ] Confirm engram/ directory contains: MEMORY_PROTOCOL.md, VS_CODE_MCP_SETUP.md, ENGRAM_INTEGRATION_STRATEGY.md, environment.example.env

**Check**:
```bash
ls -R .github/
cat .github/engram/environment.example.env | grep ENGRAM_PROJECT
```

### Memory Layers Coherent
- [ ] `/memories/repo/planning_policy.md` and SKILL.md agree on branch naming
- [ ] `/memories/repo/planning_policy.md` and ENGRAM_INTEGRATION_STRATEGY.md agree on Engram canonical name
- [ ] `/memories/session/plan.md` reflects all 12 tasks with known state
- [ ] No duplicate definitions across files

**Check**:
```bash
echo "=== Checking branch naming consistency ==="
grep "feature/prj-2026-001" /memories/repo/planning_policy.md
grep "feature/prj-2026-001" docs/.github/skills/github-branch-standards/SKILL.md

echo "=== Checking Engram naming consistency ==="
grep "cash-flow-design" /memories/repo/planning_policy.md
grep "cash-flow-design" .github/engram/ENGRAM_INTEGRATION_STRATEGY.md
grep "ENGRAM_PROJECT" .github/engram/environment.example.env
```

---

## Pre-Engram-Installation Verification (Before Phase B)

### Environment Setup
- [ ] Windows version >= 10 (for Engram MCP support)
- [ ] VS Code version >= 1.90
- [ ] PowerShell core available for installation scripts
- [ ] GitHub CLI (gh) installed and configured

**Check**:
```bash
# Windows build version
[Environment]::OSVersion.Version

# VS Code version
code --version

# gh version
gh --version
```

### Configuration Files Ready
- [ ] `~/.engram/` directory does not exist yet (will be created during install)
- [ ] Make a copy of `.github/engram/environment.example.env` for manual deployment
- [ ] Confirm path C:\Users\%USERNAME%\ is accessible

**Check**:
```bash
# Should not exist yet
ls ~/.engram/

# Example file should be readable
cat .github/engram/environment.example.env
```

---

## Engram Installation & Validation (Phase B - After Engram Binary Downloaded)

### MCP Server Start
- [ ] Engram binary downloaded and added to PATH
- [ ] `~/.engram/.env` created from environment.example.env (with paths adjusted)
- [ ] MCP server starts without errors: `engram server start`
- [ ] MCP server logs show: "Engram MCP listening on http://localhost:8765"

**Check**:
```bash
engram server status
# Expected: "Server running on port 8765"

tail -f ~/.engram/logs/mcp.log
```

### VS Code MCP Integration
- [ ] Github Copilot extension is installed
- [ ] Engram MCP extension installed
- [ ] VS Code settings.json contains:
  - `"engram.enabled": true`
  - `"engram.projectName": "cash-flow-design"`
  - `"github.copilot.chat.extensions": [...]` references engram

**Check**:
```bash
# In VS Code settings (Ctrl+,)
# Search for: engram.enabled
# Expected: true
```

### FTS5 Indexing & Search
- [ ] `engram reindex --project cash-flow-design` completes without errors
- [ ] Index report shows >= 2 documents indexed (planning_policy.md, at minimum)
- [ ] Test query in Copilot Chat: `@engram mem_search "GitFlow PR"`
- [ ] Response includes reference to PR #3 or planning_policy.md

**Check**:
```bash
# In Copilot Chat type:
@engram mem_search "planning_policy GitFlow"
# Expected: Returns matching snippets from indexed files
```

### Memory Protocol Commands
- [ ] `mem_search(query)` returns results for "GitFlow"
- [ ] `mem_save(content, tags, tier)` accepts data without errors
- [ ] `mem_context(session_id)` works (may return empty if first session)
- [ ] `mem_timeline(start_date, end_date)` returns events
- [ ] `mem_session_summary()` generates summary without errors

**Check** (in Copilot Chat):
```
@engram mem_search "GitHub standards"
@engram mem_save "Test message" --tags test --tier debug
@engram mem_session_summary
```

---

## Cross-Session Continuity (After 2+ Sessions with MCP Active)

### Session N Data Captured
- [ ] `/memories/session/plan.md` was modified during session N
- [ ] At session end, Engram received `mem_session_summary()` call
- [ ] No errors in ~/.engram/logs/mcp.log during summary save

### Session N+1 Discovery
- [ ] Open VS Code (new terminal, new session)
- [ ] Engram MCP connects automatically (or manual: `engram server start`)
- [ ] Execute in Copilot Chat: `@engram mem_timeline "2026-04-11" "2026-04-15"`
- [ ] Response includes events from session N
- [ ] Execute: `@engram mem_context session-20260411-001`
- [ ] Response includes summary of session N's work (GitFlow + Engram design)

**Validation**: User can answer "What did we complete in the previous session?" without re-reading files.

---

## Naming Consistency Audit (Critical - Run Quarterly)

### Canonical Name Verification
- [ ] Search all .env files: `grep ENGRAM_PROJECT ~/.engram/.env` → results: `cash-flow-design`
- [ ] Search planning_policy.md: `grep "cash-flow-design" /memories/repo/planning_policy.md` → results: ≥ 2
- [ ] Search Engram DB (if FTS working): `@engram mem_search "cash-flow-design"` → results: ≥ 1
- [ ] Query database directly (if shell access): `sqlite3 ~/.engram/cash-flow-design/db.sqlite "SELECT DISTINCT project FROM fts_index LIMIT 1;"` → returns: `cash-flow-design`

### Fragmentation Detection
- [ ] No references to: `CashFlow`, `cash-flow`, `cash_flow_design`, `Cash-Flow-Design` in config files

**Check**:
```bash
grep -r "CashFlow\|cash_flow\|Cash-Flow" ~/.engram/ /memories/repo/ docs/.github/engram/ 2>/dev/null
# Expected: No results (empty)
```

---

## Final Approval Sign-Off (T-12 Completion)

### Governance Sign-Off
- [ ] PM reviews planning_policy.md changes — **APPROVED**
- [ ] TI reviews SKILL.md and branch standards — **APPROVED**
- [ ] Design reviews Figma v3 mantenedor frame — **APPROVED**
- [ ] Engram architecture reviewed by system architect — **APPROVED**

### Documentation Completeness
- [ ] All documents cross-linked and tracked in plan.md
- [ ] No dangling references or TODO markers left
- [ ] Installation instructions tested on clean Windows system (if possible)
- [ ] Memory Protocol tested with real Copilot queries

### Ready for Deployment
- [ ] `develop` branch is stable (all PRs #3, #4 merged)
- [ ] No merge conflicts
- [ ] All tasks T-00 through T-11 marked ✅ Completed
- [ ] Phase B (Installation) scheduled for next week
- [ ] Stakeholder validation scheduled post-merge

---

## Appendix: Validation Script (Optional, for Automation)

Save this as `.github/scripts/validate_gitflow_engram.sh`:

```bash
#!/bin/bash
set -e

echo "=== VALIDATION: GitFlow + Engram Integration ==="

# 1. Check branches
echo "[1] Checking Git branches..."
git branch -r | grep -q "origin/develop" && echo "✅ develop branch exists" || echo "❌ develop branch missing"
git branch -r | grep -q "feature/prj-2026-001" && echo "✅ feature branches exist" || echo "❌ feature branches missing"

# 2. Check files
echo "[2] Checking documentation files..."
ls .github/skills/github-branch-standards/SKILL.md && echo "✅ SKILL.md exists" || echo "❌ SKILL.md missing"
ls .github/engram/MEMORY_PROTOCOL.md && echo "✅ MEMORY_PROTOCOL.md exists" || echo "❌ MEMORY_PROTOCOL.md missing"

# 3. Check naming consistency
echo "[3] Checking canonical naming consistency..."
grep -q "cash-flow-design" /memories/repo/planning_policy.md && echo "✅ planning_policy.md has canonical name" || echo "❌ planning_policy.md missing canonical name"
grep -q "cash-flow-design" .github/engram/ENGRAM_INTEGRATION_STRATEGY.md && echo "✅ ENGRAM_INTEGRATION_STRATEGY.md has canonical name" || echo "❌ Missing canonical name"

# 4. Check PRs
echo "[4] Checking PRs target develop..."
gh pr view 3 --json baseRefName | grep -q "develop" && echo "✅ PR #3 targets develop" || echo "❌ PR #3 doesn't target develop"
gh pr view 4 --json baseRefName | grep -q "develop" && echo "✅ PR #4 targets develop" || echo "❌ PR #4 doesn't target develop"

echo ""
echo "=== VALIDATION COMPLETE ==="
```

Run as: `bash .github/scripts/validate_gitflow_engram.sh`

---

**Document Version**: 1.0  
**Status**: Ready for Validation  
**Last Updated**: 2026-04-11  
**Next Review**: After PR #3 and PR #4 merge to develop
