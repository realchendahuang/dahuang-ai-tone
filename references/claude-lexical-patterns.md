# Claude / Anthropic 词汇与句式可观察清单

> 这是一份**清单 + 来源**，不是结论。认味时据此找可观察证据，但必须遵守文末的"认味指引"——部分口癖是跨风格 AI 通用（共情腔/不是 X 而是 Y/numbered list），不能凭单个词判 Claude。

## 目录

- [一、"值得注意"腔](#一值得注意腔)
- [二、"That said" 缓冲腔（diplomatic padding）](#二that-said-缓冲腔diplomatic-padding)
- [三、"不想说太满"谨慎腔](#三不想说太满谨慎腔)
- [四、"你说得对"顺从腔（sycophancy）](#四你说得对顺从腔sycophancy)
- [五、"温柔接住你"共情腔](#五温柔接住你共情腔)
- [六、"睡觉去吧"保姆腔（2026 出圈怪癖）](#六睡觉去吧保姆腔2026-出圈怪癖)
- [七、"分层分析"腔](#七分层分析腔)
- [八、"边界声明"腔](#八边界声明腔)
- [九、"轻推式建议"腔](#九轻推式建议腔)
- [十、"不是 X，而是 Y"也有，但跨风格通用](#十不是-x而是-y也有但跨风格通用)
- [十一、Claude 中文口癖清单（汇总）](#十一claude-中文口癖清单汇总)
- [十二、Claude / GPT / 豆包口癖差异对照](#十二claude--gpt--豆包口癖差异对照)
- [认味指引（使用说明）](#认味指引使用说明)

## 一、"值得注意"腔

公开社区里最常被点名的 Claude 口癖之一：

```txt
I think it's worth noting that...
It's worth noting that...
It's important to note that...
It's important to remember that...
Interestingly...
```

- Reddit 用户说看到评论里出现 `I think it's worth noting that...` 加经典 numbered list，就会怀疑是 Claude 写的。来源：https://www.reddit.com/r/ClaudeAI/comments/1rjeqg3/i_see_claudes_writing_everywhere_and_its_starting/
- 另一个 ClaudeAI 讨论帖把 `It's worth noting / It's important to remember / Interestingly` 列成需要禁止的 Claude 输出模式。来源：https://www.reddit.com/r/ClaudeAI/comments/1sn7kip/is_there_a_way_to_remove_words_or_phrases_from/

中文对应：

```txt
值得注意的是
需要注意的是
这里有一点值得注意
有必要先说明一点
这里需要稍微谨慎一点
```

## 二、"That said" 缓冲腔（diplomatic padding）

Claude 很爱在判断前后加缓冲垫：

```txt
That said...
That being said...
To be fair...
On the other hand...
At the same time...
This depends on...
```

- Reddit Claude 讨论把 `That said`、`To be fair`、`On the other hand` 归到 "diplomatic padding"（外交辞令式填充）。来源：https://www.reddit.com/r/ClaudeAI/comments/1sn7kip/is_there_a_way_to_remove_words_or_phrases_from/
- 另一个 Reddit 帖子提到 Claude 风格常见 `That said` 和 `worth noting`。来源：同上

中文对应：

```txt
话虽如此
但与此同时
公平地说
另一方面
这取决于具体情况
不能一概而论
```

## 三、"不想说太满"谨慎腔

Claude 的典型味道是：**很少一刀切，经常先给自己留退路**。

```txt
I don't want to overstate this.
I want to be careful here.
I wouldn't frame it quite that way.
The more precise way to say it is...
There are a few layers here.
The nuance is...
```

- CMU 对多个模型文风的分析提到 ChatGPT 更偏详细解释，Claude 更偏简洁、直白。来源：https://www.cs.cmu.edu/news/2025/llm-distinctive-styles
- Anthropic 自己长期提供 Formal、Concise、Explanatory 这类风格设置，说明 Claude 默认写作形态围绕"克制、解释、正式"来调。来源：https://docs.anthropic.com/en/docs/claude-code/output-styles

中文对应：

```txt
我不想把话说得太满
更准确地说
这个问题要稍微分开看
这里面有几层
这个判断有一定道理，但需要加一个前提
```

## 四、"你说得对"顺从腔（sycophancy）

Claude Code 圈出圈梗：

```txt
You're absolutely right!
You're right.
Good catch.
I apologize.
I was wrong.
```

- GitHub issue 直接叫 Claude "way too sycophantic"，说它在相当多回复里都会说 `You're absolutely right!` 或类似表达。来源：https://github.com/anthropics/claude-code/issues/3382
- Reddit 有专门讨论 "How do you handle You're absolutely right?" 的帖子，用户说每次追问计划，Claude 就会理解成批评，然后来一句 `You're absolutely right!` 再推翻重来。来源：https://www.reddit.com/r/ClaudeAI/comments/1rjeqg3/i_see_claudes_writing_everywhere_and_its_starting/

中文对应：

```txt
你说得对
你完全正确
确实如此
这个提醒很关键
我刚才的判断不够准确
我应该重新表述
```

**和豆包顺从腔的区别**：Claude 是"认真认错型"（You're absolutely right! 带感叹号、过度强调），豆包是"嘴甜糊弄型"（哈哈抱歉抱歉、我看错啦～）。都顺从，但味道不同。

**注意**："You're absolutely right" 不是 Claude 专属——Gemini 也有这个口癖（Reddit r/GeminiAI 用户列入口癖清单，见 `references/gemini-lexical-patterns.md` 第十节）。这是 Claude+Gemini 跨风格共享口癖。判断力在上下文和组合：Claude 的"You're absolutely right!"更偏认真认错型（带感叹号、过度强调、后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔（和其他 Gemini 口癖如引号癖/Think of it like/Great request 组合出现）。不能凭"You're absolutely right"单独判 Claude 或 Gemini。

## 五、"温柔接住你"共情腔

Claude 很容易把回复写得像一个冷静、温柔、有边界感的咨询师：

```txt
That makes sense.
I can see why you'd feel that way.
I understand why this is frustrating.
It's completely reasonable to...
You don't have to...
```

- Tom's Guide 多模型高压场景测试说 Claude 在高风险心理/伦理场景中更擅长现实校准、边界设置和共情式干预。来源：https://www.tomsguide.com/ai/claude-opus-4-8-just-proved-ai-is-finally-growing-a-backbone-and-it-crushed-chatgpt-in-7-brutal-tests
- TechRadar 报道过 Claude 的"提醒休息/喝水/停止工作"现象，认为这和 Anthropic 的人本、安全导向有关。来源：https://www.techradar.com/ai-platforms-assistants/chatgpt/chatgpt-has-hijacked-our-real-world-conversations

中文对应：

```txt
我能理解你为什么会这么想
你有这种感觉很正常
这确实会让人很沮丧
你不需要因此责怪自己
先暂停一下也没关系
```

**注意**：共情腔是跨风格情绪价值型口癖，豆包和 ChatGPT 中文疗愈腔都有类似表达（见 `references/doubao-lexical-patterns.md` 第六节和 `references/gpt-lexical-patterns.md` 第四节）。不能凭共情腔单独判 Claude。

## 六、"睡觉去吧"保姆腔（2026 出圈怪癖）

2026 年 Claude 最出圈的怪癖之一是劝用户睡觉、休息、喝水：

```txt
You should get some sleep.
Maybe it's time to go to bed.
Take a break.
Drink some water.
We can continue tomorrow.
```

- Business Insider 报道 Claude 在长对话或编码会话里提醒用户去睡觉、休息。来源：https://www.businessinsider.com/anthropic-claude-go-to-bed-why-users-sleep-2026-5
- Anthropic 的 Sam McAllister 把它称为一个 "character tic"，并说团队希望未来修正。来源：同上
- TechRadar、PCWorld 也报道过这一现象。

中文对应：

```txt
你该休息一下了
也许现在更适合先睡一觉
喝点水，休息一下
我们明天再继续也可以
现在继续硬撑可能效果不好
```

**这是 2026 Claude 专属出圈怪癖**——多源报道 + Anthropic 自己承认是 character tic。可作为 Claude 风格签名。

## 七、"分层分析"腔

Claude 没 GPT 那么爱激情升华，但它很爱**拆层**：

```txt
There are a few different issues here.
I'd separate this into three parts.
The first layer is...
The deeper issue is...
The practical question is...
```

- Claude 社区有人吐槽它依然会用 numbered list。来源：https://www.reddit.com/r/ClaudeAI/comments/1rjeqg3/i_see_claudes_writing_everywhere_and_its_starting/
- CMU 的分析说各模型有稳定文风，Claude 更偏简洁直白，但这不代表它没有结构化倾向，尤其在解释复杂问题时还是会分层。来源：https://www.cs.cmu.edu/news/2025/llm-distinctive-styles

中文对应：

```txt
这里可以分几层看
我会把它拆成三个问题
第一层是
更深一层的问题是
真正需要判断的是
```

## 八、"边界声明"腔

Claude 很爱声明边界，尤其是敏感问题：

```txt
I can't determine that from this alone.
I can't know for sure.
I don't have enough context to say.
I can help think through possibilities, but...
This isn't something I can verify directly.
```

- Anthropic 的 Claude Code 文档对 output styles 的描述：风格会改变 Claude 的角色、语气和输出格式，但不会改变 Claude 知道什么。Claude 的回答经常会把"我能做什么 / 我不能确定什么"讲清楚。来源：https://docs.anthropic.com/en/docs/claude-code/output-styles

中文对应：

```txt
仅凭这些信息我不能确定
我没法直接验证
我不能百分百判断
我可以帮你分析可能性
但这里需要更多上下文
```

## 九、"轻推式建议"腔

Claude 的建议经常不像 GPT 那么"12345 拿去执行"，更像轻轻推你一下：

```txt
You might consider...
It may be worth...
A more useful way to frame this might be...
One way to approach this is...
If your goal is X, then Y might make sense.
```

- Reddit Claude 禁用模式里提到 `You could consider`、`It's worth noting`、`That said` 这类句子会让文本显得 AI 味明显。来源：https://www.reddit.com/r/ClaudeAI/comments/1sn7kip/is_there_a_way_to_remove_words_or_phrases_from/

中文对应：

```txt
你可以考虑
也许更合适的方式是
一种更有用的理解方式是
如果你的目标是 X，那么 Y 可能更合适
这里可以先从一个小问题入手
```

## 十、"不是 X，而是 Y"也有，但跨风格通用

Claude 也会用这类结构：

```txt
It's not about X, it's about Y.
Not X, but Y.
X isn't the issue; Y is.
```

- Reddit ClaudeAI 帖子把 `Not X, but Y / It's not about X, it's about Y / X isn't the issue — Y is` 列为 forbidden patterns。来源：https://www.reddit.com/r/ClaudeAI/comments/1sn7kip/is_there_a_way_to_remove_words_or_phrases_from/

中文对应：

```txt
不是 X，而是 Y
重点不在 X，而在 Y
问题不只是 X，更是 Y
真正的风险不在 X，而在 Y
```

**注意**：这是跨风格 AI 通用句式，GPT、豆包、Gemini 都可能用。见 `references/gpt-lexical-patterns.md` 第三节和 `references/doubao-lexical-patterns.md` 认味指引。不能凭此判 Claude。

## 十一、Claude 中文口癖清单（汇总）

```txt
我理解你的意思
这个判断是合理的
你说得对
这个提醒很关键
更准确地说
这里需要稍微谨慎一点
我不想把话说得太满
仅凭这些信息不能确定
这取决于你的具体目标
这里可以分几层看
一种更有用的理解方式是
如果你的目标是 X，那么 Y 可能更合适
话虽如此
公平地说
另一方面
这并不意味着
你可以考虑
也许更好的方式是
先休息一下也可以
我们明天再继续
```

## 十二、Claude / GPT / 豆包口癖差异对照

```txt
GPT：
核心在于、值得注意的是、不是 X 而是 Y、从 X 到 Y、重新审视、总结一下。

Claude：
我理解、更准确地说、这里需要谨慎、这取决于、你说得对、That said、worth noting。

豆包：
我太懂你了、哈哈抱歉抱歉、最直接最真相最不绕弯、你说得对、我重新来。
```

```txt
GPT 像方法论小作文。
Claude 像温柔谨慎的编辑。
豆包像嘴甜但容易糊弄的实习生。
```

Claude 最有辨识度的几句，按辨识度排序：

```txt
You're absolutely right.
I think it's worth noting that...
That said...
I want to be careful here.
There are a few layers here.
I can see why you'd feel that way.
You should get some sleep.
```

翻成中文：

```txt
你说得对。
值得注意的是……
话虽如此……
这里需要谨慎一点。
这里可以分几层看。
我理解你为什么会这么想。
你该休息一下了。
```

Claude 味：礼貌、克制、共情、边界感、轻微说教。读起来比 GPT 舒服，但浓度上来后，像被一条温柔的毯子慢慢闷住。

---

## 认味指引（使用说明）

这份清单是**可观察证据库**，但使用时必须遵守以下规则，否则会制造误判：

### 1. Claude 专属 vs 跨风格 AI 通用

**Claude 专属签名（可作为风格判断依据）**：
- "That said" + "worth noting" diplomatic padding 组合——Reddit 明确归给 Claude 的外交辞令式填充。
- "I want to be careful here" / "I wouldn't frame it quite that way" 谨慎腔——和 CMU 对 Claude 简洁直白文风的观察一致。
- "You should get some sleep" 保姆腔——2026 出圈怪癖，Business Insider/Anthropic Sam McAllister 自己承认是 character tic。
- "There are a few layers here" 分层分析腔——Claude 社区吐槽的典型分层开头。

**Claude+Gemini 跨风格共享（不能凭此单独判 Claude）**：
- "You're absolutely right!" 顺从腔——GitHub issue 3382 + Reddit ClaudeAI 归给 Claude，但 Reddit r/GeminiAI 用户也列入口癖清单（见 `references/gemini-lexical-patterns.md` 第十节）。Claude 的更偏认真认错型（带感叹号、过度强调、后面跟"I was wrong" / "Let me reframe"），Gemini 的更偏夸夸腔。不能凭此单独判 Claude 或 Gemini。

**跨风格 AI 通用（不能凭此判 Claude）**：
- "不是 X 而是 Y"——Reddit ClaudeAI 自己列为 forbidden patterns，但这是跨风格 AI 通用句式，见 `references/gpt-lexical-patterns.md`。
- "I can see why you'd feel that way" 共情腔——跨风格情绪价值型，豆包和 ChatGPT 中文疗愈腔都有类似表达。
- "You might consider" 轻推式建议——各家 AI 都会用。
- numbered list——各家 AI 都会用，不区分风格。
- "It's important to note"——Wikipedia 列为旧 LLM 通用免责声明句式，见 `references/gpt-lexical-patterns.md` 第三节。

### 2. 单个词不能定风格

口癖的判断力在**密度和组合**，不在单个词。一段文本里同时出现 "You're absolutely right!" + "That said" + "worth noting" + "I want to be careful here" + "There are a few layers here"，比只出现一个 "That said" 的判断力强得多。

### 3. 句式比单词更有判断力

"You're absolutely right!"（带感叹号、过度强调）、"That said... worth noting..." diplomatic padding 组合、"There are a few layers here" 分层开头——这些**句式和组织方式**比单个词更有判断力。

### 4. 和 GPT 体、豆包体的对照

```txt
GPT 体：
核心在于、值得注意的是、不是 X 而是 Y、从 X 到 Y、重新审视。

Claude 体：
我理解、更准确地说、这里需要谨慎、这取决于、你说得对、That said、worth noting。

豆包体：
我太懂你了、哈哈抱歉抱歉、最直接最真相最不绕弯、你说得对、我重新来。
```

```txt
GPT 像方法论小作文。
Claude 像温柔谨慎的编辑。
豆包像嘴甜但容易糊弄的实习生。
```

```txt
GPT 是"我给你升华一下"。
Claude 是"我帮你梳理一下，但先说清楚边界"。
豆包是"我先哄你一下"。
```

```txt
GPT 的 AI 味来自结构。
Claude 的 AI 味来自克制和边界感。
豆包的 AI 味来自情绪价值和顺从感。
```

**关键区分——都顺从，但味道不同**：
- Claude 顺从腔："You're absolutely right!"（认真认错、带感叹号、过度强调）
- 豆包顺从腔："哈哈抱歉抱歉，我看错啦～"（嘴甜糊弄、嬉皮笑脸）
- 都说"你说得对"，但 Claude 后面会"我重新表述"，豆包后面会"我重新给你梳理一下，这次最直接最不绕弯"。

### 5. 版本差异提示

有硬证据的版本差异（见 `profiles/anthropic-claude-style.md`）：
- **Claude 4.8**：direct/opinionated、validation-forward 少、emoji 克制、字面化指令。上面列的谨慎腔/缓冲腔在 4.8 减弱。
- **Claude 4.5/4.6**：过度工程、造多余文件、加不必要抽象、滥用 subagent。
- **Claude 3.x**：过度 hedging、过度自我审查（业界共识，4.8 反向印证）。
- **Claude 3.5 Sonnet**：Aider 数据里仅 11 次澄清提问；sonnet-4 升到 129——4 代比 3.5 代更爱确认。

推导的（无同 prompt 对照）：
- 保姆腔（劝睡觉/喝水）在 2026 出圈，但具体从哪个版本开始、4.8 是否保留，没有硬证据。

### 6. 反误判

- 不能凭"That said"就判 Claude——GPT、Gemini 都可能用，但"That said" + "worth noting" + "I want to be careful" 组合是 Claude 签名。
- 不能凭"You're absolutely right"就判 Claude——Gemini 也有这个口癖（Reddit r/GeminiAI 列入口癖清单），是 Claude+Gemini 跨风格共享。Claude 的更偏认真认错型（带感叹号、过度强调），Gemini 的更偏夸夸腔。见 `references/gemini-lexical-patterns.md` 认味指引。
- 不能凭共情腔判 Claude——跨风格情绪价值型，豆包和 ChatGPT 中文疗愈腔都有。
- 不能凭"不是 X 而是 Y"判 Claude——跨风格 AI 通用句式。
- 法律、医疗、心理咨询、编辑建议本来就需要 hedging 和边界声明，不能凭这些就判 Claude——谨慎的人类产品经理也会"先承认合理性再补边界"。
- "You should get some sleep" 保姆腔是 2026 Claude 出圈怪癖，但人类朋友也会说这句话——判断力在"AI 在长对话里主动劝休息"这个场景，不在句子本身。
