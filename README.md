# Dahuang AI Tone

> 判断一段文字像 GPT、Claude、Gemini 还是豆包的腔调——靠可观察证据，不靠印象。

## 这是什么

`dahuang-ai-tone` 是一个 Agent Skill，给 AI 编码助手装上"模型腔调审计"能力。

它做两件事：

1. **审计**——给定一段文本，判断它更像哪个模型家族（GPT/o-series、Claude、Gemini、豆包）的风格，能区分到版本档位和产品表面，每条判断都落到可观察证据（具体词、句式、段落组织、行为模式），而不是"感觉像"。
2. **加味**——按指定模型家族/版本把文本改得更像那个模型，改的是结构、语气、行为模式，不是堆口癖。

## 为什么需要它

市面上 AI 检测器大多只回答"这是不是 AI 写的"——这在学术上叫 detection，可靠性有限，改写和翻译就能绕过。

这个 skill 做的是另一件事：**characterization**（风格表征）。不判断"是不是 AI 写的"，而是判断"如果是 AI 写的，它更像哪个家族的腔调"。学术上 Source Family Classification 已被证明可行（见 `references/research.md`）。

它的核心纪律：

- **只能说"风格相似"，不能说"就是某模型生成"**。
- **判断必须落到可观察证据**——具体词、句式、段落组织、行为模式，能数、能指、能引用，不靠印象。
- **版本差异只列有硬证据的**（官方明文或量化数据），其他标推导。
- **区分模型家族、具体版本、产品表面**——Perplexity 不是基础模型家族，是检索增强回答产品表面。
- **主动标注跨家族通用口癖**——delve/tapestry 不是 GPT 专属，em dash 不是 Gemini 专属，"You're absolutely right" 是 Claude+Gemini 共享，不能凭单个词判家族。

## 能做什么

| 能力 | 说明 |
|---|---|
| 家族审计 | 判断文本更像 GPT/Claude/Gemini/豆包哪个家族，输出引用原文的证据报告 |
| 版本判断 | 区分有硬证据的版本（o-series 无 markdown、Claude 4.8 direct、chatgpt-4o 格式脏、Gemini 100% 合规）和推导 |
| 产品表面识别 | 识别 ChatGPT、Claude.ai、Perplexity 式检索回答、编程助手等产品表面 |
| 反误判 | 主动标注翻译腔、人工模板、谨慎人类写作等误伤风险 |
| 跨家族对比 | 量化行为数据（Aider polyglot 榜单）+ 推导对比矩阵 |
| 加模型腔 | 按指定家族/版本改写文本，改结构不改口癖，自带"删标志词后还像不像"自检 |

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

### 审计

```
Use $dahuang-ai-tone 审计下面这段文字更像哪个模型家族，注意区分版本和产品表面，证据要落到可观察形式：

<贴文本>
```

### 加味

```
Use $dahuang-ai-tone 把下面这段改成 Claude Opus 4.8 风格，不要堆"可能/取决于"，要改开场和收尾的组织方式：

<贴文本>
```

### 跨家族对比

```
Use $dahuang-ai-tone 对比下面两段文字的模型腔调差异，说明它们分别像哪个家族：
```

## 内置模型家族

| 家族 | Profile | 词汇句式清单 |
|---|---|---|
| OpenAI GPT / o-series | `profiles/openai-gpt-family.md` | `references/gpt-lexical-patterns.md` |
| Anthropic Claude | `profiles/anthropic-claude-family.md` | `references/claude-lexical-patterns.md` |
| Google Gemini | `profiles/google-gemini-family.md` | `references/gemini-lexical-patterns.md` |
| 字节豆包 / Doubao | `profiles/bytedance-doubao-family.md` | `references/doubao-lexical-patterns.md` |

DeepSeek、Grok、Kimi、Qwen 等暂不做默认 profile，用户明确要求时临时扩展。

## 诚实声明

这个 skill 不是万能的，以下空白如实告知：

1. **缺同一 prompt 跨四家真实对比样本**——"同义不同写"的对比都是推导。
2. **Gemini 官方文档 fetch 被墙**，纯文本散文真实样本缺失（有社区/媒体/学术多源口癖证据补足）。
3. **豆包专属硬特征缺失**——用 DeepSeek/Qwen/Kimi 作中文模型代理，只能给"中文模型共相"。
4. **多数版本差异是推导**——只有 `references/model-version-policy.md` 列的几条有硬证据。

详细空白说明见 `references/research.md`。

## 仓库结构

```
dahuang-ai-tone/
├── SKILL.md                  # 入口：路由 + 硬边界 + 工作流
├── references/               # 按需加载的详细文档
│   ├── model-version-policy.md
│   ├── audit-workflow.md
│   ├── taxonomy.md
│   ├── anti-misjudgment.md
│   ├── report-schema.md
│   ├── reverse-humanizer.md
│   ├── evaluation.md
│   ├── research.md
│   └── *-lexical-patterns.md
├── profiles/                 # 模型家族 profile
├── examples/                 # 示范报告
└── agents/openai.yaml        # UI 元数据
```
