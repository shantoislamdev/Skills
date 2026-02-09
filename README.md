# Skills

A collection of reusable AI agent skills for extending agent capabilities.

## Overview

This repository contains modular skills that can be loaded by AI agents to perform specialized tasks. Each skill is self-contained with its own instructions, scripts, and resources.

## Structure

```
Skills/
├── README.md
├── LICENSE
├── agents.md
└── [skill-name]/
    ├── SKILL.md          # Main instruction file (required)
    ├── scripts/          # Helper scripts and utilities
    ├── examples/         # Reference implementations
    └── resources/        # Additional files and templates
```

## Available Skills

| Skill | Description |
|-------|-------------|
| `deep-audit` | Security and robustness scanner for codebases |

## Usage

Skills are automatically discovered and loaded by compatible AI agents. To use a skill, simply reference it in your agent configuration or invoke it during a conversation.

## Licensing

> **Note:** Each skill may have its own license. Please refer to the individual skill directories for specific licensing information.

The repository-level LICENSE file provides the default license for shared infrastructure and documentation. Individual skills may override this with their own `LICENSE` file in their respective directories.

## Contributing

Contributions are welcome! When adding a new skill:

1. Create a new directory with your skill name
2. Add a `SKILL.md` file with YAML frontmatter (name, description) and detailed instructions
3. Include any necessary scripts, examples, or resources
4. Optionally add a skill-specific `LICENSE` file if different from the repository default
