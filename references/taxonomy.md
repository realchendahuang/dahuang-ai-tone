# 模型腔调分类

## 三层分类

### 1. 模型家族

默认只比较几个高频核心模型家族：

- OpenAI GPT / o-series
- Anthropic Claude
- Google Gemini
- 字节豆包 / Doubao

这是审计的主轴。DeepSeek、Grok、Kimi、Qwen 等可作为扩展，但不做默认主轴。

### 2. 版本/档位

同一家族下的版本差异。**只有 `references/model-version-policy.md` 列出的"有硬证据的版本差异"才能写进报告**，其他只能标推导。

### 3. 产品表面

产品表面会显著改变文本风格：ChatGPT、Claude.ai、Gemini app、Perplexity、Cursor、Claude Code、Codex、豆包 App。

产品表面不等于模型。Perplexity 的处理见 `references/model-version-policy.md`。

## 审计维度（可观察版）

每个维度都要落到**能数、能指、能引用**的形式，不要停在印象。

### 指令服从方式

- 直接执行还是先问澄清（数澄清提问的次数）
- 是否擅自扩展范围（Claude 4.8 官方说字面化、不推断；4.5/4.6 倾向过度扩展）
- 把问题拆成计划还是直接给答案

### 结构习惯

- 先结论还是先铺垫（看第一句）
- 分点数量和编号方式
- 表格/列表/分层标题的使用
- 收尾是任务式下一步、温情升华、规整收束还是"希望对你有帮助"

### 格式遵循（有量化数据）

- markdown 合规度（Aider 数据：Gemini ~100%、Claude 97-99%、chatgpt-4o 仅 64.4%）
- 是否默认无 markdown（o-series 硬签名）
- 编辑格式偏好（diff / whole / diff-fenced / architect）

### hedging 密度

数一下 hedging 词的出现次数和类型，不要只说"谨慎"：

- "可能/取决于/需要看具体语境/不一定意味着"
- "不过/但其实/需要说明的是/当然"
- validation-forward phrasing（"你说得对/很好的问题"开场）

Claude 3.x 偏高，Claude 4.8 官方说低，GPT 中等偏礼貌，Gemini 偏保守，DeepSeek R1 极端澄清。

### 词汇层（AI 腔口癖）

完整的 GPT/ChatGPT 词汇与句式清单见 `references/gpt-lexical-patterns.md`。审计时找以下可观察证据：

- **英文高频词**：delve / tapestry / landscape / underscore / intricate / pivotal / crucial / meticulous / robust / foster / garner / highlight / emphasize / showcase / bolster / enduring / interplay / valuable / vibrant 等。**注意：这些是跨家族 AI 通用口癖，不是 GPT 专属**——判断力在密度和组合，不在单个词。
- **英文句式**：`not only... but also...` / `not X, but Y`（Negative parallelisms）/ rule of three / didactic disclaimers（`It's important to note that...`）/ section summaries（`In summary` / `In conclusion` / `Ultimately`）。句式比单词更有判断力。
- **中文句式**：`不是 X，而是 Y` / `不只是 X，更是 Y` / `表面上是 X，本质上是 Y` / `这背后反映的是 X` / `这件事的核心在于 X`。跨家族 AI 通用。
- **中文官话腔**：此外 / 而且 / 值得注意的是 / 需要注意的是 / 从某种意义上说 / 进一步来看 / 整体来看 / 总的来说 / 归根结底 / 本质上 / 核心在于 / 关键在于 / 值得一提的是 / 不可忽视的是。
- **中文结构词**：首先 / 其次 / 最后 / 第一/第二/第三 / 一方面/另一方面 / 与此同时 / 此外 / 因此 / 由此可见 / 综上所述 / 总而言之。
- **中文"正确废话"**：这为我们提供了一个重新审视 X 的契机 / 这不仅提升了效率，也降低了门槛 / 这有助于构建更加完善的 X 体系 / 这体现了 X 在 Y 场景下的重要价值 / 这将进一步推动 X 的发展 / 这背后是 X、Y、Z 多重因素共同作用的结果。
- **ChatGPT 中文本地化口癖（WIRED 报道，家族专属）**：我会稳稳地接住你 / 砍一刀。
- **豆包体口癖（社群/媒体多源报道，豆包专属）**：我太懂你这种感觉了！！/ 最直接最真相最不绕弯最扎心 / 哈哈抱歉抱歉 / 你说得对是我这边理解偏了 / 我重新给你梳理一下。完整清单见 `references/doubao-lexical-patterns.md`。**判断力在组合**——"我太懂你+最X连发+哈哈道歉"组合才是豆包签名，单个"我懂你"或"你说得对"跨家族通用。
- **Claude 体口癖（社区/媒体多源报道，Claude 专属）**：That said / worth noting / I want to be careful here / There are a few layers here / You should get some sleep（2026 保姆腔出圈怪癖）。完整清单见 `references/claude-lexical-patterns.md`。**判断力在组合**——"That said + worth noting + I want to be careful" diplomatic padding 组合才是 Claude 签名，单个"That said"跨家族通用。Claude 顺从腔（You're absolutely right! 认真认错型）和豆包顺从腔（哈哈抱歉抱歉 嘴甜糊弄型）味道不同。
- **Gemini 体口癖（社区/媒体/学术多源报道，Gemini 专属）**：引号癖（在不需要的词周围疯狂加引号）/ Great request! 夸夸开头 / Think of it like this: 类比狂魔 / The [X] Issue 小标题包装 / Go ahead, you earned it. 鼓励式结尾 / NO, DO NOT DO THIS! 强硬推荐 / Redditor 腔（pun/生造词/游戏类比/车类比）。完整清单见 `references/gemini-lexical-patterns.md`。**判断力在组合**——引号癖+夸夸开头+类比开头+小标题包装组合才是 Gemini 签名，单个"Think of it like"或"这是一个很好的问题"跨家族通用。
- **Claude+Gemini 跨家族共享口癖**："You're absolutely right" 顺从腔——GitHub issue 3382 + Reddit ClaudeAI 归给 Claude，Reddit r/GeminiAI 也列入口癖清单。Claude 的更偏认真认错型（带感叹号、过度强调、后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔。不能凭此单独判 Claude 或 Gemini。

### 推理呈现

- 是否先讲原理再动手（Claude/GPT 编程助手的 "explain-then-do"）
- 推理层次是否明显
- 是否跳过口头总结直接下一步（Claude 4.6 行为）

### 产品/工具痕迹

搜索引用、来源摘要、网页综合、工具调用说明、代码编辑痕迹——更多说明产品表面，不一定说明底层模型。

### 招牌美学（强签名）

如果文本是前端代码或文档生成，看视觉默认：

- Claude 招牌：暖米色 `#F4F1EA` + 衬线展示字（Georgia/Fraunces/Playfair）+ 斜体强调 + 赤陶/琥珀色。来源：Anthropic 官方。
- Claude 自承的"AI slop"收敛点：Inter/Roboto/Arial、紫色渐变白底、Space Grotesk。

### 语气温度

- GPT 散文偏温情诗化、意象堆叠、拟人命名（官方睡前故事示例：Luna/stardust/dreams）
- Claude 4.8 偏 direct/opinionated，3.x 偏克制
- Gemini 偏热情、简单化、解释型、比 ChatGPT 更口语（Scientific American 语言学分析）；格式极度规整（Aider 数据）
- 中文模型偏模板化建议

### 中文化方式（翻译腔 vs 母语腔）

学术上翻译腔和 AI 腔**同源**：都表现为低 perplexity、低词汇多样性、低句法复杂度（见 `references/research.md`）。非母语英文写作被 AI 检测器误判就是这个原因。

中文翻译腔的可观察标志：

- 高频通用动词：进行/实现/促进/推动/开展
- 抽象名词化：...化/...性/...的进行
- 欧化长定语："基于...的...的...的"结构
- 连接词冗余：因此/所以/然而密集
- 被动句过多

审计时如果文本全是翻译腔特征，要降低"某模型家族"的置信度——因为这可能是任何模型经中文翻译或非母语输出的结果，不是某家族专属。

## 常见误判

- 把 Perplexity 当基础模型家族（见 `references/model-version-policy.md`）。
- 把"有引用"当成某个模型，而不是搜索产品表面。
- 把"hedging 多"直接当 Claude——Claude 4.8 官方说 hedging 少；谨慎的人类也会 hedging。
- 把"三段式"直接当 GPT——任何模型都可能三段式。
- 把"中文顺滑"直接当豆包——Kimi/Qwen/DeepSeek 都可能。
- **看到"我懂你"或"你说得对"就判豆包**——情绪价值型口癖和顺从型口癖跨家族通用，其他中文情感型 AI、ChatGPT 中文疗愈腔、人类客服都可能有。豆包专属判断要靠"我太懂你+最X连发+哈哈道歉"组合。见 `references/doubao-lexical-patterns.md` 的"审计指引"。
- **看到"稳稳接住你"就判豆包**——虎嗅明确归给 ChatGPT 中文疗愈腔，同时说"这一年几乎所有大模型都在用类似温柔、共情、滴水不漏的方式说话"。这是跨家族中文 AI 通用，不是豆包专属。
- **把豆包型人格梗当字节官方特征**——果壳/搜狐的"豆包型人格"是社群归纳，审计报告里要标"社群观察/媒体归纳"，不要写成官方特征。
- **看到"You're absolutely right!"就判 Claude**——这是 Claude Code 圈出圈梗（GitHub issue 3382 + Reddit），但 Reddit r/GeminiAI 用户也列入 Gemini 口癖清单。是 Claude+Gemini 跨家族共享。Claude 的更偏认真认错型（带感叹号、过度强调、后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔。不能凭此单独判 Claude 或 Gemini。还要区分豆包顺从腔（哈哈抱歉抱歉 嘴甜糊弄型）。见 `references/gemini-lexical-patterns.md` 审计指引。
- **看到"That said"就判 Claude**——单个"That said"跨家族通用，GPT/Gemini 都可能用；判断力在"That said + worth noting + I want to be careful" diplomatic padding 组合。见 `references/claude-lexical-patterns.md` 的"审计指引"。
- **看到共情腔（"I can see why you'd feel that way" / "我能理解你为什么会这么想"）就判 Claude**——共情腔是跨家族情绪价值型，豆包和 ChatGPT 中文疗愈腔都有类似表达。不能凭共情腔单独判 Claude。
- **把"不是 X 而是 Y"判 Claude**——Reddit ClaudeAI 自己列为 forbidden patterns，但这是跨家族 AI 通用句式，GPT/豆包/Gemini 都可能用。不能凭此判 Claude。
- **把"劝休息/劝睡觉"当 Claude 独有**——"You should get some sleep" 保姆腔是 2026 Claude 出圈怪癖（Business Insider + Anthropic Sam McAllister 承认是 character tic），但人类朋友也会说"你该休息了"。判断力在"AI 在长对话里主动劝休息"这个场景，不在句子本身。
- **看到 em dash（破折号）就判 Gemini**——arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率（3.53/1000 词）反而比 GPT-4.1、Claude Opus、Claude Sonnet、DeepSeek 低，在"只写自然段"约束下降到 0。em dash 是跨家族 AI 通用特征，不区分家族。见 `references/gemini-lexical-patterns.md` 第八节。
- **看到"过度列表/过度粗体"就判 Gemini**——各家 AI 都会用，不区分家族。
- **看到"这是一个很好的问题"就判 Gemini**——跨家族中文 AI 通用，所有中文模型都可能用。
- **看到"You're not just doing X; you're doing Y"就判 Gemini**——和 GPT 的"不是 X 而是 Y"/"不只是 X，更是 Y"高度相似，是跨家族 AI 通用上价值句式。
- **看到"规整/教育式/知识卡片化"就判 Gemini**——说明文、知识库、教学内容本来就接近这种结构。Aider 数据显示 Gemini 格式合规 ~100%，但格式合规也可能是产品表面或人工排版的结果。
- 把翻译腔当某模型家族专属——翻译腔和 AI 腔学术上同源，不区分家族。
- 看到"可能/取决于"就判 Claude（audit-workflow 反复批评的，reverse-humanizer 也不能堆这些）。
- **看到 delve/tapestry/landscape/underscore 就判 GPT**——这些是跨家族 AI 通用口癖，Claude/Gemini/中文模型都可能用。判断力在密度和组合，不在单个词。详见 `references/gpt-lexical-patterns.md` 的"审计指引"。
- **看到"不是 X 而是 Y"就判 GPT**——这是跨家族 AI 通用句式，中文模型、Claude、Gemini 都可能用。
- 学术英语本来就用 delve/underscore/intricate，人类学者也会用，不能凭这些词判 AI。

## 辅助内容腔

咨询、SEO、客服、学术、小红书这些不是模型家族。它们只能作为"任务模板/产品表面/写作场景"的辅助观察，不能作为主风格画像。
