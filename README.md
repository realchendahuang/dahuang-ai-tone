# Dahuang AI Tone

> AI 味是梗。这里是四大模型家族的味标本馆——加味、认味、玩味。

## 这是什么

`dahuang-ai-tone` 是一个 Agent Skill，给 AI 编码助手装上"AI 味"的玩梗能力。

它做两件事：

1. **加味**（主）——把正常文本改成某个模型家族的纯味。改的是结构、语气、行为模式，不是堆口癖。
2. **找味**（次）——指出一段文本里的 AI 味在哪、像哪个家族。

为什么需要它：**知道了什么是 AI 味，才能在别处去掉 AI 味**。但去 AI 味不是这个 skill 的事——这个 skill 只负责把 AI 味玩明白。不同模型家族有不同的 AI 味，这里是它们的特征标本馆。

## 四大模型家族的味

| 家族 | 一句话闻味 |
|---|---|
| OpenAI GPT / o-series | 像方法论小作文——结论先行、分点升华、温情诗化 |
| Anthropic Claude | 像温柔谨慎的编辑——克制、边界感、That said、劝你睡觉 |
| Google Gemini | 像热情的解释型辅导老师——引号癖、夸夸开头、Think of it like this |
| 字节豆包 / Doubao | 像嘴甜但容易糊弄的实习生——我太懂你、最X连发、哈哈抱歉抱歉 |

每个家族的完整味签名见 `profiles/`，词汇句式味标本见 `references/*-lexical-patterns.md`。

## 玩梗纪律

- **只能说"风格相似"，不能说"就是某模型生成"**——这是玩梗认味，不是来源鉴定。
- **判断落到可观察的东西**——具体词、句式、段落组织、行为模式，能指能引用，不靠印象。
- **跨家族通用口癖不能单独判家族**——`delve`/`tapestry` 不是 GPT 专属，em dash 不是 Gemini 专属，"You're absolutely right" 是 Claude+Gemini 共享，"不是 X 而是 Y" 是跨家族通用句式。判断力在密度和组合。
- **加味改结构不堆口癖**——把加的标志词删掉，还像那个家族才算加成了味，否则只是塞词。

## 安装

### 方式一：skills CLI（推荐）

```bash
npx skills add realchendahuang/dahuang-ai-tone-skill -g
```

`-g` 安装到全局（用户级），所有项目可用。去掉 `-g` 则只装到当前项目。

安装后重启 Codex / Claude Code 即可生效。

### 方式二：手动复制

```bash
# Codex
cp -r dahuang-ai-tone ~/.codex/skills/

# Claude Code
cp -r dahuang-ai-tone ~/.claude/skills/
```

或者把本目录作为资源目录，在 system prompt 里引用 `SKILL.md` 路径。

## 使用

### 加味

```
Use $dahuang-ai-tone 把下面这段改成 Claude 腔，不要堆"可能/取决于"，要改开场和收尾的组织方式：

<贴文本>
```

```
Use $dahuang-ai-tone 给这段加豆包味，要最X连发那种：

<贴文本>
```

### 找味

```
Use $dahuang-ai-tone 看看下面这段的 AI 味在哪、像哪个家族：

<贴文本>
```

### 跨家族对比

```
Use $dahuang-ai-tone 对比下面两段文字的模型腔调差异，说明它们分别像哪个家族：
```

## 仓库结构

```
dahuang-ai-tone/
├── SKILL.md                  # 入口：玩梗定位 + 加味/找味工作流
├── references/               # 按需加载的详细文档
│   ├── reverse-humanizer.md  # 加味主方法 + 自检规则
│   └── *-lexical-patterns.md # 四大家族词汇句式味标本
├── profiles/                 # 四大模型家族 profile（味签名 + 加味方法）
├── examples/                 # 加味示范、找味示范、跨家族对比、真实味标本
└── agents/openai.yaml        # Codex 专属 UI 元数据（可选）
```
