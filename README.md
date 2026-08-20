# Awesome Harness Engineering [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of articles, playbooks, benchmarks, specifications, and open-source projects for harness engineering: the practice of shaping the environment around AI agents so they can work reliably.

Harness engineering sits at the intersection of context engineering, evaluation, observability, orchestration, safe autonomy, and software architecture. This list focuses on resources that make agents more dependable in real workflows, especially long-running coding and research tasks.

Generic agent tooling is out of scope unless the page directly covers harness design, context management, evaluation, runtime control, or other reliability-critical harness primitives.

## Contents

- [Courses & Learning Resources](#courses--learning-resources)
- [Foundations](#foundations)
- [Context, Memory & Working State](#context-memory--working-state)
  - [Context Design & Delivery](#context-design--delivery)
  - [Memory & Knowledge Systems](#memory--knowledge-systems)
- [Constraints, Guardrails & Safe Autonomy](#constraints-guardrails--safe-autonomy)
  - [Tool Design & Execution Boundaries](#tool-design--execution-boundaries)
  - [Security, Authorization & Policy](#security-authorization--policy)
  - [Operational Autonomy & Reliability](#operational-autonomy--reliability)
- [Specs, Agent Files & Workflow Design](#specs-agent-files--workflow-design)
  - [Instruction Files & Formats](#instruction-files--formats)
  - [Spec-Driven Development](#spec-driven-development)
  - [Operating Principles & Human Oversight](#operating-principles--human-oversight)
- [Evals & Observability](#evals--observability)
  - [Evaluation Design](#evaluation-design)
  - [Verification & Quality Gates](#verification--quality-gates)
  - [Telemetry, Tracing & Performance](#telemetry-tracing--performance)
- [Benchmarks](#benchmarks)
  - [Coding & Terminal Agents](#coding--terminal-agents)
  - [Web, GUI & Computer Use](#web-gui--computer-use)
  - [Tools, APIs & MCP](#tools-apis--mcp)
  - [Multi-Agent, General & Interactive](#multi-agent-general--interactive)
  - [Safety, Robustness & Economic Agency](#safety-robustness--economic-agency)
- [Runtimes, Harnesses & Reference Implementations](#runtimes-harnesses--reference-implementations)
  - [Runtime Foundations & Control Layers](#runtime-foundations--control-layers)
  - [Sandboxes & Execution Infrastructure](#sandboxes--execution-infrastructure)
  - [Coding-Agent Harnesses](#coding-agent-harnesses)
  - [Multi-Agent Orchestration](#multi-agent-orchestration)
  - [Browser, MCP & Tool Integration](#browser-mcp--tool-integration)
  - [Workflow, Profiles & Asset Management](#workflow-profiles--asset-management)
- [Contributing](#contributing)
- [License](#license)

## Courses & Learning Resources

- [walkinglabs/learn-harness-engineering](https://github.com/walkinglabs/learn-harness-engineering) - A project-based course repository on making Codex and Claude Code more reliable, centered on an Electron personal knowledge base app with lecture handouts, example artifacts, and practical harness projects.
- [Phelan164/codex-howto](https://github.com/Phelan164/codex-howto) - A Codex-focused engineering curriculum with installable skills, repository instructions, scoped permissions, testing, review, orchestration, and reproducible token measurements for building an inspectable coding-agent harness.
- [hardness1020/awesome-agent-architecture](https://github.com/hardness1020/awesome-agent-architecture) - Trilingual architecture notes and runnable demos covering agent loops, tool execution, memory, permissions, context delivery, and orchestration.
- [awesome-agentic-ai](https://github.com/adriannoes/awesome-agentic-ai) - Learning hub with a vendored harness skill, spec-driven PM templates, and curated papers on agentic coding — complements course-style repos like awesome-agent-architecture.

## Foundations

<!-- FIXME: 403 Forbidden — - [Agent Harness for Large Language Model Agents: A Survey](https://www.preprints.org/manuscript/202604.0428) - A survey that formalizes, taxonomizes, and frames harness design for long-running LLM agents as a distinct research area. -->
- [Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/) - OpenAI's flagship field report on building a large application with Codex using architectural constraints, repo-local instructions, browser validation, and telemetry.
- [Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) - Anthropic's core article on initializer agents, feature lists, `init.sh`, self-verification, and handoff artifacts across many context windows.
- [Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps) - Anthropic follow-up focused on improving long-running app generation with better task state and evaluator design.
- [The Anatomy of an Agent Harness](https://blog.langchain.com/the-anatomy-of-an-agent-harness/) - LangChain's concise framing of an agent as model plus harness, with prompts, tools, middleware, orchestration, and runtime infrastructure.
- [Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html) - Thoughtworks' framing of harness work into context engineering, architectural constraints, and "garbage collection" against entropy.
- [Building effective agents](https://www.anthropic.com/engineering/building-effective-agents) - Anthropic's broader guide to workflows, agents, tools, and when structured systems outperform raw prompting.
- [Skill Issue: Harness Engineering for Coding Agents](https://www.humanlayer.dev/blog/skill-issue-harness-engineering-for-coding-agents) - A practical argument that weak results from coding agents are often harness problems rather than model problems.
- [Your Agent Needs a Harness, Not a Framework](https://www.inngest.com/blog/your-agent-needs-a-harness-not-a-framework) - Inngest's case for treating state, retries, traces, and concurrency as first-class infrastructure.
- [Greenfield AI, Brownfield AI, and the Vibecode You Just Inherited](https://sawinyh.com/blog/greenfield-vs-brownfield-ai-codebases) - A three-way taxonomy of codebases agents encounter — agent-native greenfield, true legacy brownfield, and recently-vibecoded inheritance — with playbooks for installing layered `CLAUDE.md` rules, ratcheted pre-commit hooks, baselined lint violations, and feature-folder refactors so the codebase itself stops being the harness bottleneck.
- [Harness Engineering for Language Agents: The Harness Layer as Control, Agency, and Runtime](https://www.preprints.org/manuscript/202603.1756) - A position paper that treats the harness layer as a first-class research object, proposes the **control–agency–runtime (CAR)** decomposition, and introduces **HarnessCard** for structured reporting of harness design and evaluation.
- [Many Hands Engineering](https://github.com/mseeks/many-hands-engineering/blob/main/many-hands-engineering.pdf) - A handbook framing the layer above the per-agent harness: how multiple harnessed agents share a commons, where decisions belong on a planned / emergent spectrum, and how human stewardship operates at a different cadence than agent execution. Treats harness engineering as a critical layer of "terrain" the framework sits on top of.
- [Agent Frameworks, Runtimes, and Harnesses, Oh My!](https://blog.langchain.com/agent-frameworks-runtimes-and-harnesses-oh-my/) - LangChain's decomposition of what belongs in a framework, a runtime, and a harness.

## Context, Memory & Working State

### Context Design & Delivery

- [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) - Anthropic's guidance on managing the context window as a working memory budget rather than a dumping ground.
- [Context Engineering for AI Agents: Lessons from Building Manus](https://manus.im/blog/Context-Engineering-for-AI-Agents-Lessons-from-Building-Manus) - Manus' detailed playbook on KV-cache locality, tool masking, filesystem memory, and keeping useful failures in-context.
- [Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) - Thoughtworks guidance on shaping the task environment so coding agents can stay grounded and productive.
- [Advanced Context Engineering for Coding Agents](https://www.humanlayer.dev/blog/advanced-context-engineering) - HumanLayer patterns for reducing context drift and making coding sessions easier to resume.
- [Context-Efficient Backpressure for Coding Agents](https://www.humanlayer.dev/blog/context-efficient-backpressure) - HumanLayer's ideas for preventing agents from burning context on noisy or low-value work.
- [OpenHands Context Condensensation for More Efficient AI Agents](https://openhands.dev/blog/openhands-context-condensensation-for-more-efficient-ai-agents) - OpenHands' design for bounded conversation memory that preserves goals, progress, critical files, and failing tests while keeping long-running coding sessions efficient.
- [Writing a good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md) - A practical guide to creating durable, repo-local instructions that agents can repeatedly follow.
- [Deterministic Context Routing](https://github.com/ai-erp-collab/deterministic-context-routing) - A context-management methodology that routes only the necessary-and-sufficient context to an agent through a deterministic chain (module registry → wiki → session state), cutting overread and context loss on large, under-documented multi-module codebases.
- [DevProjex](https://github.com/Avazbek22/DevProjex) - GUI, TUI, and CLI tooling for selecting and exporting structured codebase context with folder trees, token estimates, ignore rules, and previews.

### Memory & Knowledge Systems

- [wiki](https://github.com/plasma-ai/wiki) - Indexed Markdown knowledge bases that give agents incremental project context through deterministic indexes, scoped CLI access, and merge handling for parallel edits.
- [Data Olympus](https://github.com/knaisoma/data-olympus) - Git-native project knowledge base and MCP server with governed proposal-to-acceptance workflows, validity windows, supersession chains, and retrieval of in-force engineering guidance.
- [OpenViking](https://github.com/volcengine/OpenViking) - Context database that unifies agent memory, knowledge retrieval, and skills behind an MCP-accessible storage layer.

## Constraints, Guardrails & Safe Autonomy

### Tool Design & Execution Boundaries

- [Code execution with MCP: building more efficient agents](https://www.anthropic.com/engineering/code-execution-with-mcp) - Anthropic's approach to giving agents controlled execution power through explicit, inspectable tool boundaries.
- [Writing effective tools for agents](https://www.anthropic.com/engineering/writing-tools-for-agents) - Anthropic's guidance on tool interfaces that are easier for models to call correctly and safely.
- [mcp-guardian](https://github.com/S1LV3RJ1NX/mcp-guardian) - MCP proxy for progressive tool discovery, scope-based allow/block lists, and audit logging, reducing startup context while preventing blocked tools from being discovered or called.

### Security, Authorization & Policy

- [Beyond permission prompts: making Claude Code more secure and autonomous](https://www.anthropic.com/engineering/claude-code-sandboxing) - Anthropic on reducing approval friction without losing control through better sandboxing and policy design.
- [Mitigating Prompt Injection Attacks in Software Agents](https://openhands.dev/blog/mitigating-prompt-injection-attacks-in-software-agents) - OpenHands' practical guide to confirmation mode, analyzers, sandboxing, and hard policies for reducing prompt-injection risk in autonomous coding agents.
- [APort Agent Guardrails](https://github.com/aporthq/aport-agent-guardrails) - Deterministic pre-action authorization hooks for AI-agent tool calls, with adapters for Claude Code, Cursor, OpenClaw, LangChain, CrewAI, and related runtimes.
- [Lurkr](https://github.com/agentveil-protocol/lurkr) - Static scanner that runs in CI before deploy to surface AI-agent capability risks, including shadow capabilities, credentials into LLM context, eval/subprocess in `@tool`, direct prompt interpolation, and unverified MCP endpoints.
- [HEAAL](https://github.com/hyun06000/AIL) - Grammar-enforced safety constraints for AI agents via AIL (AI-Intent Language).

### Operational Autonomy & Reliability

- [Spend rails for autonomous agents: a number, not a vibe](https://joeyycli.github.io/agent-ops-kit-guide/docs/spend-rails-for-autonomous-agents.html) - A concrete pattern for giving a scheduled agent real purchasing authority without real risk: a per-transaction autonomy line, an escalation threshold, a hard lifetime ceiling, and a transaction ledger as the actual enforcement mechanism instead of relying on the model's judgment.
- [Distributed retry patterns: bounding blast radius across a fleet](https://loopandretry.github.io/posts/fleet-retry-patterns/) - Practitioner guidance on concurrency bounds, decorrelated backoff, circuit breakers, and idempotency for preventing agent retry storms.

## Specs, Agent Files & Workflow Design

### Instruction Files & Formats

- [AGENTS.md](https://github.com/agentsmd/agents.md) - A lightweight open format for repo-local instructions that tell agents how to work inside a codebase.
- [agent.md](https://github.com/agentmd/agent.md) - A related standardization effort for machine-readable agent instructions across projects and tools.

### Spec-Driven Development

- [GitHub Spec Kit](https://github.com/github/spec-kit) - GitHub's toolkit for spec-driven development, useful when you want agents to execute against explicit product and engineering specs.
- [Context Repository-Driven Development (CRDD)](https://github.com/qual-lab/CRDD) - A repository-centered methodology for preserving product intent, decisions, specifications, evidence, and traceability as durable context while keeping approval authority with humans.
- [Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) - Thoughtworks on why strong specs make AI-assisted software delivery more dependable.

### Operating Principles & Human Oversight

- [12 Factor Agents](https://www.humanlayer.dev/blog/12-factor-agents) - HumanLayer's operating principles for production agents, including explicit prompts, state ownership, and clean pause-resume behavior.
- [12-Factor AgentOps](https://www.12factoragentops.com/) - An operations-oriented companion focused on context discipline, validation, and reproducible agent workflows.
- [Anchoring AI to a reference application](https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-reference.html) - Thoughtworks on constraining agents with concrete exemplars so they produce more consistent output.
- [Humans and Agents in Software Engineering Loops](https://martinfowler.com/articles/exploring-gen-ai/humans-and-agents.html) - A clear mental model for where humans should strengthen the harness instead of micromanaging every artifact.
- [Claude Code: Best practices for agentic coding](https://code.claude.com/docs) - Anthropic's practical recommendations for repo structure, checkpoints, validation, and delegation in agentic coding workflows.

## Evals & Observability

### Evaluation Design

- [Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills/) - OpenAI's concrete guide to turning agent traces into repeatable evals with JSONL logs and deterministic checks.
- [How to Evaluate Agent Skills (And Why You Should)](https://openhands.dev/blog/evaluating-agent-skills) - OpenHands' hands-on playbook for measuring whether a skill actually helps using bounded tasks, deterministic verifiers, no-skill baselines, and trace review.
- [Agent evals](https://platform.openai.com/docs/guides/agent-evals) - OpenAI's product guide for measuring agent quality with reproducible task-level and workflow-level evaluations.
- [Evaluation best practices](https://platform.openai.com/docs/guides/evaluation-best-practices) - OpenAI's general guide to building eval suites that match real-world distributions and catch regressions early.
- [Trace grading](https://platform.openai.com/docs/guides/trace-grading) - OpenAI documentation on grading agent traces directly, which is especially helpful for long multi-step tasks.
- [Inspect AI](https://inspect.aisi.org.uk/) - UK AISI's open-source evaluation framework with solver, scorer, sandboxing, tool-use, MCP, and log-viewer primitives for building reproducible agent eval harnesses.
- [Demystifying Evals for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) - Anthropic's guidance on what to measure when agents have many possible trajectories to success or failure.
- [Evaluating Deep Agents: Our Learnings](https://blog.langchain.com/evaluating-deep-agents-our-learnings/) - LangChain's practical breakdown of single-step, full-run, and multi-turn eval design for stateful agents.

### Verification & Quality Gates

- [Assessing internal quality while coding with an agent](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html) - Thoughtworks on moving quality checks into the loop instead of relying on after-the-fact manual review.
- [Better Harness](https://github.com/QoderAI/better-harness) - Reviewer for coding-agent workflows that turns repository and session evidence into prioritized, verifiable harness improvements while keeping unobserved behavior explicit.
- [Learning to Verify AI-Generated Code](https://openhands.dev/blog/20260305-learning-to-verify-ai-generated-code) - OpenHands' overview of a layered verification stack using trajectory critics trained on production traces for reranking, early stopping, and review-time quality control.
- [Improving Deep Agents with harness engineering](https://blog.langchain.com/improving-deep-agents-with-harness-engineering/) - LangChain's evidence that harness changes alone can significantly improve benchmark performance.

### Telemetry, Tracing & Performance

- [OpenTelemetry Semantic Conventions for Generative AI Systems](https://opentelemetry.io/docs/specs/semconv/gen-ai/) - Standard span, metric, event, and attribute conventions for instrumenting LLM and agent workflows so harness traces stay portable across observability backends.
- [AgentOps](https://github.com/AgentOps-AI/agentops) - Open-source Python SDK for agent monitoring, session replay, cost tracking, benchmarking, and tracing across common LLM and agent frameworks.
- [agenttrace](https://github.com/luoyuctl/agenttrace) - Local-first TUI/CLI for auditing AI coding-agent session traces, health gates, cost spikes, tool failures, latency gaps, and attempt-to-attempt diffs.
- [flameox](https://github.com/morluto/flameox) - Profiling and optimization toolkit for agents: bounded CLI and MCP workflows capture traces, preserve native evidence, and compare experiments behind runtime conclusions.
- [ax](https://github.com/Necmttn/ax) - Local-first telemetry and memory graph for auditing coding-agent sessions, costs, skills, tool usage, and OTLP events across multiple agent runtimes.
- [Quantifying infrastructure noise in agentic coding evals](https://www.anthropic.com/engineering/infrastructure-noise) - Anthropic on how runtime configuration can move coding benchmark scores by more than many leaderboard gaps.

## Benchmarks

These benchmarks are especially useful when you want to compare harness quality, not just model quality. They stress context handling, tool calling, environment control, verification logic, and the runtime scaffolding around the model.

### Coding & Terminal Agents

- [EvoClaw: Evaluating AI Agents on Continuous Software Evolution](https://openhands.dev/blog/evoclaw-benchmark) - A benchmark write-up on evaluating agents across dependent milestone sequences from real repository history, surfacing regression accumulation and long-horizon precision loss.
- [Introducing Terminal-Bench 2.0 and Harbor](https://www.tbench.ai/news/announcement-2-0) - The Terminal-Bench 2.0 announcement, useful for understanding the harder tasks and generalized evaluation harness behind Harbor.
- [LeetCode-Hard Gym](https://github.com/GammaTauAI/leetcode-hard-gym) - An RL environment interface to LeetCode's submission server for evaluating codegen agents, giving harnesses direct access to execution-based feedback on hard algorithmic problems.
- [SEC-bench](https://github.com/SEC-bench/SEC-bench) - A benchmark for evaluating LLM agents on real-world software security tasks including vulnerability reproduction and patching, stressing harness design around code execution, containerized environments, and security-aware tooling.
- [SWE-bench Verified](https://www.swebench.com/) - A strong benchmark for software engineering agents working against real GitHub issues and tests, which makes harness choices around retrieval, patching, and validation highly visible.
- [Terminal-Bench](https://www.tbench.ai/) - A benchmark suite for terminal-native agents operating in shells, filesystems, and verification-heavy environments, which is especially useful for comparing coding-agent harnesses.

### Web, GUI & Computer Use

- [AgentStudio](https://github.com/SkyworkAI/agent-studio) - An integrated benchmark suite with realistic environments and comprehensive toolkits for evaluating virtual agents on real computer software, useful for measuring harness depth against a broad task surface.
- [AssistantBench](https://github.com/oriyor/AssistantBench) - A benchmark that evaluates web agents on realistic, time-consuming research tasks requiring multi-step tool use and information synthesis, making it a good proxy for harness quality in long-horizon web scenarios.
- [BrowseComp](https://www.kaggle.com/benchmarks/openai/browsecomp) - A benchmark that evaluates AI agents on locating hard-to-find information, stressing search strategy, context management, and retrieval harness design under difficult conditions.
- [BrowserGym Leaderboard](https://huggingface.co/spaces/ServiceNow/browsergym-leaderboard) - A gym environment and leaderboard for evaluating LLMs, VLMs, and agents on web navigation tasks, offering a reproducible framework for comparing harnesses across multiple web benchmarks in one place.
- [ClawBench: Can AI Agents Complete Everyday Online Tasks?](https://huggingface.co/papers/2604.08523) - A browser-agent benchmark of 153 everyday web tasks across 144 live production sites in 15 categories, using a lightweight interception layer that captures and blocks only the final submission request so agents can be scored end-to-end on real websites without real-world side effects.
- [Computer Agent Arena](https://github.com/xlang-ai/computer-agent-arena) - An open evaluation platform where users compare LLM/VLM-based agents on real-world computer tasks ranging from general computer use to coding, data analysis, and video editing, surfacing harness differences across a wide task surface.
- [OSWorld](https://os-world.github.io/) - A real computer-use benchmark with 369 tasks across Ubuntu, Windows, and macOS, complete with initial-state setup and execution-based evaluators, making it excellent for testing desktop and multimodal harnesses.
- [OSWorld-MCP](https://osworld-mcp.github.io) - An extension of OSWorld that evaluates AI agents on real-world computer tasks using the Model Context Protocol, making it useful for comparing MCP-enabled harnesses on a realistic desktop task suite.
- [VAB](https://github.com/THUDM/VisualAgentBench) - VisualAgentBench evaluates large multimodal models as visual foundation agents across embodied, GUI, and visual design tasks, useful for comparing harnesses on visually grounded, multi-step agent workflows.
- [VisualWebArena](https://jykoh.com/vwa) - A benchmark for multimodal web agents on realistic visually grounded tasks, extending WebArena with image and screenshot inputs that stress harness support for visual context in browser environments.
- [WebArena](https://webarena.dev/) - A standalone, self-hostable web environment for evaluating autonomous agents on realistic tasks, making it a reproducible baseline for comparing web-facing harness designs.
- [WebArena-Verified](https://github.com/ServiceNow/webarena-verified) - A verified web-agent benchmark with curated tasks and deterministic evaluators over agent responses and captured network traces, making it a good fit for measuring web-facing harnesses.
- [WorkArena](https://github.com/ServiceNow/WorkArena) - A benchmark for browser agents on common knowledge-work tasks, useful for comparing harnesses on realistic enterprise-style web workflows instead of toy browser tasks.

### Tools, APIs & MCP

- [AgentBench](https://github.com/THUDM/AgentBench) - A cross-environment benchmark spanning OS, databases, knowledge graphs, web browsing, and more, useful for seeing whether a harness generalizes beyond one narrow task loop.
- [AppWorld](https://appworld.dev/) - A controllable world of apps and people for benchmarking interactive coding agents, with state-based and execution-based unit tests that surface harness quality around planning, code generation, and collateral-damage control.
- [GTA](https://github.com/open-compass/GTA) - A benchmark that evaluates the tool-use capability of LLM-based agents using human-written queries, real deployed tools, and authentic multimodal inputs, exposing harness gaps between isolated testing and real deployment.
- [MCP Bench](https://github.com/modelscope/MCPBench) - A benchmark for evaluating AI models on MCP server interactions, measuring tool accuracy, latency, and token use across server types, which directly reflects harness design choices around MCP integration.
- [MCP Universe](https://mcp-universe.github.io/) - A leaderboard comparing AI model performance on MCP tasks, tracking how different models and harness configurations handle tool-augmented agent workflows.
- [MCPMark](https://github.com/eval-sys/mcpmark) - A stress-testing benchmark for model and agent capabilities in real-world MCP tasks across tools like Notion, GitHub, and Postgres, making harness MCP integration quality directly measurable.
- [τ-Bench](https://github.com/sierra-research/tau-bench) - A benchmark that emulates dynamic conversations between a simulated user and a language agent equipped with domain-specific API tools and policy guidelines, making it useful for evaluating harnesses built around structured tool use and policy enforcement.
- [tau2-bench](https://github.com/sierra-research/tau2-bench) - A benchmark for realistic, multi-step agent tasks where success depends on tool use and execution quality rather than a single-shot answer.
- [TravelPlanner](https://github.com/OSU-NLP-Group/TravelPlanner) - A benchmark for evaluating LLM agents on tool use and complex planning within multiple constraints, revealing how harness design handles multi-constraint satisfaction and long-horizon planning.

### Multi-Agent, General & Interactive

- [Agent Arena](https://www.agent-arena.com/leaderboard) - A leaderboard that ranks AI agents, models, tools, and frameworks using ELO-style ratings from head-to-head battles, providing a structured way to compare harness-level choices across categories.
- [AgentBoard](https://github.com/HKUST-NLP/AgentBoard) - A benchmark for multi-turn LLM agents complemented by an analytical evaluation board for assessing model performance beyond final success rates, making partial-progress and trajectory quality visible.
- [CharacterEval](https://github.com/morecry/CharacterEval) - A benchmark for evaluating role-playing conversational agents using multi-turn dialogues and character profiles, with metrics across four dimensions including character fidelity and conversational coherence.
- [ClawBench](https://clawbench.net) - A benchmark that evaluates AI agents across search, reasoning, coding, safety, and multi-turn conversation tasks, covering the breadth of harness demands in a single suite.
- [GAIA](https://huggingface.co/datasets/gaia-benchmark/GAIA) - A benchmark for general AI assistants that is often used to compare harness-level choices around tools, planning, verification, and long-horizon autonomy.
- [Galileo Agent Leaderboard](https://huggingface.co/spaces/galileo-ai/agent-leaderboard) - An open evaluation platform tracking LLM agents on task completion and tool calling across business domains, useful for comparing harness quality in enterprise-grade agentic scenarios.
- [HAL: Holistic Agent Leaderboard](https://hal.cs.princeton.edu/) - A benchmark and leaderboard for agent systems with attention to reliability, cost, and broad task coverage, making it useful for comparing end-to-end harness behavior.
- [LLM Colosseum Leaderboard](https://github.com/OpenGenerativeAI/llm-colosseum) - A platform that evaluates LLMs by having them fight in Street Fighter III, testing speed, adaptability, and real-time decision-making as proxies for harness responsiveness under tight latency constraints.
- [MAgIC](https://zhiyuanhubj.github.io/MAgIC/) - A benchmark measuring cognition, adaptability, rationality, and collaboration of LLMs in multi-agent systems, useful for evaluating how harnesses coordinate agent interactions and shared state.
- [WildClawBench](https://github.com/InternLM/WildClawBench) - An in-the-wild benchmark running agents inside a live OpenClaw environment on 60 original tasks including multimodal, long-horizon, and safety-critical scenarios, making harness robustness under real-world conditions directly visible.

### Safety, Robustness & Economic Agency

- [ClawWork](https://github.com/HKUDS/ClawWork) - A real-world economic benchmark where AI agents complete professional tasks spanning 44 occupations, earning income while managing token costs and economic solvency, making it a direct test of harness efficiency under resource constraints.
- [Olas Predict Benchmark](https://github.com/valory-xyz/olas-predict-benchmark) - A benchmark for evaluating agents on historical prediction market data, testing harness design for research, retrieval, and forecasting in long-horizon reasoning tasks.

## Runtimes, Harnesses & Reference Implementations

### Runtime Foundations & Control Layers

- [Building agents with the Claude Agent SDK](https://claude.com/blog/building-agents-with-the-claude-agent-sdk) - Anthropic's guide to a production-oriented agent SDK with sessions, tools, and orchestration support.
- [AgentKit](https://github.com/inngest/agent-kit) - Inngest's TypeScript toolkit for building durable, workflow-aware agents on top of event-driven infrastructure.
- [SandBase Harness](https://github.com/sandbaseai/sandbase-harness) - Apache-2.0 agent runtime with persistent sessions, governed MCP tools, credential handling, audit and replay, and interchangeable local or sandboxed execution backends.
- [DSH Studio](https://github.com/Moresyl/dsh-studio) - Cross-platform desktop host for DeepSeek Harness with health probes, restart backoff, collision-free ports, and whole-process-tree cleanup.
- [BitRouter](https://github.com/bitrouter/bitrouter) - Apache-2.0 model router with cross-protocol routing, MCP gateway, guardrails, observability, virtual keys, and multi-account failover.
- [rust-norion](https://github.com/yanghao1143/rust-norion) - GPL-3.0 Rust inference-control prototype exploring runtime boundaries, governed memory and replay, evidence-based writer gates, audit traces, and rollback for self-evolving agent systems.

### Sandboxes & Execution Infrastructure

- [SWE-ReX](https://github.com/SWE-agent/SWE-ReX) - Sandboxed code execution infrastructure for AI agents, useful when harness work starts to merge into execution runtime design.
- [Harbor](https://github.com/harbor-framework/harbor) - A generalized harness for evaluating and improving agents at scale, released alongside Terminal-Bench 2.0.
- [Mitos](https://github.com/mitos-run/mitos) - Snapshot-fork microVM sandboxes that give agent sessions clean, isolated starting states with declarative lifecycle control and parallel execution.

### Coding-Agent Harnesses

- [deepagents](https://github.com/langchain-ai/deepagents) - LangChain's open-source project for building deeper, longer-running agents with middleware and harness patterns.
- [SWE-agent](https://github.com/SWE-agent/SWE-agent) - A mature research coding agent that makes the harness, prompt, tools, and environment design directly inspectable.
- [Citadel](https://github.com/SethGammon/Citadel) - A harness for Claude Code and OpenAI Codex with isolated worktrees, multi-agent coordination, and persisted memory and campaign state.
- [Harness Evolver](https://github.com/raphaelchristi/harness-evolver) - Claude Code plugin that autonomously evolves LLM agent harnesses using multi-agent proposers, LangSmith-backed evaluation, and git worktree isolation. Based on Meta-Harness (Lee et al., 2026).
- [Ralph Wiggum as a Software Engineer](https://ghuntley.com/ralph/) - Geoffrey Huntley's write-up of "Ralph," a minimalist `while :; do cat PROMPT.md | claude-code; done` harness pattern that uses single-task loops, deterministic prompt stacking, and bounded subagent parallelism to drive long-running autonomous coding.
- [RailWarden](https://github.com/advaith-1212/railwarden) - Deterministic control plane for multi-agent software work with dependency-aware packages, isolated worktrees, durable validation evidence, recovery checkpoints, and integration gates.
- [OpenCode Agent Orchestration Kit](https://github.com/jcarlosrodicio/opencode-agent-orchestration-kit) - Reproducible OpenCode harness with role-based agents, explicit handoffs, repo-local skills, safe installation, and mechanical contract validation.
- [LoopTroop](https://github.com/looptroop-ai/LoopTroop) - Local-first GUI harness for long-running coding work with multi-model planning, isolated worktrees, and fresh-context recovery loops.
- [Agent AFK](https://github.com/griffinwork40/agent-afk) - Headless coding-agent harness for asynchronous runs with explicit terminal states, editable lifecycle hooks, permission gates, model routing, and append-only traces.
- [completely](https://github.com/23ag1/completely) - Claude Code plugin harness with a default-fail evaluator, deterministic write and close gates, orphan recovery, and parallel-worker integration checks.
- [forge-harness](https://github.com/chrono-meta/forge-harness) - Claude Code plugin for adversarial validation, source-grounding audits, session-learning capture, and pre-deployment transfer simulation.

### Multi-Agent Orchestration

- [How we built our multi-agent research system](https://www.anthropic.com/engineering/multi-agent-research-system) - Anthropic's architecture write-up for a multi-agent system with separation of roles and structured coordination.
- [Orkas](https://github.com/Orkas-AI/Orkas) - Local-first desktop harness for coordinating multiple agents with shared files, independent work contexts, human approval gates, and resumable execution.
- [Agentlas OS](https://github.com/agentlas-ai/Agentlas-OS) - Local-first agent operation environment that composes specialist teams while retaining host-local tools, permissions, memory boundaries, and verification rules.
- [Squadron](https://github.com/mlund01/squadron) - MIT-licensed declarative runtime for multi-agent workflows defined in HCL, including orchestration, state, dependency resolution, routing, persistence, and resume.
- [Cowork Forge](https://github.com/sopaco/cowork-forge) - MIT-licensed multi-agent software-development workflow with specialized roles and a staged pipeline from requirements through delivery.

### Browser, MCP & Tool Integration

- [browser-use/browser-harness](https://github.com/browser-use/browser-harness) - A thin CDP-based browser harness that lets agents extend helper functions during execution, useful for inspecting self-healing web-task workflows.
- [Uni-CLI](https://github.com/olo-dot-io/Uni-CLI) - Universal CLI hub connecting agents to 134 sites and desktop apps via 711 declarative YAML pipelines. Ships an 8-phase Karpathy-style self-repair loop, eval harness with a starter catalog, per-call cost ledger, hardcoded sensitive-path deny list, and `unicli mcp serve` that auto-registers one MCP tool per adapter. ~80 tokens per invocation.
- [OpenAgentRelay](https://github.com/ShakespeareLabs/open-agent-relay) - Inspectable runtime boundary for exposing a local agent or automation as a keyed LAN capability with target verification, bounded conversations, JSON output, and explicit exit codes.
- [BrowserAct](https://github.com/browser-act/skills) - Open-source browser automation layer for agents with isolated parallel sessions, multi-account operation, and human handoff when automation is blocked.

### Workflow, Profiles & Asset Management

- [Bring Your AI MCP](https://github.com/unitedideas/bringyour-mcp) - Public harness-migration reference for Claude Code to Codex moves, with installable auditor artifacts and explicit validation notes for hooks, MCP config, and instruction-file differences.
- [skills.sh](https://skills.sh) - A community marketplace for discovering, sharing, and installing reusable AI agent skills across runtimes like Claude Code and OpenClaw, making harness capabilities portable and composable.
- [stelow](https://github.com/calionauta/stelow) - Agentic product-workflow harness with Shape Up boundaries, adversarial plan review, acceptance-based execution contracts, and audit loops.
- [Build A Harness](https://github.com/3IVIS/buildaharness) - Apache-2.0 visual canvas for agent harnesses that compiles a runtime-neutral FlowSpec to several orchestration frameworks.
- [agent-harness](https://github.com/ar27111994/agent-harness) - Reproducible lifecycle for coding-agent assets with authority-ranked discovery, pinned mirrors, quarantine routing, staged activation, and host-specific wiring.
- [codex-profiles](https://github.com/Ducksss/codex-profiles) - Codex CLI and Desktop profile launcher that isolates authentication, configuration, sessions, connectors, plugins, and logs by `CODEX_HOME`.
- [AgentPlane](https://github.com/basilisk-labs/agentplane) - Git-native workflow-control harness that stores task records, policy, verification evidence, and closure state as reviewable repository artifacts.

## Contributing

Contributions are welcome. Please prefer resources that are:

- Specific about how agents are constrained, evaluated, resumed, observed, or orchestrated
- Original implementations, primary-source articles, or high-signal technical write-ups
- Useful to practitioners building real harnesses instead of generic AI commentary

If two links say the same thing, prefer the more primary, practical, and implementation-oriented one.

See [CONTRIBUTING.md](./CONTRIBUTING.md) for contribution guidelines and the preferred entry format.

## License

[CC0 1.0](./LICENSE)
