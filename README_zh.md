<!--
╬══════════════════════════════════════════════════════════╬
  Author / 作者
  Name / 姓名:  倪啸庭  (Xiaoting Ni)
  Affiliation: School of Pharmacy, Qiqihar Medical University
               Dept. of Pharmacy, The First Affiliated Hospital
               of Harbin Medical University
  Email:       nixt1998@163.com
  ORCID:       0009-0009-6400-4071
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

# Narrative Review Writing Skill
## 叙述性综述写作技能 · 临床药理学与基础药理机制研究

### 为药学领域严谨、可复现、循证据的叙述性综述写作，提供结构化AI辅助流程，基于NLM范式与13篇同行评审方法学文献

**19 个工作流步骤 · 40 条需求规范 · 30 种NLM引用类型 · 13 篇方法学文献 · 零虚构文献**

> ⭐ 如果这个技能对您的研究有帮助，请 **star** 该项目以示支持！

</div>

---

## 总目的

建立严谨、可复现、循证据的药学叙述性综述写作框架，帮助研究者产出符合最高科学诚信标准的出版级稿件。本技能架桔了AI辅助与学术严谨性之间的鸿沟，将结构化工作流强制与不可或缺的人类判断内在整合。

---

## 目录

- [为什么选择「人机协作」](#为什么选择人机协作)
- [优势对比](#优势对比)
- [功能特色](#功能特色)
- [能做什么，不能做什么](#能做什么)
- [适用人群](#适用人群)
- [工作流总览](#工作流总览)
- [各阶段用户输入模板](#输入模板)
- [实际输出文件概述](#输出文件)
- [输出文章结构](#文章结构)
- [支持引用格式](#引用格式)
- [支持语言](#语言)
- [版本更新说明](#版本更新)
- [适用领域](#领域)
- [安装方式](#安装)
- [快速开始](#快速开始)
- [核心规则](#核心规则)
- [研究基础](#研究基础)
- [免责声明](#免责声明)
- [贡献](#贡献)
- [更新记录](#更新记录)

---

## 为什么选择「人机协作」，而非「全自动流程」。

药学文献机制复杂、进展迅速。全自动化流程存在虚构引用、机制论述过度简化、批判性综合失调等问题。纯手动写作则耗时耗力、组织不一致。

本工具采用「人机协作」模式：

- **AI 负责:** 结构强制、格式合规、防幻觉协议、系统化三轮核验、大规模文献集上下文管理。
- **研究者负责:** 科学判断、文献选择、机制论述解释、框架决策及每个关键步骤的确认。

每个关键节点——框架锁定、段落确认、参考文献核验——研究者均需明确批准。这不是一键生成稿件的工具，而是一种精密仪器，在保留每个关键判断的同时放大研究能力。

---

## 优势对比

| 维度 | 纯手动 | 全自动 | 其他技能 | NRW v2.1 |
|---|:---:|:---:|:---:|:---:|
| 零虚构引用 | ✅ | ❌ | ⚠️ | ✅✅ |
| 引用三轮核验 | ⚠️ | ❌ | ❌ | ✅ |
| 人工关口确认 | ✅ | ❌ | ⚠️ | ✅ |
| 100+ 文献上下文管理 | ❌ | ⚠️ | ❌ | ✅ |
| 动态N批量核验协议 | ❌ | ❌ | ❌ | ✅ |
| Obsidian 知识图谱 | ❌ | ❌ | ❌ | ✅ |
| Section Brief(写作逻辑) 输出 | ❌ | ❌ | ❌ | ✅ |
| Vancouver/NLM 30种类型完整规则 | ⚠️ | ⚠️ | ⚠️ | ✅ |
| 基因/蛋白质命名规范强制 | ⚠️ | ❌ | ❌ | ✅ |
| 多平台 (DeepSeek/Claude) | - | ⚠️ | ❌ | ✅ |
| 可复现检索记录 | ⚠️ | ⚠️ | ❌ | ✅ |
| 独立Word分量输出 | ❌ | ❌ | ❌ | ✅ |
| 保留科学判断 | ✅ | ❌ | ⚠️ | ✅ |
| 耗时 | 很高 | 很低 | 中 | 中 |

✅ 完全支持 · ⚠️ 部分/不确定 · ❌ 不支持/高风险

---

## 功能特色

全部详情请参阅 [SKILL.md](SKILL.md)

1. **动态防幻觉协议** -- 任何引用必须可追溯至已验证PDF；无法核验的直接排除
2. **动态N分批核验** -- N<35 逐篇; N≥35 每批≥50%抄查
3. **Obsidian 知识图谱** -- 大规模文献集上下文管理
4. **Section Brief** -- 写作前强制输出写作逻辑
5. **分批输出协议** -- DeepSeek/Claude 全平台兼容
6. **多数据库可复现检索** -- 9项完整记录
7. **基因/蛋白质命名规范** -- HGNC/MGI/UniProt
8. **独立模块Word输出** -- 图说/表格/缩略词表
9. **完整引用规范** -- 内置vancouver-guide.md (30种类型)
10. **运行日志** -- 全程审计跟踪

---

## 能做什么，不能做什么

### 可以:
- 提供19步标准工作流
- 强制防幻觉
- 100+篇文献上下文管理
- 基因/蛋白质符号核验
- Vancouver/NLM/AMA/APA格式引用
- 独立Word文件

### 不可以:
- 替代科学判断
- 评估文献方法学质量
- 产生文献之外的新假说
- 替代同行评審

> **关于独立思考:** 工具强制框架，您提供科学。全程以批判性思维审视。**

---

## 适用人群

推荐: 药学/临床药学研究者、博士生、博后

---

## 工作流总览 (v2.1 -- 19 步骤)

```
Step 0.0    语言选择                                          [v2.1 NEW]
Step 0.0b   模型与平台选择                                    [v2.1 NEW]
Step 0.1    NR vs SR 介绍
Step 0.5    前置环境检查
Step 0.9    标题确认                                          [v2.1 NEW]
Step 1.0    项目参数 + 范围界定
Step 2.0    多数据库检索策略 + 文献清单
Step 3.0    文献验证 + 结构化笔记 + 冲突证据矩阵
Step 3.5    Obsidian 知识图谱生成
Step 4.0    框架生成 -> 确认 -> LOCK
Step 5.0    逐节写作 (含Section Brief)
Step 5.5    跨节一致性检查                              [巠 Step 4.5]
Step 6.0    结论
Step 6.5    摘要                                          [v2.1 NEW]
Step 6.6    Keywords (MeSH)                                  [v2.1 NEW]
Step 7.0    图绘制指令 + 图注 (.docx)
Step 8.0    总结表格 (.docx)
Step 9.0    参考文献组装 + 三轮核验
Step 10.0   最终装配 + 输出
```

---

## 各阶段用户输入模板

**Step 0.0 -- 语言选择**
```
A) 中文  B) English
```

**Step 1.0 -- 项目参数**
```
工作目录: C:/Users/YourName/Documents/MyReview
字数: 5000 words
图表: 3/2
文献: 100
引用格式: Vancouver
投稿期刊: [期刊名, e.g., Pharmacological Research]
```

**Step 4.0 -- LOCK**
```
输入LOCK 或修改指令
```

**Step 5.0 -- 节确认**
```
CONFIRM / REVISE / REWRITE
```

---

## 实际输出文件概述

详见 [README.md](README.md) 中的输出文件表格:

| 文件 | 路径 | 内容 |
|---|---|---|
| 运行日志 | `pipeline_output/run_log.md` | 全程跟踪 |
| 文献清单 | `pipeline_output/01_reference_list.md` | PMID/DOI+文件名 |
| 知识图谱 | `obsidian_vault/` | 完整知识图谱 |
| 框架 | `pipeline_output/03_framework.md` | LOCK后的大纽 |
| 分节草稿 | `pipeline_output/04_draft_section_*.md` | 含Section Brief |
| 图注 | `pipeline_output/06_figure_legends.docx` | 独立Word |
| 表格 | `pipeline_output/07_tables_standalone.docx` | 独立Word |
| 终稿 | `pipeline_output/09_final_manuscript.docx` | 主文正文 |
| 缩略词表 | `pipeline_output/10_abbreviations.docx` | 独立Word |

---

## 输出文章结构

```
标题
摘要 (结构化或非结构化)
Keywords (5-8 MeSH)
1. 引言 (300-500 词)
   1.1. / 1.2. ... 正文各节（结论性标题
结论 (350-500 词)
表格 | 图注 | 参考文献 | 缩略词表
```

---

## 支持引用格式

| 格式 | 状态 | 说明 |
|---|---|---|
| Vancouver/NLM | 默认 | 完整内置, 30种文献类型, 详见[Citing Medicine PDF](Citing%20Medicine-The%20NLM%20Style%20Guide%20for%20Authors%2C%20Editors%2C%20and%20Publishers.pdf) |
| AMA | 支持 | Step 1.0 提供期刊指南URL |
| APA | 支持 | Step 1.0 提供期刊指南URL |
| 期刊定制 | 支持 | 提供示例参考文献或指南URL |

---

## 支持语言

| 组件 | 语言 |
|---|---|
| 稿件输出 | 仅英文 |
| 用户交互 | 中文或英文 (Step 0.0选择) |
| 平台 | Claude terminal/app, DeepSeek |

---

## 版本更新说明

### v2.1 vs v1.0

| 组件 | v1.0 | v2.1 |
|---|---|---|
| 工作流步骤 | 11 | 19 |
| 文献核验 | 单轮 | 三轮 |
| 批量閘验 | 固定阈値 | N/2 动态 |
| 输出Word | 主文一份 | 主文+3独立 |
| Vancouver | 基础 | 内置30种类型 |
| 需求覆盖 | 11 | 40 |

---

## 适用领域

主要: 临床药理学 + 基础药理机制研究

- 药物作用机制 (受体结合、酶抑制、转运体)
- 信号通路与分子靶 (NF-kB/PI3K/MAPK/JAK-STAT)
- 药代动学(ADME,药物相互作用)
- 药物毒性机制 (肆毒、心毒、肝毒)
- 构效关系(SAR)
- 药物基因组学/精准医学

---

## 安装方式

| 依赖 | 必需 | 用途 |
|---|---|---|
| Claude Code / Kiro CLI | 是 | 运行环境 |
| pdf skill | 是 | PDF验证(Step 3.0) |
| docx skill | 可选 | Word输出(Step 10.0) |
| Obsidian | 推荐 | 知识图谱(Step 3.5) |

```bash
git clone https://github.com/YOUR_USERNAME/narrative-review-skill.git ~/.claude/skills/narrative-review
```

---

## 快速开始

```
您: write a narrative review about [主题]
Claude: Step 0.0 语言选择 -> Step 0.0b 平台 -> Step 1.0 参数 ... -> Step 10.0 交付
```

---

## 核心规则

1. **零虚构引用** -- 每条可追溯PDF
2. **引用三轮核验** -- Steps 3.0+5.0+9.0
3. **人工关口确认** -- 每步明确批准
4. **动态N批量** -- N<35逐篇; N>=35 N/2触发
5. **基因蛋白质命名** -- HGNC/MGI/UniProt
6. **禁止AI典型用语** -- 交付前扫描去除

---

## 研究基础

基于13篇同行评审方法学文献，+ NLM 引用指南

| 作者(年) | 来源 | 核心贡献 |
|---|---|---|
| Dhillon P (2022) | FEBS J Q1 | 范围核查, 图表设计 |
| Chaney MA (2021) | JCVA Q2 | NR 质量标准 |
| Pautasso M (2013) | PLoS Comput Biol Q1 | 十条规则 |
| Gasparyan AY (2011) | Rheumatol Int Q3 | 作者签名伦理 |
| Patrias K (NLM 2007) | NLM书籍 | 30种类型引用规范 |

详见[references.md](references.md) | [references_summary.txt](references_summary.txt)

---

## 文件结构

```
narrative-review/
+-- SKILL.md # 主工作流推进(v2.1 19步骤)
+-- README.md # 英文README
+-- README_zh.md # 中文README
+-- vancouver-guide.md # NLM 30种引用规则
+-- preflight-check.md # 依赖扫描逻辑
+-- quality-checklist.md # 验收清单v2.1
+-- search-strategy.md # 多数据库检索指南
+-- Citing Medicine...pdf # NLM权威引用指南
```

---

## 免责声明

**仅供学术研究参考**。本工具为辅助学术写作的工具，非完整的可直接发表的稿件生成系统。用户对以下内容负责: 内容科学准确性, 引用核实, 期刊要求合规, 同行评审过程。

---

## 反馈与联系

- **Email:** nixt1998@163.com
- **ORCID:** 0009-0009-6400-4071
- GitHub Issue 进行错误报告或功能建议

---

## 贡献

| 姓名 | 单位 | 贡献角色 |
|---|---|---|
| 倪啸庭 (Xiaoting Ni) | School of Pharmacy, Qiqihar Medical University; Dept. of Pharmacy, The First Affiliated Hospital of Harbin Medical University | 创始人 & Lead Developer |
| [您的姓名] | [您的单位] | [贡献描述] |
| [科研团队名] | [所在单位] | [团队贡献] |

> **期待您的加入，共同创作开发，为Narrative Review Writing Skill（面向临床药理学与基础药理机制研究的叙述性综述写作技能）更好的发展!**

---

## 更新记录

### v2.1 -- 2026-07-09

本次重大更新将11步骤基础框架升级为19步骤生产级工作流，将34条原始需求, 6条追加需求, 8项架构修复, 20项一致性改进全部融入。
**新增:** Step 0.0语言, 0.0b平台, 0.9标题, 6.5摘要, 6.6 MeSH关键词, 分批协议, Section Brief, 动态N批量, 日志, 实语行, 独立Word; **变更:** Step 4.5 -> 5.5, Vancouver内置; **修正:** 閘验率阈値统一(90%返工/95%目标), 文件名04.5->05.5

### v1.0 -- 2026-06-30

初始版本, 建立11步骤基础工作流，包含零虚构引用、双轨架构、知识图谱、Vancouver格式、冲突证据矩阵等13篇方法学文献支d。

---

## 许可证

MIT -- 详见[LICENSE](LICENSE)

---

<p align="center">
  <sub>为 ❤️ 严谨、可复现的科学写作而构建。</sub>
</p>
