# stage-release

`stage-release` 是一个面向 AI 分阶段开发的 Codex Skill，用于读取项目框架、工程 README 和 Git 状态，判断当前项目阶段，实施下一个阶段，完成验证、README 更新、阶段说明输出、commit 和 tag。

它的核心目标是让 AI 不再“一次性大改”，而是按照框架小步推进，每个阶段都可编译、可验证、可归档、可回退。

## 背景

在 AI 协作开发中，如果没有阶段控制，容易出现：

- 一次修改范围太大，问题难定位
- README、阶段说明和 Git tag 不一致
- AI 不读取项目框架，只凭上下文记忆继续写
- 硬件调试步骤不固定，验证结果不可复现
- 完成代码后没有及时归档版本
- 项目庞大，需要多轮对话导致任务被超多上下文拖垮，且上下文压缩后出现记忆力不集中导致的结果和预料不同

`stage-release` 用来把阶段执行流程固定下来：每次先读框架，再确认当前状态，然后只完成当前阶段范围内的工作。

## 适用场景

- 项目已经有框架 Markdown
- 项目按 `V0.1 / V0.2 / V0.3` 等阶段推进
- 每个阶段完成后需要更新 README 和阶段说明
- 需要 Git commit/tag 记录每个阶段
- 需要根据框架里的调试方法执行硬件或软件验证

## 一键安装

安装到当前 AI 环境：

```powershell
帮我安装 https://github.com/705810790/stage-release.git 的 skill
```

如果需要设置为全局在任意文件夹调用的 skill：

```powershell
帮我安装 https://github.com/705810790/stage-release.git 的 skill 到全局目录下
```

## Skill 结构

```text
stage-release/
├── README.md
├── SKILL.md
└── agents/
    └── openai.yaml
```

## 使用方式

推荐提示：

```text
使用 $stage-release，读取项目框架并继续推进下一个阶段。
```

`stage-release` 需要知道：

- 项目框架 Markdown 路径
- 真实工程目录
- 工程内部 README 路径
- 外部阶段说明文档输出目录

如果框架里已经记录这些路径，AI 会优先使用框架中的信息。

## 执行流程

`stage-release` 每次执行都应按这个顺序：

```text
读取项目框架
→ 读取 Git tag / Git log
→ 读取工程 README
→ 读取已有阶段说明
→ 判断当前阶段和下一阶段
→ 实施当前阶段
→ 编译/测试/硬件验证
→ 更新工程 README.md
→ 输出 Vx.y_阶段说明.md
→ 必要时更新项目框架
→ git commit
→ git tag
```

## 版本规则

默认规则：

- 一个完成阶段对应一个 release commit
- tag 使用阶段版本号，例如 `V0.3`
- commit 信息使用单行英文，例如 `V0.3: add PS2 byte receive stage`
- 详细实现说明写入阶段说明文档，不写进 commit body
- 不提交编译产物、IDE 噪声或无关用户修改

## 硬件调试和用户确认

如果框架中记录了硬件调试方法，`stage-release` 必须在验证前读取并执行。

对于需要用户插拔设备、按键、观察屏幕等场景，可以让 AI 使用 Windows 提示框列出测试步骤，等用户点击“确定”后，再读取日志、计数器、串口输出或调试器状态。

提示框确认只用于测试步骤同步，不替代刷写、删除、安装依赖、提交、推送等风险操作的明确审批。

## AI 推荐用法

继续下一个阶段：

```text
使用 $stage-release，框架路径是 <framework.md>，工程目录是 <project-dir>，阶段说明输出到 <docs-dir>。
```

如果 README 和 Git tag 不一致：

```text
使用 $stage-release，先对比 Git tag、README 和框架，说明当前版本不一致点，再判断下一步。
```

如果需要硬件验证：

```text
使用 $stage-release，按框架里的调试方法验证；需要我人工操作时，用提示框列出步骤。
```

## 注意事项

- 每次执行阶段前必须先读项目框架
- Git tag/log 是已发布代码状态的最高优先级依据
- README 可能滞后，不能只凭 README 判断当前版本
- 不要把下个阶段或无关重构混进当前阶段
- 如果有用户未提交修改，必须避免误提交或覆盖
