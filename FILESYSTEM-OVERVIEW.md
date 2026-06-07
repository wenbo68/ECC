# Filesystem Overview

- Date: 2026-06-07
- Summary: **everything-claude-code (ECC)** is a production-ready Claude Code plugin — a curated
  collection of agents, skills, hooks, commands, rules, and MCP configurations that provide
  battle-tested workflows for software development with Claude Code. It supports 60+ specialized
  subagents, 250+ domain skills (web, AI/ML, mobile, infra, healthcare, web3, and more), 79 slash
  commands, per-language coding rules for 20 languages, a rich hook system, and a modular install
  architecture with profiles. It also ships adapter configs for every major AI coding assistant
  (Cursor, Codex, Gemini, Kiro, OpenCode, Qwen, Zed, etc.) and a Rust TUI next-generation
  implementation in `ecc2/`.

## Structure

```
ECC/
├── .env.example               — environment variable template for secrets and feature flags
├── .gitignore                 — git ignore rules
├── .markdownlint.json         — markdownlint configuration for .md files
├── .mcp.json                  — project-level MCP server configuration
├── .npmignore                 — files excluded from npm publish
├── .prettierrc                — Prettier code formatter settings
├── .tool-versions             — asdf runtime version pins (Node, Python, etc.)
├── .yarnrc.yml                — Yarn v2+ package manager configuration
├── AGENTS.md                  — guide to selecting and using ECC agents
├── CHANGELOG.md               — version history and release notes
├── CLAUDE.md                  — Claude Code project instructions for this repo
├── CODE_OF_CONDUCT.md         — community code of conduct
├── COMMANDS-QUICK-REF.md      — quick-reference card for all slash commands
├── CONTRIBUTING.md            — contribution guidelines and artifact format specs
├── EVALUATION.md              — evaluation methodology and benchmark descriptions
├── LICENSE                    — MIT license
├── README.md                  — main project documentation, quick-start, and feature overview
├── README.zh-CN.md            — Simplified Chinese translation of README
├── REPO-ASSESSMENT.md         — repository quality self-assessment
├── RULES.md                   — overview of per-language coding rules
├── SECURITY.md                — security policy and vulnerability reporting
├── SOUL.md                    — design philosophy and guiding principles
├── SPONSORING.md              — how to sponsor the project
├── SPONSORS.md                — list of current sponsors
├── TROUBLESHOOTING.md         — common issues, diagnostics, and fixes
├── VERSION                    — current release version string
├── WORKING-CONTEXT.md         — active development notes and in-progress context
├── agent.yaml                 — top-level agent YAML definition for agent harness
├── commitlint.config.js       — commit message linting rules (conventional commits)
├── ecc_dashboard.py           — Python dashboard utility for ECC metrics visualization
├── eslint.config.js           — ESLint flat config for JS scripts
├── install.ps1                — Windows PowerShell installer
├── install.sh                 — Unix shell installer
├── package-lock.json          — npm dependency lockfile
├── package.json               — Node.js project manifest, scripts, and dev dependencies
├── pyproject.toml             — Python project manifest (for src/ LLM library)
├── the-longform-guide.md      — comprehensive long-form guide to Claude Code workflows
├── the-security-guide.md      — security best practices and threat modeling guide
├── the-shortform-guide.md     — concise short-form coding guide
├── yarn.lock                  — Yarn dependency lockfile
│
├── .agents/                   — agent definitions adapted for non-Claude AI providers
├── .claude-plugin/            — Claude plugin metadata and registration config
├── .claude/                   — Claude Code project-level commands, skills, and rules
├── .codebuddy/                — Codebuddy AI assistant integration configuration
├── .codex-plugin/             — Codex plugin metadata
├── .codex/                    — OpenAI Codex integration configuration
├── .cursor/                   — Cursor IDE AI integration settings
├── .gemini/                   — Google Gemini AI integration configuration
├── .git/                      — git repository data
├── .github/                   — GitHub Actions CI/CD workflows and issue templates
├── .kiro/                     — Kiro AI assistant integration configuration
├── .opencode/                 — OpenCode AI coding assistant configuration
├── .qwen/                     — Alibaba Qwen AI integration configuration
├── .trae/                     — Trae AI integration configuration
├── .vscode/                   — VS Code editor settings and extension recommendations
├── .zed/                      — Zed editor integration settings
│
├── agents/                    — 63 specialized subagent .md files, each invokable via Agent()
│   ├── a11y-architect.md          — accessibility-focused architecture and remediation
│   ├── architect.md               — system design and architecture planning
│   ├── build-error-resolver.md    — diagnoses and fixes build failures
│   ├── chief-of-staff.md          — high-level planning and session prioritization
│   ├── code-architect.md          — code-level design and structure decisions
│   ├── code-explorer.md           — read-only codebase exploration and mapping
│   ├── code-reviewer.md           — correctness and quality code review
│   ├── code-simplifier.md         — refactoring for clarity and simplicity
│   ├── codebase-explorer.md       — thin orchestrator for filesystem + dependency overviews
│   ├── comment-analyzer.md        — reviews code comments for quality
│   ├── cpp-reviewer.md            — C++-specific code review
│   ├── database-reviewer.md       — database schema and query review
│   ├── doc-updater.md             — keeps documentation in sync with code changes
│   ├── e2e-runner.md              — generates and runs end-to-end tests
│   └── … (49 more: framework-specific reviewers, build resolvers, planners, etc.)
│
├── assets/                    — static visual assets for documentation
│   └── images/
│       ├── guides/                — screenshots and diagrams for guide docs
│       ├── longform/              — images for the long-form guide
│       ├── security/              — images for the security guide
│       └── shortform/            — images for the short-form guide
│
├── commands/                  — 79 slash-command definitions (each invoked as /command-name)
│   ├── aside.md                   — record an aside note without disrupting flow
│   ├── auto-update.md             — auto-update ECC components
│   ├── build-fix.md               — diagnose and fix build errors
│   ├── checkpoint.md              — save current session state as a checkpoint
│   ├── code-review.md             — run structured code quality review
│   ├── cost-report.md             — report current session token and cost usage
│   ├── ecc-guide.md               — interactive ECC feature walkthrough
│   ├── evolve.md                  — evolve a skill from session learnings
│   ├── feature-dev.md             — structured feature development workflow
│   └── … (70 more: language-specific build/review/test, research, planning, ops, etc.)
│
├── config/                    — project configuration data
│   └── project-stack-mappings.json  — maps project types to recommended ECC skill stacks
│
├── contexts/                  — reusable context documents loaded at session start
│   ├── dev.md                     — development session context (tools, conventions, goals)
│   ├── research.md                — research session context
│   └── review.md                  — code review session context
│
├── docs/                      — extended documentation, architecture notes, and translations
│   ├── ANTIGRAVITY-GUIDE.md       — advanced / undocumented ECC usage patterns
│   ├── ARCHITECTURE-IMPROVEMENTS.md — architecture evolution proposals
│   ├── COMMAND-AGENT-MAP.md       — maps each slash command to its backing agent
│   ├── COMMAND-REGISTRY.json      — machine-readable registry of all commands
│   ├── ECC-2.0-GA-ROADMAP.md      — ECC 2.0 general-availability roadmap
│   ├── ECC-2.0-REFERENCE-ARCHITECTURE.md — reference architecture for ECC 2.0
│   ├── SKILL-PLACEMENT-POLICY.md  — policy for curated vs. generated skill placement
│   ├── SKILL-DEVELOPMENT-GUIDE.md — guide for writing new skills
│   ├── TOKEN-optimization.md      — techniques for minimizing token usage
│   ├── … (many more reference and planning docs)
│   ├── architecture/              — deep-dive architecture research documents
│   ├── business/                  — business context, capability templates
│   ├── de-DE/                     — German translations
│   ├── drafts/                    — work-in-progress documentation
│   ├── examples/                  — example patterns and templates
│   ├── fixes/                     — bug fix documentation
│   ├── ja-JP/                     — Japanese translations of agents, commands, skills, rules
│   ├── ko-KR/                     — Korean translations
│   ├── pt-BR/                     — Brazilian Portuguese translations
│   ├── releases/                  — per-version release notes
│   ├── ru/                        — Russian translations
│   ├── security/                  — security documentation
│   ├── th/                        — Thai translations
│   ├── tr/                        — Turkish translations
│   ├── vi-VN/                     — Vietnamese translations
│   ├── zh-CN/                     — Simplified Chinese translations
│   └── zh-TW/                     — Traditional Chinese translations
│
├── ecc2/                      — Rust / TUI next-generation ECC implementation (ECC 2.0)
│   ├── Cargo.lock                 — Rust dependency lockfile
│   ├── Cargo.toml                 — Rust project manifest
│   ├── README.md                  — ecc2 overview, design goals, and build instructions
│   └── src/                       — Rust source modules
│       ├── main.rs                — binary entry point
│       ├── notifications.rs       — notification system
│       ├── comms/                 — inter-component communication
│       ├── config/                — configuration loading
│       ├── observability/         — metrics and tracing
│       ├── session/               — session lifecycle management
│       ├── tui/                   — terminal UI (TUI) rendering
│       └── worktree/              — git worktree management
│
├── examples/                  — reference CLAUDE.md files and prototype implementations
│   ├── CLAUDE.md                  — generic example CLAUDE.md for new projects
│   ├── django-api-CLAUDE.md       — Django REST API project example
│   ├── go-microservice-CLAUDE.md  — Go microservice project example
│   ├── harmonyos-app-CLAUDE.md    — HarmonyOS app example
│   ├── hud-status-contract.json   — HUD status display contract spec
│   ├── laravel-api-CLAUDE.md      — Laravel API project example
│   ├── rust-api-CLAUDE.md         — Rust API project example
│   ├── saas-nextjs-CLAUDE.md      — SaaS Next.js project example
│   ├── evaluator-rag-prototype/   — RAG evaluator prototype implementation
│   └── gan-harness/               — GAN training harness prototype
│
├── hooks/                     — hook configuration and persistent state
│   ├── README.md                  — hooks overview, event types, and usage guide
│   ├── hooks.json                 — hook event matchers and command bindings
│   └── memory-persistence/        — session memory persistence hook implementation
│
├── integrations/              — third-party security and platform integrations
│   └── aura/                      — Aura security integration (threat model, adapter, tests)
│
├── legacy-command-shims/      — backwards-compatibility shims for renamed commands
│   ├── README.md                  — shim usage and migration guide
│   └── commands/                  — shim files redirecting old command names to new locations
│
├── manifests/                 — install manifests controlling what gets installed per profile
│   ├── install-components.json    — component-level install definitions
│   ├── install-modules.json       — module-level groupings of components
│   └── install-profiles.json      — named install profiles (full, minimal, etc.)
│
├── mcp-configs/               — MCP server configurations for external tool integrations
│   └── mcp-servers.json           — server definitions with transport, auth, and tool settings
│
├── plugins/                   — plugin system definitions and discovery
│   └── README.md                  — plugin architecture overview
│
├── research/                  — internal research documents and codebase analyses
│   └── ecc2-codebase-analysis.md  — deep analysis of the ecc2 Rust codebase
│
├── rules/                     — per-language coding rules auto-loaded by Claude Code
│   ├── README.md                  — rules overview and how they're applied
│   ├── angular/                   — Angular coding standards
│   ├── arkts/                     — ArkTS (HarmonyOS) coding standards
│   ├── common/                    — language-agnostic rules (agents, code-review, coding-style,
│   │                                git-workflow, hooks, patterns, performance, security, testing)
│   ├── cpp/                       — C++ coding standards
│   ├── csharp/                    — C# coding standards
│   ├── dart/                      — Dart/Flutter coding standards
│   ├── fsharp/                    — F# coding standards
│   ├── golang/                    — Go coding standards
│   ├── java/                      — Java coding standards
│   ├── kotlin/                    — Kotlin coding standards
│   ├── perl/                      — Perl coding standards
│   ├── php/                       — PHP coding standards
│   ├── python/                    — Python coding standards
│   ├── react/                     — React coding standards
│   ├── ruby/                      — Ruby coding standards
│   ├── rust/                      — Rust coding standards
│   ├── swift/                     — Swift coding standards
│   ├── typescript/                — TypeScript coding standards
│   └── web/                       — General web (HTML/CSS/JS) standards
│
├── schemas/                   — JSON schemas for validating ECC configuration files
│   ├── ecc-install-config.schema.json  — install configuration schema
│   ├── hooks.schema.json               — hooks.json validation schema
│   ├── install-components.schema.json  — components manifest schema
│   ├── install-modules.schema.json     — modules manifest schema
│   ├── install-profiles.schema.json    — profiles manifest schema
│   ├── install-state.schema.json       — install state persistence schema
│   ├── package-manager.schema.json     — package manager config schema
│   ├── plugin.schema.json              — plugin definition schema
│   ├── provenance.schema.json          — artifact provenance tracking schema
│   └── state-store.schema.json         — state store schema
│
├── scripts/                   — Node.js CLI utilities, CI validators, and hook implementations
│   ├── auto-update.js             — auto-update ECC components from upstream
│   ├── catalog.js                 — builds the skill/agent/command catalog index
│   ├── claw.js                    — OpenClaw protocol implementation
│   ├── consult.js                 — AI consultation utility
│   ├── control-pane.js            — control pane state management
│   ├── doctor.js                  — environment diagnostics and health checks
│   ├── ecc.js                     — main ECC CLI entry point
│   ├── install-apply.js           — applies a computed install plan to disk
│   ├── install-plan.js            — computes what to install given a profile
│   ├── harness-audit.js           — audits the agent harness for compliance
│   ├── … (more top-level utilities)
│   ├── ci/                        — CI validation scripts (validate-agents, validate-commands,
│   │                                validate-skills, validate-hooks, supply-chain checks, etc.)
│   ├── codemaps/                  — code map generation (generate.ts)
│   ├── codex/                     — Codex integration scripts (merge-mcp-config, merge-codex-config)
│   ├── codex-git-hooks/           — git hook scripts for the Codex workflow
│   └── hooks/                     — 45+ hook implementations: pre-bash, post-edit, session-start,
│                                    cost-tracker, quality-gate, security monitors, formatters, etc.
│
├── skills/                    — 251 named skill directories; each holds SKILL.md (and optional assets)
│   ├── accessibility/             — web accessibility audit and WCAG remediation
│   ├── agent-architecture-audit/  — review multi-agent system design for correctness
│   ├── agent-eval/                — evaluate and score agent output quality
│   ├── agentic-engineering/       — build and orchestrate agentic pipelines
│   ├── backend-patterns/          — backend API and service architecture patterns
│   ├── create-deps-overview/      — write DEPENDENCY-OVERVIEW.md for any codebase
│   ├── create-filesystem-overview/ — write FILESYSTEM-OVERVIEW.md for any codebase
│   ├── deep-research/             — multi-source web research with adversarial verification
│   ├── deployment-patterns/       — cloud and container deployment workflows
│   ├── django-patterns/           — Django-specific development and testing patterns
│   ├── e2e-testing/               — end-to-end test generation and execution
│   ├── everything-claude-code/    — ECC development conventions and patterns
│   ├── git-workflow/              — git branching, commit, and PR workflows
│   ├── react-patterns/            — React component, hook, and state patterns
│   ├── rename-claude-artifact/    — safely rename agents, commands, or skills across .claude
│   ├── security-review/           — security audit workflow
│   ├── tdd-workflow/              — test-driven development workflow
│   ├── typescript-patterns/       — TypeScript typing, module, and tooling patterns
│   └── … (233 more skills: AI/ML, healthcare, mobile, infra, web3, data, and more)
│
├── src/                       — Python LLM provider library used by ecc's Python tooling
│   └── llm/
│       ├── __init__.py            — package initializer and public API
│       ├── __main__.py            — CLI entry point
│       ├── cli/                   — command-line interface layer
│       ├── core/                  — core abstractions, types, and interfaces
│       ├── prompt/                — prompt templating and construction
│       ├── providers/             — LLM provider implementations (Claude, etc.)
│       └── tools/                 — tool definitions for structured LLM calls
│
└── tests/                     — test suite mirroring scripts/ and covering Python modules
    ├── run-all.js                 — test runner entry point
    ├── codex-config.test.js       — Codex config validation tests
    ├── opencode-config.test.js    — OpenCode config validation tests
    ├── opencode-plugin-hooks.test.js — OpenCode plugin hook tests
    ├── plugin-manifest.test.js    — plugin manifest validation tests
    ├── conftest.py                — pytest fixtures for Python tests
    ├── test_astraflow_provider.py — Astraflow LLM provider tests
    ├── test_builder.py            — prompt builder tests
    ├── test_claude_provider.py    — Claude provider tests
    ├── test_executor.py           — executor tests
    ├── test_provider_tools.py     — provider tool definition tests
    ├── test_resolver.py           — resolver tests
    ├── test_templates.py          — prompt template tests
    ├── test_types.py              — type definition tests
    ├── ci/                        — tests for CI validation scripts
    ├── commands/                  — command definition validation tests
    ├── docs/                      — documentation lint and correctness tests
    ├── hooks/                     — hook implementation tests (45+ test files)
    ├── integration/               — integration tests across components
    ├── lib/                       — unit tests for scripts/lib/ (37 test files)
    └── scripts/                   — tests for top-level script utilities
```
