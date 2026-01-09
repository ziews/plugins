# Ziew Plugins

Official plugin repository for [Ziew](https://ziew.sh).

## Installation

```bash
# Add plugins to your project
ziew plugin add sqlite notify steamworks

# List available plugins
ziew plugin list
```

## Available Plugins

### Core Plugins

| Plugin | Description | Dependencies |
|--------|-------------|--------------|
| [sqlite](./sqlite) | SQLite database | libsqlite3-dev |
| [notify](./notify) | System notifications | libnotify-dev |
| [keychain](./keychain) | Secure credential storage | libsecret-1-dev |
| [lua](./lua) | LuaJIT scripting | libluajit-5.1-dev |
| [tray](./tray) | System tray icon | - |
| [menu](./menu) | Native application menus | - |
| [single_instance](./single_instance) | Single app instance | - |

### Input Plugins

| Plugin | Description | Dependencies |
|--------|-------------|--------------|
| [hotkeys](./hotkeys) | Global keyboard shortcuts | libx11-dev |
| [gamepad](./gamepad) | Game controller input | - |
| [serial](./serial) | Serial port communication | - |

### AI Plugins

| Plugin | Description | Dependencies |
|--------|-------------|--------------|
| [llama](./llama) | Local LLM via llama.cpp | llama.cpp |
| [piper](./piper) | Text-to-speech | Piper CLI |

### Platform Plugins

| Plugin | Description | Dependencies |
|--------|-------------|--------------|
| [steamworks](./steamworks) | Steam integration | Steamworks SDK |

## Usage Examples

### SQLite

```zig
const sqlite = @import("ziew").plugins.sqlite;

var db = try sqlite.open("app.db");
defer db.close();

try db.exec("CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)");
```

### Steamworks

```zig
const steam = @import("ziew").plugins.steamworks;

try steam.init();
defer steam.deinit();

try steam.Achievements.unlock("FIRST_WIN");
const name = steam.User.getPersonaName();
```

### Notifications

```zig
const notify = @import("ziew").plugins.notify;

try notify.init("MyApp");
try notify.sendSimple("Hello", "World!");
```

## Creating Plugins

Each plugin is a directory containing:

```
my-plugin/
├── plugin.json    # Required: metadata
├── my-plugin.zig  # Zig source
└── README.md      # Documentation
```

### plugin.json

```json
{
  "name": "my-plugin",
  "version": "0.1.0",
  "type": "native",
  "description": "What this plugin does",
  "status": "stable",
  "requires": {
    "ziew": ">=0.3.0"
  },
  "dependencies": {
    "linux": "libfoo-dev"
  }
}
```

## Third-Party Plugins

Create your own plugin repo:

```bash
# Users install with:
ziew plugin add yourusername/your-plugin
```

## Links

- **Main repo:** [github.com/ziews/ziew](https://github.com/ziews/ziew)
- **Website:** [ziew.sh](https://ziew.sh)
- **Docs:** [ziew.sh/docs](https://ziew.sh/docs)

## License

MIT
