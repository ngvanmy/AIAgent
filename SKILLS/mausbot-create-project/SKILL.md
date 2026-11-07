---
name: mausbot-create-project
description: Create a new Mausbot project with plan.md, architecture.md, requirements.md, tasks/, reports/. Use when the user wants to create a project or initialize project documentation.
---

# Mausbot Create Project

When creating a new project:
1. Register the project in the central Project Registry: `E:\MausBot\project-registry.json` (authoritative registry location for the entire workspace).
2. Set `documentation_path` to `E:\MausBot\projects\{project-id}\`.
3. Set `repository.local_path` to the local source repository path (e.g. `D:\ERP`).
4. Set `worktree_root` to `E:\MausBot\worktrees\{project-id}\`.
5. Set `codegraph_path` to the repository root where CodeGraph is indexed.
6. Create directory `E:\MausBot\projects\{project-id}\`.
7. Create plan.md, architecture.md, requirements.md in `E:\MausBot\projects\{project-id}\`.
8. Create tasks/ and reports/ directories under `E:\MausBot\projects\{project-id}\`.
9. Generate TASK-01.md template in tasks/.
10. Link plan.md to tasks.
11. Register project documentation for Brain ingestion.

Do NOT create duplicate `project-registry.json` files inside project directories.
