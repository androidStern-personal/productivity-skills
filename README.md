# Productivity Skills

Personal productivity system — task management, workplace memory, and a visual dashboard. Forked from [anthropics/knowledge-work-plugins](https://github.com/anthropics/knowledge-work-plugins) and adapted for cross-harness use.

## Compatible With

- **Claude Code** — install as a plugin via marketplace
- **OpenClaw** — load via `extraDirs`

## Skills

| Skill | Type | What it does |
|-------|------|-------------|
| `productivity-start` | command | Initialize tasks, memory, and dashboard |
| `productivity-update` | command | Sync tasks and refresh memory from activity |
| `productivity-tasks` | auto | Task management via TASKS.md |
| `productivity-memory` | auto | Two-tier memory system (MEMORY.md + memory/) |

**Commands** (`user-invocable: true`) are invoked explicitly via `/productivity-start` and `/productivity-update`.
**Auto skills** fire automatically when the agent detects relevance.

## Installation

### Claude Code (plugin marketplace)

Add the marketplace, then install the plugin:

```
/plugin marketplace add androidStern-personal/productivity-skills
/plugin install productivity@productivity-skills
```

Skills are namespaced: `/productivity:productivity-start`, `/productivity:productivity-update`, etc.

For local development:

```bash
claude --plugin-dir ~/src/skills/productivity
```

### OpenClaw (extraDirs mode)

Add to `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "load": {
      "extraDirs": ["~/src/skills/productivity/skills"],
      "watch": true
    }
  }
}
```

### Updating

```bash
git pull   # both harnesses pick up changes
```

### MCP Connectors

These skills work with any MCP-connected tools. They describe workflows in terms of categories (chat, email, calendar, project tracker, etc.) rather than specific products. If a category isn't connected, the agent skips it and notes the gap.

## Files Created at Runtime

The skills create these files in your working directory:

- `TASKS.md` — task list (created by productivity-start or productivity-tasks)
- `MEMORY.md` — working memory hot cache (created by productivity-start)
- `memory/` — deep memory directory (glossary, people, projects, context)
- `dashboard.html` — visual task board and memory viewer (copied from productivity-start)
