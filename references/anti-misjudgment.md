# 反误判清单（唯一真源）

> 跨家族通用口癖 + 常见误判。其他文件只引用本文件，不重复。

## 核心原则

判断力在**密度和组合**，不在单个词/单个句式。看到任何单一标志就判家族，都是循环论证。

## 跨家族通用：不能单独判家族的口癖

### 英文高频词（AI 通用，不是 GPT 专属）

delve / tapestry / landscape / underscore / intricate / pivotal / crucial / meticulous / robust / foster / garner / highlight / emphasize / showcase / bolster / enduring / interplay / valuable / vibrant 等。

Claude、Gemini、中文模型都可能用。判断力在密度和组合，且即使密集也不能单独判 GPT 家族。学术英语本来就用这些词，人类学者也会用。

### 句式（跨家族 AI 通用）

- `not only... but also...` / `not X, but Y`（Wikipedia 称 Negative parallelisms）
- rule of three（三个形容词或三个短语）
- didactic disclaimers（`It's important to note that...`）
- section summaries（`In summary` / `In conclusion` / `Ultimately`）
- 中文 `不是 X，而是 Y` / `不只是 X，更是 Y` / `表面上是 X，本质上是 Y`

这些 GPT/Claude/Gemini/豆包都可能用，不区分家族。

### em dash（破折号，不是 Gemini 专属）

arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率（3.53/1000 词）反而比 GPT-4.1、Claude Opus、Claude Sonnet、DeepSeek 低，在"只写自然段"约束下降到 0。em dash 是跨家族 AI 通用特征。

### "You're absolutely right"（Claude+Gemini 跨家族共享）

GitHub issue 3382 + Reddit ClaudeAI 归给 Claude，Reddit r/GeminiAI 也列入 Gemini 口癖清单。Claude 的更偏认真认错型（带感叹号、过度强调、后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔。要区分需要看上下文和其他口癖组合。

### 共情腔（跨家族情绪价值型，不区分家族）

"I can see why you'd feel that way" / "我能理解你为什么会这么想"——豆包和 ChatGPT 中文疗愈腔都有类似表达。不能凭共情腔单独判 Claude。

### "稳稳接住你"（ChatGPT 中文疗愈腔，不是豆包专属）

虎嗅明确归给 ChatGPT 中文疗愈腔，同时说"这一年几乎所有大模型都在用类似温柔、共情、滴水不漏的方式说话"。是跨家族中文 AI 通用，不是豆包专属。

### 情绪价值型口癖（跨家族通用）

"我懂你" / "你说得对" / "别太为难自己" / "我在这里陪你"——跨家族通用，其他中文情感型 AI、ChatGPT 中文疗愈腔、人类客服都可能有。

### 过度列表 / 过度粗体（跨家族通用）

各家 AI 都会用，不区分家族。

### "这是一个很好的问题"（跨家族中文 AI 通用）

所有中文模型都可能用，不区分家族。

## 家族专属判断要靠组合

### GPT 家族专属判断

不能只靠英文高频词或"不是 X 而是 Y"。要配合：
- 温情诗化散文（拟人命名 Luna/stardust + 意象堆叠 + 抒情收尾）——官方样本
- o-series 默认无 markdown——官方硬签名
- ChatGPT 中文本地化口癖"我会稳稳地接住你""砍一刀"——WIRED 报道

### Claude 家族专属判断

不能只靠"That said"或共情腔或"不是 X 而是 Y"。要靠组合：
- diplomatic padding 组合：`That said` + `worth noting` + `I want to be careful here`
- 顺从腔：`You're absolutely right!` 认真认错型（带感叹号、过度强调），区别于豆包嘴甜糊弄型
- 保姆腔：`You should get some sleep`（2026 出圈怪癖，Anthropic 自己承认是 character tic）
- 分层腔：`There are a few layers here`

### Gemini 家族专属判断

不能只靠 em dash 或过度列表或"这是一个很好的问题"。要靠组合：
- 引号癖（在不需要的词周围疯狂加引号）——最强专属签名
- 夸夸开头：`Great request!`
- 类比开头：`Think of it like this:`
- 小标题包装：`The [X] Issue` / `The [X] Effect`

### 豆包家族专属判断

不能只靠"我懂你"或"你说得对"或"稳稳接住你"。要靠组合：
- `我太懂你这种感觉了！！` + `最X` 连发（最直接/最真相/最不绕弯/最扎心）
- 哈哈道歉型：`哈哈抱歉抱歉` / `我看错啦～` / `没错没错`
- 顺从反弯：`你说得对，是我这边理解偏了，我重新给你梳理一下`

豆包顺从腔是"嘴甜糊弄型"（哈哈抱歉抱歉），区别于 Claude"认真认错型"（You're absolutely right! 带感叹号）。

## 常见误判清单

| 看到 | 错误判断 | 正确处理 |
|---|---|---|
| delve/tapestry/landscape | 判 GPT | 跨家族 AI 通用，只能判"AI 腔重" |
| "不是 X 而是 Y" | 判 GPT 或 Claude | 跨家族 AI 通用句式 |
| "可能/取决于" | 判 Claude | Claude 4.8 官方说 hedging 少；谨慎的人类也会 hedging |
| "That said" | 判 Claude | 单个跨家族通用，要靠 diplomatic padding 组合 |
| 共情腔 | 判 Claude | 跨家族情绪价值型，豆包/ChatGPT 都有 |
| em dash | 判 Gemini | arXiv 数据显示 Gemini 反而更低 |
| 过度列表/粗体 | 判 Gemini | 跨家族通用 |
| "这是一个很好的问题" | 判 Gemini | 跨家族中文 AI 通用 |
| "我懂你"/"你说得对" | 判豆包 | 跨家族通用，要靠"我太懂你+最X连发+哈哈道歉"组合 |
| "稳稳接住你" | 判豆包 | 虎嗅归给 ChatGPT 中文疗愈腔，跨家族通用 |
| "You're absolutely right" | 单独判 Claude 或 Gemini | Claude+Gemini 跨家族共享 |
| hedging 多 | 判 Claude | Claude 4.8 官方说 hedging 少；谨慎人类也 hedging |
| 结构清楚/分点 | 判 GPT | 任何模型都可能结构化 |
| 中文顺滑 | 判豆包 | Kimi/Qwen/DeepSeek 都可能 |
| 三段式 | 判 GPT | 任何模型都可能三段式 |
| 有引用/来源 | 判某模型 | 是搜索产品表面，不是底层模型 |
| 翻译腔 | 判某家族 | 翻译腔和 AI 腔学术上同源，不区分家族 |
| 豆包型人格梗 | 当字节官方特征 | 是社群归纳（果壳/搜狐），要标"社群观察/媒体归纳" |

## 翻译腔 vs AI 腔（学术同源）

翻译腔和 AI 腔在语言层面**同源**：低 perplexity、低词汇多样性、低句法复杂度。非母语英文写作被 AI 检测器误判就是这个原因（见 `references/research.md` 引用的 arxiv 2304.02819）。

中文翻译腔的可观察标志：

- 高频通用动词：进行/实现/促进/推动/开展
- 抽象名词化：...化/...性/...的进行
- 欧化长定语："基于...的...的...的"结构
- 连接词冗余：因此/所以/然而密集
- 被动句过多

审计时如果文本全是翻译腔特征，要降低"某模型家族"的置信度——可能是任何模型经中文翻译或非母语输出的结果。
