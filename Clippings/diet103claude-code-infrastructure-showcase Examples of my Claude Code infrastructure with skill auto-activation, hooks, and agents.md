---
title: "diet103/claude-code-infrastructure-showcase: Examples of my Claude Code infrastructure with skill auto-activation, hooks, and agents"
source: "https://github.com/diet103/claude-code-infrastructure-showcase"
author:
  - "[[GitHub]]"
published:
created: 2025-11-14
description: "Examples of my Claude Code infrastructure with skill auto-activation, hooks, and agents - diet103/claude-code-infrastructure-showcase"
tags:
  - "clippings"
---
在过去六个月的密集使用中，我打造了一套强大且实用的Claude Code工作体系，助力我单人重写30万行代码，提升质量与效率。这篇长文分享我的经验和实操技巧，希望给你带来启发。  
  
核心亮点包括：  
  
1. 技能自动激活系统  
过去技能往往静默无用，我通过TypeScript钩子实现自动激活。每次提交请求前，系统会分析关键词、意图、文件路径等，智能注入相关技能指导，确保Claude主动遵循最新最佳实践。完成后再进行代码风险自检提醒，保证代码质量。

2. 分层模块化技能设计  
遵循Anthropic建议，将大型技能拆分成500行以下主文件加多个资源文件。这样Claude初始加载轻量主文件，按需调用资源，大大提升上下文效率，减少Token浪费。

3. 开发文档系统，防止上下文丢失  
通过为每个任务建立三份文档（计划、上下文、任务清单），让Claude即使在重启或上下文压缩后依然能快速“接盘”，避免走偏或遗忘细节。

4. PM2进程管理实现后端日志实时监控  
7个后端微服务由PM2统一管理，Claude可实时查看日志、自动重启服务，极大提升调试效率和稳定性，摆脱人工复制日志的低效。

5. 钩子系统确保无遗漏质量管控  
- 编辑后自动跟踪文件和仓库  
- 会话结束时自动执行构建检查，捕获TypeScript错误  
- 错误提醒钩子温和提示错误处理是否完善  
- （曾试过自动Prettier格式化，后因Token消耗大已弃用）

这些钩子形成闭环，杜绝错误遗留，代码始终整洁一致。  
  
6. 专用代理（Agents）和快捷命令（Slash Commands）  
我构建了十多个专责代理，负责代码审查、重构规划、测试认证路由、错误定位修复等，搭配多种快捷命令，极大简化重复操作，提升工作流连贯性。

7. 附加实用脚本与工具  
例如测试认证路由的脚本，自动化生成测试数据，数据库重置及备份，提升整体开发体验。推荐所有实用脚本都写入相关技能或文档，方便复用。

8. 理念与心得  
- AI不是魔法，碰到复杂逻辑或常识问题时，适时介入修正，避免浪费时间。  
- 多次重试和反思提示设计，提升输出质量。  
- 规划先行，详细计划是成功的关键。  
- 文档与技能互补，文档聚焦项目架构与流程，技能聚焦最佳实践和模式。  
- 提问要具体且中立，避免引导性问题以获得更客观反馈。

这套系统让我从混乱的技术债务和零测试覆盖，转变成拥有稳定流程、可维护代码和高生产效率的现代项目。虽然搭建过程费时费力，但回报丰厚，尤其适合大规模代码库和复杂项目。  
  
如果你也在用Claude Code，强烈建议参考我的GitHub仓库，快速上手自动化技能激活和钩子机制：  
github.com/diet103/claude-code-infrastructure-showcase  
  
总结一句话：  
让AI主动工作，而非被动等待，规划和规范驱动，才是高效AI编程的王道。

原文：www.reddit.com/r/ClaudeAI/comments/1oivjvm/claude_code_is_a_beast_tips_from_6_months_of/

[[Claude Code is a Beast – Tips from 6 Months of Hardcore Use]]

**[claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase)** Public

Examples of my Claude Code infrastructure with skill auto-activation, hooks, and agents

[MIT license](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/diet103/claude-code-infrastructure-showcase?resume=1)

<table><thead><tr><th colspan="2"><span>Name</span></th><th colspan="1"><span>Name</span></th><th><p><span>Last commit message</span></p></th><th colspan="1"><p><span>Last commit date</span></p></th></tr></thead><tbody><tr><td colspan="3"><p><span><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/a5818cb99f54f360303feacdeebe2ded291fdf71">Claude made up a random link for my reddit post, fixed</a></span></p><p><span><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/a5818cb99f54f360303feacdeebe2ded291fdf71">a5818cb</a> ·</span></p><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commits/main/"><span><span><span>8 Commits</span></span></span></a></p></td></tr><tr><td colspan="2"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/tree/main/.claude">.claude</a></p></td><td colspan="1"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/tree/main/.claude">.claude</a></p></td><td><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/c586f9d8854989abbe9040cde61527888ded3904">Enhance CLAUDE_INTEGRATION_GUIDE and add backend resources</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/tree/main/dev">dev</a></p></td><td colspan="1"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/tree/main/dev">dev</a></p></td><td><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/3ef16a99842c7b8168b9ddcdfdd05f9b84f2c0c5">Complete infrastructure showcase as reference library</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.gitignore">.gitignore</a></p></td><td colspan="1"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.gitignore">.gitignore</a></p></td><td><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/e3ce3c11fca3a5ed9db8ed92e4b71d4343302352">Initial repository structure</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/CLAUDE_INTEGRATION_GUIDE.md">CLAUDE_INTEGRATION_GUIDE.md</a></p></td><td colspan="1"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/CLAUDE_INTEGRATION_GUIDE.md">CLAUDE_INTEGRATION_GUIDE.md</a></p></td><td><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/c586f9d8854989abbe9040cde61527888ded3904">Enhance CLAUDE_INTEGRATION_GUIDE and add backend resources</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/LICENSE">LICENSE</a></p></td><td colspan="1"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/LICENSE">LICENSE</a></p></td><td><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/e3ce3c11fca3a5ed9db8ed92e4b71d4343302352">Initial repository structure</a></p></td><td></td></tr><tr><td colspan="2"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/README.md">README.md</a></p></td><td colspan="1"><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/README.md">README.md</a></p></td><td><p><a href="https://github.com/diet103/claude-code-infrastructure-showcase/commit/a5818cb99f54f360303feacdeebe2ded291fdf71">Claude made up a random link for my reddit post, fixed</a></p></td><td></td></tr><tr><td colspan="3"></td></tr></tbody></table>

**A curated reference library of production-tested Claude Code infrastructure.**

Born from 6 months of real-world use managing a complex TypeScript microservices project, this showcase provides the patterns and systems that solved the "skills don't activate automatically" problem and scaled Claude Code for enterprise development.

> **This is NOT a working application** - it's a reference library. Copy what you need into your own projects.

---

## What's Inside

**Production-tested infrastructure for:**

- ✅ **Auto-activating skills** via hooks
- ✅ **Modular skill pattern** (500-line rule with progressive disclosure)
- ✅ **Specialized agents** for complex tasks
- ✅ **Dev docs system** that survives context resets
- ✅ **Comprehensive examples** using generic blog domain

**Time investment to build:** 6 months of iteration **Time to integrate into your project:** 15-30 minutes

---

**Claude:** Read [`CLAUDE_INTEGRATION_GUIDE.md`](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/CLAUDE_INTEGRATION_GUIDE.md) for step-by-step integration instructions tailored for AI-assisted setup.

**The breakthrough feature:** Skills that actually activate when you need them.

**What you need:**

1. The skill-activation hooks (2 files)
2. A skill or two relevant to your work
3. 15 minutes

**👉 [Setup Guide:.claude/hooks/README.md](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/hooks/README.md)**

Browse the [skills catalog](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills) and copy what you need.

**Available:**

- **backend-dev-guidelines** - Node.js/Express/TypeScript patterns
- **frontend-dev-guidelines** - React/TypeScript/MUI v7 patterns
- **skill-developer** - Meta-skill for creating skills
- **route-tester** - Test authenticated API routes
- **error-tracking** - Sentry integration patterns

**👉 [Skills Guide:.claude/skills/README.md](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/README.md)**

10 production-tested agents for complex tasks:

- Code architecture review
- Refactoring assistance
- Documentation generation
- Error debugging
- And more...

**👉 [Agents Guide:.claude/agents/README.md](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/agents/README.md)**

---

**Problem:** Claude Code skills just sit there. You have to remember to use them.

**Solution:** UserPromptSubmit hook that:

- Analyzes your prompts
- Checks file context
- Automatically suggests relevant skills
- Works via `skill-rules.json` configuration

**Result:** Skills activate when you need them, not when you remember them.

### Production-Tested Patterns

These aren't theoretical examples - they're extracted from:

- ✅ 6 microservices in production
- ✅ 50,000+ lines of TypeScript
- ✅ React frontend with complex data grids
- ✅ Sophisticated workflow engine
- ✅ 6 months of daily Claude Code use

The patterns work because they solved real problems.

Large skills hit context limits. The solution:

```
skill-name/
  SKILL.md                  # <500 lines, high-level guide
  resources/
    topic-1.md              # <500 lines each
    topic-2.md
    topic-3.md
```

**Progressive disclosure:** Claude loads main skill first, loads resources only when needed.

---

## Repository Structure

```
.claude/
├── skills/                 # 5 production skills
│   ├── backend-dev-guidelines/  (12 resource files)
│   ├── frontend-dev-guidelines/ (11 resource files)
│   ├── skill-developer/         (7 resource files)
│   ├── route-tester/
│   ├── error-tracking/
│   └── skill-rules.json    # Skill activation configuration
├── hooks/                  # 6 hooks for automation
│   ├── skill-activation-prompt.*  (ESSENTIAL)
│   ├── post-tool-use-tracker.sh   (ESSENTIAL)
│   ├── tsc-check.sh        (optional, needs customization)
│   └── trigger-build-resolver.sh  (optional)
├── agents/                 # 10 specialized agents
│   ├── code-architecture-reviewer.md
│   ├── refactor-planner.md
│   ├── frontend-error-fixer.md
│   └── ... 7 more
└── commands/               # 3 slash commands
    ├── dev-docs.md
    └── ...

dev/
└── active/                 # Dev docs pattern examples
    └── public-infrastructure-repo/
```

---

## Component Catalog

| Skill | Lines | Purpose | Best For |
| --- | --- | --- | --- |
| [**skill-developer**](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/skill-developer) | 426 | Creating and managing skills | Meta-development |
| [**backend-dev-guidelines**](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/backend-dev-guidelines) | 304 | Express/Prisma/Sentry patterns | Backend APIs |
| [**frontend-dev-guidelines**](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/frontend-dev-guidelines) | 398 | React/MUI v7/TypeScript | React frontends |
| [**route-tester**](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/route-tester) | 389 | Testing authenticated routes | API testing |
| [**error-tracking**](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/error-tracking) | ~250 | Sentry integration | Error monitoring |

**All skills follow the modular pattern** - main file + resource files for progressive disclosure.

**👉 [How to integrate skills →](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/README.md)**

| Hook | Type | Essential? | Customization |
| --- | --- | --- | --- |
| skill-activation-prompt | UserPromptSubmit | ✅ YES | ✅ None needed |
| post-tool-use-tracker | PostToolUse | ✅ YES | ✅ None needed |
| tsc-check | Stop | ⚠️ Optional | ⚠️ Heavy - monorepo only |
| trigger-build-resolver | Stop | ⚠️ Optional | ⚠️ Heavy - monorepo only |
| error-handling-reminder | Stop | ⚠️ Optional | ⚠️ Moderate |
| stop-build-check-enhanced | Stop | ⚠️ Optional | ⚠️ Moderate |

**Start with the two essential hooks** - they enable skill auto-activation and work out of the box.

**👉 [Hook setup guide →](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/hooks/README.md)**

**Standalone - just copy and use!**

| Agent | Purpose |
| --- | --- |
| code-architecture-reviewer | Review code for architectural consistency |
| code-refactor-master | Plan and execute refactoring |
| documentation-architect | Generate comprehensive documentation |
| frontend-error-fixer | Debug frontend errors |
| plan-reviewer | Review development plans |
| refactor-planner | Create refactoring strategies |
| web-research-specialist | Research technical issues online |
| auth-route-tester | Test authenticated endpoints |
| auth-route-debugger | Debug auth issues |
| auto-error-resolver | Auto-fix TypeScript errors |

**👉 [How agents work →](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/agents/README.md)**

| Command | Purpose |
| --- | --- |
| /dev-docs | Create structured dev documentation |
| /dev-docs-update | Update docs before context reset |
| /route-research-for-testing | Research route patterns for testing |

---

## Key Concepts

**The system:**

1. **skill-activation-prompt hook** runs on every user prompt
2. Checks **skill-rules.json** for trigger patterns
3. Suggests relevant skills automatically
4. Skills load only when needed

**This solves the #1 problem** with Claude Code skills: they don't activate on their own.

**Problem:** Large skills hit context limits

**Solution:** Modular structure

- Main SKILL.md <500 lines (overview + navigation)
- Resource files <500 lines each (deep dives)
- Claude loads incrementally as needed

**Example:** backend-dev-guidelines has 12 resource files covering routing, controllers, services, repositories, testing, etc.

**Problem:** Context resets lose project context

**Solution:** Three-file structure

- `[task]-plan.md` - Strategic plan
- `[task]-context.md` - Key decisions and files
- `[task]-tasks.md` - Checklist format

**Works with:**`/dev-docs` slash command to generate these automatically

---

### settings.json

The included `settings.json` is an **example only**:

- Stop hooks reference specific monorepo structure
- Service names (blog-api, etc.) are examples
- MCP servers may not exist in your setup

**To use it:**

1. Extract ONLY UserPromptSubmit and PostToolUse hooks
2. Customize or skip Stop hooks
3. Update MCP server list for your setup

Skills use generic blog examples (Post/Comment/User):

- These are **teaching examples**, not requirements
- Patterns work for any domain (e-commerce, SaaS, etc.)
- Adapt the patterns to your business logic

Some hooks expect specific structures:

- `tsc-check.sh` expects service directories
- Customize based on YOUR project layout

---

## Integration Workflow

**Recommended approach:**

1. Copy skill-activation-prompt hook
2. Copy post-tool-use-tracker hook
3. Update settings.json
4. Install hook dependencies
1. Pick ONE relevant skill
2. Copy skill directory
3. Create/update skill-rules.json
4. Customize path patterns
1. Edit a file - skill should activate
2. Ask a question - skill should be suggested
3. Add more skills as needed
- Add agents you find useful
- Add slash commands
- Customize Stop hooks (advanced)

---

## Getting Help

### For Users

**Issues with integration?**

1. Check [CLAUDE\_INTEGRATION\_GUIDE.md](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/CLAUDE_INTEGRATION_GUIDE.md)
2. Ask Claude: "Why isn't \[skill\] activating?"
3. Open an issue with your project structure

When helping users integrate:

1. **Read CLAUDE\_INTEGRATION\_GUIDE.md FIRST**
2. Ask about their project structure
3. Customize, don't blindly copy
4. Verify after integration

---

❌ Skills don't activate automatically ❌ Have to remember which skill to use ❌ Large skills hit context limits ❌ Context resets lose project knowledge ❌ No consistency across development ❌ Manual agent invocation every time

✅ Skills suggest themselves based on context ✅ Hooks trigger skills at the right time ✅ Modular skills stay under context limits ✅ Dev docs preserve knowledge across resets ✅ Consistent patterns via guardrails ✅ Agents streamline complex tasks

---

## Community

**Found this useful?**

- ⭐ Star this repo
- 🐛 Report issues or suggest improvements
- 💬 Share your own skills/hooks/agents
- 📝 Contribute examples from your domain

**Background:**This infrastructure was detailed in a post I made to Reddit ["Claude Code is a Beast – Tips from 6 Months of Hardcore Use"](https://www.reddit.com/r/ClaudeAI/comments/1oivjvm/claude_code_is_a_beast_tips_from_6_months_of/). After hundreds of requests, this showcase was created to help the community implement these patterns.

---

## License

MIT License - Use freely in your projects, commercial or personal.

---

## Quick Links

- 📖 [Claude Integration Guide](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/CLAUDE_INTEGRATION_GUIDE.md) - For AI-assisted setup
- 🎨 [Skills Documentation](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/skills/README.md)
- 🪝 [Hooks Setup](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/hooks/README.md)
- 🤖 [Agents Guide](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/.claude/agents/README.md)
- 📝 [Dev Docs Pattern](https://github.com/diet103/claude-code-infrastructure-showcase/blob/main/dev/README.md)

**Start here:** Copy the two essential hooks, add one skill, and see the auto-activation magic happen.

## Releases

No releases published

## Packages

No packages published  

## Languages

- [Shell 60.1%](https://github.com/diet103/claude-code-infrastructure-showcase/search?l=shell)
- [JavaScript 39.9%](https://github.com/diet103/claude-code-infrastructure-showcase/search?l=javascript)