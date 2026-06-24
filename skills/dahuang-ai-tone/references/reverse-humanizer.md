# 加味方法

## 核心思路

"加模型腔"不是堆口癖，而是改变回答表面：结构、语气、边界感、推理呈现、行为模式。

**加味绝不等于堆标志词**。如果你加 Claude 味只是把"可能/取决于"塞进去，加出来的只是"AI 通用腔"，不是 Claude 味。加豆包味不能只塞"你可以先……再……"。加味要改的是整体组织方式。

改写前先确定目标：

1. 模型风格：GPT / o-series / Claude / Gemini / 豆包。
2. 版本味（可选）：如果用户指定 Sonnet 4.8、Opus 4.6、o-series、Flash 等，就按对应版本的味调整——见各风格 profile 的"版本味差异"。
3. 产品表面（可选）：如果用户指定 ChatGPT、Claude.ai、豆包 App 等产品表面，可加入产品痕迹。

## 风格级加味方向

各风格的详细加味方法（签名 + 句式 + 版本味 + 避免项）在对应 profile 的"加味方法"章节：

- **GPT / o-series**：`profiles/openai-gpt-style.md`
- **Claude**：`profiles/anthropic-claude-style.md`
- **Gemini**：`profiles/google-gemini-style.md`
- **豆包**：`profiles/bytedance-doubao-style.md`

加味时读对应 profile 的"加味方法"，不要凭印象堆词。

**通用 AI 味原料**：如果只要加"AI 通用腔"（不指向特定模型），见 `references/common-ai-patterns.md`——那是跨风格通用 AI 味的完整清单。注意：通用口癖加了只增加"AI 味"，不增加某模型专属味。

## 交付格式

```md
## 改写后

{文本}

## 我加的模型腔

1. {结构变化——具体改了什么组织方式}
2. {语气/行为变化——具体改了开场/收尾/hedging 密度}
3. {版本味/产品表面变化——引用了哪个签名}

## 边界

这是风格模拟，不代表由该模型生成，也不能判断具体版本。
```

## 自检：加味有没有变成堆口癖？

改写完自检：

- 我加的是整体结构/行为模式，还是只是塞了几个标志词？
- 如果把加的标志词删掉，文本还像那个风格吗？如果不像，说明我加的是口癖不是腔调，要重做。
- 我有没有堆跨风格通用口癖（delve/tapestry、"不是 X 而是 Y"、共情腔、em dash、三段式）当某模型专属味？这些是通用 AI 味，堆了不像某模型专属，反而像"AI 通用腔"。见 `references/common-ai-patterns.md`。
- 各风格的专属 vs 通用边界，见对应 lexical-patterns 文件末尾的"认味指引"。
