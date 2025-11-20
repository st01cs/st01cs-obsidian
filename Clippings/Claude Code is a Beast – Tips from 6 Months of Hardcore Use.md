---
title: "Claude Code is a Beast – Tips from 6 Months of Hardcore Use"
source: "https://www.reddit.com/r/ClaudeAI/comments/1oivjvm/claude_code_is_a_beast_tips_from_6_months_of/"
author:
  - "[[JokeGold5455]]"
published: 2025-10-29
created: 2025-11-14
description:
tags:
  - "clippings"
---
*Quick pro-tip from a fellow lazy person: You can throw this book of a post into one of the many text-to-speech AI services like* [*ElevenLabs Reader*](https://elevenlabs.io/text-reader) *or* [*Natural Reader*](https://www.naturalreaders.com/online/) *and have it read the post for you* :)

Edit: Many of you are asking for a repo so I will make an effort to get one up in the next couple days. All of this is a part of a work project at the moment, so I have to take some time to copy everything into a fresh project and scrub any identifying info. I will post the link here when it's up. You can also follow me and I will post it on my profile so you get notified. Thank you all for the kind comments. I'm happy to share this info with others since I don't get much chance to do so in my day-to-day.

Edit (final?): I bit the bullet and spent the afternoon getting a github repo up for you guys. Just made a post with some additional info [here](https://www.reddit.com/r/ClaudeAI/comments/1ojqxbg/claude_code_is_a_beast_examples_repo_by_popular/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button) or you can go straight to the source:

**🎯 Repository:** [https://github.com/diet103/claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase)

# Disclaimer

I made a post about six months ago sharing my experience after a week of hardcore use with Claude Code. It's now been about six months of hardcore use, and I would like to share some more tips, tricks, and word vomit with you all. I may have went a little overboard here so strap in, grab a coffee, sit on the toilet or whatever it is you do when doom-scrolling reddit.

I want to start the post off with a disclaimer: all the content within this post is merely me sharing what setup is working best for me currently and should not be taken as gospel or the only correct way to do things. It's meant to hopefully inspire you to improve your setup and workflows with AI agentic coding. I'm just a guy, and this is just like, my opinion, man.

Also, I'm on the 20x Max plan, so your mileage may vary. And if you're looking for vibe-coding tips, you should look elsewhere. If you want the best out of CC, then you should be working together with it: planning, reviewing, iterating, exploring different approaches, etc.

# Quick Overview

After 6 months of pushing Claude Code to its limits (solo rewriting 300k LOC), here's the system I built:

- Skills that actually auto-activate when needed
- Dev docs workflow that prevents Claude from losing the plot
- PM2 + hooks for zero-errors-left-behind
- Army of specialized agents for reviews, testing, and planning

Let's get into it.

# Background

I'm a software engineer who has been working on production web apps for the last seven years or so. And I have fully embraced the wave of AI with open arms. I'm not too worried about AI taking my job anytime soon, as it is a tool that I use to leverage my capabilities. In doing so, I have been building MANY new features and coming up with all sorts of new proposal presentations put together with Claude and GPT-5 Thinking to integrate new AI systems into our production apps. Projects I would have never dreamt of having the time to even consider before integrating AI into my workflow. And with all that, I'm giving myself a good deal of job security and have become the AI guru at my job since everyone else is about a year or so behind on how they're integrating AI into their day-to-day.

With my newfound confidence, I proposed a pretty large redesign/refactor of one of our web apps used as an internal tool at work. This was a pretty rough college student-made project that was forked off another project developed by me as an intern (created about 7 years ago and forked 4 years ago). This may have been a bit overly ambitious of me since, to sell it to the stakeholders, I agreed to finish a top-down redesign of this fairly decent-sized project (~100k LOC) in a matter of a few months...all by myself. I knew going in that I was going to have to put in extra hours to get this done, even with the help of CC. But deep down, I know it's going to be a hit, automating several manual processes and saving a lot of time for a lot of people at the company.

It's now six months later... yeah, I probably should not have agreed to this timeline. I have tested the limits of both Claude as well as my own sanity trying to get this thing done. I completely scrapped the old frontend, as everything was seriously outdated and I wanted to play with the latest and greatest. I'm talkin' React 16 JS → React 19 TypeScript, React Query v2 → TanStack Query v5, React Router v4 w/ hashrouter → TanStack Router w/ file-based routing, Material UI v4 → MUI v7, all with strict adherence to best practices. The project is now at ~300-400k LOC and my life expectancy ~5 years shorter. It's finally ready to put up for testing, and I am incredibly happy with how things have turned out.

This used to be a project with insurmountable tech debt, ZERO test coverage, HORRIBLE developer experience (testing things was an absolute nightmare), and all sorts of jank going on. I addressed all of those issues with decent test coverage, manageable tech debt, and implemented a command-line tool for generating test data as well as a dev mode to test different features on the frontend. During this time, I have gotten to know CC's abilities and what to expect out of it.

# A Note on Quality and Consistency

I've noticed a recurring theme in forums and discussions - people experiencing frustration with usage limits and concerns about output quality declining over time. I want to be clear up front: I'm not here to dismiss those experiences or claim it's simply a matter of "doing it wrong." Everyone's use cases and contexts are different, and valid concerns deserve to be heard.

That said, I want to share what's been working for me. In my experience, CC's output has actually improved significantly over the last couple of months, and I believe that's largely due to the workflow I've been constantly refining. My hope is that if you take even a small bit of inspiration from my system and integrate it into your CC workflow, you'll give it a better chance at producing quality output that you're happy with.

Now, let's be real - there are absolutely times when Claude completely misses the mark and produces suboptimal code. This can happen for various reasons. First, AI models are stochastic, meaning you can get widely varying outputs from the same input. Sometimes the randomness just doesn't go your way, and you get an output that's legitimately poor quality through no fault of your own. Other times, it's about how the prompt is structured. There can be significant differences in outputs given slightly different wording because the model takes things quite literally. If you misword or phrase something ambiguously, it can lead to vastly inferior results.

# Sometimes You Just Need to Step In

Look, AI is incredible, but it's not magic. There are certain problems where pattern recognition and human intuition just win. If you've spent 30 minutes watching Claude struggle with something that you could fix in 2 minutes, just fix it yourself. No shame in that. Think of it like teaching someone to ride a bike, sometimes you just need to steady the handlebars for a second before letting go again.

I've seen this especially with logic puzzles or problems that require real-world common sense. AI can brute-force a lot of things, but sometimes a human just "gets it" faster. Don't let stubbornness or some misguided sense of "but the AI should do everything" waste your time. Step in, fix the issue, and keep moving.

I've had my fair share of terrible prompting, which usually happens towards the end of the day where I'm getting lazy and I'm not putting that much effort into my prompts. And the results really show. So next time you are having these kinds of issues where you think the output is way worse these days because you think Anthropic shadow-nerfed Claude, I encourage you to take a step back and reflect on how you are prompting.

**Re-prompt often.** You can hit double-esc to bring up your previous prompts and select one to branch from. You'd be amazed how often you can get way better results armed with the knowledge of what you don't want when giving the same prompt. All that to say, there can be many reasons why the output quality seems to be worse, and it's good to self-reflect and consider what you can do to give it the best possible chance to get the output you want.

As some wise dude somewhere probably said, "Ask not what Claude can do for you, ask what context you can give to Claude" ~ Wise Dude

Alright, I'm going to step down from my soapbox now and get on to the good stuff.

# My System

I've implemented a lot changes to my workflow as it relates to CC over the last 6 months, and the results have been pretty great, IMO.

# Skills Auto-Activation System (Game Changer!)

This one deserves its own section because it completely transformed how I work with Claude Code.

# The Problem

So Anthropic releases this Skills feature, and I'm thinking "this looks awesome!" The idea of having these portable, reusable guidelines that Claude can reference sounded perfect for maintaining consistency across my massive codebase. I spent a good chunk of time with Claude writing up comprehensive skills for frontend development, backend development, database operations, workflow management, etc. We're talking thousands of lines of best practices, patterns, and examples.

And then... nothing. Claude just wouldn't use them. I'd literally use the exact keywords from the skill descriptions. Nothing. I'd work on files that should trigger the skills. Nothing. It was incredibly frustrating because I could see the potential, but the skills just sat there like expensive decorations.

# The "Aha!" Moment

That's when I had the idea of using **hooks**. If Claude won't automatically use skills, what if I built a system that MAKES it check for relevant skills before doing anything?

So I dove into Claude Code's hook system and built a multi-layered auto-activation architecture with TypeScript hooks. And it actually works!

# How It Works

I created two main hooks:

**1\. UserPromptSubmit Hook** (runs BEFORE Claude sees your message):

- Analyzes your prompt for keywords and intent patterns
- Checks which skills might be relevant
- Injects a formatted reminder into Claude's context
- Now when I ask "how does the layout system work?" Claude sees a big "🎯 SKILL ACTIVATION CHECK - Use project-catalog-developer skill" (project catalog is a large complex data grid based feature on my front end) before even reading my question

**2\. Stop Event Hook** (runs AFTER Claude finishes responding):

- Analyzes which files were edited
- Checks for risky patterns (try-catch blocks, database operations, async functions)
- Displays a gentle self-check reminder
- "Did you add error handling? Are Prisma operations using the repository pattern?"
- Non-blocking, just keeps Claude aware without being annoying

# skill-rules.json Configuration

I created a central configuration file that defines every skill with:

- **Keywords**: Explicit topic matches ("layout", "workflow", "database")
- **Intent patterns**: Regex to catch actions ("(create|add).\*?(feature|route)")
- **File path triggers**: Activates based on what file you're editing
- **Content triggers**: Activates if file contains specific patterns (Prisma imports, controllers, etc.)

Example snippet:

{
  "backend-dev-guidelines": {
    "type": "domain",
    "enforcement": "suggest",
    "priority": "high",
    "promptTriggers": {
      "keywords": \["backend", "controller", "service", "API", "endpoint"\],
      "intentPatterns": \[
        "(create|add).\*?(route|endpoint|controller)",
        "(how to|best practice).\*?(backend|API)"
      \]
    },
    "fileTriggers": {
      "pathPatterns": \["backend/src/\*\*/\*.ts"\],
      "contentPatterns": \["router\\\\.", "export.\*Controller"\]
    }
  }
}

# The Results

Now when I work on backend code, Claude automatically:

1. Sees the skill suggestion before reading my prompt
2. Loads the relevant guidelines
3. Actually follows the patterns consistently
4. Self-checks at the end via gentle reminders

**The difference is night and day.** No more inconsistent code. No more "wait, Claude used the old pattern again." No more manually telling it to check the guidelines every single time.

# Following Anthropic's Best Practices (The Hard Way)

After getting the auto-activation working, I dove deeper and found Anthropic's official best practices docs. Turns out I was doing it wrong because they recommend keeping the main SKILL.md file **under 500 lines** and using progressive disclosure with resource files.

Whoops. My frontend-dev-guidelines skill was 1,500+ lines. And I had a couple other skills over 1,000 lines. These monolithic files were defeating the whole purpose of skills (loading only what you need).

So I restructured everything:

- **frontend-dev-guidelines**: 398-line main file + 10 resource files
- **backend-dev-guidelines**: 304-line main file + 11 resource files

Now Claude loads the lightweight main file initially, and only pulls in detailed resource files when actually needed. Token efficiency improved 40-60% for most queries.

# Skills I've Created

Here's my current skill lineup:

**Guidelines & Best Practices:**

- `backend-dev-guidelines` - Routes → Controllers → Services → Repositories
- `frontend-dev-guidelines` - React 19, MUI v7, TanStack Query/Router patterns
- `skill-developer` - Meta-skill for creating more skills

**Domain-Specific:**

- `workflow-developer` - Complex workflow engine patterns
- `notification-developer` - Email/notification system
- `database-verification` - Prevent column name errors (this one is a guardrail that actually blocks edits!)
- `project-catalog-developer` - DataGrid layout system

All of these automatically activate based on what I'm working on. It's like having a senior dev who actually remembers all the patterns looking over Claude's shoulder.

# Why This Matters

Before skills + hooks:

- Claude would use old patterns even though I documented new ones
- Had to manually tell Claude to check BEST\_PRACTICES.md every time
- Inconsistent code across the 300k+ LOC codebase
- Spent too much time fixing Claude's "creative interpretations"

After skills + hooks:

- Consistent patterns automatically enforced
- Claude self-corrects before I even see the code
- Can trust that guidelines are being followed
- Way less time spent on reviews and fixes

If you're working on a large codebase with established patterns, I cannot recommend this system enough. The initial setup took a couple of days to get right, but it's paid for itself ten times over.

# CLAUDE.md and Documentation Evolution

In a post I wrote 6 months ago, I had a section about rules being your best friend, which I still stand by. But my CLAUDE.md file was quickly getting out of hand and was trying to do too much. I also had this massive BEST\_PRACTICES.md file (1,400+ lines) that Claude would sometimes read and sometimes completely ignore.

So I took an afternoon with Claude to consolidate and reorganize everything into a new system. Here's what changed:

# What Moved to Skills

Previously, BEST\_PRACTICES.md contained:

- TypeScript standards
- React patterns (hooks, components, suspense)
- Backend API patterns (routes, controllers, services)
- Error handling (Sentry integration)
- Database patterns (Prisma usage)
- Testing guidelines
- Performance optimization

**All of that is now in skills** with the auto-activation hook ensuring Claude actually uses them. No more hoping Claude remembers to check BEST\_PRACTICES.md.

# What Stayed in CLAUDE.md

Now CLAUDE.md is laser-focused on **project-specific info** (only ~200 lines):

- Quick commands (`pnpm pm2:start`, `pnpm build`, etc.)
- Service-specific configuration
- Task management workflow (dev docs system)
- Testing authenticated routes
- Workflow dry-run mode
- Browser tools configuration

# The New Structure

Root CLAUDE.md (100 lines)
├── Critical universal rules
├── Points to repo-specific claude.md files
└── References skills for detailed guidelines

Each Repo's claude.md (50-100 lines)
├── Quick Start section pointing to:
│   ├── PROJECT\_KNOWLEDGE.md - Architecture & integration
│   ├── TROUBLESHOOTING.md - Common issues
│   └── Auto-generated API docs
└── Repo-specific quirks and commands

**The magic:** Skills handle all the "how to write code" guidelines, and CLAUDE.md handles "how this specific project works." Separation of concerns for the win.

# Dev Docs System

This system, out of everything (besides skills), I think has made the most impact on the results I'm getting out of CC. Claude is like an extremely confident junior dev with extreme amnesia, losing track of what they're doing easily. This system is aimed at solving those shortcomings.

The dev docs section from my CLAUDE.md:

\### Starting Large Tasks

When exiting plan mode with an accepted plan: 1.\*\*Create Task Directory\*\*:
mkdir -p ~/git/project/dev/active/\[task-name\]/

2.\*\*Create Documents\*\*:

- \`\[task-name\]-plan.md\` - The accepted plan
- \`\[task-name\]-context.md\` - Key files, decisions
- \`\[task-name\]-tasks.md\` - Checklist of work

3.\*\*Update Regularly\*\*: Mark tasks complete immediately

### Continuing Tasks

- Check \`/dev/active/\` for existing tasks
- Read all three files before proceeding
- Update "Last Updated" timestamps

These are documents that always get created for every feature or large task. Before using this system, I had many times when I all of a sudden realized that Claude had lost the plot and we were no longer implementing what we had planned out 30 minutes earlier because we went off on some tangent for whatever reason.

# My Planning Process

My process starts with planning. **Planning is king**. If you aren't at a minimum using planning mode before asking Claude to implement something, you're gonna have a bad time, mmm'kay. You wouldn't have a builder come to your house and start slapping on an addition without having him draw things up first.

When I start planning a feature, I put it into planning mode, even though I will eventually have Claude write the plan down in a markdown file. I'm not sure putting it into planning mode necessary, but to me, it feels like planning mode gets better results doing the research on your codebase and getting all the correct context to be able to put together a plan.

I created a `strategic-plan-architect` subagent that's basically a planning beast. It:

- Gathers context efficiently
- Analyzes project structure
- Creates comprehensive structured plans with executive summary, phases, tasks, risks, success metrics, timelines
- Generates three files automatically: plan, context, and tasks checklist

But I find it really annoying that you can't see the agent's output, and even more annoying is if you say no to the plan, it just kills the agent instead of continuing to plan. So I also created a custom slash command (`/dev-docs`) with the same prompt to use on the main CC instance.

Once Claude spits out that beautiful plan, I take time to review it thoroughly. **This step is really important.** Take time to understand it, and you'd be surprised at how often you catch silly mistakes or Claude misunderstanding a very vital part of the request or task.

More often than not, I'll be at 15% context left or less after exiting plan mode. But that's okay because we're going to put everything we need to start fresh into our dev docs. Claude usually likes to just jump in guns blazing, so I immediately slap the ESC key to interrupt and run my `/dev-docs` slash command. The command takes the approved plan and creates all three files, sometimes doing a bit more research to fill in gaps if there's enough context left.

And once I'm done with that, I'm pretty much set to have Claude fully implement the feature without getting lost or losing track of what it was doing, even through an auto-compaction. I just make sure to remind Claude every once in a while to update the tasks as well as the context file with any relevant context. And once I'm running low on context in the current session, I just run my slash command `/update-dev-docs`. Claude will note any relevant context (with next steps) as well as mark any completed tasks or add new tasks before I compact the conversation. And all I need to say is "continue" in the new session.

During implementation, depending on the size of the feature or task, I will specifically tell Claude to only implement one or two sections at a time. That way, I'm getting the chance to go in and review the code in between each set of tasks. And periodically, I have a subagent also reviewing the changes so I can catch big mistakes early on. If you aren't having Claude review its own code, then I highly recommend it because it saved me a lot of headaches catching critical errors, missing implementations, inconsistent code, and security flaws.

# PM2 Process Management (Backend Debugging Game Changer)

This one's a relatively recent addition, but it's made debugging backend issues so much easier.

# The Problem

My project has seven backend microservices running simultaneously. The issue was that Claude didn't have access to view the logs while services were running. I couldn't just ask "what's going wrong with the email service?" - Claude couldn't see the logs without me manually copying and pasting them into chat.

# The Intermediate Solution

For a while, I had each service write its output to a timestamped log file using a `devLog` script. This worked... okay. Claude could read the log files, but it was clunky. Logs weren't real-time, services wouldn't auto-restart on crashes, and managing everything was a pain.

# The Real Solution: PM2

Then I discovered PM2, and it was a game changer. I configured all my backend services to run via PM2 with a single command: `pnpm pm2:start`

**What this gives me:**

- Each service runs as a managed process with its own log file
- **Claude can easily read individual service logs in real-time**
- Automatic restarts on crashes
- Real-time monitoring with `pm2 logs`
- Memory/CPU monitoring with `pm2 monit`
- Easy service management (`pm2 restart email`, `pm2 stop all`, etc.)

**PM2 Configuration:**

// ecosystem.config.jsmodule.exports = {
  apps: \[
    {
      name: 'form-service',
      script: 'npm',
      args: 'start',
      cwd: './form',
      error\_file: './form/logs/error.log',
      out\_file: './form/logs/out.log',
    },
// ... 6 more services
  \]
};

**Before PM2:**

Me: "The email service is throwing errors"
Me: \[Manually finds and copies logs\]
Me: \[Pastes into chat\]
Claude: "Let me analyze this..."

**The debugging workflow now:**

Me: "The email service is throwing errors"
Claude: \[Runs\] pm2 logs email --lines 200
Claude: \[Reads the logs\] "I see the issue - database connection timeout..."
Claude: \[Runs\] pm2 restart email
Claude: "Restarted the service, monitoring for errors..."

Night and day difference. Claude can autonomously debug issues now without me being a human log-fetching service.

**One caveat:** Hot reload doesn't work with PM2, so I still run the frontend separately with `pnpm dev`. But for backend services that don't need hot reload as often, PM2 is incredible.

# Hooks System (#NoMessLeftBehind)

The project I'm working on is multi-root and has about eight different repos in the root project directory. One for the frontend and seven microservices and utilities for the backend. I'm constantly bouncing around making changes in a couple of repos at a time depending on the feature.

And one thing that would annoy me to no end is when Claude forgets to run the build command in whatever repo it's editing to catch errors. And it will just leave a dozen or so TypeScript errors without me catching it. Then a couple of hours later I see Claude running a build script like a good boy and I see the output: "There are several TypeScript errors, but they are unrelated, so we're all good here!"

No, we are not good, Claude.

# Hook #1: File Edit Tracker

First, I created a **post-tool-use hook** that runs after every Edit/Write/MultiEdit operation. It logs:

- Which files were edited
- What repo they belong to
- Timestamps

Initially, I made it run builds immediately after each edit, but that was stupidly inefficient. Claude makes edits that break things all the time before quickly fixing them.

# Hook #2: Build Checker

Then I added a **Stop hook** that runs when Claude finishes responding. It:

1. Reads the edit logs to find which repos were modified
2. Runs build scripts on each affected repo
3. Checks for TypeScript errors
4. If < 5 errors: Shows them to Claude
5. If ≥ 5 errors: Recommends launching auto-error-resolver agent
6. Logs everything for debugging

Since implementing this system, I've not had a single instance where Claude has left errors in the code for me to find later. The hook catches them immediately, and Claude fixes them before moving on.

# Hook #3: Prettier Formatter

This one's simple but effective. After Claude finishes responding, automatically format all edited files with Prettier using the appropriate `.prettierrc` config for that repo.

No more going into to manually edit a file just to have prettier run and produce 20 changes because Claude decided to leave off trailing commas last week when we created that file.

**⚠️ Update: I No Longer Recommend This Hook**

After publishing, a reader shared [detailed data](https://www.reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2cxm7/) showing that file modifications trigger `<system-reminder>` notifications that can consume significant context tokens. In their case, Prettier formatting led to 160k tokens consumed in just 3 rounds due to system-reminders showing file diffs.

While the impact varies by project (large files and strict formatting rules are worst-case scenarios), I'm removing this hook from my setup. It's not a big deal to let formatting happen when you manually edit files anyway, and the potential token cost isn't worth the convenience.

If you want automatic formatting, consider running Prettier manually between sessions instead of during Claude conversations.

# Hook #4: Error Handling Reminder

This is the gentle philosophy hook I mentioned earlier:

- Analyzes edited files after Claude finishes
- Detects risky patterns (try-catch, async operations, database calls, controllers)
- Shows a gentle reminder if risky code was written
- Claude self-assesses whether error handling is needed
- No blocking, no friction, just awareness

**Example output:**

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
📋 ERROR HANDLING SELF-CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚠️  Backend Changes Detected
   2 file(s) edited

   ❓ Did you add Sentry.captureException() in catch blocks?
   ❓ Are Prisma operations wrapped in error handling?

   💡 Backend Best Practice:
      - All errors should be captured to Sentry
      - Controllers should extend BaseController
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# The Complete Hook Pipeline

Here's what happens on every Claude response now:

Claude finishes responding
  ↓
Hook 1: Prettier formatter runs → All edited files auto-formatted
  ↓
Hook 2: Build checker runs → TypeScript errors caught immediately
  ↓
Hook 3: Error reminder runs → Gentle self-check for error handling
  ↓
If errors found → Claude sees them and fixes
  ↓
If too many errors → Auto-error-resolver agent recommended
  ↓
Result: Clean, formatted, error-free code

And the UserPromptSubmit hook ensures Claude loads relevant skills BEFORE even starting work.

**No mess left behind.** It's beautiful.

# Scripts Attached to Skills

One really cool pattern I picked up from Anthropic's official skill examples on GitHub: **attach utility scripts to skills**.

For example, my `backend-dev-guidelines` skill has a section about testing authenticated routes. Instead of just explaining how authentication works, the skill references an actual script:

\### Testing Authenticated Routes

Use the provided test-auth-route.js script:

node scripts/test-auth-route.js http://localhost:3002/api/endpoint

The script handles all the complex authentication steps for you:

1. Gets a refresh token from Keycloak
2. Signs the token with JWT secret
3. Creates cookie header
4. Makes authenticated request

When Claude needs to test a route, it knows exactly what script to use and how to use it. No more "let me create a test script" and reinventing the wheel every time.

I'm planning to expand this pattern - attach more utility scripts to relevant skills so Claude has ready-to-use tools instead of generating them from scratch.

# Tools and Other Things

# SuperWhisper on Mac

Voice-to-text for prompting when my hands are tired from typing. Works surprisingly well, and Claude understands my rambling voice-to-text surprisingly well.

# Memory MCP

I use this less over time now that skills handle most of the "remembering patterns" work. But it's still useful for tracking project-specific decisions and architectural choices that don't belong in skills.

# BetterTouchTool

- Relative URL copy from Cursor (for sharing code references)
	- I have VSCode open to more easily find the files I’m looking for and I can double tap CAPS-LOCK, then BTT inputs the shortcut to copy relative URL, transforms the clipboard contents by prepending an ‘@’ symbol, focuses the terminal, and then pastes the file path. All in one.
- Double-tap hotkeys to quickly focus apps (CMD+CMD = Claude Code, OPT+OPT = Browser)
- Custom gestures for common actions

Honestly, the time savings on just not fumbling between apps is worth the BTT purchase alone.

# Scripts for Everything

If there's any annoying tedious task, chances are there's a script for that:

- Command-line tool to generate mock test data. Before using Claude code, it was extremely annoying to generate mock data because I would have to make a submission to a form that had about a 120 questions Just to generate one single test submission.
- Authentication testing scripts (get tokens, test routes)
- Database resetting and seeding
- Schema diff checker before migrations
- Automated backup and restore for dev database

**Pro tip:** When Claude helps you write a useful script, immediately document it in CLAUDE.md or attach it to a relevant skill. Future you will thank past you.

# Documentation (Still Important, But Evolved)

I think next to planning, documentation is almost just as important. I document everything as I go in addition to the dev docs that are created for each task or feature. From system architecture to data flow diagrams to actual developer docs and APIs, just to name a few.

**But here's what changed:** Documentation now works WITH skills, not instead of them.

**Skills contain:** Reusable patterns, best practices, how-to guides **Documentation contains:** System architecture, data flows, API references, integration points

For example:

- "How to create a controller" → **backend-dev-guidelines skill**
- "How our workflow engine works" → **Architecture documentation**
- "How to write React components" → **frontend-dev-guidelines skill**
- "How notifications flow through the system" → **Data flow diagram + notification skill**

I still have a LOT of docs (850+ markdown files), but now they're laser-focused on project-specific architecture rather than repeating general best practices that are better served by skills.

You don't necessarily have to go that crazy, but I highly recommend setting up multiple levels of documentation. Ones for broad architectural overview of specific services, wherein you'll include paths to other documentation that goes into more specifics of different parts of the architecture. It will make a major difference on Claude's ability to easily navigate your codebase.

# Prompt Tips

When you're writing out your prompt, you should try to be as specific as possible about what you are wanting as a result. Once again, you wouldn't ask a builder to come out and build you a new bathroom without at least discussing plans, right?

"You're absolutely right! Shag carpet probably is not the best idea to have in a bathroom."

Sometimes you might not know the specifics, and that's okay. If you don't ask questions, tell Claude to research and come back with several potential solutions. You could even use a specialized subagent or use any other AI chat interface to do your research. The world is your oyster. I promise you this will pay dividends because you will be able to look at the plan that Claude has produced and have a better idea if it's good, bad, or needs adjustments. Otherwise, you're just flying blind, pure vibe-coding. Then you're gonna end up in a situation where you don't even know what context to include because you don't know what files are related to the thing you're trying to fix.

**Try not to lead in your prompts** if you want honest, unbiased feedback. If you're unsure about something Claude did, ask about it in a neutral way instead of saying, "Is this good or bad?" Claude tends to tell you what it thinks you want to hear, so leading questions can skew the response. It's better to just describe the situation and ask for thoughts or alternatives. That way, you'll get a more balanced answer.

# Agents, Hooks, and Slash Commands (The Holy Trinity)

# Agents

I've built a small army of specialized agents:

**Quality Control:**

- `code-architecture-reviewer` - Reviews code for best practices adherence
- `build-error-resolver` - Systematically fixes TypeScript errors
- `refactor-planner` - Creates comprehensive refactoring plans

**Testing & Debugging:**

- `auth-route-tester` - Tests backend routes with authentication
- `auth-route-debugger` - Debugs 401/403 errors and route issues
- `frontend-error-fixer` - Diagnoses and fixes frontend errors

**Planning & Strategy:**

- `strategic-plan-architect` - Creates detailed implementation plans
- `plan-reviewer` - Reviews plans before implementation
- `documentation-architect` - Creates/updates documentation

**Specialized:**

- `frontend-ux-designer` - Fixes styling and UX issues
- `web-research-specialist` - Researches issues along with many other things on the web
- `reactour-walkthrough-designer` - Creates UI tours

The key with agents is to give them **very specific roles** and clear instructions on what to return. I learned this the hard way after creating agents that would go off and do who-knows-what and come back with "I fixed it!" without telling me what they fixed.

# Hooks (Covered Above)

The hook system is honestly what ties everything together. Without hooks:

- Skills sit unused
- Errors slip through
- Code is inconsistently formatted
- No automatic quality checks

With hooks:

- Skills auto-activate
- Zero errors left behind
- Automatic formatting
- Quality awareness built-in

# Slash Commands

I have quite a few custom slash commands, but these are the ones I use most:

**Planning & Docs:**

- `/dev-docs` - Create comprehensive strategic plan
- `/dev-docs-update` - Update dev docs before compaction
- `/create-dev-docs` - Convert approved plan to dev doc files

**Quality & Review:**

- `/code-review` - Architectural code review
- `/build-and-fix` - Run builds and fix all errors

**Testing:**

- `/route-research-for-testing` - Find affected routes and launch tests
- `/test-route` - Test specific authenticated routes

The beauty of slash commands is they expand into full prompts, so you can pack a ton of context and instructions into a simple command. Way better than typing out the same instructions every time.

# Conclusion

After six months of hardcore use, here's what I've learned:

**The Essentials:**

1. **Plan everything** - Use planning mode or strategic-plan-architect
2. **Skills + Hooks** - Auto-activation is the only way skills actually work reliably
3. **Dev docs system** - Prevents Claude from losing the plot
4. **Code reviews** - Have Claude review its own work
5. **PM2 for backend** - Makes debugging actually bearable

**The Nice-to-Haves:**

- Specialized agents for common tasks
- Slash commands for repeated workflows
- Comprehensive documentation
- Utility scripts attached to skills
- Memory MCP for decisions

And that's about all I can think of for now. Like I said, I'm just some guy, and I would love to hear tips and tricks from everybody else, as well as any criticisms. Because I'm always up for improving upon my workflow. I honestly just wanted to share what's working for me with other people since I don't really have anybody else to share this with IRL (my team is very small, and they are all very slow getting on the AI train).

If you made it this far, thanks for taking the time to read. If you have questions about any of this stuff or want more details on implementation, happy to share. The hooks and skills system especially took some trial and error to get right, but now that it's working, I can't imagine going back.

TL;DR: Built an auto-activation system for Claude Code skills using TypeScript hooks, created a dev docs workflow to prevent context loss, and implemented PM2 + automated error checking. Result: Solo rewrote 300k LOC in 6 months with consistent quality.

---

## Comments

> **ClaudeAI-mod-bot** • [1 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlygsgb/) •
> 
> **If this post is showcasing a project you built with Claude, please change the post flair to Built with Claude so that it can be easily found by others.**

> **tmoothy** • [307 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyobac/) •
> 
> Are we still on Reddit or is this Wikipedia 🤓
> 
> > **\[deleted\]** • [29 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz3oc6/) •
> > 
> > don't you love infinite output ? and speaking everything out with max details because anything you miss will be used against you
> > 
> > **bbbggghhhjjjj** • [18 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz8a0a/) •
> > 
> > Amazing how people overcomplicate everything to death just to make themselves feel smart. I know no one read this but guy says he has 850+ md files. That’s more text in documents than in code, probably.
> > 
> > > **lucianw** • [34 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2kqpb/) •
> > > 
> > > I read all of OP's post. It was excellent quality. Don't dismiss it because of its length.
> > > 
> > > My day job (in big tech) is figuring out how to apply AI agents, and writing our own. The stuff that OP posted is exactly what we've been doing too, and for the same reasons.
> > > 
> > > > **\-Crash\_Override-** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nmb1rk2/) •
> > > > 
> > > > > (in big tech)
> > > > 
> > > > Just died of second hand cringe. RIP
> > 
> > **gefahr** • [18 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm07v1n/) •
> > 
> > I read it. There's at least two of us.
> > 
> > **Dex4Sure** • [15 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm1q10u/) •
> > 
> > His code was over 300K lines of code and apparently he’s software engineer. I wouldn’t be so quick to judge. Some people are smarter than others and it shouldn’t offend you. Too often these days you got people like yourself hating on people who try and work hard. It tells a lot about yourself.
> > 
> > **bman8810** • [6 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0if7a/) •
> > 
> > I love the idea that code should be the compiled version of documentation -- write docs, not code, just like we write code not compiled code.
> > 
> > > **acrackingnut** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2xv6e/) •
> > > 
> > > Code is deterministic, document to code conversion with AI is probabilistic. If you were working on any solution that needs precision/accuracy, think of the outcomes that will vary every time you build and deploy compiled code.
> > > 
> > > > **bman8810** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm3soye/) •
> > > > 
> > > > Except if you have to defined your specification properly then it comes with all of the criteria necessary to ensure that the solution is working precisely as you want it to.
> > > > 
> > > > As such, it doesn't matter whether the code is the same every time you reproduce from documentation. What matters is the outcome (the end product, not the code itself) is consistent.
> > > > 
> > > > There are a million ways to skin a cat with code.
> > > > 
> > > > > **killersnail2417** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm3tloz/) •
> > > > > 
> > > > > Aren't you just reinventing coding at that point?
> > 
> > **JokeGold5455** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0fagg/) •
> > 
> > No, not even close 😅. Also, keep in mind, a majority of those documents I can actually delete at this point since they are dev docs from already completed features. But they are actually incredibly useful to keep if I need to build upon and/or change that feature. I just attach them as context and Claude knows all it needs to know without me explaining hardly anything.
> 
> **zestypesty556655** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz5l99/) •
> 
> Tldr plz
> 
> > **WhereWhatWhoHuh** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz901r/) •
> > 
> > Tldr: Dis' Reddit or Wiki?
> > 
> > > **Dex4Sure** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm1q628/) •
> > > 
> > > Don’t know how to use AI to summarize? Everything must be spoon fed?

> **Livid-Reward8282** • [30 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyk974/) •
> 
> can you please share some hooks you mentioned? wondering how to use userprompthook to suggest available skills
> 
> > **JokeGold5455** • [163 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyl9eb/) •
> > 
> > As I Mentioned to another user that DM'd me, I'll look at getting a GitHub set up with some boilerplate later this week if enough people want it. I just really wanted to get this out, since it's been sitting in my drafts forever (I've just been adding stuff here and there. I started writing it before skills came out, so I ended up having to rewrite a good portion of it). In the meantime, you could probably just chuck my post-it Into a markdown file and include it as context to Claude and ask it to help you make it.
> > 
> > > **theblackpen** • [13 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyq5mf/) •
> > > 
> > > Please do! Excellent work m8!!!
> > > 
> > > **maddada\_** • [6 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyv1lz/) •
> > > 
> > > Great post, thank you! Would be awesome to have the github too please
> > > 
> > > **spacenglish** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz3912/) •
> > > 
> > > Please do the GitHub. Meanwhile, I will DM you as well.
> > > 
> > > **meepz** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0do45/) •
> > > 
> > > My legal name is "enough people". And I want it.
> > > 
> > > **No\_Gas\_3727** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0qq0p/) •
> > > 
> > > yeah, github would be cool to look at, looks like u've done titanic job mate, thank you in advance!
> > > 
> > > **\[deleted\]** • [0 points](https://reddit.com/) •
> > > 
> > > lol the entitlement. It probably has project-specific things in it he'd have to scrub. Where's your github we can demand things at?
> > > 
> > > > **gefahr** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0816q/) •
> > > > 
> > > > lol the entitlement. It probably has project-specific things in it he'd have to scrub. Where's your github we can demand things at?

> **SamuelQuackenbush** • [74 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlysy0x/) •
> 
> I've spent a lot of time on this sub, but this might be the best post I've read. So much of it makes sense.
> 
> > **JokeGold5455** • [26 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyw0uo/) •
> > 
> > Thanks, man. That means a lot to me. Glad I could help :)

> **Swashbuckler\_75** • [24 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzybx8/) •
> 
> This post is in the top 1% for genuine insight into how to use Claude Code 🚀

> **seatlessunicycle** • [14 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlynqrm/) •
> 
> Great stuff, thanks for sharing. I don't know anything about hooks, but that seems like the answer to a lot of my issues
> 
> > **\_chromascope\_** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyzjze/) •
> > 
> > Same here. Would love to know more about how hooks work. I'm not a dev but read through the entire post for productivity tips. Hooks is the one thing I'm most curious about.

> **macdigger** • [16 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyjzr6/) •
> 
> How much money on AI tools did you spend over that 6 months period?
> 
> > **JokeGold5455** • [23 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlykp4a/) •
> > 
> > Just the $200 plan, so $1200.
> > 
> > > **macdigger** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyldrp/) •
> > > 
> > > Hm not too bad! Thanks!
> > > 
> > > **PsychologicalWeird** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzb4dx/) •
> > > 
> > > Could you have done it all on the Pro plan or do you think it would take a lot longer? Im hobbyist more than being asked to redevelop so dont fancy more than $20 a month instead of $100/200 just to do a couple of projects for personal satisfaction.
> > > 
> > > > **JokeGold5455** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0m85p/) •
> > > > 
> > > > No way I could've done this on the Pro plan, but I do think I could have squeaked by on the 100 if I really evenly spaced out the work and made use of the limits perfectly. Maybe even a few Pro plans used extremely efficiently I suppose. That said, all this is still applicable to use on the Pro plan and would help with efficient context usage. Because I would guess there are some people wasting a large amount of context trying to attach too many files and then having to do that with every new conversation about the same feature.

> **lucianw** • [8 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0y8ql/) •
> 
> This is a fascinating and important post.
> 
> Your comments about hooks are spot on. Everyone needs to adopt them.
> 
> I disagree about "Hook #3: Prettier Formatter". I don't believe formatting belongs during the lifetime of a Claude conversation. It will cause context bloat: every time prettier changes a file on disk, Claude will get a <system-reminder> on its next UserPrompt, listing all lines changed. These will all be useless tokens. Remember with Claude, that every token spent in your context that doesn't contribute to your answer, will decrease the quality of the answer.
> 
> I think that formatting should only be run after a conversation has finished, before the next conversation starts.
> 
> > **JokeGold5455** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm1dr74/) •
> > 
> > Hmmm, I did not realize that! I will look into this and update my post accordingly. Thank you for the feedback.
> > 
> > Edit: So after looking into it, I found that in Anthropic's own documentation, they use Prettier as a PostToolUse hook example here [https://docs.claude.com/en/docs/claude-code/hooks-guide](https://docs.claude.com/en/docs/claude-code/hooks-guide) , which suggests they don't consider it a major concern.  
> > That said, I think the practical impact for Prettier specifically is minimal in most cases since it only changes formatting, and if code is already mostly formatted, the diffs are small.
> > 
> > But you make a fair point about token efficiency. For readers who are really context-constrained or working with massive files, running formatting on Stop instead of PostToolUse could be a smart optimization. I'll add a note about this tradeoff in the post.
> > 
> > > **lucianw** • [7 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2cxm7/) •
> > > 
> > > As to why Anthropic mentioned it, I don't know (maybe it was a cool idea at the time or maybe they're fixated on small documents), but here's what I observed from users in my company. This is a real transcript.
> > > 
> > > (1) USER MESSAGE.
> > > 
> > > - (There had been a previous conversation which got auto-compacted, and so the summary was inserted into the first user message)
> > > - The user's actual prompt was "In @ file.js please change function foo". Claude's behavior for @ file mentions is to insert the full file contents, in this case 4025 lines
> > > - (As always, the content of CLAUDE.md gets inserted into the first user message)
> > > 
> > > (2) ASSISTANT MESSAGE. Just a `Read()` tool use to read 30 lines from that file
> > > 
> > > (3) USER MESSAGE.
> > > 
> > > - Tool result with those 30 lines
> > > - But also, prettier kicked in, so Claude inserted a 1890 line <system-reminder> of the lines that were modified
> > > 
> > > (4) ASSISTANT MESSAGE. Just an `Edit()` tool use to make a small edit
> > > 
> > > (5) USER MESSAGE. Tool result of just a few lines showing the result of that edit
> > > 
> > > (6) ASSISTANT MESSAGE. Another `Read()` to read 100 lines from that file
> > > 
> > > (7) USER MESSAGE.
> > > 
> > > - Tool result with those 100 lines
> > > - But also, prettier kicked in, so claude inserted a 1626 <system-reminder> of the lines that were modified.
> > > 
> > > At this point there had been only three rounds with the LLM, we didn't even manage to finish a single user prompt through to the StopHook, and we already hit 160k token context -- which exceeds the limit of 200k tokens minus 45k tokens reserved for compaction.
> > > 
> > > I think that Claude's diffs are rarely well formatted according to strict prettier and rustfmt settings. Also, the way system-reminders are done in Claude, if there was a small formatting change near the top and a small formatting change near the bottom, Claude's "diff reconstruction" algorithm turns that into a <system-reminder> that encompasses the ENTIRE RANGE of what was changed.
> > > 
> > > As another example, in my company we enforce autoformat for all files. Claude loves to spit out markdown files (and we encourage it to when we're writing plans, or having it do research). So Claude produces 300 lines of really valuable content, and then autoformat kicks in to reformat that into 600 lines with word-wrap at 80 characters wide, and Claude gets a <system-reminder> that the file has changed on disk and gets the entire context spat back at itself.
> > > 
> > > > **JokeGold5455** • [6 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2h1ak/) •
> > > > 
> > > > Wow, that is very interesting information. Thank you so much for taking the time to write such a detailed reply. I really appreciate it. I'll update my post shortly.
> > > > 
> > > > > **lucianw** • [6 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2jzgn/) •
> > > > > 
> > > > > There's another bit from Anthropic docs which I love, and applies here: [https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices#concise-is-key](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/best-practices#concise-is-key)
> > > > > 
> > > > > "The context window is a public good."
> > > > > 
> > > > > And then for each token it gets, "Does this paragraph justify its token cost?". (It's talking about paragraphs within [SKILLS.md](http://skills.md/) files right here, but I think the same sentiment applies to the tokens it gets from file-change notifications).

> **Avidium18** • [19 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyjj29/) •
> 
> Wow 🤯
> 
> > **ArcyRC** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzo5dg/) •
> > 
> > Wow. WOW!
> > 
> > > **mrcaumartin** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm11bs4/) •
> > > 
> > > Wow. WOW! Much Wow 🤯
> > > 
> > > > **Important\_Place2514** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm49sii/) •
> > > > 
> > > > Wow. Wow. Wow. Wow

> **Zulfiqaar** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlysd10/) •
> 
> Fantastic post. Looks like its about time I setup hooks. I've had some very significant improvements by just putting core rules in CLAUDE.md but the meta-analyser would all but erase UI framework errors in my projects.

> **painvader** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz1z9x/) •
> 
> Can you share some repo’s? Seeing a working repo with this entirely setup helps more than just the post with theory

> **purposelycacophonic** • [5 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2lyep/) •
> 
> You're absolutely right!

> **PettyHoe** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzqh5g/) •
> 
> Have you looked at something like spec-kit from GitHub, and how that might augment your flow. They are very much overlapped but spec-kit is more general towards software development.
> 
> This would allow something that is potentially more transferrable across human/LLM.
> 
> Either way, great writeup and contribution. I'll be looking into how I can augment my and our orgs process from your experience.

> **ToiletSenpai** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlylfu2/) •
> 
> Thanks for all the quality info. This is gold

> **0sko59fds24** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyn5yq/) •
> 
> share hook pls

> **AlDente** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzaqwu/) •
> 
> It looks like I need to learn about hooks and using skills properly.
> 
> Amazing post!

> **whats\_a\_monad** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzw073/) •
> 
> What is the point of that complicated skills hook system? The entire skills system is designed so that it can lazy load context based on the skill description. Is that not working for you?
> 
> If you need context to always be loaded based on file paths, do the proper thing and put it in a CLAUDE.md in that directory
> 
> > **lucianw** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0yzsi/) •
> > 
> > Strong disagree. Skills and tools only ever have "LLM-instigated use of a feature".
> > 
> > It's a COMMON problem that LLMs aren't making the right call on whether or not to use a feature (use a tool, use a skill).
> > 
> > Anthropic already use hooks to remind the LLM that it should use the TodoWrite tool. OP has applied the exact same technique that Anthropic are already using, not just for TodoWrite, but also for other tools+skills.
> > 
> > > **PaulRBerg** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nmg0zp3/) •
> > > 
> > > Fingers-crossed that future LLMs will be intelligent enough to not need so much hand-holding

> **kikkoman23** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzyb2h/) •
> 
> So the skills and sub agents seem to cross maybe. Although I think sub agents are for parallel work. And skills are things that CC should pickup and know to use via natural language.
> 
> So instead of explicitly using slash commands. You promote and CC knows to use it.
> 
> Also funny how prior to code assist you’d had Git Hooks you can setup to do similar like linting ts code. But now we just go thru CC to do it. Keep it in one place.
> 
> But I assume you use latest Anthropic model. Thinking the sub agents and skills don’t work on older models like 3.7. This is a limitation of work models.
> 
> Awesome write up and appreciate you sharing!

> **dradik** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm04gk2/) •
> 
> I’ve had success with a skill that dynamically pulls my development standards using code execution.
> 
> All my standards are maintained as individual documents in a central repository outside of the project (e.g., data\_handling.md, uiux\_guidelines.md, desktop\_uiux.md, anti\_patterns.md). When I update my preferences, I just update these files.
> 
> When triggered, the skill executes a script. This script first reads only an index file from the repo. This index tells the script which standard documents to use for the current context. The skill then executes a script to read contents of that relevant standard.
> 
> I do this to onboard my agent and it ensures my rules are consistently enforced, the context is always pulled from the latest version in my repo, and only the exact standards needed for a given task are loaded it’s context.

> **WestminsterNinja** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm06nyp/) •
> 
> This post was pretty exciting to read. Thanks!

> **johannthegoatman** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm1qnmf/) •
> 
> GOAT post. Appreciate it immensely

> **Blackwater\_7** • [9 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlywsid/) •
> 
> chatgpt summarize this and tell me what this user is yapping about

> **lasajo2771** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlywjed/) •
> 
> Show me your code broham.

> **Ok\_Lettuce\_7939** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyp9us/) •
> 
> Thank you OP for all the legwork and detailed analysis! Just for my own curiosity what is your background?

> **dashingsauce** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyxgaj/) •
> 
> PARKOUR

> **blakeyuk** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyzb7a/) •
> 
> Awesome, thanks for sharing. I think most seasoned devs come to the same conclusion (plan, document, custom prompts for specific uses) but the variety of ways we all get there is amazing.

> **CuriousLif3** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz03zs/) •
> 
> Bro we are the same lmfao even the start comment on reader. I use speechify but am looking to the options you mentioned

> **villagezero** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzjfpd/) •
> 
> I’m by no means a dev let alone a junior but have been tinkering on building an app and some of your points hit home especially the ones of “humans just getting it” faster albeit with the knowledge gap of mine. I’ve often felt that if I could just keep CC semi-aware of its previous iterations or have it track at least a previos prompt or more it would reduce its amnesia and save precious tokens.
> 
> I’m not smart enough to understand all of it and I’ll probably use CC to eli5 it but on the surface it sounds like skills+ hooks and having specialized agents would help tremendously.
> 
> My apologies for not adding much to the convo but thank you for the suggestions.

> **bernieth** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzpsnc/) •
> 
> So awesome to see someone else's workflow in this detail, thank you! I'm using similar strategies on a smaller project (~20k lines) in the Cursor workflow (the main model has been Gemini 2.5 in Max mode). At a high level, all the same conclusions, strategies, and great results. Cursor rules allow you to match rules files with file globs, which substitutes for the skills hooks. For most of my career, the path to success was "more agile" because of the slowness of human teams. Now with AI, it's "more waterfall" with refinement of up-front designs first, and keeping those docs up to date through the project -- to keep that amnesiatic army of junior devs in line as they pump out code, tests, docs, utilities, and all the good stuff I could never afford the time to do before. Again, thanks for sharing!

> **musictechgeek** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0ix6h/) •
> 
> Excellent post. I just used this to add several enhancements to my Home Assistant-specific implementation of Claude Code. I built the skills auto-activation system you described: created four domain-specific skills for my setup (automations, Node-RED flows, ESPHome devices, and legacy system integrations). I added the UserPromptSubmit hook with skill-rules.json to detect when each skill is relevant. Now when I'm working on something, the right guidelines will load automatically. This will be a game changer for keeping Claude focused and consistent.
> 
> Thank you!

> **ragnhildensteiner** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0s2wm/) •
> 
> With so much work going into it that it needed 50 pages to explain the whole thing, did you actually save any time compared to manually coding the thing?
> 
> This sounds like one of those 1000h went into over-engineering tools, systems and processes and 10h of actual work type deal.

> **radshot84** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm1c1wb/) •
> 
> Appreciate the write up and everyone should keep in mind that there is a disclaimer that qualifies this is not a vibe bibble.
> 
> I would suggest Chrome DevTools MCP for frontend debugging. It provided the same aha efficiency as what you found with PM2 for backend.

> **TFT\_TheMeta** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm1t3ow/) •
> 
> Nice work!

> **WinterFox7** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm1tvue/) •
> 
> How much are you spending per month on Claude Code API usage?

> **RepoBirdAI** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2b2bc/) •
> 
> Recommending github speckit for claude code or any spec driven development for more robust, context aware, aligned coding.

> **Desperate-Ninja9194** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2c4v6/) •
> 
> This post is the best example of how Reddit can be used efficiently by communities of like minded people.
> 
> Loved it, thanks
> 
> Would be super awesome if you can also share the repo

> **Ellipsoider** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2nbcb/) •
> 
> Fantastic treasure trove of information. Thank you very much.

> **rieferX** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2qbpo/) •
> 
> Thanks for sharing! !remindme 1 month

> **Dtaild** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm2qffq/) •
> 
> TYFYS

> **ResponsibilityDue530** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm3udoq/) •
> 
> Who tf has time to read this shit? 🤣 I got bored scrolling.

> **ArielCoding** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm55dd7/) •
> 
> I have the same problem you solved with pm2 from a different angle. I’m giving Claude access to data from multiple sources, but it runs out of tokens. I’m thinking of consolidating all sources into a data warehouse using Windsor.ai, making some optimized tables, and giving Claude access to them instead.

> **Current-Usual-24** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm5kgnt/) •
> 
> Holy moly dude. This is really interesting and impressive.

> **bhupesh-g** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm5krxb/) •
> 
> Many people have shared their workflows, all are appreciated for their efforts and sharing but this is best system I have seen and aligned with my thoughts as well. Thanks for sharing

> **No\_Swordfish1677** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm65bqe/) •
> 
> wow , it's amazing, it helps me !!

> **Necessary-Cloud9881** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm6bqxf/) •
> 
> OP, a newbie AI train commuter here - I will be right back.

> **fsharpman** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm6br66/) •
> 
> Thanks for creating this. SWE here too. Was skeptical at first because there's a lot of AI slop posts here where people are trying to promote a bloated tool or overengineered workflow like BMAD.
> 
> Then as I kept reading, I noticed you have a lot of the lessons learned and underrated tricks that most people overlook. Including the ease of pressing escape twice and iterating on your own prompt.
> 
> You also clearly know what you're talking about because most people on here don't bother to turn to the docs for best practices.
> 
> I don't have the attention span to absorb everything you wrote in one sitting. But this post was good enough for me to carve out an hour of my day later to parse this, try to interpret some of your details, and see how I could adopt them.
> 
> (I have a project written in React Remix 1 where I was planning to do something similar to what you did, but rewritten in NextJS). Mainly the stuff around combining hooks with Skills.
> 
> I do think a major caveat to what you shared is you mentioned you have to know exactly what you want. And what you're trying to do. I don't think most people do. They just defer to a plan, and trust the code works. Which is why I think all of this sounds great for a rewrite. But for vibecoding, building new features, or starting a greenfield project where there are no new patterns and you're architecting them as you go, I'd be curious how you'd change some of this.

> **odarkshineo** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm6yq7c/) •
> 
> This is AMAZING, thank you so much! The number of comments that don't understand the insight offered here is astounding.

> **TinyDancer218** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm710b1/) •
> 
> thanks for this... I copied & pasted your post to Claude Code and told it to incorporate appropriate parts of your post to our project, and it is. Awesomeness... one of the many reasons I love Reddit.

> **\_yemreak** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nmeiqj1/) •
> 
> Wow, that's crazy! Is anyone else wondering what's going on here? What's this guy coding? I really want to see the result / the product. That's absolutely nuts! I might actually buy something if it's useful for me. This is seriously mind-blowing!
> 
> I also experienced the same concept on the journey. (pm2, cli tools, ts-morph, using types as docs, hooks, mapping intents, etc.) Finally I see someone I'm looking for
> 
> Tell me, How can I support / help YOU, what's the bottleneck u faced

> **bilboismyboi** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nmib6bx/) •
> 
> Very well, and thorough. Really appreciate this. One of the best guides I've come across. Wondering why the skills were not auto picked? Isn't that the official claude way? So with hooks it's just like manually injecting the skill prompt in your context, right?
> 
> > **JokeGold5455** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nmjwsqo/) •
> > 
> > Yeah, it's supposed to be automatic, but unfortunately I couldn't get it to work that way no matter what I did. I tried using exact keyword matches and still had no luck. I had Claude research skills thoroughly and when I asked why it wasn't automatically triggering them, it basically said, "I don't know, you did everything right and I still didn't use the skill." So the hooks are a workaround to make it work until Anthropic figures out how to make them more reliable.

> **mynameismati** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nmtpdib/) •
> 
> Nice job dude, thanks for sharing, really interesting and high quality insights. The combination of elements provided by claude you made is really interesting, the hooks approach caught my attention the most and surely I'll implement this. Will check your repo tomorrow, thanks

> **Spatialsquirrel** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nn7wg2b/) •
> 
> Thank you so much — I honestly don’t know how to thank you enough. Not only has your repo helped me understand how hooks, agents, and skills work, but it’s also improved my development workflow tremendously. Now I can focus on writing much more detailed tasks without repeating myself all the time. I don’t have to restate the same things thousands of times, and the context persistence in dev/active works perfectly. When other solutions didn’t work for me… yours did. Thank you again!
> 
> PS: Off the back of this, I’ve started building my own skills, agents, and commands, and writing custom hooks around my own structure. Absolutely fantastic.

> **bobafan211** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nndt0m8/) •
> 
> Love the systemization here. Big +1 on skills and docs. I’d add: keep a small “definition of done” file per feature so the agent can self-check.

> **Ok\_Paper1017** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/noec4qq/) •
> 
> This is awesome! I am going to have claude take a look at this and fine tune it for my project. I have been working on something like this one step at a time. This puts that process on steroids! Thanks for sharing.

> **clduab11** • [2 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nogptpr/) •
> 
> Every time I see a thread about how "AI is gonna take over everything", and then those same people in the same breath say "I'm not reading that lol", **especially when this post cracks Claude Code and it's what SWEs have been doing for months to those paying attention to it**, makes me remember people in AI are gonna be just fine lmao.

> **Veloder** • [3 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0dmwc/) •
> 
> TLDR from Claude:
> 
> After 6 months refactoring 100k to 400k LOC, the author built a TypeScript hooks system that auto-injects relevant coding guidelines into Claude's context and a dev docs workflow (plan, context, tasks files) that prevents Claude from losing focus mid-implementation. These systems dramatically improved consistency by forcing Claude to follow established patterns rather than hoping it remembers them.

> **jedenjuch** • [1 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlzrh02/) •
> 
> I’m not gonna read this ai crap
> 
> > **lucianw** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm0yip1/) •
> > 
> > This isn't AI crap. It's a really good post. I've been coding pretty much the same things within my enterprise (keywords, hooks, ...) since supporting AI devtools is my day job. This is the first time I've seen a public statement of it.
> > 
> > > **jedenjuch** • [4 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm17426/) •
> > > 
> > > I read it, cool post

> **UsefulEntry9764** • [1 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlyya4n/) •
> 
> .

> **thatsalie-2749** • [1 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nlz1vdj/) •
> 
> Awesome

> **nicobaogim** • [1 points](https://reddit.com/r/ClaudeAI/comments/1oivjvm/comment/nm128xh/) •
> 
> Thank you this is gold.