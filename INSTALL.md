# Installation Guide

## Prerequisites

- [QwenPaw](https://github.com/agentscope-ai/QwenPaw) installed and running
- Git (optional, for cloning)
- Your agent workspace path (default: `~/.qwenpaw/workspaces/{agent_id}/skills/`)

## Method 1: Direct Copy (Simplest)

### 1. Locate your QwenPaw workspace skills directory

```bash
# Default path
~/.qwenpaw/workspaces/{your_agent_id}/skills/

# Example: agent named "default"
~/.qwenpaw/workspaces/default/skills/

# Example: agent named "DAbwGG"
~/.qwenpaw/workspaces/DAbwGG/skills/
```

### 2. Copy the skills

```bash
# From a cloned repo
cp -r Superpowers4Qwenpaw/skills/* ~/.qwenpaw/workspaces/{agent_id}/skills/

# Or directly from this repo URL (download ZIP)
# 1. Download https://github.com/pocketdigi/Superpowers4Qwenpaw/archive/refs/heads/main.zip
# 2. Unzip
# 3. Copy skills/* to your workspace skills directory
```

### 3. Restart QwenPaw

```bash
# Stop QwenPaw
# Start QwenPaw again
qwenpaw app
```

Skills are auto-detected on startup. They will appear in the skill list as "customized" skills.

## Method 2: QwenPaw Console Import

1. Open the QwenPaw web console
2. Navigate to **Workspace → Skills**
3. Click **Import from ZIP**
4. Upload the `skills/` directory as a ZIP
5. Enable the imported skills

## Method 3: Manual Registration

If you prefer to register skills via `skill.json`:

```json
{
  "schema_version": "workspace-skill-manifest.v1",
  "skills": {
    "brainstorming": {
      "enabled": true,
      "channels": ["all"],
      "source": "customized",
      "metadata": {
        "name": "brainstorming",
        "description": "You MUST use this before any creative work...",
        "source": "customized",
        "protected": false,
        "requirements": { "require_bins": [], "require_envs": [] }
      },
      "requirements": { "require_bins": [], "require_envs": [] }
    }
    // ... repeat for each skill
  }
}
```

But automatic detection is simpler — just copy the files and restart.

## Verifying Installation

After restarting, ask your QwenPaw agent:

> "Tell me about your superpowers"

Or check that the skills are loadable:

```
# In the agent session
Skill("brainstorming")    # should return the skill content
Skill("writing-plans")    # should return the skill content
```

If a skill returns content, it's installed correctly.

## Troubleshooting

### Skills not found after restart

1. Verify files exist in the correct location:
   ```bash
   ls ~/.qwenpaw/workspaces/{agent_id}/skills/brainstorming/SKILL.md
   ```

2. Check the `skill.json` manifest in your workspace directory.
   If the skills directory has files but `skill.json` doesn't list them,
   they will be auto-discovered on the next reconciliation.

3. Restart QwenPaw completely (not just reload).

### Permission errors on Windows

If using Windows and skills don't copy correctly, try:
```powershell
Copy-Item -Path "Superpowers4Qwenpaw/skills/*" -Destination "$env:USERPROFILE\.qwenpaw\workspaces\{agent_id}\skills\" -Recurse -Force
```

## Updating

```bash
cd Superpowers4Qwenpaw
git pull
cp -r skills/* ~/.qwenpaw/workspaces/{agent_id}/skills/
```

Restart QwenPaw to apply updates.
