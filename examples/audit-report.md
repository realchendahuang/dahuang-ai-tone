# 找味示范

> 示范对象：Aider 真实对话样本 C-1（Claude 编程助手 explain-then-do 开场）。展示怎么引用原文指出 AI 味在哪、像哪个家族。

## 找味对象

> To create a Flask app with a `/hello` endpoint that returns 'Hello, World!', we need to install Flask, import it, create an app instance, and define a route for the `/hello` endpoint. Here's how to update the `app.py` file:

## 结论

最像的模型家族：Anthropic Claude（编程助手场景）
版本：家族级，无法区分具体版本
置信度：中

一句话：这段是典型的 "explain-then-do" 编程助手开场——先一句原理解释再给方案，是 Claude/GPT 编程助手的共享特征，但语气和组织方式略偏 Claude。

## 风格相似度

- **Anthropic Claude**：中到高  
  像在：先讲原理（"we need to install Flask, import it, create an app instance, and define a route"）再给方案（"Here's how to update the `app.py` file:"），是 Claude 编程助手的典型 explain-then-do 开场（见 `profiles/anthropic-claude-family.md` 样本 C-1）。
- **OpenAI GPT**：中  
  像在：explain-then-do 也是 GPT 编程助手的共享特征，无法凭这一条区分。但这段的语气更克制、更教学式，不像 GPT 那样偏任务化结论先行。
- **Google Gemini**：低  
  像在：教学式语气有一点，但不像 Gemini 那样知识卡片化、定义先行。
- **字节豆包**：低  
  像在：无中文产品助手感（文本是英文）。

## 逐处找味

### 味 1

> we need to install Flask, import it, create an app instance, and define a route for the `/hello` endpoint.

可观察：先给一句包含四个步骤的原理解释（install → import → create → define），是动词链式任务分解，不是直接给代码。

为什么像：Claude 编程助手的典型 "explain-then-do" 开场——先讲清楚要做什么，再给方案。见 `profiles/anthropic-claude-family.md` 样本 C-1。GPT 编程助手也有这个特征，但 Claude 更倾向于先讲原理。

相似家族：Anthropic Claude
强度：中

### 味 2

> Here's how to update the `app.py` file:

可观察：用 "Here's how to..." 过渡到方案，不是直接贴代码或用"下一步"命令式。

为什么像：Claude 常见的过渡句式，语气教学式、引导式。GPT 更倾向直接给代码或"接下来"。

相似家族：Anthropic Claude
强度：中

### 味 3

> To create a Flask app with a `/hello` endpoint that returns 'Hello, World!'

可观察：开头用 "To create..." 目的状语从句，先复述用户目标再展开。

为什么像：Claude 倾向先确认理解用户意图再动手。但这也是很多编程助手的共享特征，区分力弱。

相似家族：Claude / GPT 编程助手共享
强度：弱

## 认味不丢人

- explain-then-do 是 Claude/GPT 编程助手的共享特征，不能凭这一条就判 Claude。
- 文本来自 Aider 场景，可能有 Aider 的系统提示影响，不是纯模型输出。
- 文本较短，无法判断具体版本。
- 一个教学风格的人类工程师也可能这样开场。
