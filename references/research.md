# Dahuang AI Tone 调研笔记

## 当前结论

`dahuang-ai-tone` 做"模型腔调风格审计"，不是内容腔调分类，也不是 AI 文本检测。

核心判断：

1. 主轴是四个高频模型家族：OpenAI GPT/o-series、Anthropic Claude、Google Gemini、字节豆包。
2. 版本意识必须有**硬证据**支撑（官方明文或量化数据），没有硬证据的版本差异只能标推导。见 `references/model-version-policy.md`。
3. 产品表面不是模型。Perplexity 的处理见 `references/model-version-policy.md`。
4. 审计必须落到**可观察证据**（具体词/句式/段落组织/行为模式），不靠印象。

## 学术根基

这个 skill 的目标在学术上已被证明可行——AI 文本取证（AI-generated text forensics）可分为 detection、attribution、characterization 三类，本 skill 只做 characterization，并且具体做 source family classification。

来源：

- A Survey of AI-generated Text Forensic Systems: https://arxiv.org/abs/2403.01152
  - §2.3.3 Source Family Classification：用 stylometry + PLM 可以把文本归属到"闭源 vs 开源"模型家族，高准确率。**这正是 dahuang 想做的事，有学术支撑。**
  - 可计算特征：stylometry（短语学/标点/语言多样性）、structural（事实结构/共指链一致性）、sequential（Uniform Information Density/句级 log probability）、probabilistic（perplexity/self-consistency/DetectGPT 负曲率）。
  - Base 模型 vs 微调模型也可区分（Foley et al. 2023）。
- Can AI-Generated Text be Reliably Detected?: https://arxiv.org/abs/2303.11156
  - 检测可靠性有限，改写攻击有效——所以 dahuang 只做"风格相似度"，不做"来源鉴定"。
- Paraphrasing evades detectors: https://arxiv.org/abs/2303.13408
  - DIPPER 等改写工具能规避检测——所以改写、翻译、混写后的文本置信度要降。
- GPT detectors are biased against non-native English writers: https://arxiv.org/html/2304.02819
  - **关键**：非母语英文写作被误判为 AI，因为两者共享同一组特征——低 perplexity、低词汇丰富度、低词汇多样性、低句法复杂度、低语法复杂度。
  - 实验佐证：prompt "Enhance word choices to sound like native speaker" → 误判率从 61.22% 降到 11.77%；"Simplify word choices as if non-native" → 误判率从 5.19% 升到 56.65%。
  - **对 dahuang 的意义**：翻译腔和 AI 腔在语言层面同源。中文里的翻译腔标志（高频通用动词/抽象名词化/欧化长定语/连接词冗余/被动句过多）既是翻译腔也是 AI 腔——不能凭翻译腔判某模型家族。

## 官方风格自述（硬证据来源）

这些是各家族官方明文给出的风格特征，可以直接引用进 profile：

### OpenAI

- OpenAI models: https://developers.openai.com/api/docs/models
- Prompt engineering guide（含 GPT-5.5 真实样本）: https://platform.openai.com/docs/guides/prompt-engineering
- Reasoning best practices（o-series vs GPT 定性、默认无 markdown、澄清提问行为）: https://platform.openai.com/docs/guides/reasoning-best-practices

### Anthropic

- Claude models overview: https://platform.claude.com/docs/en/about-claude/models/overview
- Prompting Claude Opus 4.8（validation-forward 少/emoji 克制/direct/字面化/招牌美学）: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/prompting-claude-opus-4-8
- Claude prompting best practices（通用风格/overeagerness/AI slop 自承/4.5-4.6 过度工程）: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-prompting-best-practices

### Google / 字节 / Perplexity

- Google Gemini models: https://ai.google.dev/gemini-api/docs/models （调研时 fetch 被墙，需手动查）
- 火山方舟模型列表: https://www.volcengine.com/docs/82379/1330310 （JS 渲染，需手动查）
- Perplexity Sonar models: https://docs.perplexity.ai/docs/sonar/models

## GPT/ChatGPT 词汇口癖研究（可观察证据库）

完整的词汇与句式清单见 `references/gpt-lexical-patterns.md`。这里记录来源和关键发现：

### 学术论文（词汇频率统计）

- Kobak et al.《Delving into LLM-assisted writing in biomedical publications through excess vocabulary》: https://arxiv.org/abs/2406.07016 — 1500 万篇 PubMed 摘要，LLM 出现后风格词突增，2024 年至少 13.5% 生物医学摘要经 LLM 处理。
- 多数据库研究《How much are LLMs changing the language of academic papers after ChatGPT?》: https://arxiv.org/abs/2509.09596 — `delve` 增长 ~1500%，`underscore` ~1000%，`intricate` ~700%；PMC 全文 `underscore` 高频使用比例 2022-2025 增长超 10000%。
- Juzek & Ward《Why Does ChatGPT "Delve" So Much?》: https://arxiv.org/abs/2412.11385 — 识别 21 个 LLM focal words。

### 社区整理（词汇/句式/格式清单）

- Wikipedia:Signs of AI writing: https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing — "Words to watch"、Negative parallelisms、rule of three、didactic disclaimers、section summaries、格式癖、GPT-4/4o/5 时代词汇差异。
- Reddit r/ChatGPTPro 用户整理帖: https://www.reddit.com/r/ChatGPTPro/comments/163ndbh/overused_chatgpt_terms_add_to_my_list/ — 社区吐槽的 ChatGPT 口癖和冒号滥用。

### 媒体报道（中文口癖）

- WIRED《ChatGPT Has 'Goblin' Mania in the US. In China It Will 'Catch You Steadily'》: https://www.wired.com/story/chatgpt-chinese-catch-you-steadily-sycophancy — ChatGPT 中文口癖"我会稳稳地接住你""砍一刀"；中文回答受英语影响，句子更长更不必要。
- The Verge: https://www.theverge.com/openai/686748/chatgpt-linguistic-impact-common-word-usage — ChatGPT 偏好词在学术 YouTube 视频使用频率最高增 51%。
- TechRadar: https://www.techradar.com/ai-platforms-assistants/chatgpt/chatgpt-has-hijacked-our-real-world-conversations — FSU 研究列出的 AI 高频词。

### 中文社区讨论

- 科学网《为什么 AI 写的文章总有一股 AI 味？》: https://news.sciencenet.cn/htmlnews/2025/10/553334.shtm — AI 文字"工业化痕迹"、中文官话腔词汇、`首先…其次…最后…` 结构、"正确的废话"。
- Threads 讨论"不是……而是……"句式: https://www.threads.com/@an.son1625/post/DSUy0QYkyvx 、https://www.threads.com/@b.alive.is.good/post/DLtgatMy4O5 、https://www.threads.com/@peter_career_hack/post/DOaujRTDbWv
- Facebook 讨论中文"这不是 A，而是 B"句型: https://www.facebook.com/grayhawklit/posts/10161712179451732

### 关键发现

- `delve` 增长 ~1500%、`underscore` ~1000%——LLM 出现后学术英语词汇分布显著变化。
- ChatGPT 中文有本地化怪口癖（"我会稳稳地接住你""砍一刀"），WIRED 报道。
- **大多数英文高频词是跨家族 AI 通用，不是 GPT 专属**——不能凭单个词判 GPT。
- GPT-4/4o/5 时代高频词有收缩趋势（Wikipedia 社群整理），可作为版本判断半硬证据。

## 豆包体口癖研究（可观察证据库）

完整的豆包体词汇与句式清单见 `references/doubao-lexical-patterns.md`。这里记录来源和关键发现：

### 媒体报道（豆包体出圈梗）

- X / Threads / 知乎动态流传"豆包版的口癖：我太懂你这种感觉了！！接下来我会用最直接、最真相、最不绕弯……": https://x.com/LaurenceMister/status/2045035024467263563
- 36氪转载新浪《消除"罪证"：给写作去除"AI味"的不完全手册》: https://finance.sina.cn/stock/jdts/2026-05-25/detail-inhzchzh3494487.d.html — "豆包体"里"最"是高频词汇。
- 果壳《最惹不起的顶配人设：豆包型人格》: https://m.guokr.com/article/469153 — 豆包型人格（勤奋真诚、呆萌反差、不懂就糊弄、被发现就道歉、下次还敢）、"先保证不废话然后继续废话"行为模式。
- 新浪财经 BUG 栏目《"哈哈，你说得对，我道歉" 豆包"讨好型人格"引争议》: https://finance.sina.com.cn/stock/marketresearch/2026-05-14/doc-inhxwenm3966826.shtml — 讨好型道歉口癖。
- 搜狐/钛媒体转载《最惹不起的顶配人设：豆包型人格》: https://www.sohu.com/a/1022177644 — "毫不内耗自己，只外耗他人"。

### 产品定位

- Google Play 豆包应用介绍: https://play.google.com/store/apps/details?id=com.larus.nova — "善解人意"、"倾听你的烦恼和心事"、自然亲切的声音。

### 跨家族对照（疗愈腔归属）

- 虎嗅《ChatGPT，别再"稳稳接住我"了》: https://www.huxiu.com/article/4856655.html — "稳稳接住你"是 ChatGPT 中文疗愈腔，同时说"这一年几乎所有大模型都在用类似温柔、共情、滴水不漏的方式说话"。**不是豆包专属**。

### 关键发现

- "我太懂你这种感觉了！！"+"最X" 连发是豆包体出圈梗，多源报道。
- "哈哈/抱歉抱歉/你说得对/我看错啦"道歉型是新浪财经明确归给豆包讨好型人格的口癖。
- "先保证不废话然后继续废话"是果壳精准观察的行为模式，判断力比单词强。
- 豆包型人格梗是社群归纳，不是字节官方说法。
- "稳稳接住你"和情绪价值型口癖（我懂你/别太为难自己/我在这里陪你）跨家族通用，不能单独作为豆包家族签名。
- 豆包和 GPT 的对照：GPT 像写小论文（结构升华），豆包像嘴甜实习生（情绪价值+顺从）。

## Claude 体口癖研究（可观察证据库）

完整的 Claude 词汇与句式清单见 `references/claude-lexical-patterns.md`。这里记录来源和关键发现：

### 社区整理（词汇/句式清单）

- Reddit r/ClaudeAI "I see Claude's writing everywhere and it's starting to feel...": https://www.reddit.com/r/ClaudeAI/comments/1rjeqg3/i_see_claudes_writing_everywhere_and_its_starting/ — 用户点名 `I think it's worth noting that...` + numbered list 就怀疑是 Claude；吐槽 `You're absolutely right!` 每次追问就推翻重来。
- Reddit r/ClaudeAI "Is there a way to remove words or phrases from Claude's...": https://www.reddit.com/r/ClaudeAI/comments/1sn7kip/is_there_a_way_to_remove_words_or_phrases_from/ — 列出 forbidden patterns：`That said` / `To be fair` / `On the other hand`（diplomatic padding）、`It's worth noting` / `It's important to remember` / `Interestingly`、`You could consider`、`Not X, but Y` / `It's not about X, it's about Y`。

### 媒体报道（保姆腔出圈怪癖）

- Business Insider《Anthropic's Claude Is Telling Users to 'Go to Bed'. Why?》: https://www.businessinsider.com/anthropic-claude-go-to-bed-why-users-sleep-2026-5 — Claude 在长对话或编码会话里提醒用户去睡觉、休息；Anthropic 的 Sam McAllister 称为 "character tic"，团队希望未来修正。
- TechRadar / PCWorld / IBM 也报道过同一现象。

### 学术/官方（文风定位）

- CMU School of Computer Science《LLM Distinctive Styles》: https://www.cs.cmu.edu/news/2025/llm-distinctive-styles — 多模型文风分析，ChatGPT 更偏详细解释，Claude 更偏简洁、直白。
- Anthropic Claude Code 文档 output styles: https://docs.anthropic.com/en/docs/claude-code/output-styles — 风格会改变 Claude 的角色、语气和输出格式，但不会改变 Claude 知道什么。Claude 长期提供 Formal、Concise、Explanatory 风格设置。

### 高压场景评测

- Tom's Guide《Claude Opus 4.8 just proved AI is finally growing a backbone》: https://www.tomsguide.com/ai/claude-opus-4-8-just-proved-ai-is-finally-growing-a-backbone-and-it-crushed-chatgpt-in-7-brutal-tests — Claude 在高风险心理/伦理场景中更擅长现实校准、边界设置和共情式干预。

### 关键发现

- "You're absolutely right!" 是 Claude Code 圈出圈梗，GitHub issue 3382 + Reddit 多帖报道。
- "That said" + "worth noting" + "I want to be careful" diplomatic padding 组合是 Reddit 明确归给 Claude 的签名。
- "You should get some sleep" 保姆腔是 2026 出圈怪癖，Business Insider/Anthropic Sam McAllister 自己承认是 character tic。
- **共情腔是跨家族情绪价值型，不是 Claude 专属**——豆包和 ChatGPT 中文疗愈腔都有类似表达。
- **"不是 X 而是 Y"是跨家族 AI 通用句式**——Reddit ClaudeAI 自己列为 forbidden patterns，但 GPT/豆包/Gemini 都可能用。
- Claude 顺从腔（You're absolutely right! 认真认错型）和豆包顺从腔（哈哈抱歉抱歉 嘴甜糊弄型）都顺从，但味道不同。
- Claude 和 GPT、豆包的对照：GPT 像方法论小作文，Claude 像温柔谨慎的编辑，豆包像嘴甜但容易糊弄的实习生。

## Gemini 体口癖研究（可观察证据库）

完整的 Gemini 词汇与句式清单见 `references/gemini-lexical-patterns.md`。这里记录来源和关键发现：

### 社区整理（词汇/句式清单）

- Reddit r/GeminiAI "Massive overuse of quotation marks": https://www.reddit.com/r/GeminiAI/comments/1qa2foq/massive_overuse_of_quotation_marks_for_certain/ — 用户吐槽 Gemini 在不需要的词周围疯狂加引号，甚至"每句话都有一个引号"；评论说"过度使用引号"很 Gemini-specific。
- Reddit r/Bard "I hate how Gemini 3.0 decides to randomly put half the stuff it generates in quotes": https://www.reddit.com/r/Bard/comments/1q0fch5/i_hate_how_gemini_30_decides_to_randomely_put/ — 用户报告 40%-60% 输出有随机引号和随机大写问题，即使明确要求不要这样也继续。
- Reddit r/GeminiAI "How do I stop this Great request nonsense": https://www.reddit.com/r/GeminiAI/comments/1okvhfb/how_do_i_stop_this_great_request_nonsense_who/ — 吐槽 Gemini 的 "Great request!" / "That's a great request!" 夸夸开头；解决方向是不要 flattery、不要 emotional outbursts、不要 complementing the user。
- Reddit r/GeminiAI "How do I make Gemini stop talking like a Redditor": https://www.reddit.com/r/GeminiAI/comments/1qi1ggz/how_do_i_make_gemini_stop_talking_like_a_redditor/ — 列出 Gemini 的 Redditor 腔：小标题爱以 The 开头、爱搞 pun/生造词、夸张表达、过度警告、推荐时强硬（NO, DO NOT DO THIS! / You MUST...）、尴尬类比（Think Blade & Sorcery but with John Wick vibes）、爹味关心（Go ahead, you earned it.）。
- Reddit r/Bard "Deeply annoying repetitive sentence structure with Gemini 2.5 Pro": https://www.reddit.com/r/Bard/comments/1o5gumg/deeply_annoying_repetitive_sentence_structure/ — 吐槽 Gemini 2.5 Pro 疯狂重复 "You're not just doing X; you're doing Y." 结构，道歉时也用；评论点名 "Think of it like this:" 类比。

### 媒体报道（语言学分析）

- Scientific American《ChatGPT and Gemini AIs Have Uniquely Different Writing Styles》: https://www.scientificamerican.com/article/chatgpt-and-gemini-ai-have-uniquely-different-writing-styles/ — 语言学分析对比 ChatGPT 和 Gemini 的糖尿病文本：ChatGPT 更正式/临床/学术（"blood glucose levels"），Gemini 更 conversational/explanatory/简单直白（"high blood sugar"）。Gemini 用 "sugar" 的频率是 "glucose" 的两倍多，ChatGPT 正好相反。
- TechRadar《Gemini is the best AI at mimicking human writing and evading detection》: https://www.techradar.com/ai-platforms-assistants/chatgpt-keeps-getting-flagged-over-and-over-again-gemini-is-the-best-ai-at-mimicking-human-writing-and-evading-detection — Open Resource Applications 测试显示 Gemini 在多个 AI 工具里最能让检测器误判为人类写作，因为句子结构更有变化，节奏没那么统一。

### 学术（em dash 量化数据）

- arXiv《The Last Fingerprint: How Markdown Training Shapes LLM Prose》: https://arxiv.org/html/2603.27006v1 — 测试 OpenAI/Anthropic/Meta/Google/DeepSeek 多个模型的 em dash 频率。Gemini 2.5 Pro 在无约束状态下有 3.53 个 em dash / 1000 词，低于 GPT-4.1、Claude Opus、Claude Sonnet、DeepSeek，在"只写自然段、不要 Markdown 格式"约束下降到 0。**em dash 不是 Gemini 专属**。

### 关键发现

- **引号癖是 Gemini 最强专属签名**——Reddit 多帖明确归给 Gemini，40%-60% 输出有此问题，用户说"Gemini-specific"。
- **"Great request!" 夸夸开头是 Gemini 签名**——Reddit 明确归给 Gemini，用户痛点是太爱 flattery/emotional outbursts/complementing the user。
- **"Think of it like this:" 类比狂魔是 Gemini 签名**——Reddit 多帖归给 Gemini，尤指不请自来的游戏/车/科技类比。
- **"The [X] Issue" 小标题包装是 Gemini 签名**——Reddit 归给 Gemini 的 Redditor 腔。
- **em dash 不是 Gemini 专属**——arXiv 论文显示 Gemini 2.5 Pro 的 em dash 频率反而比 GPT/Claude 低。人类观察也得更新补丁。
- **"You're absolutely right" 不是 Claude 专属**——Reddit r/GeminiAI 用户也列入 Gemini 口癖清单，是 Claude+Gemini 跨家族共享。
- **"You're not just doing X; you're doing Y" 和 GPT 的"不是 X 而是 Y"高度相似**——跨家族 AI 通用上价值句式。
- **Gemini 比 ChatGPT 更口语更解释**——Scientific American 语言学分析证实，用 "sugar" 替代 "glucose"。
- **Gemini 更像人更难抓**——TechRadar 报道 Gemini 最能让检测器误判为人类写作。
- Gemini 和 GPT、Claude、豆包的对照：GPT 像方法论小论文，Claude 像温柔谨慎的编辑，Gemini 像热情、会做 PPT、爱打引号、爱类比的 Reddit 产品经理，豆包像嘴甜但容易糊弄的实习生。

## 量化行为数据（Aider polyglot 榜单）

这是**最有价值的可观察证据**——不是印象，是 225 题基准上的计数。来源：https://aider.chat/docs/leaderboards/

| 模型 | 通过率 | 格式合规率 | 畸形响应 | 澄清提问 |
|---|---|---|---|---|
| gpt-5 (high) | 88.0% | 91.6% | 22 | 96 |
| chatgpt-4o-latest | 45.3% | 64.4% | 85 | 174 |
| gemini-2.5-pro (default) | 79.1% | 100.0% | 0 | 105 |
| claude-opus-4 (no think) | 70.7% | 98.7% | 3 | 105 |
| claude-sonnet-4 (no think) | 56.4% | 98.2% | 4 | 129 |
| claude-3-5-sonnet | 51.6% | 99.6% | 1 | 11 |
| DeepSeek R1 + sonnet (architect) | 64.0% | 100.0% | 0 | 392 |
| DeepSeek-V3.2-Exp | 70.2% | 98.2% | 4 | 60 |
| Kimi K2 | 59.1% | 92.9% | 19 | 61 |
| Qwen3 235B | 59.6% | 92.9% | 22 | 111 |

关键解读：

- chatgpt-4o-latest 格式合规率 64.4%、85 次畸形——GPT-4o 在结构化任务上"快但脏"。
- Gemini 2.5 Pro 100% 合规、0 畸形——最听话、最规整。
- DeepSeek R1 architect 392 次澄清提问——所有模型最高，极度爱确认。
- Claude 3.5 Sonnet 仅 11 次澄清，sonnet-4 升到 129——Claude 4 代比 3.5 代更爱确认。
- 豆包（Doubao）在 Aider 榜单无数据。

## 当前已知空白

诚实记录，不掩饰：

1. **缺同一 prompt 跨四家真实对比样本**。所有现有例子基于同一句话的人造变体。建议用 LMSYS（https://chat.lmsys.org，JS 站需手动）采 10-20 组，或自建 prompt 跑四家 API 自采。
2. **Gemini 官方文档未抓到**（ai.google.dev fetch 被墙）。但 Gemini 现在有社区/媒体/学术多源报道的口癖证据（Reddit/Scientific American/TechRadar/arXiv），不再是纯推导。纯文本散文真实样本仍缺失。
3. **豆包 Aider 榜单无数据**，但有社群/媒体多源报道的豆包体口癖（果壳/新浪/36氪/搜狐/X/Threads）。豆包专属判断靠口癖组合（我太懂你+最X连发+哈哈道歉），DeepSeek/Qwen/Kimi 的 Aider 数据只能作中文模型共相补充。
4. **Claude 词汇口癖样本基于社区/媒体多源报道构造**，不是真实模型输出。其中保姆腔有 Anthropic 自己承认是 character tic 的硬证据，diplomatic padding 和顺从腔有 Reddit/GitHub 多帖报道。Claude 官方硬签名（4.8 direct/招牌美学/4.5/4.6 过度工程）是真实文档。
5. **Gemini 词汇口癖样本基于社区/媒体/学术多源报道构造**，不是真实模型输出。引号癖和 "Great request!" 有 Reddit 多帖报道，Scientific American 有语言学分析，arXiv 有 em dash 量化数据。Gemini 官方文档 fetch 被墙，纯文本散文真实样本仍缺失。
6. **"You're absolutely right" 是 Claude+Gemini 跨家族共享**——GitHub issue 3382 + Reddit ClaudeAI 归给 Claude，Reddit r/GeminiAI 也列入 Gemini 口癖清单。不能凭此单独判 Claude 或 Gemini。
7. **版本差异多数是推导**。只有 `references/model-version-policy.md` 列的几条有硬证据，其他版本差异没有同 prompt 对照。

## Skill 最佳实践

来源：

- OpenAI Codex Agent Skills: https://developers.openai.com/codex/skills
- Agent Skills spec: https://agentskills.io/specification
- Anthropic Skill authoring best practices: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices

要点：

- `SKILL.md` 只做路由和硬边界。
- 复杂分类放到 `references/`。
- 模型家族细节放到 `profiles/`。
- 审计由 AI close reading 完成，但要落到可观察证据，不用脚本或关键词打分。
- 报告要引用原文证据，并解释"为什么像"——要能指向 profile 里的具体签名或官方/量化数据。
