# Code Onboard Workflow

Use this workflow to make an existing project easier for a new developer to understand. The main outputs are:

- Better comments in project-owned source files.
- An updated internal `README.md` that explains the current codebase and quick-start workflow.

Do not treat this as feature development or release tagging.

## Required Inputs

Identify before editing:

- Real project directory.
- Internal README path, usually `<project>/README.md`.
- Source scope to annotate, such as `User/App`, `src`, `include`, or selected files.
- Files or directories to exclude, especially third-party libraries, generated code, SDKs, build outputs, and vendor code.
- Optional project framework path, stage notes path, or existing architecture document.

If the project framework is available, read it before editing.

## First Understand The Code

- Inspect the project tree and identify owned application code versus third-party or generated code.
- Read important headers and source files in dependency order.
- Identify project purpose, runtime flow, module responsibilities, public interfaces, state machines, queues, interrupts, tasks, callbacks, protocol mappings, and hardware/toolchain assumptions.
- Compare README, Git tags/log, and framework if available. Note mismatches, but do not fix unrelated versioning issues unless the user asked.
- Decide comment style from existing project conventions.

## What To Annotate

Annotate only code that benefits future readers:

- Project-owned `.c`, `.h`, `.cpp`, `.hpp`, or equivalent source files.
- Module entry points, public APIs, tasks, ISRs, callbacks, protocol handlers, state machines, hardware access functions, and unusual decisions.
- Structs, enums, macro groups, configuration constants, and mapping tables that are difficult to infer from names alone.
- Critical logic blocks where reason, data shape, timing, ordering, or side effect is not obvious.

Avoid:

- Repeating what the code already says.
- Commenting every trivial line.
- Reformatting unrelated code.
- Changing behavior while adding comments.
- Editing third-party libraries, generated files, SDK files, build outputs, or vendored code unless explicitly asked.

## C/C++ Comment Style

File header:

```c
/**********************************************************************************************************
 * File: xxx.c
 * Purpose: One sentence describing the file's responsibility.
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

Rules:

- Mark special roles such as `(FreeRTOS Task)`, `(ISR)`, `(callback)`, or `(static helper)`.
- For pointer parameters, note direction when useful.
- Describe behavior and intent, not line-by-line implementation.
- Use arrows for data flow when useful.

Structs, enums, and macros may use compact comments:

```c
#define APP_QUEUE_LEN 32  /**< Queue depth for raw input bytes */
```

Group related macros:

```c
/* ---- Hardware pins ---- */
/* ---- Queue depths ---- */
/* ---- Timeouts (ms) ---- */
```

## README Update

After code annotation, update internal `README.md` as a quick-start document for someone taking over the project.

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

For embedded/RTOS projects, include:

- Project purpose in one paragraph.
- Core capabilities in 3-5 bullets.
- Hardware pin table when hardware is involved.
- Directory tree with one-line responsibilities.
- ASCII flow diagram for key data/control flow.
- RTOS task table if tasks exist.
- Queue/event/timer/configuration tables when central.
- Build tools, debugger, diagnostic counters/logs, or hardware verification methods.
- Version history based on Git tags/log or existing project notes.

README rules:

- README describes current state, not a long development diary.
- Do not put detailed verification logs or stage narratives in README.
- Do not add TODO or future plans unless the existing project README already has that policy.
- If README baseline/version conflicts with Git tags, mention the mismatch in the response and update only when confident.

## Verification

After editing:

- Re-read modified files for comment consistency and broken formatting.
- Build or run normal checks when available and reasonable.
- If no build is possible, explain why and perform static inspection.
- Confirm no behavior-changing edits were introduced intentionally.
- Report excluded directories and files, modified files, README updates, and verification results.
