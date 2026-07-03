# Chen_MCU_PIE(MCU project implementation engineer)

Chen_MCU_PIE 是一组面向 AI 项目推进流程的 Codex Skills 组合包。它可以对项目需求进行系统化的展开，将大型项目划分为一个一个的小阶段，然后每完成一个阶段就进行git版本控制，完美适配大型项目。收录 `project-frame`、`stage-release`、`code-onboard` 三个独立 Skill，用于把一个工程从“需求整理”推进到“阶段实现”，再沉淀成“可接手、可维护、可归档”的代码项目。

这个组合包的核心目标是让 AI 不再只做一次性的代码生成，而是按照明确框架、小步阶段、验证归档、文档沉淀的方式持续推动项目。

## 仓库定位

`Chen_MCU_PIE` 是一个 **索引/收录仓库**，不是三个 Skill 的源码副本仓库。

三个 Skill 的实际维护发生在各自独立仓库：

- `project-frame`: https://github.com/705810790/project-frame
- `stage-release`: https://github.com/705810790/stage-release
- `code-onboard`: https://github.com/705810790/code-onboard

以后如果只修改某一个 Skill，只需要更新对应的独立仓库。`Chen_MCU_PIE` 不需要同步复制源码，也不需要跟随每个 Skill 的普通版本变更而提交更新。只有在新增/移除 Skill、调整组合说明或修改推荐工作流时，才需要更新这个收录仓库。

## 名称解释

Chen_MCU_PIE 的全称是 **MCU项目实施工程师(MCU project implementation engineer)**。

Chen_MCU_PIE并不是单纯的代码生成器，而是面向 MCU 和工程项目的 AI 实施流程助手：

- **MCU**：优先服务嵌入式 MCU、硬件驱动、RTOS、协议转换、调试验证等工程场景，同时也可复用于其他软件项目
- **project-frame**：先整理需求、参考资料、项目目标、约束和模块框架
- **stage-release**：按阶段实施、验证、更新文档并进行版本归档
- **code-onboard**：补充代码注释、快速上手 README 和长期维护所需的工程化信息

## 背景

在 AI 协作开发中，常见问题不是 AI 不会写代码，而是项目流程没有被固定下来，导致写出来的代码并非所想：

- 开始写代码前，需求、参考资料、约束条件没有被系统整理，开发毫无规程
- 项目推进过程中，AI 不知道当前处于哪个阶段，往往会干一些多余的事浪费时间和tokens
- 每次开发都依赖上下文记忆，缺少可长期读取的项目框架，关键信息在压缩后出现失真导致方向越来越模糊
- 阶段完成后，README、阶段说明和 Git tag 容易不同步，未做版本控制导致出现异常情况无法回滚
- 代码完成后缺少接手友好的注释和快速上手文档
- 硬件调试、用户人工操作、日志读取等验证方法没有固定记录

Chen_MCU_PIE 将这些流程拆成三个 Skill：

```text
project-frame   → 需求到动态项目框架
stage-release   → 阶段实施与版本归档
code-onboard    → 代码注释与快速上手 README
```

组合使用时，它可以形成一条完整的 AI 项目开发链路。

## 可以实现什么

Chen_MCU_PIE 可以帮助 AI 完成以下工作：

- 读取需求文件夹、主需求文档和参考资料文件夹
- 提炼项目目标、硬件/软件/工具链约束和用户特别提醒
- 生成可持续更新的项目框架 Markdown
- 将项目拆分成多个可验证阶段
- 每阶段按框架实施、验证、更新 README、输出阶段说明
- 对真实工程执行 commit/tag 版本归档
- 记录硬件调试、用户确认、日志读取等验证方法
- 阅读已有代码，为项目自有源码补充高价值注释
- 更新工程内部 `README.md`，让接手者快速理解项目

## 适用场景

- 嵌入式 MCU、硬件驱动、协议转换、RTOS 应用等工程
- 上位机工具、测试脚本、自动化工具、文档工程等需要阶段推进的项目
- 用户会在开发前准备需求文件夹和参考资料文件夹
- 项目希望按 `V0.1 / V0.2 / V0.3` 等阶段小步提交
- 项目需要长期维护，并希望 AI 每次接手时先读框架
- 项目完成后需要补充代码注释和快速上手 README

## 安装方式

`Chen_MCU_PIE` 本身用于说明和收录，不建议作为组合 Skill 源码包安装。请按需安装其中一个或多个独立 Skill。

安装 `project-frame`：

```powershell
帮我安装 https://github.com/705810790/project-frame.git 的skill
```

安装 `stage-release`：

```powershell
帮我安装 https://github.com/705810790/stage-release.git 的skill
```

安装 `code-onboard`：

```powershell
帮我安装 https://github.com/705810790/code-onboard.git 的skill
```

## 项目结构

```text
Chen_MCU_PIE/
└── README.md
```

本仓库只保留组合说明和独立仓库链接，不复制三个 Skill 的 `SKILL.md`、`README.md` 或 `agents/openai.yaml`。

## Skill 分工

| Skill | 作用 | 典型使用时机 |
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

需求文件夹中可以放：

- 主需求文档
- 背景说明
- 用户特殊要求
- 验收目标

参考资料文件夹中可以放：

- 数据手册
- SDK 示例
- 参考代码
- 调试日志
- 原理图或接口说明
- 旧版本项目资料

### 2. 生成项目框架

使用：

```text
使用 $project-frame，读取我的需求文件夹、主需求文档和参考资料文件夹，生成项目框架 md。
```

输出的框架会记录：

- 项目目标
- 需求来源
- 参考资料和复用策略
- 已知约束
- 模块拆分
- 调试和验证方法
- 阶段实现计划
- 文档和版本规则

### 3. 按阶段推进项目

使用：

```text
使用 $stage-release，按项目框架继续推进下一个阶段。
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

当代码形成稳定基线后，使用：

```text
使用 $code-onboard，阅读当前工程代码，补充注释，并更新工程 README.md。
```

它会重点处理：

- 项目自有源码
- 模块入口和公共 API
- 任务、ISR、回调、状态机
- 队列、事件、协议映射
- 关键硬件约束和调试点
- 工程内部快速上手 README

## 文档分层建议

推荐将外部项目管理文档和真实工程文档分开：

```text
外部项目管理区
├── 需求文档.md
├── 项目框架.md
└── 各阶段说明文档/
    ├── V0.1_阶段说明.md
    ├── V0.2_阶段说明.md
    └── 项目管理拆分及版本控制.md

真实工程区
├── README.md
├── src/ 或 User/
├── include/
└── 工程配置文件
```

规则：

- 项目框架是动态文档，阶段完成后与真实工程状态对齐
- 阶段说明只在阶段完成后生成，用于记录思路、验证和遗留问题
- 工程内部 `README.md` 跟随代码版本，面向接手开发者
- 严格 commit/tag 的对象通常是真实工程代码和工程内部 README
- 外部文档不需要每次临时修改都做版本管理

## 硬件调试和用户确认

Chen_MCU_PIE 支持将调试方法写入项目框架，例如：

- 串口工具
- OpenOCD / WCH-Link / J-Link
- 日志和诊断计数器
- USB 插拔、按键、观察屏幕等人工测试步骤
- Windows 提示框确认流程

当某个阶段需要用户人工操作硬件时，AI 可以弹出提示框列出测试步骤，等待用户点击“确定”后，再继续读取日志、计数器或设备状态。

提示框确认只用于测试步骤同步，不替代刷写、删除、安装依赖、提交、推送等风险操作的明确审批。

## 独立仓库

三个 Skill 也可以单独安装和使用：

- `project-frame`: https://github.com/705810790/project-frame
- `stage-release`: https://github.com/705810790/stage-release
- `code-onboard`: https://github.com/705810790/code-onboard

## 注意事项

- `Chen_MCU_PIE` 是收录仓库，不是三个 Skill 的源码同步仓库
- 单个 Skill 的修改只提交到它自己的独立仓库
- `project-frame` 不应盲目读取整个参考资料文件夹，应先列候选文件，再读取相关资料
- `stage-release` 每次执行阶段前必须先读项目框架
- `code-onboard` 不应修改第三方库、SDK、自动生成代码和编译产物
- 不要在 Skill 或 README 中写死个人工程路径
