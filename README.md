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

**1. Learn the methodology**

```bash
minter explain
```

This prints the full spec-driven development reference — what behaviors are, how NFR categories work, cross-reference binding, override rules, and how specs map to tests.

**2. Explore the file formats**

```bash
minter format spec
minter format nfr
```

These print the complete grammar for each DSL format. Everything you need to author valid files.

**3. Scaffold your first spec**

```bash
minter scaffold spec > specs/my-feature.spec
```

Open the generated file — it's a ready-to-edit template with an example behavior.

**4. Validate it**

```bash
minter validate specs/my-feature.spec
```

```
✓ my-feature v0.1.0 (1 behavior)
```

**5. Watch for changes**

```bash
minter watch specs/
```

Minter re-validates on every save with colored output. Press `Ctrl+C` to stop.

**6. Explore the dependency graph**

```bash
minter graph specs/
```

```
3 specs, 11 behaviors, 2 NFR categories, 5 constraints

checkout v1.0.0 (4 behaviors)
├── payment v2.1.0 (7 behaviors)
│   └── user-auth v1.0.0 (3 behaviors)
└── [nfr] performance v1.0.0 (2 constraints)
    ├── #api-response-time
    └── #db-query-time
```

**All commands**

```bash
minter --help
```

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
