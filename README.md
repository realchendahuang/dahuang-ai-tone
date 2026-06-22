# Dahuang AI Tone

> AI 味是梗。把文本加成 GPT/Claude/Gemini/豆包的味，或者看一段文本最像哪个模型写的。

## 它能做什么

这个 skill 给 AI 编码助手装上两种能力：

1. **加味**（主）——把一段普通文本改写成某个 AI 模型的风格。改的是句子组织、语气、行为模式，不是堆口癖。
   - 想让一段文字读起来像 Claude 写的、像 GPT 写的、像豆包写的？贴进来，指定模型，就行。
   - 也可以指定版本：Claude 4.8 的直球味、Claude 3.x 的谨慎味、o-series 的无 markdown 味，等等。
2. **找味**（次）——指出一段文本里的 AI 味在哪、最像哪个模型风格。
   - 贴一段文本，它会按原文顺序逐处指出 AI 味，并说明它像哪个模型的什么特征。

**为什么有它**：知道了什么是 AI 味，才能在别处去掉 AI 味。但去 AI 味不是这个 skill 的事——这个 skill 只负责把 AI 味玩明白。

## 看看效果

同一段原文，加不同模型的味：

> **原文**：这个功能别急着上。用户还没说清楚自己要什么，我们先做会浪费时间。

**加 Claude 4.8 味**（直球、不啰嗦）：
> 不建议直接上线。用户需求还没说清楚，先做 3-5 个访谈能更快判断真实优先级，也能避免返工。

**加 Claude 3.x 味**（hedging、温和可商量）：
> 我会倾向于先不要急着上线这个功能。但这不一定意味着功能本身没有价值，而是说在用户需求还没有被充分说清楚的情况下，直接进入开发可能会带来额外的返工成本。更稳妥的做法，是先明确用户真正想解决的问题。

**加 o-series 味**（无 markdown、先问再做）：
> 用户需求未明确，直接上线风险高。建议先确认几个问题：目标用户是谁、核心场景是什么、现有流程里这个功能解决哪个痛点。确认后再决定是否排期。

完整示范见 `examples/injection-report.md`。

## 四大模型风格

每个风格有自己的味签名。想尝味，读对应风格的 profile + 词汇句式清单。

| 风格 | 一句话闻味 |
|---|---|
| OpenAI GPT / o-series | 像方法论小作文——结论先行、分点升华、温情诗化 |
| Anthropic Claude | 像温柔谨慎的编辑——克制、边界感、That said、劝你睡觉 |
| Google Gemini | 像热情的解释型辅导老师——引号癖、夸夸开头、Think of it like this |
| 字节豆包 / Doubao | 像嘴甜但容易糊弄的实习生——我太懂你、最X连发、哈哈抱歉抱歉 |

DeepSeek、Grok、Kimi、Qwen 等暂不做默认 profile，明确要求时可以临时扩展。

## 安装

### 方式一：skills CLI（推荐）

```bash
npx skills add realchendahuang/dahuang-ai-tone-skill -g
```

`-g` 安装到全局（用户级），所有项目可用。去掉 `-g` 则只装到当前项目。安装后重启 Codex / Claude Code 即可生效。

### 方式二：手动复制

```bash
# Codex
cp -r dahuang-ai-tone ~/.codex/skills/

# Claude Code
cp -r dahuang-ai-tone ~/.claude/skills/
```

或者把本目录作为资源目录，在 system prompt 里引用 `SKILL.md` 路径。

## 使用

### 加味：把文本改成某个模型风格

```
Use $dahuang-ai-tone 把下面这段改成 Claude 腔，不要堆"可能/取决于"，要改开场和收尾的组织方式：

<贴文本>
```

```
Use $dahuang-ai-tone 给这段加豆包味，要最X连发那种：

<贴文本>
```

```
Use $dahuang-ai-tone 把这段改成 o-series 味，不要 markdown，开头先问一个澄清问题：

<贴文本>
```

### 找味：看一段文本的 AI 味在哪、像哪个模型

```
Use $dahuang-ai-tone 看看下面这段的 AI 味在哪、像哪个风格：

<贴文本>
```

### 跨风格对比

```
Use $dahuang-ai-tone 对比下面两段文字的模型腔调差异，说明它们分别像哪个风格：
```

更多示范见 `examples/`：

- `injection-report.md`——同一段原文加成不同风格的味
- `audit-report.md`——逐处指出 AI 味在哪
- `comparison.md`——四大风格对比矩阵
- `fixtures.md`——真实味标本（官方/Aider/学术来源）

## 仓库结构

```
dahuang-ai-tone/
├── SKILL.md                  # 入口：加味/找味工作流（给模型读）
├── references/               # 按需加载的详细文档
│   ├── reverse-humanizer.md  # 加味主方法 + 自检规则
│   └── *-lexical-patterns.md # 四大风格词汇句式味标本
├── profiles/                 # 四大模型风格 profile（味签名 + 加味方法）
├── examples/                 # 加味示范、找味示范、跨风格对比、真实味标本
└── agents/openai.yaml        # Codex 专属 UI 元数据（可选）
```
