<div align="center">

# Zhishu Agent (知枢智能体) — Harness Engineering Patterns

### Build Production-Grade Coding Agents & Harness Control Planes from Scratch: Java 17 (Spring Boot 3) Full-Stack Studio + Zero-Dependency Python Pattern Labs

[![Java](https://img.shields.io/badge/Java-17_+_Spring_Boot_3.3-ED8B00?style=flat-square&logo=springboot&logoColor=white)](#-1-java-17--spring-boot-3-full-stack-workbench-harness-agent)
[![Python](https://img.shields.io/badge/Python-3.9+_Zero_Deps-3776AB?style=flat-square&logo=python&logoColor=white)](#-2-zero-dependency-python-8-pattern-labs--wg-harness-cli)
[![MCP](https://img.shields.io/badge/Protocol-MCP_JSON--RPC_2.0-2E5AA8?style=flat-square)](#-2-zero-dependency-python-8-pattern-labs--wg-harness-cli)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](./LICENSE)
[![Stars](https://img.shields.io/github/stars/wangguode/zhishu-agent?style=flat-square)](https://github.com/wangguode/zhishu-agent/stargazers)

**🇺🇸 English** | [🇨🇳 简体中文](./README.zh-CN.md) · [📖 Architecture Deep-Dive (DEV.to)](https://dev.to/wangguode/self-healing-coding-agents-how-to-build-a-production-grade-harness-loop-with-mcp-48i9) · [🎙️ HardCall (52ms Voice AI)](https://github.com/wangguode/hardcall) · [📊 StatementFlow AI](https://github.com/wangguode/statementflow-ai)

**The model sets the ceiling. The Harness sets the floor.**
<br>Dual-engine implementation featuring a **Java 17 + Spring Boot 3 Full-Stack Web/Desktop Studio** and a **zero-dependency Python CLI & lab suite**. Run the complete Agent Loop, HITL approval gates, `/compact` context compaction, MCP JSON-RPC 2.0 sandbox, and test-driven self-healing loop out of the box with zero API keys—or switch to DeepSeek / Qwen / OpenAI-compatible endpoints via a single environment variable.

</div>

---

## Editorial Architecture Overview

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./docs/assets/architecture-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="./docs/assets/architecture-light.svg">
    <img alt="Zhishu Agent Harness Architecture" src="./docs/assets/architecture-light.svg" width="100%">
  </picture>
</p>

---

## Why Zhishu Agent?

Production coding agents like Codex, Claude Code, and AgentScope span hundreds of thousands of lines. When engineering teams deploy Java or Python agent control planes inside an enterprise, they consistently hit five core architectural bottlenecks:

1. **Agent Loop Convergence & Self-Verification**: How to guarantee the agent converges inside a *Reason → Edit → Run Tests → Parse Stderr → Self-Heal* loop instead of hallucinating "All done!" without running tests.
2. **PreToolUse / PostToolUse Guardrails & HITL**: How to block `rm -rf /` in milliseconds, suspend a `CompletableFuture` on `kubectl rollout restart` pending human approval, and automatically mask `sk-*` secrets in stdout.
3. **Two-Tier `/compact` Context Compaction**: How to prune oversized tool outputs and synthesize structured Checkpoint summaries when long tasks approach context saturation (saving **85%+ tokens** in benchmarks).
4. **3-Tier Progressive Skills Disclosure & MCP JSON-RPC 2.0**: How to mount hundreds of enterprise skills without bloating the system prompt, and implement standard MCP `initialize` / `tools/list` / `tools/call`.
5. **Time-Decayed Cross-Session Memory**: How to combine a `14-day half-life × importance × lexical overlap` scoring function so agents retain institutional knowledge without stale memory pollution.

---

## 1. Java 17 + Spring Boot 3 Full-Stack Workbench (`Harness Agent`)

Built for enterprise Java backends and cross-platform desktop workflows (`java-harness-studio/`, `web-ui/`, `desktop-shell/`), powered by **Java 17 + Spring Boot 3.3.5 + Next.js/React + Electron (macOS / Windows)**:

### Main Conversation & Trace View (ReAct Tooling + Self-Verification Loop + Live Diff Drawer)
<p align="center">
  <img alt="Harness Agent Main Conversation & Trace View" src="./docs/assets/studio-preview.png" width="100%">
</p>

### Tools & MCP Server Registry (One-Click Toggle & JSON-RPC 2.0 Debugger)
<p align="center">
  <img alt="Harness Agent MCP & Tools Registry" src="./docs/assets/studio-mcp-tools.png" width="100%">
</p>

### Progressive Agent Skills (`SKILL.md`) Manager
<p align="center">
  <img alt="Harness Agent Skills Manager" src="./docs/assets/studio-skills.png" width="100%">
</p>

### 30-Second Cross-Platform Quick Start

```bash
git clone https://github.com/wangguode/zhishu-agent.git
cd zhishu-agent

# Option A: macOS / Linux Web Studio (auto-builds & opens http://127.0.0.1:8090)
./start-mac-linux.sh

# Option B: Windows 10/11 Web Studio
start-windows.bat

# Option C: Standalone Electron Desktop App (macOS .dmg / Windows .exe)
cd desktop-shell
npm install
npm start            # Launch desktop shell with embedded Java 17 engine
npm run build:mac    # Package macOS installer (dist/*.dmg, dist/*.zip)
npm run build:win    # Package Windows installer (dist/*.exe)
```

> **Connect a Live LLM (DeepSeek / Qwen / OpenAI-compatible):**
> ```bash
> export RUN_MODE=cloud
> export LLM_BASE_URL=https://api.deepseek.com/v1
> export LLM_API_KEY=sk-your-key
> export LLM_MODEL=deepseek-chat
> mvn spring-boot:run
> ```

---

## 2. Zero-Dependency Python 8-Pattern Labs & `wg-harness` CLI

Each core pattern is distilled into a standalone, zero-dependency Python standard-library script—runnable directly or mountable into Claude Code / Cursor as a live `stdio` MCP Server via `wg-harness`:

| # | Pattern | Java Core Class | Python Lab | Quick Run |
| :-: | :--- | :--- | :--- | :--- |
| 01 | **Agent Loop & Escalation** | `kernel/AgentLoopEngine.java` | [01_agent_loop](./labs/01_agent_loop/agent_loop.py) | `python3 labs/01_agent_loop/agent_loop.py` |
| 02 | **Two-Tier `/compact` Compaction** | `context/ContextCompactorService.java` | [02_context_compaction](./labs/02_context_compaction/compaction.py) | `python3 labs/02_context_compaction/compaction.py` |
| 03 | **3-Tier Progressive Skills** | `mcp/McpToolRegistryService.java` | [03_skills_progressive_disclosure](./labs/03_skills_progressive_disclosure/skills_loader.py) | `python3 labs/03_skills_progressive_disclosure/skills_loader.py` |
| 04 | **Parallel Subagent Orchestration** | `kernel/AgentLoopEngine.java` | [04_subagent_orchestration](./labs/04_subagent_orchestration/subagents.py) | `python3 labs/04_subagent_orchestration/subagents.py` |
| 05 | **Hooks Guardrails & Secret Masking** | `guard/HookGuardrailService.java` | [05_hooks_guardrails](./labs/05_hooks_guardrails/hooks.py) | `python3 labs/05_hooks_guardrails/hooks.py` |
| 06 | **Time-Decayed Memory Store** | `memory/DecayMemoryStore.java` | [06_agent_memory](./labs/06_agent_memory/memory.py) | `python3 labs/06_agent_memory/memory.py` |
| 07 | **MCP Server (JSON-RPC 2.0)** | `mcp/McpToolRegistryService.java` | [07_mcp_server_stdio](./labs/07_mcp_server_stdio/mcp_stdio.py) | `python3 labs/07_mcp_server_stdio/mcp_stdio.py` |
| 08 | **Test-Driven Self-Verification Loop** | `kernel/AgentLoopEngine.java` | [08_self_verification_loop](./labs/08_self_verification_loop/verify_loop.py) | `python3 labs/08_self_verification_loop/verify_loop.py` |

```bash
pip install -e .
wg-harness list
wg-harness run all
wg-harness mcp-stdio   # Standard stdio MCP Server for Claude Code / Cursor
```

---

## Repository Structure

```text
zhishu-agent/
├── java-harness-studio/                            # Java 17 + Spring Boot 3.3 Full-Stack Studio
│   ├── pom.xml
│   └── src/main/
│       ├── java/com/wangguoai/harness/
│       │   ├── HarnessStudioApplication.java       # Spring Boot entry point (port 8090)
│       │   ├── api/HarnessStudioController.java    # REST + SSE streaming controller
│       │   ├── kernel/AgentLoopEngine.java         # Agent Loop, self-healing & HITL state machine
│       │   ├── guard/HookGuardrailService.java     # PreToolUse 3-tier guard + PostToolUse masking
│       │   ├── context/ContextCompactorService.java# Two-tier /compact pruning & checkpointing
│       │   ├── mcp/McpToolRegistryService.java     # Standard JSON-RPC 2.0 MCP Server & Skills
│       │   └── memory/DecayMemoryStore.java        # 14-day half-life decayed memory store
│       └── resources/static/                       # Editorial Tech adaptive web console
├── labs/01_agent_loop ~ 08_self_verification_loop/ # Zero-dependency Python pattern labs
├── wg_harness_cli.py & pyproject.toml              # `wg-harness` CLI & stdio MCP entry point
└── docs/assets/                                    # Light/dark vector architecture & UI previews
```

---

## Acknowledgments & License

Control-plane patterns and architecture draw inspiration from [agentscope-ai/agentscope-java](https://github.com/agentscope-ai/agentscope-java), [alibaba/spring-ai-alibaba](https://github.com/alibaba/spring-ai-alibaba), [openai/codex](https://github.com/openai/codex), [anthropics/skills](https://github.com/anthropics/skills), and [modelcontextprotocol](https://github.com/modelcontextprotocol).

[MIT](./LICENSE) © 2026 Wang Guo (`wangguode`)
