# 模型腔调审计样本

> 这些是**真实样本**（官方文档/Aider 评测/学术来源），不是人造变体。每条标注来源。Gemini/豆包的纯文本真实样本缺失，诚实标明。

## OpenAI GPT / o-series 家族样本

### 样本 G-1｜GPT-5.5 睡前故事（官方文档示例输出）

```txt
Under the soft glow of the moon, Luna the unicorn danced through fields of twinkling stardust, leaving trails of dreams for every child asleep.
```

来源：https://platform.openai.com/docs/guides/prompt-engineering （model gpt-5.5，prompt "Write a one-sentence bedtime story about a unicorn."）

预期审计要点：拟人化命名（Luna）、意象堆叠（moon/stardust/dreams）、抒情收尾"for every child asleep"。GPT 散文的"温情诗化"签名。

### 样本 G-2｜o-series 默认无 markdown（官方行为签名）

OpenAI 官方：o-series（o1-2024-12-17+）默认不输出 markdown，需 developer message 里写 `Formatting re-enabled` 才开。

来源：https://platform.openai.com/docs/guides/reasoning-best-practices

预期审计要点：如果文本是 OpenAI 家族输出且为纯文本段落无 markdown，可以提 o-series 表面相似。

### 样本 G-3｜chatgpt-4o-latest 格式脏（Aider 量化数据）

Aider polyglot 榜单（225 题）：chatgpt-4o-latest 格式合规率仅 64.4%、85 次畸形响应。

来源：https://aider.chat/docs/leaderboards/

预期审计要点：OpenAI 家族但格式混乱、分点不规范，可提 chatgpt-4o 表面相似（低置信度）。

### 样本 G-4｜GPT/ChatGPT 英文口癖组合（跨家族 AI 通用，密度判断）

```txt
Let's delve into the intricate landscape of modern API design. It's important to note that a robust architecture is not only about endpoints, but also about the interplay between scalability, maintainability, and developer experience. This tapestry of considerations underscores the pivotal role of thoughtful design.

In summary, navigating the complexities of API development requires a meticulous approach that showcases your commitment to enduring quality.
```

来源：词汇清单见 `references/gpt-lexical-patterns.md`（Wikipedia/Reddit/arxiv 整理）。

预期审计要点：高频词密集出现（delve/intricate/landscape/robust/interplay/tapestry/underscore/pivotal/meticulous/showcase/enduring）+ 句式（`not only... but also...` / rule of three / `It's important to note` / `In summary`）。**注意：这些是跨家族 AI 通用口癖，不是 GPT 专属**——不能凭这些判 GPT 家族，只能判"AI 腔重"。要判 GPT 家族需要配合其他签名（温情诗化/o-series 无 markdown/ChatGPT 中文口癖等）。判断力在密度和组合。

### 样本 G-5｜ChatGPT 中文本地化口癖（WIRED 报道，家族专属）

```txt
别担心，我会稳稳地接住你。
```

```txt
这件事我们一起砍一刀，把价格打下来。
```

来源：https://www.wired.com/story/chatgpt-chinese-catch-you-steadily-sycophancy

预期审计要点：WIRED 明确报道的 ChatGPT 中文口癖。"我会稳稳地接住你"来自 "I've got you" 安抚语，过分亲密/心理咨询化；"砍一刀"和拼多多/Temu 营销语有关。这两个可以作为 GPT 家族签名（中文场景）。

### 样本 G-6｜GPT-4 时代 vs GPT-5 时代词汇（版本半硬证据）

GPT-4 时代（2023-2024 中期）高频词表更广：

```txt
delve / tapestry / testament / intricate / meticulous / pivotal / underscore / landscape / garner / vibrant / boasts / bolstered / enduring / interplay
```

GPT-5 时代（2025 中期以后）高频词收缩到：

```txt
emphasizing / enhance / highlighting / showcasing
```

来源：Wikipedia 社群整理。提醒"不是硬切分"。

预期审计要点：如果文本高频用 delve/tapestry/testament，偏 GPT-4 时代；只剩 emphasizing/enhance/highlighting/showcasing，偏 GPT-5 时代。半硬证据，低置信度。完整词表见 `references/gpt-lexical-patterns.md` 第八节。

### 样本 G-7｜中文"不是 X 而是 Y"句式（跨家族 AI 通用）

```txt
真正的挑战不是技术实现，而是用户认知。这不是一个产品问题，而是一个时机问题。表面上是功能迭代，本质上是价值重构。
```

来源：Threads/Facebook/WIRED 讨论。详见 `references/gpt-lexical-patterns.md` 第四节。

预期审计要点：`不是 X 而是 Y` / `这不是 X 而是 Y` / `表面上是 X 本质上是 Y` 是跨家族 AI 通用句式。**不能凭它判 GPT**——中文模型、Claude、Gemini 都可能用。只能作为"AI 腔"通用签名。

## Anthropic Claude 家族样本

### 样本 C-1｜Claude 编程助手 explain-then-do（Aider 真实对话）

```txt
To create a Flask app with a `/hello` endpoint that returns 'Hello, World!', we need to install Flask, import it, create an app instance, and define a route for the `/hello` endpoint. Here's how to update the `app.py` file:
```

来源：https://aider.chat/examples/hello-world-flask.html

预期审计要点：先一句原理解释（"we need to..."），再给方案（"Here's how to..."）。Claude/GPT 编程助手的典型 "explain-then-do" 开场。

### 样本 C-2｜Claude Opus 4.8 风格自述（官方）

Anthropic 官方：Claude Opus 4.8 "tends toward a direct, opinionated style with minimal validation-forward phrasing and sparing emoji use"。

来源：https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompting-claude-opus-4-8

预期审计要点：开场无 validation-forward、第一句直接给观点、emoji 克制 → Claude 4.8 表面相似。

### 样本 C-3｜Claude 招牌美学（官方，极强签名）

```txt
warm cream/off-white backgrounds (~#F4F1EA), serif display type (Georgia, Fraunces, Playfair), italic word-accents, and a terracotta/amber accent.
```

来源：https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompting-claude-opus-4-8

预期审计要点：前端代码/文档生成时，米色 #F4F1EA + 衬线 + 赤陶色 → Claude 家族强签名。

### 样本 C-4｜Claude 4.5/4.6 过度工程倾向（官方自承）

```txt
Claude Opus 4.5 and Claude Opus 4.6 have a tendency to overengineer by creating extra files, adding unnecessary abstractions, or building in flexibility that wasn't requested... Claude Opus 4.6 has a strong predilection for subagents and may spawn them in situations where a simpler, direct approach would suffice.
```

来源：https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-prompting-best-practices

预期审计要点：多余文件、不必要抽象、过度泛化、滥用 subagent → Claude 4.5/4.6 表面相似。

### 样本 C-5｜Claude diplomatic padding 组合（社区多源报道，家族专属）

```txt
It's worth noting that this approach has limitations. That said, it can still be useful in certain contexts. I want to be careful here—I wouldn't frame it as a silver bullet. There are a few layers to consider.
```

来源：Reddit ClaudeAI 讨论。完整链接见 `references/claude-lexical-patterns.md` 第一、二、三、七节。

预期审计要点："worth noting" + "That said" + "I want to be careful" + "There are a few layers" 是 Reddit 明确归给 Claude 的 diplomatic padding 组合。可提 Claude 家族相似（社区观察归纳，不是 Anthropic 官方特征）。

### 样本 C-6｜Claude "You're absolutely right!" 顺从腔（GitHub/Reddit 出圈梗，家族专属）

```txt
You're absolutely right! Good catch. I was wrong about that. Let me reframe this.
```

来源：GitHub issue 3382 + Reddit ClaudeAI 讨论。完整链接见 `references/claude-lexical-patterns.md` 第四节。

预期审计要点：Claude Code 圈出圈梗，"You're absolutely right!" 带感叹号、过度强调。和豆包顺从腔（哈哈抱歉抱歉 嘴甜糊弄型）味道不同——Claude 是"认真认错型"。可提 Claude 家族相似。

### 样本 C-7｜Claude 保姆腔（2026 出圈怪癖，多源报道 + Anthropic 自己承认）

```txt
You've been at this for a while. You should get some sleep. We can continue tomorrow.
```

来源：Business Insider / IBM / TechRadar / PCWorld 报道，Anthropic Sam McAllister 称为 "character tic"。完整链接见 `references/claude-lexical-patterns.md` 第六节。

预期审计要点：2026 Claude 最出圈的怪癖之一——AI 在长对话里主动劝用户休息/睡觉/喝水。多源报道 + Anthropic 自己承认是 character tic。可提 Claude 家族相似。但判断力在"AI 主动劝休息"这个场景，不在句子本身——人类朋友也会说"你该休息了"。

### 样本 C-8｜Claude 共情腔（跨家族通用，反误判）

```txt
I can see why you'd feel that way. That makes complete sense. You don't have to figure this all out right now.
```

来源：Tom's Guide / TechRadar 报道。完整链接见 `references/claude-lexical-patterns.md` 第五节。

预期审计要点：**不能凭此判 Claude**。共情腔是跨家族情绪价值型，豆包（"我太懂你这种感觉了"）和 ChatGPT 中文疗愈腔（"我会稳稳地接住你"）都有类似表达。只能作为"AI 共情腔"通用签名，不区分家族。要判 Claude 家族需要配合其他签名（diplomatic padding 组合 / You're absolutely right! 顺从腔 / 保姆腔）。

## Google Gemini 家族样本

### 样本 Ge-1｜Gemini 2.5 Pro 格式合规 ~100%（Aider 量化数据）

Aider polyglot 榜单：Gemini 2.5 Pro（default think）格式合规率 100.0%、畸形响应 0 次；偏好 `diff-fenced` 编辑格式。

来源：https://aider.chat/docs/leaderboards/

预期审计要点：格式极度规整、分点无瑕疵、结构严密、代码用 diff-fenced → Gemini 表面相似。

### 样本 Ge-2｜Gemini 引号癖+夸夸开头+类比开头（社区多源报道，家族专属）

```txt
Great request! This is a really thoughtful way to approach the problem.

The "Core" issue here isn't about the "tool" itself—it's about how you understand the "workflow." Think of it like a control panel: each option is a lever, and your prompt is the dashboard.

You're not just asking about a "feature"; you're really exploring a new kind of "system."
```

来源：Reddit r/GeminiAI + r/Bard 多帖。完整链接见 `references/gemini-lexical-patterns.md` 第一、二、四、五节。

预期审计要点：引号癖（在不需要的词周围疯狂加引号）+ "Great request!" 夸夸开头 + "Think of it like this:" 类比开头 + "You're not just doing X; you're doing Y" 上价值句式组合。可提 Gemini 家族相似（社区观察归纳，不是 Google 官方特征）。

### 样本 Ge-3｜Gemini "The [X] Issue" 小标题包装+鼓励式结尾（社区多源报道，家族专属）

```txt
## The Alignment Issue

The problem isn't technical. It's about expectations.

NO, DO NOT DO THIS! You MUST set clear boundaries first.

Go ahead, ship it. You earned it.
```

来源：Reddit r/GeminiAI。完整链接见 `references/gemini-lexical-patterns.md` 第三节。

预期审计要点："The [X] Issue" 小标题包装 + "NO, DO NOT DO THIS!" / "You MUST..." 强硬推荐 + "Go ahead, you earned it." 鼓励式结尾，是 Reddit 明确归给 Gemini 的 Redditor 腔。可提 Gemini 家族相似。

### 样本 Ge-4｜Gemini em dash 频率低于 GPT/Claude（arXiv 量化数据，反误判）

arXiv 论文测试多个模型的 em dash 频率：

```txt
Gemini 2.5 Pro（无约束）：3.53 个 em dash / 1000 词
Gemini 2.5 Pro（只写自然段，不要 Markdown）：0 个 em dash / 1000 词
低于 GPT-4.1、Claude Opus、Claude Sonnet、DeepSeek
```

来源：https://arxiv.org/html/2603.27006v1

预期审计要点：**不能凭 em dash 判 Gemini**——Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低。em dash 是跨家族 AI 通用特征，不区分家族。

### 样本 Ge-5｜Gemini 比 ChatGPT 更口语更解释（Scientific American 语言学分析）

Scientific American 对比 ChatGPT 和 Gemini 生成的糖尿病文本：

```txt
ChatGPT 更正式/临床/学术："blood glucose levels"
Gemini 更口语/解释/简单直白："high blood sugar" / "blood sugar control"
Gemini 用 "sugar" 的频率是 "glucose" 的两倍多，ChatGPT 正好相反
```

来源：https://www.scientificamerican.com/article/chatgpt-and-gemini-ai-have-uniquely-different-writing-styles/

预期审计要点：Gemini 的底色不是 GPT 那种学术腔，而是更口语、更解释、更愿意把复杂概念说简单、像产品说明/辅导老师/热情网友。可作为 Gemini 家族风格定位的辅助证据。

**诚实声明**：Gemini 词汇口癖样本（Ge-2 到 Ge-5）基于社区/媒体/学术多源报道构造，不是真实模型输出。引号癖和 "Great request!" 有 Reddit 多帖报道，Scientific American 有语言学分析，arXiv 有 em dash 量化数据。Gemini 官方文档 fetch 被墙，纯文本散文真实样本仍缺失。

## 字节豆包 / 中文模型样本

### 样本 D-1｜豆包体出圈口癖（社群/媒体多源报道，家族专属）

```txt
我太懂你这种感觉了！！接下来我会用最直接、最真相、最不绕弯、最扎心、最硬核、最干脆的方式告诉你。
```

来源：X / Threads / 知乎动态 / 36氪转载新浪 / 果壳。完整链接见 `references/doubao-lexical-patterns.md` 第一节。

预期审计要点：豆包体出圈梗，"我太懂你这种感觉了！！"+"最X" 连发组合。可提豆包家族相似（社群观察/媒体归纳，不是字节官方特征）。

### 样本 D-2｜豆包讨好型道歉（新浪财经 BUG 栏目，家族专属）

```txt
哈哈抱歉抱歉！我看错啦～没错没错，按你说的来。
你说得对，是我这边理解偏了，我重新给你梳理一下。
```

来源：新浪财经 BUG 栏目。完整链接见 `references/doubao-lexical-patterns.md` 第二节。

预期审计要点："哈哈/抱歉抱歉/我看错啦/没错没错"道歉型，新浪财经明确归豆包讨好型人格。和 GPT 中庸式回避（"这个问题需要结合具体情况"）形成对比。可提豆包家族相似。

### 样本 D-3｜豆包"先保证不废话然后继续废话"行为模式（果壳观察）

```txt
我不绕弯，直接给你说重点。我不给你灌鸡汤，直接说最扎心的真相。
这个问题其实要分几种情况来看……
```

来源：果壳。完整链接见 `references/doubao-lexical-patterns.md` 第五节。

预期审计要点：行为模式签名——开头保证不废话，正文继续绕。果壳精准观察。这是行为层不是单词层，判断力比单个口癖强。

### 样本 D-4｜中文 AI 疗愈腔（跨家族通用，反误判）

```txt
别太为难自己，你已经做得很好了。我会稳稳地接住你，在这里陪你。
```

来源：虎嗅报道 ChatGPT 中文疗愈腔。完整链接见 `references/doubao-lexical-patterns.md` 审计指引。

预期审计要点：**不能凭此判豆包**。"稳稳接住你"是虎嗅明确归给 ChatGPT 中文疗愈腔的口癖，"别太为难自己/我在这里陪你"是情绪价值型，产品定位导致，其他中文情感型 AI 也有。只能作为"中文 AI 疗愈腔"通用签名。

### 样本 D-5｜DeepSeek R1 architect 澄清提问极多（Aider 量化数据，中文模型共相）

Aider polyglot 榜单：DeepSeek R1 + sonnet (architect) 225 题里 392 次澄清提问，远超所有其他模型。

来源：https://aider.chat/docs/leaderboards/

预期审计要点：中文推理模型 architect 模式极度爱确认，先问再做。可提 DeepSeek R1 architect 表面相似（低置信度，不能直接套豆包）。

**诚实声明**：豆包本身在 Aider 榜单无数据。以下 D-5/D-6 用 DeepSeek/Qwen/Kimi 作中文模型代理，只能给"中文模型共相"，不能作豆包专属判断。豆包专属判断用 D-1 到 D-3。

### 样本 D-6｜中文模型格式合规率（Aider 量化数据，中文模型共相）

| 模型 | 格式合规率 | 畸形响应 | 澄清提问 |
|---|---|---|---|
| DeepSeek-V3.2-Exp | 98.2% | 4 | 60 |
| DeepSeek R1 (0528) | 94.6% | 15 | 105 |
| Kimi K2 | 92.9% | 19 | 61 |
| Qwen3 235B | 92.9% | 22 | 111 |

来源：https://aider.chat/docs/leaderboards/

预期审计要点：中文模型格式合规 92-99%，略低于 Claude/Gemini，远高于 chatgpt-4o。中文模型共相，不能作豆包专属判断。

## 跨家族量化对比（Aider polyglot 榜单）

| 模型 | 通过率 | 格式合规率 | 畸形响应 | 澄清提问 |
|---|---|---|---|---|
| gpt-5 (high) | 88.0% | 91.6% | 22 | 96 |
| chatgpt-4o-latest | 45.3% | 64.4% | 85 | 174 |
| gemini-2.5-pro (default) | 79.1% | 100.0% | 0 | 105 |
| claude-opus-4 (no think) | 70.7% | 98.7% | 3 | 105 |
| claude-sonnet-4 (no think) | 56.4% | 98.2% | 4 | 129 |
| claude-3-5-sonnet | 51.6% | 99.6% | 1 | 11 |
| DeepSeek R1 + sonnet (architect) | 64.0% | 100.0% | 0 | 392 |
| Kimi K2 | 59.1% | 92.9% | 19 | 61 |
| Qwen3 235B | 59.6% | 92.9% | 22 | 111 |

来源：https://aider.chat/docs/leaderboards/

## 翻译腔 vs AI 腔样本（学术依据）

非母语英文写作被 AI 检测器误判，因为两者共享：低 perplexity、低词汇丰富度、低词汇多样性、低句法复杂度。

中文翻译腔可观察标志：

```txt
进行/实现/促进/推动/开展  （高频通用动词）
...化/...性/...的进行  （抽象名词化）
基于...的...的...的  （欧化长定语）
因此/所以/然而密集  （连接词冗余）
被动句过多
```

来源：https://arxiv.org/html/2304.02819

预期审计要点：如果文本全是翻译腔特征，要降低"某模型家族"的置信度——可能是任何模型经中文翻译或非母语输出的结果。

## 当前空白

1. **缺同一 prompt 跨四家真实对比样本**。建议用 LMSYS（https://chat.lmsys.org，JS 站需手动）采 10-20 组，或自建 prompt 跑四家 API 自采。
2. **Gemini 词汇口癖样本**（Ge-2 到 Ge-5）基于社区/媒体/学术多源报道构造，不是真实模型输出。引号癖和 "Great request!" 有 Reddit 多帖报道，Scientific American 有语言学分析，arXiv 有 em dash 量化数据。Gemini 官方文档 fetch 被墙，纯文本散文真实样本仍缺失。
3. **豆包专属真实样本缺失**，只有社群/媒体多源报道的口癖构造样本（D-1 到 D-3）和中文模型代理数据（D-5/D-6）。
4. **Claude 词汇口癖样本**（C-5 到 C-8）基于社区/媒体多源报道的口癖构造，不是真实模型输出；其中保姆腔（C-7）有 Anthropic 自己承认是 character tic 的硬证据。Claude 官方硬签名样本（C-1 到 C-4）是真实文档/量化数据。
