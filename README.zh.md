# Superpowers for QwenPaw ⚡

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> **Superpowers** 是一套完整的编码智能体方法论——现在可以在 **QwenPaw** 上运行。

本项目将 [obra/superpowers](https://github.com/obra/superpowers) v6.2.0（最初为 Claude Code 构建的一组可组合技能与工作流）移植到 [QwenPaw](https://github.com/agentscope-ai/QwenPaw)，这个开源的智能体框架。

## 🚀 快速开始

```bash
# 1. 进入 QwenPaw 工作区技能目录
cd ~/.qwenpaw/workspaces/{你的智能体ID}/skills/

# 2. 克隆本仓库
git clone https://github.com/pocketdigi/Superpowers4Qwenpaw.git

# 3. 复制技能到工作区
cp -r Superpowers4Qwenpaw/skills/* ./

# 4. 重启 QwenPaw — 技能会被自动检测加载
```

搞定，你的 QwenPaw 智能体现在拥有 Superpowers 了。

## 📦 包含的技能

| 技能 | 说明 |
|------|------|
| 🧠 **brainstorming** | 实现前先探索用户意图、需求和设计，避免盲目开干 |
| 📋 **writing-plans** | 根据需求规格编写详细、可执行的实现计划 |
| 🔴 **test-driven-development** | 红-绿-重构 TDD 循环——先写测试再写代码 |
| 🐛 **systematic-debugging** | 面对 Bug 和测试失败时的结构化调试工作流 |
| 🤖 **subagent-driven-development** | 派生子智能体逐任务执行计划，每步有审查门禁 |
| 🚀 **executing-plans** | 在隔离会话中按书面计划执行，带审查检查点 |
| 👥 **dispatching-parallel-agents** | 并行分发无依赖的独立任务 |
| 👀 **requesting-code-review** | 合并前请求代码审查 |
| 📬 **receiving-code-review** | 收到审查反馈后系统化处理 |
| ✅ **verification-before-completion** | 声称完成前先验证——拒绝凭感觉说"好了" |
| 🪵 **using-git-worktrees** | 用 Git Worktree 隔离工作区 |
| 🏁 **finishing-a-development-branch** | 测试通过后决定如何集成代码 |
| ✍️ **writing-skills** | 创建和编辑新技能 |
| ⚡ **using-superpowers** | **核心引导技能**——教会智能体主动检查并使用技能 |

## 🎯 工作原理

Superpowers for QwenPaw **不是一个插件**——它是一组 QwenPaw 原生支持的技能文件（带 YAML frontmatter 的 Markdown）。

工作流是自我强化的：

```
用户提出任务
  → using-superpowers 技能触发："先检查所有技能"
    → brainstorming 技能：理解需求
      → writing-plans 技能：创建执行计划
        → subagent-driven-development 技能：逐个任务执行
          → verification-before-completion：验证后再声称完成
```

每个技能是一个 `SKILL.md` 文件，包含 `name` 和 `description` frontmatter——与 QwenPaw 内置技能完全相同的格式，无需任何转译。

## 🛠️ QwenPaw 集成对照

| Superpowers 概念 | QwenPaw 对应 |
|-----------------|-------------|
| 技能（SKILL.md） | QwenPaw 原生技能——直接放入 `skills/` 目录 |
| 子智能体调度 | `spawn_subagent` 工具 |
| 代码审查 | `requesting-code-review` / `receiving-code-review` 技能 |
| TDD 循环 | `test-driven-development` 技能 |
| 计划执行 | `executing-plans` / `subagent-driven-development` 技能 |
| MCP 服务器 | 不包含——需要时单独配置 |
| brainstorm 服务器 | 不包含——需要手动安装 Node.js 依赖 |

## 📖 详细安装

参见 [INSTALL.md](INSTALL.md) 获取分步安装说明，包括：
- 手动复制文件
- QwenPaw 控制台导入
- 通过 CLI 导入
- 验证安装是否成功

## 🔄 更新

```bash
cd Superpowers4Qwenpaw
git pull
cp -r skills/* ~/.qwenpaw/workspaces/{你的智能体ID}/skills/
```

重启 QwenPaw 即可生效。

## 📄 许可证

MIT — 见 [LICENSE](LICENSE)。本项目是 [obra/superpowers](https://github.com/obra/superpowers)（同样基于 MIT）的移植版本。

## 🙏 致谢

- [Jesse Vincent](https://github.com/obra) — Superpowers 的创造者
- [Qwen Lab / AgentScope](https://github.com/agentscope-ai/QwenPaw) — QwenPaw 框架
