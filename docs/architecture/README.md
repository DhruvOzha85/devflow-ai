# DevFlow AI — Architecture Overview

## 1. System Vision
DevFlow AI is an autonomous AI development orchestration platform designed to bridge high-level conceptual discussions (ChatGPT, Claude conversations) with autonomous agentic execution environments (e.g., Google Antigravity, local CLI agents, MCP-connected agents). It automates task dispatching, context management, test verification, self-healing iteration loops, and delivery validation.

---

## 2. High-Level Component Architecture

```
+-----------------------------------------------------------------------+
|                             USER INTERFACES                           |
|  +---------------------------+       +-----------------------------+  |
|  |     Web Application       |       |      Browser Extension      |  |
|  |       (apps/web)          |       |      (apps/extension)       |  |
|  +-------------+-------------+       +--------------+--------------+  |
+----------------|------------------------------------|-----------------+
                 |                                    |
                 v                                    v
+-----------------------------------------------------------------------+
|                            BACKEND SERVER                             |
|                             (apps/server)                             |
|  - API Gateway & WebSocket Session Server                             |
|  - Workspace & Project State Manager                                  |
|  - Security & Authentication Boundaries                               |
+-----------------------------------|-----------------------------------+
                                    |
                                    v
+-----------------------------------------------------------------------+
|                          ORCHESTRATION LAYER                          |
|                       (packages/orchestrator)                         |
|  - Finite State Machine / Directed Graph Engine                       |
|  - Task Planner, Dispatcher & Retry Supervisor                        |
+--------+--------------------------+-------------------------+---------+
         |                          |                         |
         v                          v                         v
+-------------------+      +------------------+      +------------------+
|   AGENT ADAPTERS  |      |  CONTEXT ENGINE  |      |   VERIFICATION   |
| (agent-adapters)  |      | (context-engine) |      |  (verification)  |
| - Antigravity     |      | - Token Budget   |      | - Unit & E2E     |
| - Claude/ChatGPT  |      | - Diff Context   |      | - Static Lint    |
| - CLI Subagents   |      | - Memory Vault   |      | - Quality Gate   |
+--------+----------+      +------------------+      +------------------+
         |
         v
+-----------------------------------------------------------------------+
|                            INTEGRATION LAYER                          |
|  +--------------------------------+   +----------------------------+  |
|  |           MCP Server           |   |      Antigravity Skills    |  |
|  |      (packages/mcp-server)     |   |    (skills/antigravity)    |  |
|  +--------------------------------+   +----------------------------+  |
+-----------------------------------------------------------------------+
                                    |
                                    v
+-----------------------------------------------------------------------+
|                             SHARED UTILS                              |
|                          (packages/shared)                            |
|             Types, Schemas, Telemetry, Common Utilities               |
+-----------------------------------------------------------------------+
```

---

## 3. Package and Application Boundaries

### Applications (`apps/`)
- **`apps/web`**: Web-based control plane and developer dashboard. Provides interactive job tracking, visual pipeline monitoring, log streaming, and human-in-the-loop approvals.
- **`apps/server`**: Central API service handling communication between frontends, orchestrators, and external notification hooks.
- **`apps/extension`**: Browser extension capturing context and interaction prompts directly from web-based chat agents (ChatGPT, Claude web interfaces) into DevFlow pipelines.

### Core Packages (`packages/`)
- **`packages/orchestrator`**: The workflow execution brain. Manages pipeline state, agent task queueing, retry logic, error classification, and task completion verification.
- **`packages/agent-adapters`**: Pluggable interface abstraction layer connecting DevFlow to different AI coding engines (Google Antigravity, local CLI harnesses, headless agent runtimes).
- **`packages/context-engine`**: Semantic code retrieval, smart file bundling, token budget optimization, and workspace diff distillation.
- **`packages/verification`**: Automated test runners, linters, security scanners, build checkers, and rule conformance validators that ensure code output meets acceptance criteria.
- **`packages/mcp-server`**: Model Context Protocol (MCP) server exposing tools, resources, and workflows to MCP-compliant host agents.
- **`packages/shared`**: Shared TypeScript types, Zod schemas, logging wrappers, error standards, and constants.

### Skills & Customizations (`skills/`)
- **`skills/antigravity`**: Specialized agent skills, workflow definitions, and rules tailored for Google Antigravity pairings.

---

## 4. Key Architectural Tenets
1. **Separation of Concerns**: UI, orchestration, model integration, and code execution are strictly decoupled behind defined schema contracts.
2. **Defensive Verification**: No agent output is accepted until verified by deterministic checks (linter, unit tests, build validation).
3. **Pluggable Agent Backends**: Modular agent adapters ensure DevFlow AI is never locked to a single model provider or execution harness.
4. **Observable by Design**: Structured logs, execution traces, and telemetry provide clear visibility into every agent decision.

