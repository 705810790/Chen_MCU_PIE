---
name: chen-mcu-pie
description: MCU project implementation engineer for AI-assisted engineering workflows. Use when a user wants Codex to drive a project from requirements and reference folders into a living project framework, then continue staged implementation with verification, README updates, stage notes, Git commit/tag release management, and later code annotation plus quick-start README onboarding. Especially useful for embedded MCU, hardware driver, RTOS, protocol-conversion, debugging-heavy, or staged engineering projects. Routes to project-frame, stage-release, or code-onboard workflows as needed.
---

# Chen_MCU_PIE

Use this skill as the single entry point for the MCU project implementation engineer workflow.

Choose the matching workflow:

- For starting a project from requirements/reference folders or updating a living framework, read [references/project-frame.md](references/project-frame.md).
- For continuing the next staged milestone, verification, README updates, stage notes, commit, and tag, read [references/stage-release.md](references/stage-release.md).
- For reading existing code, adding high-signal comments, and updating the internal quick-start README, read [references/code-onboard.md](references/code-onboard.md).

If the user request spans multiple workflows, execute them in this order:

```text
project-frame -> stage-release -> code-onboard
```

## Core Rules

- Treat the project framework as the long-lived coordination artifact.
- Before staged implementation, always read the framework if it exists.
- Keep external project-management documents separate from the real engineering project when the user wants a clean project tree.
- Keep the engineering README focused on current project state and quick onboarding.
- Use stage notes for implementation narrative, verification details, and lessons learned.
- Preserve user changes and avoid committing unrelated files.
- Ask for missing paths only when they cannot be discovered safely.

## Typical Routing

Use `project-frame` when the user says things like:

- "I have a requirements folder and references; generate a project framework."
- "Before coding, help me organize the project plan."
- "Update the framework based on the current project status."

Use `stage-release` when the user says things like:

- "Continue the next stage."
- "Follow the framework and finish this version."
- "Implement, verify, write the stage note, then commit and tag."

Use `code-onboard` when the user says things like:

- "Read the code and add comments."
- "Update README as a quick-start document."
- "Make this project easier for another developer to take over."

## Final Response Expectations

Report:

- Which workflow was used.
- Important paths read or written.
- Files changed.
- Verification performed.
- Any mismatches between framework, README, Git tags, or stage notes.
- Commit/tag information when a release workflow was executed.
