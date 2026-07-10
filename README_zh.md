<!--
╬══════════════════════════════════════════════════════════╬
  Author / 作者
  Name / 姓名:  倪啸庭  (Xiaoting Ni)
  Affiliation / 单位:
    School of Pharmacy, Qiqihar Medical University, China
    Dept. of Pharmacy, The First Affiliated Hospital of Harbin Medical University
  Email:  nixt1998@163.com
  ORCID:  0009-0009-6400-4071
╚══════════════════════════════════════════════════════════╝
-->

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-orange)](https://claude.ai/code)
[![Version](https://img.shields.io/badge/Version-v2.1-brightgreen.svg)]()
[![NLM Vancouver](https://img.shields.io/badge/Citation-Vancouver%2FNLM-purple.svg)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg)]()
[![Stars](https://img.shields.io/badge/GitHub-Stars%20Welcome-yellow.svg)]()

**语言:** &nbsp; [🇬🇧 English](README.md) &nbsp; | &nbsp; 🇨🇳 **中文**

<div align="center">

# Narrative Review Writing Skill · 临床药理学与基础药理机制研究

### 为药学领域严谨、可复现、循证据的叙述性综述写作，提供结构化人机协作工作流，基于NLM范式与13篇同行评审方法学文献

**19 个工作流步骤 · 40 条需求规范 · 30 种NLM引用类型 · 13 篇方法学文献 · 零虚构引用**

> ⭐⭐ 如果本工具对您的研究有帮助，请点亮Star⭐以表示支持！⭐⭐

</div>

---

## 总目的

建立严谨、可复现、循证据的药学叙述性综述写作框架，帮助研究者产出符合最高科学诚信标准的出版级稿件。本工具架起了 AI 辅助与学术严谨性之间的鸿沟，将结构化工作流强制执行与不可或缺的人类判断内在整合，以支持药物机制、药代动力学和临床药理学领域的循证研究。

---

## 目录

- [为什么选择「人机协作」](#为什么选择人机协作)
- [优势对比](#优势对比)
- [功能特色](#功能特色)
- [能做什么，不能做什么](#能做什么不能做什么)
- [适用人群](#适用人群)
- [工作流总览（v2.1，19 步骤）](#工作流总览)
- [各阶段用户输入模板](#各阶段用户输入模板)
- [实际输出文件概述](#实际输出文件概述)
- [输出文章结构](#输出文章结构)
- [支持引用格式](#支持引用格式)
- [支持语言](#支持语言)
- [版本更新说明](#版本更新说明)
- [适用领域](#适用领域)
- [安装方式](#安装方式)
- [快速开始](#快速开始)
- [核心规则](#核心规则)
- [研究基础](#研究基础)
- [文件结构](#文件结构)
- [免责声明](#免责声明)
- [反馈与联系](#反馈与联系)
- [贡献](#贡献)
- [更新记录](#更新记录)
- [许可证](#许可证)

---

## 为什么选择「人机协作」

药学文献的机制论述高度复杂且进展迅速，全自动化流程面临虚构引用、机制论述过度简化、批判性综合失调等风险。纯手动写作则耗时耗力、组织不一致且容易漏掉重要文献。

本工具采用「人机协作」模式：

- **AI 负责：** 结构强制执行、格式合规检查、防幻觉协议、系统化三轮核验、大规模文献集上下文管理、动态分批处理、可复现检索记录
- **研究者负责：** 科学判断、文献选择、机制论述解释、框架决策以及每个关键步骤的明确确认

在每一个关键节点——框架定稿、章节验收、参考文献核验——研究者均予以明确确认。这绝非一键生成的“速成文稿工具”，而是一台精密仪器：它在放大研究者能力的同时，将每一项科学决策权牢牢交还至领域专家手中。

---

## 优势对比

| 维度 | 纯手动 | 全自动 | 其他Skill | NRW v2.1 |
|---|:---:|:---:|:---:|:---:|
| 零虚构引用 | ✅ | ❌ | ⚠️ | ✅✅ |
| 引用三轮核验(3 Pass) | ⚠️ | ❌ | ❌ | ✅ |
| 人工审批关口 | ✅ | ❌ | ⚠️ | ✅ |
| 100+篇上下文管理 | ❌ | ⚠️ | ❌ | ✅ |
| 动态N批量核验协议 | ❌ | ❌ | ❌ | ✅ |
| Obsidian知识图谱 | ❌ | ❌ | ❌ | ✅ |
| Section Brief(写作逻辑) | ❌ | ❌ | ❌ | ✅ |
| Vancouver/NLM 30种类型完整规则 | ⚠️ | ⚠️ | ⚠️ | ✅ |
| 基因蛋白质命名规范 | ⚠️ | ❌ | ❌ | ✅ |
| 多平台(DeepSeek/Claude) | - | ⚠️ | ❌ | ✅ |
| 可复现检索记录(9项) | ⚠️ | ⚠️ | ❌ | ✅ |
| 独立Word模块输出 | ❌ | ❌ | ❌ | ✅ |
| 全程审计日志 | ❌ | ❌ | ❌ | ✅ |
| 保留科学判断 | ✅ | ❌ | ⚠️ | ✅ |
| 耗时 | 很高 | 很低 | 中等 | 中等 |

✅ 完全支持 · ⚠️ 部分/不确定 · ❌ 不支持/高风险

---

## 功能特色

每一个特色都是针对已识别的失败模式而做出的有意设计

**1. 动态防幻觉协议**
特色：每条引用必须可追溯至用户提供的已验证 PDF，无法核验的引用直接排除，而非附以警告保留。
重要性：AI 引用幻觉在学术领域有充分记录。一条虚构引用就能破坏整个稿件的可信度。
依据：PMID/DOI 交叉验证 + 三轮核验（Step 3.0 + 5.0 + 9.0）。详见 [SKILL.md Step 3.0](SKILL.md)

**2. 动态N基分批核验**
特色：N<35 时，逐篇验证（覆盖 100%）；N≥35 时，批量在 N/2 处触发，每批抽查 ≥50%。
重要性：固定阈值对小规模综述过度抽查，对大规模综述覆盖不足。
依据：比例式分配，确保任意规模综述均具一致覆盖。详见 [SKILL.md Step 3.1](SKILL.md)

**3. Obsidian 知识图谱**
特色：验证完成后，每篇文献自动生成具双向链接的 Obsidian 笔记；主题和 MOC 映射自动生成。
重要性：直接将 100+ 篇文献全部加载入 AI 上下文将导致溢出。
依据：受控 MOC → 主题 → 笔记顺序读取。详见 [SKILL.md Step 3.5](SKILL.md)

**4. 段落前 Section Brief**
特色：写作每个段落前，Claude 输出当前段落的 Section Brief，包含写作逻辑、核心论点、证据依据、字数预算。
重要性：在生成文本前强制论证段落逻辑，及早发现结构错误。
依据：详见 [SKILL.md Step 5.0](SKILL.md)

**5. 分批输出协议**
特色：大体输出按平台分批分发，带续传标记 [OUTPUT PART X/N]。
重要性：Claude app、Claude terminal 和 DeepSeek 有不同的 token 输出上限，无限制输出将导致内容丢失。
依据：平台分批大小在 Step 0.0b 记录。详见 [SKILL.md Batched Output Protocol](SKILL.md)

**6. 多数据库可复现检索记录**
特色：支持 PubMed / WOS / ScienceDirect / Wiley / Embase，完整记录包含检索日期、数据库版本、完整 Boolean 查询字符串及去重前后结果计数（9 项）。
重要性：可复现性是科学的核心价值，同行评审者日益要求提供完整检索记录。
依据：Step 2.8 九项记录。详见 [SKILL.md Step 2.8](SKILL.md)

**7. 基因/蛋白质命名规范**
特色：人类基因全大写斜体（HGNC），小鼠基因首字母大写余小写斜体（MGI），蛋白质非斜体（UniProt），写作前核验。
重要性：命名错误是药学期刊投稿被拒的常见原因之一。
依据：HGNC / GeneCards / MGI / UniProt。详见 [SKILL.md Core Rules](SKILL.md)

**8. 独立模块 Word 输出**
特色：图注、表格、缩略词表各自输出为独立 Word 文件，随正文一同提交。
重要性：大多数药学期刊要求表格和图表分别提交，内联将导致投稿错误。
依据：三个独立 .docx 文件：06_figure_legends.docx、07_tables_standalone.docx、10_abbreviations.docx

**9. 完整 Vancouver / NLM 引用规则**
特色：内置 vancouver-guide.md 包含 NLM 全部 30 种文献类型格式规则，源自 *Citing Medicine*（NLM 2007，更新 2020）。
重要性：部分实现缺少常见类型（预印本、博士论文、专利）。
依据：无外部路径依赖。详见 [Citing Medicine PDF](Citing%20Medicine-The%20NLM%20Style%20Guide%20for%20Authors%2C%20Editors%2C%20and%20Publishers.pdf)

**10. 运行日志与审计跟踪**
特色：pipeline_output/run_log.md 记录每个步骤的用户输入、操作、输出文件及时间戳。
重要性：长时间会话可能被中断，日志支持精确重建决策内容。
依据：全局规则适用于全部 19 步骤。详见 [SKILL.md Step 0.0](SKILL.md)

---

## 能做什么，不能做什么

### 本工具能帮您:

- 提供完整19步工作流
- 强制防幻觉协议
- 100+篇不溢出上下文文献管理
- 写作每节前输出Section Brief
- 基因/蛋白质符号验证(HGNC/MGI/UniProt)
- Vancouver/NLM等格式引用
- .txt / .docx 符合格式规范（Times New Roman 10pt，1.5 倍行距，两端对齐）
- 图注/表格/缩略词表独立Word文件
- 9项可复现检索记录
- 运行日志审计跟踪

### 本工具CANNOT帮您:

- **替代科学判断**，这是不可替代的人类决策
- **评估文献方法学质量**，只能确认引用匹配，不能评方法学
- **产生文献外的新假说**
- **替代同行评審**
- **保证发表**，它提升结构，不可替代科学贡献

> **关于批判性思考：** 工具强制框架，您提供科学。请对 AI 生成草稿保持严格的批判性审视。

---

## 适用人群

**推荐:**
- 药理学与药学科学研究者
- 临床药学、药学及相关领域的专科生、本科生、硕士研究生、博士研究生及博士后研究员
- 需要英文学术写作结构与格式支持的非英语母语研究者
- 需要管理大量文献（50～150 篇）并进行系统性组织的研究者
- 监督综述写作项目的实验室负责人或导师

**不推荐:**
- 系统评价（Systematic Review）或 Meta 分析写作（请使用基于 PRISMA 的工作流）
- 完全脱离药理学或生物医学机制研究的场景

---

## 工作流总览

```
Step 0.0    语言选择                                [v2.1 NEW]
Step 0.0b   模型与平台选择                            [v2.1 NEW]
Step 0.1    NR vs SR 介绍
Step 0.5    前置环境检查
Step 0.9    标题确认                                [v2.1 NEW]
Step 1.0    项目参数 + 范围界定
Step 2.0    多数据库检索 + 文献清单
Step 3.0    文献验证 + 结构化笔记 + 冲突证据矩阵
Step 3.5    Obsidian 知识图谱
Step 4.0    框架 -> 确认 -> LOCK
Step 5.0    逐节写作  (Section Brief)
Step 5.5    跨节一致性检查               [原 Step 4.5]
Step 6.0    结论
Step 6.5    摘要                                [v2.1 NEW]
Step 6.6    Keywords (MeSH)                        [v2.1 NEW]
Step 7.0    图绘制指令 + 图注(.docx)
Step 8.0    表格(.docx)
Step 9.0    参考文献组装 + 三轮核验
Step 10.0   最终装配 + 输出
```

---

## 各阶段用户输入模板

**Step 0.0 -- 语言选择**
```
A) 中文  (交互中文; 稿件英文)
B) English  (交互稿件均英文)
默认: B
```

**Step 1.0 -- 项目参数**
```
工作目录: C:/Users/YourName/Documents/MyReview
字数: 5000  (推荐: 4000-6000)
图表: 3 / 2
文献: 100
引用格式: Vancouver
投稿期刊: [期刊名]
```

**Step 2.0 -- 检索策略**
```
数据库: PubMed (默认); WOS, ScienceDirect, Wiley, Embase
年限: 2015-2026
文献类型: 原始研究, 综述, 临床试验
排除: 预印本、会议摘要、社论
```

**Step 4.0 -- LOCK**
```
输入LOCK 锁定框架
或: "将第2节移至第1节之前"
```

**Step 5.0 -- 节确认**
```
CONFIRM  -- 接受
REVISE   -- 修改
REWRITE  -- 重写
```

**Step 9.0 -- 参考文献组装**
```
自动: Claude 编辑清单
手动: 自己在引用管理器中格式化
```

---

## 实际输出文件概述

| 文件 | 路径 | 内容 |
|---|---|---|
| 运行日志 | `pipeline_output/run_log.md` | 全程审计跟踪 |
| 语言 | `pipeline_output/00_language.md` | 语言选择 |
| 前置检查 | `pipeline_output/00_preflight_check.md` | 依赖和网络状态 |
| 项目配置 | `pipeline_output/00_project_config.md` | 所有参数 |
| 检索策略 | `pipeline_output/01_search_strategy.md` | 9项可复现记录 |
| 文献清单 | `pipeline_output/01_reference_list.md` | PMID/DOI |
| 文献笔记 | `pipeline_output/02_literature_notes.md` | 核验笔记+冲突矩阵 |
| 知识图谱 | `obsidian_vault/` | 完整知识图谱 |
| 框架 | `pipeline_output/03_framework.md` | 锁定的大纲 |
| 段落草稿 | `pipeline_output/04_draft_section_*.md` | 含Section Brief |
| 一致性检查 | `pipeline_output/05.5_cross_section_check.md` | 跨节报告 |
| 结论 | `pipeline_output/05_conclusion.md` | 结论草稿 |
| 摘要 | `pipeline_output/05b_abstract.md` | 摘要草稿 |
| 关键词 | `pipeline_output/05c_keywords.md` | MeSH关键词 |
| 图指令 | `pipeline_output/06_figure_instructions.md` | 每图绘制指令 |
| 图注 | `pipeline_output/06_figure_legends.docx` | 独立Word |
| 表格 | `pipeline_output/07_tables_standalone.docx` | 独立Word |
| 参考文献 | `pipeline_output/08_references_final.md` | 完整格式化列表 |
| 终稿txt | `pipeline_output/09_final_manuscript.txt` | 纯文本 |
| 终稿docx | `pipeline_output/09_final_manuscript.docx` | 主文Word |
| 缩略词表 | `pipeline_output/10_abbreviations.docx` | 独立Word |
| 安全日志 | `pipeline_output/10_selfcheck_log.md` | QA记录 |

---

## 输出文章结构

```
标题
摘要(结构化/非结构化)
Keywords (5-8 MeSH)
1. 引言 (300-500 词)
   1.1. / 1.2. ... 正文各节 (结论性标题)
结论 (350-500 词)
表格 | 图注 | 参考文献 | 缩略词表
```

---

## 支持引用格式

| 格式 | 状态 | 说明 |
|---|---|---|
| Vancouver/NLM | 默认 | 完整30种类型内置 | 
| AMA | 支持 | Step 1.0提供URL |
| APA | 支持 | Step 1.0提供URL |
| 期刊定制 | 支持 | 提供示例URL |

**关于NLM Citing Medicine指南:** 本工具使用的Vancouver/NLM格式规则来自*Citing Medicine: The NLM Style Guide for Authors, Editors, and Publishers*, 2nd ed. (Patrias K; NLM, 2007，更新2020). 完整指南包括30种文献类型，内置于vancouver-guide.md。请参阅[Citing Medicine PDF](Citing%20Medicine-The%20NLM%20Style%20Guide%20for%20Authors%2C%20Editors%2C%20and%20Publishers.pdf)或 [NLM在线]( https://www.ncbi.nlm.nih.gov/books/NBK7256/ )

---

## 支持语言

| 组件 | 语言 |
|---|---|
| 稿件输出 | 仅英文 |
| 用户交互 | 中文或英文 (Step 0.0) |
| 平台 | Claude terminal/app，DeepSeek |

---

## 版本更新说明

### v2.1 vs v1.0

| 组件 | v1.0 | v2.1 |
|---|---|---|
| 工作流步骤 | 11 | 19 |
| 文献核验 | 单轮 | 三轮 |
| 分批核验 | 固定 | N/2 动态 |
| 输出Word | 主文一份 | 主文+3独立 |
| Vancouver | 基础 | 内置30种类型 |
| 需求覆盖 | 11 | 40 |

---

## 适用领域

主要: 临床药理学 + 基础药理机制研究

- 药物作用机制 (受体结合、酶抑制、转运体)
- 信号通路与分子靶点（NF-kB / PI3K / MAPK / JAK-STAT / mTOR）
- 药代动力学（ADME，药物相互作用）
- 药物毒性机制（肾毒性、心脏毒性、肝毒性）
- 构效关系(SAR)
- 药物基因组学/精准医学

---

## 安装方式

| 依赖 | 必需 | 用途 |
|---|---|---|
| Claude Code / Kiro CLI | 是 | 运行环境 |
| pdf skill | 是 | 验证PDF (Step 3.0) |
| docx skill | 可选 | Word输出 (Step 10.0) |
| Obsidian | 推荐 | 知识图谱 (Step 3.5) |

```bash
git clone https://github.com/YOUR/narrative-review-skill.git ~/.claude/skills/narrative-review
```

---

## 快速开始

```
您: write a narrative review about [主题]
Claude: Step 0.0 -> 0.0b -> 0.1 -> 0.5 -> 0.9 -> 1.0 -> 2.0 -> 3.0 -> 3.5
        -> 4.0 -> 5.0 -> 5.5 -> 6.0 -> 6.5 -> 6.6 -> 7.0 -> 8.0 -> 9.0 -> 10.0
每步均有确认提示和下一步引导
```

---

## 核心规则

| # | 规则 | 执行方式 |
|---|---|---|
| 1 | 零虚构引用 | 每条引用可追溯PDF |
| 2 | 引用三轮核验 | Steps 3.0+5.0+9.0 |
| 3 | 批判性综合 | 禁止列举，必须评价优缺点 |
| 4 | 平衡覆盖 | 矛盾证据必须讨论 |
| 5 | 引用原始研究 | 一手文献，非综述的综述 |
| 6 | PMID/DOI 三轮核验 | 与PDF交叉验证 |
| 7 | 人工关口确认 | 每步明确批准 |
| 8 | 动态N批量核验 | N<35逐篇; N>=35 N/2触发 |
| 9 | 基因蛋白质命名 | HGNC/MGI/UniProt |
| 10 | 去除AI典型用语 | 每节交付前扫描 |

---

## 研究基础

基于**13篇**同行评审方法学文献 + NLM 引用指南

| 作者(年) | JCR | 核心贡献 |
|---|---|---|
| Dhillon P (2022) | FEBS J Q1 | 范围核查, 图表设计 |
| Chaney MA (2021) | JCVA Q2 | NR 质量标准, NR vs SR |
| Pautasso M (2013) | PLoS Comput Biol Q1 | 十条规则 |
| Gasparyan AY (2011) | Rheumatol Int Q3 | 生物医学NR，作者伦理 |
| Patrias K (NLM 2007) | NLM书籍 | 30种引用类型 |

详见[references.md](references.md) | [references_summary.txt](references_summary.txt)

---

## 文件结构

```
narrative-review/
+-- SKILL.md  # 主工作流推进(v2.1, 19步骤)
+-- README.md  # 英文README
+-- README_zh.md  # 本文件，中文README
+-- vancouver-guide.md  # NLM 30种引用类型(55KB)
+-- preflight-check.md  # 依赖扫描逻辑(v2.1)
+-- quality-checklist.md  # 验收清单(v2.1, 扩展Word文件检查)
+-- search-strategy.md  # 多数据库检索指南
+-- figure-template.md  # 图指令模板(v2.1)
+-- table-template.md  # 表格模板(v2.1)
+-- obsidian-templates.md  # Obsidian笔记模板
+-- nr-vs-sr.md  # NR vs SR 对比表
+-- scope-checklist.md  # 6要素评估表
+-- references.md  # 13篇方法学文献+NLM
+-- references_summary.txt  # 按期刊分区排序/IF
+-- Citing Medicine...pdf  # NLM权威引用指南
```

---

## 关于灰色文献的说明

虽然研究基础包含Paez (2017)的灰色文献检索方法，**本工具仅处理用户提供的已验证同行评审文献**。

---

## 免责声明

**仅供学术研究辅助**。本工具定位为引导学术写作的工具，而非可直接出版的稿件生成系统。用户对以下内容全权负责：

- 所有内容的科学准确性与学术诚信
- 所有引用的最终核实
- 符合目标期刊投稿指南与伦理标准
- 出版所需的同行评審与修订

该工具是写作辅助，不能替代领域专业知识、独立批判思考或学术判断。

---

## 反馈与联系

- **Email:** nixt1998@163.com
- **ORCID:** 0009-0009-6400-4071
- 请在GitHub 提交Issue进行错误报告或功能建议

---

## 贡献

| 姓名 | 单位 | 贡献角色 |
|---|---|---|
| 倪啸庭 (Xiaoting Ni) | School of Pharmacy, Qiqihar Medical University; Dept. of Pharmacy, The First Affiliated Hospital of Harbin Medical University | 创始人 & Lead Developer |
| 傅文瑜 (Wenyu Fu) | School of Pharmacy, Qiqihar Medical University | v2.1优化 |
| [团队名] | [所属单位] | [团队贡献] |

我们欢迎来自药理学、临床药学和 AI 领域的贡献，无论是改进工作流、增加领域知识，还是修复问题。

> **期待您的加入，共同创作开发，为Narrative Review Writing Skill（临床药理学与基础药理机制研究叙述性综述写作技能）更好的发展!**

---

## 更新记录

### v2.1 -- 2026-07-09

本次重大更新将11步骤基础框架升级为19步骤生产级工作流，整合34条原始需求, 6条追加需求, 8项架构修复, 20项一致性改进

**新增:** Step 0.0 语言选择, 0.0b 平台选择, 0.9 标题确认, 6.5 摘要, 6.6 MeSH关键词, 分批输出协议, Section Brief, 动态N分批核验, 运行日志, 多数据库检索, 独立Word输出, 基因蛋白质命名; **变更:** Step 4.5重命名为5.5，Vancouver内置，无外部路径依赖; **修正：** 核验率阈值统一（90% 返工底线 / 95% 目标），文件名 04.5 → 05.5。

### v1.0 -- 2026-06-30

初始版本发布. 建立11步骤核心工作流，包含零虚构引用、双轨上下文架构，Obsidian知识图谱生成，Vancouver格式，冲突证据矩阵，13篇方法学文献。

**新增:** 11步骤完整工作流, 零虚构协议, 知识图谱, Vancouver引用格式, 关键条件检验和人工关口

---

## 许可证

MIT -- 详见[LICENSE](LICENSE)

---

<p align="center">
  <sub>为 ❤️ 严谨、可复现的科学写作而构建</sub>
</p>
