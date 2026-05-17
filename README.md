# 🏗️ Awesome Harness Engineering [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> **The most comprehensive, information-dense collection of resources for harness engineering** — the practice of shaping the environment around AI agents so they work reliably in real-world production systems.

Harness engineering sits at the intersection of **context engineering**, **evaluation**, **observability**, **orchestration**, **safe autonomy**, and **software architecture**. While an agent is the model plus its tools, the *harness* is everything else: the constraints, state management, verification loops, and runtime infrastructure that make agents dependable.

```
┌─────────────────────────────────────────────────────────────────┐
│                        AGENT HARNESS                            │
│                                                                 │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐  ┌───────────────┐  │
│  │ Context  │  │ Guardrails│  │  Evals &  │  │   Runtime &   │  │
│  │ Engine   │  │ & Safety │  │Observability│ │ Orchestration │  │
│  └────┬─────┘  └────┬─────┘  └─────┬─────┘  └──────┬────────┘  │
│       │              │              │               │           │
│       └──────────────┴──────┬───────┴───────────────┘           │
│                             │                                   │
│                      ┌──────┴──────┐                            │
│                      │  LLM Agent  │                            │
│                      │ (Model+Tools)│                           │
│                      └─────────────┘                            │
│                                                                 │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐  ┌───────────────┐  │
│  │ Memory & │  │  Specs & │  │ Sandbox & │  │  Benchmarks   │  │
│  │  State   │  │Agent Files│  │ Execution │  │               │  │
│  └──────────┘  └──────────┘  └───────────┘  └───────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

**Why this list?** The shift from *prompt engineering* → *context engineering* → *harness engineering* marks a maturation of the AI engineering discipline. This list tracks that evolution with primary sources, not commentary.

---

## 📑 Contents

- [Foundations](#-foundations)
  - [Seminal Articles](#seminal-articles)
  - [Evolution & Big Picture](#evolution--big-picture)
- [Context, Memory & Working State](#-context-memory--working-state)
  - [Context Engineering](#context-engineering)
  - [Memory & State Management](#memory--state-management)
  - [Structured Output (Agent I/O Harness)](#structured-output-agent-io-harness)
- [Constraints, Guardrails & Safe Autonomy](#%EF%B8%8F-constraints-guardrails--safe-autonomy)
  - [Safety & Control Patterns](#safety--control-patterns)
  - [Guardrail Frameworks](#guardrail-frameworks)
- [Specs, Agent Files & Workflow Design](#-specs-agent-files--workflow-design)
  - [Agent Instruction Standards](#agent-instruction-standards)
  - [Workflow & Orchestration Design](#workflow--orchestration-design)
- [Evals & Observability](#-evals--observability)
  - [Evaluation Guides & Frameworks](#evaluation-guides--frameworks)
  - [Observability Platforms](#observability-platforms)
- [Benchmarks](#-benchmarks)
  - [Evaluation Frameworks & Tools](#evaluation-frameworks--tools)
- [Runtimes, Harnesses & Reference Implementations](#%EF%B8%8F-runtimes-harnesses--reference-implementations)
  - [Agent SDKs & Frameworks](#agent-sdks--frameworks)
  - [Sandbox & Execution Environments](#sandbox--execution-environments)
  - [Reference Implementations](#reference-implementations)
- [MCP (Model Context Protocol)](#-mcp-model-context-protocol)
- [Coding Agents in Practice](#-coding-agents-in-practice)
  - [Tools & Products](#tools--products)
  - [Field Reports from Coding Agent Companies](#field-reports-from-coding-agent-companies)
- [Production Deployment](#-production-deployment)
- [Academic Research](#-academic-research)
  - [Harness & Context Engineering](#harness--context-engineering)
  - [Agent Reliability & Safety](#agent-reliability--safety)
  - [Evaluation & Benchmarking](#evaluation--benchmarking)
- [Learning Resources & Curated Lists](#-learning-resources--curated-lists)
- [Contributing](#contributing)
- [License](#license)

---

## 🏛️ Foundations

### Seminal Articles

The foundational writings that defined harness engineering as a discipline.

| Source | Article | Description |
|:------:|---------|-------------|
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/) | The article that coined "harness engineering" — how OpenAI built a large application with Codex using architectural constraints, repo-local instructions, browser validation, and telemetry |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) | Core article on initializer agents, feature lists, `init.sh`, self-verification, and handoff artifacts across many context windows |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps) | GAN-inspired multi-agent harness — generator/evaluator loop for autonomous frontend design and long-running app generation |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Building effective agents](https://www.anthropic.com/research/building-effective-agents) | Foundational guide distinguishing workflows vs. agents, with composable patterns for building reliable systems |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [The Anatomy of an Agent Harness](https://blog.langchain.com/the-anatomy-of-an-agent-harness/) | Derives harness components from first principles: prompts, tools, middleware, orchestration, and runtime infrastructure |
| ![Thoughtworks](https://img.shields.io/badge/Thoughtworks-F2617A?style=flat) | [Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html) | Framing harness work into context engineering, architectural constraints, and "garbage collection" against entropy |
| ![HumanLayer](https://img.shields.io/badge/HumanLayer-FF6B35?style=flat) | [Skill Issue: Harness Engineering for Coding Agents](https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents) | A practical argument that weak results from coding agents are often harness problems, not model problems |
| ![Inngest](https://img.shields.io/badge/Inngest-5D5FEF?style=flat) | [Your Agent Needs a Harness, Not a Framework](https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework) | Why state, retries, traces, and concurrency are first-class infrastructure concerns |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Unlocking the Codex harness: how we built the App Server](https://openai.com/index/unlocking-the-codex-harness/) | Deep dive into the Codex app server harness implementation |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/) | Technical breakdown of the Codex agent loop architecture |

### Evolution & Big Picture

Understanding the trajectory from prompt engineering to harness engineering.

- 🔗 [The Third Evolution: Prompt → Context → Harness](https://www.epsilla.com/blogs/harness-engineering-evolution-prompt-context-autonomous-agents) — Epsilla's three-era framework for AI engineering evolution
- 🔗 [2025 Was Agents. 2026 Is Agent Harnesses.](https://aakashgupta.medium.com/2025-was-agents-2026-is-agent-harnesses-heres-why-that-changes-everything-073e9877655e) — Industry overview of the agent-to-harness shift
- 🔗 [The Rise of AI Harness Engineering](https://cobusgreyling.medium.com/the-rise-of-ai-harness-engineering-5f5220de393e) — Overview of the emerging discipline
- 🔗 [The importance of Agent Harness in 2026](https://www.philschmid.de/agent-harness-2026) — CPU-OS analogy; "the harness is the dataset"; trajectory capture as competitive advantage
- 🔗 [Harness Engineering: The Missing Layer Behind AI Agents](https://www.louisbouchard.ai/harness-engineering/) — Clear distinction between prompt/context/harness engineering
- 🔗 [Agent Harnesses: From DIY Patterns to Product](https://paddo.dev/blog/agent-harnesses-from-diy-to-product/) — Evolution from ad-hoc patterns to productized harnesses
- 🔗 [What we miss when we talk about "AI Harnesses"](https://www.futureofbeinghuman.com/p/what-we-miss-when-we-talk-about-ai-harnesses) — Philosophical critique of the harness framing
- 🔗 [Agent Frameworks, Runtimes, and Harnesses, Oh My!](https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/) — LangChain's decomposition of what belongs in a framework, a runtime, and a harness
- 🔗 [Conductors to Orchestrators: The Future of Agentic Coding](https://www.oreilly.com/radar/conductors-to-orchestrators-the-future-of-agentic-coding/) — O'Reilly's take on the future of agent-driven development
- 🔗 [Martin Fowler on Preparing for AI's Nondeterministic Computing](https://thenewstack.io/martin-fowler-on-preparing-for-ais-nondeterministic-computing/) — Engineering for nondeterminism in agent systems
- 🔗 [Why AI Agent Reliability Depends More on the Harness Than the Model](https://hackernoon.com/why-ai-agent-reliability-depends-more-on-the-harness-than-the-model) — HackerNoon on harness-first reliability
- 🔗 [What Is an Agent Harness?](https://www.firecrawl.dev/blog/what-is-an-agent-harness) — Firecrawl's breakdown: infrastructure that makes AI agents actually work
- 🔗 [What is an agent harness in the context of LLMs?](https://parallel.ai/articles/what-is-an-agent-harness) — The model is CPU, context window is RAM, harness is OS, agent is application
- 🔗 [The GAN-Style Agent Loop: Deconstructing Anthropic's Harness](https://www.epsilla.com/blogs/anthropic-harness-engineering-multi-agent-gan-architecture) — Analysis of generator-evaluator harness pattern
- 🔗 [From Prompts to Context to Harness Engineering](https://manjeet.substack.com/p/from-prompts-context-harness-engineering) — Evolution overview
- 🔗 [OpenAI Introduces Harness Engineering](https://www.infoq.com/news/2026/02/openai-harness-engineering-codex/) — InfoQ coverage of the paradigm shift
- 🔗 [Agent Engineering: A New Discipline](https://blog.langchain.com/agent-engineering-a-new-discipline/) — LangChain on the emergence of agent engineering
- 🔗 [Agents At Work: The 2026 Playbook](https://promptengineering.org/agents-at-work-the-2026-playbook-for-building-reliable-agentic-workflows/) — Building reliable agentic workflows
- 🔗 [Anthropic 2026 Agentic Coding Trends Report (PDF)](https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf) — How coding agents are reshaping development

---

## 🧠 Context, Memory & Working State

### Context Engineering

The art of managing what goes into the context window — treating it as a working memory budget, not a dumping ground.

| Source | Article | Description |
|:------:|---------|-------------|
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) | Managing the context window as a working memory budget with practical strategies |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [Context Engineering for Agents](https://blog.langchain.com/context-engineering-for-agents/) | Four strategies: writing, selecting, compressing, isolating context |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [The Rise of Context Engineering](https://blog.langchain.com/the-rise-of-context-engineering/) | Why context engineering matters more than prompt engineering |
| ![Manus](https://img.shields.io/badge/Manus-000000?style=flat) | [Context Engineering for AI Agents: Lessons from Building Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) | KV-cache locality, tool masking, filesystem memory, and keeping useful failures in-context |
| ![Thoughtworks](https://img.shields.io/badge/Thoughtworks-F2617A?style=flat) | [Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) | Shaping the task environment so coding agents stay grounded and productive |
| ![Google](https://img.shields.io/badge/Google-4285F4?style=flat&logo=google&logoColor=white) | [Architecting efficient context-aware multi-agent framework](https://developers.googleblog.com/architecting-efficient-context-aware-multi-agent-framework-for-production/) | ADK's tiered state architecture: Session, Memory, Artifacts |
| ![HumanLayer](https://img.shields.io/badge/HumanLayer-FF6B35?style=flat) | [Advanced Context Engineering for Coding Agents](https://www.humanlayer.dev/blog/advanced-context-engineering) | Patterns for reducing context drift and making coding sessions easier to resume |
| ![HumanLayer](https://img.shields.io/badge/HumanLayer-FF6B35?style=flat) | [Context-Efficient Backpressure for Coding Agents](https://www.humanlayer.dev/blog/context-efficient-backpressure) | Preventing agents from burning context on noisy or low-value work |
| ![LlamaIndex](https://img.shields.io/badge/LlamaIndex-6F42C1?style=flat) | [Context Engineering: What It Is and Techniques to Consider](https://www.llamaindex.ai/blog/context-engineering-what-it-is-and-techniques-to-consider) | LlamaIndex's techniques for context engineering |
| | [Context Engineering (Lance Martin)](https://rlancemartin.github.io/2025/06/23/context_engineering/) | Practical guide from LangChain co-founder |
| | [Context Engineering: Bringing Engineering Discipline to Prompts](https://addyo.substack.com/p/context-engineering-bringing-engineering) — Addy Osmani | Systematic approach to context management |
| ![JetBrains](https://img.shields.io/badge/JetBrains-000000?style=flat&logo=jetbrains&logoColor=white) | [Efficient Context Management for LLM-Powered Agents](https://blog.jetbrains.com/research/2025/12/efficient-context-management/) | NeurIPS 2025 research: simple observation masking ≈ LLM summarization, ~50% cost reduction |
| | [Context Engineering Best Practices](https://www.comet.com/site/blog/context-engineering/) — Comet | Best practices for agentic systems |
| | [Context Engineering Best Practices](https://www.kubiya.ai/blog/context-engineering-best-practices) — Kubiya | Practical reliability-focused best practices |

### Memory & State Management

How agents persist knowledge, recover from interruptions, and maintain state across sessions.

| Project | Description |
|---------|-------------|
| [Letta](https://letta.com/) (formerly MemGPT) | Stateful agents with OS-like memory management (RAM/disk analogy) |
| [Rearchitecting Letta's Agent Loop](https://www.letta.com/blog/letta-v1-agent) | Lessons from ReAct, MemGPT, and Claude Code for agent loop design |
| [Memory Blocks](https://www.letta.com/blog/memory-blocks) — Letta | Discrete functional memory units for context window management |
| [LangGraph + Redis](https://redis.io/blog/langgraph-redis-build-smarter-ai-agents-with-memory-persistence/) | <1ms latency state persistence for agents |
| [LangGraph + DynamoDB](https://aws.amazon.com/blogs/database/build-durable-ai-agents-with-langgraph-and-amazon-dynamodb/) | Durable agent state on AWS infrastructure |
| [Checkpoint/Restore Systems for AI Agents](https://eunomia.dev/blog/2025/05/11/checkpointrestore-systems-evolution-techniques-and-applications-in-ai-agents/) | Survey of checkpoint/restore techniques |
| [Databricks Agent Memory](https://docs.databricks.com/aws/en/generative-ai/agent-framework/stateful-agents) | Built-in memory for Databricks agent framework |
| [Mem0](https://github.com/mem0ai/mem0) | Hybrid storage (Postgres + vector); extracts memories with ADD/UPDATE/DELETE operations; up to 26% accuracy gains |
| [Zep](https://github.com/getzep/zep) | Temporal knowledge graph tracking how facts change over time; combines graph memory with vector search |
| [Cognee](https://github.com/topoteretes/cognee) | Knowledge graph layer that structures, connects, and retrieves information as interconnected knowledge |

### Structured Output (Agent I/O Harness)

Libraries that ensure reliable, schema-compliant agent output.

| Project | Description |
|---------|-------------|
| [Instructor](https://github.com/instructor-ai/instructor) | Type-safe structured extraction from LLMs using Pydantic; SDKs for Python, TypeScript, Go, Ruby |
| [Outlines](https://github.com/dottxt-ai/outlines) | FSM-based token masking ensures 100% schema-compliant output at generation time |

---

## 🛡️ Constraints, Guardrails & Safe Autonomy

### Safety & Control Patterns

Reducing approval friction without losing control — sandboxing, policy design, and quality loops.

| Source | Article | Description |
|:------:|---------|-------------|
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Beyond permission prompts: making Claude Code more secure](https://www.anthropic.com/engineering/claude-code-sandboxing) | Better sandboxing and policy design for secure autonomous agents |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Code execution with MCP: building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp) | Controlled execution power through explicit, inspectable tool boundaries; 150K → 2K token reduction |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents) | Tool interfaces that are easier for models to call correctly and safely |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Advanced tool use on the Claude Developer Platform](https://www.anthropic.com/engineering/advanced-tool-use) | Tool Search, Programmatic Tool Calling, and Tool Use Examples |
| ![Thoughtworks](https://img.shields.io/badge/Thoughtworks-F2617A?style=flat) | [Assessing internal quality while coding with an agent](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html) | Moving quality checks into the loop instead of relying on after-the-fact review |
| ![Thoughtworks](https://img.shields.io/badge/Thoughtworks-F2617A?style=flat) | [Anchoring AI to a reference application](https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html) | Constraining agents with concrete exemplars for more consistent output |
| ![Thoughtworks](https://img.shields.io/badge/Thoughtworks-F2617A?style=flat) | [Humans and Agents in Software Engineering Loops](https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html) | Where humans should strengthen the harness instead of micromanaging artifacts |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Claude Code: Best practices for agentic coding](https://www.anthropic.com/engineering/claude-code-best-practices) | Repo structure, checkpoints, validation, and delegation in agentic workflows |
| | [Agentic Engineering Patterns](https://simonwillison.net/2026/Feb/23/agentic-engineering-patterns/) — Simon Willison | Coding practices and patterns for working with agents |
| | [The lethal trifecta for AI agents](https://simonw.substack.com/p/the-lethal-trifecta-for-ai-agents) — Simon Willison | Private data + untrusted content + external communication = security risk |
| | [Governing Claude Code with Kong AI Gateway](https://konghq.com/blog/engineering/claude-code-governance-with-an-ai-gateway) | Secure agent harness rollouts via API gateway |
| | [AI Agent Safety](https://cleanlab.ai/blog/ai-agent-safety/) — Cleanlab | Managing unpredictability at scale in production agents |
| | [Lessons from 2025: Agent Mitigation](https://devops.com/lessons-from-2025-the-year-agent-mitigation-became-a-thing/) | How "agent mitigation" became a new discipline |

### Guardrail Frameworks

| Project | Description |
|---------|-------------|
| [Invariant Guardrails](https://invariantlabs.ai/guardrails) (now Snyk) | Rule-based guardrailing for MCP and agentic AI |
| [Invariant MCP-scan](https://github.com/invariantlabs-ai/invariant) | Security scanner for MCP servers: prompt injection, tool poisoning detection |
| [NeMo Guardrails](https://developer.nvidia.com/nemo-guardrails) — NVIDIA | Open-source programmable guardrails; sub-100ms latency; GPU-accelerated |
| [Guardrails AI](https://guardrailsai.com/) | Open-source framework for LLM output validation |

---

## 📋 Specs, Agent Files & Workflow Design

### Agent Instruction Standards

How to tell agents what to do — repo-local instruction files and machine-readable specifications.

| Project | Description |
|---------|-------------|
| [AGENTS.md](https://github.com/agentsmd/agents.md) | Open format for repo-local instructions; [intro by OpenAI](https://openai.com/index/introducing-agents-md/) |
| [agent.md](https://github.com/agentmd/agent.md) | Related standardization effort for machine-readable agent instructions |
| [GitHub Spec Kit](https://github.com/github/spec-kit) | Toolkit for spec-driven development — agents execute against explicit specs |
| [Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) | Practical guide to creating durable, repo-local instructions; 150–200 instruction limit |
| [Equipping agents with Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) — Anthropic | SKILL.md-based progressive disclosure system for domain-specific agent capabilities |
| [How to write a great agents.md](https://github.blog/ai-and-ml/github-copilot/how-to-write-a-great-agents-md-lessons-from-over-2500-repositories/) — GitHub | Lessons from 2,500+ repositories |
| [awesome-agents-md](https://github.com/Ischca/awesome-agents-md) | Curated list of real-world AGENTS.md files, templates, guides & tools |
| [awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | 1,000+ agent skills from official dev teams and community |
| [CLAUDE.md vs AGENTS.md vs .cursorrules](https://thepromptshelf.dev/blog/cursorrules-vs-claude-md/) | Comparison of agent configuration file formats |

### Workflow & Orchestration Design

| Source | Article | Description |
|:------:|---------|-------------|
| ![HumanLayer](https://img.shields.io/badge/HumanLayer-FF6B35?style=flat) | [12 Factor Agents](https://www.humanlayer.dev/blog/12-factor-agents) | Operating principles for production agents: explicit prompts, state ownership, clean pause-resume |
| | [12-Factor AgentOps](https://www.12factoragentops.com/) | Operations-oriented companion focused on context discipline and reproducibility |
| ![Thoughtworks](https://img.shields.io/badge/Thoughtworks-F2617A?style=flat) | [Understanding Spec-Driven-Development](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) | Why strong specs make AI-assisted delivery more dependable |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) | Orchestrator-worker pattern with parallel subagents; 90%+ improvement over single-agent |
| ![Google](https://img.shields.io/badge/Google-4285F4?style=flat&logo=google&logoColor=white) | [Developer's guide to multi-agent patterns in ADK](https://developers.googleblog.com/developers-guide-to-multi-agent-patterns-in-adk/) | Multi-agent orchestration patterns in Google ADK |
| ![LlamaIndex](https://img.shields.io/badge/LlamaIndex-6F42C1?style=flat) | [Introducing AgentWorkflow](https://www.llamaindex.ai/blog/introducing-agentworkflow-a-powerful-system-for-building-ai-agent-systems) | Multi-agent orchestration system |
| ![LlamaIndex](https://img.shields.io/badge/LlamaIndex-6F42C1?style=flat) | [Workflows 1.0](https://www.llamaindex.ai/blog/announcing-workflows-1-0-a-lightweight-framework-for-agentic-systems) | Event-driven framework for agentic workflows |
| | [Emerging Patterns in Building GenAI Products](https://martinfowler.com/articles/gen-ai-patterns/) — Martin Fowler | Architecture patterns for generative AI products |
| | [Agent-Native Engineering](https://www.generalintelligencecompany.com/writing/agent-native-engineering) | Engineering practices for agent-first development |

---

## 📊 Evals & Observability

### Evaluation Guides & Frameworks

How to measure whether your agent actually works — evaluation methodology for non-deterministic systems.

| Source | Article | Description |
|:------:|---------|-------------|
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills/) | Turning agent traces into repeatable evals with JSONL logs and deterministic checks |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Agent evals](https://platform.openai.com/docs/guides/agent-evals) | Measuring agent quality with reproducible task-level and workflow-level evaluations |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Evaluation best practices](https://platform.openai.com/docs/guides/evaluation-best-practices) | Building eval suites that match real-world distributions and catch regressions |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Trace grading](https://platform.openai.com/docs/guides/trace-grading) | Grading agent traces directly, especially for long multi-step tasks |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Demystifying Evals for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) | What to measure when agents have many possible trajectories |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Quantifying infrastructure noise in agentic coding evals](https://www.anthropic.com/engineering/infrastructure-noise) | Runtime configuration can move benchmark scores more than many leaderboard gaps |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [Evaluating Deep Agents: Our Learnings](https://blog.langchain.com/evaluating-deep-agents-our-learnings/) | Single-step, full-run, and multi-turn eval design for stateful agents |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [Improving Deep Agents with harness engineering](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) | Top 30 → Top 5 on Terminal-Bench 2.0 by only changing the harness |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [How we build evals for Deep Agents](https://blog.langchain.com/how-we-build-evals-for-deep-agents/) | Eval methodology for LangChain's deep agents |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [How Middleware Lets You Customize Your Agent Harness](https://blog.langchain.com/how-middleware-lets-you-customize-your-agent-harness/) | Middleware patterns for loop detection and custom harness behavior |
| | [8 benchmarks shaping the next generation of AI agents](https://ainativedev.io/news/8-benchmarks-shaping-the-next-generation-of-ai-agents) | Overview of key agent benchmarks |

### Observability Platforms

| Platform | Type | Description |
|----------|:----:|-------------|
| [Arize Phoenix](https://github.com/Arize-ai/phoenix) | OSS | OpenTelemetry-based tracing, evals, and experiments for AI |
| [agenttrace](https://github.com/luoyuctl/agenttrace) | OSS | TUI observability and audit trail for local AI coding-agent sessions across Claude Code, Codex CLI, Gemini CLI, Aider, Cursor, Qwen Code, Cline, OpenCode/OpenClaw, Kimi CLI, and JSON/JSONL traces |
| [Langfuse](https://langfuse.com/) | OSS | LLM observability: tracing, prompt management, evals (MIT license) |
| [LangSmith](https://www.langchain.com) | Commercial | Agent engineering platform: tracing, evaluation, deployment |
| [Braintrust](https://www.braintrust.dev/) | Commercial | AI observability + evaluation; used by Notion, Stripe, Zapier |
| [Helicone](https://www.helicone.ai/) | Commercial | AI Gateway with routing, caching, rate limiting, cost analytics |
| [AI observability tools buyer's guide 2026](https://www.braintrust.dev/articles/best-ai-observability-tools-2026) | Guide | Comprehensive comparison of observability platforms |
| [Portkey](https://portkey.ai/) | Commercial | AI gateway + observability; routing, fallbacks, load balancing, caching, and prompt versioning |
| [LiteLLM](https://github.com/BerriAI/litellm) | OSS | Unified proxy for 100+ LLMs in OpenAI format; cost tracking, guardrails, load balancing |
| [OpenTelemetry for LLMs](https://opentelemetry.io/blog/2025/ai-agent-observability/) | Standard | Emerging standard; OpenLLMetry and OpenLIT emit OTLP-compatible spans |
| [Comparing open-source AI agent frameworks](https://langfuse.com/blog/2025-03-19-ai-agent-comparison) | Guide | Framework comparison with observability perspective |

---

## 🏆 Benchmarks

Benchmarks that stress **harness quality**, not just model quality — context handling, tool calling, environment control, verification logic, and runtime scaffolding.

| Benchmark | Focus | Description |
|-----------|:-----:|-------------|
| [SWE-bench Verified](https://www.swebench.com/) | 🔧 Code | Real GitHub issues and tests; harness choices around retrieval, patching, and validation are highly visible |
| [SWE-PolyBench](https://amazon-science.github.io/SWE-PolyBench/) — Amazon | 🔧 Code | Multi-language: 2,110 instances across 21 repos in Java/JS/TS/Python |
| [SWE-Bench Pro](https://openreview.net/) | 🔧 Code | 1,865 problems from 41 repos and 123 programming languages |
| [FeatureBench](https://arxiv.org/abs/2602.10975) | 🔧 Code | 200 eval instances; SOTA agents achieve only 11% (vs 74% on SWE-bench) |
| [Terminal-Bench](https://www.tbench.ai/) | 💻 Terminal | Terminal-native agents in shells, filesystems, and verification-heavy environments |
| [Terminal-Bench 2.0 & Harbor](https://www.tbench.ai/news/announcement-2-0) | 💻 Terminal | Harder tasks and generalized evaluation harness |
| [OSWorld](https://os-world.github.io/) | 🖥️ Desktop | 369 tasks across Ubuntu, Windows, macOS with execution-based evaluators |
| [AppWorld](https://appworld.dev/) | 🌐 Interactive | Controllable world of apps for testing planning, code generation, and collateral-damage control |
| [AgentBench](https://github.com/THUDM/AgentBench) | 🌐 Multi-env | Cross-environment: OS, databases, knowledge graphs, web browsing |
| [tau2-bench](https://github.com/sierra-research/tau2-bench) | 🔄 Multi-step | Realistic multi-step tasks where success depends on tool use and execution quality |
| [WebArena-Verified](https://github.com/ServiceNow/webarena-verified) | 🌐 Web | Curated web-agent tasks with deterministic evaluators over responses and network traces |
| [WorkArena](https://github.com/ServiceNow/WorkArena) | 🌐 Enterprise | Common knowledge-work tasks on realistic enterprise-style web workflows |
| [GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) | 🤖 General | General AI assistant benchmark for tools, planning, verification, and long-horizon autonomy |
| [HAL: Holistic Agent Leaderboard](https://hal.cs.princeton.edu/) | 📊 Leaderboard | Reliability, cost, and broad task coverage for comparing end-to-end harness behavior |
| [DPAI Arena](https://blog.jetbrains.com/blog/2025/10/28/introducing-developer-productivity-ai-arena-an-open-platform-for-ai-coding-agents-benchmarks/) — JetBrains | 🔧 Code | Open platform for coding agent benchmarks across full dev lifecycle |
| [LOCA-bench](https://arxiv.org/abs/2602.07962) | 🧠 Context | Benchmarks long-context agents; reveals "context rot" phenomenon |
| [SWE-bench Live](https://swe-bench-live.github.io/) | 🔧 Code | Live benchmark with real-time GitHub issues |

### Evaluation Frameworks & Tools

| Tool | Description |
|------|-------------|
| [Inspect AI](https://github.com/UKGovernmentBEIS/inspect_ai) | UK AI Safety Institute's eval framework; batteries-included with pre-built benchmarks |
| [ai-agent-benchmark-compendium](https://github.com/philschmid/ai-agent-benchmark-compendium) | Compendium of 50+ agent benchmarks, categorized by function calling, reasoning, coding |
| [Galileo Agent Eval](https://galileo.ai/blog/agent-evaluation-framework-metrics-rubrics-benchmarks) | Framework with metrics, rubrics, and benchmarks for production agent evaluation |

---

## ⚙️ Runtimes, Harnesses & Reference Implementations

### Agent SDKs & Frameworks

| Framework | Maintainer | Description |
|-----------|:----------:|-------------|
| [Claude Agent SDK](https://platform.claude.com/docs/en/agent-sdk/overview) | Anthropic | Production-oriented SDK with sessions, tools, orchestration, and compact feature |
| [OpenAI Agents SDK](https://openai.com/index/introducing-agentkit/) | OpenAI | Visual canvas + Agent Builder + ChatKit + Connector Registry |
| [Google ADK](https://google.github.io/adk-docs/) | Google | Open-source framework for building multi-agent applications |
| [Microsoft Agent Framework](https://learn.microsoft.com/en-us/agent-framework/overview/) | Microsoft | Convergence of AutoGen + Semantic Kernel; [checkpointing & resuming](https://learn.microsoft.com/en-us/agent-framework/tutorials/workflows/checkpointing-and-resuming) |
| [AutoGen](https://github.com/microsoft/autogen) | Microsoft | Open-source multi-agent programming framework |
| [LangGraph](https://github.com/langchain-ai/langgraph) | LangChain | Graph-based agent orchestration with built-in persistence |
| [deepagents](https://github.com/langchain-ai/deepagents) | LangChain | Deeper, longer-running agents with middleware and harness patterns |
| [CrewAI](https://crewai.com/) | CrewAI | Role-driven multi-agent orchestration; fastest-growing for multi-agent |
| [MetaGPT](https://github.com/geekan/MetaGPT) | Open Source | Simulates software company with PM/Architect/Engineer/QA agents |
| [Pydantic AI](https://ai.pydantic.dev/) | Pydantic | Type-safe Python agent framework |
| [Agno](https://agno.dev/) | Agno | High-performance multi-agent runtime |
| [Smolagents](https://huggingface.co/docs/smolagents) | Hugging Face | Ultra-minimal agent framework |
| [Mastra](https://mastra.ai/) | Gatsby team | JavaScript agent framework |
| [AWS Strands Agents](https://aws.amazon.com/strands-agents/) | AWS | Model-driven ReAct pattern; deep Lambda integration |
| [AgentKit](https://github.com/inngest/agent-kit) | Inngest | TypeScript toolkit for durable, workflow-aware agents |
| [Vercel AI SDK](https://ai-sdk.dev/) | Vercel | Unified toolkit for 30+ LLM providers; frontend-to-backend agent infrastructure |
| [VoltAgent](https://github.com/VoltAgent/ai-agent-platform) | VoltAgent | TypeScript agent platform with orchestration, memory, RAG, and enterprise observability |

### Sandbox & Execution Environments

| Platform | Description |
|----------|-------------|
| [E2B](https://e2b.dev/) | Open-source Firecracker microVM sandboxing; ~150ms cold starts |
| [Modal](https://modal.com/) | Container-based agent execution; scales to 50K+ concurrent instances |
| [Daytona](https://daytona.io/) | Docker-based sandbox; sub-90ms creation; pivoted to agent infra in 2025 |
| [SWE-ReX](https://github.com/SWE-agent/SWE-ReX) | Sandboxed code execution infrastructure for AI agents |
| [awesome-sandbox](https://github.com/restyler/awesome-sandbox) | Curated list of code sandboxing solutions for AI agents |
| [Browserbase](https://www.browserbase.com/) | Cloud-hosted browser instances for AI agents at scale |
| [Stagehand](https://github.com/browserbase/stagehand) | Browserbase's open-source SDK bridging Playwright and AI agents |
| [Firecrawl](https://www.firecrawl.dev/) | Managed isolated browser environment + web scraping API for agents |
| [Top AI Code Sandbox Products](https://modal.com/blog/top-code-agent-sandbox-products) — Modal | 2025 comparison of sandbox solutions |

### Reference Implementations

| Project | Description |
|---------|-------------|
| [SWE-agent](https://github.com/SWE-agent/SWE-agent) | Mature research coding agent with inspectable harness, prompt, tools, and environment |
| [Harbor](https://github.com/harbor-framework/harbor) | Generalized harness for evaluating and improving agents at scale |
| [Terminal-Bench](https://github.com/harbor-framework/terminal-bench) | Open-source terminal benchmark implementation |

---

## 🔌 MCP (Model Context Protocol)

The emerging standard for giving agents structured, controlled access to tools and data sources.

| Resource | Description |
|----------|-------------|
| [MCP Specification (2025-11-25)](https://modelcontextprotocol.io/specification/2025-11-25) | Latest protocol specification |
| [2026 MCP Roadmap](http://blog.modelcontextprotocol.io/posts/2026-mcp-roadmap/) | Priorities: remote deployment, auth, enterprise features |
| [MCP Roadmap Growing Pains](https://thenewstack.io/model-context-protocol-roadmap-2026/) — The New Stack | Production challenges and planned solutions |
| [MCP Servers](https://github.com/modelcontextprotocol/servers) | Official reference server implementations |
| [MCP Auth Spec Updates](https://auth0.com/blog/mcp-specs-update-all-about-auth/) — Auth0 | Authentication additions to MCP |
| [MCP + Codex](https://developers.openai.com/codex/mcp) — OpenAI | How Codex integrates with MCP |
| [MCP.so](https://mcp.so/) | Marketplace/directory for MCP servers; 1,000+ live connectors |
| [Context7 MCP](https://context7.com/) | Provides LLMs with up-to-date, version-specific documentation and code examples |
| [awesome-mcp-servers](https://github.com/wong2/awesome-mcp-servers) | Most popular community-curated list of MCP servers |

---

## 💻 Coding Agents in Practice

### Tools & Products

| Tool | Type | Description |
|------|:----:|-------------|
| [Claude Code](https://www.anthropic.com/claude-code) | CLI | Anthropic's agentic coding CLI with hooks, sub-agents, and MCP |
| [Codex](https://openai.com/index/codex/) | CLI | OpenAI's cloud-based coding agent |
| [Cursor](https://cursor.com/) | IDE | AI-first code editor with Background Agents |
| [Windsurf](https://windsurf.com/) | IDE | Cascade engine for agentic coding workflows |
| [Aider](https://aider.chat/) | CLI | Open-source AI pair programming in the terminal |
| [Continue](https://continue.dev/) | Extension | Open-source AI code assistant for VS Code and JetBrains |
| [OpenHands](https://github.com/All-Hands-AI/OpenHands) | Platform | Open platform for AI software developers |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | CLI | Google's open-source AI agent for the terminal |
| [Devin](https://devin.ai/) | Platform | Cognition's autonomous coding agent |
| [Replit Agent](https://replit.com/) | Platform | In-browser agent with snapshot engine and self-healing tests |
| [Goose](https://github.com/block/goose) | CLI | Block's fully open-source (Apache-2.0) MCP-native agent; model-agnostic |
| [Cline](https://github.com/cline/cline) | Extension | BYOM (bring your own model) agent for VS Code |
| [Devon](https://github.com/entropy-research/Devon) | CLI | Open-source pair programmer with autonomous planning and debugging |
| [OpenCode](https://opencode.ai/) | CLI | 75+ provider support, LSP integration, privacy-first |
| [v0](https://v0.dev/) | Platform | Vercel's AI-powered frontend development agent |

### Field Reports from Coding Agent Companies

Real-world insights from teams building and deploying coding agents at scale.

| Source | Article | Key Insight |
|:------:|---------|-------------|
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [A practical guide to building agents](https://openai.com/business/guides-and-resources/a-practical-guide-to-building-ai-agents/) | Comprehensive guide covering use case selection, design patterns, guardrails |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [Building an AI-native engineering team](https://developers.openai.com/codex/guides/build-ai-native-engineering-team/) | Guide for teams adopting agent-first development |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | [OpenAI Cookbook — Agents](https://cookbook.openai.com/topic/agents) | Collection of agent-related code examples and tutorials |
| ![Cognition](https://img.shields.io/badge/Cognition-000000?style=flat) | [Coding Agents 101](https://devin.ai/agents101) | Practical guide to working with coding agents effectively |
| ![Cognition](https://img.shields.io/badge/Cognition-000000?style=flat) | [Devin's 2025 Performance Review](https://cognition.ai/blog/devin-annual-performance-review-2025) | Learnings from 18 months of agents at work; task scoping insights |
| ![Cognition](https://img.shields.io/badge/Cognition-000000?style=flat) | [Rebuilding Devin for Claude Sonnet 4.5](https://cognition.ai/blog/devin-sonnet-4-5-lessons-and-challenges) | Context management insights from model migration |
| ![Cognition](https://img.shields.io/badge/Cognition-000000?style=flat) | [How Cognition Uses Devin to Build Devin](https://cognition.ai/blog/how-cognition-uses-devin-to-build-devin) | Self-referential agent development case study |
| ![Replit](https://img.shields.io/badge/Replit-F26207?style=flat&logo=replit&logoColor=white) | [Decision-Time Guidance](https://blog.replit.com/decision-time-guidance) | Injecting situational instructions at key moments vs. front-loading |
| ![Replit](https://img.shields.io/badge/Replit-F26207?style=flat&logo=replit&logoColor=white) | [Inside Replit's Snapshot Engine](https://blog.replit.com/inside-replits-snapshot-engine) | Reversible compute and storage fabric for agent safety |
| ![Replit](https://img.shields.io/badge/Replit-F26207?style=flat&logo=replit&logoColor=white) | [Introducing Agent 3](https://blog.replit.com/introducing-agent-3-our-most-autonomous-agent-yet) | Self-healing testing, 200-minute autonomous runtime |
| ![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat&logo=vercel&logoColor=white) | [Introducing the new v0](https://vercel.com/blog/introducing-the-new-v0) | Sandbox-based runtime, Git workflow integration |
| ![Meta](https://img.shields.io/badge/Meta-0467DF?style=flat&logo=meta&logoColor=white) | [Ranking Engineer Agent (REA)](https://engineering.fb.com/2026/03/17/developer-tools/ranking-engineer-agent-rea-autonomous-ai-system-accelerating-meta-ads-ranking-innovation/) | Autonomous AI agent accelerating Meta's ads ranking engineering |
| ![Google](https://img.shields.io/badge/Google-4285F4?style=flat&logo=google&logoColor=white) | [Closing the knowledge gap with agent skills](https://developers.googleblog.com/en/closing-the-knowledge-gap-with-agent-skills/) | How agent skills help bridge domain knowledge gaps |
| | [My LLM Coding Workflow Going into 2026](https://medium.com/@addyosmani/my-llm-coding-workflow-going-into-2026-52fe1681325e) — Addy Osmani | Practical coding workflow with agents |
| | [The Cognition: Devin is in the Details](https://www.swyx.io/cognition) — swyx | Deep dive into Devin's architecture |
| ![Replit](https://img.shields.io/badge/Replit-F26207?style=flat&logo=replit&logoColor=white) | [Introducing Agent 4](https://blog.replit.com/introducing-agent-4-built-for-creativity) | Parallel task execution, multi-platform development |
| ![Anthropic](https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white) | [Building agents with the Claude Agent SDK](https://www.anthropic.com/engineering/building-agents-with-the-claude-agent-sdk) | Production-oriented SDK; compact feature for context management |

---

## 🏭 Production Deployment

Lessons from running agents in production — what breaks, what works, and what scales.

| Source | Article | Key Finding |
|:------:|---------|-------------|
| | [AI Agents in Production 2025](https://cleanlab.ai/ai-agents-in-production-2025/) — Cleanlab | Survey of 1,837 respondents; only 95 with agents live in production |
| | [Key Findings from 1,200 Production Deployments](https://www.zenml.io/blog/the-experimentation-phase-is-over-key-findings-from-1-200-production-deployments) — ZenML | 95% of agent deployments fail; system fragility, not model intelligence |
| | [The State of Agentic AI in 2025: A Year-End Reality Check](https://www.arionresearch.com/blog/the-state-of-agentic-ai-in-2025-a-year-end-reality-check) | Industry reality check on agent deployment |
| | [Building Production-Grade AI Agents](https://pub.towardsai.net/building-production-grade-ai-agents-in-2025-the-complete-technical-guide-9f02eff84ea2) — Towards AI | Complete technical guide for production agents |
| | [Building Reliable Autonomous Agentic AI](https://www.techempower.com/blog/2026/01/12/bulding-reliable-autonomous-agentic-ai/) — TechEmpower | Practical reliability patterns |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) | [State of Agent Engineering](https://www.langchain.com/state-of-agent-engineering) | Survey of 1,300+ professionals on agent engineering challenges |
| ![Google](https://img.shields.io/badge/Google-4285F4?style=flat&logo=google&logoColor=white) | [Lessons from 2025 on agents and trust](https://cloud.google.com/transform/ai-grew-up-and-got-a-job-lessons-from-2025-on-agents-and-trust) | Google Cloud CTO lessons on agent deployment and trust |
| | [Harness Engineering 101: Claude Code / Codex Workflows](https://muraco.ai/en/articles/harness-engineering-claude-code-codex/) | Practical reproducible, safe, long-running workflows |

---

## 📚 Academic Research

Papers advancing the theoretical and empirical foundations of harness engineering.

### Harness & Context Engineering

| Paper | Venue/Date | Key Contribution |
|-------|:----------:|------------------|
| [Building Effective AI Coding Agents for the Terminal](https://arxiv.org/abs/2603.05344) | arXiv, Mar 2026 | OpenDev agent; scaffolding vs. harness architecture distinction |
| [Natural-Language Agent Harnesses](https://arxiv.org/abs/2603.25723) | arXiv, Mar 2026 | Harness-level control via natural language: roles, contracts, verification gates |
| [Agentic Context Engineering (ACE)](https://arxiv.org/abs/2510.04618) | arXiv, Oct 2025 | Contexts as evolving playbooks; 14.8% improvement over ReAct |
| [Meta Context Engineering via Agentic Skill Evolution](https://arxiv.org/abs/2601.21557) | arXiv, Jan 2026 | Bi-level framework where meta-level agent refines engineering skills |
| [Context Engineering for AI Agents in Open-Source Software](https://arxiv.org/abs/2510.21413) | arXiv, Oct 2025 | Study of context engineering file adoption in 466 open-source projects |
| [PAACE: Plan-Aware Automated Agent Context Engineering](https://arxiv.org/abs/2512.16970) | arXiv, Dec 2025 | Context engineering as a learnable, plan-aware optimization problem |
| [The Complexity Trap](https://github.com/JetBrains-Research/the-complexity-trap) | NeurIPS 2025 | Simple observation masking ≈ LLM summarization; ~50% cost reduction |

### Agent Reliability & Safety

| Paper | Venue/Date | Key Contribution |
|-------|:----------:|------------------|
| [Memory Management for Long-Running Low-Code Agents](https://arxiv.org/abs/2509.25250) | arXiv, Sep 2025 | Memory management for persistent agent sessions |
| [Efficient On-Device Agents via Adaptive Context Management](https://arxiv.org/abs/2511.03728) | arXiv, Nov 2025 | Context management for resource-constrained environments |
| [Agentic AI: Challenges and Opportunities](https://arxiv.org/abs/2601.02749) | arXiv, Jan 2026 | Comprehensive survey of verifiable planning, coordination, memory, governance |
| [From Competition to Coordination: Safe Multi-Agent LLM Systems](https://arxiv.org/abs/2511.17621) | arXiv, Nov 2025 | Market-making framework for safe multi-agent coordination |
| [Emergent Coordination in Multi-Agent Language Models](https://arxiv.org/abs/2510.05174) | arXiv, Oct 2025 | How prompt design steers multi-agent LLMs |
| [Towards a Science of AI Agent Reliability](https://arxiv.org/abs/2602.16666) | arXiv, Feb 2026 | Evaluates 14 models across 3 providers with scaffolding strategies |
| [Confucius Code Agent](https://arxiv.org/abs/2512.10398) | arXiv, Dec 2025 | Scalable agent scaffolding with persistent note-taking for cross-session learning |
| [Agentic AI Frameworks: Architectures, Protocols, Design](https://arxiv.org/abs/2508.10146) | arXiv, Aug 2025 | Comprehensive survey of agentic AI architectures and protocols |
| [A Practical Guide for Production-Grade Agentic AI Workflows](https://arxiv.org/abs/2512.08769) | arXiv, Dec 2025 | Nine best practices: tool-first design, single-responsibility agents, KISS principle |

### Evaluation & Benchmarking

| Paper | Venue/Date | Key Contribution |
|-------|:----------:|------------------|
| [Towards a Science of Scaling Agent Systems](https://arxiv.org/abs/2512.08296) | DeepMind, Dec 2025 | Scaling multi-agent systems scientifically |
| [Measuring Agents in Production](https://arxiv.org/abs/2512.04123) | arXiv, Dec 2025 | Framework for measuring agent performance in production |
| [Evaluation and Benchmarking of LLM Agents: A Survey](https://arxiv.org/abs/2507.21504) | arXiv, 2025 | Comprehensive survey of agent evaluation methods |
| [Harnessing Multi-Agent LLMs for Complex Engineering](https://arxiv.org/abs/2501.01205) | arXiv, Jan 2025 | Multi-agent framework for engineering design projects |
| [Multi-Agent Coordination: A Survey](https://arxiv.org/abs/2502.14743) | arXiv, Feb 2025 | Survey of coordination mechanisms across domains |

---

## 🎓 Learning Resources & Curated Lists

### Harness & Context Engineering

| Resource | Description |
|----------|-------------|
| [awesome-agent-harness](https://github.com/AutoJunjie/awesome-agent-harness) | Curated list of agent harness resources |
| [walkinglabs/awesome-harness-engineering](https://github.com/walkinglabs/awesome-harness-engineering) | The original awesome list for harness engineering |
| [Context-Engineering handbook](https://github.com/davidkimai/Context-Engineering) | First-principles handbook inspired by Karpathy |
| [Awesome-Context-Engineering](https://github.com/Meirtz/Awesome-Context-Engineering) | Comprehensive survey: hundreds of papers, frameworks, guides |
| [yzfly/awesome-context-engineering](https://github.com/yzfly/awesome-context-engineering) | Curated papers, tools, and best practices for context engineering |
| [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) | Reverse-engineers Claude Code's harness mechanisms session by session |
| [harness-engineering (deusyu)](https://github.com/deusyu/harness-engineering) | Learning guide from concept to practice |
| [Harness Engineering Academy](https://harnessengineering.academy/) | Tutorials, career guides, and learning paths |
| [agent-engineering.dev](https://www.agent-engineering.dev/) | Articles on harness engineering as a production discipline |
| [harness-engineering.ai](https://harness-engineering.ai/) | Complete guide to agent harness concepts |
| [Prompt Engineering Guide: Context Engineering](https://www.promptingguide.ai/guides/context-engineering-guide) | Community reference guide |
| [ACE-FCA (HumanLayer)](https://github.com/humanlayer/advanced-context-engineering-for-coding-agents) | "Frequent intentional compaction" approach; tested on 300K LOC Rust codebase |

### Agent Frameworks & General AI

| Resource | Description |
|----------|-------------|
| [awesome-ai-agents-2026](https://github.com/caramaschiHG/awesome-ai-agents-2026) | 300+ resources across 20+ categories, updated monthly |
| [awesome-agents (kyrolabs)](https://github.com/kyrolabs/awesome-agents) | Open-source tools and products to build AI agents |
| [awesome-ai-agent-frameworks](https://github.com/axioma-ai-labs/awesome-ai-agent-frameworks) | Most up-to-date list of AI Agent Frameworks |
| [awesome-cli-coding-agents](https://github.com/bradAGI/awesome-cli-coding-agents) | Terminal-native agents and harnesses |
| [awesome-vibe-coding](https://github.com/filipecalegario/awesome-vibe-coding) | Curated list of vibe coding references |
| [awesome-claude-code](https://github.com/jqueryscript/awesome-claude-code) | Tools, IDE integrations, frameworks for Claude Code |
| [awesome-copilot](https://github.com/github/awesome-copilot) | GitHub's official awesome-copilot with AGENTS.md |
| [Awesome-LLMOps](https://github.com/tensorchord/Awesome-LLMOps) | LLMOps tools for developers |

### Agent Security

| Resource | Description |
|----------|-------------|
| [awesome-ai-agents-security](https://github.com/ProjectRecon/awesome-ai-agents-security) | Living map of AI agent security ecosystem by security lifecycle |
| [awesome-ai-guardrails](https://github.com/enguard-ai/awesome-ai-guardrails) | Curated materials on AI guardrails |

### Research Paper Collections

| Resource | Description |
|----------|-------------|
| [awesome-ai-agent-papers](https://github.com/VoltAgent/awesome-ai-agent-papers) | Curated 2026 AI agent research papers, updated weekly from arXiv |
| [Awesome-Agent-Papers](https://github.com/luo-junyu/Awesome-Agent-Papers) | Up-to-date LLM Agent survey: methodology, applications, challenges |
| [Awesome-Self-Evolving-Agents](https://github.com/EvoAgentX/Awesome-Self-Evolving-Agents) | Comprehensive survey of self-evolving AI agents (2023–2025) |
| [Autonomous-Agents](https://github.com/tmgthb/Autonomous-Agents) | Autonomous Agents research papers, updated daily |
| [KDD 2025 Tutorial: Evaluation of LLM Agents](https://sap-samples.github.io/llm-agents-eval-tutorial/) | Two-dimensional taxonomy of evaluation objectives and processes |

---

## Contributing

Contributions are welcome! Please prefer resources that are:

- **Primary sources** — original implementations, first-party articles, or seminal papers
- **Specific** — about how agents are constrained, evaluated, resumed, observed, or orchestrated
- **Practical** — useful to practitioners building real harnesses, not generic AI commentary
- **Current** — actively maintained or recently published (2024+)

If two links say the same thing, prefer the more primary, practical, and implementation-oriented one.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for contribution guidelines and the preferred entry format.

## License

[CC0 1.0](./LICENSE)
