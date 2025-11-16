# MCP Project Workflows - Complete Guide

Comprehensive guide for configuring MCP servers based on your project type, from greenfield development to legacy modernization.

---

## Table of Contents

- [Overview](#overview)
- [The 6 Core MCP Servers](#the-6-core-mcp-servers)
- [13 Project Type Configurations](#13-project-type-configurations)
- [Quick Start by Project Type](#quick-start-by-project-type)
- [Workspace Setup Templates](#workspace-setup-templates)
- [Cost Optimization Guide](#cost-optimization-guide)
- [Troubleshooting](#troubleshooting)

---

## Overview

This guide helps you configure the optimal MCP server setup based on your **project type**. Each project type has recommended minimal, optimal, and maximum configurations that balance functionality, cost, and complexity.

### What You'll Learn

- Which MCP servers to use for your project type
- Minimal vs. Optimal vs. Maximum configurations
- Estimated monthly costs and setup times
- Step-by-step workspace configuration
- How to verify your setup is working

---

## The 6 Core MCP Servers

### 1. **Spec Kit** (Constitutional Development)

**Official Repository:** https://github.com/github/spec-kit
**Type:** CLI Tool (not traditional MCP server)
**License:** MIT

**Purpose:** Specification-Driven Development (SDD) where detailed specifications become executable blueprints

**Key Features:**
- PRD parsing and validation
- Constitutional development methodology
- 0→1 project scaffolding
- 8 slash commands for complete workflow

**Installation:**
```bash
# Requires Python 3.11+ and uv package manager
# Install uv: https://docs.astral.sh/uv/

# Persistent installation (recommended)
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# Verify installation
specify --version
```

**Initialize Project:**
```bash
# For Claude Code
specify init my-project --ai claude --script sh

# For Windows PowerShell
specify init my-project --ai claude --script ps
```

**Slash Commands (used in AI agent):**
- `/speckit.constitution` - Establish governing principles
- `/speckit.specify` - Create specifications
- `/speckit.plan` - Generate implementation plans
- `/speckit.tasks` - Break down into tasks
- `/speckit.implement` - Execute implementation
- `/speckit.analyze` - Validate consistency

**Cost:** Free (no API keys required)

**Best For:** Greenfield, Replatforming, Migration, Rewrite projects

---

### 2. **OpenSpec** (Change Tracking & Analysis)

**Official Repository:** https://github.com/Fission-AI/OpenSpec
**Package:** @fission-ai/openspec
**License:** MIT

**Purpose:** AI-native spec-driven development with change proposal system

**Key Features:**
- Change proposals with /proposal, /apply, /archive commands
- Spec vs. changes separation (truth vs. proposals)
- Codebase analysis and validation
- Integration with 20+ AI tools

**Installation:**
```bash
# Requires Node.js 20.19.0+
npm install -g @fission-ai/openspec@latest

# Verify installation
openspec --version
```

**Initialize Project:**
```bash
cd /path/to/project
openspec init --tools claude,cursor,cline  # Or --tools all
```

**Slash Commands:**
- `/proposal` - Create change proposal
- `/apply` - Implement approved proposal
- `/archive` - Finalize completed changes

**CLI Commands:**
- `openspec list` - Show active changes
- `openspec view` - Interactive dashboard
- `openspec validate` - Validate changes/specs
- `openspec archive` - Archive completed work

**Cost:** Free (no API keys required)

**Best For:** Brownfield, Enhancement, Integration, Extension projects

---

### 3. **Task Master** (Orchestration & Memory)

**Official Repository:** https://github.com/eyaltoledano/claude-task-master
**Package:** task-master-ai
**License:** MIT WITH Commons-Clause
**Stars:** 23.7k

**Purpose:** AI-powered task management with persistent memory across sessions

**Key Features:**
- 39 tools for complete task lifecycle
- Epic sharding and PRD parsing
- Task memory with tag-based contexts
- Research mode with AI-powered analysis
- Multi-model support (Claude, GPT, Gemini, Perplexity, etc.)

**Installation:**
```bash
# Requires Node.js 18+
npm install -g task-master-ai

# Configure AI providers
task-master models --setup  # Interactive configuration
```

**MCP Configuration:**
```json
{
  "mcpServers": {
    "task-master-ai": {
      "command": "node",
      "args": ["./dist/mcp-server.js"],
      "env": {
        "DATA_DIR": "/absolute/path/to/data",
        "ANTHROPIC_API_KEY": "your-key",
        "OPENAI_API_KEY": "your-key",
        "PERPLEXITY_API_KEY": "your-key",
        "TASK_MASTER_TOOLS": "standard"
      },
      "timeout": 300
    }
  }
}
```

**Key Tools:**
- `add-task`, `update-task`, `remove-task`, `set-task-status`
- `add-subtask`, `split-tasks`, `expand-task`
- `parse-prd`, `analyze`, `research`, `complexity-report`
- `add-tag`, `use-tag`, `copy-tag` (git branch alignment)

**Cost:** $0-200/month (depending on AI provider usage)

**Best For:** Enhancement, Legacy Modernization, Rewrite, Integration projects

---

### 4. **Shrimp** (Task Decomposition & Research)

**Official Repository:** https://github.com/cjo4m06/mcp-shrimp-task-manager
**Package:** @cjo4m06/mcp-shrimp-task-manager
**License:** MIT
**Version:** 1.0.21

**Purpose:** Advanced task decomposition with persistent memory and research-driven development

**Key Features:**
- 15 tools for task lifecycle management
- Chain-of-thought processing and reflection
- Research mode for systematic exploration
- Persistent memory across sessions
- React-based Task Viewer dashboard
- Multi-language template support (10 languages)

**Installation:**
```bash
# Requires Node.js 18+
git clone https://github.com/cjo4m06/mcp-shrimp-task-manager.git
cd mcp-shrimp-task-manager
npm install
npm run build
```

**MCP Configuration:**
```json
{
  "mcpServers": {
    "shrimp-task-manager": {
      "command": "node",
      "args": ["/absolute/path/to/dist/index.js"],
      "env": {
        "DATA_DIR": "/absolute/path/to/data",
        "TEMPLATES_USE": "en",
        "ENABLE_GUI": "false",
        "WEB_PORT": "3000"
      }
    }
  }
}
```

**Key Tools:**
- `plan_task`, `analyze_task`, `reflect_task`, `split_tasks`
- `execute_task`, `verify_task`, `complete_task`
- `research_mode` - Systematic investigation (5+ char topics)
- `init_project_rules` - Establish standards
- `process_thought` - Chain-of-thought reasoning

**Cost:** Free (optional OpenAI for agent assignment)

**Best For:** Brownfield, Migration, Maintenance, Refactoring, Research-heavy projects

---

### 5. **Zen** (Multi-Model Validation)

**Official Repository:** https://github.com/BeehiveInnovations/zen-mcp-server
**License:** MIT
**Version:** 9.1.3

**Purpose:** Multi-model orchestration platform coordinating work across multiple AI providers

**Key Features:**
- 18 tools for collaboration, code quality, development
- Multi-model validation (Gemini, OpenAI, X.AI, Azure, DIAL, Ollama)
- `clink` - CLI-to-CLI bridge for spawning subagents
- `chat`, `thinkdeep`, `planner`, `consensus` tools
- `codereview`, `debug`, `precommit` quality tools
- Security auditing with OWASP Top 10 (`secaudit`)
- Test generation (`testgen`), refactoring (`refactor`), documentation (`docgen`)

**Installation:**
```bash
# Requires Python 3.10+ (3.12 recommended)
# Option 1: uvx (quickest)
# Add to ~/.claude/settings.json (see configuration below)

# Option 2: Clone repository
git clone https://github.com/BeehiveInnovations/zen-mcp-server.git
cd zen-mcp-server
./run-server.sh  # Linux/macOS
.\run-server.ps1  # Windows PowerShell
```

**MCP Configuration:**
```json
{
  "mcpServers": {
    "zen": {
      "command": "bash",
      "args": ["-c", "uvx --from git+https://github.com/BeehiveInnovations/zen-mcp-server.git zen-mcp-server"],
      "env": {
        "GEMINI_API_KEY": "your-key",
        "OPENAI_API_KEY": "your-key",
        "XAI_API_KEY": "your-key",
        "DEFAULT_MODEL": "auto",
        "DISABLED_TOOLS": "analyze,refactor,testgen,secaudit,docgen,tracer"
      }
    }
  }
}
```

**Example Prompts:**
- "Use zen to analyze code for security with gemini pro"
- "Perform codereview using gemini pro and o3"
- "Use zen precommit to validate changes before committing"
- "Get consensus from multiple models on architecture"

**Cost:** $50-300/month (depending on AI providers and usage)

**Best For:** All project types - universal validation, quality, and orchestration layer

---

### 6. **BMAD-METHOD** (Comprehensive AI-Human Collaboration Framework)

**Official Repository:** https://github.com/bmad-code-org/BMAD-METHOD
**License:** MIT
**Version:** v6.0.0-alpha.10

**Purpose:** Open-source framework amplifying human-AI collaboration through specialized agents and guided workflows

**Key Features:**
- **19+ specialized AI agents** across 4 modules (Core, BMM, BMB, CIS, BMGD)
- **50+ guided workflows** for software, game dev, and creative innovation
- **Multi-phase methodology:** Analysis → Planning → Solutioning → Implementation
- **Scale-adaptive tracks:** Quick Flow (1-4 hrs), BMad Method (1-3 days), Enterprise (3-7 days)
- **Party Mode:** Multi-agent collaboration in single conversation
- **Agent customization** and personalization
- **16 IDE integrations** (Claude Code, Cursor, VS Code, etc.)

**Key Agents:**
- **Software Team (8):** PM, Analyst, Architect, Scrum Master, Developer, Test Architect, UX Designer, Technical Writer
- **Game Team (4):** Game Designer, Game Developer, Game Architect, Frame Expert
- **Creative Suite (5):** Carson (Brainstorming), Maya (Design Thinking), Dr. Quinn (Problem Solving), Victor (Innovation), Sophia (Storytelling)
- **Builder (1):** Custom agent/workflow creator

**Installation:**
```bash
# Requires Node.js 20+
# Current version (v6 Alpha)
npx bmad-method@alpha install

# Interactive setup prompts for:
# - Module selection
# - IDE integration
# - Core settings
# - Project configuration
```

**IDE Integration:**

**Claude Code:**
```
/bmad-{agent-name}
/bmad:bmm:agents:dev
/bmad:core:workflows:party-mode
*workflow-init
*document-project
```

**Cursor:**
```
@{bmad_folder}/bmm/agents/dev
@{bmad_folder}/index  # Load all agents
```

**Key Workflows:**
- Phase 0: `document-project` (brownfield codebase analysis)
- Phase 1: `brainstorm-project`, `research`, `product-brief`, `game-brief`
- Phase 2: `tech-spec`, `prd`, `gdd`, `architecture`
- Phase 3: `create-epics-and-stories`, `implementation-readiness`
- Phase 4: `sprint-planning`, `epic-tech-context`, `develop-story`, `code-review`

**Cost:** $100-500/month (depending on AI providers and project complexity)

**Best For:** Enterprise projects, Game development, Creative workflows, Multi-phase lifecycles, Teams needing structured methodology

---

## 13 Project Type Configurations

### 1. Greenfield Development

**Description:** Starting a new project from scratch (0→1)

**Recommended Configurations:**

#### Minimal Team (2 servers) - $0/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Constitutional development */ },
    "zen": { /* Multi-model validation */ }
  }
}
```

**Setup Time:** 10 minutes
**Use Case:** Solo developer, simple MVP, learning project

#### Optimal Team (3 servers) - $200-350/month
```json
{
  "mcpServers": {
    "spec-kit": { /* PRD parsing, constitutional principles */ },
    "taskmaster": { /* Task orchestration */ },
    "zen": { /* Multi-model consensus */ }
  }
}
```

**Setup Time:** 30 minutes
**Use Case:** Professional development, funded startup, team project

#### Maximum Team (4 servers) - $300-500/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Complete 0→1 methodology */ },
    "taskmaster": { /* Epic sharding */ },
    "shrimp": { /* Code review from day 1 */ },
    "zen": { /* O3-level validation */ }
  }
}
```

**Setup Time:** 45 minutes
**Use Case:** Enterprise project, critical infrastructure, high-compliance

**Primary Benefits:**
- Constitutional development principles from day 1
- PRD parsing and requirement validation
- Multi-model consensus on architecture decisions
- Complete 0→1 methodology with validation

---

### 2. Brownfield Development

**Description:** Working with existing codebase, adding features/fixes

**Recommended Configurations:**

#### Minimal Team (2 servers) - $30-80/month
```json
{
  "mcpServers": {
    "openspec": { /* Change tracking */ },
    "shrimp": { /* Codebase analysis */ }
  }
}
```

**Setup Time:** 15 minutes
**Use Case:** Small team, moderate codebase, frequent updates

#### Optimal Team (3 servers) - $100-180/month
```json
{
  "mcpServers": {
    "openspec": { /* Change proposals, delta tracking */ },
    "shrimp": { /* Deep code analysis */ },
    "zen": { /* Multi-model code review */ }
  }
}
```

**Setup Time:** 20 minutes
**Use Case:** Professional team, large codebase, quality-focused

#### Maximum Team (4 servers) - $150-280/month
```json
{
  "mcpServers": {
    "openspec": { /* Explicit deltas */ },
    "taskmaster": { /* Change orchestration */ },
    "shrimp": { /* Intelligent review */ },
    "zen": { /* Validation layer */ }
  }
}
```

**Setup Time:** 30 minutes
**Use Case:** Enterprise, mission-critical, regulated industry

**Primary Benefits:**
- Change tracking with explicit deltas
- Intelligent codebase analysis
- Multi-layer code review
- Task memory for complex changes

---

### 3. Replatforming/Migration

**Description:** Moving from legacy platform to modern stack

**Recommended Configurations:**

#### Minimal Team (2 servers) - $50-120/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Constitutional migration principles */ },
    "shrimp": { /* Legacy analysis */ }
  }
}
```

**Setup Time:** 15 minutes

#### Optimal Team (3 servers) - $150-250/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Migration methodology */ },
    "shrimp": { /* Platform comparison */ },
    "zen": { /* Multi-model architecture validation */ }
  }
}
```

**Setup Time:** 25 minutes

#### Maximum Team (4 servers) - $250-400/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Complete migration framework */ },
    "taskmaster": { /* Phase orchestration */ },
    "shrimp": { /* Deep platform analysis */ },
    "zen": { /* Cross-platform consensus */ }
  }
}
```

**Setup Time:** 40 minutes

**Primary Benefits:**
- Legacy codebase deep analysis
- Constitutional migration principles
- Multi-model architecture validation
- Phase-by-phase orchestration

---

### 4. Enhancement/Feature Development

**Description:** Adding new features to existing product

**Recommended Configurations:**

#### Minimal Team (2 servers) - $50-120/month
```json
{
  "mcpServers": {
    "openspec": { /* Change proposals */ },
    "taskmaster": { /* Feature task orchestration */ }
  }
}
```

**Setup Time:** 15 minutes

#### Optimal Team (3 servers) - $100-200/month
```json
{
  "mcpServers": {
    "taskmaster": { /* PRD parsing, epic sharding */ },
    "openspec": { /* Integration analysis */ },
    "zen": { /* Feature validation */ }
  }
}
```

**Setup Time:** 25 minutes

#### Maximum Team (4 servers) - $150-300/month
```json
{
  "mcpServers": {
    "taskmaster": { /* Complete task orchestration */ },
    "openspec": { /* Change tracking */ },
    "shrimp": { /* Impact analysis */ },
    "zen": { /* Multi-model consensus */ }
  }
}
```

**Setup Time:** 35 minutes

**Primary Benefits:**
- PRD parsing and feature breakdown
- Change proposal workflow
- Research-with-context for unknowns
- Task orchestration and memory

---

### 5. Maintenance

**Description:** Bug fixes, updates, keeping systems running

**Recommended Configurations:**

#### Minimal Team (2 servers) - $50-100/month
```json
{
  "mcpServers": {
    "zen": { /* O3 debugging routing */ },
    "shrimp": { /* Code analysis */ }
  }
}
```

**Setup Time:** 15 minutes

#### Optimal Team (3 servers) - $80-150/month
```json
{
  "mcpServers": {
    "zen": { /* Debugging tools */ },
    "shrimp": { /* Code review */ },
    "openspec": { /* Change tracking */ }
  }
}
```

**Setup Time:** 20 minutes

#### Maximum Team (4 servers) - $120-220/month
```json
{
  "mcpServers": {
    "zen": { /* Advanced debugging */ },
    "shrimp": { /* Deep analysis */ },
    "openspec": { /* Minimal spec overhead */ },
    "taskmaster": { /* Task memory */ }
  }
}
```

**Setup Time:** 30 minutes

**Primary Benefits:**
- O3 routing for complex debugging
- Intelligent code review
- Minimal spec overhead
- Task memory for recurring issues

---

### 6. Legacy Modernization

**Description:** Updating old codebase to modern standards (requires 3-4 servers minimum)

**Recommended Configurations:**

#### Optimal Team (4 servers) - $180-300/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Constitutional modernization */ },
    "shrimp": { /* Legacy analysis */ },
    "zen": { /* Validation */ },
    "bmad": { /* Epic sharding */ }
  }
}
```

**Setup Time:** 35 minutes

#### Maximum Team (5 servers) - $250-450/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Constitutional principles */ },
    "taskmaster": { /* Multi-phase orchestration */ },
    "shrimp": { /* Deep legacy analysis */ },
    "zen": { /* Multi-model consensus */ },
    "bmad": { /* Epic complexity management */ }
  }
}
```

**Setup Time:** 50 minutes

**Primary Benefits:**
- Legacy codebase deep analysis
- Constitutional modernization principles
- Epic sharding for complexity
- Multi-phase orchestration

---

### 7. Integration Projects

**Description:** Connecting systems, APIs, third-party services

**Recommended Configurations:**

#### Minimal Team (2 servers) - $50-120/month
```json
{
  "mcpServers": {
    "openspec": { /* Integration point mapping */ },
    "zen": { /* API validation */ }
  }
}
```

**Setup Time:** 15 minutes

#### Optimal Team (3 servers) - $120-220/month
```json
{
  "mcpServers": {
    "openspec": { /* Change proposals for integrations */ },
    "taskmaster": { /* API orchestration */ },
    "zen": { /* Multi-model validation */ }
  }
}
```

**Setup Time:** 25 minutes

#### Maximum Team (4 servers) - $180-320/month
```json
{
  "mcpServers": {
    "openspec": { /* Integration analysis */ },
    "taskmaster": { /* Workflow orchestration */ },
    "shrimp": { /* API compatibility review */ },
    "zen": { /* Cross-system validation */ }
  }
}
```

**Setup Time:** 35 minutes

**Primary Benefits:**
- Change proposals for integration points
- API orchestration and testing
- Multi-model validation
- Cross-system compatibility analysis

---

### 8. Prototype/POC

**Description:** Rapid prototyping, proof of concept, experiments

**Recommended Configurations:**

#### Minimal Team (2 servers) - $20-60/month
```json
{
  "mcpServers": {
    "shrimp": { /* Research mode */ },
    "zen": { /* Rapid validation */ }
  }
}
```

**Setup Time:** 10 minutes

#### Optimal Team (3 servers) - $40-100/month
```json
{
  "mcpServers": {
    "shrimp": { /* Rapid brainstorming */ },
    "zen": { /* Consensus validation */ },
    "spec-kit": { /* Minimal spec overhead */ }
  }
}
```

**Setup Time:** 15 minutes

#### Maximum Team (4 servers) - $80-180/month
```json
{
  "mcpServers": {
    "shrimp": { /* Research + brainstorming */ },
    "zen": { /* Multi-model consensus */ },
    "spec-kit": { /* Quick scaffolding */ },
    "taskmaster": { /* Rapid iteration */ }
  }
}
```

**Setup Time:** 25 minutes

**Primary Benefits:**
- Research mode for exploration
- Rapid brainstorming and iteration
- Minimal spec overhead
- Consensus validation for ideas

---

### 9. Refactoring

**Description:** Improving code structure without changing behavior

**Recommended Configurations:**

#### Minimal Team (2 servers) - $50-120/month
```json
{
  "mcpServers": {
    "zen": { /* Refactoring tool with O3 */ },
    "shrimp": { /* Code analysis */ }
  }
}
```

**Setup Time:** 15 minutes

#### Optimal Team (3 servers) - $100-200/month
```json
{
  "mcpServers": {
    "zen": { /* Refactoring + validation */ },
    "shrimp": { /* Challenge critique */ },
    "spec-kit": { /* Reflection validation */ }
  }
}
```

**Setup Time:** 20 minutes

#### Maximum Team (4 servers) - $120-250/month
```json
{
  "mcpServers": {
    "zen": { /* Advanced refactoring */ },
    "shrimp": { /* Deep critique */ },
    "spec-kit": { /* Constitutional validation */ },
    "openspec": { /* Consistency analysis */ }
  }
}
```

**Setup Time:** 30 minutes

**Primary Benefits:**
- O3-powered refactoring tool
- Challenge critique before changes
- Reflection and validation
- Consistency analysis across codebase

---

### 10. Bug Fix/Patch

**Description:** Quick fixes, hotfixes, security patches

**Recommended Configurations:**

#### Minimal Team (2 servers) - $30-80/month
```json
{
  "mcpServers": {
    "zen": { /* O3 debugging */ },
    "shrimp": { /* Root cause analysis */ }
  }
}
```

**Setup Time:** 10 minutes

#### Optimal Team (3 servers) - $60-130/month
```json
{
  "mcpServers": {
    "zen": { /* Debugging with O3 routing */ },
    "shrimp": { /* Codebase analysis */ },
    "openspec": { /* Change tracking */ }
  }
}
```

**Setup Time:** 15 minutes

#### Maximum Team (4 servers) - $100-200/month
```json
{
  "mcpServers": {
    "zen": { /* Advanced debugging */ },
    "shrimp": { /* Impact analysis */ },
    "openspec": { /* Delta tracking */ },
    "taskmaster": { /* Fast workflow */ }
  }
}
```

**Setup Time:** 25 minutes

**Primary Benefits:**
- O3 routing for complex debugging
- Root cause analysis
- Fast workflow optimization
- Change tracking for patches

---

### 11. Rewrite/Rebuild

**Description:** Complete rewrite of existing system (requires 3-4 servers minimum)

**Recommended Configurations:**

#### Optimal Team (4 servers) - $250-400/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Constitutional rewrite principles */ },
    "taskmaster": { /* PRD parsing */ },
    "shrimp": { /* Legacy analysis */ },
    "zen": { /* Multi-model validation */ }
  }
}
```

**Setup Time:** 40 minutes

#### Maximum Team (5 servers) - $350-550/month
```json
{
  "mcpServers": {
    "spec-kit": { /* Complete methodology */ },
    "taskmaster": { /* Epic sharding */ },
    "shrimp": { /* Deep legacy analysis */ },
    "zen": { /* O3 validation */ },
    "bmad": { /* Epic complexity management */ }
  }
}
```

**Setup Time:** 55 minutes

**Primary Benefits:**
- Constitutional rewrite principles
- Legacy system deep analysis
- PRD parsing and validation
- Epic sharding for complexity

---

### 12. Extension/Plugin Development

**Description:** Building extensions for existing platforms (VS Code, browser, etc.)

**Recommended Configurations:**

#### Minimal Team (2 servers) - $50-120/month
```json
{
  "mcpServers": {
    "openspec": { /* Modular change proposals */ },
    "taskmaster": { /* Plugin task organization */ }
  }
}
```

**Setup Time:** 15 minutes

#### Optimal Team (3 servers) - $120-220/month
```json
{
  "mcpServers": {
    "openspec": { /* Extension architecture */ },
    "taskmaster": { /* Task orchestration */ },
    "zen": { /* Host system integration validation */ }
  }
}
```

**Setup Time:** 25 minutes

#### Maximum Team (4 servers) - $150-280/month
```json
{
  "mcpServers": {
    "openspec": { /* Modular proposals */ },
    "taskmaster": { /* Plugin workflow */ },
    "shrimp": { /* Host compatibility analysis */ },
    "zen": { /* Multi-platform validation */ }
  }
}
```

**Setup Time:** 35 minutes

**Primary Benefits:**
- Modular change proposals
- Plugin task organization
- Host system integration validation
- Multi-platform compatibility checks

---

### 13. Port/Adaptation

**Description:** Porting software to different platform/language/framework

**Recommended Configurations:**

#### Minimal Team (2 servers) - $50-120/month
```json
{
  "mcpServers": {
    "openspec": { /* Platform-specific change proposals */ },
    "shrimp": { /* Codebase comparison */ }
  }
}
```

**Setup Time:** 15 minutes

#### Optimal Team (3 servers) - $100-200/month
```json
{
  "mcpServers": {
    "openspec": { /* Platform mapping */ },
    "shrimp": { /* Cross-platform analysis */ },
    "zen": { /* Multi-platform validation */ }
  }
}
```

**Setup Time:** 25 minutes

#### Maximum Team (4 servers) - $150-300/month
```json
{
  "mcpServers": {
    "openspec": { /* Platform-specific proposals */ },
    "taskmaster": { /* Port orchestration */ },
    "shrimp": { /* Deep comparison */ },
    "zen": { /* Cross-platform consensus */ }
  }
}
```

**Setup Time:** 35 minutes

**Primary Benefits:**
- Platform-specific change proposals
- Codebase comparison and mapping
- Cross-platform validation
- Multi-model consensus on adaptations

---

## Quick Start by Project Type

### Step 1: Identify Your Project Type

Choose from the 13 project types above based on your current work.

### Step 2: Choose Configuration Level

- **Minimal:** Budget-conscious, solo developer, simple projects
- **Optimal:** Professional development, recommended for most teams
- **Maximum:** Enterprise, critical systems, high-compliance needs

### Step 3: Install Required MCP Servers

Based on your chosen configuration, install the required servers:

```bash
# Example for Greenfield Optimal
npm install -g @modelcontextprotocol/server-spec-kit
npm install -g @modelcontextprotocol/server-taskmaster
npm install -g @modelcontextprotocol/server-zen
```

### Step 4: Configure Your IDE

See IDE-specific guides:
- [Claude Code Setup →](/claude-code/mcp-setup/)
- [Claude Desktop Setup →](/claude-desktop/mcp-configuration/)
- [Gemini CLI Setup →](/gemini-cli/configuration/)
- [VS Code Extensions Setup →](/vscode-extensions/configuration/)

### Step 5: Verify Setup

Run verification commands in your IDE:

```
# For Claude Code
/mcp list

# For Claude Desktop
Check Extensions panel

# For Gemini CLI
gemini mcp list
```

---

## Workspace Setup Templates

### Template: Greenfield Optimal

**Project:** New SaaS application
**Configuration:** Spec Kit + Task Master + Zen

**.claude/config.json:**
```json
{
  "mcpServers": {
    "spec-kit": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-spec-kit"],
      "env": {
        "SPEC_KIT_MODE": "constitutional",
        "SPEC_KIT_PRD_PARSING": "true"
      }
    },
    "taskmaster": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-taskmaster"],
      "env": {
        "TASKMASTER_MEMORY_ENABLED": "true",
        "TASKMASTER_EPIC_SHARDING": "auto"
      }
    },
    "zen": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-zen"],
      "env": {
        "ZEN_MODELS": "claude-3-5-sonnet,gpt-4,gemini-2.5-pro",
        "ZEN_O3_ROUTING": "true",
        "ANTHROPIC_API_KEY": "${ANTHROPIC_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}",
        "GOOGLE_API_KEY": "${GOOGLE_API_KEY}"
      }
    }
  }
}
```

---

### Template: Brownfield Optimal

**Project:** Existing e-commerce platform
**Configuration:** OpenSpec + Shrimp + Zen

**.claude/config.json:**
```json
{
  "mcpServers": {
    "openspec": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-openspec", "${workspaceFolder}"],
      "env": {
        "OPENSPEC_TRACK_CHANGES": "true",
        "OPENSPEC_DELTA_MODE": "explicit"
      }
    },
    "shrimp": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-shrimp", "${workspaceFolder}"],
      "env": {
        "SHRIMP_ANALYSIS_DEPTH": "deep",
        "SHRIMP_REVIEW_MODE": "intelligent"
      }
    },
    "zen": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-zen"],
      "env": {
        "ZEN_MODELS": "claude-3-5-sonnet,gpt-4",
        "ZEN_VALIDATION_MODE": "code-review",
        "ANTHROPIC_API_KEY": "${ANTHROPIC_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}"
      }
    }
  }
}
```

---

### Template: Legacy Modernization Maximum

**Project:** Modernizing 10-year-old monolith
**Configuration:** Spec Kit + Task Master + Shrimp + Zen + BMAD

**.claude/config.json:**
```json
{
  "mcpServers": {
    "spec-kit": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-spec-kit"],
      "env": {
        "SPEC_KIT_MODE": "modernization",
        "SPEC_KIT_CONSTITUTIONAL": "true"
      }
    },
    "taskmaster": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-taskmaster"],
      "env": {
        "TASKMASTER_MEMORY_ENABLED": "true",
        "TASKMASTER_EPIC_SHARDING": "aggressive",
        "TASKMASTER_PHASES": "analyze,plan,execute,validate"
      }
    },
    "shrimp": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-shrimp", "${workspaceFolder}"],
      "env": {
        "SHRIMP_ANALYSIS_DEPTH": "comprehensive",
        "SHRIMP_LEGACY_MODE": "true"
      }
    },
    "zen": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-zen"],
      "env": {
        "ZEN_MODELS": "claude-3-opus,gpt-4,gemini-2.5-pro",
        "ZEN_O3_ROUTING": "true",
        "ZEN_CONSENSUS_REQUIRED": "true",
        "ANTHROPIC_API_KEY": "${ANTHROPIC_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}",
        "GOOGLE_API_KEY": "${GOOGLE_API_KEY}"
      }
    },
    "bmad": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-bmad"],
      "env": {
        "BMAD_EPIC_MODE": "true",
        "BMAD_PHASES": "break,make,analyze,decide",
        "BMAD_COMPLEXITY_THRESHOLD": "high"
      }
    }
  }
}
```

---

### Template: Maintenance Minimal

**Project:** Production bug fixes
**Configuration:** Zen + Shrimp

**.claude/config.json:**
```json
{
  "mcpServers": {
    "zen": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-zen"],
      "env": {
        "ZEN_MODELS": "claude-3-5-sonnet,gpt-4",
        "ZEN_O3_ROUTING": "true",
        "ZEN_DEBUG_MODE": "true",
        "ANTHROPIC_API_KEY": "${ANTHROPIC_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}"
      }
    },
    "shrimp": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-shrimp", "${workspaceFolder}"],
      "env": {
        "SHRIMP_ANALYSIS_DEPTH": "targeted",
        "SHRIMP_REVIEW_MODE": "fast"
      }
    }
  }
}
```

---

## Cost Optimization Guide

### Free Tier Strategy

**Best for:** Prototypes, learning, personal projects

**Configuration:**
- Use Gemini CLI with free tier (60 req/min)
- Zen with only Gemini 2.5 Pro
- Minimal server count (2 max)

**Monthly Cost:** $0

---

### Budget Strategy ($50-100/month)

**Best for:** Solo developers, small teams, non-critical projects

**Configuration:**
- Claude Code with personal plan
- 2-3 MCP servers
- Zen with Claude + free Gemini

**Recommended Projects:**
- Maintenance
- Bug fixes
- Prototypes
- Small enhancements

---

### Professional Strategy ($150-250/month)

**Best for:** Professional teams, funded startups, production systems

**Configuration:**
- Claude Code/Desktop with Pro plan
- 3-4 MCP servers (Optimal configurations)
- Zen with Claude + GPT-4

**Recommended Projects:**
- Greenfield development
- Brownfield features
- Refactoring
- Integrations

---

### Enterprise Strategy ($300-500+/month)

**Best for:** Enterprise, mission-critical, regulated industries

**Configuration:**
- Claude Code with team/enterprise plan
- 4-5 MCP servers (Maximum configurations)
- Zen with all 3 models (Claude Opus + GPT-4 + Gemini Pro)

**Recommended Projects:**
- Legacy modernization
- Rewrite/rebuild
- Replatforming
- Complex integrations

---

## Verification Checklist

### Before Starting Development

- [ ] Project type identified
- [ ] Configuration level chosen (Minimal/Optimal/Maximum)
- [ ] All required MCP servers installed
- [ ] IDE configuration file created
- [ ] Environment variables set
- [ ] API keys configured
- [ ] Test connection to each server

### Verification Commands

**Claude Code:**
```bash
# List MCP servers
/mcp list

# Test specific server
/mcp test spec-kit
/mcp test zen
```

**Claude Desktop:**
```
Extensions panel → Check all servers show "Connected"
```

**Gemini CLI:**
```bash
gemini mcp list
gemini mcp test zen
```

---

## Troubleshooting

### MCP Server Not Found

**Problem:** Server doesn't appear in `/mcp list`

**Solutions:**
1. Verify installation: `npm list -g | grep modelcontextprotocol`
2. Check config file syntax (valid JSON)
3. Restart IDE
4. Check logs: `~/.claude/logs/mcp.log`

---

### Environment Variables Not Loading

**Problem:** `${ANTHROPIC_API_KEY}` not being replaced

**Solutions:**
1. Set in shell: `export ANTHROPIC_API_KEY="sk-..."`
2. Add to `.bashrc` / `.zshrc`
3. Use hardcoded value (not recommended for version control)
4. Restart terminal/IDE

---

### High Costs

**Problem:** Monthly costs exceeding budget

**Solutions:**
1. Reduce configuration level (Max → Optimal → Minimal)
2. Use fewer models in Zen (only Claude, drop GPT-4)
3. Use Gemini free tier
4. Disable O3 routing temporarily
5. Consider per-project configurations

---

### Setup Too Complex

**Problem:** 50+ minutes to configure all servers

**Solutions:**
1. Start with Minimal configuration
2. Use templates from this guide
3. Add servers incrementally
4. Use workspace-specific configs
5. Create setup scripts

---

## Next Steps

1. **Identify your project type** from the 13 types above
2. **Choose configuration level** based on budget and needs
3. **Follow workspace template** for your project type
4. **Install MCP servers** using npm commands
5. **Configure your IDE** using IDE-specific guides
6. **Verify setup** using checklist above
7. **Start developing** with optimal MCP support!

---

## IDE-Specific Setup Guides

- **[Claude Code MCP Setup →](/claude-code/mcp-setup/)**
- **[Claude Desktop Extensions →](/claude-desktop/mcp-configuration/)**
- **[Gemini CLI MCP Configuration →](/gemini-cli/configuration/)**
- **[VS Code Extensions →](/vscode-extensions/configuration/)**
- **[Cline Configuration →](/cline/configuration/)**
- **[Roo-Code Setup →](/roo-code/setup/)**

---

*Last updated: 2025-11-16*
*Next update: 2025-12-16*
