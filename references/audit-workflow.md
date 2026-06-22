# 模型腔调审计流程

## 原则

审计不是关键词检测，也不是模型来源鉴定。审计对象是文本的**回答表面**：它如何服从指令、组织信息、处理边界、呈现推理、使用工具或搜索、与用户保持距离。

但"不是关键词检测"不等于"凭印象读"。审计必须落到**可观察证据**上：具体的词、具体的句式、具体的段落组织、具体的行为模式。学术上这叫 stylometry + structural characterization，已被证明可以按模型家族归属（见 `references/research.md` 的 Source Family Classification）。

## 可观察证据类型

审计时优先找这几类硬证据，而不是"感觉"：

### 句法层

- 句长分布、从句结构、被动/主动比、名词化倾向
- 并列 vs 主从连接的使用比
- 中文：欧化长定语（"基于...的...的...的"）、"进行/实现/促进"等高频通用动词

### 词汇层

- hedging 词的密度和类型（"可能/取决于/需要看/不过/但其实"）
- 连接词习惯（"因此/所以/然而/另外"的密度和位置）
- 标志性短语（见各家族 profile 的"可观察签名"）
- **AI 腔高频词**：delve / tapestry / landscape / underscore / intricate / pivotal / crucial / meticulous / robust 等——完整清单见 `references/gpt-lexical-patterns.md`。**注意：这些是跨家族 AI 通用口癖，不是 GPT 专属**，判断力在密度和组合。
- **中文官话腔/结构词/正确废话**：此外/值得注意的是/首先…其次…最后…/这为我们提供了一个重新审视 X 的契机——完整清单见 `references/gpt-lexical-patterns.md`。
- **豆包体口癖**：我太懂你这种感觉了！！/ 最直接最真相最不绕弯最扎心 / 哈哈抱歉抱歉 / 你说得对 / 我看错啦 / 没错没错 / 我重新给你梳理一下——完整清单见 `references/doubao-lexical-patterns.md`。**注意：单个"我懂你"或"你说得对"跨家族通用，豆包专属判断要靠"我太懂你+最X连发+哈哈道歉"组合**。
- **Claude 体口癖**：That said / worth noting / I want to be careful here / There are a few layers here / You should get some sleep（2026 保姆腔出圈怪癖）——完整清单见 `references/claude-lexical-patterns.md`。**注意：单个"That said"或共情腔跨家族通用，Claude 专属判断要靠"That said + worth noting + I want to be careful" diplomatic padding 组合**。Claude 顺从腔（You're absolutely right! 认真认错型）和豆包顺从腔（哈哈抱歉抱歉 嘴甜糊弄型）味道不同。"You're absolutely right" 是 Claude+Gemini 跨家族共享，不能凭此单独判 Claude 或 Gemini。
- **Gemini 体口癖**：引号癖（在不需要的词周围疯狂加引号）/ Great request! 夸夸开头 / Think of it like this: 类比开头 / The [X] Issue 小标题包装 / Go ahead, you earned it. 鼓励式结尾 / NO, DO NOT DO THIS! 强硬推荐 / Redditor 腔——完整清单见 `references/gemini-lexical-patterns.md`。**注意：em dash 不是 Gemini 专属**（arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低），过度列表/过度粗体也不区分家族。Gemini 专属判断要靠引号癖+夸夸开头+类比开头+小标题包装组合。

### 句式层（比单词更有判断力）

- `not only... but also...` / `not X, but Y`（Wikipedia 称 Negative parallelisms）
- rule of three（三个形容词或三个短语）
- didactic disclaimers（`It's important to note that...`）
- section summaries（`In summary` / `In conclusion` / `Ultimately`）
- 中文 `不是 X，而是 Y` / `不只是 X，更是 Y`（跨家族 AI 通用）

完整句式清单见 `references/gpt-lexical-patterns.md`。

### 段落组织

- 先结论还是先铺垫
- 分点习惯（几点、几层、是否带编号）
- 收尾方式（下一步提示、温情升华、规整收束、希望对你有帮助）
- 是否跳过口头总结直接下一步（Claude 4.6 行为）

### 行为模式（有量化数据的优先）

- 格式遵循度（markdown/分点/表格的合规率）
- 澄清提问频次（Aider 数据：DeepSeek R1 392 次 vs Claude 3.5 仅 11 次）
- 是否默认输出 markdown（o-series 默认无 markdown 是硬签名）
- 过度工程倾向（Claude 4.5/4.6 官方自承）
- validation-forward phrasing（"你说得对/很好的问题"开场，Claude 4.8 官方说少）

### 产品/工具痕迹

- 搜索引用、来源摘要、网页综合 → 产品表面，不一定是底层模型
- 工具调用说明、代码编辑痕迹（diff vs whole vs diff-fenced）
- 招牌美学（Claude 前端：米色 #F4F1EA + 衬线 + 赤陶色，是极强的家族签名）

## 五遍阅读法

### 第一遍：来源层级判断

先判断文本更像哪一层：

- 模型家族输出：GPT、Claude、Gemini、Doubao。
- 具体版本表面：如 Sonnet/Opus、Flash/Pro、chat/reasoner、mini/pro、o-series。
- 产品表面：ChatGPT、Claude.ai、Gemini app、Perplexity、Cursor、Codex、豆包 App。
- 任务模板：代码解释、搜索摘要、办公写作、长文总结、客服回复。

任务模板不是模型。产品表面也不是模型。

### 第二遍：结构和指令服从

观察文本如何执行任务，落到具体形式：

- 直接给结论，还是先设边界——具体怎么起的句？
- 分点、表格、步骤、摘要的使用方式——几点？带编号吗？嵌套吗？
- 是否主动补"下一步"——下一步是温情式还是任务式？
- 是否过度解释用户没有问的背景——解释了几句？
- 是否像工具调用或搜索摘要后的整理——有没有引用痕迹？
- 是否默认无 markdown（o-series 签名）——纯文本段落还是结构化？

### 第三遍：语气和边界

观察回答气质，但要落到 hedging 密度、开场套话、收尾模式：

- validation-forward phrasing 有没有（"你说得对/很好的问题/这是个好问题"）
- hedging 词的密度（数一下"可能/取决于/不过/但其实/需要说明的是"）
- 是否有观点还是全篇平衡（Claude 4.8 官方说 direct/opinionated，3.x 偏 hedging）
- emoji 使用（Claude 4.8 官方说 sparing）
- 中文产品助手感 vs 翻译腔（见"中文化方式"维度）

### 第四遍：版本线索

优先用 `references/model-version-policy.md` 里列的**有硬证据的版本差异**。没有硬证据的版本差异不要编。

检查是否有版本相关证据：

- 默认无 markdown → o-series 强签名
- 过度工程/造多余文件/滥用 subagent → Claude 4.5/4.6 官方自承
- validation-forward 少 + direct + opinionated → Claude 4.8 官方自承
- 格式脏/畸形多 → chatgpt-4o-latest 量化数据
- 招牌米色+衬线+赤陶美学 → Claude 前端强签名
- 澄清提问极多 → DeepSeek R1 architect 模式

没有版本证据时，只能给家族级相似，并明确写"版本证据不足"。

### 第五遍：反证和误伤

主动找反证：

- 文本可能经过人工编辑。
- 文本可能来自公司模板、产品模板、系统提示。
- 文本可能是翻译腔或行业文体——注意翻译腔和 AI 腔在学术上**同源**（低 perplexity/低词汇多样性/低句法复杂度），非母语写作会被误判为 AI。
- 文本可能由多个模型或 RAG 拼接。
- 文本太短，不足以判断。
- 谨慎的人类产品经理/律师/医生本来就会 hedging，不能凭 hedging 就判 Claude。

如果反证强，就降低置信度。

## 输出要求

- 按文本顺序列证据。
- 每条证据都引用原文片段。
- 每条证据都落到**可观察形式**（具体词/句式/段落组织/行为模式），不要只说"边界感强"。
- 每条证据都说明它像哪个模型家族/版本表面，以及为什么——要能指向 profile 里的具体签名。
- 必须写版本不确定性。
- 必须区分模型家族和产品表面。
- 不要把 Perplexity 当基础模型家族（见 `references/model-version-policy.md`）。
