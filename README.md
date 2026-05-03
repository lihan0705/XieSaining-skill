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

### 关于 `npx skills add`

`npx` 本身不是 skill registry，它只是从 npm 临时运行一个 CLI。除非某个 `skills` npm CLI 明确支持从 GitHub 安装这个仓库，否则下面这种命令不应作为默认安装方式：

```bash
npx skills add lihan0705/XieSaining-skill
```

因此当前 README 默认推荐 git/manual 安装。

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
