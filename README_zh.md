[English](./README.md) | **简体中文**

# Hi, I'm Zhenrui Zheng (CH4AcKO3) 👋

- 🌱 我目前是香港中文大学（深圳）在读博士
- 🔭 我的研究兴趣很广泛，比较熟悉的有：生成模型、强化学习、Agent 系统等。
- 🌈 我也对开发具有兴趣，尤其是游戏开发、算法优化、自动化系统、Infra。

## 研究与技术栈

我能在无 AI 辅助的情况下：

- **研究：** 「生成模型」 · 「扩散模型」 · 「强化学习」 · 「离线学习」
- **Agent Systems：** 「Local Agent Runtime」 · 「Multi-Agent Orchestration」 · 「Agent Protocol」 · 「Tool & Skills & Memory Systems」
- **Agent Infra：** 「Persistent Context & Session」 · 「Authorization」 · 「Sandboxing」 · 「Lifecycle」
- **编程语言：** 「C/C++」 · 「Python」 · 「Rust」 · 「Lean」
- **前端：** 「HTML」 · 「CSS」 · 「Vue」 · 「React」
- **Tooling：** 「Node.js」 · 「pnpm」 · 「uv」 · 「Vite」

我能在 AI 辅助下：

- **编程语言：** 「JavaScript/TypeScript」 · 「C#」

## 项目

### Agent Systems

**[Frontal-Lobe: Modern MCP-based Meta Harness Framework](https://github.com/CH4AcKO3/Frontal-Lobe)**

这是一个使用 Rust 开发的、基于 Modern MCP 协议的分布式 Harness 框架，设计理念是将传统单体式的本地嵌入 Agent App，转换为去中心化的、以微服务的形式构建的服务集群。每个 Agent、Tool、Provider 以提供服务的方式实现沟通，并在此基础上构建更复杂的应用。这个框架严格实现了一致性模型、事务模型，确保不可靠环境中的稳定性。~~在项目进入发布阶段时被定位相同的 DeepSeek Harness 撞飞了，但是已经实现了一系列有趣的功能，并最终决定迁移到 DSH 上：[Frontal Lobe Preview](https://icn07qje5tl4.feishu.cn/wiki/NLGAwkXpsicdGgk6hnoc0vRknDf?from=from_copylink)~~

**[dsh-harmony: A library for patching, replacing and decorating dsh plugin during runtime](https://github.com/memorax-ai/dsh-harmony)**

为 DeepSeek Harness 设计并开发的插件运行时热补丁框架，基本原理是让补丁定义 AST 查询与替换语法，实现运行时对插件编译后的 JavaScript 源码的 Patching，为 DSH 框架补上了插件不可热修改的缺口。背后实际有比较多的工程问题与解决技巧，例如补丁冲撞的解决、启动时 AST 查询的效率问题等。

> 对于补丁冲撞，采用1.以迭代 Tarjan 算法分解强连通分量；对不超过 14 个节点的循环分量，使用 $O(k^2 2^k)$ 的子集 DP 求出违例数最少的顺序，并以相对原顺序的逆序数作为 tie-break；2.对更大的循环分量，则采用反复剥离 source/sink、并在剩余节点中选择最大 `out-degree - in-degree` 的 feedback-arc heuristic，将指数搜索限制在小分量内，最后通过稳定的 Kahn 拓扑排序合并结果。

> 对于 AST 查询-替换，将 TSQuery selector 编译为查询计划，以 SyntaxKind 和等值属性索引选择候选数最少的锚点；为 AST 子树计算双 32-bit Merkle hash，并将 selector 与子树 hash 映射为可复用的相对节点定位；通用 selector 则在缓存键中加入祖先、兄弟与位置等上下文指纹。源码发生小规模变动时，系统按需增量更新并复用原 AST 索引。多线程 preflight 则使用并查集，按共享目标文件将 Patch 合并为互不相交的连通分量，把独立分量交给 worker pool。

**[dsh-agent-fleet](https://github.com/CH4AcKO3/dsh-agent-fleet)**

开发了完整的 multi-agent 持久协作系统。与传统多智能体模型不同的是，其不依赖一个中心化的协调 Agent，极大缓解了协作场景下对一个强中心 Agent 的依赖和相应的性能界限。作为产品，我参考了飞书、Raft 等人/Agent 的办公与协作应用，吸收了其中大量有益的功能特性，并将学术领域有名的 Agent 模拟开发团队研究 [ChatDev: Communicative Agents for Software Development](https://arxiv.org/abs/2307.07924) 做了进一步完善，形成可配置的 Agent 阵容，为每个 Agent 配置了独特的提示词（也许你可以称之为“分布式提示词”）。在开发过程中，我也为社区贡献了一系列基础设施：[dsh-render-engine](https://github.com/memorax-ai/dsh-render-engine)（一套渲染 infra 服务插件），[dsh-hover-hint](https://www.npmjs.com/package/dsh-hover-hint)（界面悬浮提示框的原生风格组件）

**[dsh-webui-studio](https://github.com/memorax-ai/dsh-webui-studio)**

一个类 WYSIWYG 应用，用于 DSH 插件的前端界面开发。问题场景是，DSH 插件的客户端界面开发不像普通的前端开发，后者可以自由修改源码并实时应用，而前者需要在插件的能力范围内进行构建。我为这个场景搭建了一整套集成的客户端开发工具——同时给人类与 Agent。让开发时 Agent 真正能“看到”人的意图，并以配套的可调用 Tool 辅助进行实现。

**[dsh-patchouli](https://github.com/memorax-ai/dsh-patchouli)**

为 DeepSeek Harness 设计并开发的 local-first Agent memory 与 knowledge hub。
它以统一的 update / retrieve / subscribe 接口解耦数据来源、记忆算法和消费方，
支持流式检索、来源追踪、可插拔本地/远程实现，以及基于 Rust 和 SQLite 的事务存储。

### Research

**MODULI: Unlocking Preference Generalization via Diffusion Models for Offline Multi-Objective Reinforcement Learning *ICML2025*** · [Paper](https://arxiv.org/abs/2408.15501) · [Code](https://github.com/pickxiguapi/MODULI)

这是一个关于扩散生成模型在多目标策略优化中的应用的工作。我们观察了扩散生成模型中的引导强度，与多目标策略中的偏好对齐两个概念之间的联系，并在实验中取得了 SOTA 的效果。我为理论模型编写了实验代码，并搭建和优化了训练 pipeline。另外，我们在实验中挖掘了引导强度与定量偏好之间的数值关系，将从另一工作 (Sliding Guidance) 取得的灵感成功实施到生成式策略领域中。

**[Aerodrome](https://github.com/CH4AcKO3/Aerodrome)**

我的本科毕业论文项目。我尝试为飞行器导航制导的参数化策略优化构建一个高性能的、C++ 实现的仿真平台，并在此基础上构建了一个实现示例：为 F-16 战斗机训练一个强化学习控制策略。

### Game Dev

**[Simple Mending Yourself](https://github.com/CH4AcKO3/SimpleMendingYourself)**

一个 RimWorld 的 QoL 模组，让游戏角色可以直接使用原料修补自己的装备。这个小模组看起来解决了一个游戏中很多人遇到的小问题，在创意工坊受到欢迎。

## 联系我

- Website: [ch4acko3.github.io](https://ch4acko3.github.io)
- Google Scholar: [Zhenrui Zheng](https://scholar.google.com/citations?user=KPpd1pYAAAAJ)
- ORCID: [0009-0006-6125-871X](https://orcid.org/0009-0006-6125-871X)
- QQ: 920404212

---

感谢你的访问，欢迎查看我的项目或与我交流！
