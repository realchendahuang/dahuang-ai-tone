# 模型腔生成方法

## 核心思路

"加模型腔"不是堆口癖，而是改变回答表面：结构、语气、边界感、推理呈现、产品痕迹、行为模式。

这个 skill 同时做"审计"和"加味"，看起来矛盾，但不矛盾的关键在于：

- **审计**判断的是"这段像不像某家族"——靠可观察证据（句法/词汇/段落/行为）。
- **加味**改的是"这段的整体表面"——靠改结构/语气/行为模式，不是堆标志词。

**加味绝不等于堆标志词**。如果你加 Claude 味只是把"可能/取决于"塞进去，那 audit-workflow 批评的"看到'可能'就判 Claude"就是你亲手制造的误判。加味要改的是整体组织方式，见各家族 profile 的"加味方法"。

改写前先确定目标：

1. 模型家族：GPT / o-series / Claude / Gemini / Doubao。
2. 版本档位：如果用户指定 Sonnet 4.8、Opus 4.6、o-series、Flash 等，就按指定版本表面调整。**只列有硬证据的版本特征**（见 `references/model-version-policy.md`），不要编版本差异。
3. 产品表面：如果用户指定 ChatGPT、Claude.ai、Perplexity、豆包 App 等，要加入产品表面痕迹。

## 家族级改写方向

### OpenAI GPT / o-series 家族

基于 `profiles/openai-gpt-family.md` 的可观察签名：

- **GPT 味**：先给结论 → 分点解释（3-5 点带编号）→ 任务化下一步"如果要继续，可以……"。语气稳、礼貌、工具化。
- **o-series 味**：去掉 markdown 格式，改成纯文本段落；开头先给一句规划或问一个澄清问题；不要"think step by step"式铺垫。
- **GPT 散文味**：加拟人命名、意象堆叠、抒情收尾（参考官方睡前故事样本 Luna/stardust/dreams）。
- **GPT 句式味**：可参考 `references/gpt-lexical-patterns.md` 的句式（`not only... but also...` / rule of three / didactic disclaimers / section summaries）。**句式比单词更有判断力**——改组织方式，不要堆单个词。
- **ChatGPT 中文味**：可参考 `references/gpt-lexical-patterns.md` 的中文句式和官话腔。`不是 X 而是 Y` 是跨家族 AI 通用句式，用的时候要配合其他 GPT 特征。"我会稳稳地接住你""砍一刀"是 WIRED 报道的 ChatGPT 中文签名，但用要克制，避免变成梗。
- **版本时代味**：GPT-4 时代用更广词表（delve/tapestry/testament），GPT-5 时代收缩到（emphasizing/enhance/highlighting/showcasing）。见 `references/gpt-lexical-patterns.md` 第八节。
- **避免**：只堆"结论是……原因有三点"这种表面标签——要改的是整体结构。**不要堆单个英文高频词**（delve/tapestry 等）——这些是跨家族 AI 通用口癖，堆了也不像 GPT 专属，反而像"AI 通用腔"。

### Anthropic Claude 家族

基于 `profiles/anthropic-claude-family.md` 和 `references/claude-lexical-patterns.md` 的可观察签名：

- **Claude 4.8 味**：去掉 validation-forward 开场（不要"你说得对/很好的问题"），第一句直接给观点；emoji 克制；收尾直接下一步不啰嗦总结。
- **Claude 3.x 味**：先承认合理性 → 加边界和例外 → 用"更像是""可能说明"降低结论强度 → 温和可商量的下一步。
- **编程场景**：先一句原理解释（"we need to..."），再给方案（"Here's how to..."）。
- **前端场景**：米色 #F4F1EA 背景 + 衬线展示字（Georgia/Fraunces/Playfair）+ 斜体强调 + 赤陶色。
- **词汇层加味**（见 `references/claude-lexical-patterns.md`）：
  - 加 diplomatic padding：判断前后加 "That said..." / "To be fair..." / "话虽如此" / "公平地说"。
  - 加谨慎腔："I want to be careful here" / "I wouldn't frame it quite that way" / "我不想把话说得太满" / "更准确地说"。
  - 加顺从腔（3.x/4.5/4.6 强，4.8 弱）："You're absolutely right!" / "Good catch." / "你说得对" / "这个提醒很关键"。注意 Claude 顺从腔是"认真认错型"（带感叹号、过度强调），和豆包"嘴甜糊弄型"（哈哈抱歉抱歉）味道不同。
  - 加分层腔："There are a few layers here" / "I'd separate this into three parts" / "这里可以分几层看"。
  - 加保姆腔（2026 出圈怪癖）："You should get some sleep" / "Take a break" / "你该休息一下了" / "我们明天再继续也可以"。
- **避免**：只堆"可能/取决于/不一定意味着"——这正是 audit-workflow 批评的误判源。要改的是开场方式、收尾方式、是否有观点。
- **避免**：堆跨家族通用口癖（共情腔/不是 X 而是 Y/numbered list）——这些不增加 Claude 味，只增加通用 AI 味。共情腔（"I can see why you'd feel that way"）豆包和 ChatGPT 中文疗愈腔都有，"不是 X 而是 Y"是跨家族 AI 通用句式。

### Google Gemini 家族

基于 `profiles/google-gemini-family.md` 和 `references/gemini-lexical-patterns.md` 的可观察签名：

- **引号癖**：在不需要的普通名词周围加引号（"问题"/"工具"/"功能"/"工作流"），像 AI 在给每个词戴安全帽。这是 Gemini 最强专属签名。
- **夸夸开头**：回答第一句先夸"Great request!" / "这是一个非常好的问题"，像过度兴奋的客服。
- **类比开头**：用 "Think of it like this:" / "你可以把它想象成……" 开头解释概念，不请自来的游戏/车/科技类比。
- **小标题包装**：用 "The [X] Issue" / "The [X] Effect" / "The [X] Problem" 格式做小标题。
- **简单化**：用更口语的词替代学术词（"high blood sugar" 而不是 "blood glucose levels"），像产品说明/辅导老师/热情网友。
- **格式展示**：增加粗体、列表、小标题密度，像给每个回答套 Google Slides 模板。
- **鼓励式收尾**：用 "Go ahead, you earned it." / "你可以做到的" 收尾。
- **代码编辑**：用 diff-fenced 格式（```diff 包裹）。
- **避免**：堆 em dash 当 Gemini 味——arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低。
- **避免**：堆"You're absolutely right"当 Gemini 味——这是 Claude+Gemini 跨家族共享，不区分家族。
- **避免**：堆"过度列表"当 Gemini 味——各家 AI 都会用，不区分家族。要加 Gemini 味应该改引号癖+夸夸开头+类比开头+小标题包装组合。

### 字节豆包 / 中文模型家族

基于 `profiles/bytedance-doubao-family.md` 和 `references/doubao-lexical-patterns.md` 的可观察签名：

- **共情开头**：用"我太懂你这种感觉了！！"或"你这个感觉太真实了"开头。
- **"最X" 连发**：承诺用"最直接、最真相、最不绕弯、最扎心"的方式回答。
- **道歉型语气**：被质疑时用"哈哈抱歉抱歉，我看错啦～"而不是冷冰冰的"非常抱歉"。
- **顺从反弯**：用户一反驳立刻"你说得对，是我这边理解偏了，我重新给你梳理一下"。
- **"先保证不废话然后继续废话"**：开头说"我不绕弯，直接给你说重点"，然后正文继续分情况。
- **情绪价值层**：加"你已经做得很好了/别太为难自己/我在这里陪你"做甜嘴补救。
- **避免**：只堆"你可以先……再……"——这是上一版 profile 的推导，没有硬证据支撑。
- **避免**：只堆单个"我懂你"或"你说得对"——这些跨家族通用，堆了不像豆包专属。要加豆包味应该改整体语气：共情+最X连发+哈哈道歉+顺从反弯组合。
- **诚实提醒**：豆包型人格梗是社群归纳，不是字节官方说法。

## 产品表面改写

### Perplexity 式检索增强回答

Perplexity 不是基础模型家族。要做的是产品表面：

- 先给简短答案。
- 补来源感或引用感。
- 综合多个网页信息。
- 避免长篇闲聊。

如果用户明确指定 Sonar API 模型，再按 Sonar / Sonar Pro / Sonar Reasoning Pro 等模型表面处理。见 `references/model-version-policy.md`。

## 交付格式

```md
## 改写后

{文本}

## 我加的模型腔

1. {结构变化——具体改了什么组织方式}
2. {语气/行为变化——具体改了开场/收尾/hedging 密度}
3. {版本/产品表面变化——引用了哪个硬证据签名}

## 边界

这是风格模拟，不代表由该模型生成，也不能判断具体版本。
```

## 自检：加味有没有变成堆口癖？

改写完自检：

- 我加的是整体结构/行为模式，还是只是塞了几个标志词？
- 如果把加的标志词删掉，文本还像那个家族吗？如果不像，说明我加的是口癖不是腔调，要重做。
- 我引用的版本特征是 `references/model-version-policy.md` 里的硬证据吗？如果是推导，我标低置信度了吗？
- **我有没有堆英文高频词（delve/tapestry/landscape 等）当 GPT 味？**这些是跨家族 AI 通用口癖，堆了不像 GPT 专属，反而像"AI 通用腔"。要加 GPT 味应该改句式（`not only but also` / rule of three）和组织方式，不是堆词。见 `references/gpt-lexical-patterns.md` 的"审计指引"。
- **我有没有堆"不是 X 而是 Y"当 GPT 味？**这是跨家族 AI 通用句式。可以用来加"AI 通用腔"，但不能用来加"GPT 专属味"。
- **我有没有堆"That said"或共情腔当 Claude 味？**单个"That said"跨家族通用，共情腔豆包和 ChatGPT 中文疗愈腔都有。要加 Claude 味应该改 diplomatic padding 组合（That said + worth noting + I want to be careful）+ 顺从腔（You're absolutely right! 认真认错型，不是豆包嘴甜糊弄型）+ 分层腔 + 保姆腔（2026 出圈怪癖）。见 `references/claude-lexical-patterns.md`。
- **我有没有堆 em dash 当 Gemini 味？**arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低。要加 Gemini 味应该改引号癖（在不需要的词周围加引号）+ 夸夸开头（Great request!）+ 类比开头（Think of it like this:）+ 小标题包装（The [X] Issue）组合。见 `references/gemini-lexical-patterns.md`。
