# Hi, I'm Zhenrui Zheng (CH4AcKO3) 👋

I am a PhD student at **The Chinese University of Hong Kong, Shenzhen (CUHK-Shenzhen)**.

My research interests are broad, with a focus on generative models, reinforcement learning, and agent systems. I also enjoy building software—particularly games, optimized algorithms, automation systems, and infrastructure.

## Research & Technical Stack

### Core stack — independent

I can work independently, without AI assistance, in:

- **Research:** 「Generative Models」 · 「Diffusion Models」 · 「Reinforcement Learning」 · 「Offline Learning」
- **Agent Systems:** 「Local Agent Runtime」 · 「Multi-Agent Orchestration」 · 「Agent Protocol」 · 「Tool, Skill & Memory Systems」
- **Agent Infrastructure:** 「Persistent Context & Sessions」 · 「Authorization」 · 「Sandboxing」 · 「Lifecycle」
- **Programming Languages:** 「C/C++」 · 「Python」 · 「Rust」 · 「Lean」
- **Frontend:** 「HTML」 · 「CSS」 · 「Vue」 · 「React」
- **Tooling:** 「Node.js」 · 「pnpm」 · 「uv」 · 「Vite」

### Additional stack — AI-assisted

With AI assistance, I can also work in:

- **Programming Languages:** 「JavaScript/TypeScript」 · 「C#」

## Selected Projects

### Agent Systems

**[Frontal-Lobe](https://github.com/CH4AcKO3/Frontal-Lobe) — Modern MCP-based Meta-Harness Framework**

A distributed harness framework written in Rust and built on the modern MCP protocol. It explores replacing the traditional monolithic, locally embedded agent application with a decentralized cluster of services, where every agent, tool, and provider communicates by exposing capabilities as services. The framework implements explicit consistency and transaction models to remain stable in unreliable environments.

~~Just as the project was approaching release, DeepSeek Harness appeared with nearly the same positioning. The work nevertheless produced several interesting features, and I ultimately decided to migrate them to DSH. [Frontal-Lobe Preview](https://icn07qje5tl4.feishu.cn/wiki/NLGAwkXpsicdGgk6hnoc0vRknDf?from=from_copylink)~~

**[dsh-harmony](https://github.com/memorax-ai/dsh-harmony) — Runtime Patching for DSH Plugins**

A runtime hot-patching framework designed and developed for DeepSeek Harness. Patch definitions use an AST query-and-rewrite syntax to modify the compiled JavaScript of plugins at runtime, filling the gap left by plugins that cannot otherwise be changed live. Its implementation addresses engineering problems such as patch conflicts and the startup cost of AST queries.

<details>
<summary><strong>Implementation notes: conflict resolution and AST query performance</strong></summary>

**Patch conflict resolution.** The system first decomposes the dependency graph into strongly connected components using an iterative Tarjan algorithm. For cyclic components with at most 14 nodes, an $O(k^2 2^k)$ subset dynamic program finds an ordering with the fewest violated edges, using the inversion count relative to the original order as a tie-breaker. Larger components use a feedback-arc heuristic that repeatedly removes sources and sinks, then selects the node with the maximum `out-degree - in-degree`. This confines exponential search to small components, after which a stable Kahn topological sort combines the results.

**AST query and rewrite.** TSQuery selectors are compiled into query plans. Indexes over `SyntaxKind` and equality-tested properties are used to choose the anchor with the smallest candidate set. Each AST subtree receives a pair of 32-bit Merkle hashes, and the selector–subtree-hash pair maps to a reusable relative node location. For general selectors, the cache key additionally includes contextual fingerprints derived from ancestors, siblings, and source positions. When the source changes only slightly, the system incrementally updates and reuses the existing AST indexes. Multithreaded preflight uses a disjoint-set union structure to group patches that share target files into disjoint connected components, which can then be processed independently by a worker pool.

</details>

**[dsh-agent-fleet](https://github.com/CH4AcKO3/dsh-agent-fleet) — Persistent Multi-Agent Collaboration**

A complete system for persistent multi-agent collaboration. Unlike conventional multi-agent designs, it does not rely on a central coordinating agent, substantially reducing both the dependence on a single powerful coordinator and the resulting performance ceiling. Its product and system design draws inspiration from collaboration tools such as Feishu and distributed protocols such as Raft. It also extends the well-known agent-based software development study [ChatDev: Communicative Agents for Software Development](https://arxiv.org/abs/2307.07924) with configurable agent rosters, giving each agent a distinct prompt—perhaps best described as *distributed prompting*.

During development, I also contributed infrastructure to the community: [dsh-render-engine](https://github.com/CH4AcKO3/dsh-render-engine), a suite of rendering-infrastructure service plugins, and [dsh-hover-hint](https://www.npmjs.com/package/dsh-hover-hint), a native-style hover-tooltip component.

**[dsh-webui-studio](https://github.com/memorax-ai/dsh-webui-studio) — WYSIWYG Development for DSH Plugin Interfaces**

A WYSIWYG application for developing frontend interfaces for DSH plugins. Unlike ordinary frontend development, where source code can be edited and reflected immediately, a DSH plugin interface must be built within the capabilities exposed by the plugin. I created an integrated client-development environment for both humans and agents, allowing an agent to genuinely “see” the developer's intent and use a companion toolset to implement it.

**[dsh-patchouli](https://github.com/memorax-ai/dsh-patchouli) — Local-First Agent Memory & Knowledge Hub**

A local-first memory and knowledge hub for DeepSeek Harness. It decouples data sources, memory algorithms, and consumers through unified `update`, `retrieve`, and `subscribe` interfaces. It supports streaming retrieval, provenance tracking, pluggable local and remote implementations, and transactional storage built with Rust and SQLite.

### Research

**MODULI: Unlocking Preference Generalization via Diffusion Models for Offline Multi-Objective Reinforcement Learning** — *ICML 2025* · [Paper](https://arxiv.org/abs/2408.15501) · [Code](https://github.com/pickxiguapi/MODULI)

A study of diffusion generative models for multi-objective policy optimization. We identified a connection between guidance strength in diffusion models and preference alignment in multi-objective policies, achieving state-of-the-art experimental results. I implemented the experiments for the theoretical model and built and optimized the training pipeline. We also uncovered a quantitative relationship between guidance strength and preferences, successfully transferring an idea from our related work, *Sliding Guidance*, into the domain of generative policies.

**[Aerodrome](https://github.com/CH4AcKO3/Aerodrome) — High-Performance Simulation for Policy Optimization**

My undergraduate thesis project. I built a high-performance simulation platform in C++ for optimizing parameterized aircraft navigation and guidance policies, together with an example application that trains a reinforcement-learning controller for an F-16 fighter aircraft.

### Game Development

**[Simple Mending Yourself](https://github.com/CH4AcKO3/SimpleMendingYourself) — A RimWorld Quality-of-Life Mod**

A small mod that allows pawns to repair their own equipment directly with raw materials. It addresses a surprisingly common pain point and has been warmly received on the Steam Workshop.

**[Rim Alert](https://github.com/CH4ACKO3/RimAlert) — A Campaign and Operations Framework for RimWorld**

A work-in-progress RimWorld mod that provides narrative and gameplay frameworks for campaigns and operations, giving the ecosystem's many combat and character-enhancement mods meaningful scenarios in which to be used.

## Contact

- **Website:** [ch4acko3.github.io](https://ch4acko3.github.io)
- **Google Scholar:** [Zhenrui Zheng](https://scholar.google.com/citations?user=KPpd1pYAAAAJ)
- **ORCID:** [0009-0006-6125-871X](https://orcid.org/0009-0006-6125-871X)
- **QQ:** 920404212

---

<p align="center"><em>Thanks for visiting—feel free to explore my projects or get in touch.</em></p>
