# Stage Release Workflow

Use this workflow to continue a staged project from an existing framework and finish the stage with verification, README updates, stage documentation, and Git release tagging.

## Required Inputs

Before making changes, identify:

- Project framework Markdown path.
- Real project directory path.
- Internal project README path, usually inside the real project directory.
- External stage-note output directory.

If any path is missing, ask for it. If paths are present in the framework, use those values and confirm only when ambiguous.

## Always Read The Framework First

At the start of every stage execution, read the project framework before deciding what to change. The framework is the source for:

- Current project goal and architecture.
- User reminders and project-specific cautions.
- Debugging tools, preferred commands, and user-intervention workflows.
- Stage plan and acceptance criteria.
- Documentation and version-control rules.

If the framework references a separate debugging-method document, read that document before verification work.

## Determine Current State

Read sources in this priority order:

1. Git tags and recent Git log in the real project repository.
2. Internal project README.
3. External project framework staged plan.
4. Existing external stage notes.

Use Git tags/log as the highest authority for the already-released code state. README can be stale, so compare it against Git.

If these sources disagree, state the mismatch before changing files. Continue with the Git state unless the user explicitly says otherwise.

## Implementation Workflow

1. Inspect the relevant code and project structure.
2. Implement only the current stage scope.
3. Keep unrelated refactors out of the stage.
4. Run the appropriate build, test, static check, or hardware verification workflow available for the project.
5. If verification requires the user to operate hardware or observe UI/device behavior, use the project's user-intervention protocol from the framework.
6. Fix issues found during verification when they are within current stage scope.
7. Stop and ask before expanding scope beyond the stage objective.

## User-Intervention Verification

For projects that require human hardware actions, prefer structured confirmation over loose chat instructions:

- Explain what is being verified.
- Present exact ordered user actions.
- Wait until the user confirms completion.
- Immediately read objective evidence such as logs, counters, device state, serial output, debugger memory, or test output.
- Combine user-observed results with objective data before judging pass/fail.

On Windows, if the framework asks for prompt-box confirmation, show a Windows message box with exact test steps, wait for the user to click OK, then continue verification. This does not replace explicit approval for risky operations such as flashing, erasing, installing dependencies, deleting files, or committing/pushing.

## Documentation Updates

After implementation and verification:

- Update internal README to describe current released project state.
- Keep README concise and practical: build, run, use, architecture, current version, known constraints.
- Write external `Vx.y_阶段说明.md` or equivalent stage note in the configured output directory.
- Update the external framework when implementation changed architecture, stages, constraints, accepted assumptions, future plans, or debugging methods.

Stage note template:

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

## Version-Control Rules

- One completed stage equals one release commit.
- Tag the commit with the stage version, such as `V0.3`.
- Use a concise one-line commit message: `<version>: <short English description>`.
- Keep detailed implementation explanation in the external stage note, not the commit body.
- Do not commit build artifacts or IDE noise unless the project intentionally tracks them.
- Check `git status` before committing and avoid staging unrelated user changes.

## Release Checklist

- The framework was read during this execution.
- User reminders and debugging methods from the framework were followed.
- Current stage acceptance criteria are satisfied or explicitly documented as not verifiable.
- Internal README current version matches the release being made.
- External stage note exists.
- Framework is updated if the stage changed the plan, architecture, constraints, or debugging process.
- `git status` contains only intended release changes.
- Build/test/verification command output is recorded in the final response.
