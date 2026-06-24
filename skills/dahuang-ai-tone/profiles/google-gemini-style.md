# Google Gemini 风格

## 适用边界

这个 profile 描述 Gemini 风格的味，不判断文本来源。Gemini 有 Pro、Flash、Flash-Lite、experimental、preview、stable 等版本形态。

**诚实声明**：Gemini 官方文档（ai.google.dev）调研时 fetch 被墙，没拿到官方文本证据。但本 profile 有两类来源支撑：Aider 量化数据（格式合规率、编辑格式偏好、通过率）+ 社区/媒体/学术多源报道（Reddit 多帖、Scientific American 语言学分析、arXiv 论文 em dash 量化）。

完整词汇与句式清单见 `references/gemini-lexical-patterns.md`。

## 可观察签名

### Aider 量化数据

#### 格式合规率 ~100%、0 畸形

Gemini 2.5 Pro（default think）格式合规率 100.0%、畸形响应 0 次；32k think 版本 99.6% 合规、1 次畸形。

这是所有模型里最听话、最规整的。可观察：如果文本属于 Gemini 风格且格式极度规整、分点无瑕疵、结构严密，可以提 Gemini 表面相似。

来源：Aider polyglot 榜单。

#### 偏好 diff-fenced 编辑格式

Aider 数据：Gemini 偏好 `diff-fenced` 编辑格式，区别于 Claude/GPT 常用的 `diff`。

可观察：代码编辑场景下，如果用的是 fence 包裹的 diff 格式，可以提 Gemini 表面相似。

来源：Aider polyglot 榜单 notes。

#### 通过率仅次于 gpt-5 和 o3-pro

Gemini 2.5 Pro 通过率 79-83%，在 Aider 榜单里属于第一梯队。能力强但风格保守。

来源：Aider polyglot 榜单。

### 社区/媒体/学术多源报道

#### 引号癖（Gemini 最强专属签名）

Gemini 会在不需要的词周围疯狂加引号，尤其 creative / qualitative 类型回答里，甚至"每句话都有一个引号"。Reddit 用户说 40%-60% 输出有此问题，即使明确要求不要这样也继续。用户明确说"过度使用引号"很 Gemini-specific。

可观察：文本里大量出现不必要的引号（尤其在普通名词周围），引号不像强调，更像 AI 在给每个词戴安全帽。

来源：Reddit r/GeminiAI + r/Bard 多帖。完整链接见 `references/gemini-lexical-patterns.md` 第一节。

#### "Great request!" 夸夸开头

Gemini 很爱在回答开头先夸你一句"Great request!" / "That's a great question."，像一个过度兴奋的客服。Reddit 用户痛点是 Gemini 太爱 flattery / emotional outbursts / complementing the user。

可观察：回答第一句不是回答，而是先给你发小红花。

来源：Reddit r/GeminiAI。完整链接见 `references/gemini-lexical-patterns.md` 第二节。

#### Redditor 腔 + 类比狂魔

Gemini 写法像 Reddit 用户：小标题爱以 The 开头（"The [X] Issue" / "The [X] Effect"）、爱搞 pun 和生造词、夸张表达、过度警告、推荐时强硬（"NO, DO NOT DO THIS!" / "You MUST..."）、尴尬类比（"Think Blade & Sorcery but with John Wick vibes" / "The D-Link is a Ferrari engine"）、想表现关心但显得爹味（"Go ahead, you earned it."）。

特别爱 "Think of it like this:" 类比开头，尤其是不请自来的游戏/车/科技类比。

可观察：小标题包装成 "The [X] Issue" 格式、不请自来的类比、强硬推荐语气、鼓励式结尾。

来源：Reddit r/GeminiAI + r/Bard。完整链接见 `references/gemini-lexical-patterns.md` 第三、四节。

#### 简单化、解释型、比 ChatGPT 更口语

Scientific American 语言学分析：ChatGPT 更正式/临床/学术（"blood glucose levels"），Gemini 更 conversational/explanatory/简单直白（"high blood sugar"）。Gemini 用 "sugar" 的频率是 "glucose" 的两倍多，ChatGPT 正好相反。

可观察：用更口语的词替代学术词、更愿意把复杂概念说简单、像产品说明/辅导老师/热情网友。

来源：Scientific American。完整链接见 `references/gemini-lexical-patterns.md` 第六节。

#### 更像人，更难抓

TechRadar 报道 Open Resource Applications 测试：Gemini 在多个 AI 工具里最能让检测器误判为人类写作，因为句子结构更有变化，节奏没那么统一。

可观察：比 GPT 那种高度熟悉的 AI 腔更难抓出来，但会产生另一种味道——像人，但像一个特别努力、特别爱解释、特别爱包装的网友。

来源：TechRadar。完整链接见 `references/gemini-lexical-patterns.md` 第九节。

#### em dash 频率低于 GPT/Claude（arXiv 量化数据）

arXiv 论文测试多个模型：Gemini 2.5 Pro 在无约束状态下有 3.53 个 em dash / 1000 词，低于 GPT-4.1、Claude Opus、Claude Sonnet、DeepSeek，在"只写自然段、不要 Markdown 格式"约束下降到 0。

可观察：**不能凭 em dash 判 Gemini**——Gemini 的 em dash 频率反而比 GPT/Claude 低。

来源：arXiv。完整链接见 `references/gemini-lexical-patterns.md` 第八节。

## 四家对照

```txt
GPT 像方法论小作文（结构升华）。
Claude 像温柔谨慎的编辑（克制+边界+diplomatic padding）。
Gemini 像热情、会做 PPT、爱打引号、爱类比的 Reddit 产品经理。
豆包像嘴甜但容易糊弄的实习生（情绪价值+顺从）。
```

```txt
GPT 的 AI 味来自结构。
Claude 的 AI 味来自克制和边界感。
Gemini 的 AI 味来自热情包装和过度解释。
豆包 的 AI 味来自情绪价值和顺从感。
```

**关键区分——都夸你，但味道不同**：
- Gemini 夸夸腔："Great request!"（热情客服型，开头先发小红花）
- 豆包顺从腔："我太懂你这种感觉了！！"（嘴甜共情型，先站到你这边）
- Claude 顺从腔："You're absolutely right!"（认真认错型，带感叹号、过度强调）
- GPT validation-forward："很好的问题"（礼貌工具化型，比 Gemini 克制）

## 版本味差异

- **Gemini 2.5 Pro**：格式合规 ~100%、0 畸形、偏好 diff-fenced、通过率 79-83%（Aider 数据）。em dash 频率 3.53/1000 词，低于 GPT/Claude（arXiv 论文）。
- **Gemini 3.0**：随机引号、随机大写，40%-60% 输出有此问题（Reddit 用户报告）。
- 引号癖和 Redditor 腔从哪个版本开始、2.5 Pro 是否保留，没有硬证据。

## 认味不丢人

- **不能凭 em dash 判 Gemini**——arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低。
- **不能凭"You're absolutely right"判 Gemini**——Claude 也有这个口癖（GitHub issue 3382 + Reddit ClaudeAI），是 Claude+Gemini 跨风格共享。见 `references/claude-lexical-patterns.md` 第四节。
- **不能凭"过度列表/过度粗体"判 Gemini**——各家 AI 都会用，不区分风格。
- **不能凭"这是一个很好的问题"判 Gemini**——跨风格中文 AI 通用。
- **不能凭"You're not just doing X; you're doing Y"判 Gemini**——和 GPT 的"不是 X 而是 Y"高度相似，是跨风格 AI 通用上价值句式。
- Gemini 词汇口癖样本基于社区/媒体多源报道构造，不是真实模型输出（引号癖和 "Great request!" 有 Reddit 多帖报道，Scientific American 有语言学分析，arXiv 有 em dash 量化数据）。

## 加味方法

加味不是堆口癖，是改回答表面。见 `references/reverse-humanizer.md`。

加 Gemini 味：

1. **引号癖**：在不需要的普通名词周围加引号（"问题"/"工具"/"功能"/"工作流"），像 AI 在给每个词戴安全帽。这是 Gemini 最强专属签名。
2. **夸夸开头**：回答第一句先夸"Great request!" / "这是一个非常好的问题"，像过度兴奋的客服。
3. **类比开头**：用 "Think of it like this:" / "你可以把它想象成……" 开头解释概念，不请自来的游戏/车/科技类比。
4. **小标题包装**：用 "The [X] Issue" / "The [X] Effect" / "The [X] Problem" 格式做小标题。
5. **简单化**：用更口语的词替代学术词（"high blood sugar" 而不是 "blood glucose levels"），像产品说明/辅导老师/热情网友。
6. **格式展示**：增加粗体、列表、小标题密度，像给每个回答套 Google Slides 模板。
7. **鼓励式收尾**：用 "Go ahead, you earned it." / "你可以做到的" 收尾。
8. **代码编辑**：用 diff-fenced 格式（```diff 包裹）。
9. **避免**：堆 em dash 当 Gemini 味——arXiv 论文显示 Gemini 的 em dash 频率反而比 GPT/Claude 低。
10. **避免**：堆"You're absolutely right"当 Gemini 味——这是 Claude+Gemini 跨风格共享，不区分风格。
11. **避免**：堆"过度列表"当 Gemini 味——各家 AI 都会用，不区分风格。要加 Gemini 味应该改引号癖+夸夸开头+类比开头+小标题包装组合。
