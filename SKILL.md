---
name: dox-init
description: Initialize the DOX tree (self-documenting AGENTS.md hierarchy) in the current project. Use when the user says "init dox", "initialize DOX", "set up DOX tree", "/dox", "dox this project", or wants a new project to start with DOX. One command replaces pasting the agent0ai/dox link. DOX itself is NOT created by this skill - full credit to Agent Zero.
---

# dox-init

Initialize the DOX tree for the current project. DOX is a hierarchical AGENTS.md framework by Agent Zero - this skill is only a bootstrapper that installs it and builds the tree. Not our creation.

## Steps

### 1. Install root AGENTS.md

Fetch the official DOX contract and write it to the project root:

```bash
curl -fsSL https://raw.githubusercontent.com/agent0ai/dox/main/AGENTS.md -o AGENTS.md
```

If `AGENTS.md` already exists and contains `# DOX framework`, keep it (do not overwrite user customizations). If it exists without DOX, back it up to `AGENTS.md.bak` first, then fetch.

### 2. Scan the project

Recursively list the real structure - source dirs, configs, docs, assets, tests. Ignore `node_modules`, `.git`, `dist`, `build`, `venv`, `.venv`, `__pycache__`, `coverage`, lockfiles.

### 3. Build the tree

For each folder that is a durable boundary (own purpose, rules, workflow, or responsibility), create a child `AGENTS.md` nested at that level. Do not create files for trivial or empty folders.

Default section order in every child file:

```
## Purpose
## Ownership
## Local Contracts
## Work Guidance
## Verification
## Child DOX Index
```

Rules:
- Parent indexes list direct children with one line each: path + what it covers
- Broader rules live in parents, concrete details in children
- Leave Work Guidance / Verification empty if no standards or checks exist yet - update later, never invent
- No duplication across files unless each scope needs a local version
- Deep nesting only where complexity warrants it - prefer shallow

### 4. Fill root Child DOX Index

Replace the placeholder line `This project is not yet indexed...` in root `AGENTS.md` with the actual top-level index of child AGENTS.md files.

### 5. Report

List every AGENTS.md created (path + scope) and any folders intentionally skipped. Done - future edits in this project will walk this tree.

## Attribution

DOX by [Agent Zero](https://www.agent-zero.ai/) - [agent0ai/dox](https://github.com/agent0ai/dox), MIT. This skill only automates initialization.
