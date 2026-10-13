# Book Agent Generator (`book-agent`)

> **Language**
> **English Version** (this page) / **[日本語版 README](README.md)**

> [!Warning]
> This is a test version and is subject to major changes.

**Related Article**
**[Instantly Power Up Your Tech Book Knowledge! The Shortest Workflow from Sub Agent Creation to Design Support and Reviews](https://zenn.dev/furedea/articles/53b5117b389454)** - Zenn Article (Japanese)

# Overview

A custom slash command for Claude Code that interactively generates Sub Agent definition files from your notes on technical books and articles.

## Features

- 🧠 **Knowledge Analysis & Structuring**: Analyzes the provided text (e.g., technical book highlights, article notes) to automatically generate a structured knowledge base with sections like "Core Principles," "Key Techniques," and "Anti-patterns."
- 🤖 **Automatic Sub Agent Generation**: Creates a complete Sub Agent definition file (`.md`) with the proper frontmatter (`name`, `description`, etc.) that Claude Code can recognize directly.
- 🗣️ **Interactive Generation Process**: Presents the generated agent name and content as a draft, allowing for user approval or modification requests to finalize the definition file interactively. (Supports `-y` flag for auto-approval).
- 📁 **Automatic File Management**: Automatically avoids filename conflicts and safely saves the file to the specified directory (`./.claude/agents/book-agent/`).

## Installation & Setup

1.  Clone or download this repository.
2.  Copy the entire `.claude/commands/book-agent/` directory from this repository into your project's `.claude/commands/` directory.

```
    <your-project>
    └── .claude/
        └── commands/
            └── book-agent/      <-- Place it here
                └── book2agent.md
```
    
3.  (Recommended) For a smoother workflow, consider setting up Obsidian with plugins like Kindle Highlights and MCP Tools by following the [Zenn article](https://zenn.dev/furedea/articles/53b5117b389454).

## Usage

This command is designed to be used by linking a knowledge source (technical book highlights, article notes, etc.) aggregated in [Obsidian](https://obsidian.md/) with Claude Code.

### Basic Workflow

1.  **Prepare Knowledge**: Use Obsidian plugins like `Kindle Highlights` or `Web Clipper` to gather the technical resources you want to turn into a Sub Agent into an Obsidian note.
2.  **Link Context**: Use the `MCP Tools` plugin in Obsidian to load the content of the target note as context in Claude Code.
3.  **Run Command**: With the context loaded, run the `/book-agent:book2agent` command to generate the Sub Agent interactively.

### Command Examples

#### 1. Obsidian + MCP Integration (Recommended)

1.  Connect to Obsidian and load the active note into the context using the /mcp command.
>
> /mcp

2.  Run the command without arguments.
>
> /book-agent:book2agent {path_to_obsidian_note}

---

#### 2. File Input

You can also export an Obsidian note as a Markdown file and have the command read it directly.
>
> /book-agent:book2agent {path_to_file}

---

#### 3. Auto-Approval Mode

Use the `-y` flag if you want to skip the interactive confirmation steps and run the generation process automatically from start to finish.
>
> /book-agent:book2agent -y {path_to_file}

## License

This project is licensed under the [MIT License](LICENSE).

## Contributing

Bug reports and feature suggestions are welcome via Issues and Pull Requests.
