# minter

The deterministic validation gate for spec-driven development.

Minter parses a custom `.spec` DSL that defines behavioral contracts (given/when/then) and a `.nfr` DSL that defines non-functional requirements as measurable constraints. It enforces semantic rules, resolves dependency graphs, cross-validates NFR references, and provides watch mode for instant feedback during authoring.

```
Human intent --> .spec (DSL) --> minter validate (deterministic) --> downstream agents read .spec
```

## Install

### Homebrew (macOS and Linux)

```bash
brew install arnaudlewis/tap/minter
```

This installs both `minter` (CLI) and `minter-mcp` (MCP server).

### Shell (Linux)

```bash
curl -fsSL https://github.com/arnaudlewis/minter-releases/releases/latest/download/minter-$(curl -fsSL https://api.github.com/repos/arnaudlewis/minter-releases/releases/latest | grep -o '"tag_name":"[^"]*"' | cut -d'"' -f4)-$(uname -m | sed 's/x86_64/x86_64-unknown-linux-gnu/' | sed 's/aarch64/aarch64-unknown-linux-gnu/').tar.gz | tar xz -C /tmp && sudo install /tmp/minter /tmp/minter-mcp /usr/local/bin/
```

Or step by step:

```bash
# 1. Pick your architecture
ARCH=$(uname -m)  # x86_64 or aarch64

# 2. Get the latest version tag
TAG=$(curl -fsSL https://api.github.com/repos/arnaudlewis/minter-releases/releases/latest | grep -o '"tag_name":"[^"]*"' | cut -d'"' -f4)

# 3. Map to Rust target
case "$ARCH" in
  x86_64)  TARGET="x86_64-unknown-linux-gnu" ;;
  aarch64) TARGET="aarch64-unknown-linux-gnu" ;;
esac

# 4. Download and extract
curl -fsSL "https://github.com/arnaudlewis/minter-releases/releases/download/${TAG}/minter-${TAG}-${TARGET}.tar.gz" | tar xz -C /tmp

# 5. Install
sudo install /tmp/minter /tmp/minter-mcp /usr/local/bin/
```

### Manual download

Download the archive for your platform from the [latest release](https://github.com/arnaudlewis/minter-releases/releases/latest), extract it, and place `minter` and `minter-mcp` on your `PATH`.

### Verify

```bash
minter --version
```

## Supported platforms

| Platform | Target | Archive |
|----------|--------|---------|
| macOS ARM64 (Apple Silicon) | `aarch64-apple-darwin` | `.tar.gz` |
| macOS x86_64 (Intel) | `x86_64-apple-darwin` | `.tar.gz` |
| Linux x86_64 | `x86_64-unknown-linux-gnu` | `.tar.gz` |
| Linux ARM64 | `aarch64-unknown-linux-gnu` | `.tar.gz` |
| Windows x86_64 | `x86_64-pc-windows-msvc` | `.zip` |

Each archive contains: `minter`, `minter-mcp`, `LICENSE`, and `README.md`.

SHA-256 checksums are published alongside every release in `SHA256SUMS.txt`.

## What's included

| Binary | Description |
|--------|-------------|
| `minter` | CLI tool — validate, watch, format, scaffold, inspect, explain, graph |
| `minter-mcp` | [MCP](https://modelcontextprotocol.io/) server for AI agent and IDE integration |

### MCP configuration

Add to your Claude Desktop, Cursor, or other MCP-compatible tool:

```jsonc
{
  "mcpServers": {
    "minter": {
      "command": "minter-mcp"
    }
  }
}
```

## Quick start

```bash
# Scaffold a spec
minter scaffold spec > specs/my-feature.spec

# Validate it
minter validate specs/my-feature.spec

# Watch for changes
minter watch specs/

# Explore the dependency graph
minter graph specs/
```

Run `minter --help` for full command reference.

## License

Proprietary. See [LICENSE](LICENSE) included in each release archive.
