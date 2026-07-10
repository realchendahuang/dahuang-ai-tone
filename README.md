# Dahuang AI Tone

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skill Version](https://img.shields.io/badge/Skill-v4.0.0-111827.svg)](CHANGELOG.md)
[![Language](https://img.shields.io/badge/Language-中文写作-e11d48.svg)](skills/dahuang-ai-tone/SKILL.md)

> 模拟或分析 GPT、Claude、Gemini、豆包等模型家族的可观察写作风格。它做的是风格实验，不是来源鉴定。

\`\`\`bash
npx skills add realchendahuang/dahuang-ai-tone -g
\`\`\`

## 两种核心能力

1. **加味**：把普通文本改成某个模型家族、历史版本快照或产品表面。
2. **找味**：指出文本里的通用 AI 模式和家族级相似方向，同时给出竞争解释。

还可以把同一段内容改成多个家族风格，做横向对比。

## 为什么要分三层

模型输出不是固定人格。它至少同时受三层影响：

| 层次 | 说明 |
|---|---|
| 家族风格 | 跨多个样本反复出现的组织、语气和互动倾向 |
| 版本快照 | 某个具体模型、日期或官方样本的表现，会漂移 |
| 产品表面 | ChatGPT、API、Claude.ai、App、系统提示、格式设置和后处理 |

例如，某些 reasoning API 会在特定配置下避免 Markdown。这是产品和配置表面，不能仅凭一段纯文本反推出 OpenAI 家族。

## 当前覆盖

| 家族 | 主要模拟方向 |
|---|---|
| OpenAI GPT / reasoning | 结论与执行结构、方法化组织、任务表面 |
| Anthropic Claude | 边界、不确定性、协商或直接判断 |
| Google Gemini | 解释型语气、类比、概念引号和规整分层 |
| 字节豆包 / Doubao | 高密度共情、最高级承诺、口语纠错和步骤建议 |

DeepSeek、Grok、Kimi、Qwen 等没有默认 Profile。用户明确要求时，应基于当前样本临时扩展，不凭印象硬套。

## 加味示例

原文：

> 这个功能别急着上。用户还没说清楚自己要什么，我们先做会浪费时间。

Claude 家族近似：

> 不建议现在上线。需求还没有被用户说清楚，直接开发大概率会返工。
>
> 先做几次访谈，确认目标用户、核心场景和现有流程里的真实阻力。答案稳定以后，再决定要不要排期。

Gemini 家族近似：

> 先别急着上线。现在做这个功能，有点像地基还没确认就开始盖房子：不是一定会倒，但返工概率很高。
>
> 先确认目标用户、核心场景和现有阻力，再决定路线。

更多示例见 [加味示范](skills/dahuang-ai-tone/examples/injection-report.md) 和 [家族对比](skills/dahuang-ai-tone/examples/comparison.md)。

## 证据纪律

- 单个口癖、Markdown、emoji、列表或破折号不能区分模型。
- 至少组合两个不同类别的特征，再给家族级相似判断。
- 每次找味都要考虑提示词、翻译、体裁、人工编辑或产品表面等竞争解释。
- 普通未知文本最高给中等相似度。
- 具体版本默认不猜；需要版本模拟时先核对当前官方资料。
- 不使用百分比或“硬签名”制造伪精确。

完整规则见 [风格证据与时效策略](skills/dahuang-ai-tone/references/evidence-policy.md)。

## 使用

模拟家族风格：

\`\`\`text
Use $dahuang-ai-tone 把下面这段改成 Claude 家族风格。保留事实，重点改开场、边界和收尾：

<粘贴文本>
\`\`\`

分析 AI 味：

\`\`\`text
Use $dahuang-ai-tone 看看下面这段有哪些通用 AI 模式、与哪个模型家族更相似。必须给竞争解释，不做来源鉴定：

<粘贴文本>
\`\`\`

做横向对比：

\`\`\`text
Use $dahuang-ai-tone 把同一段内容分别改成 GPT、Claude、Gemini 和豆包风格，并说明组织方式的差异：

<粘贴文本>
\`\`\`

## 安装

### skills CLI

\`\`\`bash
# 全局安装
npx skills add realchendahuang/dahuang-ai-tone -g

# 当前项目安装
npx skills add realchendahuang/dahuang-ai-tone
\`\`\`

### 手动安装

\`\`\`bash
git clone https://github.com/realchendahuang/dahuang-ai-tone.git

# Codex
cp -r dahuang-ai-tone/skills/dahuang-ai-tone ~/.codex/skills/

# Claude Code
cp -r dahuang-ai-tone/skills/dahuang-ai-tone ~/.claude/skills/
\`\`\`

## 仓库结构

\`\`\`text
.
├── README.md
├── LICENSE
├── CHANGELOG.md
└── skills/
    └── dahuang-ai-tone/
        ├── SKILL.md
        ├── agents/openai.yaml
        ├── profiles/
        ├── references/
        └── examples/
\`\`\`

## 核心文档

- [Skill 入口](skills/dahuang-ai-tone/SKILL.md)
- [风格证据与时效策略](skills/dahuang-ai-tone/references/evidence-policy.md)
- [通用 AI 模式](skills/dahuang-ai-tone/references/common-ai-patterns.md)
- [加味方法](skills/dahuang-ai-tone/references/reverse-humanizer.md)
- [GPT Profile](skills/dahuang-ai-tone/profiles/openai-gpt-style.md)
- [Claude Profile](skills/dahuang-ai-tone/profiles/anthropic-claude-style.md)
- [Gemini Profile](skills/dahuang-ai-tone/profiles/google-gemini-style.md)
- [豆包 Profile](skills/dahuang-ai-tone/profiles/bytedance-doubao-style.md)

## 边界

- 不确认文本由哪个模型生成。
- 不猜作者身份或具体版本。
- 不把历史快照描述成当前稳定行为。
- 不为模拟风格篡改事实。

## License

[MIT](LICENSE) © 2026 realchendahuang
