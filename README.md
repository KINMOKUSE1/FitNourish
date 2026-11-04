# FitNourish

**AI-Assisted Fitness and Nutrition Coaching System**

软件工程课程项目：帮助教练借助 AI 制定训练与饮食方案，并通过学员执行记录和反馈持续调整指导。

## 用户与核心流程

系统包含学员、教练、管理员三种角色。AI 为教练提供辅助能力，不作为第四种用户角色。

```text
学员完善档案 → 教练生成或编写方案草稿 → 教练确认发布
    → 学员执行并记录 → 教练反馈 → 调整下一周期计划
```

训练及饮食 AI 草稿均由教练确认后发布。

## 功能树与范围对照

完整功能树集中维护在 `context.md` 第 5 节：

- [MVP1 范围总览](context.md#51-范围总览)：第一版各模块包含的能力。
- [FitNourish 功能树](context.md#52-fitnourish-功能树)：展开训练、AI 训练构建、AI 营养指导、反馈、学员管理与基础管理。
- [角色与模块对应](context.md#53-角色与模块的对应关系)：说明学员、教练、管理员分别参与哪些操作。

以上是待实现的 MVP1 范围；指导关系的具体建立方式和餐食照片上传仍待确认。

## 当前阶段

本周为项目上下文与协作基础建设阶段。本地已建立上下文、规则、标准目录和 PR 模板；尚未实现业务功能，技术栈和 AI 服务商待确认。

[GitHub 仓库](https://github.com/KINMOKUSE1/FitNourish)和[课程看板](https://github.com/users/KINMOKUSE1/projects/3)已建立，本周五条 Issue 已录入；文档与结构通过 `chore/project-bootstrap` 分支提交评审。当前没有运行命令、部署入口或已完成业务功能。任务进度以看板为准。

## 文档导航

| 入口 | 职责 |
| --- | --- |
| [context.md](context.md) | 项目目标、角色、MVP、非目标、技术约束和待定项 |
| [agent-rules.md](agent-rules.md) | 人与 AI 的协作、范围、验证及 Git 规则 |
| [spec/](spec/) | 后续功能规格与验收标准 |
| [adr/](adr/) | 后续重要技术决策及依据 |
| [plans/](plans/) | 后续任务拆解、依赖和 Issue 关联 |
| [docs/spike/](docs/spike/) | 必要技术探针与结果 |
| [PR 模板](.github/PULL_REQUEST_TEMPLATE.md) | 变更、验证、AI 使用和评审信息 |

开始协作时，请明确要求 AI 读取 `context.md`、`agent-rules.md` 和当前任务相关文件。

## 标准目录

```text
FitNourish/
├── README.md
├── context.md
├── agent-rules.md
├── .gitignore
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md
├── spec/
├── adr/
├── plans/
├── src/
├── tests/
└── docs/
    └── spike/
```

空目录中的 `.gitkeep` 仅用于 Git 保留目录。当前不生成业务脚手架；前后端目录及启动方法在技术栈确定并实际实现后补充。

## 本周交付与 GitHub 准备

| 交付物 | 本地内容或后续入口 |
| --- | --- |
| 项目全局边界 | `context.md` |
| AI 规则文件 | `agent-rules.md` |
| 标准化仓库 | 本目录结构、README 和忽略规则 |
| GitHub Projects 看板 | [FitNourish — Course Project](https://github.com/users/KINMOKUSE1/projects/3) |
| 无业务代码演练 PR | 本次任务分支将发起演练 PR，创建后补充链接 |

看板状态沿用课程要求：`Backlog → This Week → In Progress → Review → Done`。远端建立后，任务状态以看板为准。

以下任务已建立真实 Issue，当前负责人为 `@KINMOKUSE1`。文档此前已在本地起草，本次导入仓库并开展评审，不追溯改写执行时间。本周尚无 Spec，Issue 引用本周文档。人工评审尚未完成。

| Issue 标题 | 验收标准 |
| --- | --- |
| [#1 编写 FitNourish 项目上下文](https://github.com/KINMOKUSE1/FitNourish/issues/1) | 明确目标、三角色、MVP、至少三条可判定 Non-Goals、技术约束和风险；待定事项单列；完成范围评审 |
| [#2 编写 AI 协作规则](https://github.com/KINMOKUSE1/FitNourish/issues/2) | 明确读取入口、修改范围、AI 发布边界、验证与 Git 权限；规则可执行、可检查 |
| [#3 初始化标准仓库结构](https://github.com/KINMOKUSE1/FitNourish/issues/3) | 目录与课程要求一致；README 链接有效；无业务代码和密钥；完成本地结构检查 |
| [#4 建立项目看板](https://github.com/KINMOKUSE1/FitNourish/issues/4) | 设置五种状态；录入本周 Issue，指定负责人并关联看板 |
| [#5 完成无业务代码 PR 演练](https://github.com/KINMOKUSE1/FitNourish/issues/5) | PR 关联 Issue；填写变更、验证及 AI 使用说明；包含实际评审意见；变更仅涉及文档、结构及配置 |

每个 Issue 正文包含：业务背景、任务范围、验收标准、关联规格或本周文档、负责人。

### 演练 PR 草案

建议标题：`chore: initialize FitNourish project context and repository structure`

- 关联任务：填写实际 Issue 编号，不使用虚构编号。
- 变更内容：增加项目上下文、AI 协作规则、README、标准目录、忽略规则和 PR 模板。
- 验证方式：检查文档一致性、本地链接、目录完整性、业务目录占位及敏感信息。
- AI 使用说明：AI 根据已确认的项目范围起草文档和结构；团队人工评审业务边界及协作规则。
- 评审关注点：三角色权限、两类 AI 草稿的确认发布机制、MVP 与 Non-Goals、待定项是否完整。

执行顺序：创建远端仓库和看板 → 建 Issue → 用户审阅并提交本地变更 → 推送任务分支 → 将任务移入 Review → 创建关联 Issue 的 PR → 人工评审。Git 操作需另行明确授权，或由用户通过 GitHub Desktop 执行。

## 后续文档规划

以下文件尚未创建，在对应阶段逐步完善：

- `spec/coaching-relationship.md`：指导关系和数据权限。
- `spec/training-plan.md`：训练计划及 AI 生成、编辑、确认、发布流程。
- `spec/nutrition-guidance.md`：饮食指导及 AI 草稿流程。
- `spec/execution-feedback.md`：执行记录、反馈、历史关联与进度。
- `adr/001-technology-stack.md`：有依据地比较并确定技术栈。
- `plans/mvp1.md`：依据确认后的规格、设计和决策拆解任务。

## 参考资料

- [ABC Trainerize](https://www.trainerize.com/)：产品参考。
- 课程《06 AI 原生项目管理与上下文构建》及本周交付截图：目录结构与协作交付要求。课件保存在课程资料会话中，未复制进入仓库。
