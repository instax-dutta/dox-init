---
name: dox-init
description: Initialize the DOX tree (self-documenting AGENTS.md hierarchy) in the current project. Use when the user says "init dox", "initialize DOX", "set up DOX tree", "/dox", "dox this project", or wants a new project to start with DOX. One command replaces pasting the agent0ai/dox link. DOX itself is NOT created by this skill - full credit to Agent Zero.
---

# dox-init

Initialize the DOX tree for the current project. DOX is a hierarchical AGENTS.md framework by Agent Zero - this skill is only a bootstrapper that installs it and builds the tree. Not our creation.

Existing instructions always win. An `AGENTS.md` the user already wrote is not replaced, renamed or overwritten without being read first and without explicit approval. The upstream template is reference material, not authority: it never overrides a rule already in the repository.

## Steps

### 1. Inspect existing instructions

Verify the intended repository root, then list the `AGENTS.md` files in scope and read each one before deciding whether it needs an edit.

- Root already contains the DOX marker (`# DOX framework`): report that the tree is installed and preserve it. Do not fetch, do not overwrite.
- Root exists without the marker: keep its existing rules and propose a merge into the DOX structure. Ask before replacing or removing any existing rule.
- No root file: continue to step 2.

### 2. Stage and review the upstream template

Fetch Agent Zero's template from the pinned revision to a unique temporary file **outside** the repository, and inspect it as reference:

```bash
curl -fsSL https://raw.githubusercontent.com/agent0ai/dox/765ae4ac02cc884eefcd41a3d0f71941721adb89/AGENTS.md -o "$TMPDIR/dox-AGENTS.md"
```

If the download fails, discard the temporary file and stop. Never write a partial or truncated contract into the project.

Before writing anything, show the user the proposed file list and every change to an existing rule. Back up each existing file that will change to a unique recovery path. Apply merged content only after the user authorizes changes to existing rules; a fresh root file starts from the reviewed template with the repository-specific index filled in.

### 3. Scan the project

Recursively list the real structure - source dirs, configs, docs, assets, tests. Ignore `node_modules`, `.git`, `dist`, `build`, `venv`, `.venv`, `__pycache__`, `coverage`, lockfiles.

### 4. Build the tree

For each folder that is a durable boundary (own purpose, rules, workflow, or responsibility), create a child `AGENTS.md` nested at that level. Do not create files for trivial or empty folders. Retain existing child rules when adapting a file, and verify the file is inside the intended repository before writing.

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

### 5. Fill root Child DOX Index

Replace the placeholder line `This project is not yet indexed...` in root `AGENTS.md` with the actual top-level index of child AGENTS.md files.

### 6. Report

List every AGENTS.md created (path + scope), every existing file edited with the location of its recovery copy, and any folders intentionally skipped. Done - future edits in this project will walk this tree.

## Attribution

DOX by [Agent Zero](https://www.agent-zero.ai/) - [agent0ai/dox](https://github.com/agent0ai/dox), MIT. This skill only automates initialization.
