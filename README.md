# Ziew Plugins

Official plugin repository for [Ziew](https://ziew.sh).

## Installation

```bash
# Official plugins (short name)
ziew plugin add lua
ziew plugin add llama

# Third-party plugins (user/repo)
ziew plugin add someuser/cool-plugin

# Direct URL
ziew plugin add https://example.com/my-plugin
```

## Available Plugins

### Native Plugins

| Plugin | Description | Status |
|--------|-------------|--------|
| [lua](./lua) | LuaJIT scripting for backend logic | Planned |
| [sqlite](./sqlite) | SQLite database bindings | Planned |

### AI Plugins

| Plugin | Description | Status |
|--------|-------------|--------|
| [llama](./llama) | Local LLM inference via llama.cpp | Planned |
| [whisper](./whisper) | Speech-to-text via whisper.cpp | Planned |

## Style Presets

CSS frameworks are **not plugins** - they're built into the CLI:

```bash
ziew init myapp --style=pico
ziew init myapp --style=tailwind
```

Available styles: `pico`, `water`, `simple`, `mvp`, `tailwind`

## Creating Plugins

Each plugin is a directory containing:

```
my-plugin/
├── plugin.json    # Required: metadata
├── README.md      # Documentation
└── src/           # Zig source files
```

### plugin.json

```json
{
  "name": "my-plugin",
  "version": "1.0.0",
  "type": "native|ai|tool",
  "description": "What this plugin does",
  "status": "stable|beta|planned",
  "requires": {
    "ziew": ">=0.3.0"
  }
}
```

### Plugin Types

| Type | Purpose | Examples |
|------|---------|----------|
| `native` | Zig bindings to C libs | lua, sqlite |
| `ai` | AI model integrations | llama, whisper |
| `tool` | CLI extensions | bundler, hot-reload |

## Third-Party Plugins

Create your own plugin repo with a `plugin.json` at the root:

```bash
# Users install with:
ziew plugin add yourusername/your-plugin
```

## License

MIT
