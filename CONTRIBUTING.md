# Contributing to Claude Plugins Marketplace

Thank you for your interest in contributing! This document provides guidelines for adding plugins to this marketplace.

## Getting Started

1. Fork this repository
2. Clone your fork locally
3. Create a new branch for your plugin: `git checkout -b add-your-plugin-name`

## Plugin Requirements

### Quality Standards

Your plugin should:

- Have clear, concise documentation
- Follow the official plugin structure
- Include a well-formed `plugin.json` manifest
- Provide useful functionality that extends Claude Code
- Be tested and working

### Required Files

- `.claude-plugin/plugin.json`: Plugin manifest with metadata
- `README.md`: Clear documentation explaining functionality and usage
- Component files (commands, skills, agents, etc.) as declared in plugin.json

### plugin.json Template

```json
{
  "name": "your-plugin-name",
  "description": "Clear, concise description of what your plugin does",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "your.email@example.com"
  },
  "homepage": "https://github.com/yourusername/your-plugin",
  "repository": {
    "type": "git",
    "url": "https://github.com/yourusername/your-plugin.git"
  },
  "license": "MIT",
  "keywords": ["relevant", "keywords"]
}
```

## Submission Process

### 1. Add Your Plugin

Place your plugin in the `plugins/` directory:

```
plugins/
└── your-plugin-name/
    ├── .claude-plugin/
    │   └── plugin.json
    ├── commands/          # If applicable
    ├── skills/            # If applicable
    ├── agents/            # If applicable
    ├── hooks/             # If applicable
    └── README.md
```

### 2. Update Marketplace Catalog

Add an entry to `.claude-plugin/marketplace.json`:

```json
{
  "name": "your-plugin-name",
  "source": "./plugins/your-plugin-name",
  "description": "Brief description",
  "version": "1.0.0",
  "category": "appropriate-category",
  "tags": ["tag1", "tag2"],
  "keywords": ["keyword1", "keyword2"],
  "author": {
    "name": "Your Name"
  },
  "homepage": "https://github.com/yourusername/your-plugin",
  "license": "MIT"
}
```

### 3. Create Pull Request

Submit a PR with:

- **Title**: "Add [plugin-name] plugin"
- **Description**:
  - What your plugin does
  - Why it's useful
  - Any dependencies or requirements
  - Link to documentation or examples

**PR Template:**

```markdown
## Plugin Information

**Name**: your-plugin-name
**Category**: utilities
**Description**: Brief description of functionality

## Checklist

- [ ] Plugin has valid `plugin.json` manifest
- [ ] README.md included with usage instructions
- [ ] Entry added to `.claude-plugin/marketplace.json`
- [ ] All component files are present and valid
- [ ] Plugin tested and working
- [ ] Documentation is clear and complete
- [ ] No sensitive data or credentials included

## Additional Notes

[Any special considerations, dependencies, or setup requirements]
```

## Plugin Categories

Choose the most appropriate category:

- **utilities**: General-purpose tools and helpers
- **development**: Development workflow enhancements
- **productivity**: Productivity and automation
- **integration**: External service integrations
- **ai**: AI and LLM-related capabilities
- **data**: Data processing and analysis

## Best Practices

### Documentation

- Write clear, comprehensive README files
- Include usage examples
- Document any configuration options
- List prerequisites or dependencies

### Code Quality

- Follow consistent formatting
- Use clear, descriptive names
- Comment complex logic
- Test thoroughly before submitting

### Security

- Never include credentials, API keys, or secrets
- Validate and sanitize user inputs
- Follow security best practices for external integrations
- Clearly document any security considerations

### Naming Conventions

- Use kebab-case for plugin names: `my-awesome-plugin`
- Use descriptive, meaningful names
- Avoid overly generic names
- Keep names concise but clear

## Review Process

After submission:

1. Maintainers will review your PR
2. May request changes or clarifications
3. Once approved, your plugin will be merged
4. Your plugin becomes available in the marketplace

## Questions?

- Review the [example plugin](./plugins/example-plugin)
- Check the [official documentation](https://docs.claude.com/en/docs/claude-code/plugins)
- Open an issue for questions or support

## License

By contributing, you agree that your plugin will be licensed under the terms you specify in your plugin's manifest, and your contribution to the marketplace catalog is licensed under MIT.
