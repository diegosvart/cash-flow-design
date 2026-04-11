# VS Code MCP Configuration for Engram

This file documents the required VS Code settings to enable Engram MCP integration with GitHub Copilot.

## Installation Steps

### 1. Install Engram Extension
```bash
# Via VS Code command palette
Cmd+Shift+P → "Install from VSIX" → gentleman-programming.engram-1.0.0.vsix

# OR via CLI
code --install-extension gentleman-programming.engram
```

### 2. Create/Update VS Code settings.json

Add the following to your `.vscode/settings.json` (Workspace level):

```json
{
  "engram.enabled": true,
  "engram.projectName": "cash-flow-design",
  "engram.databasePath": "${userHome}/.engram/cash-flow-design",
  "engram.mcpPort": 8765,
  "engram.mcpLogLevel": "debug",
  
  "github.copilot.chat.extensions": [
    {
      "name": "engram",
      "endpoint": "http://localhost:8765",
      "type": "mcp"
    }
  ],
  
  "[markdown]": {
    "editor.wordWrap": "on",
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  }
}
```

### 3. Configure Engram MCP Server

Create `~/.engram/.env` with:

```bash
# Copy from .github/engram/environment.example.env
ENGRAM_PROJECT=cash-flow-design
ENGRAM_DB_PATH=C:\Users\%USERNAME%\AppData\Local\Engram\cash-flow-design
ENGRAM_FTS_ENABLED=true
ENGRAM_SEARCH_MODE=semantic
VSCODE_MCP_PORT=8765
VSCODE_MCP_LOG_LEVEL=debug
```

### 4. Start MCP Server

In VS Code terminal:
```bash
engram server start --project cash-flow-design
# Output: Engram MCP listening on http://localhost:8765
```

### 5. Verify Connection

In GitHub Copilot chat, type:
```
@engram mem_search "planning_policy"
```

Expected response: Returns matches from FTS index.

## Available Commands in Copilot Chat

Once configured, use these in Copilot Chat:

### Search
```
@engram mem_search "GitFlow PR #3"
```

### Save Decision
```
@engram mem_save "We decided to use feature/* branches deriving from develop" \
  --tags governance,decision \
  --tier curation
```

### Get Context from Previous Session
```
@engram mem_context session-20260410-001
```

### View Timeline
```
@engram mem_timeline 2026-04-01 2026-04-15
```

### Generate Session Summary
```
@engram mem_session_summary
```

## Troubleshooting

### MCP Server not connecting
1. Check port 8765 is not in use: `netstat -ano | findstr 8765`
2. Restart MCP server: `engram server stop` then `engram server start`
3. Check logs: `tail -f ~/.engram/logs/mcp.log`

### Engram queries return no results
1. Verify database exists: `ls -la ~/.engram/cash-flow-design/db.sqlite`
2. Re-index: `engram reindex --project cash-flow-design`
3. Check FTS is enabled: `ENGRAM_FTS_ENABLED=true` in `~/.engram/.env`

### Project name mismatch
1. Canonical name is `cash-flow-design` (with hyphens, lowercase)
2. Check `$ENGRAM_PROJECT` env var: `echo $env:ENGRAM_PROJECT`
3. Verify in `planning_policy.md` Engram section

### VS Code Extension not loading
1. Check extension is installed: Extensions → Search "Engram"
2. Reload VS Code: `Ctrl+Shift+P` → "Reload Window"
3. Check extension logs: Output panel → Select "Engram"

## Memory Protocol Quick Reference

| Layer | Location | Scope | Sync to Engram? |
|-------|----------|-------|-----------------|
| Repo | `/memories/repo/` | Permanent policies | Yes (if changed) |
| Session | `/memories/session/` | Ephemeral plan | Resumen only |
| Engram | `~/.engram/cash-flow-design/` | Persistent search | Receives syncs |

---

**Document Version**: 1.0  
**Platform**: Windows 10/11 + VS Code 1.90+  
**MCP Version**: Engram 1.0  
**Last Updated**: 2026-04-11
