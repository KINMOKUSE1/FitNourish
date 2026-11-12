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

MVP1 的最小范围已锁定在 [spec/mvp1-scope.md](spec/mvp1-scope.md)（基线 v1.0，九个模块各有一份可测试 Spec）。`context.md` 第 5 节仍是业务边界主文档：

- [范围总览](context.md#51-范围总览)：MVP1 九大模块及第一版包含的能力。
- [FitNourish 功能树](context.md#52-fitnourish-功能树)：展开训练、AI 训练构建、AI 营养指导、反馈、学员管理与基础管理。
- [角色与模块对应](context.md#53-角色与模块的对应关系)：说明学员、教练、管理员分别参与哪些操作。

以上均为待实现的 MVP1 范围；指导关系的具体建立方式和餐食照片上传仍待确认，见 [spec/mvp1-scope.md](spec/mvp1-scope.md) 第 9 节。

## 当前阶段

上一阶段完成了项目上下文、协作规则、标准目录与 PR 模板。本周（2026-11-11）锁定 MVP1 最小范围，为九个模块各写一份 Given/When/Then 可测试 Spec，并完成一次冷启动校验；交付物见 [文档导航](#文档导航) 与 [本周交付](#本周交付与-github-准备)。

**本周仍不写业务代码**：`src/` 保持空占位，尚未实现任何业务功能，技术栈、数据库与 AI 服务商待确认，当前没有运行命令或部署入口。

远端仓库、GitHub Projects、Issue 和演练 PR 均待建立；看板链接待创建后补充。

## 文档导航

| 入口 | 职责 |
| --- | --- |
| [context.md](context.md) | 项目目标、角色、MVP、非目标、技术约束和待定项 |
| [agent-rules.md](agent-rules.md) | 人与 AI 的协作、范围、验证及 Git 规则 |
| [spec/mvp1-scope.md](spec/mvp1-scope.md) | MVP1 范围基线、九个模块编号、AC 写法约定与虚构演示数据 |
| [spec/ 模块 Spec](spec/) | M01–M09 各自的可测试 Spec 与 Given/When/Then 编号验收标准 |
| [docs/test/cold-start-01.md](docs/test/cold-start-01.md) | 本周冷启动校验的提示词、实际结果、文档缺口与复验结论 |
| [adr/001-technology-stack.md](adr/001-technology-stack.md) | 技术栈对比框架（Proposed，待团队评审） |
| [adr/](adr/) | 后续重要技术决策及依据 |
| [plans/](plans/) | 后续任务拆解、依赖和 Issue 关联 |
| [docs/spike/](docs/spike/) | 必要技术探针与结果 |
| [PR 模板](.github/PULL_REQUEST_TEMPLATE.md) | 变更、验证、AI 使用和评审信息 |

开始协作时，请明确要求 AI 读取 `context.md`、`agent-rules.md`、`spec/mvp1-scope.md` 以及当前任务对应的模块 Spec。

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
│   ├── mvp1-scope.md
│   └── module-01 … module-09-*.md
├── adr/
├── plans/
├── src/
├── tests/
└── docs/
    ├── spike/
    └── test/
        └── cold-start-01.md
```

空目录中的 `.gitkeep` 仅用于 Git 保留目录。当前不生成业务脚手架；前后端目录及启动方法在技术栈确定并实际实现后补充。

## 本周交付与 GitHub 准备

| 交付物 | 本地内容或后续入口 |
| --- | --- |
| 项目全局边界 | `context.md` |
| AI 规则文件 | `agent-rules.md` |
| MVP1 范围锁定 | [`spec/mvp1-scope.md`](spec/mvp1-scope.md) |
| 九份可测试模块 Spec | [`spec/`](spec/)（M01–M09，Given/When/Then 编号 AC） |
| 冷启动校验记录 | [`docs/test/cold-start-01.md`](docs/test/cold-start-01.md) |
| 标准化仓库 | 本目录结构、README 和忽略规则 |
| GitHub Projects 看板 | 待创建；创建后在本节补充链接 |
| 无业务代码演练 PR | 待创建；创建后在本节补充链接 |

看板状态沿用课程要求：`Backlog → This Week → In Progress → Review → Done`。远端建立后，任务状态以看板为准。

以下为上一阶段（基础建设周）遗留的待录入 Issue 草案，不表示 GitHub 上已经存在对应任务。负责人由团队分配；本周已有 Spec，新建 Issue 的关联规格栏应引用 `spec/mvp1-scope.md` 及对应模块 Spec。

| Issue 标题 | 验收标准 |
| --- | --- |
| 编写 FitNourish 项目上下文 | 明确目标、三角色、MVP、至少三条可判定 Non-Goals、技术约束和风险；待定事项单列；完成范围评审 |
| 编写 AI 协作规则 | 明确读取入口、修改范围、AI 发布边界、验证与 Git 权限；规则可执行、可检查 |
| 初始化标准仓库结构 | 目录与课程要求一致；README 链接有效；无业务代码和密钥；完成本地结构检查 |
| 建立项目看板 | 设置五种状态；录入本周 Issue，指定负责人并关联看板 |
| 完成无业务代码 PR 演练 | PR 关联 Issue；填写变更、验证及 AI 使用说明；包含实际评审意见；变更仅涉及文档、结构及配置 |

每个 Issue 正文包含：业务背景、任务范围、验收标准、关联规格或本周文档、负责人。

### 本周（Spec 与冷启动）Issue 草案

| Issue 标题 | 验收标准 |
| --- | --- |
| 锁定 MVP1 最小范围并编写范围基线 | `spec/mvp1-scope.md` 明确 In/Out of Scope、九个模块编号、角色矩阵、AC 写法约定与待确认项；范围可判定且与 `context.md` 一致 |
| 为 MVP1 全部模块编写可测试 Spec | 九个模块各一份 Spec；每条 AC 使用 Given/When/Then 并带类型标注；覆盖正常流、异常流、权限边界；M04/M05 含 AI 失败，M03/M05/M08 含历史一致性 |
| 完成一次冷启动校验 | `docs/test/cold-start-01.md` 记录提示词、逐题实际结果、发现的问题及复验结论；不把未执行的校验写成已完成 |
| 同步文档导航并修复失效链接 | README 锚点与 `context.md` 实际章节一致；导航指向本周交付物；变更仅涉及文档、目录和配置 |

### 演练 PR 草案（上一阶段，保留备查）

建议标题：`chore: initialize FitNourish project context and repository structure`

- 关联任务：填写实际 Issue 编号，不使用虚构编号。
- 变更内容：增加项目上下文、AI 协作规则、README、标准目录、忽略规则和 PR 模板。
- 验证方式：检查文档一致性、本地链接、目录完整性、业务目录占位及敏感信息。
- AI 使用说明：AI 根据已确认的项目范围起草文档和结构；团队人工评审业务边界及协作规则。
- 评审关注点：三角色权限、两类 AI 草稿的确认发布机制、MVP 与 Non-Goals、待定项是否完整。

执行顺序：创建远端仓库和看板 → 建 Issue → 用户审阅并提交本地变更 → 推送任务分支 → 将任务移入 Review → 创建关联 Issue 的 PR → 人工评审。Git 操作需另行明确授权，或由用户通过 GitHub Desktop 执行。

## 后续文档规划

以下文件尚未创建，在对应阶段逐步完善：

- `plans/mvp1.md`：依据确认后的规格、设计和决策拆解任务。
- `docs/spike/`：技术探针，记录 AI 输入输出结构、校验、超时与重试的验证结论。已起草 `spike-01/02/03` 执行模板（针对方案 B，待执行），首批建议见 [`adr/001-technology-stack.md`](adr/001-technology-stack.md) 第 5 节。
- 各模块 Spec 第 7 节的待确认项：确认后在原模块文件内细化，不另建重复文档。

早期规划中的 `spec/coaching-relationship.md`、`spec/training-plan.md`、`spec/nutrition-guidance.md`、`spec/execution-feedback.md` 四个分主题文件，其内容已由 [`spec/mvp1-scope.md`](spec/mvp1-scope.md) 与 M01–M09 九份模块 Spec 覆盖，不再单独创建，避免维护两份内容。

## 参考资料

- [ABC Trainerize](https://www.trainerize.com/)：产品参考。
