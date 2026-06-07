# Dependency Overview

- Date: 2026/06/07
- Sources: `package.json`, `pyproject.toml`, `ecc2/Cargo.toml`

## List

### `package.json` — dependencies (runtime)

- `@iarna/toml`: `^2.2.5`
    - TOML parser used to read `.tool-versions`, plugin manifests, and ECC config files at runtime
- `ajv`: `^8.18.0`
    - JSON Schema validator used to validate hooks, install manifests, and plugin definitions against the schemas in `schemas/`
- `sql.js`: `^1.14.1`
    - Pure-JS SQLite (compiled from WebAssembly) used as the persistent state store for install state, session tracking, and observer data

### `package.json` — devDependencies

- `@eslint/js`: `^9.39.2`
    - ESLint's built-in JavaScript rule set, loaded by `eslint.config.js` (flat config)
- `@opencode-ai/plugin`: `^1.0.0`
    - OpenCode AI plugin SDK used to build and validate the OpenCode integration in `.opencode/`
- `@types/node`: `25.7.0`
    - TypeScript type definitions for Node.js built-ins, used by the `codemaps/generate.ts` build script
- `c8`: `^11.0.0`
    - V8-native code coverage tool; wired to `npm run coverage` with 80% thresholds for scripts/
- `eslint`: `^9.39.2`
    - JavaScript linter for all `.js` scripts; run as part of `npm run lint`
- `globals`: `^17.4.0`
    - Provides named global variable sets (browser, node, etc.) consumed by `eslint.config.js`
- `markdownlint-cli`: `^0.48.0`
    - Markdown linter for all `.md` files across agents/, commands/, skills/, rules/; run as part of `npm run lint`
- `typescript`: `^6.0.3`
    - TypeScript compiler used only for `scripts/codemaps/generate.ts`; the rest of the codebase is plain JS

---

### `pyproject.toml` — dependencies (runtime)

- `anthropic`: `>=0.25.0`
    - Anthropic Claude SDK; used by `src/llm/providers/` as the Claude LLM provider implementation
- `openai`: `>=1.30.0`
    - OpenAI SDK; used by `src/llm/providers/` as the GPT/OpenAI provider implementation

### `pyproject.toml` — optional-dependencies [dev]

- `pytest`: `>=8.0`
    - Test runner for all Python tests in `tests/` (conftest.py, test_*.py files)
- `pytest-asyncio`: `>=0.23`
    - Async test support for testing async LLM provider calls
- `pytest-cov`: `>=4.1`
    - Coverage reporting plugin for pytest
- `pytest-mock`: `>=3.12`
    - Mocking fixtures for pytest, used to mock LLM provider responses
- `ruff`: `>=0.4`
    - Fast Python linter and formatter (replaces flake8 + isort + black)
- `mypy`: `>=1.10`
    - Static type checker for the `src/llm/` package

---

### `ecc2/Cargo.toml` — dependencies

- `ratatui`: `0.30` (features: crossterm_0_28)
    - Terminal UI framework that renders the ecc2 TUI dashboard and session panels
- `crossterm`: `0.28`
    - Cross-platform terminal manipulation library used as the ratatui backend
- `tokio`: `1` (features: full)
    - Async runtime underpinning all async session management and I/O in ecc2
- `rusqlite`: `0.32` (features: bundled)
    - SQLite bindings (with bundled libsqlite3) for the ecc2 state store
- `git2`: `0.20` (features: ssh)
    - libgit2 bindings for git worktree management and repository operations in ecc2
- `serde`: `1` (features: derive)
    - Serialization/deserialization framework; derive macros used on all config and state structs
- `serde_json`: `1`
    - JSON (de)serialization for MCP server communication and API payloads
- `toml`: `0.8`
    - TOML (de)serialization for reading ECC and project config files
- `regex`: `1`
    - Regular expressions used for path matching and hook condition evaluation
- `sha2`: `0.10`
    - SHA-256 hashing for content-addressable artifact provenance in the state store
- `ureq`: `2` (features: json)
    - Lightweight synchronous HTTP client for MCP server pings, update checks, and API calls
- `clap`: `4` (features: derive)
    - CLI argument parsing for the `ecc-tui` binary entry point
- `tracing`: `0.1`
    - Structured instrumentation (spans and events) throughout the ecc2 codebase
- `tracing-subscriber`: `0.3` (features: env-filter)
    - Collects and formats tracing events; `env-filter` enables `RUST_LOG`-based filtering
- `anyhow`: `1`
    - Ergonomic error propagation with context chaining used across all ecc2 modules
- `thiserror`: `2`
    - Derive macro for typed error enums in ecc2's domain-specific error types
- `libc`: `0.2`
    - Raw OS bindings for low-level signal handling and platform-specific syscalls
- `chrono`: `0.4` (features: serde)
    - Date/time types with serde support for timestamps stored in the SQLite state store
- `cron`: `0.12`
    - Cron expression parsing for scheduled session triggers in the ecc2 control plane
- `uuid`: `1` (features: v4)
    - Generates random UUIDs (v4) for unique session and worktree identifiers
- `dirs`: `6`
    - Detects platform-appropriate config/data/cache directories (XDG on Linux, AppData on Windows)

---

## Taxonomy

- **LLM Providers** (src/llm/ Python library — the abstraction layer over AI APIs)
    - `anthropic`
    - `openai`

- **JSON/Config Validation** (Node.js runtime — validates all ECC configuration at install and run time)
    - `ajv`
    - `@iarna/toml`

- **Persistent State / Storage** (Node.js runtime + Rust ecc2 — both projects use SQLite for state)
    - `sql.js`
    - `rusqlite`

- **Terminal UI** (Rust ecc2 — the TUI dashboard layer)
    - `ratatui`
    - `crossterm`

- **Async Runtime** (Rust ecc2 — all async I/O and concurrency)
    - `tokio`

- **Serialization** (Rust ecc2 — config files, API payloads, state structs)
    - `serde`
    - `serde_json`
    - `toml`

- **Git Integration** (Rust ecc2 — worktree management and repo operations)
    - `git2`

- **CLI & HTTP** (Rust ecc2 — binary entry point and outbound HTTP)
    - `clap`
    - `ureq`

- **Observability & Error Handling** (Rust ecc2 — structured logging and typed errors)
    - `tracing`
    - `tracing-subscriber`
    - `anyhow`
    - `thiserror`

- **Utilities** (Rust ecc2 — time, crypto, IDs, OS paths, patterns, scheduling)
    - `chrono`
    - `cron`
    - `uuid`
    - `dirs`
    - `regex`
    - `sha2`
    - `libc`

- **Linting & Code Quality** (Node.js dev — enforces code and Markdown standards)
    - `eslint`
    - `@eslint/js`
    - `globals`
    - `markdownlint-cli`
    - `ruff`
    - `mypy`

- **Testing & Coverage** (Node.js + Python dev — test infrastructure for both stacks)
    - `c8`
    - `pytest`
    - `pytest-asyncio`
    - `pytest-cov`
    - `pytest-mock`

- **Build & Types** (Node.js dev — TypeScript compilation and type definitions)
    - `typescript`
    - `@types/node`

- **Platform Integration** (Node.js dev — OpenCode AI plugin SDK for the OpenCode adapter)
    - `@opencode-ai/plugin`
