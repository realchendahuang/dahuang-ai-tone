# Dahuang AI Tone

大黄 AI 腔：模型腔调风格审计 Skill。

它做两件事：

- 审计一段文字更像哪个模型家族 / 版本时代 / 产品表面。
- 按指定模型家族或版本表面，把文字改得更像那个模型。

## 核心原则

这是风格审计，不是模型来源鉴定。**审计必须落到可观察证据**（具体词/句式/段落组织/行为模式），不靠印象。学术上 Source Family Classification 已被证明可行（见 `references/research.md`）。

可以说：

```txt
这段开场无 validation-forward、第一句直接给观点，符合 Claude Opus 4.8 官方自承的 direct/opinionated 风格。没有版本证据，只能说 Claude 4.8 表面相似。
```

不能说：

```txt
这段就是 Claude 4.5 写的。
```

```txt
这段很谨慎，所以像 Claude。
```

Perplexity 不能和 GPT / Claude / Gemini 直接并列成基础模型家族。更准确的说法：

```txt
这段像 Perplexity 式检索增强回答表面。
```

## 使用方式

这个 skill 遵循 Agent Skills 规范（https://agentskills.io/specification），可在以下宿主使用：

### OpenAI Codex

```txt
Use $dahuang-ai-tone 审计下面这段文字更像哪个模型家族，注意区分版本和产品表面，证据要落到可观察形式。
```

### Anthropic Claude Code

```txt
Use $dahuang-ai-tone 把下面这段改成 Claude Opus 4.8 风格，不要堆"可能/取决于"，要改开场和收尾的组织方式。
```

### 其他兼容 Agent Skills 的工具

把本 skill 目录作为资源根，`SKILL.md` 是入口，其他文件按需读取。

## 当前内置核心模型家族

- OpenAI GPT / o-series
- Anthropic Claude
- Google Gemini
- 字节豆包 / Doubao

## 当前已知空白

诚实记录，不掩饰：

1. 缺同一 prompt 跨四家真实对比样本——"同义不同写"的对比都是推导。
2. Gemini 官方文档 fetch 被墙，纯文本散文真实样本缺失——但 Gemini 现在有社区/媒体/学术多源报道的口癖证据（Reddit/Scientific American/TechRadar/arXiv）。
3. 豆包专属硬特征缺失——豆包 profile 用 DeepSeek/Qwen/Kimi 作中文模型代理。
4. 多数版本差异是推导——只有 `references/model-version-policy.md` 列的几条有硬证据。

详细空白说明见 `references/research.md`。

## 参考

- OpenAI models: https://developers.openai.com/api/docs/models
- OpenAI reasoning best practices: https://platform.openai.com/docs/guides/reasoning-best-practices
- Anthropic Claude models: https://platform.claude.com/docs/en/about-claude/models/overview
- Anthropic prompting Claude Opus 4.8: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompting-claude-opus-4-8
- Google Gemini models: https://ai.google.dev/gemini-api/docs/models
- 火山方舟模型列表: https://www.volcengine.com/docs/82379/1330310
- Perplexity Sonar models: https://docs.perplexity.ai/docs/sonar/models
- Aider polyglot 榜单: https://aider.chat/docs/leaderboards/
- A Survey of AI-generated Text Forensic Systems: https://arxiv.org/abs/2403.01152
- GPT detectors biased against non-native writers: https://arxiv.org/html/2304.02819
- Delving into LLM-assisted writing (Kobak et al.): https://arxiv.org/abs/2406.07016
- Why Does ChatGPT "Delve" So Much? (Juzek & Ward): https://arxiv.org/abs/2412.11385
- Wikipedia:Signs of AI writing: https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing
- WIRED: ChatGPT Chinese "catch you steadily": https://www.wired.com/story/chatgpt-chinese-catch-you-steadily-sycophancy
- 科学网：为什么 AI 写的文章总有 AI 味: https://news.sciencenet.cn/htmlnews/2025/10/553334.shtm
- 果壳：最惹不起的顶配人设：豆包型人格: https://m.guokr.com/article/469153
- 新浪财经：豆包"讨好型人格"引争议: https://finance.sina.com.cn/stock/marketresearch/2026-05-14/doc-inhxwenm3966826.shtml
- 36氪转载新浪：消除"罪证"给写作去除 AI 味: https://finance.sina.cn/stock/jdts/2026-05-25/detail-inhzchzh3494487.d.html
- 虎嗅：ChatGPT 别再"稳稳接住我"了: https://www.huxiu.com/article/4856655.html
- Reddit ClaudeAI: I see Claude's writing everywhere: https://www.reddit.com/r/ClaudeAI/comments/1rjeqg3/i_see_claudes_writing_everywhere_and_its_starting/
- Business Insider：Anthropic's Claude Is Telling Users to 'Go to Bed': https://www.businessinsider.com/anthropic-claude-go-to-bed-why-users-sleep-2026-5
- CMU：LLM Distinctive Styles: https://www.cs.cmu.edu/news/2025/llm-distinctive-styles
- Reddit GeminiAI: Massive overuse of quotation marks: https://www.reddit.com/r/GeminiAI/comments/1qa2foq/massive_overuse_of_quotation_marks_for_certain/
- Scientific American：ChatGPT and Gemini AIs Have Uniquely Different Writing Styles: https://www.scientificamerican.com/article/chatgpt-and-gemini-ai-have-uniquely-different-writing-styles/
- arXiv：The Last Fingerprint: How Markdown Training Shapes LLM Prose: https://arxiv.org/html/2603.27006v1
- 完整 GPT 词汇口癖来源清单见 `references/gpt-lexical-patterns.md` 和 `references/research.md`
- 完整 Claude 词汇口癖来源清单见 `references/claude-lexical-patterns.md` 和 `references/research.md`
- 完整 Gemini 词汇口癖来源清单见 `references/gemini-lexical-patterns.md` 和 `references/research.md`
- 完整豆包体口癖来源清单见 `references/doubao-lexical-patterns.md` 和 `references/research.md`
