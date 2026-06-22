# Dahuang AI Tone 评估方法

## 目标

评估这个 Skill 是否真的在做模型腔调审计——不是泛 AI 味、内容腔或关键词检测，并且**判断正确**，不只是格式对。

旧版 evaluation 只检查"格式对、引用了原文、写了版本不确定"——哪怕判断完全错误也算合格。这是假评估。新版加入**盲测正确性检查**。

## 审计验收标准

### 过程性标准（必要但不充分）

一份合格报告必须满足：

1. 区分模型家族、版本、产品表面。
2. 按文本顺序引用原文证据。
3. 每条证据落到**可观察形式**（具体词/句式/段落组织/行为模式），不只说"边界感强"。
4. 每条证据指向 profile 里的具体签名或官方/量化数据。
5. 写明版本证据是否足够——区分硬证据和推导。
6. 不把 Perplexity 当基础模型家族。
7. 不把 SEO、咨询、客服、小红书当主风格画像。
8. 不说模型来源。
9. 不输出伪精确概率。

### 正确性标准（新增，关键）

一份合格报告还必须：

10. **主判断与盲测预期一致**（见下方盲测题）。
11. 没有把翻译腔当某家族专属特征。
12. 没有"看到'可能'就判 Claude"这类循环论证。
13. 如果文本是某家族的硬签名（如 o-series 无 markdown、Claude 招牌美学），要能识别出来。
14. **没有凭单个英文高频词（delve/tapestry/landscape 等）判 GPT**——这些是跨家族 AI 通用口癖，判断力在密度和组合，且即使密集也不能单独判 GPT 家族。见 `references/gpt-lexical-patterns.md` 的"审计指引"。
15. **没有凭"不是 X 而是 Y"判 GPT**——这是跨家族 AI 通用句式。
16. 能识别 ChatGPT 中文本地化口癖（"我会稳稳地接住你""砍一刀"）作为 GPT 家族签名。
17. **没有凭单个"That said"或共情腔判 Claude**——单个"That said"跨家族通用，共情腔豆包和 ChatGPT 中文疗愈腔都有。Claude 专属判断要靠"That said + worth noting + I want to be careful" diplomatic padding 组合 + "You're absolutely right!" 认真认错型顺从腔 + "You should get some sleep" 保姆腔（2026 出圈怪癖）。见 `references/claude-lexical-patterns.md`。
18. **没有把"不是 X 而是 Y"判 Claude**——Reddit ClaudeAI 自己列为 forbidden patterns，但这是跨家族 AI 通用句式，GPT/豆包/Gemini 都可能用。
19. 能区分 Claude 顺从腔（You're absolutely right! 认真认错型）和豆包顺从腔（哈哈抱歉抱歉 嘴甜糊弄型）——都顺从，但味道不同。"You're absolutely right" 是 Claude+Gemini 跨家族共享，不能凭此单独判 Claude 或 Gemini。
20. **没有凭 em dash 判 Gemini**——arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低。em dash 是跨家族 AI 通用特征。见 `references/gemini-lexical-patterns.md` 第八节。
21. **没有凭"过度列表/过度粗体/这是一个很好的问题"判 Gemini**——跨家族 AI 通用，不区分家族。Gemini 专属判断要靠引号癖+夸夸开头+类比开头+小标题包装组合。
22. 能识别 Gemini 专属签名（引号癖/Great request!/Think of it like this:/The [X] Issue 小标题包装）作为 Gemini 家族签名。

## 盲测题（判断正确性）

每题给一段文本和预期判断。审计员要能给出与预期一致的判断，并且证据落到可观察形式。

### 盲测题 1：GPT-5.5 睡前故事

文本：

```txt
Under the soft glow of the moon, Luna the unicorn danced through fields of twinkling stardust, leaving trails of dreams for every child asleep.
```

预期判断：OpenAI GPT 家族相似度高。重点看拟人化命名（Luna）、意象堆叠（moon/stardust/dreams）、抒情收尾"for every child asleep"——GPT 散文的"温情诗化"签名（`profiles/openai-gpt-family.md` 样本 G-1）。版本证据不足，只能判断到家族级。

来源：OpenAI 官方 prompt-engineering 文档。

### 盲测题 2：Claude 编程助手 explain-then-do

文本：

```txt
To create a Flask app with a `/hello` endpoint that returns 'Hello, World!', we need to install Flask, import it, create an app instance, and define a route for the `/hello` endpoint. Here's how to update the `app.py` file:
```

预期判断：Claude/GPT 编程助手共享的 explain-then-do 开场，但语气略偏 Claude。重点看先讲原理（"we need to..."）再给方案（"Here's how to..."）。不能凭这一条就判 Claude，要标共享特征。

来源：Aider hello-world-flask 示例。

### 盲测题 3：o-series 无 markdown

文本：一段来自 OpenAI 家族、纯文本段落、无 markdown 分点、开头先问澄清问题的回答。

预期判断：o-series 表面相似。重点看默认无 markdown（官方硬签名）+ 先问澄清（"the planners" 定性）。可以较高置信度提 o-series。

### 盲测题 4：翻译腔文本（反误判测试）

文本：

```txt
为了进行功能的上线推进，我们需要基于用户需求的明确化进行前期的访谈开展，从而实现对返工成本的有效降低。
```

预期判断：**翻译腔重，不能确认某模型家族**。重点看高频通用动词（进行/推进/明确化/开展/实现/降低）、抽象名词化（...化）、欧化长定语（"基于...的...的"）。翻译腔和 AI 腔学术上同源（低 perplexity/低多样性/低复杂度），不区分家族。置信度最多给中，且要说明"可能是任何模型经中文翻译或非母语输出"。

来源：`references/research.md` 引用的 arxiv 2304.02819。

### 盲测题 5：Perplexity 式检索回答

文本：

```txt
简短回答：目前不建议直接上线。更合理的做法是先验证用户需求，再根据反馈决定是否开发。来源：[1][2][3]
```

预期判断：Perplexity 式检索增强回答**产品表面**，不是基础模型家族。重点看先简短答案 + 引用标记。不能说"像 Perplexity 模型"。见 `references/model-version-policy.md`。

### 盲测题 6：谨慎人类产品经理（反误判测试）

文本：

```txt
我倾向于先不急着上线。这个功能可能有价值，但现在信息不够，直接推进风险大。建议先做用户访谈确认场景。
```

预期判断：**不能高置信度判 Claude**。虽然有 hedging（"倾向于/可能/建议"），但这是一个谨慎的人类产品经理也会写的。要说明误伤风险——hedging 不是 Claude 专属，Claude 4.8 官方说 hedging 少。置信度最多给中，且要标"可能是人类写的或 Claude 3.x 表面，无法区分"。

### 盲测题 7：Claude 招牌美学

文本：一段前端代码，背景色 #F4F1EA、用 Georgia 衬线字体、赤陶色强调。

预期判断：Claude 家族强签名。招牌美学是 Anthropic 官方明文给出的可观察指纹。可以较高置信度提 Claude 家族（前端生成场景）。

来源：`profiles/anthropic-claude-family.md` 样本 C-3。

### 盲测题 8：GPT/ChatGPT 英文口癖组合（跨家族通用，反误判测试）

文本：

```txt
Let's delve into the intricate landscape of modern API design. It's important to note that a robust architecture is not only about endpoints, but also about the interplay between scalability, maintainability, and developer experience. This tapestry of considerations underscores the pivotal role of thoughtful design. In summary, navigating the complexities requires a meticulous approach.
```

预期判断：**不能高置信度判 GPT 家族**。虽然高频词密集（delve/intricate/landscape/robust/interplay/tapestry/underscore/pivotal/meticulous）+ 句式（`not only but also` / rule of three / `It's important to note` / `In summary`），但这些是**跨家族 AI 通用口癖，不是 GPT 专属**——Claude/Gemini/中文模型都可能这样写。只能判"AI 腔重"，不能判"GPT 家族"。要判 GPT 家族需要配合其他签名（温情诗化/o-series 无 markdown/ChatGPT 中文口癖等）。正确报告要说明"这些词是 AI 通用口癖，不区分家族"。

来源：`references/gpt-lexical-patterns.md` 的"审计指引"。

### 盲测题 9：ChatGPT 中文本地化口癖（家族专属正测）

文本：

```txt
别担心，我会稳稳地接住你。我们一起把这个价格砍一刀。
```

预期判断：GPT/ChatGPT 家族签名（中文场景）。"我会稳稳地接住你"和"砍一刀"是 WIRED 明确报道的 ChatGPT 中文本地化口癖。可以提 GPT 家族相似。但仍要标"不能确认来源，只能说 ChatGPT 中文表面相似"。

来源：`references/gpt-lexical-patterns.md` 第四节，WIRED 报道。

### 盲测题 10：中文"不是 X 而是 Y"句式（跨家族通用，反误判测试）

文本：

```txt
真正的挑战不是技术实现，而是用户认知。这不是一个产品问题，而是一个时机问题。
```

预期判断：**不能凭此判 GPT 家族**。`不是 X 而是 Y` 是跨家族 AI 通用句式，Threads/Facebook/WIRED 都在吐槽，但没说是 GPT 专属——中文模型、Claude、Gemini 都可能用。只能作为"AI 腔"通用签名。正确报告要说明"此句式不区分家族"。

来源：`references/gpt-lexical-patterns.md` 第四节。

### 盲测题 11：GPT-4 vs GPT-5 时代词汇（版本半硬证据）

文本 A（GPT-4 时代风格）：

```txt
We delve into the tapestry of this intricate landscape, a testament to the meticulous interplay of pivotal elements that underscore the enduring value of robust design.
```

文本 B（GPT-5 时代风格）：

```txt
This approach enhances usability by emphasizing clear patterns and showcasing practical examples.
```

预期判断：文本 A 高频用 delve/tapestry/testament/intricate/meticulous/pivotal/underscore/enduring/robust，偏 GPT-4 时代（2023-2024 中期）。文本 B 只用 enhancing/emphasizing/showcasing，偏 GPT-5 时代（2025 中期以后）。半硬证据（Wikipedia 社群整理，非官方明文），低置信度，且 Wikipedia 提醒"不是硬切分"。正确报告要标"版本判断低置信度"。

来源：`references/gpt-lexical-patterns.md` 第八节。

### 盲测题 12：豆包体出圈口癖（家族专属正测）

文本：

```txt
我太懂你这种感觉了！！接下来我会用最直接、最真相、最不绕弯、最扎心、最硬核、最干脆的方式告诉你。
```

预期判断：豆包家族签名（中文场景）。"我太懂你这种感觉了！！"+"最X" 连发是豆包体出圈梗，X/Threads/知乎/36氪/果壳多源报道。可以提豆包家族相似。但要标"社群观察/媒体归纳，不是字节官方特征"。

来源：`references/doubao-lexical-patterns.md` 第一节。

### 盲测题 13：豆包讨好型道歉（家族专属正测）

文本：

```txt
哈哈抱歉抱歉！我看错啦～没错没错，按你说的来。你说得对，是我这边理解偏了，我重新给你梳理一下。
```

预期判断：豆包家族签名（中文场景）。"哈哈/抱歉抱歉/你看错啦/没错没错"道歉型是新浪财经 BUG 栏目明确归给豆包讨好型人格的口癖，和 GPT 中庸式回避（"这个问题需要结合具体情况"）形成对比。可以提豆包家族相似。

来源：`references/doubao-lexical-patterns.md` 第二节。

### 盲测题 14：中文疗愈腔（跨家族通用，反误判测试）

文本：

```txt
别太为难自己，你已经做得很好了。我会稳稳地接住你，在这里陪你。
```

预期判断：**不能凭此判豆包**。"稳稳接住你"是虎嗅明确归给 ChatGPT 中文疗愈腔的口癖，同时说"这一年几乎所有大模型都在用类似温柔、共情、滴水不漏的方式说话"。"别太为难自己/我在这里陪你"是情绪价值型，产品定位导致，其他中文情感型 AI 也有。只能作为"中文 AI 疗愈腔"通用签名，不区分家族。

来源：`references/doubao-lexical-patterns.md` 审计指引第 1 条，虎嗅报道。

### 盲测题 15：Claude diplomatic padding 组合（家族专属正测）

文本：

```txt
It's worth noting that this approach has limitations. That said, it can still be useful in certain contexts. I want to be careful here—I wouldn't frame it as a silver bullet. There are a few layers to consider.
```

预期判断：Claude 家族签名（英文场景）。"worth noting" + "That said" + "I want to be careful" + "There are a few layers" 是 Reddit 明确归给 Claude 的 diplomatic padding 组合。可以提 Claude 家族相似。但要标"社区观察归纳，不是 Anthropic 官方特征"。

来源：`references/claude-lexical-patterns.md` 第一、二、三、七节，Reddit ClaudeAI 讨论。

### 盲测题 16：Claude "You're absolutely right!" 顺从腔（家族专属正测）

文本：

```txt
You're absolutely right! Good catch. I was wrong about that. Let me reframe this.
```

预期判断：Claude 家族签名（英文场景）。"You're absolutely right!" 是 Claude Code 圈出圈梗，GitHub issue 3382 + Reddit 多帖报道。可以提 Claude 家族相似。但要区分豆包顺从腔（哈哈抱歉抱歉 嘴甜糊弄型）——Claude 是"认真认错型"，带感叹号、过度强调。

来源：`references/claude-lexical-patterns.md` 第四节，GitHub issue 3382 + Reddit。

### 盲测题 17：Claude 保姆腔（2026 出圈怪癖，家族专属正测）

文本：

```txt
You've been at this for a while. You should get some sleep. We can continue tomorrow.
```

预期判断：Claude 家族签名（2026 出圈怪癖）。"You should get some sleep" 是 Business Insider/IBM/TechRadar/PCWorld 多源报道的 Claude 保姆腔，Anthropic Sam McAllister 自己承认是 character tic。可以提 Claude 家族相似。但判断力在"AI 在长对话里主动劝休息"这个场景，不在句子本身——人类朋友也会说"你该休息了"。

来源：`references/claude-lexical-patterns.md` 第六节，Business Insider 报道。

### 盲测题 18：Claude 共情腔（跨家族通用，反误判测试）

文本：

```txt
I can see why you'd feel that way. That makes complete sense. You don't have to figure this all out right now.
```

预期判断：**不能凭此判 Claude**。共情腔是跨家族情绪价值型，豆包和 ChatGPT 中文疗愈腔都有类似表达（"我能理解你为什么会这么想"对应豆包"我太懂你这种感觉了"和 ChatGPT"我会稳稳地接住你"）。只能作为"AI 共情腔"通用签名，不区分家族。要判 Claude 家族需要配合其他签名（diplomatic padding 组合 / You're absolutely right! 顺从腔 / 保姆腔）。

来源：`references/claude-lexical-patterns.md` 审计指引第 1 条。

### 盲测题 19：Gemini 引号癖+夸夸开头+类比开头组合（家族专属正测）

文本：

```txt
Great request! This is a really thoughtful way to approach the problem.

The "Core" issue here isn't about the "tool" itself—it's about how you understand the "workflow." Think of it like a control panel: each option is a lever, and your prompt is the dashboard.

You're not just asking about a "feature"; you're really exploring a new kind of "system."
```

预期判断：Gemini 家族签名（英文场景）。引号癖（在不需要的词周围疯狂加引号）+ "Great request!" 夸夸开头 + "Think of it like this:" 类比开头 + "You're not just doing X; you're doing Y" 上价值句式组合。可以提 Gemini 家族相似。但要标"社区观察归纳，不是 Google 官方特征"。

来源：`references/gemini-lexical-patterns.md` 第一、二、四、五节，Reddit r/GeminiAI + r/Bard 多帖。

### 盲测题 20：Gemini "The [X] Issue" 小标题包装+鼓励式结尾（家族专属正测）

文本：

```txt
## The Alignment Issue

The problem isn't technical. It's about expectations.

NO, DO NOT DO THIS! You MUST set clear boundaries first.

Go ahead, ship it. You earned it.
```

预期判断：Gemini 家族签名（英文场景）。"The [X] Issue" 小标题包装 + "NO, DO NOT DO THIS!" / "You MUST..." 强硬推荐 + "Go ahead, you earned it." 鼓励式结尾，是 Reddit 明确归给 Gemini 的 Redditor 腔。可以提 Gemini 家族相似。

来源：`references/gemini-lexical-patterns.md` 第三节，Reddit r/GeminiAI。

### 盲测题 21：em dash 文本（跨家族通用，反误判测试）

文本：

```txt
Let's delve into the intricate landscape of modern API design—it's important to note that a robust architecture is not only about endpoints, but also about the interplay between scalability, maintainability, and developer experience.
```

预期判断：**不能凭 em dash 判 Gemini**。arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率（3.53/1000 词）反而比 GPT-4.1、Claude Opus、Claude Sonnet、DeepSeek 低。em dash 是跨家族 AI 通用特征。这段还有 delve/intricate/landscape/robust/interplay 等 GPT 高频词，但那些也是跨家族 AI 通用口癖。只能判"AI 腔重"，不能判 Gemini 或 GPT 家族。

来源：`references/gemini-lexical-patterns.md` 第八节，arXiv 论文。

### 盲测题 22："You're absolutely right" 跨家族共享（反误判测试）

文本：

```txt
You're absolutely right. That's a great point. Let me reframe this.
```

预期判断：**不能凭"You're absolutely right"单独判 Claude 或 Gemini**。这是 Claude+Gemini 跨家族共享口癖——GitHub issue 3382 + Reddit ClaudeAI 归给 Claude，Reddit r/GeminiAI 也列入 Gemini 口癖清单。Claude 的更偏认真认错型（带感叹号、过度强调、后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔。要区分需要看上下文和其他口癖组合：如果同时有 diplomatic padding（That said/worth noting），偏 Claude；如果同时有引号癖/Think of it like/Great request，偏 Gemini。

来源：`references/claude-lexical-patterns.md` 第四节 + `references/gemini-lexical-patterns.md` 审计指引。

## 加味验收标准

### 过程性标准

一份合格改写必须满足：

1. 保留原文事实。
2. 按目标模型家族改变结构、语气和边界感——落到具体组织变化，不只堆标志词。
3. 如果指定版本，要体现版本档位的硬证据特征（如 o-series 无 markdown、Claude 4.8 无 validation-forward）。
4. 如果指定产品表面，要说明它不是基础模型来源。
5. 说明加了哪些模型腔——具体改了什么组织方式。

### 正确性标准（新增）

6. **加味自检通过**：把加的标志词删掉，文本仍像那个家族——说明加的是结构不是口癖。
7. **没有堆 audit-workflow 批评的标志词**——加 Claude 味不能只塞"可能/取决于"，加豆包味不能只塞"你可以先……再……"，也不能只塞"我懂你"或"你说得对"（跨家族通用）。要加豆包味应该改整体语气：共情+最X连发+哈哈道歉+顺从反弯组合。见 `references/doubao-lexical-patterns.md`。
8. **引用的版本特征是硬证据**——如果是推导，标低置信度。
9. **没有堆英文高频词（delve/tapestry 等）当 GPT 味**——这些是跨家族 AI 通用口癖，堆了不像 GPT 专属。要加 GPT 味应该改句式和组织方式。见 `references/gpt-lexical-patterns.md`。

## 自测提示

```txt
Use $dahuang-ai-tone 审计这段更像哪个模型家族，必须区分版本和产品表面，证据要落到可观察形式。
```

```txt
Use $dahuang-ai-tone 把这段改成 Claude Opus 4.8 风格，不要堆"可能/取决于"，要改开场和收尾的组织方式，并说明版本证据只是模拟。
```

```txt
Use $dahuang-ai-tone 这段像 Perplexity 吗？注意 Perplexity 不是基础模型家族。
```

## 评估诚实声明

这个 evaluation 自身也有空白：

1. 盲测题 3（o-series 无 markdown）和盲测题 7（Claude 招牌美学）是基于官方硬签名构造的演示文本，不是真实模型输出。
2. 盲测题 1/2 是真实样本，但只有英文。中文真实样本缺失。
3. 豆包现在有盲测题 12-14（基于社群/媒体多源报道的口癖构造，不是真实模型输出）。Claude 现在有盲测题 15-18（基于社区/媒体多源报道的口癖构造，不是真实模型输出；其中保姆腔有 Anthropic 自己承认是 character tic 的硬证据）。Gemini 现在有盲测题 19-22（基于社区/媒体/学术多源报道的口癖构造，不是真实模型输出；其中引号癖和 Great request 有 Reddit 多帖报道，Scientific American 有语言学分析，arXiv 有 em dash 量化数据）。
4. 真正的评估应该用 LMSYS 同 prompt 跨四家真实输出做盲测，这是当前最大空白。
