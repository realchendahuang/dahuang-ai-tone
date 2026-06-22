---
name: dahuang-ai-tone
description: "AI 味玩梗 skill。不同模型风格有不同的 AI 味，这里是它们的味标本馆。把正常文本加成 GPT/Claude/Gemini/豆包的纯味，或者指出一段文本里的 AI 味在哪、像哪个风格。Use when: 加 AI 味、改成 GPT 腔/Claude 腔/Gemini 腔/豆包腔、把这段改成某模型味、检测 AI 味、这段哪里像 AI、AI 味在哪、模型腔调、AI 味特征、AI 味梗、玩 AI 味的梗、去 AI 味的前置知识. Also use for: AI writing style, model fingerprint, AI 味, 模型腔, 加味, 改写风格, 风格相似度."
license: MIT
compatibility: "Designed for OpenAI Codex and Anthropic Claude Code, or other Agent Skills compatible hosts."
metadata:
  version: "3.0.0"
  author: realchendahuang
---

# Dahuang AI Tone

## 这是什么

一个玩 AI 味的梗的 skill。AI 味是梗，加味是玩梗，认味是认梗。

它做两件事：

1. **加味**（主）——把正常文本改成某个模型风格的纯味。改的是结构、语气、行为模式，不是堆口癖。
2. **找味**（次）——指出一段文本里的 AI 味在哪、像哪个风格。

为什么有这个 skill：**知道了什么是 AI 味，才能在别处去掉 AI 味**。但去 AI 味不是这个 skill 的事——这个 skill 只负责把 AI 味玩明白。这里是四大模型风格的味标本馆，来尝味、来玩梗。

## 四大模型风格的味

每个风格有自己的味。想尝味，读对应风格的 profile + 词汇句式清单——这是这个 skill 的主菜：

| 风格 | Profile（签名 + 加味方法） | 词汇句式清单（味标本） |
|---|---|---|
| OpenAI GPT / o-series | `profiles/openai-gpt-style.md` | `references/gpt-lexical-patterns.md` |
| Anthropic Claude | `profiles/anthropic-claude-style.md` | `references/claude-lexical-patterns.md` |
| Google Gemini | `profiles/google-gemini-style.md` | `references/gemini-lexical-patterns.md` |
| 字节豆包 / Doubao | `profiles/bytedance-doubao-style.md` | `references/doubao-lexical-patterns.md` |

一句话闻味：

- **GPT** 像方法论小作文——结论先行、分点升华、温情诗化。
- **Claude** 像温柔谨慎的编辑——克制、边界感、That said、劝你睡觉。
- **Gemini** 像热情的解释型辅导老师——引号癖、夸夸开头、Think of it like this。
- **豆包** 像嘴甜但容易糊弄的实习生——我太懂你、最X连发、哈哈抱歉抱歉。

DeepSeek、Grok、Kimi、Qwen 等暂不做默认 profile，用户明确要求时临时扩展。

## 加味（主玩法）

把正常文本改成某风格的纯味。

1. 读对应风格 profile 的"加味方法" + `references/reverse-humanizer.md`。
2. **加味改的是结构/语气/行为模式，不是堆标志词**。加 Claude 味不能只塞"可能/取决于"，加豆包味不能只塞"你可以先……再……"。
3. 想加哪个版本的味（如 Claude 4.8 直球、3.x 谨慎、o-series 无 markdown），看 profile 里的版本味说明。
4. 自检：**把加的标志词删掉，文本还像不像那个风格？**不像就是堆口癖，重做。
5. 交付时说明加了哪些味——具体改了什么组织方式。示范见 `examples/injection-report.md`。

## 找味（次玩法）

指出一段文本里的 AI 味在哪、像哪个风格。

1. 读对应风格 profile + lexical-patterns。
2. 按文本顺序引用原文，每条指出它像哪个风格的什么味（具体词/句式/段落组织/行为模式）。
3. 只说"风格相似"，不说"就是某模型生成的"——这是玩梗认味，不是来源鉴定。
4. 不知道具体版本时只给风格级判断。
5. 示范见 `examples/audit-report.md`。想看跨风格对比见 `examples/comparison.md`，想看真实味标本见 `examples/fixtures.md`。

## 玩梗纪律（认味不丢人的底线）

- **只能说"风格相似"，不能说"就是某模型生成"**。
- **判断要落到可观察的东西**——具体词、句式、段落组织、行为模式，能指能引用，不靠印象。
- **跨风格通用口癖不能单独判风格**——这是最容易认错梗的地方：
  - `delve` / `tapestry` 不是 GPT 专属，是跨风格 AI 通用词。
  - em dash 不是 Gemini 专属（arXiv 数据：Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低）。
  - "You're absolutely right" 是 Claude + Gemini 跨风格共享。
  - "不是 X 而是 Y" 是跨风格 AI 通用句式。
  - 共情腔（"我能理解你为什么会这么想"）豆包、ChatGPT 中文疗愈腔都有。
  - 判断力在**密度和组合**，不在单个词。每个 lexical-patterns 文件末尾的"认味指引"列了专属 vs 通用的边界。
- **这是玩梗，不是来源鉴定**，别拿去做严肃取证。

## 宿主兼容

这个 skill 遵循 Agent Skills 规范（https://agentskills.io/specification），可在以下宿主使用：

- OpenAI Codex：`Use $dahuang-ai-tone ...`
- Anthropic Claude Code：`Use $dahuang-ai-tone ...`（或在 system prompt 里引用本 skill 路径）
- 其他兼容 Agent Skills 的工具

调用时把本 skill 目录作为资源根，SKILL.md 是入口，其他文件按需读取。

## 资源说明

- `profiles/`：四大模型风格的味签名 + 加味方法 + 版本味说明。
- `references/*-lexical-patterns.md`：四大模型风格的词汇句式味标本（每份末尾有"专属 vs 跨风格通用"的认梗指引）。
- `references/reverse-humanizer.md`：加味主方法 + 自检规则。
- `examples/injection-report.md`：加味示范（同一段原文加成不同风格的味）。
- `examples/audit-report.md`：找味示范。
- `examples/comparison.md`：跨风格对比 + 同一意思不同风格怎么写。
- `examples/fixtures.md`：真实味标本（官方/Aider/学术来源），拿来尝味。
- `agents/openai.yaml`：Codex 专属 UI 元数据（可选，不影响 skill 功能）。
