# Skills Repository Instructions

This `AGENT.md` file provides context and instructions for AI agents interacting with this repository.

## Repository Overview

This repository contains a collection of **Skills**—modular capabilities that extend the functionality of AI agents. Each directory at the root (excluding standard repo files like `README.md` and `LICENSE`) represents a distinct skill.

## Skill Structure

Each skill directory follows a consistent structure:

-   `SKILL.md`: The primary instruction file. **Always read this first** to understand the skill's purpose, usage, and available commands. It contains YAML frontmatter with metadata and markdown content with detailed instructions.
-   `scripts/`: Contains executable scripts or utilities helper functions.
-   `examples/`: Provides reference implementations.
-   `resources/`: Stores additional assets or templates.

## Instructions for Agents

When a user requests a specific capability or task that matches a skill in this repository:

1.  **Locate the Skill**: Find the directory matching the requested skill name.
2.  **Read Instructions**: Read the `SKILL.md` file within that directory to understand the skill's capabilities and usage.
3.  **Check License**: **CRITICAL**: Check for a `LICENSE` file within the *specific skill directory*.
    -   If a skill-specific `LICENSE` exists, it overrides the root `LICENSE`.
    -   If no skill-specific `LICENSE` exists, the root `LICENSE` applies.
    -   **Always respect the terms of the active license.**
4.  **Execute**: Follow the instructions in `SKILL.md` to perform the task.

## New Skill Creation

If the user asks you to create a new skill:

1.  Create a new directory with a descriptive, kebab-case name.
2.  Create a `SKILL.md` file with:
    -   YAML frontmatter (`name`, `description`).
    -   Clear, step-by-step markdown instructions for the agent.
3.  Add a skill-specific `LICENSE` if necessary.
4.  Populate `scripts/`, `examples/`, and `resources/` as needed.
