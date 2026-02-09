# Skills

A collection of reusable AI agent skills for extending agent capabilities.

## Overview

This repository contains modular skills that can be loaded by AI agents to perform specialized tasks. Each skill is self-contained with its own instructions, scripts, and resources.

## Structure

```
Skills/
├── README.md
├── LICENSE
├── AGENT.md
└── [skill-name]/
    ├── SKILL.md          # Main instruction file (required)
    ├── scripts/          # Helper scripts and utilities
    ├── examples/         # Reference implementations
    └── resources/        # Additional files and templates
```

## Available Skills

### `deep-audit`

**Description:**
A universal, language-agnostic security and robustness scanner designed to detect tech stacks, formulate custom audit plans, and recursively analyze code for bugs and vulnerabilities.

**Features:**
-   **Tech Stack Detection**: Automatically identifies languages and frameworks used in the codebase.
-   **Custom Audit Plan**: Generates a tailored audit strategy based on the detected stack.
-   **Recursive Analysis**: Scans files recursively to identify potential security issues and bugs.
-   **Report Generation**: Produces a comprehensive report of findings.

**Usage:**
This skill is used by AI agents to perform security audits on codebases. The agent loads the skill instructions from `deep-audit/SKILL.md` and executes the defined workflow.

---

*(More skills will be added here)*

## Licensing

> **Note:** Each skill may have its own license. Please refer to the individual skill directories for specific licensing information.

The repository-level LICENSE file provides the default license for shared infrastructure and documentation. Individual skills may override this with their own `LICENSE` file in their respective directories.

## Contributing

Contributions are welcome! When adding a new skill:

1. Create a new directory with your skill name
2. Add a `SKILL.md` file with YAML frontmatter (name, description) and detailed instructions
3. Include any necessary scripts, examples, or resources
4. Optionally add a skill-specific `LICENSE` file if different from the repository default
