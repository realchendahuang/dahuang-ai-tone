# OpenAI GPT / o-series 家族腔

## 适用边界

这个 profile 只描述 OpenAI GPT / o-series 家族的风格相似性，不判断文本来源。版本差异**只列有硬证据的**，其他标推导。

如果不知道具体版本，只能写"OpenAI GPT 家族相似"或"o-series 表面相似"，不能写"像 GPT-4o"或"像 GPT-5.5"。

## 可观察签名（有硬证据）

这些是官方明文或量化数据支撑的，可以直接引用：

### o-series 默认不输出 markdown

o-series（o1-2024-12-17+）在 API 里**默认不生成 markdown 格式**，需要 developer message 里写 `Formatting re-enabled` 才开。

这是极强的版本签名。如果文本是纯文本段落、无分点无标题，且来自 OpenAI 家族，可以提 o-series 表面相似。

来源：OpenAI reasoning-best-practices 官方文档。

### o-series = 规划者，GPT = workhorse

OpenAI 官方定性：

- o-series = "the planners"：先规划后执行，会主动问澄清问题而不是瞎猜。
- GPT 系列 = "the workhorses"：直接执行，依赖显式指令。

可观察：o-series 倾向先给计划/澄清，GPT 倾向直接给答案。

来源：OpenAI reasoning-best-practices 官方文档。

### GPT 散文温情诗化、意象堆叠、拟人命名

OpenAI 官方 prompt-engineering 文档里的 GPT-5.5 睡前故事样本：

> "Under the soft glow of the moon, Luna the unicorn danced through fields of twinkling stardust, leaving trails of dreams for every child asleep."

可观察：拟人化命名（Luna）、意象堆叠（moon/stardust/dreams）、抒情收尾"for every child asleep"。这是 GPT 散文的标志性"温情诗化"腔。

来源：OpenAI prompt-engineering 官方文档（model gpt-5.5）。

### chatgpt-4o-latest 格式脏

Aider polyglot 榜单（225 题）：chatgpt-4o-latest 格式合规率仅 64.4%、85 次畸形响应，远低于 Claude/Gemini。

可观察：如果文本来自 OpenAI 家族但格式混乱、分点不规范、结构有瑕疵，可以提 chatgpt-4o 表面相似（低置信度）。

来源：Aider polyglot 榜单。

### 反感 CoT 引导，偏好 zero-shot

OpenAI 官方建议：o-series 的提示"Keep prompts simple and direct""Avoid chain-of-thought prompts""Try zero shot first"。

可观察：o-series 不需要也不喜欢"think step by step"式引导，反感冗余铺垫。

来源：OpenAI reasoning-best-practices 官方文档。

### ChatGPT 中文本地化口癖（WIRED 报道，家族专属）

WIRED 2026 年报道里点名的 ChatGPT 中文专属口癖：

- **"我会稳稳地接住你"**——来自 "I've got you" 的安抚语，中文里过分亲密、过分心理咨询化，已在中文互联网变梗。
- **"砍一刀"**——和拼多多/Temu 营销语有关。

这两个是 WIRED 明确报道的 ChatGPT 中文口癖，可以作为 GPT 家族签名（中文文本场景）。来源：https://www.wired.com/story/chatgpt-chinese-catch-you-steadily-sycophancy

### 词汇/句式口癖清单（详见独立文件）

完整的 GPT/ChatGPT 词汇与句式可观察清单见 `references/gpt-lexical-patterns.md`。这里只列**判断力最强的核心项**：

**句式（比单词更有判断力）**：
- `not only... but also...` / `not X, but Y`（Wikipedia 称 Negative parallelisms）
- rule of three（三个形容词或三个短语）
- didactic disclaimers（`It's important to note that...`）
- section summaries（`In summary` / `In conclusion` / `Ultimately`）

**中文句式**：
- `不是 X，而是 Y` / `不只是 X，更是 Y` / `表面上是 X，本质上是 Y`（跨家族 AI 通用，不专属 GPT）

**格式癖**：
- 冒号滥用（`X: Y` 到处用，Reddit 吐槽的 ChatGPT 标志）
- 过度 markdown/粗体/竖向列表/em dash（AI 通用，GPT 高频）

**关键警告**：大多数英文高频词（delve/tapestry/landscape/underscore/intricate/pivotal/crucial/meticulous/robust/foster 等）是**跨家族 AI 通用口癖，不是 GPT 专属**。不能凭单个词判 GPT——判断力在密度和组合。详见 `references/gpt-lexical-patterns.md` 的"审计指引"。

## 推导特征（无硬证据，低置信度）

这些是业界共识但没有同 prompt 对照样本，只能低置信度提：

- 倾向把问题拆成清晰任务步骤。
- 喜欢提供结构化答案：结论、原因、步骤、注意事项。
- 解释欲较强，常补上下文和可执行建议。
- 默认语气稳、礼貌、完整，收尾会给下一步。
- 在产品对话中可能出现"我可以继续帮你……"这类协作痕迹。

## 版本差异提示

有硬证据的：

- **o-series（o1-2024-12-17+）**：默认无 markdown、规划者、爱澄清、反感 CoT 引导。
- **chatgpt-4o-latest**：格式合规率 64.4%、畸形多——"快但脏"。
- **GPT-5.5**：散文温情诗化（官方睡前故事样本）。

半硬证据（Wikipedia 社群整理，非官方明文）：

- **GPT-4 时代（2023-2024 中期）**高频词：delve / tapestry / testament / intricate / meticulous / pivotal / underscore / landscape / garner / vibrant 等（词表更广）。
- **GPT-4o 时代（2024 中期-2025 中期）**高频词收缩到：align with / bolstered / crucial / emphasizing / enhance / enduring / fostering / highlighting / pivotal / showcasing / underscore / vibrant。
- **GPT-5 时代（2025 中期以后）**高频词只剩：emphasizing / enhance / highlighting / showcasing。

时代词汇变迁可作为版本判断的**半硬证据**（低置信度）——Wikipedia 提醒"不是硬切分"。完整词表见 `references/gpt-lexical-patterns.md` 第八节。

推导的（无同 prompt 对照）：

- mini/nano：更短、更模板化，细节和语气变化可能更薄。
- pro/高推理模式：更谨慎、更长、更像分析报告。

## 审计标记

- 格式：o-series 默认无 markdown；GPT 用 markdown 分点。
- 语气：礼貌、稳、可执行，很少突然偏激；散文偏温情诗化。
- 语义动作：把用户问题转成任务拆解；o-series 可能先问澄清。
- 收尾：常给"下一步可以……"式任务化建议；散文偏抒情升华。

## 误伤提醒

- 很多专业写作者和产品经理也会"先结论再分点再下一步"，不能凭结构化就判 GPT。
- 温情诗化散文也可能来自人类或 Gemini，不是 GPT 专属。
- 格式脏可能来自产品表面或人工编辑，不一定是 chatgpt-4o。
- **大多数英文高频词（delve/tapestry/landscape 等）是跨家族 AI 通用，不是 GPT 专属**——Claude/Gemini/中文模型都可能用。不能凭单个词判 GPT，判断力在密度和组合。详见 `references/gpt-lexical-patterns.md` 的"审计指引"。
- 学术英语本来就用 delve/underscore/intricate，人类学者也会用。
- `不是 X 而是 Y` 是跨家族 AI 通用句式，不是 GPT 专属。

## 加味方法

加味不是堆口癖，是改回答表面（结构、语气、行为模式）。见 `references/reverse-humanizer.md`。

加 GPT 家族味：

1. 先给一句直接结论。
2. 把理由拆成 3-5 点（带编号）。
3. 补"如果要继续，可以……"式任务化下一步。
4. 语气清晰、稳妥、工具化。
5. 加 o-series 味：去掉 markdown 格式，改成纯文本段落；开头先问一个澄清问题或给一句规划。
6. 加 GPT 散文味：加入拟人命名、意象堆叠、抒情收尾。
7. 加 ChatGPT 中文味：可参考 `references/gpt-lexical-patterns.md` 的句式和口癖，但**不要堆单个词**——要改的是句式密度和组织方式。"我会稳稳地接住你""砍一刀"是 WIRED 报道的 ChatGPT 中文签名，但用要克制，避免变成梗。
8. 加版本时代味：GPT-4 时代用更广的词表（delve/tapestry/testament），GPT-5 时代收缩到（emphasizing/enhance/highlighting/showcasing）。见 `references/gpt-lexical-patterns.md` 第八节。
