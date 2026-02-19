# agent-skills

A [Claude Code](https://claude.ai/code) plugin marketplace by [Frankenstein AI](https://github.com/frankenstein-ai) — curated skills that extend Claude Code with new capabilities.

## Quick Start

**1. Add the marketplace:**

```
/plugin marketplace add frankenstein-ai/agent-skills
```

**2. Install a plugin:**

```
/plugin install frankenstein-ai/create-flutter-app
```

**3. Use it:**

```
/create-flutter-app my_app
```

## Available Plugins

| Plugin | Description |
|---|---|
| [create-flutter-app](./plugins/create-flutter-app/) | Scaffolds production-ready Flutter apps targeting iOS and Android with sensible defaults |

## Contributing

To add a new skill to this marketplace:

1. Create a directory under `plugins/<skill-name>/`
2. Add a `.claude-plugin/plugin.json` with your plugin metadata
3. Add a `skills/<skill-name>/SKILL.md` defining the skill behavior
4. Register the plugin in `.claude-plugin/marketplace.json`
5. Open a pull request

See [create-flutter-app](./plugins/create-flutter-app/) for a reference implementation.

## Author

[Emerson Macedo](https://github.com/emerleite) — Frankenstein AI

## License

MIT
