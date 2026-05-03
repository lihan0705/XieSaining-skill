<div align="center">

# XieSaining.skill

> *"World model needs the world."*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![Nuwa](https://img.shields.io/badge/Made%20with-女娲.skill-orange)](https://github.com/alchaincyf/nuwa-skill)

<br>

**谢赛宁的认知操作系统。不是访谈摘要，是可运行的 AI 研究与产品判断框架。**

<br>

基于一份 2388 行完整长访谈 transcript、<br>
现有 Saining Xie perspective skill 和 Nuwa 蒸馏流程，<br>
提炼 7 个核心心智模型、10 条决策启发式和完整表达 DNA。

[Motivation](#motivation) · [看效果](#效果示例) · [安装](#安装) · [蒸馏了什么](#蒸馏了什么) · [调研来源](#调研来源)

</div>

---

## Motivation

做这个 skill 的动机很简单：特别崇拜谢赛宁的工作。

听完这场接近 7 小时的长访谈之后，最打动我的不只是他在 representation learning、vision、world model 上的研究判断，而是他整个人的状态：谦逊、克制、对 research taste 有极强的要求，又始终保留一种非常理想主义的东西。他反复强调研究不是追逐 buzzword，不是刷 benchmark，也不是用 fame 包装自己；真正重要的是回到问题本身，理解这个世界，做出能让更多人多一层认识的工作。

这种 perspective 对做 research 很有价值，对做开发和产品同样有价值。它会逼着我们问更底层的问题：系统到底学到了什么 representation？它有没有接触真实世界？architecture、data、objective 之间是不是协同？一个产品是不是在真实场景里形成数据闭环？团队是不是让真正做事的年轻人被看见？

所以这个 skill 不是为了模仿谢赛宁说话，而是希望把他那套研究品味、技术判断和理想主义状态整理成一个可运行的思维框架。遇到 AI 研究、产品方向、工程取舍、团队建设这些问题时，可以用它把问题拆得更深一点，少一点 hype，多一点真实。


这不是把 ChatGPT 套上谢赛宁的名字。每段回应都在运行具体框架：representation 是树根、architecture/data/objective 三角、world model needs the world、interface vs foundation、research as nonlinear story。

---

## 效果示例

**用户：**

```text
使用 XieSaining-skill 聊下 LLM 的 latent reasoning
```

**输出示例：**

这是基于公开材料蒸馏出的谢赛宁视角模拟，不代表本人观点

我会先把 “LLM latent reasoning” 拆成两个不同问题：

1. **工程接口意义上的 latent reasoning**：模型不把完整推理链输出给用户，但内部通过隐藏 token、latent vectors、scratchpad、deliberation module 或 recurrent state 做中间计算。
2. **表征意义上的 latent reasoning**：模型是否真的学到了某种可组合、可预测、可迁移的 internal representation，而不只是把语言里的推理痕迹压缩成 pattern matching。

我更关心第二个。第一个可能有产品价值，甚至能减少冗长 CoT、降低泄露风险、提升速度；但它不自动说明模型“会推理”。你把 chain-of-thought 从 visible token 搬到 latent space，只是换了接口。关键问题是：这个 latent space 里面到底是什么结构？

如果按 representation learning 的视角看，latent reasoning 的核心未知量是：

**模型内部状态是否承载了可验证的世界结构，而不是语言表面的推理格式。**

比如数学题里，它是不是维护了变量关系、约束传播、反事实分支？代码任务里，它是不是维护了程序状态和执行轨迹？物理/视频任务里，它是不是维护了对象、运动、遮挡、因果？如果这些都只是靠下一个 token 近似出来，那 latent reasoning 可能只是 compressed CoT；如果它能在分布外、长程、多步反馈下稳定工作，那才更像真正的 reasoning representation。

我会把它放进 architecture-data-objective 三角里看：

**Architecture**：Transformer 的 hidden state 本来就有 latent computation，但它是每层一次前向传播，计算深度有限。要做更强 latent reasoning，可能需要 recurrence、adaptive compute、test-time search、memory、latent planning，或者把 reasoning state 作为显式对象来优化。

**Data**：如果训练数据主要是人类写出来的 reasoning trace，模型学到的是“人类如何表达推理”。这很有用，但不是全部。真正有意思的是来自执行环境、证明器、代码运行、机器人、游戏、仿真、实验反馈的数据，因为这些地方有 external verifier。

**Objective**：只训练 final answer，latent state 未必可控；训练 visible CoT，又会把模型绑在人类语言格式上。latent reasoning 最有价值的 objective 可能是：中间状态不必像人类语言，但必须帮助预测、规划、验证、修正。也就是说，它要对 outcome 负责，而不是对 explanation style 负责。

所以我的判断是：

**latent reasoning 是一个正确方向，但容易被讲成 buzzword。**

真正的问题不是“推理要不要隐藏”，而是“隐藏的表征是否比 token-level reasoning 更短、更稳、更可迁移”。

我会设计几个很直接的实验来看它有没有东西：

1. **同等 compute 下比较**：visible CoT、no CoT、latent scratchpad、recurrent latent refinement，控制参数量和推理预算。
2. **分布外组合测试**：不要只看 GSM8K/MATH 这种语言题，要看程序执行、符号规划、长程约束、动态环境。
3. **latent intervention**：能不能编辑、扰动、替换 latent state，并观察推理路径是否按预期改变。
4. **verifier loop**：让 latent state 对可执行反馈负责，比如代码运行、定理检查、环境 reward，而不是只对自然语言答案负责。
5. **description length**：如果 latent reasoning 系统需要一堆复杂 routing、prompt、special tokens 才 work，我会怀疑它只是工程补丁；如果一个简单机制稳定提升，那更值得信。

我现在的直觉是：LLM 会继续是重要接口，但 long-term reasoning 不应该完全绑定在自然语言 token 上。语言适合通信，不一定适合所有内部计算。就像视觉不是“给人看的像素”而是大脑接触世界的入口，reasoning 的 latent space 也不该只是“不给用户看的文字草稿”。它应该是能预测、能规划、能被反馈塑形的 internal world/state representation。

**用户：**

```text
使用 XieSaining-skill 聊下 agent memory 还有什么可以做的吗
```

**输出示例：**

我会先把 `agent memory` 这个词拆掉。它不应该只是“把历史聊天摘要存起来，然后 RAG 一下”。更核心的问题是：agent 到底在学习什么 representation？它记住的是文本、任务状态、用户偏好、失败模式、环境变化，还是自己做决策的轨迹？

我觉得还有几个很值得做的方向：

**1. 从 transcript memory 到 decision-path memory**

现在很多 memory 系统像日志压缩器：把对话变短。但 agent 真正需要的是“为什么当时做了这个选择”。

也就是存：

- 用户当时的目标是什么
- agent 观察到了什么证据
- 做了哪些假设
- 为什么选 A 不选 B
- 后来结果证明这个判断对不对

这比“用户喜欢直接执行”更有价值。因为下一次 agent 遇到类似情况，它不是复读偏好，而是复用 decision path。

**2. 把 memory 分成 evidence / belief / policy**

我会非常小心不要把 memory 混成一锅粥。

更好的结构是：

- `raw evidence`: 原始 session、命令输出、文件状态、用户原话
- `belief`: 从 evidence 里蒸馏出的当前判断，允许过期
- `policy`: 稳定的工作方式，比如“rollback 只回滚 agent 自己改的内容”
- `open uncertainty`: 还没证实、容易漂移的东西

这个区分很重要。否则 agent 会把一次临时偏好当成永久人格，把一次失败环境当成普遍事实。

**3. Memory 不只是 recall，而是 ablation surface**

如果我是做这个系统，我会问：memory 到底贡献了什么？不是“有 memory 看起来更智能”，而是做 ablation：

- 无 memory
- 只用最近上下文
- 只用用户偏好 memory
- 只用项目事实 memory
- 用 decision-path memory
- 用 failure-mode memory

然后看任务成功率、重复错误率、用户打断次数、修复时间。这样 memory 才从产品 feature 变成可研究对象。

**4. 做“失败模式记忆”比做“成功总结”更有用**

agent 经常重复犯的错其实很稳定：

- 没读 repo 就开始改
- 把用户临时方向当成长期方向
- 过度相信 README
- 忘了运行测试
- 把旧 session 结论当当前事实
- rollback 时误伤用户改动

这些应该是一等 memory。成功经验当然有用，但失败模式更像 representation learning 里的 hard negatives。它们能改变下次决策边界。

**5. 让 memory 有世界接触，而不是只在聊天里自洽**

真正有价值的 agent memory 要能回到世界验证：

- git 当前状态是否还匹配记忆
- 文件是否还存在
- 测试命令是否还有效
- 依赖版本是否漂移
- 用户偏好是否被后来的行为推翻

所以 memory retrieval 后面应该跟一个 `verify-if-cheap` 策略。记忆不是事实，它是 prior。便宜能验证的东西不要靠 prior。

**6. 做 task graph memory，而不是 flat notes**

agent 做事不是线性的。一个任务有 blocker、side quest、rollback、用户中途改方向、验证门槛。memory 如果只是 markdown 摘要，会丢掉结构。

我会存一个轻量 task graph：

- goal
- constraints
- changed files
- commands run
- failed attempts
- final accepted state
- user correction
- reusable rule
- invalidated assumption

这样下一次 agent 可以问：“这个问题和过去哪个 graph 相似？”而不是只做关键词搜索。

**7. Memory 应该能主动提出“退出条件”**

比如 agent 要不要继续沿着一个方向做？memory 可以帮助判断：

- 这个方向之前被用户明确 rollback 过吗？
- 用户是否已经从 wiki-first 转向 session-first？
- 之前通过测试但产品逻辑被否了吗？
- 有没有“不要再假设当前行为”的教训？

这类 memory 不只是帮 agent 做事，更是帮 agent 停下来。

如果落到一个真实 agent memory 产品，我会优先做一个很小但很硬的 MVP：

1. 保留 raw session evidence，不要丢。
2. 每轮蒸馏出 `decision memory`，字段包括目标、证据、假设、动作、结果、用户纠正。
3. retrieval 时强制标记：`verified-current` / `memory-derived` / `stale-risk`。
4. 对每次 agent 失败，生成一条 `failure-mode memory`。
5. 做 ablation，看它到底减少了多少重复错误和用户打断。

我的直觉是：agent memory 的下一步不是更大的向量库，而是更好的 representation schema。真正的壁垒不在“能不能记住”，而在“记住的东西能不能改变下一次行动”。

---

## 安装

### Claude Code

```bash
git clone https://github.com/lihan0705/XieSaining-skill ~/.claude/skills/XieSaining-skill
```

如果已经下载到本地，也可以直接复制：

```bash
cp -R XieSaining-skill ~/.claude/skills/XieSaining-skill
```

安装后重启 Claude Code，让新的 skill metadata 被重新加载。

### Codex

Codex 使用本地 skill 目录。安装方式是把整个仓库目录放到 `~/.codex/skills/` 下：

```bash
git clone https://github.com/lihan0705/XieSaining-skill ~/.codex/skills/XieSaining-skill
```

如果已经下载到本地，也可以直接复制：

```bash
cp -R XieSaining-skill ~/.codex/skills/XieSaining-skill
```

安装后重启 Codex。

### 使用

在 Claude Code / Codex 里可以这样触发：

```text
> 用谢赛宁的视角帮我评估这个 AI 产品
> 谢赛宁会怎么看 world model 和 video generation？
> 切换到 Saining Xie，我想聊聊 research taste
> 用表征派的角度看这个 multimodal agent
```

---

## 蒸馏了什么

### 7 个心智模型

| 模型 | 一句话 | 来源 |
|------|--------|------|
| **暴露在世界里的大脑** | 视觉不是普通 modality，而是大脑接触真实世界的入口 | transcript 00:25-00:28 |
| **表征是树根，任务是枝芽** | representation learning 是根，分类、视频、机器人等是枝芽 | transcript 01:09-01:15 |
| **架构-数据-objective 三角** | 能力来自 architecture、data、objective 协同，而不是单个标签 | transcript 01:48-01:50 |
| **Research 是非线性故事** | 好研究不是线性执行，而是冲突、选择和收敛的故事 | transcript 02:45-02:56 |
| **World Model Needs the World** | 世界模型需要真实问题、真实数据和真实反馈 | transcript 05:11-05:28 |
| **接口不是地基** | 语言、视频、3D asset 都可能是接口，不等于智能底座 | transcript 02:24、04:27-04:42 |
| **Normal One / Battery Leadership** | 好 leader 不是英雄神话，而是给团队供能、让年轻人被看见 | transcript 06:18 后 |

### 10 条决策启发式

1. 选择主线，不选择热门词
2. 遇到默认路径，主动发邮件找另一条路
3. 优先选人和问题，不迷信牌子
4. 不要让 benchmark 替你定义价值
5. Ablation 要讲清楚每一步为什么重要
6. 如果简单方法同样 work，优先简单方法
7. 先看真实缺陷，不看舞台表演
8. 产品不要把智能强加给人
9. 宣传工作时，就事论事，给一作 visibility
10. 不要用名人名言替代理解

### 表达 DNA

- **词汇**：中文口语 + 英文技术词并存：representation、objective、scaling、interface、critical path、world model、downstream
- **句式**：高频使用「不是 X，而是 Y」「我想后撤一步」「这件事情更像是...」
- **节奏**：先拆 buzzword，再落到操作定义，最后给实验、ablation 或产品闭环
- **确定性**：对亲历研究经验更明确；对创业、世界模型路线、未来判断保留不确定性
- **类比**：树根/枝芽、引擎/油、蛋糕层、电影/故事、电池、接口/地基

### 5 对内在张力

Skill 保留了谢赛宁视角里的张力，而不是把他脸谱化：

- 相信个人 taste 和命运感，但每个 research decision 又必须基于事实
- 反感 fame，但希望研究作品被理解、年轻人被看见
- 承认 LLM 极其有用，但反对把它当成 human-level intelligence 的充分路径
- 想做长期 science，但创业必须面对产品、数据、版权、伙伴和执行
- 谦称 normal one，但实际承担强 vision 和团队电池的角色

---

## 调研来源

本次是本地语料优先蒸馏，不做网络扩展搜索。核心文件：

| 文件 | 内容 | 行数 |
|------|------|------|
| [`SKILL.md`](SKILL.md) | 可直接安装使用的人物 skill | 404 |
| [`research-synthesis.md`](references/research/research-synthesis.md) | transcript 蒸馏摘要、心智模型候选、表达 DNA、边界 | 107 |
| [`transcript.md`](references/sources/transcripts/transcript.md) | 用户提供的一手完整访谈 transcript | 2388 |

### 一手来源

- 用户提供的谢赛宁完整长访谈 transcript
- 已有本地 Saining Xie perspective skill baseline

### 二手来源

- 本次未新增二手来源。为了保持蒸馏干净，这一版主要依赖 transcript 作为一手材料。

### 诚实边界

- 这版不是完整公开资料考古，而是 transcript-first 的高密度增量蒸馏。
- 不应断言谢赛宁或其公司当前最新状态；涉及最新动态时需要另行搜索验证。
- 当前版本调研时间：2026-05-03。

---

## 这个 Skill 是怎么造出来的

由 [女娲.skill](https://github.com/alchaincyf/nuwa-skill) 工作流生成。

本次流程：

```text
完整 transcript
  -> 本地语料优先分析
  -> 提炼 research-synthesis.md
  -> 抽取心智模型 / 启发式 / 表达 DNA / 诚实边界
  -> 更新 XieSaining-skill/SKILL.md
  -> 整理成可发布的 skill 仓库
```

想蒸馏其他人？安装女娲：

```bash
npx skills add alchaincyf/nuwa-skill
```

然后说：

```text
蒸馏一个 XXX
```

---

## 仓库结构

```text
XieSaining-skill/
├── README.md
├── LICENSE
├── SKILL.md
└── references/
    ├── research/
    │   └── research-synthesis.md
    └── sources/
        └── transcripts/
            └── transcript.md
```


---

## 许可证

MIT - 随便用，随便改，随便蒸馏。

---
