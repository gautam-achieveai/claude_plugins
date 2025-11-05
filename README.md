# Claude Plugins Marketplace

A curated marketplace of plugins for Claude Code, making it easy to discover, install, and manage extensions.

## What is this?

This repository serves as a plugin marketplace for Claude Code. It provides a catalog of available plugins that extend Claude's capabilities with custom commands, skills, agents, and tool integrations.

## Quick Start

### Using this Marketplace

To use plugins from this marketplace:

1. Add the marketplace to Claude Code:
   ```
   /plugin marketplace add yourusername/claude-plugins
   ```

2. Browse available plugins:
   ```
   /plugin
   ```

3. Install a plugin:
   ```
   /plugin install example-plugin
   ```

## Available Plugins

- **example-plugin**: A template plugin demonstrating basic structure and capabilities
  - Custom `/hello` command
  - Context-aware greeting skill

## Repository Structure

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json       # Marketplace catalog
├── plugins/
│   └── example-plugin/        # Example plugin
│       ├── .claude-plugin/
│       │   └── plugin.json    # Plugin manifest
│       ├── commands/          # Custom slash commands
│       ├── skills/            # Agent skills
│       └── README.md
├── scratchpad/                # Research and development notes
└── README.md                  # This file
```

## Creating Your Own Plugin

### Plugin Structure

Each plugin should follow this structure:

```
your-plugin/
├── .claude-plugin/
│   └── plugin.json            # Required: Plugin metadata
├── commands/                  # Optional: Custom slash commands
│   └── command-name.md
├── skills/                    # Optional: Agent skills
│   └── skill-name/
│       └── SKILL.md
├── agents/                    # Optional: Custom agents
├── hooks/                     # Optional: Event handlers
│   └── hooks.json
└── README.md                  # Recommended: Documentation
```

### plugin.json Schema

```json
{
  "name": "your-plugin-name",
  "description": "Brief description of your plugin",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "your.email@example.com"
  },
  "homepage": "https://github.com/yourusername/your-plugin",
  "license": "MIT",
  "keywords": ["keyword1", "keyword2"],
  "commands": {
    "command-name": "commands/command-name.md"
  },
  "skills": {
    "skill-name": "skills/skill-name/SKILL.md"
  }
}
```

### Adding to Marketplace

1. Create your plugin in the `plugins/` directory
2. Add an entry to `.claude-plugin/marketplace.json`:

```json
{
  "name": "your-plugin-name",
  "source": "./plugins/your-plugin",
  "description": "Your plugin description",
  "version": "1.0.0",
  "category": "utilities",
  "tags": ["tag1", "tag2"],
  "keywords": ["keyword1", "keyword2"]
}
```

## Plugin Categories

Organize your plugins using these categories:

- **utilities**: General-purpose tools and helpers
- **development**: Development workflow enhancements
- **productivity**: Productivity and automation tools
- **integration**: External service integrations
- **ai**: AI and LLM-related capabilities
- **data**: Data processing and analysis tools

## Resources

- [Official Plugin Documentation](https://docs.claude.com/en/docs/claude-code/plugins)
- [Marketplace Documentation](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)
- [Claude Code Plugins Announcement](https://www.anthropic.com/news/claude-code-plugins)
- [Model Context Protocol (MCP)](https://www.anthropic.com/news/model-context-protocol)

## Contributing

1. Fork this repository
2. Create your plugin in the `plugins/` directory
3. Add your plugin to `.claude-plugin/marketplace.json`
4. Submit a pull request with:
   - Plugin code and documentation
   - Entry in marketplace.json
   - Brief description of functionality

## Support

For issues or questions:

- Check the [official documentation](https://docs.claude.com/en/docs/claude-code/plugins)
- Review the example plugin for reference
- Open an issue in this repository

## License

This marketplace is MIT licensed. Individual plugins may have their own licenses.
