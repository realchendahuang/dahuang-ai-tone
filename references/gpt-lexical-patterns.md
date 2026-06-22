# GPT / ChatGPT 词汇与句式可观察清单

> 这是一份**清单 + 来源**，不是结论。审计员据此找可观察证据，但必须遵守文末的"审计指引"——很多口癖是跨家族 AI 通用，不能凭单个词判 GPT。

## 目录

- [一、英文高频词口癖](#一英文高频词口癖)
- [二、英文社区吐槽里的 ChatGPT 口癖](#二英文社区吐槽里的-chatgpt-口癖)
- [三、英文句式口癖](#三英文句式口癖)
- [四、中文 GPT / ChatGPT 口癖](#四中文-gpt--chatgpt-口癖)
- [五、中文结构口癖](#五中文结构口癖)
- [六、中文"正确废话"表达](#六中文正确废话表达)
- [七、格式口癖](#七格式口癖)
- [八、GPT-4 / GPT-4o / GPT-5 时代词汇差异](#八gpt-4--gpt-4o--gpt-5-时代词汇差异)
- [审计指引（使用说明）](#审计指引使用说明)

## 一、英文高频词口癖

论文和社区里反复出现的 ChatGPT / LLM 高频词：

```txt
delve
intricate
underscore
pivotal
crucial
meticulous
realm
landscape
tapestry
robust
foster / fostering
garner
highlight
emphasize / emphasizing
showcase / showcasing
bolster / bolstered
enduring
interplay
valuable
vibrant
```

- Kobak et al. 统计 2010-2024 年 1500 多万篇 PubMed 摘要，发现 LLM 出现后某些"风格词"突然上升，估计 2024 年至少 13.5% 的生物医学摘要经过 LLM 处理；论文题目本身用了 `Delving into...`。来源：https://arxiv.org/abs/2406.07016
- 多数据库研究追踪 12 个 LLM 相关词：2022-2024 年 `delve` 增长约 1500%，`underscore` 约 1000%，`intricate` 约 700%；PMC 全文里 `underscore` 高频使用比例从 2022 到 2025 增长超 10000%。来源：https://arxiv.org/abs/2509.09596
- Juzek & Ward《Why Does ChatGPT Delve So Much?》识别出 21 个很可能与 LLM 使用有关的 focal words。来源：https://arxiv.org/abs/2412.11385
- Wikipedia 社群整理的 "Words to watch"：`additionally`、`boasts`、`bolstered`、`crucial`、`delve`、`emphasizing`、`enduring`、`enhance`、`fostering`、`garner`、`highlight`、`interplay`、`intricate`、`landscape`、`meticulous`、`pivotal`、`robust`、`showcase`、`tapestry`、`testament`、`underscore`、`valuable`、`vibrant`。来源：https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing
- The Verge 引用 Max Planck Institute 研究：ChatGPT 偏好的 `meticulous`、`delve`、`realm`、`adept` 等词，在 ChatGPT 发布后 18 个月里，学术 YouTube 视频使用频率最高增加到 51%。来源：https://www.theverge.com/openai/686748/chatgpt-linguistic-impact-common-word-usage
- TechRadar 报道 FSU 研究：`garner`、`delve`、`intricate`、`underscore`、`meticulous`、`strategically`、`surpass`、`boast`；人们更倾向说 `underscore` 而不是 `accentuate`，说 `delve` 而不是 `explore`。来源：https://www.techradar.com/ai-platforms-assistants/chatgpt/chatgpt-has-hijacked-our-real-world-conversations

## 二、英文社区吐槽里的 ChatGPT 口癖

Reddit r/ChatGPTPro 用户整理帖及后续补充：

```txt
It's important to note
Delve into
Tapestry
Bustling
In summary
In conclusion
Remember that
Take a dive into
Navigating the landscape
Navigating the complexities of
The landscape of
A testament to
In the world of
Realm
Embark
It depends on
That being said
You may want to
It's worth noting that
This is not an exhaustive list
You could consider
On the other hand
As previously mentioned
Ultimately
To put it simply
Dive into
In today's digital era
Reverberate
meticulous
navigating
complexities
ever-evolving
game changer
designed to enhance
daunting
when it comes to
in the realm of
unlock the secrets
unveil the secrets
robust
elevate
unleash
cutting-edge
rapidly expanding
harness
crucial
essential
ensure
furthermore
therefore
additionally
notably
```

帖子里还特别吐槽 ChatGPT 写标题和列表喜欢到处用冒号（`X: Y` 格式）。来源：https://www.reddit.com/r/ChatGPTPro/comments/163ndbh/overused_chatgpt_terms_add_to_my_list/

## 三、英文句式口癖

### 1. not only... but also...（Negative parallelisms）

```txt
not only X, but also Y
not just X, but also Y
doesn't just X; it Y
```

Wikipedia 把这类叫 "Negative parallelisms"，LLM 常使用包含 `not`、`but`、`however` 的平行结构。来源：https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing

### 2. not X, but Y

```txt
It's not X, it's Y
not X, but Y
no X, no Y, just Z
```

Wikipedia 单列 `Not X, but Y`：先否定一个表层判断，再给出"更高级"的定义。来源：同上。

### 3. Rule of three

```txt
adjective, adjective, adjective
short phrase, short phrase, and short phrase
```

Wikipedia 把 "rule of three" 列为 LLM 过度使用的结构，用三个形容词或三个短语制造"更全面"的表面分析感。来源：同上。

### 4. 免责声明句式（didactic disclaimers）

```txt
It's important to note that...
It's crucial to remember that...
It's worth noting that...
This may vary...
Keep in mind that...
```

Wikipedia 指出 2022-2024 年左右的旧 LLM 经常加入 `important to note` 这类提醒式免责声明。来源：同上。

### 5. 总结收束句式（section summaries）

```txt
In summary
In conclusion
Overall
To summarize
Ultimately
```

Wikipedia 指出旧 LLM 在长输出里经常添加 `Conclusion` 标题，并用这些词收束段落或章节。来源：同上。

## 四、中文 GPT / ChatGPT 口癖

### 中文句式

```txt
不是 X，而是 Y
这不是 X，而是 Y
不只是 X，更是 Y
表面上是 X，本质上是 Y
真正重要的不是 X，而是 Y
这背后反映的是 X
这件事的核心在于 X
从 X 到 Y
重新审视 X
```

- Threads 多条帖子讨论"不是……而是……"已成 ChatGPT/AI 腔标志，"常被用在很有道理、但没有人站在里面说话的位置"。来源：https://www.threads.com/@an.son1625/post/DSUy0QYkyvx
- Threads 帖子直接吐槽"AI 腔爱讲「不是...而是...」"。来源：https://www.threads.com/@b.alive.is.good/post/DLtgatMy4O5
- Threads 用户"看腻了『不是...而是』句型吗"。来源：https://www.threads.com/@peter_career_hack/post/DOaujRTDbWv
- Facebook 用户吐槽到处都是 AI 生成的"这不是 A，而是 B"句型。来源：https://www.facebook.com/grayhawklit/posts/10161712179451732
- WIRED 2026 年文章点名 ChatGPT 爱用 "it's not A; it's B" 结构。来源：https://www.wired.com/story/chatgpt-chinese-catch-you-steadily-sycophancy

### 中文翻译腔 / 本地化怪口癖（ChatGPT 专属，WIRED 报道）

```txt
我会稳稳地接住你
```

WIRED：来自 "I've got you" 的安抚语，中文里显得过分亲密、过分心理咨询化，已在中文互联网上变成梗。来源：https://www.wired.com/story/chatgpt-chinese-catch-you-steadily-sycophancy

```txt
砍一刀
```

WIRED：中文社交媒体讨论 ChatGPT 爱说"砍一刀"，和拼多多/Temu 营销语有关。来源：同上。

WIRED 还写到 ChatGPT 中文回答常有英语影响：句子更长，结构更不必要；中文学术研究称 ChatGPT 中文回答的某些语言属性更接近英语写法。来源：同上。

### 中文官话腔词汇

科学网文章把"AI 味"描述成文本的"工业化痕迹"：措辞过于标准、情感过于克制、逻辑过于工整、内容过于全面。点名的中文官样词：

```txt
此外
而且
值得注意的是
```

来源：https://news.sciencenet.cn/htmlnews/2025/10/553334.shtm

同类表达：

```txt
需要注意的是
从某种意义上说
进一步来看
整体来看
总的来说
归根结底
本质上
核心在于
关键在于
值得一提的是
不可忽视的是
```

`需要注意的是 / 值得注意的是` 对应英文 `It's important to note / It's worth noting`，是"安全垫 + 提醒式废话"的中文版本。

## 五、中文结构口癖

```txt
首先
其次
最后
第一
第二
第三
一方面
另一方面
与此同时
此外
因此
由此可见
综上所述
总而言之
```

科学网：`首先…其次…最后…` 几乎成了 AI 标配。对应英文 `Firstly / Secondly / Lastly / Furthermore / Therefore / In conclusion`。来源：https://news.sciencenet.cn/htmlnews/2025/10/553334.shtm

## 六、中文"正确废话"表达

```txt
这为我们提供了一个重新审视 X 的契机
这不仅提升了效率，也降低了门槛
这有助于构建更加完善的 X 体系
这体现了 X 在 Y 场景下的重要价值
这将进一步推动 X 的发展
这背后是 X、Y、Z 多重因素共同作用的结果
```

科学网称这种现象为"正确的废话"：面面俱到却浅尝辄止。对应 Wikipedia 的 superficial analyses：`highlighting`、`underscoring`、`reflecting`、`symbolizing` 常用于制造表面分析感。

## 七、格式口癖

Wikipedia 列的格式层特征：

```txt
过度使用 Markdown
过度使用粗体
过度使用竖向列表
过度使用 em dash
不自然的小标题
跳级标题
不寻常地使用表格
```

Reddit 用户吐槽 ChatGPT 写标题和 bullet list 喜欢到处放冒号（`X: Y`）。

来源：https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing 、https://www.reddit.com/r/ChatGPTPro/comments/163ndbh/overused_chatgpt_terms_add_to_my_list/

## 八、GPT-4 / GPT-4o / GPT-5 时代词汇差异

Wikipedia 社群整理的不同阶段 AI vocabulary（提醒：不是硬切分，具体分布会随模型和时间变化）：

```txt
2023 到 2024 中期，GPT-4 时代：
Additionally
boasts
bolstered
crucial
delve
emphasizing
enduring
garner
intricate / intricacies
interplay
key
landscape
meticulous / meticulously
pivotal
underscore
tapestry
testament
valuable
vibrant
```

```txt
2024 中期到 2025 中期，GPT-4o 时代：
align with
bolstered
crucial
emphasizing
enhance
enduring
fostering
highlighting
pivotal
showcasing
underscore
vibrant
```

```txt
2025 中期以后，GPT-5 时代：
emphasizing
enhance
highlighting
showcasing
```

来源：https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing

---

## 审计指引（使用说明）

这份清单是**可观察证据库**，但使用时必须遵守以下规则，否则会制造误判：

### 1. 跨家族通用 vs GPT 专属

**大多数英文高频词（delve/tapestry/landscape/underscore/intricate/pivotal/crucial/meticulous/robust/foster/garner/highlight/emphasize/showcase/bolster/enduring/interplay/valuable/vibrant）是跨家族 AI 通用口癖，不是 GPT 专属。** Claude、Gemini、中文模型都可能用。不能凭单个词判 GPT。

**GPT/ChatGPT 专属（可作为家族签名）**：
- 中文"我会稳稳地接住你""砍一刀"——WIRED 报道的 ChatGPT 中文本地化口癖。
- 冒号滥用（`X: Y` 到处用）——Reddit 吐槽的 ChatGPT 格式癖。

### 2. 单个词不能定家族

口癖的判断力在**密度和组合**，不在单个词。一段文本里同时出现 delve + tapestry + landscape + navigating the complexities + rule of three + not only but also，比只出现一个 delve 的判断力强得多。

### 3. 句式比单词更有判断力

`not X but Y`、`not only... but also...`、rule of three、didactic disclaimers、section summaries 这些**句式**比单个词更有判断力，因为它们是组织方式，不是词汇选择。

### 4. 时代词汇变迁是版本半硬证据

GPT-4/4o/5 时代的词汇差异（Wikipedia 社群整理）可以作为**版本判断的半硬证据**——不是官方明文，但有社群数据支撑。如果文本高频用 `delve/tapestry/testament`，偏 GPT-4 时代；高频用 `align with/fostering/showcasing`，偏 GPT-4o 时代；只剩 `emphasizing/enhance/highlighting/showcasing`，偏 GPT-5 时代。但要标低置信度，因为 Wikipedia 提醒"不是硬切分"。

### 5. 中文口癖的判断力

中文"不是 X 而是 Y"是跨家族 AI 通用句式（Threads/Facebook/WIRED 都在吐槽，但没说是 GPT 专属）——不能凭它判 GPT。但"我会稳稳地接住你""砍一刀"是 WIRED 明确报道的 ChatGPT 中文口癖，可以作为 GPT 家族签名。

### 6. 格式口癖

过度 markdown/粗体/竖向列表/em dash/跳级标题/冒号滥用——这些是 AI 通用格式癖，不区分家族，但 GPT 家族（尤其 ChatGPT 产品表面）高频。o-series 例外：默认无 markdown（见 `references/model-version-policy.md`）。

### 7. 反误判

- 不能凭"delve"就判 GPT——任何 AI 都可能用。
- 不能凭"不是 X 而是 Y"就判 GPT——中文模型、Claude、Gemini 都可能用。
- 学术英语本来就用 delve/underscore/intricate，人类学者也会用，不能凭这些词判 AI。
- 翻译腔和这些口癖重叠——非母语写作也可能用高频通用词，见 `references/research.md` 的 arxiv 2304.02819。
