# OpenAI GPT / reasoning 风格

描述可模拟的写作表面，不用于识别生成来源。先读 \`references/evidence-policy.md\`。

## 目录

1. 家族级倾向
2. reasoning 与 GPT 的任务表面
3. 产品和配置表面
4. 加味方法
5. 误判边界
6. 来源

## 家族级倾向

以下适合作为模拟方向，不能单独用于归因：

- 先给结论或可执行答案，再用分点补理由。
- 喜欢把问题整理成方法、步骤、清单或决策框架。
- 语气通常完整、稳妥、可交付，容易把结尾收成总结或下一步。
- 在散文任务中可能出现流畅、温情、意象化的成品感。
- 在中文说明文中容易出现“核心在于”“更重要的是”“综上”等通用 AI 结构。

这些特征与其他家族高度重叠。必须结合互动方式、任务表面和多个结构特征判断。

## reasoning 与 GPT 的任务表面

OpenAI 官方文档把 reasoning models 和 GPT models 视为不同的提示对象：

- reasoning models 更适合高层目标和直接约束。
- GPT models 更受益于明确的角色、逻辑、数据和输出要求。

这是提示与任务分工，不是稳定文风。模拟时可以这样区分：

- **reasoning 表面**：问题定义更克制，先澄清成功条件，少展示模板化推理过程。
- **GPT 表面**：执行路径更显式，结构、步骤和交付格式更完整。

不要把“先问问题”写成 reasoning models 的必然人格；是否澄清首先取决于输入是否缺信息和提示要求。

## 产品和配置表面

### API Markdown 行为

OpenAI reasoning best practices 说明：从 \`o1-2024-12-17\` 起，API reasoning models 会避免 Markdown，开发者可在 developer message 首行加入 \`Formatting re-enabled\` 开启。

这只能说明特定 API 与配置表面：

- 已知上下文是该 API 配置时，可以模拟纯文本输出。
- 面对未知文本时，“没有 Markdown”只是弱信号，不能反推 OpenAI 或 o-series。
- ChatGPT、Codex、第三方产品和后处理可能呈现完全不同的格式。

### 官方示例

OpenAI prompt-engineering 页面包含一条月光、独角兽和星尘的抒情示例。它证明模型可以被提示成温情诗化风格，不证明所有 GPT 输出都如此，也不应被标成永久版本签名。

## 加味方法

### GPT 家族味

1. 第一段直接给结论或主张。
2. 把解释组织成少量清楚的步骤或维度。
3. 每一项都补一个可执行动作或具体例子。
4. 收尾给明确下一步；不要自动升华。
5. 需要“经典 ChatGPT 味”时，再适量加入完整分点、礼貌缓冲和总结感。

### reasoning API 表面

只在用户明确要求时：

1. 用直接目标和约束进入任务。
2. 不写“让我们一步步思考”或展开隐藏推理。
3. 已知目标缺关键条件时问一个必要问题，否则直接执行。
4. 用户指定旧 API Markdown 表面时输出纯文本；没有指定就不强制。

### 温情散文味

1. 使用一个具体意象，而不是堆一串“delve / tapestry”。
2. 给对象轻度拟人化或命名。
3. 用柔和画面收尾，不补方法论总结。

## 误判边界

- 结论先行、列表、Markdown、温情收尾都是跨家族特征。
- 提示词可以完全覆盖默认风格。
- API 格式行为、ChatGPT 产品表面和模型家族必须分开。
- 词汇时代差异只能作为历史观察，不能用于判断具体版本。
- 未知文本最高给中等家族相似度，不输出版本归因。

## 来源

- OpenAI Prompt engineering: https://developers.openai.com/api/docs/guides/prompt-engineering
- OpenAI Reasoning best practices: https://developers.openai.com/api/docs/guides/reasoning-best-practices

核对日期：2026-07-10。官方文档明确说明同一家族不同快照可能表现不同，应以受控样本和评测验证行为。
