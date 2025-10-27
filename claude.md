# Codex CLI Project - Overview Notes

## Project Type
**Codex CLI** - AI-powered coding agent from OpenAI that runs locally on your computer.
- Repository: https://github.com/openai/codex
- License: Apache-2.0
- Classification: CLI Tool / Agent Framework / Developer Productivity Tool

## Primary Programming Languages
1. **Rust** (70-80% of codebase) - Main implementation
   - CLI, TUI, core business logic
   - Sandboxing and execution engines
   - Native compilation for performance

2. **TypeScript/JavaScript** (15-25%) - SDK and tooling
   - TypeScript SDK for programmatic access
   - Legacy CLI wrapper (superseded by Rust)
   - Documentation tooling

3. **Markdown** - Comprehensive documentation

## Key Technologies & Frameworks

### Rust Stack
- **Tokio** - Async runtime
- **Ratatui 0.29.0** - Terminal UI (TUI) rendering
- **Axum 0.8** - Web framework for HTTP servers
- **Tonic** - gRPC framework
- **Serde** - Serialization/deserialization
- **Reqwest** - HTTP client
- **Tree-sitter** - Code parsing and syntax highlighting

### Security & Sandboxing
- **Landlock** (Linux) - File access control
- **Seatbelt** (macOS) - Apple's sandboxing framework
- **Seccompiler** - Seccomp filter compilation

### AI Integration
- **Model Context Protocol (MCP)** - Communication with AI services
- **OpenAI API** - Chat completions integration
- **RMCP 0.8.3** - MCP implementation

### Development Tools
- **Cargo** - Rust package manager (workspace of 37 crates)
- **pnpm 10.8.1+** - Node.js package manager
- **Just** - Build automation
- **Insta** - Snapshot testing
- Rust 1.90.0, Node.js 22+

## Project Structure

```
/workspaces/codex_agents/
├── codex-rs/           # Main Rust implementation (37 crates)
│   ├── cli/            # CLI entry point
│   ├── tui/            # Terminal UI application
│   ├── core/           # Business logic & agent framework
│   ├── exec/           # Headless CLI
│   ├── app-server/     # HTTP server for IDE integrations
│   ├── mcp-server/     # MCP server
│   ├── backend-client/ # OpenAI API client
│   ├── linux-sandbox/  # Linux sandboxing
│   └── ...             # 29+ other crates
├── codex-cli/          # Legacy TypeScript CLI wrapper
├── sdk/typescript/     # TypeScript SDK
├── docs/               # Documentation
└── scripts/            # Build and deployment scripts
```

## What It Does

**Core Purpose**: AI-powered coding assistant that helps developers:

1. **Code Generation & Modification**
   - Generate code from natural language
   - Refactor existing code
   - Write unit tests automatically
   - Generate migrations and boilerplate

2. **Code Execution & Iteration**
   - Execute code in isolated sandbox
   - Run tests and see results immediately
   - Iterate on fixes based on failures
   - Apply patches to files

3. **Intelligent Problem Solving**
   - Diagnose test failures
   - Review code for security vulnerabilities
   - Analyze and explain complex code
   - Suggest improvements

4. **Developer Experience**
   - Interactive TUI with real-time feedback
   - Non-interactive mode for CI/CD
   - Multi-image support
   - File patching with approval workflow
   - Session persistence

5. **Security & Safety**
   - Network-disabled sandboxing (read-only by default)
   - Platform-specific isolation
   - Approval modes: Suggest, Auto-Edit, Full-Auto
   - Configuration-driven sandbox policies

## Build System

### Rust (Primary)
- **Cargo workspace** with 37 interconnected crates
- **Just** for build automation (`justfile`)
- Profile optimization: LTO enabled, symbol stripping
- Rust 2024 edition

### TypeScript
- **pnpm workspace** monorepo
- Jest/Vitest for testing
- ESLint + Prettier for code quality

### CI/CD
- GitHub Actions (ci.yml, rust-ci.yml, rust-release.yml)
- Cross-platform binary releases
- Automated testing and linting

## Platform Support
- **macOS 12+** (Apple Seatbelt sandboxing)
- **Linux** (Landlock sandboxing / Docker)
- **Windows** (via WSL2)

## Distribution
- Single cross-platform binary (`codex`)
- npm package wrapper (`@openai/codex`)
- TypeScript SDK (`@openai/codex-sdk`)
- Homebrew cask
- GitHub releases

## Key Architectural Patterns
- Modular Rust workspace with shared core
- TUI-based primary interface (Ratatui)
- HTTP server for IDE integrations
- Streaming event-based communication
- Protocol buffers + JSON serialization
- Async/await throughout
- Model Context Protocol (MCP) for AI integration

## Development Environment
- **Nix Flake** (`flake.nix`) - Reproducible dev environment
- **Docker** - Container support
- **VSCode DevContainer** - Codespaces compatibility
- **Sentry** - Error tracking and monitoring

---

**Last Updated**: 2025-10-27
**Status**: Active open-source project with commercial backing
