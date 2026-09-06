# Analytics-Engineering
Analytics Engineering related projects and resources

# 🚀 Analytics Engineer (AE) AI 时代极简学习指南

> **定位**：低精力、高杠杆、避开复杂运维与高压 On-Call 的 FIRE 防御型主业路线。
> **核心原则**：重视架构与业务逻辑，将重复性手写 SQL/代码交由 AI (Cursor/Claude) 完成。

---

## 🎯 核心中的核心：AI 最难替代的 3 项“高杠杆技能”

AI 时代，写 SQL 和 YAML 配置的边际成本趋近于零，但以下 3 项决策性技能是 AE 的顶级护城河：

1. **业务指标对齐与口径治理 (Metrics Governance & Semantic Layer)**
   - **核心价值**：消除部门间口径撕扯，将模糊业务需求转化为统一语义模型 (dbt Semantic Layer/MetricFlow)，确保 AI 和人类看到的指标完全一致。
2. **事实与维度的概念抽象 (Kimball Dimensional Modeling)**
   - **核心价值**：定义数据表的“颗粒度 (Grain)”，设计高解耦的星型模型，防止数据倾斜与笛卡尔积膨胀，为 AI 提效打下高质量底层结构。
3. **数据链路安全与成本/性能干预 (FinOps & Data Observability)**
   - **核心价值**：优化云数仓计算成本（增量更新、分区），设计断路器测试防止脏数据污染下游，管控敏感数据权限（RLS/CLS）。

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
