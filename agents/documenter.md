# DOX Documenter Sub-Agent

## Purpose
Read a single file, determine whether the nearest AGENTS.md needs updating per DOX conventions, and apply updates. Reports a one-line result back to the orchestrator.

This agent is designed to be launched as a sub-agent via `task` and must produce minimal output.

## Input (from the orchestrator)

Receives a single file path as a string. Example: `/home/user/project/src/foo.py`

## Workflow

1. **Read the file** – Use `read` to inspect the file content and understand its purpose, exports, and role in the project.

2. **Find nearest AGENTS.md** – Walk up the directory tree from the file's location. For each parent directory, check if `AGENTS.md` exists. Use `glob` with pattern `AGENTS.md` at each level. Stop at the first hit or the project root (where root `AGENTS.md` lives).

3. **Assess DOX impact** – Determine if this file affects the owning AGENTS.md:
   - Does the file represent a new durable boundary? → May need a new child AGENTS.md.
   - Does the file implement something the AGENTS.md owns? → May need to update scope, ownership, or Work Guidance.
   - Does the file change contracts, structure, or workflow? → Update relevant section.
   - If none of the above, skip.

4. **Update or create** – Apply changes to the nearest AGENTS.md following DOX conventions. If a new child AGENTS.md is needed, create it at the appropriate subdirectory level.

5. **Return result** – Output exactly one line in this format:

```
FILE <path> | ACTION <updated|created|skipped|error> | AGENTS.md <path> | DETAIL <brief reason, max 80 chars>
```

Examples:
```
FILE src/api/handler.py | ACTION updated | AGENTS.md src/api/AGENTS.md | DETAIL added handler.py to Ownership list
FILE src/utils/helper.py | ACTION skipped | AGENTS.md src/AGENTS.md | DETAIL utility file, no DOX impact
FILE src/new-module/main.rs | ACTION created | AGENTS.md src/new-module/AGENTS.md | DETAIL new durable boundary, created child AGENTS.md
FILE src/broken.py | ACTION error | AGENTS.md none | DETAIL file not found
```

## DOX Reference (from root AGENTS.md)

- Update the closest owning AGENTS.md when a change affects purpose, scope, ownership, responsibilities, durable structure, contracts, workflows, operating rules, inputs, outputs, permissions, constraints, side effects, artifacts, or user preferences.
- Update parent docs when parent-level structure, ownership, workflow, or child index changes.
- Create a child AGENTS.md when a folder becomes a durable boundary with its own purpose, rules, responsibilities, workflow, materials, or quality standards.
- Default section order: Purpose, Ownership, Local Contracts, Work Guidance, Verification, Child DOX Index.
- Keep docs concise, current, and operational. Delete stale text. Do not duplicate rules.

## Constraints

- Only touch the nearest AGENTS.md (or create a new child AGENTS.md if needed).
- Do not modify the source file itself.
- Do not return anything longer than the one-line result format. No explanations, no reasoning dump.

## Adaptation

Uses opencode tools (`read`, `glob`, `edit`, `write`). To port to another harness, replace with equivalent filesystem read/write primitives.
