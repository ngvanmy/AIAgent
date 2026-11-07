---
name: mausbot-task-management
description: Mandatory task lifecycle management for Mausbot. Use whenever Coordinator creates, plans, decomposes, approves, assigns, executes, reviews, updates, or completes a task. Ensures Plane synchronization, Markdown documentation, Brain indexing, Git worktree allocation, and task traceability.
---

# Mausbot Task Management

## 1. Purpose

Manage every Mausbot Task consistently across:

- Project Registry
- Plane Cloud
- Markdown documentation
- Mausbot Brain
- Git Worktree
- OpenCode execution
- Reviewer verification

This Skill is mandatory for every project task.

## 2. Task Creation Rules

Whenever Coordinator creates a new task:

MANDATORY:
1. Resolve the Project ID.
2. Read the central Project Registry: `E:\MausBot\project-registry.json` (do NOT look for registry inside individual project folders).
3. Resolve individual project documents using `E:\MausBot\projects\{project-id}\`.
4. Resolve source repository from `repository.local_path` in `E:\MausBot\project-registry.json`.
5. Resolve worktree using `E:\MausBot\worktrees\{project-id}\` (or `worktree_root` in registry).
6. Resolve CodeGraph path from `codegraph_path` in `E:\MausBot\project-registry.json`.
7. Generate a unique Task ID.
8. Create a separate Markdown file under `E:\MausBot\projects\{project-id}\tasks\{TASK-ID}.md`.
9. Add the Task to `E:\MausBot\projects\{project-id}\plan.md`.
10. Record dependencies.
11. Search Brain for relevant documents.
12. Record CodeGraph investigation when applicable.
13. Create or map the Plane Work Item.
14. Register the Markdown document in Brain.

Never create a task without a corresponding Markdown file.

## 3. Task Storage

Root:

E:\MausBot\projects\{project-id}\tasks\

Filename:

{TASK-ID}.md

Example:

E:\MausBot\projects\WEB-ANNOUNCEMENT\tasks\TASK-001.md

Use UTF-8 encoding.

Never create duplicate files for the same Task ID.

## 4. Required Task Markdown Template

# {TASK-ID} - {TASK-TITLE}

## 1. Metadata

- Project ID:
- Task ID:
- Plane Work Item ID:
- Status:
- Priority:
- Assigned Agent:
- Repository:
- Created At:
- Updated At:

## 2. Objective

Describe the expected outcome.

## 3. Business Context

Explain why the task is needed.

## 4. Requirements

List functional and non-functional requirements.

## 5. Brain Knowledge References

List relevant Brain document IDs and paths.

## 6. CodeGraph Investigation

- Existing implementation
- Relevant files
- Symbols
- Dependencies
- Impact analysis

Mark unknown information as UNKNOWN.

## 7. Implementation Scope

- Expected changes
- Files/modules affected
- Out-of-scope items

## 8. Dependencies

List prerequisite tasks and their IDs.

## 9. Implementation Plan

List concrete implementation steps.

## 10. Acceptance Criteria

Define verifiable completion conditions.

## 11. Test Strategy

Define automated and manual tests.

## 12. Worktree Information

- Repository:
- Branch:
- Worktree path:
- Base commit:

## 13. Execution Results

Record actual changes, commits and test results.

## 14. Review Results

Record reviewer findings and status.

## 15. Decisions and Lessons Learned

Record important decisions and reusable knowledge.

## 16. Related Documents

- Project Plan
- Related Tasks
- Architecture
- Requirements
- Execution Reports

Do not fabricate information.
Use NOT_INVESTIGATED when investigation has not occurred.

## 5. Plan Synchronization

Whenever a task is created or updated:

Update:

projects/{project-id}/plan.md

Maintain a Task Index:

| Task ID | Title | Status | Dependencies | Document |
|---------|-------|--------|--------------|----------|

Every entry must link to its TASK-ID.md file.

Do not overwrite existing plan content.

## 6. Plane Synchronization

Every task must map to a Plane Work Item.

Record:
- Plane Project ID
- Plane Work Item ID
- Task ID
- Task title
- Status
- Priority
- Dependencies
- Markdown reference

Use the existing Plane adapter.

Do not assume unsupported Plane features.

If Plane is unavailable:
Save local Markdown and mark Plane synchronization BLOCKED.

Never invent Plane IDs.

## 7. Brain Registration

Register every Task Markdown file using existing Brain ingestion.

Metadata:

category: PROJECT_DOCUMENTATION
knowledge_type: TASK
project_id: {project-id}
task_id: {task-id}
authority: PROJECT_KNOWLEDGE
status: ACTIVE

Use incremental indexing.

Update existing document identity when the file changes.

Do not create duplicate vectors unnecessarily.

Do not reset Qdrant.

Brain must be able to retrieve:
- Task by ID
- Task by title
- Task by project
- Related tasks
- Decisions and lessons learned

## 8. Task Lifecycle

CREATED:
Markdown created and Plan updated.

PLANNED:
Requirements, dependencies and acceptance criteria defined.

PENDING_APPROVAL:
Waiting for user approval.

APPROVED:
Authorized for execution.

IN_PROGRESS:
Dedicated Git Worktree allocated.

REVIEW:
Implementation completed and awaiting review.

DONE:
Acceptance criteria passed, review completed,
execution evidence saved and Plane synchronized.

BLOCKED:
Blocker documented in Markdown and Plane.

CANCELLED:
Cancellation reason documented.
Never delete historical Task Markdown.

## 9. Git Worktree Integration

Every approved Developer task requires:

- Dedicated branch
- Dedicated worktree
- Unique task workspace

Path:

E:\MausBot\worktrees\{project-id}\{task-id}

Branch:

mausbot/{project-id}/{task-id}

Never implement directly in the primary working tree.

Never automatically delete worktrees.

Follow git-worktree.md.

## 10. Task Update Rules

When task information changes:

1. Update the existing Markdown file.
2. Update plan.md if dependencies or scope change.
3. Synchronize Plane.
4. Re-index changed documents in Brain.
5. Preserve historical decisions.
6. Update Updated At.

Never create a new Task ID for an ordinary update.

## 11. Completion Rules

Before marking DONE:

- Acceptance criteria verified.
- Tests executed.
- Test evidence recorded.
- Review passed.
- Git commit recorded.
- Worktree and branch recorded.
- Plane updated.
- Markdown updated.
- Brain indexing verified.

Do not mark DONE merely because Developer reports completion.

## 12. Failure Handling

If a required system is unavailable:

- Preserve local Markdown.
- Record the failure.
- Mark the affected integration BLOCKED.
- Never invent successful synchronization.
- Retry safely when the service returns.

## 13. Mandatory Enforcement

Coordinator must invoke this Skill before every
task creation or task decomposition operation.

Task creation must fail validation if:
- Project Registry is missing.
- Task ID is duplicated.
- Task Markdown cannot be created.
- Plan does not reference the Task.
- Required task metadata is missing.

Do not rely on prompt instructions alone.
Integrate validation into the actual task dispatch pipeline.

## 14. Final Reporting

Report:

- Task ID
- Markdown path
- Plane Work Item ID
- Brain indexing status
- Plan synchronization status
- Worktree status
- Approval status

Use:
PASS / FAIL / BLOCKED / NOT_IMPLEMENTED / NOT_TESTED

END SKILL
