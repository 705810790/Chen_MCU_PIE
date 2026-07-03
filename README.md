# Chen_MCU_PIE(MCU project implementation engineer)
Chen_MCU_PIE 是一组面向 AI 项目推进流程的 Codex Skills 组合包。
Chen_MCU_PIE 的中文名是 **MCU项目实施工程师**。它是一个面向 AI 项目推进流程的组合 Codex Skill，用一个统一入口覆盖三个连续能力：

它可以对项目需求进行系统化的展开，将大型项目划分为一个一个的小阶段，然后每完成一个阶段就进行git版本控制，完美适配大型项目。收录 `project-frame`、`stage-release`、`code-onboard` 三个独立 Skill，用于把一个工程从“需求整理”推进到“阶段实现”，再沉淀成“可接手、可维护、可归档”的代码项目。

```text
需求与资料 → 动态项目框架 → 阶段实施和版本归档 → 代码注释和快速上手 README
```

它不是单纯的代码生成器，而是帮助 AI 按工程流程推进项目：先整理清楚需求和参考资料，再按小阶段实现、验证、归档，最后把代码沉淀成可接手、可维护的工程。

## 名称解释

- **MCU**：优先服务嵌入式 MCU、硬件驱动、RTOS、协议转换、调试验证等工程场景，也可复用于其他软件项目
- **Project**：先整理需求、参考资料、项目目标、约束和模块框架
- **Implementation**：按阶段实施、验证、更新文档并进行版本归档
- **Engineering**：补充代码注释、快速上手 README 和长期维护所需的工程化信息

## 背景

在 AI 协作开发中，常见问题不是 AI 不会写代码，而是项目流程没有被固定下来：

- 开始写代码前，需求、参考资料、约束条件没有被系统整理
- 项目推进过程中，AI 不知道当前处于哪个阶段
- 每次开发都依赖上下文记忆，压缩或中断后容易丢失方向
- 阶段完成后，README、阶段说明和 Git tag 容易不同步
- 代码完成后缺少接手友好的注释和快速上手文档
- 硬件调试、用户人工操作、日志读取等验证方法没有固定记录

Chen_MCU_PIE 把这些流程固化成一个组合 Skill，让 AI 能以“项目实施工程师”的方式持续推进项目。

## 可以实现什么

Chen_MCU_PIE 可以帮助 AI 完成：

- 读取需求文件夹、主需求文档和参考资料文件夹
- 提炼项目目标、硬件/软件/工具链约束和用户特别提醒
- 生成可持续更新的项目框架 Markdown
- 将项目拆分成多个可验证阶段
- 每阶段按框架实施、验证、更新 README、输出阶段说明
- 对真实工程执行 commit/tag 版本归档
- 记录硬件调试、用户确认、日志读取等验证方法
- 阅读已有代码，为项目自有源码补充高价值注释
- 更新工程内部 `README.md`，让接手者快速理解项目

## 安装

安装组合 Skill：

```powershell
帮我安装 https://github.com/705810790/Chen_MCU_PIE.git 的skill
```

如果需要设置为全局在任意文件夹调用：

```powershell
帮我安装 https://github.com/705810790/Chen_MCU_PIE.git 的skill 到全局目录下
```

安装后主要调用：

```text
使用 $chen-mcu-pie，帮我从需求开始建立项目框架。
使用 $chen-mcu-pie，按框架继续推进下一个阶段。
使用 $chen-mcu-pie，阅读代码并补充注释和 README。
```

## 项目结构

```text
Chen_MCU_PIE/
├── README.md
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── project-frame.md
    ├── stage-release.md
    └── code-onboard.md
```

根 `SKILL.md` 是统一入口，`references/` 中保留三个能力的详细执行流程。这样用户安装的是一个 Skill，但 AI 可以根据任务选择对应流程。

## 三个能力

| 能力 | 作用 | 典型使用时机 |
| --- | --- | --- |
| `project-frame` | 读取需求和参考资料，生成动态项目框架 | 新项目开始前，或项目框架需要补全时 |
| `stage-release` | 按框架执行阶段、验证、更新 README、输出阶段说明、commit/tag | 项目进入分阶段实施后 |
| `code-onboard` | 阅读代码、补充注释、更新工程内部快速上手 README | 代码形成可用基线后，或需要交接维护前 |

## 推荐工作流

### 1. 准备需求和资料

推荐先整理项目资料：

```text
01_需求确定/
02_参考资料/
03_代码编写/
```

需求文件夹中可以放主需求文档、背景说明、用户特殊要求和验收目标。

参考资料文件夹中可以放数据手册、SDK 示例、参考代码、调试日志、原理图、接口说明或旧版本项目资料。

### 2. 生成项目框架

```text
使用 $chen-mcu-pie，读取我的需求文件夹、主需求文档和参考资料文件夹，生成项目框架 md。
```

### 3. 按阶段推进项目

```text
使用 $chen-mcu-pie，按项目框架继续推进下一个阶段。
```

每个阶段结束后，AI 应完成：

```text
代码或文档实现
→ 编译/测试/硬件验证
→ 更新工程内部 README.md
→ 输出外部 Vx.y_阶段说明.md
→ 必要时更新项目框架
→ git commit
→ git tag
```

### 4. 注释代码并完善快速上手文档

```text
使用 $chen-mcu-pie，阅读当前工程代码，补充注释，并更新工程 README.md。
```

## 独立 Skill 仓库

这三个能力也保留了独立仓库，方便单独安装、单独维护或单独测试：

- `project-frame`: https://github.com/705810790/project-frame
- `stage-release`: https://github.com/705810790/stage-release
- `code-onboard`: https://github.com/705810790/code-onboard

通常情况下，最终使用形态推荐安装 `Chen_MCU_PIE` 组合包；只有在你明确只需要某一个能力时，再安装独立 Skill。

## 注意事项

- `project-frame` 不应盲目读取整个参考资料文件夹，应先列候选文件，再读取相关资料
- `stage-release` 每次执行阶段前必须先读项目框架
- `code-onboard` 不应修改第三方库、SDK、自动生成代码和编译产物
- 组合 Skill 使用 `references/` 做渐进加载，避免一次性加载所有细节
- 不要在 Skill 或 README 中写死个人工程路径、账号密钥或未脱敏日志
