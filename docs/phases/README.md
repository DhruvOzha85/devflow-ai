# DevFlow AI — Planned Implementation Phases

This document outlines the strategic roadmap and phases for the development of the **DevFlow AI** platform. Each phase has strict entry and exit criteria to ensure robust, modular, and verified software delivery.

---

## Phase Matrix

| Phase | Title | Focus Area | Status |
|---|---|---|---|
| **Phase 0** | Foundation Setup | Monorepo structure, tooling, runtime targets, standards, git setup | **Current** |
| **Phase 1** | Shared Core & Schemas | Domain models, event contracts, Zod schemas, shared utilities | Planned |
| **Phase 2** | Context Engine & Workspace Intelligence | Codebase indexing, token optimization, workspace diffing, AST parsing | Planned |
| **Phase 3** | Agent Adapters & MCP Server | Antigravity adapter, CLI agent harnesses, Model Context Protocol server | Planned |
| **Phase 4** | Orchestrator & Workflow Engine | State machine, job scheduling, dependency graphs, self-healing retries | Planned |
| **Phase 5** | Verification & Quality Assurance | Automated test runners, linters, coverage gates, security/secret scans | Planned |
| **Phase 6** | Server & Realtime API Gateway | WebSocket session server, REST API, persistence, event streaming | Planned |
| **Phase 7** | Web Dashboard & Browser Extension | UI control plane, ChatGPT/Claude conversation capture extension | Planned |
| **Phase 8** | Integration & Autonomous Verification | End-to-end integration tests, benchmarking, production hardening | Planned |

---

## Detailed Phase Objectives

### Phase 0: Foundation Setup (Current)
- **Objective**: Establish the foundational monorepo structure, tooling configuration, runtime environment, and architectural blueprints without introducing premature application code.
- **Key Deliverables**:
  - Monorepo directory tree (`apps/*`, `packages/*`, `skills/*`, `docs/*`).
  - PNPM workspace configuration targeting Node.js 22 LTS.
  - Standardized `.editorconfig`, `.gitignore`, MIT License.
  - Core architectural documentation and development phase roadmap.
  - Environment and Git remote verification.

### Phase 1: Shared Core & Schemas
- **Objective**: Define strict domain models, contracts, and shared primitives that govern all inter-package interactions.
- **Key Deliverables**:
  - TypeScript definitions and Zod validation schemas for tasks, agent events, and artifacts.
  - Structured error hierarchy and universal logger interface in `packages/shared`.
  - Type-safe event bus definitions for inter-service messaging.

### Phase 2: Context Engine & Workspace Intelligence
- **Objective**: Provide AI agents with compact, high-signal codebase context while minimizing token burn.
- **Key Deliverables**:
  - Incremental file tree summarization and semantic indexing.
  - Git diff extractor and hunk distillation.
  - Dynamic token-budget allocator prioritizing active edits and dependencies.

### Phase 3: Agent Adapters & MCP Server
- **Objective**: Build normalized connection interfaces for multiple coding agents and expose DevFlow tools via MCP.
- **Key Deliverables**:
  - Pluggable agent adapter contracts (`packages/agent-adapters`).
  - Google Antigravity integration adapter and prompt skill bundles (`skills/antigravity`).
  - MCP server implementation (`packages/mcp-server`) with tool definitions for code actions, task updates, and report generation.

### Phase 4: Orchestrator & Workflow Engine
- **Objective**: Implement the autonomous execution loop, coordinating multi-step development plans.
- **Key Deliverables**:
  - Directed Acyclic Graph (DAG) task engine in `packages/orchestrator`.
  - State persistence for running jobs and checkpoints.
  - Failure classification (syntax, test failure, environment error) and dynamic retry strategy.

### Phase 5: Verification & Quality Assurance
- **Objective**: Enforce strict verification criteria before task outputs can be considered done.
- **Key Deliverables**:
  - Test runner wrappers (Jest/Vitest, native test runners) in `packages/verification`.
  - Static analysis, format checks, and secret scanner hooks.
  - Automated pull request and diff verification gates.

### Phase 6: Server & Realtime API Gateway
- **Objective**: Provide the persistent backend service managing active projects, runs, and live updates.
- **Key Deliverables**:
  - REST & WebSocket endpoints in `apps/server`.
  - Persistent state store for task runs, audit logs, and project metadata.
  - Real-time event broadcasting to web clients.

### Phase 7: Web Dashboard & Browser Extension
- **Objective**: Build the user-facing control plane and bridge external AI web chats into DevFlow.
- **Key Deliverables**:
  - Web UI (`apps/web`) with pipeline visualization, live log viewer, and approval prompts.
  - Browser extension (`apps/extension`) allowing one-click export of ChatGPT/Claude chat instructions into DevFlow pipelines.

### Phase 8: Integration & Autonomous Verification
- **Objective**: Perform complete end-to-end testing of autonomous coding workflows on real repositories.
- **Key Deliverables**:
  - Continuous integration workflows in `.github/workflows`.
  - End-to-end task execution benchmarks.
  - Production deployment guides and documentation release.

