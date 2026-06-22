# 模型版本策略

> 这是"模型家族 / 版本 / 产品表面"三层边界和 Perplexity 议题的**唯一真源**。其他文件只引用，不重复。

## 为什么必须区分版本

"GPT 腔""Claude 腔"只是粗标签。同一模型家族不同版本、不同推理模式、不同产品系统提示，都会改变输出风格——而且有些差异是**官方明文承认**的，不是印象。

审计前必须先问或自行判断：

1. 用户说的是模型家族，还是具体模型版本？
2. 文本来自 API、网页产品、插件、搜索产品，还是二次封装？
3. 有没有已知系统提示、模板、RAG、搜索引用或工具调用？
4. 文本是否经过人工改写、混写、翻译或压缩？

不知道这些信息时，只能给"风格相似度"，不能做来源判断。

## 三层标签

### 1. 模型家族

- OpenAI GPT / o-series
- Anthropic Claude
- Google Gemini
- 字节豆包 / Doubao

默认只维护这四个核心家族。其他模型（DeepSeek、Grok、Kimi、Qwen 等）可按用户明确要求临时扩展，但不做默认 profile。

### 2. 版本/档位

版本差异**有硬证据的**才写进 profile，没有硬证据的只能标"推导"。

- GPT-4o / GPT-4.1 / GPT-5.x / mini / nano / pro / o-series
- Claude Haiku / Sonnet / Opus / 3.x / 3.5 / 4.x / 4.5 / 4.6 / 4.8
- Gemini Pro / Flash / Flash-Lite / preview / stable / experimental
- Doubao Seed / Pro / Code / 产品助手封装

### 3. 产品表面

产品表面不是模型。它通常包含系统提示、工具、搜索、RAG、引用格式和安全策略：

- ChatGPT、Claude.ai、Gemini app、Perplexity
- Cursor / Claude Code / Codex
- 豆包 App

## Perplexity 的位置

Perplexity **不是基础模型家族**，不能和 GPT/Claude/Gemini 并列。

正确说法：

- Perplexity 作为消费产品：检索增强搜索回答产品表面。
- Perplexity Sonar API：Perplexity 提供的 Sonar 系列模型/搜索 API。

审计时可以说：

```txt
这段像 Perplexity 式检索增强回答：先综合搜索结果，再给带引用的简短结论。
```

不要说：

```txt
这段像 Perplexity 模型。
```

除非用户明确提供 API 模型名（Sonar / Sonar Pro / Sonar Reasoning Pro 等）。

## 版本差异的硬证据 vs 推导

审计员判断版本时，必须区分"有硬证据"和"推导"。

### 有硬证据的版本差异

这些是官方明文或量化数据支撑的，可以直接引用：

- **o-series（o1-2024-12-17+）默认不输出 markdown**，需 developer message 里写 `Formatting re-enabled` 才开。来源：OpenAI reasoning-best-practices 官方文档。
- **Claude Opus 4.8 转向 direct/opinionated，minimal validation-forward phrasing，sparing emoji**；区别于 3.x/4.5/4.6 的过度 hedging 和 overengineering。来源：Anthropic 官方 prompting-claude-opus-4-8 文档。
- **Claude Opus 4.5/4.6 有过度工程倾向**（造多余文件、加不必要抽象、滥用 subagent）。来源：Anthropic 官方 best-practices 文档。
- **chatgpt-4o-latest 代码格式合规率仅 64.4%、畸形响应 85 次**（225 题基准），远低于 Claude/Gemini。来源：Aider polyglot 榜单。
- **Gemini 2.5 Pro 格式合规率 ~100%、0 畸形**，偏好 `diff-fenced` 编辑格式。来源：Aider polyglot 榜单。
- **DeepSeek R1 (architect 模式) 澄清提问 392 次**，远超所有其他模型。来源：Aider polyglot 榜单。

### 半硬证据（社群整理，非官方明文）

- **GPT-4/4o/5 时代高频词变迁**（Wikipedia 社群整理）：GPT-4 时代词表更广（delve/tapestry/testament/intricate/meticulous 等），GPT-4o 时代收缩（align with/fostering/showcasing 等），GPT-5 时代只剩几个（emphasizing/enhance/highlighting/showcasing）。Wikipedia 提醒"不是硬切分"。完整词表见 `references/gpt-lexical-patterns.md` 第八节。可作为版本判断的半硬证据（低置信度）。

### 推导（无硬证据，只能低置信度提）

- "GPT-4o 更口语、GPT-5.x 更偏推理"这类说法没有同 prompt 对照样本，不要当成结论。
- "Gemini 知识卡片化"是业界共识但缺官方文本证据。
- 豆包的版本差异目前无任何硬数据。

## 当前官方来源

这些列表会变，审计前如果要判断"当前版本"，必须查官方文档：

- OpenAI models: https://developers.openai.com/api/docs/models
- OpenAI reasoning best practices: https://platform.openai.com/docs/guides/reasoning-best-practices
- Anthropic Claude models: https://platform.claude.com/docs/en/about-claude/models/overview
- Anthropic prompting Claude Opus 4.8: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompting-claude-opus-4-8
- Anthropic prompting best practices: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-prompting-best-practices
- Google Gemini models: https://ai.google.dev/gemini-api/docs/models
- 火山方舟模型列表: https://www.volcengine.com/docs/82379/1330310
- Perplexity Sonar models: https://docs.perplexity.ai/docs/sonar/models
- Aider polyglot 榜单: https://aider.chat/docs/leaderboards/

## 报告口径

强口径（有硬证据时）：

```txt
这段默认无 markdown 格式，符合 o-series（o1-2024-12-17+）的官方签名；但没有模型名证据，只能判断到 OpenAI o-series 表面相似。
```

弱口径（推导时）：

```txt
它有 Claude 家族常见的边界感，但没有版本特征能区分 3.x 还是 4.x。
```

禁止口径：

```txt
这是 Claude 4.5 写的。
```
