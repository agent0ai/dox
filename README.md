<p align="center">
  <img src="./banner.jpg" alt="DOX" width="100%">
</p>

## How DOX works

DOX is a tiny AGENTS.md framework that gives an AI agent precise project context.

The agent keeps a hierarchy of AGENTS.md files as the project changes:

- root AGENTS.md contains project-wide instructions and the top-level index
- child AGENTS.md files contain local instructions for specific areas
- before any edit, the agent walks the docs tree from the root to the area it will touch
- the relevant docs give it exact local guidelines, so it does not edit blindly
- after meaningful changes, it updates the affected AGENTS.md files

The result is simple: traverse the docs, understand the local rules, make precise edits, keep the docs current. Less guessing. Less drift. Less "why did it touch that file?"

<p align="center">
  <a href="https://youtu.be/NVkRkioBXQc">
    <img src="./video-thumbnail.jpg" alt="Watch: One markdown file just fixed AI coding forever." width="640">
  </a>
</p>

## How to use

1. Copy the contents of [AGENTS.md](./AGENTS.md?plain=1) into your project's AGENTS.md file.

<br>
That's it. No installation, no dependencies, no package, no runtime. DOX is just a Markdown instruction for AI agents.

It works with any AI agent that supports AGENTS.md files, including Codex, Claude Code, OpenCode, and similar tools.

No AGENTS.md yet? Copy the file into your project root. The agent will see these instructions and will start building the DOX tree.

For an existing project, you can tell your agent: `Initialize DOX tree for this project now.` It will create all the child AGENTS.md files and indexes.

## Credits

<p align="center">
  Created by <strong><a href="https://www.agent-zero.ai/">Agent Zero</a></strong><br>
  Open-source agentic AI framework<br>
  <a href="https://www.agent-zero.ai/">Website</a> · <a href="https://github.com/agent0ai/agent-zero">GitHub repository</a>
</p>

## Usage Examples

To better understand how to implement DOX in your projects, here are a few examples:

### Example 1: Basic Setup
1. Create a new project directory.
2. Copy the contents of [AGENTS.md](./AGENTS.md?plain=1) into your project's AGENTS.md file.
3. Initialize the DOX tree by running `Initialize DOX tree for this project now.`

### Example 2: Updating AGENTS.md
1. After making changes to your project, review the relevant AGENTS.md files.
2. Update the nearest owning AGENTS.md to reflect any changes in responsibilities or scope.
3. Ensure to refresh the Child DOX Index to keep documentation current.

These examples illustrate the straightforward process of using DOX to maintain project documentation effectively.
