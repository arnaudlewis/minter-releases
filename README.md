[![Latest Release](https://img.shields.io/github/v/release/arnaudlewis/minter-releases?label=version&color=blue)](https://github.com/arnaudlewis/minter-releases/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/arnaudlewis/minter-releases/total?color=green)](https://github.com/arnaudlewis/minter-releases/releases)
[![Homebrew](https://img.shields.io/badge/homebrew-arnaudlewis%2Ftap%2Fminter-orange)](https://github.com/arnaudlewis/homebrew-tap)
![Platforms](https://img.shields.io/badge/platforms-macOS%20%7C%20Linux%20%7C%20Windows-lightgrey)

# minter

The deterministic validation gate for spec-driven development.

Minter is a CLI that parses `.spec` and `.nfr` files — a structured DSL for defining behavioral contracts and non-functional requirements. It validates syntax and semantics, resolves dependency graphs, cross-validates NFR references, and gives you instant feedback while authoring.

The spec format has exactly one primitive: **behavioral specs that depend on other behavioral specs**. There is no type system — data shapes are specs whose behaviors describe what valid instances look like. There is no error catalog — error behavior is expressed directly as behaviors. Everything is given/when/then. One concept to learn, one concept to validate, one concept to generate tests from.

```
Human intent --> .spec (DSL) --> minter validate (deterministic) --> downstream agents read .spec
```

## Install

```bash
brew install arnaudlewis/tap/minter
```

This installs both `minter` (CLI) and `minter-mcp` (MCP server for AI agents).

## Setup MCP for Claude Code

```bash
claude mcp add minter minter-mcp
```

The MCP server embeds the spec-driven methodology directly into your AI agent's workflow. It includes a built-in authoring guide that teaches agents how to think in behaviors, structure NFR constraints, and follow the one-primitive philosophy — so every spec an agent writes follows the same rigor as one you'd write yourself.

Tools available to the agent: validate, inspect, scaffold, format, graph, initialize project, and methodology guide.

## Getting started

### Build specs with your agent

Once the MCP is set up, your agent already knows the methodology, the DSL grammar, and every validation rule. You don't need to learn the format first — just describe what you want to build.

**Learn the methodology:**

> "Read the minter methodology guide and explain spec-driven development to me."

**Initialize a project:**

> "Initialize a minter spec project in this repo."

**Break down a feature into specs:**

> "I want to build a user authentication system with registration, login, and password reset. Help me break this down into behavioral specs."

**Add non-functional requirements:**

> "Create performance and security NFR files for my project. API responses should be under 200ms and all endpoints need authentication."

**Validate and explore:**

> "Validate all specs in my project and show me the dependency graph."

**Extend an existing spec:**

> "Read the user-auth spec and add edge cases for rate limiting and expired tokens."

The agent handles scaffolding, formatting, cross-reference validation, and dependency resolution through the MCP tools. You focus on what the system should do — the agent handles the DSL.

### CLI reference

For hands-on exploration or CI integration, minter exposes everything through the CLI.

**Methodology and format reference:**

```bash
minter explain           # Full spec-driven development reference
minter format fr         # Complete .spec grammar
minter format nfr        # Complete .nfr grammar
```

**Authoring:**

```bash
minter scaffold fr                    # Generate a .spec template
minter scaffold nfr performance       # Generate an NFR template for a category
```

**Validation and inspection:**

```bash
minter validate specs/                # Validate all specs in a directory
minter validate specs/my-feature.spec # Validate a single file
minter watch specs/                   # Re-validate on every save
minter inspect specs/my-feature.spec  # Show structured metadata
minter graph specs/                   # Display dependency graph
```

## Example

The [`examples/`](examples/) directory contains a complete spec project — a task management API with user authentication, CRUD behaviors, and performance NFR bindings.

```
examples/specs/
├── user-auth.spec           # 4 behaviors — register, login, security NFR anchors
├── task-management.spec     # 5 behaviors — depends on user-auth, whole-file performance NFR
└── nfr/
    ├── performance.nfr      # 3 constraints — response time, throughput, bounded queries
    └── security.nfr         # 2 constraints — password hashing, brute-force protection
```

```bash
minter graph examples/specs/
```

```
task-management v1.0.0 (5 behaviors)
├── user-auth v1.0.0 (4 behaviors)
│   └── [nfr] security v1.0.0 (2 constraints)
│       ├── #brute-force-protection
│       └── #password-hashing
└── [nfr] performance v1.0.0 (3 constraints)
```

See [`examples/README.md`](examples/README.md) for the full walkthrough.

## Supported platforms

| Platform | Target |
|----------|--------|
| macOS ARM64 (Apple Silicon) | `aarch64-apple-darwin` |
| macOS x86_64 (Intel) | `x86_64-apple-darwin` |
| Linux x86_64 | `x86_64-unknown-linux-gnu` |
| Linux ARM64 | `aarch64-unknown-linux-gnu` |
| Windows x86_64 | `x86_64-pc-windows-msvc` |

<details>
<summary>Manual download</summary>

Download the archive for your platform from the [latest release](https://github.com/arnaudlewis/minter-releases/releases/latest), extract it, and place `minter` and `minter-mcp` on your `PATH`.

Each archive contains: `minter`, `minter-mcp`, `LICENSE`, and `README.md`. SHA-256 checksums are in `SHA256SUMS.txt`.

</details>

## Changelog

See [Releases](https://github.com/arnaudlewis/minter-releases/releases) for version history and changelogs.

## License

Proprietary. See [LICENSE](LICENSE) included in each release archive.
