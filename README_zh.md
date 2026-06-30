<!--
╔══════════════════════════════════════════════════════════╗
║  Author / 作者                                            ║
║  Name / 姓名:  [倪啸庭] [Xiaoting Ni]                                ║
║  Affiliation / 所属单位:  [School of Pharmacy, Qiqihar Medical University, China. Department of Pharmacy, The First affiliated Hospital of Harbin Medical University, China.]               ║
║  Email:  [nixt1998@163.com]                     ║
║  ORCID:  [0009-0009-6400-4071]                           ║
╚══════════════════════════════════════════════════════════╝
-->

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-orange)](https://claude.ai/code)

**语言:** &nbsp; [🇬🇧 English](README.md) &nbsp; | &nbsp; 🇨🇳 **中文**

---

# Narrative Review Writing Skill（叙述性综述写作技能）

**专为临床药理学与基础药理学机制研究设计的 Claude Code 英文叙述性综述（Narrative Review）写作技能。**

引导用户完成从选题范围界定到最终稿件装配的完整 11 步工作流——包含强制验证关口、零虚构文献约束、以及针对大规模综述（100+ 篇参考文献）的双轨上下文管理机制。

---

## 目录

- [功能特性](#功能特性)
- [适用领域](#适用领域)
- [安装方式](#安装方式)
- [快速开始](#快速开始)
- [工作流总览](#工作流总览)
- [输出结构](#输出结构)
- [核心规则](#核心规则)
- [不适用的场景](#不适用的场景)
- [研究基础](#研究基础)
- [文件结构](#文件结构)
- [许可证](#许可证)

---

## 功能特性

| 功能 | 说明 |
|------|------|
| **11 步引导式管道** | 每步输出写入磁盘，可随时中断并从任意步骤恢复 |
| **零虚构文献** | 每条引用必须可追溯至用户提供的已验证 PDF；PMID/DOI 交叉核验 |
| **Obsidian 知识图谱** | 自动生成 vault，包含结构化文献笔记、主题聚合和 `[[wikilinks]]` 双向链接，支持图谱可视化 |
| **双轨上下文管理** | 文件化管道 + Obsidian vault —— 100+ 篇参考文献不溢出上下文窗口 |
| **核心结论式标题** | 每个章节标题陈述核心发现，而非简单描述性标签 |
| **图表绘制指令** | 为每张图输出详细绘制指南，可直接交给外部 AI 绘图工具或插画师 |
| **Vancouver 参考文献格式** | 默认输出格式，正文引用 `[N]` 置于句号之前 |
| **前置环境检查** | 启动前自动扫描所需依赖 skill，缺失时阻止或警告 |
| **冲突证据矩阵** | 系统性识别和记录不同研究之间的矛盾发现 |
| **中英文双语支持** | 英文写作输出，项目文档双语呈现 |

---

## 适用领域

**主要方向**：临床药学 + 基础药理学机制研究

- 药物作用机制（受体结合、酶抑制、转运体相互作用）
- 信号通路与分子靶点（NF-κB、PI3K/Akt、MAPK、JAK/STAT 等）
- 药代动力学/药效学（ADME、药物相互作用）
- 药物毒性机制（肾毒性、心脏毒性、肝毒性）
- 构效关系（SAR）
- 药物基因组学与精准医学

可适配其他具有类似机制综述需求的生物医学领域。

---

## 安装方式

### 前置依赖

| 依赖 | 必需 | 用途 |
|------|------|------|
| [Claude Code](https://claude.ai/code) | 是 | 运行环境 |
| [`pdf` skill](https://github.com/anthropics/skills/tree/main/pdf) | **是** | 文献 PDF 验证（Step 3） |
| [`docx` skill](https://github.com/anthropics/skills/tree/main/docx) | 可选 | 输出 Word 文档（Step 10） |

### Git 克隆安装

```bash
git clone https://github.com/YOUR_USERNAME/narrative-review-skill.git ~/.claude/skills/narrative-review
```

### 手动安装

```bash
mkdir -p ~/.claude/skills/narrative-review

# 将所有文件复制到 skill 目录
cp *.md LICENSE ~/.claude/skills/narrative-review/
```

### 验证安装

在 Claude Code 中输入：

```
write a narrative review about [你的主题]
```

Skill 应自动触发，从 Step 0.0（NR vs SR 介绍）开始。

---

## 快速开始

```
你: write a narrative review about mitochondrial mechanisms
    in cisplatin-induced nephrotoxicity

Claude: [触发 narrative-review skill]
  Step 0.0 — "本 skill 仅适用于叙述性综述（Narrative Review）"
  Step 0.5 — 环境检查: pdf [✓], docx [✓] → 通过
  Step 1.0 — "请提供：工作目录路径、全文字数限制、
             图/表个数、综述标题"
  Step 1.0 — 6 要素范围界定评估...
  ...
  Step 10.0 — 最终稿件 + 缩略词表交付
```

每一步都有确认提示和下一步引导语，全程不会迷失方向。

---

## 工作流总览

```
Step 0.0  介绍：Narrative Review vs Systematic Review 区别
Step 0.5  ⭐ 前置环境检查（依赖 skill 扫描）
Step 1.0  ⭐ 项目参数设定（字数/图/表限制）+ 6 要素范围界定
Step 2.0  PubMed 检索策略 + 文献清单（PMID/DOI）
Step 3.0  文献验证 + 结构化笔记 + 冲突证据矩阵
Step 3.5  ⭐ Obsidian Vault 生成（知识图谱）
Step 4.0  文章框架生成 → 用户确认 → 锁定
Step 4.5  ⭐ 跨节一致性检查
Step 5.0  逐节写作（每节独立文件输出）
Step 6.0  结论（局限性 + 展望 + 已解决/未解决问题）
Step 7.0  图绘制指令 + 图注
Step 8.0  总结表（含可追溯引用编号）
Step 9.0  参考文献组装（Vancouver）+ 交叉验证
Step 10.0 ⭐ 最终装配 + 缩略词表 + 输出（txt + 可选 docx）
```

⭐ = 本版本新增

---

## 输出结构

```
{工作目录}/
│
├── 📁 obsidian_vault/              ← 知识图谱（用 Obsidian 打开）
│   ├── _MOC_Overview.md            ← 全部内容层级索引
│   ├── _MOC_Mechanisms.md          ← 按通路/机制分组
│   ├── _MOC_Clinical_Translation.md ← 临床转化相关性
│   ├── _MOC_Controversies.md       ← 争议性发现
│   ├── _MOC_Figure_Ideas.md        ← 可视化概念
│   ├── papers/
│   │   ├── 001_Author2024_Topic.md
│   │   ├── 002_Author2023_Topic.md
│   │   └── ...
│   ├── themes/
│   │   ├── NF-kB_Pathway.md
│   │   ├── Mitochondrial_Dysfunction.md
│   │   └── ...
│   └── templates/
│       ├── paper_template.md
│       └── theme_template.md
│
└── 📁 pipeline_output/             ← 写作管道状态
    ├── 00_preflight_check.md
    ├── 00_project_config.md
    ├── 01_search_strategy.md
    ├── 01_reference_list.md
    ├── 02_literature_notes.md       ← 含冲突证据矩阵
    ├── 03_framework.md             ← 用户已锁定的框架
    ├── 04_draft_section_01_intro.md
    ├── 04_draft_section_02_*.md
    ├── ...
    ├── 04.5_cross_section_check.md
    ├── 05_conclusion.md
    ├── 06_figure_instructions.md
    ├── 07_tables.md
    ├── 08_references_final.md
    ├── 09_final_manuscript.txt
    ├── 09_final_manuscript.docx     ← 可选
    └── 10_selfcheck_log.md
```

---

## 核心规则

工作流全程强制执行的规则：

| # | 规则 | 执行方式 |
|---|------|----------|
| 1 | **零虚构文献** | 每条引用必须可追溯至用户提供的已验证 PDF |
| 2 | **基于证据的推理** | 不过度乐观，推测性陈述须标注 |
| 3 | **批判性综合** | 禁止"洗衣清单"式罗列 —— 须评价每项研究的优缺点 |
| 4 | **平衡覆盖** | 矛盾的证据必须讨论，不可选择性忽略 |
| 5 | **引用原始研究** | 引用一手文献，非"综述的综述" |
| 6 | **PMID/DOI 验证** | 与 PubMed 和 PDF 原文交叉核验 |
| 7 | **用户关口确认** | 每步须用户明确接受后方可进入下一步 |

---

## 不适用的场景

- ❌ **系统评价（Systematic Review）** —— 请使用基于 PRISMA 的工作流
- ❌ **Meta 分析** —— 需要统计综合框架
- ❌ **Scoping Review、Rapid Review、Umbrella Review** —— 方法论不同

如果你需要的是系统评价，本 skill 会在 Step 0.0 明确告知并推荐替代方案。

---

## 研究基础

本 skill 基于 **13 篇同行评审的综述写作方法学文献**。核心来源：

| 作者（年份） | 期刊 | 核心贡献 |
|-------------|------|----------|
| **Dhillon P** (2022) | *FEBS J* | 范围检查清单、核心组件表、图表设计原则 |
| **Chaney MA** (2021) | *JCVA* | NR 三大质量标准、NR vs SR、逆向检索法 |
| **Pautasso M** (2013) | *PLoS Comput Biol* | 十条规则：边读边记、批判性评价、反馈循环 |
| **Gasparyan AY** (2011) | *Rheumatol Int* | 生物医学叙述性综述：作者署名、伦理、标题/摘要 |

详见 **[references.md](references.md)**（含全部 13 篇参考文献及 DOI）和 **[references_summary.txt](references_summary.txt)**（按期刊分区与影响因子从高到低排列的汇总表）。

---

## 文件结构

```
narrative-review/
├── SKILL.md                    # 主编排器（11 步工作流）
├── README.md                   # 本文件（英文版首页）
├── README_zh.md                # 中文版首页
├── LICENSE                     # MIT 许可证
├── .gitignore
│
├── nr-vs-sr.md                 # NR vs SR 对比表
├── scope-checklist.md          # 6 要素选题评估表
├── search-strategy.md          # PubMed/MeSH 检索策略构建指南
├── figure-template.md          # 图绘制指令模板
├── table-template.md           # 总结表模板
├── vancouver-guide.md          # Vancouver 参考文献格式规范
├── obsidian-templates.md       # Obsidian 笔记模板（文献/主题/MOC）
├── preflight-check.md          # 依赖 skill 扫描逻辑
├── quality-checklist.md        # 最终验收清单（30 项）
├── references.md               # 完整研究基础（13 篇参考文献）
└── references_summary.txt      # 按期刊分区和影响因子排列的文献汇总表
```

---

## 关于灰色文献的说明

虽然我们的研究基础中包含了 Paez (2017) 关于灰色文献检索方法学的文献，但**本 skill 的所有 protocol 仅基于用户提供的、经同行评审正式出版文献的真实数据运行。** 除非用户明确提供并通过 PDF 验证管道（Step 3.0）核实，否则不会将任何非商业出版物、预印本、会议摘要或其他灰色文献来源的内容纳入稿件。这确保了最终稿件中的每条引用均可追溯至可靠的同行评审来源。

---

## 免责声明

**仅供学术研究使用。** 本 skill 定位为辅助学术写作过程的研究工具，并非完整的、可直接用于官方出版的稿件生成系统。用户需对以下内容全权负责：

- 所有内容的科学准确性与学术诚信
- 所有引用和参考文献的最终核实
- 符合目标期刊的投稿指南与伦理标准
- 出版所需的同行评审与修订流程
- 所在领域的任何法律或监管要求

作者对使用本 skill 产生的稿件不承担任何责任。

---

## 反馈与交流

欢迎提出问题、建议或合作想法。请在 GitHub 提交 Issue，或通过页面顶部的联系方式与我取得联系。欢迎使用，期待交流！

---

## 许可证

MIT — 详见 [LICENSE](LICENSE)。

---

<p align="center">
  <sub>为严谨、可复现的科学写作而构建。</sub>
</p>
