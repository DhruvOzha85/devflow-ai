# DevFlow AI — Planned Implementation Phases

This document outlines the authoritative strategic roadmap and phases for the development of the **DevFlow AI** platform. Each phase has strict entry and exit criteria to ensure robust, modular, and verified software delivery.

---

## Authoritative Phase Matrix

| Phase | Title | Primary Monorepo Packages | Focus Area | Status |
|---|---|---|---|---|
| **Phase 0** | **Foundation** | Root, tooling, structure | Monorepo layout, pnpm workspaces, Node 22 LTS, baseline docs, git setup | **Completed** |
| **Phase 1** | **Core Backend** | `packages/shared`, `apps/server` | Framework evaluation & single selection, shared domain contracts, API/WebSocket server, persistence foundation | Planned |
| **Phase 2** | **Conversation Import** | `packages/context-engine` | ChatGPT & Claude export parsing (JSON/Markdown), prompt normalization, context extraction | Planned |
| **Phase 3** | **Orchestration Engine** | `packages/orchestrator` | Task graph DAG planner, job scheduler, execution state machine, step dependencies | Planned |
| **Phase 4** | **Antigravity Integration** | `packages/agent-adapters`, `packages/mcp-server` | Antigravity CLI proof-of-concept, adapter abstraction, MCP server tools | Planned |
| **Phase 5** | **Autonomous Loop** | `packages/orchestrator` | Closed-loop execution: agent dispatch, failure detection, retry supervisor, checkpoint recovery | Planned |
| **Phase 6** | **Verification Engine** | `packages/verification` | Deterministic quality gates, test runner wrappers, static analysis, diff acceptance verification | Planned |
| **Phase 7** | **Web Dashboard** | `apps/web` | Real-time frontend: job monitor, visual DAG status, log streaming, human approval UI | Planned |
| **Phase 8** | **Extension & Skills** | `apps/extension`, `skills/antigravity` | Browser extension for chat capture from web UIs, specialized Antigravity prompt skills & rules | Planned |
| **Phase 9** | **Production Readiness** | `.github/workflows`, `scripts/`, docs | End-to-end integration tests, CI/CD pipeline, security scanning, deployment readiness | Planned |

---

## Detailed Phase Objectives & Architectural Boundaries

### Phase 0: Foundation (Completed)
- **Objective**: Establish the foundational monorepo structure, tooling configuration, runtime environment, and architectural blueprints without introducing application code.
- **Deliverables**:
  - Monorepo directory topology (`apps/*`, `packages/*`, `skills/*`, `docs/*`, `tests/`, `scripts/`, `.github/`).
  - PNPM workspace configuration targeting Node.js 22 LTS.
  - Standardized `.editorconfig`, `.gitignore`, MIT License.
  - Core architectural documentation and authoritative Phase 0–9 development roadmap.
  - Environment inspection and Git remote verification.
- **Status**: Completed and audited.

### Phase 1: Core Backend (Planned)
- **Objective**: Select a single backend framework, define shared domain models and contracts, and establish the server runtime and persistence foundation required by the orchestration engine.
- **Architectural Refinements & Deliverables**:
  - **Framework Evaluation & Single Selection**: Conduct a concise architectural comparison between Fastify and Express, selecting exactly one runtime framework based on throughput, TypeScript typing, and WebSocket support. Do not implement both.
  - **Shared Domain Contracts (`packages/shared`)**: Define type-safe domain models, Zod schemas for tasks and agent events, and structured error standards.
  - **Server Runtime (`apps/server`)**: Implement the initial HTTP API and WebSocket event broadcasting hub using the selected framework.
  - **Persistence Foundation**: Implement the persistence foundation (e.g., SQLite via Kysely/Drizzle or structured file/document state store) required to persist task states, pipeline runs, and checkpoints for Phase 3.

### Phase 2: Conversation Import (Planned)
- **Objective**: Build the ingestion pipeline to parse, sanitize, and normalize exported conversations from ChatGPT and Claude into structured project tasks.
- **Deliverables**:
  - Implemented in `packages/context-engine`.
  - Parsers for exported conversation formats (JSON conversation dumps, raw Markdown threads, structured prompts).
  - Context extraction pipeline separating conversational chatter from technical specifications, architectural requirements, and task lists.
  - Token-budget optimization and prompt normalization.

### Phase 3: Orchestration Engine (Planned)
- **Objective**: Construct the workflow execution brain capable of decomposing specifications into Directed Acyclic Graphs (DAGs) with managed state transitions.
- **Deliverables**:
  - Implemented in `packages/orchestrator`.
  - DAG task planner calculating dependency graphs and parallel execution stages.
  - State machine governing task life cycles (`PENDING`, `IN_PROGRESS`, `VERIFYING`, `COMPLETED`, `FAILED`, `BLOCKED`).
  - Integration with the Phase 1 persistence layer for job resume and historical logging.

### Phase 4: Antigravity Integration (Planned)
- **Objective**: Connect the orchestration engine to the Google Antigravity coding environment and expose tools via the Model Context Protocol (MCP).
- **Architectural Refinements & Deliverables**:
  - **Minimal Proof-of-Concept (PoC)**: Build and execute a minimal standalone PoC validating actual Antigravity CLI invocation, argument passing, and response capture before creating architectural dependencies upon it.
  - **Agent Adapter Interface (`packages/agent-adapters`)**: Pluggable interface isolating Antigravity from other potential CLI agent engines.
  - **MCP Server (`packages/mcp-server`)**: Standard Model Context Protocol server exposing workspace inspection tools, task progress notifications, and context injection to host agents.

### Phase 5: Autonomous Loop (Planned)
- **Objective**: Build the closed-loop supervisor in `packages/orchestrator` that orchestrates agent dispatching, execution event capture, failure classification, and self-healing retries.
- **Subsystem Boundary Note**: Operates as a distinct orchestration supervisor separate from the deterministic verification engine (Phase 6).
- **Deliverables**:
  - Agent dispatcher coordinating task execution according to DAG ordering.
  - Real-time execution monitor listening to agent streaming outputs and exit codes.
  - Failure classifier distinguishing between environment errors, syntax errors, and test failures.
  - Dynamic self-healing retry supervisor feeding error diffs back to the agent up to configured retry limits.
  - Checkpoint and state recovery handling interrupted sessions.

### Phase 6: Verification Engine (Planned)
- **Objective**: Implement the dedicated, deterministic verification subsystem in `packages/verification` that validates agent output against quality gates before changes can be accepted.
- **Subsystem Boundary Note**: Operates independently of agent orchestration; executes non-agentic deterministic checks.
- **Deliverables**:
  - Test runner harness executing unit, integration, and end-to-end tests.
  - Static analysis, format verification, and security/secret linting gates.
  - Git diff inspection verifying that file modifications strictly align with assigned task scope.
  - Quality gate reporting generating structured verification certificates (`PASSED` / `FAILED` with diagnostics).

### Phase 7: Web Dashboard (Planned)
- **Objective**: Deliver a real-time developer control plane in `apps/web` for pipeline observability and human-in-the-loop control.
- **Deliverables**:
  - Real-time DAG visualizer displaying active workstreams and task progress.
  - Live log and event streaming view connected via WebSocket to `apps/server`.
  - Diff review and manual approval modal for sensitive operations (file deletion, deployment, external requests).
  - Task run history and audit dashboard.

### Phase 8: Extension & Skills (Planned)
- **Objective**: Provide browser-level conversation capture and specialized Antigravity agent instructions.
- **Deliverables**:
  - **Browser Extension (`apps/extension`)**: Lightweight extension to capture and export active conversations from ChatGPT and Claude web interfaces directly to the DevFlow backend with one click.
  - **Antigravity Skills (`skills/antigravity`)**: Prompt bundles, custom skill definitions, and behavioral rules tailored for Google Antigravity agent execution.

### Phase 9: Production Readiness (Planned)
- **Objective**: Harden the platform for reliable, reproducible deployment and automated verification.
- **Deliverables**:
  - Comprehensive end-to-end workflow integration test suite in `tests/`.
  - GitHub Actions CI/CD workflows in `.github/workflows/` (testing, linting, security scans).
  - Production containerization and deployment scripts in `scripts/`.
  - Complete user manuals, API documentation, and contributor guidelines.
