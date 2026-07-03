---
name: project-frame
description: Turn user requirements into a living project framework. Use when a user wants Codex to start a project by reading a requirement document or requirement folder, inspecting reference-material folders, extracting goals, constraints, references, user reminders, debugging methods, module boundaries, staged plans, documentation rules, and version-control expectations before implementation. Also use when maintaining or updating an existing project framework as the real project evolves.
---

# Project Frame

Use this skill to convert requirement sources and reference materials into a reusable, living project framework. The output is an external Markdown framework that guides later implementation, debugging, documentation, and staged releases.

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

If the user already gave these paths and preferences, continue without asking again. Read the primary requirement document first when present, then scan the requirement folder and reference-material folder for relevant files. Do not read every large reference blindly; list candidates, prioritize filenames that match the project goal, and open only the documents needed to build the framework.

For reference folders, extract:

- Which files are requirements, constraints, examples, SDK/vendor references, prior implementations, test evidence, or background notes.
- Which materials are authoritative versus only examples.
- Which code or documents can be reused directly, adapted, or only consulted.
- Any gaps where the folder exists but does not contain enough information.

For debugging methods, prompt with examples instead of leaving the question abstract:

- Hardware probes, serial tools, debugger tools, logs, test scripts, GUI inspection, browser devtools, or simulator/emulator.
- User-intervention protocols, such as "show a Windows message box with exact hardware test steps, wait for the user to click OK, then read counters/logs."
- Commands or skills that should be preferred for compile, flash, debug, serial, or device inspection.

## Core behavior

Generate a framework that is specific enough to drive execution but not tied to one technology stack. Treat the framework as a living document:

- Update it when implementation facts prove the original plan incomplete or wrong.
- Keep it aligned with the real project at the end of every completed stage.
- Do not require Git commits for every temporary framework edit.
- Prefer stage-level snapshots over high-frequency document versioning.
- Keep external framework and stage notes outside the real engineering project when the user wants a clean project tree.
- Put project-specific cautions, debug habits, and user-intervention rules near the top so later stage execution sees them early.
- Preserve requirement and reference-folder paths in the framework so later agents can re-open the same sources.

## Extract from requirements and references

When reading the requirement source and reference materials, separate these items explicitly:

- Project goal: what must be delivered.
- Background: why the project exists and what existing systems it touches.
- Explicit requirements: direct user statements.
- Implied requirements: necessary consequences of the goal or constraints.
- Non-goals: work that should not be done yet.
- Hardware, software, toolchain, directory, platform, and maintenance constraints.
- Reference material and reusable source assets.
- User preferences, such as simplicity, debuggability, learning-oriented documentation, or coding style.
- Debugging and verification methods the user expects later AI agents to follow.
- Open questions that block or affect implementation choices.

## Framework template

Use this structure by default. Rename sections only when the project domain strongly benefits from different wording.

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
Describe the data flow, control flow, user workflow, build flow, or system interaction flow that matters most for this project.

## 7. Recommended Project Structure

## 8. Module Breakdown
For each module:
- Responsibility
- Inputs and outputs
- Public interfaces or files
- Boundaries and dependencies
- Notes and risks

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

## Stage plan rules

When creating the staged plan:

- Make each stage independently understandable and verifiable.
- Prefer small stages that compile, run, or otherwise validate cleanly.
- Give each stage one main purpose.
- Preserve dependency order; do not schedule work that depends on a later stage.
- Include acceptance criteria that a human can check.
- Mark risky or uncertain parts as validation steps before broad implementation.
- Include documentation and release expectations if the user wants long-term maintainability.
- Include the expected debugging or verification method for stages that need special tools or user-operated hardware steps.
- Tie stages to reference materials when specific stages depend on specific examples, datasheets, APIs, or prior code.

## Documentation and version policy

Use this default policy unless the user asks for stricter document versioning:

- The real project README is internal documentation and should follow code versions.
- External framework and stage notes are project-management artifacts.
- Stage notes are written only after a stage is complete.
- The framework is updated when a completed stage changes the real architecture, plan, constraints, or debugging process.
- External documents do not need a Git commit for every temporary edit.
- If the real project uses Git, code commits and tags belong to the real project repository unless the user defines a separate management repository.

## Output expectations

When producing or updating the framework:

- Write the framework to the requested Markdown path when the user wants file output.
- Mention any assumptions made from the requirement document or folder.
- Include the requirement folder, primary requirement document, and reference-material folder paths when known.
- Put user reminders and debugging methods near the top of the framework.
- List open questions separately instead of hiding them inside the plan.
- Do not start implementation unless the user also asks to execute a stage.
- Keep wording reusable for future projects; avoid embedding project-specific rules as universal rules unless they are clearly derived from user preference.
