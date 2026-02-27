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

Once installed, add minter to your Claude Code configuration:

```bash
claude mcp add minter minter-mcp
```

This gives Claude access to minter's tools: validate, inspect, scaffold, format, graph, and a built-in authoring guide. Claude can then validate specs inline, scaffold new files, and explore your dependency graph without leaving the conversation.

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

## License

Proprietary. See [LICENSE](LICENSE) included in each release archive.
