---
name: code-onboard
description: Read and understand an existing code project, add high-signal comments to project-owned source files, and update the internal quick-start README. Use when a user wants Codex to improve code readability, document module responsibilities, explain data/control flow, annotate functions, macros, structs, state machines, interrupts, tasks, protocol mappings, or generate/update a README for developers taking over the code. Especially useful for embedded C/C++ projects, hardware drivers, RTOS applications, firmware, protocol converters, and staged engineering projects.
---

# Code Onboard

Use this skill to make an existing project easier for a new developer to understand. The main outputs are:

- Better comments in project-owned source files.
- An updated internal `README.md` that explains the current codebase and quick-start workflow.

Do not treat this as a feature-development or release-tagging skill. If the user wants stage implementation, commit, and tag handling, use the project's stage-release workflow.

## Required inputs

Identify these before editing:

- Real project directory.
- Internal README path, usually `<project>/README.md`.
- Source scope to annotate, such as `User/App`, `src`, `include`, or selected files.
- Files or directories to exclude, especially third-party libraries, generated code, SDKs, build outputs, and vendor code.
- Optional project framework path, stage notes path, or existing architecture document.

If the project framework is available, read it before editing. It can contain module boundaries, user reminders, debugging methods, version rules, and documentation expectations.

## First understand the code

Before adding comments:

- Inspect the project tree and identify owned application code versus third-party or generated code.
- Read the important headers and source files in dependency order.
- Identify the project purpose, runtime flow, module responsibilities, public interfaces, state machines, queues, interrupts, tasks, callbacks, protocol mappings, and hardware/toolchain assumptions.
- Compare README, Git tags/log, and framework if available. Note mismatches, but do not fix unrelated versioning issues unless the user asked.
- Decide the comment style from existing project conventions. If the project has no strong convention, use the style below for C/C++ embedded projects.

## What to annotate

Annotate only code that benefits future readers:

- Project-owned `.c`, `.h`, `.cpp`, `.hpp`, or equivalent source files.
- Module entry points, public APIs, tasks, ISRs, callbacks, protocol handlers, state machines, hardware access functions, and unusual decisions.
- Structs, enums, macro groups, configuration constants, and mapping tables that are difficult to infer from names alone.
- Critical logic blocks where the reason, data shape, timing, ordering, or side effect is not obvious.

Avoid:

- Repeating what the code already says.
- Commenting every trivial line.
- Reformatting unrelated code.
- Changing behavior while adding comments.
- Editing third-party libraries, generated files, SDK files, build outputs, or vendored code unless the user explicitly asks.
- Removing legal copyright or license headers. If a project also wants a uniform file-purpose block, add it after required legal text.

## C/C++ comment style

Use this style when the project does not already define a better one.

File header:

```c
/**********************************************************************************************************
 * File: xxx.c
 * Purpose: One sentence describing the file's responsibility. Use the user's language for logic and keep
 *          protocol/API/tool names in their original English form.
 **********************************************************************************************************/
```

Function header:

```c
/**********************************************************************************************************
 * Function: FuncName
 * Params: param1 - meaning, param2 - meaning
 * Purpose: Describe what the function does and its role in the data/control flow.
 * Return: Return value meaning, or "None"/"无" for void.
 **********************************************************************************************************/
```

Function rules:

- Mark special roles in `Function`, such as `(FreeRTOS Task)`, `(ISR)`, `(callback)`, or `(static helper)`.
- For pointer parameters, note direction when useful: input, output, in/out, buffer length, ownership, or lifetime.
- Describe behavior and intent, not line-by-line implementation.
- Use arrows for data flow when useful, such as `RX byte -> decoder -> event queue -> report`.

Structs, enums, and macros:

```c
/** Decode event action. */
typedef enum {
    EVENT_MAKE  = 0,  /**< Key pressed */
    EVENT_BREAK = 1,  /**< Key released */
} event_action_t;

#define APP_QUEUE_LEN 32  /**< Queue depth for raw input bytes */
```

Group related macros:

```c
/* ---- Hardware pins ---- */
/* ---- Queue depths ---- */
/* ---- Timeouts (ms) ---- */
```

Critical logic comments:

- Use short line comments for state transitions, timing boundaries, frame fields, retries, error paths, and non-obvious hardware/protocol constraints.
- Prefer explaining why a branch exists over translating the expression.

Mapping table comments:

- For protocol/key/register mapping tables, keep one entry per line and add readable names.
- Add a compact aligned header when the table has many entries.
- Mark special cases, modifiers, extended codes, reserved values, or hardware-specific meanings.

## Language and tone

- Match the user's project language. For Chinese projects, write logic explanations in Chinese and keep technical terms such as `USB`, `HID`, `FreeRTOS`, `EXTI`, `ISR`, `DMA`, and function names in English.
- Keep comments concise and useful for maintainers.
- Do not add dates, authors, or version history to source comments unless the project already requires it.

## README update

After code annotation, update the internal `README.md` as a quick-start document for someone taking over the project.

Default README structure:

```markdown
# Project Name

Current code baseline: **Vx.x** / 当前代码基线：**Vx.x**

## Project Overview / 项目概述

## Directory Structure / 目录结构

## Core Module Flow / 核心模块调用关系

## Runtime Tasks / 任务说明

## Build and Debug / 构建与调试

## Version History / 版本历史
```

Adapt the section language to the project. For embedded/RTOS projects, include:

- Project purpose in one paragraph.
- Core capabilities in 3-5 bullets.
- Hardware pin table when hardware is involved.
- Directory tree with one-line responsibilities for important folders/files.
- ASCII flow diagram for key data/control flow. Prefer plain text over Mermaid for maximum portability.
- RTOS task table if tasks exist: task name, priority, stack, responsibility.
- Queue/event/timer/configuration tables when they are central to understanding the runtime.
- Build tools, debugger, simulator, diagnostic counters/logs, or hardware verification methods.
- Version history based on Git tags/log or existing project notes.

README rules:

- README describes current state, not a long development diary.
- Do not put detailed verification logs or stage narratives in README; link to external stage notes if they exist.
- Do not add TODO or future plans unless the existing project README already has that policy.
- If README baseline/version conflicts with Git tags, mention the mismatch in the response and update only when confident.

## Verification

After editing:

- Re-read modified files for comment consistency and broken formatting.
- Build or run the project's normal checks when available and reasonable.
- If no build is possible, explain why and perform static inspection.
- Confirm no behavior-changing edits were introduced intentionally.
- Report excluded directories and files, modified files, README updates, and verification results.

## Final response

Summarize:

- Source scope annotated.
- Important comment patterns added.
- README sections updated.
- Files intentionally skipped.
- Verification performed and result.
- Any README/Git/framework mismatch found.
