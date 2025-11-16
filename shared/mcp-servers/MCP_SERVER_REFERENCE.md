# MCP Server Complete Reference Guide

Comprehensive documentation for all 6 core MCP servers used in AI-driven development workflows.

**Last Updated:** 2025-11-16

---

## Table of Contents

- [Overview](#overview)
- [Server Comparison Matrix](#server-comparison-matrix)
- [1. Spec Kit (GitHub)](#1-spec-kit-github)
- [2. Task Master](#2-task-master)
- [3. Zen MCP Server](#3-zen-mcp-server)
- [4. Shrimp Task Manager](#4-shrimp-task-manager)
- [5. OpenSpec](#5-openspec)
- [6. BMAD-METHOD](#6-bmad-method)
- [Platform-Specific Setup](#platform-specific-setup)
- [IDE Integration Examples](#ide-integration-examples)

---

## Overview

These 6 MCP servers form the foundation of spec-driven, AI-assisted development workflows. Each serves a specific purpose in the development lifecycle, from planning to implementation to validation.

### Core Philosophy

- **Spec Kit**: Constitutional development with executable specifications
- **Task Master**: AI-powered task management with persistent memory
- **Zen**: Multi-model orchestration and validation
- **Shrimp**: Task decomposition and research-driven development
- **OpenSpec**: Spec-driven development with change tracking
- **BMAD-METHOD**: Comprehensive AI-human collaboration framework

---

## Server Comparison Matrix

| Feature | Spec Kit | Task Master | Zen | Shrimp | OpenSpec | BMAD |
|---------|----------|-------------|-----|--------|----------|------|
| **Primary Use** | Greenfield | Task Mgmt | Validation | Research | Change Track | Full Framework |
| **Tools Count** | 8 commands | 39 tools | 18 tools | 15 tools | 7 commands | 19+ agents |
| **Installation** | uvx CLI | npm global | Python/Docker | npm global | npm global | npx CLI |
| **API Keys** | None | Optional | Multiple | Optional | None | Multiple |
| **Best For** | 0→1 projects | Complex tasks | Quality | Research | Brownfield | Enterprise |
| **Setup Time** | 5-10 min | 10-15 min | 15-20 min | 10-15 min | 5-10 min | 20-30 min |
| **Monthly Cost** | Free | $0-200 | $50-300 | $0-100 | Free | $100-500 |

---

## 1. Spec Kit (GitHub)

**Official Repository:** https://github.com/github/spec-kit
**License:** MIT
**Version:** 0.0.22
**Type:** CLI Tool (not traditional MCP server)

### Purpose

Implements Specification-Driven Development (SDD) where detailed specifications become executable blueprints that directly generate working implementations.

### Installation

#### Prerequisites
- Python 3.11+
- uv package manager: https://docs.astral.sh/uv/
- Git
- AI coding agent (Claude Code, Copilot, etc.)

#### Installation Steps

**Option 1: Persistent Installation (Recommended)**
```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

**Option 2: One-Time Usage**
```bash
uvx --from git+https://github.com/github/spec-kit.git specify init <PROJECT_NAME>
```

**Option 3: Upgrade Existing**
```bash
uv tool install specify-cli --force --from git+https://github.com/github/spec-kit.git
```

### Initialize Project

**Basic Initialization:**
```bash
specify init my-project --ai claude
```

**With All Options:**
```bash
specify init my-app \
  --ai claude \
  --script sh \
  --github-token YOUR_GITHUB_TOKEN
```

**Windows PowerShell:**
```bash
specify init my-app --ai copilot --script ps
```

### Complete Command Reference

#### CLI Commands

| Command | Purpose | Options |
|---------|---------|---------|
| `specify init <name>` | Initialize project | `--ai`, `--script`, `--here`, `--force`, `--no-git` |
| `specify check` | Verify installation | None |

#### Slash Commands (In AI Agent)

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/speckit.constitution` | Create governing principles | Before any feature work |
| `/speckit.specify` | Transform description → spec | Early in feature development |
| `/speckit.clarify` | Resolve spec ambiguities | After spec creation |
| `/speckit.plan` | Generate implementation plan | After spec is validated |
| `/speckit.tasks` | Break down into tasks | After planning complete |
| `/speckit.implement` | Execute implementation | After tasks are ready |
| `/speckit.analyze` | Validate consistency | After tasks complete |
| `/speckit.checklist` | Generate validation checklist | Any time during workflow |

### Configuration

**VS Code Settings** (`.vscode/settings.json`):
```json
{
  "chat.promptFilesRecommendations": {
    "speckit.constitution": true,
    "speckit.specify": true,
    "speckit.plan": true,
    "speckit.tasks": true,
    "speckit.implement": true
  },
  "chat.tools.terminal.autoApprove": [
    ".specify/scripts/bash/",
    ".specify/scripts/powershell/"
  ]
}
```

### Environment Variables

- `--github-token`: GitHub personal access token (optional)
- Git credentials via standard Git configuration

### Supported AI Agents

**CLI-Based (11):**
- Claude Code, Gemini CLI, Cursor Agent, Qwen Code, OpenCode, Codex CLI
- Auggie CLI, CodeBuddy CLI, Amazon Q Developer, Amp, SHAI

**IDE-Based (4):**
- GitHub Copilot, Windsurf, Kilo Code, Roo Code

### Typical Workflow

```bash
# 1. Install and initialize
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
specify init taskify --ai claude
cd taskify

# 2. In Claude Code - establish constitution
/speckit.constitution

# 3. Create specification
/speckit.specify Build a team productivity platform with task tracking

# 4. Clarify if needed
/speckit.clarify

# 5. Develop plan
/speckit.plan

# 6. Generate tasks
/speckit.tasks --include-tests

# 7. Implement
/speckit.implement

# 8. Validate
/speckit.analyze
```

### Example Prompts

- "Create a constitution for our e-commerce platform project"
- "Specify a new feature: user authentication with OAuth2 support"
- "Plan the implementation for the authentication feature"
- "Generate tasks with tests included for our auth implementation"

### Cost

**Free** - No API keys or subscriptions required

### Best For

- Greenfield projects (0→1 development)
- Replatforming initiatives
- Projects requiring constitutional development
- Teams using GitHub workflows
- Spec-first methodology

---

## 2. Task Master

**Official Repository:** https://github.com/eyaltoledano/claude-task-master
**Package:** task-master-ai (npm)
**License:** MIT WITH Commons-Clause
**Stars:** 23.7k

### Purpose

AI-powered task management system for AI-driven development workflows with persistent memory across sessions.

### Installation

#### Prerequisites
- Node.js 18+
- npm
- MCP-compatible AI client (Claude Code, Cursor, etc.)

#### Installation Steps

**Option 1: Global Installation**
```bash
npm install -g task-master-ai
```

**Option 2: Smithery (Claude Desktop)**
```bash
npx -y @smithery/cli install @cjo4m06/mcp-shrimp-task-manager --client claude
```

#### Setup API Keys

Create `.env` file:
```bash
# Required (at least one)
ANTHROPIC_API_KEY=sk-ant-...
OPENAI_API_KEY=sk-...
GOOGLE_API_KEY=...
PERPLEXITY_API_KEY=...

# Optional
GROQ_API_KEY=...
XAI_API_KEY=...
MISTRAL_API_KEY=...
```

#### MCP Configuration

**Cursor** (`~/.cursor/mcp.json`):
```json
{
  "mcpServers": {
    "task-master-ai": {
      "command": "node",
      "args": ["./dist/mcp-server.js"],
      "env": {
        "DATA_DIR": "/absolute/path/to/data/directory",
        "ANTHROPIC_API_KEY": "your-key",
        "OPENAI_API_KEY": "your-key",
        "PERPLEXITY_API_KEY": "your-key"
      },
      "timeout": 300
    }
  }
}
```

**VS Code** (`.vscode/mcp.json`):
```json
{
  "mcpServers": {
    "task-master-ai": {
      "command": "node",
      "args": ["./dist/mcp-server.js"],
      "env": {
        "DATA_DIR": "${workspaceFolder}/.taskmaster",
        "ANTHROPIC_API_KEY": "${ANTHROPIC_API_KEY}",
        "TASK_MASTER_TOOLS": "standard"
      },
      "timeout": 300
    }
  }
}
```

### Complete Tool Reference (39 Total)

#### Basic Task Operations (6 tools)
- `add-task` - Add new tasks with priority/dependencies
- `update-task` - Modify task properties
- `remove-task` - Delete tasks
- `set-task-status` - Change status (pending/in-progress/done/review/deferred/cancelled)
- `move-task` - Reorder or move between parents
- `next-task` - Identify next task based on dependencies

#### Subtask Management (4 tools)
- `add-subtask` - Create granular subtasks
- `update-subtask` - Modify subtask properties
- `remove-subtask` - Delete subtask
- `clear-subtasks` - Remove all subtasks from task

#### Tag Operations (6 tools)
- `add-tag` - Create tag contexts (aligned with git branches)
- `delete-tag` - Remove tag and tasks
- `copy-tag` - Clone tag context
- `rename-tag` - Change tag name
- `use-tag` - Switch between tags
- `list-tags` - Display all tags

#### Dependency Management (4 tools)
- `add-dependency` - Create prerequisite relationships
- `remove-dependency` - Break dependency links
- `fix-dependencies` - Auto-resolve conflicts
- `validate-dependencies` - Check for circular references

#### Analysis & Research (3 tools)
- `analyze` - AI-driven complexity analysis (1-10 scoring)
- `complexity-report` - Project complexity analysis
- `research` - AI research with fresh info

#### Project Operations (8 tools)
- `initialize-project` - Setup with rule profiles
- `parse-prd` - Convert PRD → structured tasks
- `expand-task` - Break down into subtasks
- `expand-all` - Expand all tasks
- `scope-up` - Consolidate tasks
- `scope-down` - Further granularize
- `generate` - AI task generation
- `update` - Batch update tasks

#### Utility Tools (5 tools)
- `models` - Configure AI providers (`--setup` for interactive)
- `rules` - Manage project rules
- `tool-registry` - Tool configuration
- `get-operation-status` - Check operation status
- `response-language` - Configure output language

#### System Tools (3 tools)
- `index` - Tool registry
- `utils` - Utility functions
- `README-ZOD-V3` - Schema validation docs

### Environment Variables

```bash
# AI Provider Keys (at least one required)
ANTHROPIC_API_KEY
OPENAI_API_KEY
GOOGLE_API_KEY
PERPLEXITY_API_KEY
GROQ_API_KEY
XAI_API_KEY
MISTRAL_API_KEY
AZURE_OPENAI_API_KEY
OLLAMA_API_KEY

# Google Vertex AI (optional)
VERTEX_PROJECT_ID
VERTEX_LOCATION=us-central1
GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json

# Configuration
TASK_MASTER_TOOLS=all|standard|core  # Controls tool loading
TASKMASTER_ENABLE_PROXY=false
http_proxy / https_proxy
CLAUDE_CODE_OAUTH_TOKEN  # For CI/CD
```

### Natural Language Prompts

```
"Initialize taskmaster-ai in my project"
"What's the next task I should work on?"
"Show me tasks 10, 12, and 15"
"Mark task 5 as done and what's next?"
"Break down task 5 into subtasks"
"Research latest best practices for JWT authentication"
"Analyze complexity of all tasks"
"Create tag 'feat-dark-mode' matching current branch"
"Expand all tasks to show better breakdown"
```

### CLI Commands

```bash
# Initialize
task-master init

# Parse PRD
task-master parse-prd --file docs/prd.txt --limit 10

# Task management
task-master list
task-master next
task-master show --ids 1,5,10
task-master add "Implement auth" --priority high --dependencies 2,3

# Expansion
task-master expand --id 5

# Research
task-master research "Latest JWT patterns"

# Analysis
task-master analyze
task-master complexity-report

# Configuration
task-master models --setup
task-master models --list
task-master models --test claude-code:sonnet
```

### Cost

- **Free tier:** Using local Ollama
- **Budget:** $50-100/month (single provider)
- **Professional:** $150-200/month (multiple providers)

### Best For

- Complex multi-phase projects
- Research-driven development
- Projects requiring task memory
- Teams using git branch workflows
- AI-assisted task orchestration

---

## 3. Zen MCP Server

**Official Repository:** https://github.com/BeehiveInnovations/zen-mcp-server
**Version:** 9.1.3
**License:** MIT

### Purpose

Multi-model orchestration platform enabling coordination across multiple AI providers (Gemini, OpenAI, X.AI, Azure, DIAL, Ollama) within unified workflows.

### Installation

#### Prerequisites
- Python 3.10+ (3.12 recommended)
- Git
- uv package manager (recommended)
- Windows: WSL2 required

#### Installation Methods

**Method A: uvx (Quickest)**

Add to `~/.claude/settings.json`:
```json
{
  "mcpServers": {
    "zen": {
      "command": "bash",
      "args": ["-c", "uvx --from git+https://github.com/BeehiveInnovations/zen-mcp-server.git zen-mcp-server"],
      "env": {
        "GEMINI_API_KEY": "your-key",
        "OPENAI_API_KEY": "your-key",
        "DISABLED_TOOLS": "analyze,refactor,testgen,secaudit,docgen,tracer"
      }
    }
  }
}
```

**Method B: Clone Repository**
```bash
git clone https://github.com/BeehiveInnovations/zen-mcp-server.git
cd zen-mcp-server
./run-server.sh  # Linux/macOS
.\run-server.ps1  # Windows PowerShell
```

### Complete Tool Reference (18 Total)

#### Collaboration & Planning (Enabled by Default)

**1. clink** - CLI-to-CLI Bridge
- Spawn specialized AI subagents (Gemini, Claude, Codex)
- Parameters: `prompt`, `cli_name`, `role`, `files`, `images`, `continuation_id`
- Example: "Use clink with gemini planner to design 3-phase rollout"

**2. chat** - Multi-turn Discussion
- Bounce ideas, get second opinions, brainstorm
- Parameters: `prompt`, `model`, `files`, `images`, `working_directory`, `thinking_mode`, `temperature`
- Example: "Chat with zen about API design patterns"

**3. thinkdeep** - Extended Reasoning
- Two-stage: specialized thinking → Claude review
- Parameters: `prompt`, `model`, `thinking_mode` (minimal to max), `problem_context`, `focus_areas`
- Example: "Use thinkdeep to validate our microservices architecture"

**4. planner** - Project Breakdown
- Five-stage: description → building → revision → branching → multi-session
- Professional ASCII diagrams, no time estimates
- Example: "Plan our migration from monolith to microservices"

**5. consensus** - Multi-Model Decisions
- Gather expert opinions from multiple models
- Parameters: `prompt`, `models` (with optional stances: supportive/critical/neutral), `focus_areas`
- Example: "Get consensus from claude, gpt4, and gemini on our database choice"

#### Code Quality & Analysis

**6. codereview** - Professional Code Review
- Two-phase: investigation → expert analysis
- Parameters: `prompt`, `model`, `review_type` (full/security/performance/quick), `focus_on`, `standards`
- Severity: CRITICAL (🔴) → HIGH → MEDIUM → LOW (🟢)

**7. debug** - Root-Cause Investigation
- Multi-step investigation with optional expert analysis
- Parameters: `step_number`, `findings`, `hypothesis`, `confidence`, `model`

**8. precommit** - Pre-Commit Validation
- Three-phase: investigation → completion → validation
- Parameters: `path`, `prompt`, `model`, `thinking_mode`, `compare_to`, `focus_on`, `severity_filter`
- Example: "Use zen precommit to validate changes before committing"

**9. analyze** - Code Analysis (Disabled by Default)
- Two-phase: investigation → expert analysis
- Parameters: `prompt`, `analysis_type`, `thinking_mode`, `output_format`

#### Development & Modernization (Disabled by Default)

**10. refactor** - Code Restructuring
- Priority: Decompose → Code Smells → Modernize → Organization
- Parameters: `refactor_type`, `model`, `focus_areas`, `style_guide_examples`

**11. testgen** - Test Generation
- Investigation → test generation phases
- Parameters: `prompt`, `model`, `test_examples`, `thinking_mode`

**12. secaudit** - Security Auditing
- 6-step OWASP-based workflow
- Parameters: `model`, `threat_level`, `compliance_requirements`, `audit_focus`, `severity_filter`
- Example: "Conduct comprehensive secaudit for our e-commerce platform"

**13. docgen** - Documentation Generation
- Two-phase: discovery → documentation
- Parameters: `document_complexity`, `document_flow`, `update_existing`, `comments_on_complex_logic`

#### Utility Tools

**14. apilookup** - Current API Documentation
- Searches latest API/SDK documentation
- Requires Codex CLI with `web_search = true`
- Example: "use apilookup SwiftUI best practices for 2025"

**15. challenge** - Critical Thinking
- Encourages thoughtful evaluation
- Example: "challenge but do we need this extra caching?"

**16. listmodels** - Model Inventory
- Display available models by provider

**17. tracer** - Execution Flow Analysis (Disabled by Default)
- Precision Mode: method/function analysis
- Dependencies Mode: class/module relationships

**18. version** - Version Information

### Environment Variables

#### API Keys (Choose One Approach)

**Option A: Native APIs**
```bash
GEMINI_API_KEY=...
OPENAI_API_KEY=...
AZURE_OPENAI_API_KEY=...
AZURE_OPENAI_ENDPOINT=...
AZURE_OPENAI_API_VERSION=...
XAI_API_KEY=...
DIAL_API_KEY=...
DIAL_API_HOST=...
```

**Option B: OpenRouter (Recommended for Beginners)**
```bash
OPENROUTER_API_KEY=...  # Single key for multiple models
```

**Important:** Use EITHER OpenRouter OR native APIs, not both!

#### Configuration

```bash
# Model Selection
DEFAULT_MODEL=auto|pro|flash|o3|o3-mini|o4-mini
DEFAULT_THINKING_MODE_THINKDEEP=minimal|low|medium|high|max

# Tool Management
DISABLED_TOOLS=analyze,refactor,testgen,secaudit,docgen,tracer

# Conversation
CONVERSATION_TIMEOUT_HOURS=5
MAX_CONVERSATION_TURNS=20

# System
LOG_LEVEL=DEBUG|INFO|WARNING|ERROR
WORKSPACE_ROOT=/path/to/workspace
```

### Usage Examples

```
"Use zen to analyze code for security with gemini pro"
"Debug this error with o3 and optimize with flash"
"Perform codereview using gemini pro and o3, then plan fixes"
"clink with gemini role=planner to draft rollout strategy"
"Get consensus from multiple models on architecture approach"
"Precommit validation ensuring changes meet requirements in FEATURE_SPEC.md"
```

### Cost

- **Free:** Using OpenRouter free tier or local Ollama
- **Budget:** $50-100/month (single provider)
- **Professional:** $150-250/month (2-3 providers)
- **Enterprise:** $300+/month (all providers + advanced features)

### Best For

- Multi-model validation workflows
- Complex debugging scenarios
- Security auditing and compliance
- Code review and quality assurance
- Architecture decision-making

---

## 4. Shrimp Task Manager

**Official Repository:** https://github.com/cjo4m06/mcp-shrimp-task-manager
**Package:** @cjo4m06/mcp-shrimp-task-manager (npm)
**License:** MIT
**Version:** 1.0.21

### Purpose

Advanced MCP server for converting natural language descriptions into structured development tasks with persistent memory across sessions.

### Installation

#### Prerequisites
- Node.js 18+
- npm
- MCP-compatible AI client

#### Installation Steps

**Option 1: Manual**
```bash
git clone https://github.com/cjo4m06/mcp-shrimp-task-manager.git
cd mcp-shrimp-task-manager
npm install
npm run build
```

**Option 2: Smithery**
```bash
npx -y @smithery/cli install @cjo4m06/mcp-shrimp-task-manager --client claude
```

#### MCP Configuration

Create `.mcp.json`:
```json
{
  "mcpServers": {
    "shrimp-task-manager": {
      "command": "node",
      "args": ["/absolute/path/to/mcp-shrimp-task-manager/dist/index.js"],
      "env": {
        "DATA_DIR": "/absolute/path/to/data/directory",
        "TEMPLATES_USE": "en",
        "ENABLE_GUI": "false",
        "WEB_PORT": "3000"
      }
    }
  }
}
```

### Complete Tool Reference (15 Total)

#### Task Management (13 tools)
- `plan_task` - Create detailed task plans (min 10 chars description)
- `analyze_task` - Examine task details and requirements
- `reflect_task` - Review completed tasks for QA
- `split_tasks` - Break into manageable subtasks
- `execute_task` - Run operations and implement
- `verify_task` - Validate completion and success criteria
- `complete_task` - Finalize and mark complete
- `delete_task` - Remove specific task
- `clear_all_tasks` - Remove entire task list (requires confirmation)
- `list_tasks` - Retrieve inventory (with filter/sort)
- `query_task` - Search and filter tasks
- `get_task_detail` - Full task info including dependencies
- `update_task` - Modify task content/metadata

#### Project Configuration (1 tool)
- `init_project_rules` - Establish guidelines and standards

#### Cognitive Processing (1 tool)
- `process_thought` - Chain-of-thought reasoning

#### Research (1 tool)
- `research_mode` - Systematic exploration (min 5 chars topic)

### Environment Variables

```bash
# Required
DATA_DIR=/absolute/path/to/data/directory

# Optional
TEMPLATES_USE=en  # Language: en, zh, es, fr, de, it, pt, ru, hi, ko
ENABLE_GUI=false
WEB_PORT=3000

# Prompt Customization (Optional)
MCP_PROMPT_PLAN_TASK=/path/to/custom/prompt.txt
MCP_PROMPT_PLAN_TASK_APPEND="Additional instructions..."
# Similar for: ANALYZE, REFLECT, SPLIT, EXECUTE, VERIFY, COMPLETE, etc.
```

### Workflow Examples

#### Complete Development Cycle
```
1. plan_task → Create high-level feature
2. split_tasks → Break into subtasks
3. execute_task → Implement each subtask
4. verify_task → Validate completion
5. reflect_task → Review quality
6. complete_task → Mark done
```

#### Research-Driven Development
```
1. research_mode → Investigate technology
2. plan_task → Plan based on research
3. split_tasks → Break into tasks
4. execute_task → Implement with knowledge
5. verify_task → Test requirements
```

### Natural Language Prompts

```
"Plan task: implement user authentication with JWT tokens"
"Split task <UUID> into research subtasks for React optimization"
"Reflect on task <UUID>: Review authentication for security"
"Enter research mode for 'TypeScript strict mode best practices'"
```

### Task Viewer Dashboard

Modern React-based visualization tool:

**Features:**
- Multi-tab draggable interface
- Real-time task listing with status badges
- Advanced search/filtering
- Dependency visualization
- Auto-refresh (5 sec to 5 min)

**Installation:**
```bash
cd tools/task-viewer
npm install
npm run build
npm start  # http://localhost:9998
```

**Development:**
```bash
npm run start:all  # API + hot reload
```

### Cost

**Free** - No API keys required (optional OpenAI for agent assignment)

### Best For

- Research-driven development
- Complex task decomposition
- Persistent task memory across sessions
- Git branch-aligned workflows
- Reflection and quality-focused teams

---

## 5. OpenSpec

**Official Repository:** https://github.com/Fission-AI/OpenSpec
**Package:** @fission-ai/openspec (npm)
**License:** MIT
**Version:** 0.15.0

### Purpose

AI-native system for spec-driven development that aligns humans and AI on requirements before code is written. Separates change proposals from specifications.

### Installation

#### Prerequisites
- Node.js >= 20.19.0
- npm or pnpm

#### Installation Steps

**Global CLI:**
```bash
npm install -g @fission-ai/openspec@latest
```

**Verify:**
```bash
openspec --version
```

**Initialize Project:**
```bash
cd /your/project
openspec init
```

**With Specific Tools:**
```bash
openspec init --tools claude,cursor,cline
openspec init --tools all   # All tools
openspec init --tools none  # AGENTS.md only
```

### Complete Command Reference (7 CLI + 3 Slash Commands)

#### CLI Commands

| Command | Purpose | Options |
|---------|---------|---------|
| `openspec init [path]` | Initialize OpenSpec | `--tools <list\|all\|none>` |
| `openspec list` | List active changes | `--specs`, `--changes`, `--long`, `--json` |
| `openspec view` | Interactive dashboard | None |
| `openspec show [item]` | Display change/spec | `--type change\|spec`, `--json`, `--noInteractive` |
| `openspec validate [item]` | Validate | `--strict`, `--json` |
| `openspec archive <change>` | Archive completed | `--yes`, `--skipValidation`, `--skipSpecUpdate` |
| `openspec update [path]` | Refresh agent instructions | None |

#### Slash Commands (AI Integration)

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/openspec:proposal` or `/proposal` | Create change proposal | New features, breaking changes, architecture mods |
| `/openspec:apply` or `/apply` | Implement approved proposal | Execute reviewed proposals |
| `/openspec:archive` or `/archive` | Finalize completed changes | Move to archive after deployment |

### Directory Structure

```
.openspec/
├── specs/                    # Current truth
│   ├── [spec-name]/
│   │   └── spec.md
├── changes/                  # Proposals
│   ├── [change-name]/
│   │   ├── proposal.md
│   │   ├── tasks.md
│   │   └── specs/
│   │       └── [spec-name]/
│   │           └── spec.md
│   └── archive/
│       └── YYYY-MM-DD-[change-name]/
├── AGENTS.md                 # Universal instructions
└── project.md               # Optional context
```

### Environment Variables

```bash
OPENSPEC_CONCURRENCY=6  # Max concurrent validations
NO_COLOR=false
```

### Supported AI Tools (20+)

- Claude Code, Cursor, GitHub Copilot, Amazon Q Developer
- CodeBuddy Code, Cline, CoStrict, Qoder
- Gemini CLI, RooCode, Windsurf, Codex
- Kilo Code, OpenCode, QwenCode
- Crush, Factory Droid, Auggie
- AGENTS.md (universal fallback)

### Usage Examples

**Trigger Phrases:**
```
"Help me create a change proposal"
"Help me plan a change"
"I want to create a spec proposal"
```

**Typical Workflow:**
```bash
# 1. Create proposal (via agent)
# Agent uses /proposal slash command

# 2. Review and refine
openspec show my-feature-change
openspec validate my-feature-change --strict

# 3. Implement (via agent)
# Agent uses /apply slash command

# 4. Archive
openspec archive my-feature-change --yes
```

**Interactive Dashboard:**
```bash
openspec view
# Shows: Summary metrics, active changes with progress bars,
# completed changes, specifications ranked by requirements
```

### Cost

**Free** - No API keys required

### Best For

- Brownfield projects
- Change tracking and management
- Spec-driven development
- Teams requiring proposal review workflows
- Projects with existing codebases

---

## 6. BMAD-METHOD

**Official Repository:** https://github.com/bmad-code-org/BMAD-METHOD
**License:** MIT
**Version:** v6.0.0-alpha.10

### Purpose

Comprehensive open-source framework for amplifying human-AI collaboration through specialized agents and guided workflows across software, game development, and creative innovation.

### Installation

#### Prerequisites
- Node.js >= v20.0.0
- npm

#### Installation Steps

**Current Version (v6 Alpha):**
```bash
npx bmad-method@alpha install
```

**Stable Version (v4):**
```bash
npx bmad-method install
```

**Interactive Setup:**
The installer prompts for:
1. Module selection (BMM, BMB, CIS, BMGD)
2. IDE integration (Claude Code, Cursor, VS Code, etc.)
3. Core settings (user name, language)
4. Project configuration
5. Workspace structure

### Complete Module & Agent Reference

#### Core Module (2 agents)
- **BMAD Master** - Party mode orchestrator
- **BMAD Web Orchestrator** - Web deployment

#### BMad Method (BMM) - 12 Agents

**Software Development (8 agents):**
1. **PM (John)** - Product Manager
2. **Analyst (Mary)** - Business Analyst
3. **Architect (Winston)** - System Architect
4. **SM (Bob)** - Scrum Master
5. **DEV (Amelia)** - Senior Developer
6. **TEA (Murat)** - Test Architect
7. **UX Designer (Sally)** - UX/UI Specialist
8. **Technical Writer (Paige)** - Documentation

**Game Development (4 agents):**
9. **Game Designer (Samus Shepard)** - Lead Game Designer
10. **Game Developer (Link Freeman)** - Senior Game Developer
11. **Game Architect (Cloud Dragonborn)** - Game Systems Architect
12. **Frame Expert (Saif)** - Visual Diagramming (Excalidraw)

#### BMad Builder (BMB) - 1 Agent
- **BMad Builder** - Custom agent/workflow creator

#### Creative Intelligence Suite (CIS) - 5 Agents
1. **Carson** - Brainstorming Specialist (36+ techniques)
2. **Maya** - Design Thinking Maestro
3. **Dr. Quinn** - Problem Solver
4. **Victor** - Innovation Oracle
5. **Sophia** - Master Storyteller

#### BMAD Game Design (BMGD) - 4 Agents
Same as BMM game team plus specialized workflows

### Complete Workflow Reference (50+ Workflows)

#### Phase 0: Documentation (Brownfield)
- `document-project` - Scan codebase, generate master index

#### Phase 1: Analysis (5 workflows)
- `brainstorm-project` - Multi-track exploration
- `brainstorm-game` - Game concept generation
- `research` - Market sizing, tech evaluation
- `product-brief` - Strategic documentation
- `game-brief` - Game project session

#### Phase 2: Planning (8 workflows)
- `workflow-init` - Unified entry point
- `tech-spec` - Lightweight spec (Quick Flow)
- `prd` - Product Requirements (scale-adaptive)
- `gdd` - Game Design Document
- `narrative` - Story-driven design
- `create-ux-design` - UX specification
- `create-epics-and-stories` - Requirement breakdown
- `correct-course` - Mid-stream changes

#### Phase 3: Solutioning (4+ workflows)
- `architecture` - Technical decisions
- `create-epics-and-stories` - After architecture
- `implementation-readiness` - Gate-check
- Enterprise extensions: `security-architecture`, `devops-strategy`

#### Phase 4: Implementation (12+ workflows)
- `sprint-planning` - Initialize sprint
- `epic-tech-context` - Epic technical guidance
- `validate-epic-tech-context` - Quality check
- `create-story` - Next story from backlog
- `validate-create-story` - Verification
- `story-context` - Assemble context XML
- `story-ready-for-dev` - Mark ready
- `develop-story` - Implement with tests
- `code-review` - Quality assessment
- `story-done` - Mark complete
- `epic-retrospective` - Review lessons
- `workflow-status` - Determine next action

#### Testing & QA (8+ workflows)
- `framework` - Test harness setup
- `ci` - CI pipeline configuration
- `test-design` - Per-epic test plans
- `atdd` - Acceptance-driven tests
- `automate` - Test suite building
- `test-review` - Quality auditing
- `nfr-assess` - Non-functional validation
- `trace` - Coverage mapping

#### Creative Intelligence (5 workflows)
- `brainstorming` - 36 techniques, 7 categories
- `design-thinking` - Five-phase empathy→test
- `problem-solving` - Root cause analysis
- `innovation-strategy` - Business model disruption
- `storytelling` - 25+ narrative frameworks

#### BMad Builder (10 workflows)
- `create-agent` - Interactive persona development
- `create-workflow` - Multi-step processes
- `create-module` - Complete module infrastructure
- `module-brief` - Strategic planning
- `edit-agent` - Persona refinement
- `edit-workflow` - Structure updates
- `edit-module` - Component enhancement
- `convert-legacy` - v4 to v6 migration
- `audit-workflow` - Validation
- `redoc` - Quality documentation

#### Game Design (4-phase system)
- `1-preproduction` - Initial prep
- `2-design` - Design and planning
- `3-technical` - Technical implementation
- `4-production` - Final production

### Configuration

**Core Config** (`config.yaml`):
```yaml
user_name: Your Name
communication_language: English
user_skill_level: Beginner|Intermediate|Expert
document_output_language: English
project_name: my-project
tech_docs: ./docs
output_folder: ./output
bmm-workflow-status: planning|development|testing
```

**Agent Customization** (`_cfg/agents/{agent-name}.customize.yaml`):
```yaml
agent:
  metadata:
    name: Custom Name
    role: Custom Role
  persona:
    personality: Custom traits
    communication_style: Preferences

memories:
  - Persistent context

startup_instructions:
  - Pre-interaction actions

custom_prompts:
  - id: unique-id
    prompt: Custom template

custom_menu_items:
  - label: Menu item
    action: "#custom-id" OR "workflow-ref"
```

### IDE Integration (16 IDEs)

**Claude Code:**
```
/bmad-{agent-name}
/bmad:module:agents:agent-name
/bmad:core:workflows:party-mode
```

**Cursor:**
```
@{bmad_folder}/{module}/agents/{agent-name}
@{bmad_folder}/bmm
@{bmad_folder}/index
```

### Special Features

#### Party Mode
Multi-agent collaboration - all 19+ agents in single conversation

```
/bmad:core:workflows:party-mode
*party-mode
```

**Use Cases:**
- Post-workflow debriefing
- High-stakes decisions
- Creative brainstorming
- Failure analysis
- Sprint activities

#### Web Bundles
Deploy to Gemini Gems or Custom GPTs

```bash
npm run bundle     # Package all
npm run rebundle   # Clear and regenerate
```

**Configuration for Web:**
```yaml
bmm-workflow-status: "standalone"
```

#### Scale-Adaptive Tracks

1. **Quick Flow** (1-4 hours) - Bug fixes, simple features
2. **BMad Method** (1-3 days) - Products, complex features
3. **Enterprise Method** (3-7 days) - Multi-tenant, compliance-heavy

### Cost

- **Free:** Using local tools only
- **Basic:** $50-100/month (single AI provider)
- **Professional:** $200-300/month (multiple providers)
- **Enterprise:** $500+/month (full capabilities, multiple models)

### Best For

- Enterprise-scale projects
- Teams requiring structured methodology
- Game development projects
- Creative innovation workflows
- Multi-phase project lifecycles
- Organizations needing customizable frameworks

---

## Platform-Specific Setup

### Windows PowerShell

#### Environment Setup
```powershell
# Install Node.js LTS
winget install OpenJS.NodeJS.LTS

# Install Python (for Zen)
winget install Python.Python.3.12

# Install uv (for Spec Kit)
irm https://astral.sh/uv/install.ps1 | iex

# Verify installations
node --version
python --version
uv --version
```

#### Install All Servers
```powershell
# Task Master
npm install -g task-master-ai

# Shrimp
git clone https://github.com/cjo4m06/mcp-shrimp-task-manager.git
cd mcp-shrimp-task-manager
npm install
npm run build

# OpenSpec
npm install -g @fission-ai/openspec@latest

# Spec Kit
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# Zen (requires WSL2)
wsl --install
# Then follow Linux instructions in WSL

# BMAD-METHOD
npx bmad-method@alpha install
```

#### Create Data Directories
```powershell
# Task Master
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.taskmaster"

# Shrimp
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.shrimp-tasks"

# OpenSpec (auto-created)
```

### WSL/Linux

#### Environment Setup
```bash
# Update package manager
sudo apt update && sudo apt upgrade -y

# Install Node.js 20+
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs

# Install Python 3.12
sudo apt install -y python3.12 python3.12-venv python3-pip

# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# Verify installations
node --version
python3 --version
uv --version
```

#### Install All Servers
```bash
# Task Master
npm install -g task-master-ai

# Shrimp
git clone https://github.com/cjo4m06/mcp-shrimp-task-manager.git
cd mcp-shrimp-task-manager
npm install
npm run build

# OpenSpec
npm install -g @fission-ai/openspec@latest

# Spec Kit
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git

# Zen
git clone https://github.com/BeehiveInnovations/zen-mcp-server.git
cd zen-mcp-server
./run-server.sh

# BMAD-METHOD
npx bmad-method@alpha install
```

#### Create Data Directories
```bash
# Task Master
mkdir -p ~/.taskmaster

# Shrimp
mkdir -p ~/.shrimp-tasks

# OpenSpec (auto-created in project)
```

### macOS

#### Environment Setup
```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Node.js
brew install node@20

# Install Python
brew install python@3.12

# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# Verify installations
node --version
python3 --version
uv --version
```

#### Install All Servers
```bash
# Same as Linux instructions above
```

---

## IDE Integration Examples

### Claude Code

#### Configuration (~/.claude/settings.json)

```json
{
  "mcpServers": {
    "taskmaster": {
      "command": "node",
      "args": ["/absolute/path/to/task-master-ai/dist/mcp-server.js"],
      "env": {
        "DATA_DIR": "${HOME}/.taskmaster",
        "ANTHROPIC_API_KEY": "${ANTHROPIC_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}",
        "TASK_MASTER_TOOLS": "standard"
      },
      "timeout": 300
    },
    "shrimp": {
      "command": "node",
      "args": ["/absolute/path/to/mcp-shrimp-task-manager/dist/index.js"],
      "env": {
        "DATA_DIR": "${HOME}/.shrimp-tasks",
        "TEMPLATES_USE": "en"
      }
    },
    "zen": {
      "command": "bash",
      "args": ["-c", "uvx --from git+https://github.com/BeehiveInnovations/zen-mcp-server.git zen-mcp-server"],
      "env": {
        "GEMINI_API_KEY": "${GEMINI_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}",
        "DISABLED_TOOLS": "analyze,refactor,testgen,secaudit,docgen,tracer"
      }
    }
  }
}
```

#### Using Spec Kit
```bash
# Initialize in project
cd /path/to/project
specify init my-app --ai claude

# Use slash commands in Claude Code
/speckit.constitution
/speckit.specify Build authentication system
/speckit.plan
/speckit.tasks --include-tests
/speckit.implement
```

#### Using OpenSpec
```bash
# Initialize
cd /path/to/project
openspec init --tools claude

# Use slash commands
/proposal
/apply
/archive
```

#### Using BMAD
```bash
# Initialize
npx bmad-method@alpha install
# Select "Claude Code" during setup

# Use slash commands
/bmad:bmm:agents:dev
/bmad:core:workflows:party-mode
/bmad:bmm:workflows:workflow-init
```

### Cursor IDE

#### Configuration (~/.cursor/mcp.json or project .cursor/mcp.json)

```json
{
  "mcpServers": {
    "taskmaster": {
      "command": "node",
      "args": ["./node_modules/task-master-ai/dist/mcp-server.js"],
      "env": {
        "DATA_DIR": "${workspaceFolder}/.taskmaster",
        "ANTHROPIC_API_KEY": "${ANTHROPIC_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}",
        "PERPLEXITY_API_KEY": "${PERPLEXITY_API_KEY}",
        "TASK_MASTER_TOOLS": "all"
      },
      "timeout": 300
    },
    "shrimp": {
      "command": "node",
      "args": ["./node_modules/@cjo4m06/mcp-shrimp-task-manager/dist/index.js"],
      "env": {
        "DATA_DIR": "${workspaceFolder}/.shrimp",
        "ENABLE_GUI": "true",
        "WEB_PORT": "9998"
      }
    },
    "zen": {
      "command": "bash",
      "args": ["-c", "uvx --from git+https://github.com/BeehiveInnovations/zen-mcp-server.git zen-mcp-server"],
      "env": {
        "GEMINI_API_KEY": "${GEMINI_API_KEY}",
        "OPENAI_API_KEY": "${OPENAI_API_KEY}",
        "DEFAULT_MODEL": "auto",
        "DISABLED_TOOLS": "testgen,secaudit,docgen"
      }
    }
  }
}
```

#### Using BMAD in Cursor
```
@{bmad_folder}/bmm/agents/dev
@{bmad_folder}/bmm/agents/architect
@{bmad_folder}/cis/agents/brainstorming-coach
@{bmad_folder}/index  # Load all agents
```

### OpenCode

#### Configuration (.opencode/config.json)

```json
{
  "mcpServers": {
    "taskmaster": {
      "command": "npx",
      "args": ["task-master-ai"],
      "env": {
        "DATA_DIR": "/absolute/path/to/.taskmaster",
        "ANTHROPIC_API_KEY": "your-key"
      }
    },
    "zen": {
      "command": "python3",
      "args": ["/absolute/path/to/zen-mcp-server/server.py"],
      "env": {
        "GEMINI_API_KEY": "your-key",
        "OPENAI_API_KEY": "your-key"
      }
    }
  }
}
```

### Gemini CLI

#### Configuration (~/.gemini/config.toml)

```toml
[tools]
mcp_enabled = true

[[mcp_servers]]
name = "taskmaster"
command = "node"
args = ["/path/to/task-master-ai/dist/mcp-server.js"]

[mcp_servers.env]
DATA_DIR = "/home/user/.taskmaster"
GOOGLE_API_KEY = "your-gemini-key"

[[mcp_servers]]
name = "zen"
command = "uvx"
args = ["--from", "git+https://github.com/BeehiveInnovations/zen-mcp-server.git", "zen-mcp-server"]

[mcp_servers.env]
GEMINI_API_KEY = "your-key"
```

---

**Last Updated:** 2025-11-16
**Version:** 1.0.0

For project-specific workflow configurations, see [MCP Project Workflows](/shared/mcp-project-workflows/).
