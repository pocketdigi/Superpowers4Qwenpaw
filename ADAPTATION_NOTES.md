# Adaptation Notes: Superpowers → QwenPaw

This document records the differences between running Superpowers on Claude Code vs. QwenPaw.

## Skill Format

Both systems use Markdown with YAML frontmatter. The frontmatter must include:

```yaml
---
name: skill-name
description: What this skill does
---
```

QwenPaw also supports an optional `metadata` field with `requires.bins` and `requires.envs`.

## Tool Name Differences

When Superpowers skills reference tools, substitute as follows:

| Superpowers (Claude Code) | QwenPaw |
|--------------------------|---------|
| `Subagent` → `task` | `spawn_subagent` (QwenPaw tool) |
| `Read` | `read_file` |
| `Edit` / `Write` | `write_file` / `edit_file` / `append_file` |
| `Bash` | `execute_shell_command` |
| `Grep` | `grep_search` |
| `Glob` | `glob_search` |
| `WebFetch` | `web_fetch` / `web_search` |
| `Browser` | `browser_use` |
| `Skill` | `Skill` (same name!) |

## What's NOT Included

The following Superpowers components are **not** part of this port:

- **MCP Servers** — Superpowers' MCP infrastructure (e.g., filesystem, GitHub) is not bundled. Configure separately in QwenPaw's MCP settings if needed.
- **brainstorm-server** — The brainstorming skill's optional Node.js visualization server requires manual setup:
  ```bash
  cd skills/brainstorming/scripts
  npm install  # if a package.json exists
  node server.cjs
  ```
- **Plugin adapters** (`.claude-plugin/`, `.opencode/`, `.cursor-plugin/`, etc.) — Not needed. QwenPaw loads skills natively from the `skills/` directory.
- **`CLAUDE.md`** — Not used by QwenPaw. Equivalent configuration belongs in `AGENTS.md`, `MEMORY.md`, or `PROFILE.md`.

## Verification

After installation, the agent should:
1. List skills with `Skill("skill-name")`
2. Be guided by the `using-superpowers` skill to proactively check skills
3. Follow each skill's instructions precisely
