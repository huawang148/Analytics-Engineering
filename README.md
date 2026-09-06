# 🚀 Analytics Engineer (AE) AI 时代极简学习指南

> **定位**：低精力、高杠杆、避开复杂运维与高压 On-Call 的 FIRE 防御型主业路线。
> **核心原则**：重视架构与业务逻辑，将重复性手写 SQL/代码交由 AI (Cursor/Claude) 完成。

---

## 🎯 核心中的核心：AI 最难替代的 3 项“高杠杆技能”

AI 时代，写 SQL 和 YAML 配置的边际成本趋近于零，但以下 3 项决策性技能是 AE 的顶级护城河：

1. **业务指标对齐与口径治理 (Metrics Governance & Semantic Layer)**
   - **核心价值**：AI 可以写出完美无瑕的 SQL，但它不知道你的公司“到底该怎么算钱”。将现实中模糊、混乱的业务口径，转化为精确、无二义性的数据模型，是 AE 最大的护城河。

重点学习与掌握：

定义“单一事实来源（Single Source of Truth）”：例如业务部门争论“客户留存率”到底是按 30 天自然日算，还是按自然月算？AE 需要协调并把最终口径固化到数据层。

语义层设计（Semantic Layer / Metric Layer）：学习如何使用 dbt Semantic Layer 或 MetricFlow 定义统一的指标（Metrics），让上游 BI 和 AI 智能体（Data Agents）调用数据时不会产生歧义。

数据溯源（Lineage）与边界认知：知道数据源头（如 Stripe 支付、Salesforce CRM、App 埋点）的各种奇葩异常（如退款导致负数、时区漂移），并提前在模型中做清洗。
2. **事实与维度的概念抽象 (Kimball Dimensional Modeling)**
   - **核心价值**：定义数据表的“颗粒度 (Grain)”，设计高解耦的星型模型，防止数据倾斜与笛卡尔积膨胀，为 AI 提效打下高质量底层结构。
   - 重点学习与掌握：经典 Kimball 维度建模：精通事实表（Fact Tables）与维度表（Dimension Tables）的设计，理解退化维、渐变维（SCD Type 1/2/3）的应用场景。这是数据仓库不变成“乱葬岗”的底层理论。分层架构设计（Medallion Architecture / Staging-Intermediate-Marts）：知道如何把原始数据干净地分层（Raw $\rightarrow$ Staging $\rightarrow$ Intermediate $\rightarrow$ Marts），确保中间层模型可以被极大复用。云数仓成本与性能调优：理解增量模型（Incremental Models）、分区（Partitioning）、聚簇（Clustering）以及虚拟仓库（Warehouse Size）的配置，用最少的计算资源跑完数据（这对公司来说是实打实的省钱）。
3. **数据链路安全与成本/性能干预 (FinOps & Data Observability)**
   - **核心价值**：优化云数仓计算成本（增量更新、分区），设计断路器测试防止脏数据污染下游，管控敏感数据权限（RLS/CLS）。
重点学习与掌握：

数据测试哲学（Data Testing）：熟练在 dbt 中编写 unique, not_null, relationships 以及断言测试（Singular Tests），确保上游数据异常时能自动拦截并报警。

AI 提示词工程与代码审查（AI Prompting & Code Review）：学会如何向 Cursor 或 Claude 提供足够的 Schema 和业务上下文，让 AI 帮你写出符合团队规范的 SQL，并能快速一眼看出 AI 生成的代码里存在的逻辑漏洞（如少写了 GROUP BY 导致的数据膨胀/Cartesian Product）。

数据安全与权限（RBAC & PII Masking）：理解敏感数据（如用户邮箱、电话）的脱敏与访问控制。
---

## 一、 技能图谱：重点 vs 交给 AI

| 技能模块 | 学习重点与考核标准 | 学习优先级 | 角色分工 |
| :--- | :--- | :--- | :--- |
| **1. 业务口径治理与语义层** | 指标定义拆解、dbt Semantic Layer / MetricFlow 语义模型配置 | 🌟🌟🌟🌟🌟 | **人类决策** (AI 辅助生成) |
| **2. Kimball 维度建模** | 颗粒度声明、事实表与维度表设计、星型模型、渐变维 (SCD) | 🌟🌟🌟🌟🌟 | **人类主导** (AI 辅助建议) |
| **3. 成本/性能与链路安全** | dbt 增量模型 (Incremental)、数据测试断路器、Snowflake 分区优化 | 🌟🌟🌟🌟☆ | **人类审查** (AI 提供方案) |
| **4. 高级 SQL & 逻辑审查** | 窗口函数 (Window Functions)、CTE、能快速识别 AI 代码里的逻辑错误 | 🌟🌟🌟🌟☆ | **人机协作** (AI 写，人审) |
| **5. AI 提示词工程** | 利用 Cursor / Claude 提供准确 Schema 与业务上下文，极速生成代码 | 🌟🌟🌟☆☆ | **人类指挥** |
| **6. 繁琐配置/死记硬背** | 复杂的语法细节、YAML 格式排版、正则表达式、底层运维脚本 | ❌ | **完全交给 AI** |

---

## 二、 4 周低功耗学习路线图

### 📅 第 1 周：SQL 逻辑演练与窗口函数
- **目标**：具备审查 AI 编写代码的能力，掌握高级查询。
- **核心任务**：
  - 攻克 `CTE (WITH 语句)` 和 `Window Functions (ROW_NUMBER, LEAD, LAG)`。
  - 在 DataLemur 或 StrataScratch 上每天刷 1–2 道 SQL Medium 题。
- **产出**：能够快速识别逻辑漏洞与性能瓶颈。

---

### 📅 第 2 周：维度建模理论 + 语义层概念
- **目标**：建立数据仓库“结构化审美”与指标治理意识。
- **核心任务**：
  - 阅读《The Data Warehouse Toolkit》（前 1–3 章，重点理解星型模型与颗粒度）。
  - 学习 dbt 官方指南：《How we structure our dbt projects》与 Semantic Layer 概念。
- **产出**：清晰掌握 Raw → Staging → Intermediate → Marts 数据分层。

---

### 📅 第 3 周：dbt + Snowflake 动手实操
- **目标**：掌握 AE 岗位的灵魂工具链。
- **核心任务**：
  - 注册 Snowflake 免费试用账号。
  - 完成 **dbt Learn 官方免费课程：`dbt Fundamentals`**。
  - 在 dbt 中编写 `models`、`schema.yml` 数据测试 (unique, not_null) 与增量策略。
- **产出**：跑通第一个完整的云端 dbt 转换与测试项目。

---

### 📅 第 4 周：AI 辅助 + GitHub Portfolio 项目
- **目标**：打造一份有说服力的 GitHub 作品集。
- **核心任务**：
  - 使用 Kaggle 公开数据集，配置 Cursor AI 辅助生成基础设施代码。
  - 手动设计维度表、事实表与 dbt 语义层 (Metrics)。
  - 将完整的 dbt 项目上传至 GitHub。
- **产出**：包含数据清洗、维度建模、测试断路器与 Lineage 图的开源项目。

---

## 三、 顶级免费学习资源清单

1. **维度建模**：《The Data Warehouse Toolkit》(Ralph Kimball 著，精读前 3 章)
2. **dbt 官方课程**：[dbt Learn - dbt Fundamentals](https://courses.getdbt.com/)（完全免费，含交互实操）
3. **语义层文档**：[dbt Semantic Layer Documentation](https://docs.getdbt.com/docs/use-dbt-semantic-layer/dbt-semantic-layer)
4. **SQL 刷题网站**：
   - [DataLemur](https://datalemur.com/) (针对 Data/AE 岗位的真实面试 SQL 题)
   - [StrataScratch](https://www.stratascratch.com/) (真实商业场景 SQL 练习)
5. **数仓体验**：[Snowflake Free Trial](https://signup.snowflake.com/) (提供 30 天免费额度)

---

## 四、 低精力 FIRE 族高效工作法则

1. **把 AI 当作“免费高级实习生”**：让 Cursor / Claude 编写长 SQL 和配置文件，你充当架构师与 Code Reviewer。
2. **拒绝“实时数据流”团队**：尽量选择基于 **批处理 (Batch/T+1)** 的数据团队，避开 7×24 实时 On-Call。
3. **模块化微深度工作**：利用 dbt 独立 Model 的特性，每天集中精力 60–90 分钟，按部就班推进，绝不强求长时间高强度烧脑。
