# onboard-guide

**English** | [한국어](README.ko.md)

A Claude Code plugin that analyzes the repository you are in and generates an **interactive onboarding page** for new team members: one `onboarding.html` file that tells them where to start reading and in what order.

This repository is also the `jacob-plugins` plugin marketplace that distributes it.

## Install

In Claude Code:

```
/plugin marketplace add Jacob-9909/onboard-guide
/plugin install onboard-guide@jacob-plugins
```

Restart Claude Code to load the plugin.

## Usage

1. Start Claude Code at the **root of the repository** you want to document.
2. Run the `onboarding` skill (`onboard-guide:onboarding`).
3. Open the generated `onboarding.html` at the repository root in a browser.

To focus on one part of the codebase, pass a subdirectory path or topic as an argument.

## What the Page Contains

| Section | Content |
|---|---|
| KPI strip | File count, lines of code, main languages, layers, dependencies, estimated learning time |
| Overview | Architecture and layers, design philosophy, core data flow, extension points, external dependencies |
| Workflow graph (SVG) | User → API → core → transport → external libraries. Click a node to jump to its module |
| Directory tree | Collapsible sidebar with a role for each entry, linked to key files |
| Pipeline diagram | Execution flow as steps. Click a step for file path, key functions, reading tips, and next-step code |
| Module cards | Functions to read first, real code snippets with notes, read/skip guide, difficulty, internal vs external dependencies |
| Reading order | Numbered learning path with the reason for each step |
| Search | Filter the tree and module cards by keyword |

Every file path, function name, and line number comes from the actual code, and the skill checks them with `ls`/`grep` after generating the page. The page is plain HTML/CSS/JS with no external CDN, so it also opens on internal networks.

## Repository Layout

```
onboard-guide/                    # marketplace root
├── .claude-plugin/
│   └── marketplace.json          # marketplace catalog
└── plugins/
    └── onboard-guide/            # the plugin
        ├── .claude-plugin/plugin.json
        ├── skills/onboarding/SKILL.md
        └── README.md
```

## Releasing an Update

Bump `version` in `plugins/onboard-guide/.claude-plugin/plugin.json` and push. Users get the new version with `/plugin marketplace update`.

For local development, register the folder directly: `/plugin marketplace add /path/to/onboard-guide`.
