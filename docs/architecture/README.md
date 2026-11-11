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
|  |   (apps/web - Phase 7)    |       |  (apps/extension - Phase 8) |  |
|  +-------------+-------------+       +--------------+--------------+  |
+----------------|------------------------------------|-----------------+
                 |                                    |
                 v                                    v
+-----------------------------------------------------------------------+
|                            BACKEND SERVER                             |
|                        (apps/server - Phase 1)                        |
|  - Unified Single Framework API Gateway (Fastify or Express)          |
|  - Realtime WebSocket Session Server                                  |
|  - Persistence Foundation (Task state, runs, checkpoints)             |
+-----------------------------------|-----------------------------------+
                                    |
                                    v
+-----------------------------------------------------------------------+
|                          ORCHESTRATION LAYER                          |
|                     (packages/orchestrator)                           |
|  - DAG Task Planner & Execution State Machine (Phase 3)               |
|  - Autonomous Closed Loop & Self-Healing Retry Supervisor (Phase 5)   |
+--------+--------------------------+-------------------------+---------+
         |                          |                         |
         v                          v                         v
+-------------------+      +------------------+      +------------------+
|   AGENT ADAPTERS  |      |  CONTEXT ENGINE  |      |   VERIFICATION   |
| (agent-adapters)  |      | (context-engine) |      |  (verification)  |
| - Antigravity CLI |      | - Conversation   |      | - Deterministic  |
|   Proof-of-Concept|      |   Import & Parser|      |   Quality Gates  |
|   & Adapter       |      |   (Phase 2)      |      | - Static Lint,   |
|   (Phase 4)       |      | - Token Budget   |      |   Unit & E2E     |
| - Local CLI Agents|      |   Optimization   |      |   Tests (Phase 6)|
+--------+----------+      +------------------+      +------------------+
         |
         v
+-----------------------------------------------------------------------+
|                            INTEGRATION LAYER                          |
|  +--------------------------------+   +----------------------------+  |
|  |           MCP Server           |   |      Antigravity Skills    |  |
|  |  (packages/mcp-server - Phase 4)   |   | (skills/antigravity - Ph 8)|  |
|  +--------------------------------+   +----------------------------+  |
+-----------------------------------------------------------------------+
                                    |
                                    v
+-----------------------------------------------------------------------+
|                             SHARED UTILS                              |
|                      (packages/shared - Phase 1)                      |
|             Types, Schemas, Telemetry, Common Utilities               |
+-----------------------------------------------------------------------+
```

---

## 3. Package and Application Boundaries

### Applications (`apps/`)
- **`apps/web` (Planned - Phase 7)**: Web-based control plane and developer dashboard. Provides interactive job tracking, visual DAG pipeline monitoring, log streaming, and human-in-the-loop approvals.
- **`apps/server` (Planned - Phase 1)**: Central API and WebSocket service built upon a single evaluated framework (Fastify or Express). Houses the persistence foundation (state, runs, checkpoints) required by the orchestration engine.
- **`apps/extension` (Planned - Phase 8)**: Browser extension capturing context and interaction prompts directly from web-based chat interfaces (ChatGPT, Claude) into DevFlow pipelines.

### Core Packages (`packages/`)
- **`packages/shared` (Planned - Phase 1)**: Shared TypeScript types, Zod domain schemas, error classes, and common utilities governing all inter-package contracts.
- **`packages/context-engine` (Planned - Phase 2)**: Conversation import parsers (JSON, Markdown), prompt normalization, and token-budget optimization.
- **`packages/orchestrator` (Planned - Phases 3 & 5)**: The workflow execution brain.
  - *Phase 3 (Orchestration Engine)*: Task DAG graph planner, step dependency management, and lifecycle state machine.
  - *Phase 5 (Autonomous Loop)*: Closed-loop execution supervisor, failure classification, dynamic retry supervisor, and session recovery.
- **`packages/agent-adapters` (Planned - Phase 4)**: Pluggable interface abstraction layer connecting DevFlow to AI coding engines, validated with a minimal Google Antigravity CLI proof-of-concept before architectural coupling.
- **`packages/mcp-server` (Planned - Phase 4)**: Model Context Protocol (MCP) server exposing workspace tools and task progress to host agents.
- **`packages/verification` (Planned - Phase 6)**: Dedicated, deterministic verification subsystem. Operates independently of agent orchestration to run automated test harnesses, linters, git diff validators, and acceptance criteria checks.

### Skills & Customizations (`skills/`)
- **`skills/antigravity` (Planned - Phase 8)**: Specialized agent skills, workflow definitions, and behavioral rules tailored for Google Antigravity pairings.

### Infrastructure & Tooling (`scripts/`, `tests/`, `.github/`)
- **`tests/` & `.github/workflows/` (Planned - Phase 9)**: Cross-package integration suites, automated CI/CD pipelines, and production containerization.

---

## 4. Key Architectural Tenets & Subsystem Separation
1. **Explicit Subsystem Boundaries**: The **Autonomous Loop** (`packages/orchestrator` - Phase 5) and the **Verification Engine** (`packages/verification` - Phase 6) are strictly decoupled. The orchestrator supervises agent execution and retries; the verification engine enforces deterministic, non-agentic quality gates.
2. **Persistence-Backed Orchestration**: The persistence foundation in `apps/server` (Phase 1) directly underpins the DAG state machine (Phase 3), ensuring state durability and session recovery.
3. **Single Backend Framework**: Rather than supporting multiple competing web frameworks, Phase 1 evaluates and commits to exactly one framework (Fastify or Express) based on throughput and developer ergonomics.
4. **Validation Before Architectural Dependency**: External agent runtimes (specifically Google Antigravity in Phase 4) must pass a minimal CLI invocation proof-of-concept before core adapters depend upon them.
5. **Separation of Concerns**: UI, orchestration, model integration, and code verification are strictly decoupled behind type-safe schema contracts (`packages/shared`).
6. **Observable by Design**: Structured logs, execution traces, and telemetry provide clear visibility into every agent decision.
