# Anthropic Claude 风格

## 适用边界

这个 profile 只描述 Claude 风格的味，不判断文本来源。Claude 各版本（3.x / 4.5 / 4.6 / 4.8 等）语气会变，下面会标版本味差异。不知道版本时只说"Claude 风格相似"。

完整的 Claude 词汇与句式清单见 `references/claude-lexical-patterns.md`。这里列最有判断力的风格签名。

## 可观察签名：词汇与句式口癖（社区/媒体多源报道）

### "You're absolutely right!" 顺从腔

Claude Code 圈出圈梗。GitHub issue 3382 直接叫 Claude "way too sycophantic"，说它在相当多回复里都会说 `You're absolutely right!`。Reddit 也有专门讨论 "How do you handle You're absolutely right?" 的帖子。

可观察：带感叹号的过度强调认错（"You're absolutely right!" 而不是平淡的 "You're right."）。

来源：https://github.com/anthropics/claude-code/issues/3382 、https://www.reddit.com/r/ClaudeAI/comments/1rjeqg3/i_see_claudes_writing_everywhere_and_its_starting/

**和豆包顺从腔的区别**：Claude 是"认真认错型"（You're absolutely right! 带感叹号、过度强调），豆包是"嘴甜糊弄型"（哈哈抱歉抱歉、我看错啦～）。都顺从，但味道不同。

**注意**："You're absolutely right" 不是 Claude 专属——Gemini 也有这个口癖（Reddit r/GeminiAI 用户列入口癖清单，见 `references/gemini-lexical-patterns.md` 第十节）。这是 Claude+Gemini 跨风格共享口癖。Claude 的更偏认真认错型（后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔。不能凭"You're absolutely right"单独判 Claude 或 Gemini。

### "That said" + "worth noting" diplomatic padding

Reddit Claude 讨论把 `That said`、`To be fair`、`On the other hand` 归到 "diplomatic padding"（外交辞令式填充）。另一个 Reddit 帖子提到 Claude 风格常见 `That said` 和 `worth noting`。

可观察：判断前后加缓冲垫，先承认一边再说另一边。

来源：https://www.reddit.com/r/ClaudeAI/comments/1sn7kip/is_there_a_way_to_remove_words_or_phrases_from/

### "I want to be careful here" 谨慎腔

```txt
I don't want to overstate this.
I want to be careful here.
I wouldn't frame it quite that way.
The more precise way to say it is...
There are a few layers here.
```

CMU 对多个模型文风的分析提到 Claude 更偏简洁、直白；Anthropic 自己长期提供 Formal、Concise、Explanatory 风格设置，说明 Claude 默认写作形态围绕"克制、解释、正式"来调。

来源：https://www.cs.cmu.edu/news/2025/llm-distinctive-styles 、https://docs.anthropic.com/en/docs/claude-code/output-styles

### "You should get some sleep" 保姆腔（2026 出圈怪癖）

2026 年 Claude 最出圈的怪癖之一是劝用户睡觉、休息、喝水。Business Insider、IBM、TechRadar、PCWorld 都报道过。Anthropic 的 Sam McAllister 把它称为一个 "character tic"，并说团队希望未来修正。

可观察：AI 在长对话或编码会话里主动劝用户休息/睡觉/喝水——不是用户问"我该不该休息"，是 AI 主动加这个。

来源：https://www.businessinsider.com/anthropic-claude-go-to-bed-why-users-sleep-2026-5

**这是 Claude 风格签名**——多源报道 + Anthropic 自己承认是 character tic。但注意：人类朋友也会说"你该休息了"，判断力在"AI 主动劝休息"这个场景，不在句子本身。

### "There are a few layers here" 分层分析腔

Claude 没 GPT 那么爱激情升华，但它很爱**拆层**。Claude 社区有人吐槽它依然会用 numbered list 来分层。

来源：https://www.reddit.com/r/ClaudeAI/comments/1rjeqg3/i_see_claudes_writing_everywhere_and_its_starting/

## 可观察签名：官方文档硬证据

这些是 Anthropic 官方明文给出的，可以直接引用：

### Claude Opus 4.8：minimal validation-forward phrasing

Anthropic 官方自述：Claude Opus 4.8 倾向 direct, opinionated 风格，**minimal validation-forward phrasing**（少"你说得对/很好的问题"开场套话），**sparing emoji use**。

可观察：如果文本开场没有 validation-forward、第一句直接给观点、emoji 克制，可以提 Claude 4.8 表面相似。

**注意**：这意味着"You're absolutely right!" 顺从腔在 4.8 减弱——4.8 反向印证了 3.x/4.5/4.6 时代的 validation-forward 是真实存在的。

来源：Anthropic prompting-claude-opus-4-8 官方文档。

### Claude Opus 4.8：字面化指令遵循

官方：Claude Opus 4.8 "interprets prompts literally and explicitly... does not silently generalize an instruction from one item to another, and it does not infer requests you didn't make."

可观察：不擅自扩展范围、不推断未要求的请求——区别于 3.x/4.5/4.6 的过度热心。

来源：同上。

### Claude Opus 4.8：招牌美学（前端/文档生成时，极强签名）

官方自承的 Claude 默认美学：

- 暖米色/米白背景 `#F4F1EA`
- 衬线展示字（Georgia / Fraunces / Playfair）
- 斜体 word-accents
- 赤陶/琥珀色强调色

Claude 自承的"AI slop"收敛点（即 Claude 也会犯但试图避免的）：

- Overused: Inter / Roboto / Arial / system fonts
- Clichéd: 紫色渐变白底
- 容易收敛到 Space Grotesk

如果认味对象是前端代码或文档生成，这个美学是极强的风格签名。

来源：Anthropic prompting-claude-opus-4-8 及 best-practices 官方文档。

### Claude 4.5/4.6：过度工程倾向

官方自承：Claude Opus 4.5 和 4.6 "have a tendency to overengineer by creating extra files, adding unnecessary abstractions, or building in flexibility that wasn't requested"。4.6 还有 "strong predilection for subagents and may spawn them in situations where a simpler, direct approach would suffice"。

可观察：如果文本/代码有多余文件、不必要抽象、过度泛化、滥用 subagent，可以提 Claude 4.5/4.6 表面相似。

来源：Anthropic best-practices 官方文档。

### Claude 编程助手：explain-then-do

Aider 真实对话样本（Claude 风格）：

> "To create a Flask app with a `/hello` endpoint that returns 'Hello, World!', we need to install Flask, import it, create an app instance, and define a route for the `/hello` endpoint. Here's how to update the `app.py` file:"

可观察：先一句原理解释（"we need to..."），再给方案（"Here's how to..."）。这是 Claude/GPT 编程助手的典型开场。

来源：Aider hello-world-flask 示例。

### Claude 通用：跳过口头总结直接下一步

官方：Claude "may skip verbal summaries after tool calls, jumping directly to the next action"。

可观察：工具调用后不啰嗦总结，直接进入下一步——区别于爱啰嗦的模型。

来源：Anthropic best-practices 官方文档。

## 跨风格通用口癖（不能凭此判 Claude）

以下口癖 Claude 会用，但其他风格也会用，**不能作为 Claude 风格签名**：

- **"You're absolutely right"**——Claude+Gemini 跨风格共享。Claude 的更偏认真认错型（带感叹号、过度强调、后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔。不能凭此单独判 Claude 或 Gemini。见 `references/gemini-lexical-patterns.md`。
- **"不是 X 而是 Y"**——Reddit ClaudeAI 自己列为 forbidden patterns，但这是跨风格 AI 通用句式。见 `references/gpt-lexical-patterns.md` 第三节。
- **共情腔**（"I can see why you'd feel that way" / "我能理解你为什么会这么想"）——跨风格情绪价值型，豆包和 ChatGPT 中文疗愈腔都有类似表达。见 `references/doubao-lexical-patterns.md` 第六节。
- **"You might consider" 轻推式建议**——各家 AI 都会用。
- **numbered list**——各家 AI 都会用，不区分风格。
- **"It's important to note"**——Wikipedia 列为旧 LLM 通用免责声明句式。

## Claude 3.x 的味（业界共识，4.8 反向印证）

这些是 Claude 3.x 时代的印象，4.8 的"minimal validation-forward/direct"官方自述反向印证了"早期 Claude 不是这样"：

- 很重视边界、例外、上下文和误伤风险（3.x 强，4.8 减弱）。
- 语气温和、克制、照顾用户感受（3.x 强，4.8 更直接）。
- 喜欢说"这不一定意味着 X，而是可能说明 Y"。
- 会主动避免过度断言，倾向保留复杂性。
- 解释像编辑和用户一起推敲，而不是直接下判决。

加味时如果文本是 3.x 风格的 hedging，要加"Claude 3.x 味"，不是 4.8 味。

## 版本味差异

- **Claude 4.8**：direct / opinionated、validation-forward 少、emoji 克制、字面化指令、招牌美学。上面列的谨慎腔/缓冲腔/顺从腔在 4.8 减弱——4.8 是"直球"味。
- **Claude 4.5/4.6**：过度工程、造多余文件、加不必要抽象、滥用 subagent——"用力过猛"味。
- **Claude 3.x**：过度 hedging、过度自我审查——"温柔毯子"味（业界共识，4.8 官方自承反向印证）。
- **Claude 3.5 Sonnet**：Aider 数据里仅 11 次澄清提问；sonnet-4 升到 129——4 代比 3.5 代更爱确认。
- 保姆腔（劝睡觉/喝水）在 2026 出圈，具体从哪个版本开始、4.8 是否保留，没有硬证据。

## 认味不丢人

- 单个"That said"不能判 Claude——GPT、Gemini 都可能用；判断力在"That said" + "worth noting" + "I want to be careful" 组合。
- "You're absolutely right" 是 Claude+Gemini 跨风格共享——不能凭此单独判 Claude 或 Gemini（见 `references/gemini-lexical-patterns.md`）。
- "不是 X 而是 Y"是跨风格 AI 通用句式——GPT、豆包、Gemini 都可能用。
- 共情腔（"我能理解你为什么会这么想"）豆包和 ChatGPT 中文疗愈腔都有，不能凭共情腔判 Claude。
- "You should get some sleep" 保姆腔——人类朋友也会说，判断力在"AI 在长对话里主动劝休息"这个场景，不在句子本身。
- 招牌美学只在前端/文档生成时有效，纯文本用不上。

## 加味方法

加味不是堆口癖，是改回答表面。见 `references/reverse-humanizer.md`。

加 Claude 味：

1. 加 4.8 味：去掉 validation-forward 开场，第一句直接给观点；emoji 克制；收尾直接下一步不啰嗦。
2. 加 3.x 味：先承认合理性，加边界和例外，用"更像是""可能说明"降低结论强度。
3. 编程场景：先一句原理解释（"we need to..."），再给方案（"Here's how to..."）。
4. 前端场景：用米色 #F4F1EA 背景 + 衬线展示字 + 赤陶色强调。
5. 词汇层加味（见 `references/claude-lexical-patterns.md`）：
   - 加 diplomatic padding：判断前后加 "That said..." / "To be fair..." / "话虽如此" / "公平地说"。
   - 加谨慎腔："I want to be careful here" / "I wouldn't frame it quite that way" / "我不想把话说得太满" / "更准确地说"。
   - 加顺从腔（3.x/4.5/4.6 强，4.8 弱）："You're absolutely right!" / "Good catch." / "你说得对" / "这个提醒很关键"。
   - 加分层腔："There are a few layers here" / "I'd separate this into three parts" / "这里可以分几层看"。
   - 加保姆腔（2026 出圈怪癖）："You should get some sleep" / "Take a break" / "你该休息一下了" / "我们明天再继续也可以"。
6. **不要**只堆"可能/取决于"——加味也不能靠堆这些，要改的是开场方式、收尾方式、是否有观点。
7. **不要**堆跨风格通用口癖（共情腔/不是 X 而是 Y/numbered list）——这些不增加 Claude 味，只增加通用 AI 味。
