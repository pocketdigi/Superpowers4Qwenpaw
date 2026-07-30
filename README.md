# Superpowers for QwenPaw ⚡

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> **Superpowers** is a complete software development methodology for coding agents — now running on **QwenPaw**.

This project ports [obra/superpowers](https://github.com/obra/superpowers) v6.2.0 — a set of composable skills and workflows originally built for Claude Code — to [QwenPaw](https://github.com/agentscope-ai/QwenPaw), the open-source agent framework.

## 🚀 Quick Start

```bash
# 1. Navigate to your QwenPaw workspace skills directory
cd ~/.qwenpaw/workspaces/{your_agent_id}/skills/

# 2. Clone this repo or copy the skills
git clone https://github.com/pocketdigi/Superpowers4Qwenpaw.git

# 3. Copy skills into your workspace
cp -r Superpowers4Qwenpaw/skills/* ./

# 4. Restart QwenPaw — skills are auto-detected
#    Or manually register them via the console.
```

Done. Your QwenPaw agent now has Superpowers.

## 📦 What's Included

| Skill | Description |
|-------|-------------|
| 🧠 **brainstorming** | Explore user intent, requirements, and design before implementation |
| 📋 **writing-plans** | Create detailed, executable implementation plans from specs |
| 🔴 **test-driven-development** | Red-Green-Refactor TDD cycle — write tests first |
| 🐛 **systematic-debugging** | Structured debugging workflow for bugs and test failures |
| 🤖 **subagent-driven-development** | Execute plans by dispatching subagents per task with review gates |
| 🚀 **executing-plans** | Execute written plans in isolated sessions with review checkpoints |
| 👥 **dispatching-parallel-agents** | Dispatch independent tasks in parallel |
| 👀 **requesting-code-review** | Request code review before merging |
| 📬 **receiving-code-review** | Process review feedback systematically |
| ✅ **verification-before-completion** | Verify before claiming work is done |
| 🪵 **using-git-worktrees** | Isolate work in git worktrees |
| 🏁 **finishing-a-development-branch** | Decide how to integrate completed work |
| ✍️ **writing-skills** | Create and edit new skills |
| ⚡ **using-superpowers** | **Core bootstrap** — teaches your agent to proactively use skills |

## 🎯 How It Works

Superpowers for QwenPaw is **not a plugin** — it's a collection of skill files (Markdown with YAML frontmatter) that QwenPaw natively understands.

The workflow is self-reinforcing:

```
User gives a task
  → using-superpowers skill triggers: "check all skills first"
    → brainstorming skill: understand requirements
      → writing-plans skill: create execution plan
        → subagent-driven-development skill: execute task-by-task
          → verification-before-completion: verify before claiming done
```

Each skill is a `SKILL.md` file with `name` and `description` frontmatter — the same format QwenPaw uses for its built-in skills. No transpilation needed.

## 🛠️ QwenPaw Integration Notes

| Superpowers Concept | QwenPaw Equivalent |
|---------------------|-------------------|
| Skill (SKILL.md) | Native QwenPaw skill — drop into `skills/` |
| Subagent dispatch | `spawn_subagent` tool |
| Code review | `requesting-code-review` / `receiving-code-review` skills |
| TDD cycle | `test-driven-development` skill |
| Plan execution | `executing-plans` / `subagent-driven-development` skills |
| MCP servers | Not included — configure separately if needed |
| brainstorm server | Not included — requires manual Node.js setup |

## 📖 Detailed Installation

See [INSTALL.md](INSTALL.md) for step-by-step installation instructions, including:
- Manual file copy
- QwenPaw console import
- CLI-based import
- Verifying installation

## 🔄 Updating

```bash
cd Superpowers4Qwenpaw
git pull
cp -r skills/* ~/.qwenpaw/workspaces/{your_agent_id}/skills/
```

Restart QwenPaw to pick up changes.

## 📄 License

MIT — see [LICENSE](LICENSE). This project is a port of [obra/superpowers](https://github.com/obra/superpowers) (also MIT).

## 🙏 Credits

- [Jesse Vincent](https://github.com/obra) — creator of Superpowers
- [Qwen Lab / AgentScope](https://github.com/agentscope-ai/QwenPaw) — QwenPaw framework
