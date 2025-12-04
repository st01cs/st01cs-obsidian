---
title: "Writing a good CLAUDE.md"
source: "https://www.humanlayer.dev/blog/writing-a-good-claude-md"
author:
published: 2025-11-25
created: 2025-12-04
description: "`CLAUDE.md` is a high-leverage configuration point for Claude Code. Learning how to write a good `CLAUDE.md` (or `AGENTS.md`) is a key skill for agent-enabled software engineering."
tags:
  - "clippings"
---
*Note: this post is also applicable to `AGENTS.md`*, the open-source equivalent of `CLAUDE.md` for agents and harnesses like OpenCode, Zed, Cursor and Codex.  
注意：本文同样适用于 `AGENTS.md` —— 这是面向 OpenCode、Zed、Cursor 和 Codex 等智能体与开发环境的开源版 `CLAUDE.md` 。

## \## Principle: LLMs are (mostly) stateless## 原则：LLMs（大语言模型）是（基本）无状态的

LLMs are stateless functions. Their weights are frozen by the time they're used for inference, so they don't learn over time. The only thing that the model knows about your codebase is the tokens you put into it.  
LLMs 是无状态函数。它们的权重在用于推理时即已冻结，因此不会随时间推移而学习。模型对你的代码库所知的唯一信息，就是你输入给它的那些 token。

Similarly, coding agent harnesses such as Claude Code usually require you to manage agents' memory explicitly. `CLAUDE.md` (or `AGENTS.md`) is the only file that by default goes into *every single conversation* you have with the agent.  
类似地，Claude Code 等编程智能体运行框架通常要求你显式管理智能体的记忆。 `CLAUDE.md` （或 `AGENTS.md` ）是默认情况下会自动加入你与该智能体每一次对话的唯一文件。

**This has three important implications:  
这带来了三个重要影响：**

1. Coding agents know absolutely nothing about your codebase at the beginning of each session.  
	每次会话开始时，编程智能体对你代码库的内容完全一无所知。
2. The agent must be told anything that's important to know about your codebase each time you start a session.  
	每次启动会话时，都必须向智能体告知所有与您的代码库相关的重要信息。
3. `CLAUDE.md` is the preferred way of doing this.  
	`CLAUDE.md` 是推荐的实现方式。

## \## CLAUDE.md onboards Claude to your codebase## CLAUDE.md 将 Claude 接入您的代码库

Since Claude doesn't know anything about your codebase at the beginning of each session, you should use `CLAUDE.md` to onboard Claude into your codebase. At a high level, this means it should cover:  
由于 Claude 在每次会话开始时对您的代码库一无所知，您应使用 `CLAUDE.md` 将其接入您的代码库。总体而言，这包括以下内容：

- **WHAT**: tell Claude about the tech, your stack, the project structure. Give Claude a map of the codebase. This is especially important in monorepos! Tell Claude what the apps are, what the shared packages are, and what everything is for so that it knows where to look for things  
	是什么：向 Claude 介绍你的技术栈、项目结构等信息，为 Claude 提供一份代码库的“地图”。这一点在单体仓库（monorepo）中尤为重要！请明确告诉 Claude：有哪些应用、哪些是共享包，以及每个部分的用途，以便它能准确知道去哪里查找相关内容。
- **WHY**: tell Claude the *purpose* of the project and what everything is doing in the repository. What are the purpose and function of the different parts of the project?  
	为什么：向 Claude 说明项目的整体目标，以及仓库中各部分的功能与作用。项目各模块的设计目的和实际职责分别是什么？
- **HOW**: tell Claude how it should work on the project. For example, do you use `bun` instead of `node`? You want to include all the information it needs to actually do meaningful work on the project. How can Claude verify Claude's changes? How can it run tests, typechecks, and compilation steps?  
	怎么做：向 Claude 说明它应如何参与该项目。例如，你们是否使用 `bun` 而非 `node` ？你需要提供所有能让 Claude 真正开展有意义工作的必要信息。Claude 如何验证自身所做修改的正确性？如何运行测试、类型检查及编译流程？

But the way you do this is important! Don't try to stuff every command Claude could possibly need to run in your `CLAUDE.md` file - you will get sub-optimal results.  
但实现这一目标的方式至关重要！切勿试图将 Claude 可能用到的所有命令一股脑塞进你的 `CLAUDE.md` 文件中——这样做只会导致效果欠佳。

## \## Claude often ignores CLAUDE.md## Claude 常常忽略 CLAUDE.md

Regardless of which model you're using, you may notice that Claude frequently ignores your `CLAUDE.md` file's contents.  
无论你使用的是哪个模型，都可能注意到 Claude 频繁忽略你的 `CLAUDE.md` 文件内容。

You can investigate this yourself by putting a logging proxy between the claude code CLI and the Anthropic API using `ANTHROPIC_BASE_URL`. Claude code injects the following system reminder with your `CLAUDE.md` file in the user message to the agent:  
你可以通过在 claude code CLI 与 Anthropic API 之间设置一个日志代理（使用 `ANTHROPIC_BASE_URL` ）来自行验证这一点。Claude code 会将你的 `CLAUDE.md` 文件内容作为系统提示，插入到发给智能体的用户消息中，具体如下：

```
<system-reminder>
      IMPORTANT: this context may or may not be relevant to your tasks. 
      You should not respond to this context unless it is highly relevant to your task.
</system-reminder>
```

As a result, Claude will ignore the contents of your `CLAUDE.md` if it decides that it is not relevant to its current task. The more information you have in the file that's not **universally applicable** to the tasks you have it working on, the more likely it is that Claude will ignore your instructions in the file.  
因此，一旦 Claude 判定你的 `CLAUDE.md` 文件内容与其当前任务无关，便会直接忽略该文件内容。你在该文件中写入的、不适用于你交由其处理的所有任务的通用信息越多，Claude 忽略其中指令的可能性就越大。

*Why did Anthropic add this?* It's hard to say for sure, but we can speculate a bit. Most `CLAUDE.md` files we come across include a bunch of instructions in the file that *aren't* broadly applicable. Many users treat the file as a way to add "hotfixes" to behavior they didn't like by appending lots of instructions that weren't necessarily broadly applicable.  
Anthropic 为何要添加这一功能？确切原因尚不明确，但我们可稍作推测。我们遇到的大多数 `CLAUDE.md` 文件中都包含大量并不具备普适性的指令。许多用户将该文件视为一种“热修复”手段，用以修正自己不喜欢的行为，因此不断追加大量指令——而这些指令往往并不具备广泛适用性。

We can only assume that the Claude Code team found that by telling Claude to ignore the bad instructions, the harness actually produced better results.  
我们只能推测，Claude Code 团队发现，若明确指示 Claude 忽略那些不良指令，实际运行效果反而更佳。

## \## Creating a good CLAUDE.md file## 编写一份优质的 CLAUDE.md 文件

The following section provides a number of recommendations on how to write a good `CLAUDE.md` file following [context engineering best practices](https://github.com/humanlayer/12-factor-agents/blob/d20c728368bf9c189d6d7aab704744decb6ec0cc/content/factor-03-own-your-context-window.md).  
以下部分将依据上下文工程（context engineering）的最佳实践，提供若干编写优质 `CLAUDE.md` 文件的建议。

*Your mileage may vary.* Not all of these rules are necessarily optimal for every setup. Like anything else, feel free to break the rules once...  
实际效果因人而异。这些规则并非在所有场景下都必然最优。与其他任何规则一样，只要满足以下条件，你完全可以打破它们……

1. you understand when & why it's okay to break them  
	你已充分理解：在何种情况下、出于何种原因打破规则是恰当的
2. you have a good reason to do so  
	你有充分且合理的理由这样做

### \### Less (instructions) is more### 少即是多（指令）

It can be tempting to try and stuff every single command that claude could possibly need to run, as well as your code standards and style guidelines into `CLAUDE.md`. **We recommend against this.**  
试图将 Claude 可能需要执行的每一个命令，以及您的代码规范和风格指南全部塞进 `CLAUDE.md` 中，这种做法颇具诱惑力。但我们不建议这样做。

Though the topic hasn't been investigated in an incredibly rigorous manner, [some research](https://arxiv.org/pdf/2507.11538) has been done which indicates the following:  
尽管这一主题尚未经过极为严谨的研究，但已有部分相关研究得出了以下结论：

1. **Frontier thinking LLMs can follow ~ 150-200 instructions with reasonable consistency.** Smaller models can attend to fewer instructions than larger models, and non-thinking models can attend to fewer instructions than thinking models.  
	前沿思维型 LLMs 能够以相对一致的表现遵循约 150–200 条指令。较小的模型能处理的指令数量少于较大的模型，而非思维型模型能处理的指令数量则少于思维型模型。
2. **Smaller models get MUCH worse, MUCH more quickly**. Specifically, smaller models tend to exhibit an expotential decay in instruction-following performance as the number of instructions increase, whereas larger frontier thinking models exhibit a linear decay (see below). For this reason, we recommend against using smaller models for multi-step tasks or complicated implementation plans.  
	较小的模型性能会急剧下降，且下降速度极快。具体而言，随着指令数量的增加，较小模型的指令遵循能力往往呈指数级衰减，而较大的前沿思维模型则表现为线性衰减（见下图）。因此，我们不建议在多步骤任务或复杂的实施计划中使用较小的模型。
3. **LLMs bias towards instructions that are on the peripheries of the prompt**: at the very beginning (the Claude Code system message and `CLAUDE.md`), and at the very end (the most-recent user messages)  
	LLMs 倾向于关注提示词边缘位置的指令：最开头（Claude Code 系统消息及 `CLAUDE.md` ）和最末尾（最近的用户消息）
4. **As instruction count increases, instruction-following quality decreases uniformly**. This means that as you give the LLM more instructions, it doesn't simply ignore the newer ("further down in the file") instructions - it begins to **ignore all of them uniformly**  
	随着指令数量的增加，模型遵循指令的质量会均匀下降。这意味着，当你向 LLM 提供越来越多的指令时，它并不会单纯忽略较新的（即“文件中位置更靠后”的）指令，而是会开始均匀地忽略所有指令。

![Instruction following](https://www.humanlayer.dev/blog/writing-a-good-claude-md/instructionfollowing.png)

Our analysis of the Claude Code harness indicates that **Claude Code's system prompt contains ~50 individual instructions**. Depending on the model you're using, that's nearly a third of the instructions your agent can reliably follow already - and that's before rules, plugins, skills, or user messages.  
我们对 Claude Code 工具链的分析表明，Claude Code 的系统提示词中包含了约 50 条独立指令。具体比例取决于您所使用的模型，但这些指令已占您的智能体能够稳定遵循的全部指令数的近三分之一——而这还尚未计入规则、插件、技能或用户消息等内容。

This implies that your `CLAUDE.md` file should contain as few instructions as possible - ideally only ones which are universally applicable to your task.  
这意味着您的 \` `CLAUDE.md` \` 文件应尽可能少地包含指令——理想情况下，仅包含对您的任务普遍适用的指令。

### \### CLAUDE.md file length & applicability### CLAUDE.md 文件长度与适用性

All else being equal, **an LLM will perform better on a task when its' context window is full of focused, relevant context** including examples, related files, tool calls, and tool results compared to when its context window has a lot of irrelevant context.  
其他条件相同时，当 LLM 的上下文窗口中填满聚焦且相关的内容（包括示例、相关文件、工具调用及工具执行结果）时，其任务表现会优于上下文窗口中充斥大量无关内容的情况。

Since `CLAUDE.md` goes into *every single session*, you should ensure that its contents are as universally applicable as possible.  
由于 `CLAUDE.md` 会进入每一个会话，因此您应确保其内容尽可能具有普适性。

For example, avoid including instructions about (for example) how to structure a new database schema - this won't matter and will distract the model when you're working on something else that's unrelated!  
例如，避免包含有关（例如）如何构建新数据库模式的说明——这类内容无关紧要，且当你处理其他不相关任务时，反而会分散模型的注意力！

Length-wise, the *less is more* principle applies as well. While Anthropic does not have an official recommendation on how long your `CLAUDE.md` file should be, general consensus is that < 300 lines is best, and shorter is even better.  
篇幅方面，“少即是多”的原则同样适用。虽然 Anthropic 并未就\` `CLAUDE.md` \`文件的推荐长度给出官方建议，但业界普遍认为其行数应少于 300 行，越短越好。

At HumanLayer, our root `CLAUDE.md` file is *less than sixty lines*.  
在 HumanLayer，我们的根目录下的 \` `CLAUDE.md` \` 文件不足六十行。

### \### Progressive Disclosure### 渐进式披露

Writing a concise `CLAUDE.md` file that covers everything you want Claude to know can be challenging, especially in larger projects.  
编写一份简洁的 \`CLAUDE.md\` 文件，使其涵盖所有你希望 Claude 了解的内容，可能颇具挑战性，尤其是在大型项目中。

To address this, we can leverage the principle of **Progressive Disclosure** to ensure that claude only sees task- or project-specific instructions when it needs them.  
为解决这一问题，我们可以运用“渐进式披露”原则，确保 Claude 仅在需要时才看到与当前任务或项目相关的具体指令。

Instead of including all your different instructions about building your project, running tests, code conventions, or other important context in your `CLAUDE.md` file, we recommend keeping task-specific instructions in *separate markdown files* with self-descriptive names somewhere in your project.  
我们建议不要将有关项目构建、测试运行、代码规范或其他重要上下文的所有不同指令都塞进您的 `CLAUDE.md` 文件中，而是将面向特定任务的指令分别保存在项目中某处、以自描述性名称命名的独立 Markdown 文件中。

For example:例如：

```
agent_docs/
  |- building_the_project.md
  |- running_tests.md 
  |- code_conventions.md
  |- service_architecture.md
  |- database_schema.md
  |- service_communication_patterns.md
```

Then, in your `CLAUDE.md` file, you can include a list of these files with a brief description of each, and instruct Claude to decide which (if any) are relevant and to read them before it starts working. Or, ask Claude to present you with the files it wants to read for aproval first before reading them.  
然后，在您的 \` `CLAUDE.md` \` 文件中，您可以列出这些文件，并为每个文件附上简短说明，同时指示 Claude 判断其中哪些（如有）与当前任务相关，并在开始工作前先阅读它们。或者，您也可以要求 Claude 先向您呈现它希望阅读的文件列表，待您批准后再进行阅读。

**Prefer pointers to copies**. Don't include code snippets in these files if possible - they will become out-of-date quickly. Instead, include `file:line` references to point Claude to the authoritative context.  
优先使用指向原始内容的链接，而非复制内容。如非必要，请勿在这些文件中包含代码片段——它们会很快过时。取而代之的是，应使用 `file:line` 引用，以引导 Claude 指向权威的上下文。

Conceptually, this is very similar to how [Claude Skills](https://code.claude.com/docs/en/skills) are intended to work, although skills are more focused on tool use than instructions.  
从概念上讲，这与 Claude 技能（Claude Skills）的设计初衷非常相似，尽管技能更侧重于工具调用，而非指令本身。

### \### Claude is (not) an expensive linter### Claude 并（不）是一个昂贵的代码检查工具

One of the most common things that we see people put in their `CLAUDE.md` file is code style guidelines. **Never send an LLM to do a linter's job**. LLMs are comparably expensive and *incredibly* slow compared to traditional linters and formatters. We think you should *always use deterministic tools whenever you can*.  
我们在人们的 \` `CLAUDE.md` \` 文件中最常看到的内容之一是代码风格指南。切勿让 LLM 执行 linter 的工作。与传统的 linter 和格式化工具相比，LLM 的成本相对高昂且速度极慢。我们认为，只要可能，就应始终使用确定性工具。

Code style guidelines will inevitably add a bunch of instructions and mostly-irrelevant code snippets into your context window, degrading your LLM's performance and instruction-following and eating up your context window.  
代码风格指南不可避免地会在你的上下文窗口中添加大量指令和大多无关的代码片段，从而降低 LLM 的性能和指令遵循能力，并占用你的上下文窗口。

**LLMs are in-context learners**! If your code follows a certain set of style guidelines or patterns, you should find that armed with a few searches of your codebase (or a good research document!) your agent should tend to follow existing code patterns and conventions without being told to.  
LLMs 是上下文学习者！如果你的代码遵循某种特定的风格指南或模式，那么只需对你的代码库进行几次搜索（或参考一份详尽的研究文档！），你就会发现，你的智能体往往会自然而然地遵循已有的代码模式和规范，而无需额外指示。

If you feel very stronly about this, you might even consider setting up a [Claude Code `Stop` hook](https://code.claude.com/docs/en/hooks#stop) that runs your formatter & linter and presents errors to Claude for it to fix. Don't make Claude find the formatting issues itself.  
如果你对此非常重视，甚至可以考虑设置一个 Claude Code `Stop` 钩子，让它自动运行你的代码格式化工具和代码检查工具，并将发现的错误呈现给 Claude，由它来修复。不要让 Claude 自己去查找格式问题。

**Bonus points**: use a linter that can automatically fix issues (we like Biome), and carefully tune your rules about what can safely be auto-fixed for maximum (safe) coverage.  
额外加分项：使用可自动修复问题的代码检查工具（我们推荐 Biome），并仔细调整规则，明确哪些问题可以安全地自动修复，以实现最大（且安全）的覆盖范围。

You could also create a [Slash Command](https://code.claude.com/docs/en/slash-commands) that includes your code guidelines and which points claude at the changes in version control, or at your `git status`, or similar. This way, you can handle implementation and formatting separately. **You will see better results with both as a result**.  
你还可以创建一个斜杠命令（Slash Command），其中包含你的代码规范，并让 Claude 指向版本控制系统中的变更内容，或指向你的 `git status` ，或类似位置。这样，你便能将实现逻辑与格式规范分开处理，从而在两方面都获得更佳效果。

### \### Don't use /init or auto-generate your CLAUDE.md### 不要使用 /init 或自动生成您的 CLAUDE.md

Both Claude Code and other harnesses with OpenCode come with ways to auto-generate your `CLAUDE.md` file (or `AGENTS.md`).  
Claude Code 和其他搭载 OpenCode 的运行环境均提供了自动生成您的 \` `CLAUDE.md` \` 文件（或 \` `AGENTS.md` \`）的功能。

Because `CLAUDE.md` goes into *every single session* with Claude code, it is one of **the highest leverage points of the harness** - for better or for worse, depending on how you use it.  
由于 `CLAUDE.md` 会进入与 Claude 进行的每一次会话代码中，因此它是该框架中杠杆效应最强的环节之一——其效果是正面还是负面，取决于你如何使用它。

A bad line of code is a bad line of code. A bad line of an implementation plan has the potential to create a **lot** of bad lines of code. A bad line of a research that misunderstands how the system works has the potential to result in a lot of bad lines in the plan, and therefore a **lot more** bad lines of code as a result.  
一行糟糕的代码就是一行糟糕的代码。 一份实施计划中的一处错误，可能导致大量糟糕的代码。 而一项未能正确理解系统运作机制的研究中的一处谬误，则可能引发计划中的诸多错误，进而导致更多糟糕的代码。

But the `CLAUDE.md` file affects **every single phase of your workflow** and every single artifact produced by it. As a result, we think you should spend some time thinking very carefully about every single line that goes into it:  
但 \` `CLAUDE.md` \` 文件会影响你工作流的每个阶段以及由此产生的每个产物。因此，我们认为你应该花些时间，仔细斟酌其中的每一行内容：

![Leverage](https://www.humanlayer.dev/blog/writing-a-good-claude-md/leverage.png)

## \## In Conclusion ## 总结

1. `CLAUDE.md` is for onboarding Claude into your codebase. It should define your project's **WHY**, **WHAT**, and **HOW**.  
	`CLAUDE.md` 用于引导 Claude 熟悉你的代码库。它应明确阐述你项目的“为何做（WHY）”、“做什么（WHAT）”以及“如何做（HOW）”。
2. **Less (instructions) is more**. While you shouldn't omit necessary instructions, you should include as few instructions as reasonably possible in the file.  
	少即是多（指令越少越好）。虽然你不应省略必要的指令，但应尽可能在文件中包含最少的合理指令。
3. Keep the contents of your `CLAUDE.md` **concise and universally applicable**.  
	请保持您的 `CLAUDE.md` 内容简洁且具有普适性。
4. Use **Progressive Disclosure** - don't tell Claude all the information you could possibly want it to know. Rather, tell it *how to find* important information so that it can find and use it, but only when it needs to to avoid bloating your context window or instruction count.  
	采用渐进式披露——不要一次性向 Claude 提供所有你可能希望它知道的信息。相反，应告知 Claude 如何查找关键信息，使其能在需要时自主检索并使用这些信息，从而避免占用过多上下文窗口空间或增加指令数量。
5. Claude is not a linter. Use linters and code formatters, and use other features like [Hooks](https://code.claude.com/docs/en/hooks) and [Slash Commands](https://code.claude.com/docs/en/slash-commands) as necessary.  
	Claude 不是代码检查工具。请使用代码检查工具（linter）和代码格式化工具，并根据需要使用 Hooks 和斜杠命令（Slash Commands）等其他功能。
6. **`CLAUDE.md` is the highest leverage point of the harness**, so avoid auto-generating it. You should carefully craft its contents for best results.  
	`CLAUDE.md` 是 harness 中杠杆效应最强的点，因此请勿自动生成。您应精心设计其内容，以获得最佳效果。