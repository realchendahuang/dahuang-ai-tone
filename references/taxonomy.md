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

完整的各家族词汇与句式清单见 `references/*-lexical-patterns.md`。审计时找以下可观察证据：

- **英文高频词**：delve / tapestry / landscape / underscore / intricate / pivotal / crucial / meticulous / robust / foster / garner / highlight / emphasize / showcase 等。完整清单见 `references/gpt-lexical-patterns.md`。
- **英文句式**：`not only... but also...` / `not X, but Y` / rule of three / didactic disclaimers / section summaries。句式比单词更有判断力。
- **中文句式**：`不是 X，而是 Y` / `不只是 X，更是 Y` / `表面上是 X，本质上是 Y` / `这背后反映的是 X` / `这件事的核心在于 X`。
- **中文官话腔/结构词/正确废话**：此外/值得注意的是/首先…其次…最后…/这为我们提供了一个重新审视 X 的契机。完整清单见 `references/gpt-lexical-patterns.md`。
- **ChatGPT 中文本地化口癖（WIRED 报道，家族专属）**：我会稳稳地接住你 / 砍一刀。
- **豆包体口癖（豆包专属）**：我太懂你这种感觉了！！/ 最X 连发 / 哈哈抱歉抱歉。完整清单见 `references/doubao-lexical-patterns.md`。
- **Claude 体口癖（Claude 专属）**：That said / worth noting / I want to be careful here / There are a few layers here / You should get some sleep。完整清单见 `references/claude-lexical-patterns.md`。
- **Gemini 体口癖（Gemini 专属）**：引号癖 / Great request! / Think of it like this: / The [X] Issue 小标题包装 / Redditor 腔。完整清单见 `references/gemini-lexical-patterns.md`。

**关键**：以上口癖哪些是跨家族通用、哪些是家族专属、判断力在组合还是单个词——完整反误判规则见 `references/anti-misjudgment.md`。不要凭单个词或单个句式判家族。

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

翻译腔和 AI 腔学术上**同源**（低 perplexity/低多样性/低复杂度），不区分家族。审计时如果文本翻译腔重，要降低家族置信度。完整可观察标志和误判处理见 `references/anti-misjudgment.md` 的"翻译腔 vs AI 腔"。

## 常见误判

完整反误判清单见 `references/anti-misjudgment.md`（唯一真源）。这里只列审计时最容易犯的几条：

- 把 Perplexity 当基础模型家族（见 `references/model-version-policy.md`）。
- 把"有引用"当成某个模型，而不是搜索产品表面。
- 凭单个词/单个句式判家族——判断力在密度和组合。
- 把翻译腔当某模型家族专属——翻译腔和 AI 腔学术上同源，不区分家族。

## 辅助内容腔

咨询、SEO、客服、学术、小红书这些不是模型家族。它们只能作为"任务模板/产品表面/写作场景"的辅助观察，不能作为主风格画像。
