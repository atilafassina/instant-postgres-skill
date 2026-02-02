# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository is for creating a Claude Code skill called "instant-postgres". Skills are modular packages that extend Claude's capabilities with specialized knowledge, workflows, and tools.

## Skill Structure

A skill requires:
- `SKILL.md` - Main skill file with YAML frontmatter (`name`, `description`) and markdown instructions
- Optional: `scripts/`, `references/`, `assets/` directories for bundled resources

## Development Workflow

The skill-creator guide is located at `.claude/skills/creator.md`. Follow its six-step process:
1. Understand the skill with concrete examples
2. Plan reusable contents (scripts, references, assets)
3. Initialize the skill structure
4. Edit SKILL.md and implement resources
5. Package with validation
6. Iterate based on usage

## Key Constraints

- Keep SKILL.md under 500 lines
- Use progressive disclosure: core workflow in SKILL.md, details in reference files
- Only include files essential for the skill's functionality
- Test any scripts by running them before packaging
