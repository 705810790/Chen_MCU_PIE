---
name: stage-release
description: Execute the next staged project milestone from a living framework and archive the release. Use when a user wants Codex to read a project framework, determine the current stage from Git history, tags, README, and stage notes, follow project-specific debugging or user-intervention rules, implement the next stage, verify it, update the internal README, write the external stage note, optionally update the framework, then commit and tag the code release.
---

# Stage Release

Use this skill to continue a staged project from an existing framework and finish the stage with verification, README updates, stage documentation, and Git release tagging.

## Required inputs

Before making changes, identify these paths:

- Project framework Markdown path.
- Real project directory path.
- Internal project README path, usually inside the real project directory.
- External stage-note output directory.

If any path is missing, ask for it. If paths are present in the framework, use those values and confirm only when ambiguous.

## Always read the framework first

At the start of every stage execution, read the project framework before deciding what to change. The framework is the source for:

- Current project goal and architecture.
- User reminders and project-specific cautions.
- Debugging tools, preferred commands, and user-intervention workflows.
- Stage plan and acceptance criteria.
- Documentation and version-control rules.

If the framework references a separate debugging-method document, read that document before verification work. Apply those rules unless they conflict with higher-priority user instructions or safety/approval requirements.

## Determine the current state

Read sources in this priority order:

1. Git tags and recent Git log in the real project repository.
2. Internal project README.
3. External project framework staged plan.
4. Existing external stage notes.

Use Git tags/log as the highest authority for the already-released code state. README can be stale, so compare it against Git. The framework is the planning source, not proof of completed code.

If these sources disagree, state the mismatch before changing files. Continue with the Git state unless the user explicitly says otherwise.

## Select the next stage

From the framework and current Git state:

- Identify the latest completed version.
- Identify the next planned stage.
- Confirm the stage objective, scope, out-of-scope work, files likely to change, and acceptance criteria.
- Identify the required debugging or verification method for this stage.
- If the next stage is unclear, propose a small stage that preserves the framework intent and ask only if proceeding would be risky.

## Implementation workflow

Follow this sequence:

1. Inspect the relevant code and project structure.
2. Implement only the current stage scope.
3. Keep unrelated refactors out of the stage.
4. Run the appropriate build, test, static check, or hardware verification workflow available for the project.
5. If verification requires the user to operate hardware or observe UI/device behavior, use the project's user-intervention protocol from the framework.
6. Fix issues found during verification when they are within the current stage scope.
7. Stop and ask before expanding scope beyond the stage objective.

## User-intervention verification

For projects that require human hardware actions, prefer a structured confirmation workflow over loose chat instructions:

- Explain what is being verified.
- Present exact ordered user actions.
- Wait until the user confirms completion.
- Immediately read objective evidence such as logs, counters, device state, serial output, debugger memory, or test output.
- Combine user-observed results with objective data before judging pass/fail.

On Windows, if the framework asks for prompt-box confirmation, show a Windows message box with the exact test steps, wait for the user to click OK, then continue verification. Use this pattern only for test-step synchronization; it does not replace explicit approval for risky operations such as flashing, erasing, installing dependencies, deleting files, or committing/pushing.

Example PowerShell pattern:

```powershell
Add-Type -AssemblyName PresentationFramework
[System.Windows.MessageBox]::Show(
    '请按以下步骤测试：`n`n1）执行当前阶段要求的人工操作；`n2）观察指定现象；`n3）完成后点击“确定”，AI 将继续读取日志或计数。',
    '验证确认',
    'OK',
    'Information'
)
```

## Documentation updates

After the implementation and verification are complete:

- Update the internal README to describe the current released project state.
- Keep README concise and practical: build, run, use, architecture, current version, known constraints.
- Do not turn README into a long development diary.
- Write an external `Vx.y_阶段说明.md` or equivalent stage note in the configured external stage-note directory.
- Update the external framework when the real implementation changed architecture, stages, constraints, accepted assumptions, future plans, or debugging methods.

Use this stage-note template by default:

```markdown
# <Version> Stage Note: <Stage Name>

## 1. Stage Goal

## 2. Modified Files

## 3. Implementation Approach

## 4. Key Details

## 5. Verification Method

## 6. Verification Result

## 7. Remaining Issues

## 8. Framework Updates

## 9. Next Stage Recommendation
```

For Chinese projects, use Chinese section titles matching the user's existing documentation style:

```markdown
# <版本> 阶段说明：<阶段名称>

## 1. 本阶段目标
## 2. 本阶段修改文件
## 3. 实现思路
## 4. 关键实现细节
## 5. 验证方法
## 6. 验证结果
## 7. 遗留问题
## 8. 对项目框架的更新
## 9. 下一阶段建议
```

## Version-control rules

Use the versioning rules from the framework when present. Otherwise use:

- One completed stage equals one release commit.
- Tag the commit with the stage version, such as `V0.3`.
- Use a concise one-line commit message: `<version>: <short English description>`.
- Keep detailed implementation explanation in the external stage note, not the commit body.
- Do not commit build artifacts or IDE noise unless the project intentionally tracks them.
- Check `git status` before committing and avoid staging unrelated user changes.
- If unrelated changes exist, leave them unstaged and explain the boundary.

## Release checklist

Before committing and tagging, verify:

- The framework was read during this execution.
- User reminders and debugging methods from the framework were followed.
- Current stage acceptance criteria are satisfied or explicitly documented as not verifiable.
- Internal README current version matches the release being made.
- External stage note for this release exists.
- Framework is updated if the stage changed the plan, architecture, constraints, or debugging process.
- `git status` contains only intended release changes.
- Build/test/verification command output is recorded in the final response.

## Final response

Summarize:

- Released version and stage name.
- Main implementation changes.
- README and external stage-note updates.
- Verification performed and result.
- Commit hash and tag if created.
- Any mismatches or follow-up risks.
