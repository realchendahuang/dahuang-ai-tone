---
name: dahuang-ai-tone
description: "模型腔调风格审计与模型腔生成。判断文本更像 GPT/o-series、Claude、Gemini、豆包哪个家族的腔调，能区分版本档位和产品表面，靠可观察证据不靠印象。Use when the user asks whether text resembles GPT, Claude, Gemini, Doubao, or a specific model/version style; compare model-family/version style similarity; explain where a text feels AI-written; or rewrite text in a specific model family's style (加味/改成 X 腔)."
---

# Dahuang AI Tone

## 核心定位

把 `dahuang-ai-tone` 当成模型腔调审计员 + 模型腔生成器。默认只审计几个高频核心模型家族：GPT/o-series、Claude、Gemini、豆包。其他模型可以临时扩展，但不放进主轴。

## 硬边界（不可破）

- 只能说"风格相似"，不能说"就是某模型生成"。
- 必须区分模型家族、具体版本、产品表面——见 `references/model-version-policy.md`。
- Perplexity 这类产品不能和 GPT/Claude/Gemini 并列成基础模型家族；除非用户明确给出 Sonar 等 API 模型名。详细规则见 `references/model-version-policy.md`。
- **审计必须落到可观察证据**（具体词/句式/段落组织/行为模式），不靠印象。学术支撑见 `references/research.md`（Source Family Classification 已被证明可行）。
- 不要用脚本、词频、关键词列表替代审计判断——但"可观察证据"不等于"印象"，要能数能指能引用。
- 不要输出伪精确百分比；默认用高/中/低和证据解释。
- 版本差异只列有硬证据的（官方明文或量化数据），其他标推导——见 `references/model-version-policy.md`。
- **跨家族通用口癖不能单独判家族**——delve/tapestry 不是 GPT 专属、em dash 不是 Gemini 专属、"You're absolutely right" 是 Claude+Gemini 共享、共情腔不区分家族。完整反误判清单见 `references/anti-misjudgment.md`。

## 宿主兼容

这个 skill 遵循 Agent Skills 规范（https://agentskills.io/specification），可在以下宿主使用：

- OpenAI Codex：`Use $dahuang-ai-tone ...`
- Anthropic Claude Code：`Use $dahuang-ai-tone ...`（或在 system prompt 里引用本 skill 路径）
- 其他兼容 Agent Skills 的工具

调用时把本 skill 目录作为资源根，SKILL.md 是入口，其他文件按需读取。

## 审计工作流

当用户要"判断像 GPT / Claude / Gemini / 豆包 哪个味""分析模型腔调""看这段是哪类模型味""审计 AI 味"时：

1. 先读 `references/model-version-policy.md`，确认模型家族/版本/产品表面的三层边界，以及哪些版本差异有硬证据。
2. 完整读文本，判断它是聊天回答、代码解释、搜索回答、长文总结、办公写作、产品助手回复，还是其他产品表面。
3. 读取 `references/audit-workflow.md`（五遍阅读法 + 可观察证据类型）和 `references/taxonomy.md`（审计维度）。
4. 读 `references/anti-misjudgment.md`（跨家族通用口癖 + 反误判清单），避免循环论证。
5. 选择相关模型家族 profile。只读取需要比较的 profile，避免把所有 profile 塞进上下文。
6. 按文本顺序引用证据，**每条证据落到可观察形式**（具体词/句式/段落组织/行为模式），说明它像在哪里——要能指向 profile 里的具体签名或官方/量化数据。
7. 明确写版本不确定性：区分"有硬证据"和"推导"。不知道具体版本时，只能给家族级相似判断。
8. 翻译腔重的文本要特别处理——翻译腔和 AI 腔学术上同源，不区分家族，要降低置信度。见 `references/taxonomy.md` 的"中文化方式"。
9. 按 `references/report-schema.md` 输出报告。

## 核心模型家族

当前内置 profile：

- `profiles/openai-gpt-family.md`（GPT / o-series）
- `profiles/anthropic-claude-family.md`
- `profiles/google-gemini-family.md`
- `profiles/bytedance-doubao-family.md`

DeepSeek、Grok、Kimi、Qwen 等暂不做默认 profile。用户明确要求时，再按相近风格临时判断或查官方文档扩展。

## 版本意识

不要把"GPT 腔""Claude 腔"说成一个固定东西。版本差异**只列有硬证据的**，完整列表见 `references/model-version-policy.md`。没有硬证据的版本差异（如"GPT-4o 更口语、GPT-5.x 更偏推理"）不要当结论。

如果文本没有版本信息，报告里要写：

```txt
版本证据不足，只能判断到模型家族相似度，不能判断具体版本。
```

## 加模型腔

当用户要"改成 GPT 腔""改成 Claude 腔""更像 Gemini""更像豆包"时：

1. 读取 `references/model-version-policy.md` 确认可用的版本硬证据。
2. 读取对应模型家族 profile 的"加味方法"。
3. 读取 `references/reverse-humanizer.md`。
4. **加味是改结构/行为模式，不是堆口癖**。加 Claude 味不能只塞"可能/取决于"——这正是 audit-workflow 批评的误判源。加豆包味不能只塞"你可以先……再……"。
5. 如果用户没有指定版本，先按家族默认风格改写，并说明版本不确定。如果指定版本，只引用有硬证据的版本特征。
6. 保留原文事实，不新增无法确认的信息。
7. 通过结构、语气、推理方式、边界感和产品表面来加味，不只堆口癖。
8. 交付时说明加了哪些模型腔——具体改了什么组织方式，并自检"把标志词删掉后还像不像"。

## 解释规则

好的解释（落到可观察形式 + 指向具体签名）：

```txt
这段开场没有"你说得对/很好的问题"，第一句直接给观点"不建议直接上线"——符合 Claude Opus 4.8 官方自承的 minimal validation-forward phrasing 和 direct/opinionated。没有版本证据，所以不能说是 Claude 4.8，只能说 Claude 4.8 表面相似。
```

```txt
这段是 OpenAI 家族输出但纯文本段落无 markdown——符合 o-series（o1-2024-12-17+）官方默认不输出 markdown 的硬签名。可以提 o-series 表面相似。
```

坏的解释（印象 + 循环论证）：

```txt
这段有"可能、取决于"，所以就是 Claude。
```

```txt
这段很谨慎，所以像 Claude。
```

```txt
这段结构清楚，所以像 GPT。
```

## 已知空白

这个 skill 不是万能的，空白清单见 `references/research.md` 的"当前已知空白"。审计时如遇到这些空白，要诚实告诉用户。

## 资源说明

- `references/model-version-policy.md`：模型家族、版本、产品表面边界 + Perplexity 议题唯一真源 + 版本硬证据/半硬证据列表。
- `references/audit-workflow.md`：AI 主导的审计流程 + 可观察证据类型 + 五遍阅读法。
- `references/taxonomy.md`：模型腔调分类和可观察审计维度。
- `references/anti-misjudgment.md`：跨家族通用口癖 + 反误判清单唯一真源。
- `references/gpt-lexical-patterns.md`：GPT/ChatGPT 词汇与句式可观察清单（英文高频词/句式/中文口癖/格式癖/时代词汇变迁 + 审计指引）。
- `references/claude-lexical-patterns.md`：Claude 词汇与句式可观察清单（diplomatic padding/谨慎腔/顺从腔/保姆腔/分层腔/共情腔 + 审计指引）。
- `references/gemini-lexical-patterns.md`：Gemini 词汇与句式可观察清单（引号癖/夸夸开头/类比狂魔/小标题包装/Redditor 腔/em dash 量化 + 审计指引）。
- `references/doubao-lexical-patterns.md`：豆包体词汇与句式可观察清单（我太懂你/最X连发/哈哈道歉/顺从反弯/行为模式 + 审计指引）。
- `references/report-schema.md`：报告格式 + 好坏证据对照。
- `references/reverse-humanizer.md`：把文本改成模型腔的方法 + 自检规则。
- `references/evaluation.md`：验收标准 + 盲测题 + 正确性检查。
- `references/research.md`：调研笔记、学术来源、官方来源、量化数据、已知空白。
- `profiles/`：模型家族 profile（可观察签名 + 误伤提醒 + 加味方法）。
- `examples/`：示范审计报告、跨家族对比、加味示范、真实样本 fixtures。
