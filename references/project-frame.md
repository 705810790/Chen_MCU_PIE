# Project Frame Workflow

Use this workflow to convert requirement sources and reference materials into a reusable, living project framework.

## Start by locating project inputs

Ask for missing paths and project habits before producing the framework:

- Requirement folder path, if the user keeps multiple demand/background files.
- Primary requirement document path, if one document is the source of truth.
- Reference-material folder path, if the user prepared datasheets, examples, SDK notes, prior code, screenshots, logs, or related documents.
- Real project directory path, or the expected future project directory if it does not exist yet.
- Framework Markdown output path.
- Optional specific reference-code, datasheet, design-note, or toolchain paths inside the reference folder.
- Debugging tools and methods the user wants later AI agents to use.
- User reminders or project-specific cautions that later AI agents must read before implementing stages.

Read the primary requirement document first when present, then scan the requirement folder and reference-material folder for relevant files. Do not read every large reference blindly; list candidates, prioritize filenames that match the project goal, and open only the documents needed to build the framework.

For reference folders, extract:

- Which files are requirements, constraints, examples, SDK/vendor references, prior implementations, test evidence, or background notes.
- Which materials are authoritative versus only examples.
- Which code or documents can be reused directly, adapted, or only consulted.
- Any gaps where the folder exists but does not contain enough information.

## Core Behavior

Generate a framework that is specific enough to drive execution but not tied to one technology stack. Treat the framework as a living document:

- Update it when implementation facts prove the original plan incomplete or wrong.
- Keep it aligned with the real project at the end of every completed stage.
- Do not require Git commits for every temporary framework edit.
- Prefer stage-level snapshots over high-frequency document versioning.
- Keep external framework and stage notes outside the real engineering project when the user wants a clean project tree.
- Put project-specific cautions, debug habits, and user-intervention rules near the top so later stage execution sees them early.
- Preserve requirement and reference-folder paths in the framework so later agents can re-open the same sources.

## Framework Template

Use this structure by default:

```markdown
# <Project Name> Framework

## 1. User Reminders and Execution Notes
- Important cautions later AI agents must read first:
- Required debugging tools or preferred skills:
- User-intervention verification method:
- Approval-sensitive operations:

## 2. Project Goal

## 3. Requirement Sources
- Requirement folder:
- Primary requirement document:
- Requirement summary:
- Explicit requirements:
- Implied requirements:
- Non-goals:

## 4. Reference Materials
- Reference folder:
- Authoritative references:
- Example-only references:
- Reusable code/assets:
- Materials intentionally ignored:
- Reference gaps:

## 5. Known Constraints
- Hardware constraints:
- Software constraints:
- Toolchain constraints:
- Directory/project constraints:
- User preferences:

## 6. Overall Flow

## 7. Recommended Project Structure

## 8. Module Breakdown

## 9. Reference Reuse Strategy

## 10. Initialization / Execution / Call Order

## 11. Debugging and Verification Methods
- Build/test commands:
- Hardware or environment setup:
- Logs/counters/state to inspect:
- User-operated steps:
- Prompt-box or confirmation workflow:
- Validation evidence to record:

## 12. Staged Implementation Plan
For each stage:
- Version
- Stage name
- Scope
- Out of scope
- Main files/modules
- Acceptance criteria

## 13. Documentation and Version Rules
- Internal README rules:
- External stage-note rules:
- Framework update rules:
- Commit/tag rules:
- External document versioning policy:

## 14. Open Questions

## 15. Implementation Principles
```

## Stage Plan Rules

- Make each stage independently understandable and verifiable.
- Prefer small stages that compile, run, or otherwise validate cleanly.
- Give each stage one main purpose.
- Preserve dependency order.
- Include acceptance criteria that a human can check.
- Tie stages to reference materials when specific stages depend on specific examples, datasheets, APIs, or prior code.

## Output Expectations

- Write the framework to the requested Markdown path when the user wants file output.
- Mention assumptions made from the requirement document or folder.
- Include requirement folder, primary requirement document, and reference-material folder paths when known.
- Put user reminders and debugging methods near the top.
- List open questions separately.
- Do not start implementation unless the user also asks to execute a stage.
