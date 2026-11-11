# DevFlow AI

> **Autonomous AI Development Orchestration Platform**  
> Bridging AI conversations with autonomous coding agents, automated execution, testing, and verified code delivery.

---

## 1. Project Introduction & Vision
Modern software engineering increasingly relies on AI reasoning models (such as ChatGPT, Claude, and Gemini) to architect solutions, but manually translating conversation prompts into local file changes, test executions, and terminal sessions remains tedious and error-prone.

**DevFlow AI** is designed as an autonomous orchestration platform that takes high-level architectural instructions and specifications from AI conversations, converts them into actionable task graphs, dispatches them to specialized coding agents (such as Google Antigravity and CLI agents), monitors their progress, runs rigorous verification suites, and automatically retries upon failure until the task is proven complete.

### Core Objectives
- **End-to-End Task Orchestration**: Automate the transition from conversational specification to tested code.
- **Agent Agnostic Execution**: Connect seamlessly with Google Antigravity, MCP-compliant tools, and CLI coding agents.
- **Autonomous Feedback & Self-Healing**: Detect test or build failures and feed contextual diffs back into agents for correction.
- **Verification-First Delivery**: Gate all deliveries behind deterministic quality checks (tests, linters, security audits).

---

## 2. Planned Capabilities
- **Chat Capture**: Capture project specifications directly from conversational AI chats (via browser extension or API).
- **DAG Workflow Engine**: Decompose requests into structured task graphs with dependencies and parallel workstreams.
- **Dynamic Context Pruning**: Provide agents with precise code context, avoiding token exhaustion while maximizing code comprehension.
- **Google Antigravity Integration**: Native adapter and custom skills tailored for Google Antigravity coding environments.
- **MCP Tool Integration**: Standard Model Context Protocol (MCP) server for tool discovery, invocation, and workspace instrumentation.
- **Automated Verification Loop**: Built-in test execution, lint checks, build checks, and secret scans before accepting changes.
- **Web Control Plane**: Interactive real-time dashboard visualizing runs, logs, diffs, and approval gates.

---

## 3. Technology Stack
- **Monorepo Management**: [pnpm](https://pnpm.io/) Workspaces
- **Runtime Environment**: [Node.js](https://nodejs.org/) (Target: v22 LTS)
- **Language**: TypeScript (ESM modules)
- **Protocol & Interfaces**: Model Context Protocol (MCP), REST, WebSockets
- **Agent Ecosystem**: Google Antigravity, Anthropic Claude, OpenAI, and local coding CLI agents
- **Testing & Quality**: Deterministic test runners, ESLint/Prettier (configured in upcoming phases)

---

## 4. Repository Structure

```text
devflow-ai/
├── apps/
│   ├── extension/          # Browser extension for chat context capture
│   ├── server/             # API Gateway, WebSocket hub, and project state
│   └── web/                # Web dashboard and monitoring interface
├── packages/
│   ├── agent-adapters/     # Adapters for Antigravity, Claude, and CLI agents
│   ├── context-engine/     # AST parsing, code retrieval, token optimization
│   ├── mcp-server/         # Model Context Protocol server implementation
│   ├── orchestrator/       # DAG task scheduler, state machine, retry supervisor
│   ├── shared/             # Common TypeScript types, schemas, and utilities
│   └── verification/       # Automated test runner and quality gates
├── skills/
│   └── antigravity/        # Custom Antigravity skills and rules
├── docs/
│   ├── architecture/       # System architecture documentation
│   ├── phases/             # Phase-by-phase implementation plans
│   └── reports/            # Execution and milestone reports
├── tests/                  # Cross-package integration and E2E test suites
├── scripts/                # Development, build, and CI/CD utility scripts
├── .github/
│   └── workflows/          # GitHub Actions CI/CD workflows
├── .editorconfig           # Consistent editor formatting rules
├── .gitignore              # Ignored files, outputs, secrets, and caches
├── LICENSE                 # MIT License
├── package.json            # Monorepo root configuration
├── pnpm-workspace.yaml     # pnpm workspace package definitions
└── README.md               # Repository documentation
```

---

## 5. Prerequisites
Before getting started, ensure you have the following installed on your machine:
- **Node.js**: `v22.0.0` or later (LTS recommended)
- **pnpm**: `v9.0.0` or later (`corepack enable` or `npm install -g pnpm`)
- **Git**: `2.30+` installed and configured

---

## 6. Installation & Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/DhruvOzha85/devflow-ai.git
   cd devflow-ai
   ```

2. **Install workspace dependencies:**
   ```bash
   pnpm install
   ```

3. **Verify repository setup:**
   ```bash
   pnpm test
   ```

---

## 7. Development Workflow
- **Branching Strategy**: Branch from `main` using descriptive names (e.g., `feat/phase-1-schemas`, `fix/adapter-timeout`).
- **Commits**: Follow conventional commits (`feat:`, `fix:`, `docs:`, `chore:`).
- **Quality Gates**: All code submissions must pass static analysis and unit tests before merging.
- **Security**: Never commit `.env` files, credentials, or proprietary API tokens.

---

## 8. Current Development Status
- **Current Milestone**: **Phase 0 — Foundation Setup** (Completed)
- **Focus**: Setting up workspace architecture, repository hygiene, runtime targets, and documentation.
- **Application Logic**: No application, agent, or database code is implemented yet in adherence to Phase 0 constraints.

---

## 9. Planned Implementation Phases
See [docs/phases/README.md](docs/phases/README.md) for the detailed phase roadmap:
1. **Phase 0**: Foundation Setup *(Current)*
2. **Phase 1**: Shared Core & Contract Schemas
3. **Phase 2**: Context Engine & Workspace Intelligence
4. **Phase 3**: Agent Adapters & MCP Server Integration
5. **Phase 4**: Orchestrator & Task Lifecycle Engine
6. **Phase 5**: Verification & Quality Assurance Pipeline
7. **Phase 6**: Backend Service & API Gateway
8. **Phase 7**: Web Dashboard & Browser Extension
9. **Phase 8**: Autonomous Integration & Production Hardening

---

## License
Distributed under the [MIT License](LICENSE).
