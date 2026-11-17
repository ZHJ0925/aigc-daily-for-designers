# 蚂蚁 Ant Design 团队 AI 实践启示：把设计体系做成 AI 可调用的上下文

> **来源说明**：蚂蚁设计系统站点文章 `https://antdesignsystem.alipay.com/article/antd-skill` 本次访问因连接关闭（ERR_CONNECTION_CLOSED）无法抓取正文，**不作为引用依据**。本文仅使用下方「可引用公开来源」表格所列的可核验渠道：GitHub 开源仓库、D20 分论坛公开转载与微信原文、ant.design 官方 For Agents 与 CLI 文档。

---

## 一、核心判断（三条，保持原意）

**判断一：重心在于「让 AI 读懂设计体系」，而非「让 AI 多画几张图」。**

蚂蚁 Ant Design 在 AI 方向的核心投入，不是提升 AI 生成界面的美观度，而是把设计体系里的规范、决策与约束——包括设计规则与资产、组件 API、Demo、Design Token、语义化结构，以及项目侧限制——整理成 AI 读得懂、调得动的上下文。

**判断二：B 端产品的真实价值在于「稳定的端到端交付」，而非「单次图像生成」。**

对大量 B 端产品而言，有意义的 AI 应用通常不是一次输出一张视觉稿，而是让 AI 同时理解设计体系与前端组件体系，在表单、列表、表格、图表等高度模式化的页面里，把「设计判断 → 组件实现」做成更稳定、可重复的端到端交付。

**判断三：UED 下一步的路在于「设计中央厨房」与「前端组件体系打通」的双向建设。**

若希望 AI 在 B 端系统中持续产生稳定价值，必须继续建设设计侧的「中央厨房」（可复用的规范、决策与资产供给），并进一步评估与前端组件体系打通的可行性——使 Token、API、Demo、语义结构可被同一套 Agent 工作流统一调用。

---

## 二、蚂蚁在做什么：两个方向，两个产品，请勿混称

蚂蚁在设计侧与工程侧分别推进，名称不同、定位不同，汇报中需明确区分。

### 2.1 设计侧：Ant Design Skill（官方设计团队出品）

| 项目 | 内容 |
|---|---|
| 产品名称 | **Ant Design Skill** |
| 出品方 | Ant Design 官方设计团队（公开报道提及设计负责人史凌超） |
| 核心定位 | 面向 AI 时代的设计系统表达与实践——把设计系统从「人理解的规范」升级为「AI 也能执行的设计能力」 |
| 对外提供 | ① 开箱即用的 Skill 技能包（按 Ant Design 规范生成界面）；② Design Skill 构建指南（从构建到测评的方法论与工具链）|
| 开源仓库 | https://github.com/AntGroupDesign/Ant-Design-Skill |
| 公开时间 | **2026-07-20**，D20 分论坛首次系统分享构建方法并同步开源 |
| 微信原文 | https://mp.weixin.qq.com/s/J6VDZK2ZDFheh9ymgL8n8A |
| 建设取舍 | 不追求一次覆盖全库；优先**高复用、形态稳定、且 AI 裸生成仍不理想**的场景：全局样式 / Design Token、复杂组件、布局与导航 |

【配图1：Ant Design Skill GitHub 开源仓 README 首页】  
*编辑建议：放截图 + 附链接脚注，一图即可说明「面向 AI 的设计系统表达」这一定位。*

公开材料的关键洞察可概括如下：

- AI 已能读到组件、Token、代码等「静态资产」，但往往缺少设计师式的决策链：**为什么用这个组件、何时用、如何用、多个选项如何取舍**。
- 因此需要在 Design Assets（资产层）之上，再建一层更适合 AI 调用的 **Design Skills**（能力层），涵盖意图、触发条件、策略与资产的组合，而不是靠「多生成几次」绕过规范缺失。
- 评价一个有效 Skill 的标准包括：场景触发稳定、覆盖核心业务、显著提升生成质量、输出符合预期方案。
- 关键词：**确定性、生长性、开放性**；并明确强调 **Design Skill ≠ 取代设计师**——可复用的判断交给 AI 执行，创新决策与新模式仍属设计师，设计师的角色同时也是 Skill 的构建者。

【配图2：D20/微信原文中「Design Assets → Design Skills」双层关系示意图】  
*编辑建议：若能拿到原图截图优先；如无法获取，可用文字框图复述「资产层 + 能力层」结构。*

---

### 2.2 工程侧：For Agents 与 `@ant-design/cli`（官方组件库 Agent 能力）

与设计 Skill 并行，Ant Design 工程文档同样明确面向 Agent 提供可调用上下文，名称与出品侧均不同，**汇报中请分开表述**。

| 能力 | 对「打通组件体系」的意义 |
|---|---|
| `@ant-design/cli` | 本地离线查询组件 props、Token、Demo、changelog、语义结构（classNames / styles）等，无需网络即可入 Agent 上下文 |
| `design.md` | 给 AI 设计工具提供视觉语言 / 组件原型 / 主题 Token 描述 |
| MCP Server | 在 Claude Code、Cursor、VS Code 等 IDE 内工具化调用 |
| LLMs.txt 等 | 结构化文档直接进入模型上下文，降低幻觉选型 |
| `ant-design/antd-skill`（另一仓库） | 面向 Agent 的 antd / Pro / X 决策类 Skill，侧重工程选型，**与设计侧 AntGroupDesign/Ant-Design-Skill 不同仓、不同产品** |

官方文档入口：

- For Agents 页面：https://ant.design/docs/react/for-agents/
- CLI 文档：https://ant.design/docs/react/cli/

【配图3：ant.design For Agents 页（CLI / design.md / MCP / LLMs.txt 四块并列）】  
*编辑建议：放截图 + 链接脚注——这一页能一眼说明「组件 API / Demo / Token / 语义结构均可被 Agent 调用」。*

---

## 三、对 B 端产品意味着什么

B 端页面高度模式化：筛选 + 表格 + 表单 + 详情 + 图表，几乎覆盖了 80% 以上的常规业务场景。若 AI 只擅长「输出一张视觉稿」，交付链路在规范一致性、组件选型、状态完整性、可开发性上仍会持续返工。

蚂蚁路径提供的对照参考：

1. **设计侧**把「专业决策」写进 Skill，从源头减少「会画但不会选」带来的规范噪声；
2. **工程侧**把 API / Token / Demo / 语义结构做成可查询上下文，减少「会选但落不对组件」的实现噪声；
3. 两端靠近后，才更接近用户所说的「标准化页面上的稳定端到端交付」。

这与「中央厨房」隐喻高度一致：厨房的价值不在多炒一盘样菜，而在**统一备料、统一刀工、统一出餐标准**，让前端工程师与 AI Agent 都能基于同一套料完成各自的工作。

---

## 四、对 UED 的启示与建议动作

### 4.1 继续建设设计「中央厨房」

不止于沉淀 Figma 组件库与文档站，还需要把「场景触发条件、决策策略、选用约束、反例」等判断性内容，整理为 AI 可执行的单元（Skill / 规则包），优先覆盖 B 端高复用的模式页（筛选表格、多步表单、嵌套布局等）。

### 4.2 评估与前端组件体系打通（建议列入下一步议题）

具体评估方向：

- 我方 Design Token 与前端组件 Token 是否同源或可映射；
- Figma 设计模板与前端 Demo 是否可被同一 Agent 工作流引用；
- 设计 Skill 的输出能否直接对应到现有组件库的具体组件，而非只导出静态图层；
- 是否适合引入 CLI / MCP / LLMs.txt 一类工程接口，作为「中央厨房」面向 AI 工具链的标准化供应出口。

### 4.3 角色叙事定位（可作收束）

蚂蚁公开材料明确表述：设计师应从「结果生产者」更多转向「规则与 Skill 的构建者」——可复用的模式与判断交由 AI 执行，设计师专注于新决策与新模式。这与 UED 建设中央厨房的组织叙事一致，可酌情引用于汇报收尾，注意避免写成「AI 替代设计」的悲观框架。

---

## 五、可引用公开来源与配图建议

| 来源 | 时间 | 产品 / 对象 | URL | 建议 |
|---|---|---|---|---|
| Ant Design Skill 开源仓 README | 持续更新（仓库已公开） | Ant Design Skill（设计侧） | https://github.com/AntGroupDesign/Ant-Design-Skill | **链接 + 截图** |
| D20 分论坛公开转载 | 2026-07-20 | Ant Design Skill / Design Skill 构建方法 | http://www.mysecretrainbow.com/blog/35410.html | 链接；关键图示可截图补充 |
| 微信原文（分享方标注） | 2026-07-20（同场） | 同上 | https://mp.weixin.qq.com/s/J6VDZK2ZDFheh9ymgL8n8A | **优先放链接**（内网汇报可截关键段） |
| Ant Group Design AI Lab 入口 | — | 设计系统 / AI Lab 总站 | https://antdesignsystem.alipay.com/ | 链接；⚠️ `/article/antd-skill` 本次访问受限，正文**无法核验，不引用** |
| ant.design For Agents 官方文档 | 文档页（官方维护） | CLI / design.md / MCP / LLMs.txt（工程侧） | https://ant.design/docs/react/for-agents/ | **链接 + 截图** |
| ant.design CLI 官方文档 | 文档页（官方维护） | `@ant-design/cli`（工程侧） | https://ant.design/docs/react/cli/ | 链接；需技术附录时再补截图 |
| ant-design/antd-skill 仓库 | 仓库创建约 2026-01-29 | Agent 决策 Skill（工程侧，另一仓库） | https://github.com/ant-design/antd-skill | 链接；需注明与设计 Skill **不同仓、不同产品** |

**编辑备注**

- **alipay 文章不可用**：`https://antdesignsystem.alipay.com/article/antd-skill` 本次连接关闭，正文无法核验，本文未引用其内容，汇报中不得以该 URL 为依据。
- **产品名称区分**：设计侧统一写 **Ant Design Skill**（`AntGroupDesign/Ant-Design-Skill`）；工程侧写 **`@ant-design/cli` / For Agents / design.md / MCP**；`ant-design/antd-skill` 是第三个独立实体，三者请勿合并为同一名称。
- **时间锚点**：以 D20 公开分享 **2026-07-20** 为设计 Skill 的主时间锚点；工程侧 For Agents / CLI 以官方文档页为准，**不虚构发版日期**。
- **配图策略**：对外汇报建议「关键页截图 2～3 张 + 来源链接脚注」并存；密级较高材料可只保留链接与文字引用。

---

*本文可直接粘贴进汇报；【配图N】为占位符，配图就绪后逐一替换即可。*
