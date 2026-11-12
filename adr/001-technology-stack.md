# ADR 001：技术栈选型对比框架

> 状态：**Proposed（提议，待团队评审）** · 日期：2026-11-11 · 决策者：团队（待定）
> 本文**不是已定方案**。按 `context.md` 第 8 节与 `agent-rules.md` 第 4 节，技术栈在团队确认前不得写成已落地事实，也不得据此生成脚手架或引入依赖。
> 目的：把课程进度表「主要框架/技术平台」一列从"未定"推进到"有候选"，并为 `docs/spike/` 探针提供验证目标。最终选型确认后状态改为 Accepted，再同步更新 `context.md` 与进度表。

## 1. 背景与约束

FitNourish MVP1 共 9 个模块、三种角色、两类 AI 草稿。已确认的硬约束（来自 `context.md` 第 8 节、`spec/mvp1-scope.md` 第 3.1 节）：

- Web 应用方向（建议，非强制）。
- 三种角色 + 权限由**服务端**判定（不能只靠隐藏前端按钮）。
- 两类 AI 草稿（训练计划、饮食建议），AI 请求由**后端**发起；密钥不下发浏览器、不进仓库、不进日志。
- 数据需支持"已发布版本不被新周期覆盖"（历史一致性）。
- 演示用虚构数据，不写入真实隐私。
- 课程项目：周期短、团队小、需可演示；AI 调用预算待定。
- 本周不写业务代码、不生成脚手架。

仍待确认（不阻塞本对比，但阻塞最终选型）：团队技术熟悉度、AI 调用预算、部署环境、课程节点与评审要求。

## 2. 评估维度

| 维度 | 说明 | 建议权重 |
| --- | --- | --- |
| 团队熟悉度 | 能否在一周内上手并产出可演示代码 | 高 |
| AI 集成成本 | 后端调用 AI、超时重试、密钥管理的实现量 | 高 |
| 权限实现 | 服务端按"角色 + 指导关系"判定的难度 | 高 |
| 数据与版本 | 计划/建议 草稿→已发布、历史不覆盖的实现难度 | 中 |
| 演示与部署 | 本地起服务、演示数据初始化的成本 | 中 |
| 费用与许可 | 框架/数据库/AI 调用的费用与开源许可 | 中 |
| 类型安全与协作 | 前后端类型共享、多人协作摩擦 | 低-中 |

## 3. 候选方案

下列每个候选都给出用途、成本与替代（按 `context.md` 第 163 行"新增依赖或外部服务应说明用途、成本及替代方案"）。三者均为 Web 应用，差异在语言生态与团队取向。

### 方案 A：React + FastAPI（Python）+ SQLite/PostgreSQL + DeepSeek

- 前端：React 18 + TypeScript + Vite + Tailwind CSS
- 后端：Python 3.11+ / FastAPI + Pydantic + SQLModel（或 SQLAlchemy）
- 数据库：开发用 SQLite，生产用 PostgreSQL
- AI：DeepSeek（OpenAI 兼容口）
- 认证：JWT，服务端签发与校验

| 项 | 用途 | 成本/许可 | 替代 |
| --- | --- | --- | --- |
| FastAPI | 异步、轻量，与 AI HTTP 调用契合 | MIT | Flask、Django |
| SQLite | 演示零配置 | 公有领域 | PostgreSQL |
| DeepSeek | 国内可直连、OpenAI 兼容、成本低 | 按量计费 | 智谱 GLM、通义千问 |

- **优势**：Python 调 AI 生态成熟、起步快、SQLite 便于演示。
- **风险**：前后端类型不共享需手动对齐；SQLite 并发与权限细节需在 Spec 层验证；Python 部署相对 Java 略繁。

### 方案 B：Vue 3 + Spring Boot（Java）+ MySQL + DeepSeek

- 前端：Vue 3 + Vite + TypeScript + Pinia + Element Plus
- 后端：Java 21 + Spring Boot 3.x + Spring Security + MyBatis-Plus
- 数据库：MySQL 8
- AI：DeepSeek（OpenAI 兼容口）
- 认证：Spring Security + JWT

| 项 | 用途 | 成本/许可 | 替代 |
| --- | --- | --- | --- |
| Spring Boot | 企业级、类型安全、Security 模块成熟 | Apache 2.0 | Quarkus |
| Element Plus | 后台管理风格组件齐全，契合教练/管理员界面 | MIT | Ant Design Vue |
| MySQL | 事务与权限成熟 | GPL/商业 | PostgreSQL |

- **优势**：类型安全、权限/事务成熟、组件库契合管理后台。
- **风险**：Java 启动与内存占用偏大、学习成本高、AI 调用需借 HTTP 客户端而非原生生态。

### 方案 C：React + NestJS（TypeScript 全栈）+ PostgreSQL + DeepSeek

- 前端：React 18 + TypeScript + Vite + Tailwind CSS
- 后端：Node.js 20+ / NestJS + TypeScript + Prisma
- 数据库：PostgreSQL
- AI：DeepSeek（OpenAI 兼容口）
- 认证：JWT + Passport

| 项 | 用途 | 成本/许可 | 替代 |
| --- | --- | --- | --- |
| NestJS | 模块化、TypeScript 原生、可与前端共享类型 | MIT | Express、Fastify |
| Prisma | 类型安全 ORM、迁移清晰 | Apache 2.0 | TypeORM |

- **优势**：全栈 TypeScript、类型共享、前后端协作摩擦最小。
- **风险**：Node 调 AI 与并发处理需验证；ORM 生态不如 Java 成熟；团队需熟悉 NestJS 约定。

## 4. AI 服务商对比

| 服务商 | 接入方式 | 成本 | 国内可用 | 替代 |
| --- | --- | --- | --- | --- |
| DeepSeek | OpenAI 兼容 HTTP | 低，按量 | 是 | 智谱 GLM、通义千问 |
| 智谱 GLM | 自有 SDK/HTTP | 低-中 | 是 | DeepSeek |
| 通义千问 | 自有 SDK | 中 | 是 | DeepSeek |
| OpenAI | 官方 SDK | 高，需代理 | 否（需代理） | DeepSeek |

建议先用 DeepSeek 做探针：OpenAI 兼容口便于在费用或可用性不达标时切换到智谱/通义，无需大改后端。具体模型与单次调用预算待 `docs/spike/` 验证后填入。

## 5. 建议的探针（docs/spike/）

按 `agent-rules.md` 第 2 节，探针放 `docs/spike/`，不得描述为正式功能：

- `spike-01-ai-contract.md`：用 DeepSeek 跑一次训练计划草稿生成，记录输入字段、输出结构、校验规则、超时与重试、单次费用，验证能否满足 M04 的 AC-04-01 / 03 / 04。
- `spike-02-permission.md`：在选定后端框架上验证"学员绕过界面直请求被服务端拒绝"（AC-01-05 / 06），确认权限不是只靠前端隐藏。
- `spike-03-versioning.md`：验证计划/建议的草稿→已发布与历史不覆盖（AC-03-06 / AC-05-06 / AC-08-07）。

探针须写明输入、配置、结果与结论边界，不把模拟返回显示为真实生成成功。

## 6. 建议倾向（非定论）

- 若团队对 Python 熟悉、重视快速演示：**方案 A**。
- 若团队对 Java/Spring 熟悉、重视类型安全与管理后台：**方案 B**。
- 若团队希望全栈 TypeScript、前后端同语言：**方案 C**。

**本节是建议倾向，不是决策。** 任何最终选型须经团队评审，状态 Proposed → Accepted 后，再更新 `context.md` 第 8、12 节、课程进度表「主要框架/技术平台」列，并据此生成脚手架与依赖清单。

## 6.1 团队评审结论（2026-11-11）

- 倾向**方案 B**（Vue 3 + Spring Boot + MySQL + DeepSeek），以此方向执行第 5 节探针。
- 状态仍为 **Proposed**：探针验证关键风险（AI 契约、服务端权限、历史版本不覆盖）后，状态改为 Accepted，并更新 `context.md` 第 8、12 节与课程进度表。
- 若探针证明 B 不可行，回到本 ADR 重选 A 或 C，不得直接改 `context.md`。
- 探针执行模板已起草：`docs/spike/spike-01-ai-contract.md`、`spike-02-permission.md`、`spike-03-versioning.md`（均针对方案 B，状态待执行）。

## 7. 不在本 ADR 范围

- 业务规格与 AC（已在 `spec/`）。
- 指导关系建立规则、餐食照片等业务待确认项（在 `spec/mvp1-scope.md` 第 9 节）。
- 具体接口路径、表结构、部署脚本（选型确认后另定，不在 Spec 与本 ADR 中预先规定）。

## 8. 后续步骤

1. 团队评审本 ADR，确认第 2 节评估权重与第 3 节候选范围。
2. 执行第 5 节探针，把结果与结论边界写入 `docs/spike/`。
3. 据探针结果选定方案，状态 Proposed → Accepted。
4. Accepted 后更新 `context.md` 第 8、12 节与课程进度表；按 `agent-rules.md` 第 7 节经授权后建仓库与脚手架。
5. 选型若变更，重开本 ADR 或新增后续 ADR，不得直接改 `context.md`。
