---
title: "12 Code Review Best Practices [2023]"
source: "https://josipmisko.com/code-review-best-practices#bonus-code-review-security-checklist"
author:
  - "[[Josip Miskovic]]"
published: 2023-02-26
created: 2025-10-01
description: "Here are some of the code review best practices that I've learned over the years that will boost your code quality.\""
tags:
  - "clippings"
---
## Key Takeaways

- Establish a standard for code quality.
- Be a human: Conform to principles, not opinions.
- Foster psychological safety by not measuring developer performance based on defects.
- Prioritize quick reviews while still being rigorous with critical parts of the system.
- Mentor or be mentored through various forms of peer code reviews.
- Automate tests, linting, formatting, and analysis to save time.
- Send nudges to reviewers if necessary.

We all know that [code reviews](https://josipmisko.com/code-reviews) are key to creating quality software.

Unreviewed code is 2x more likely to contain defects than reviewed code.

> Given enough eyeballs, all bugs are shallow. - Linus Torvalds (Linus's law)

But how to do a code review? How to make it effective?

Here are some of the **code review best practices** that I've learned over the years:

## 1\. Set the code review standard

Code review enforces a code quality bar.

But how to meet that code quality bar if it doesn't exist?

First, we need to create an established list of **code quality standards**.

Based on your standards, you can create [code review checklist](https://josipmisko.com/code-review-checklist).

Here are some questions that I use to help establish a code review quality standard:

#### 1\. Programming language standards

- Is the code following the best practices of the programming language?

#### 2\. Security standards

Every developer should follow security best practices, such as OWASP Top 10.

There's even a branch of code review practices that focuses on code reviews:

**Secure code review** audits an application's source code to identify security flaws. The process ensures that proper security controls are in place.

See: [Code review security checklist](https://josipmisko.com/code-review-best-practices#bonus-code-review-security-checklist)

#### 3\. Clarity Standards

- How easy is it to understand the intent?
- Is the new code consistent with the old one?
- Is it easy to maintain: change, remove, modify?

#### 4\. Reusability standards

- Is the code easy to reuse?
- Is the code overcomplicated because of the intent to be reused, but it will never be?

#### 5\. Performance standards

- How does the new code impact response times?
- Does it have leaks that could impact memory, CPU, and disk space?
- How does it score on benchmarking tools? (for example, Core Web Vitals for web applications)

#### 6\. Testability standards

- Is the new code covered by unit and integration tests?

#### 7\. Code format standards

- Use linters and formatters (ESLint, Prettier) to enforce code style.

#### 8\. Documentation standards

Some development teams document everything, others not much. It depends on your project.

- Is there related wiki documentation, comments, or descriptions?

---

You can use your quality standard to create a concise code review checklist that development team can reference.

### What's important in a code review?

To set a code review standard, we need to define what's important.

[Microsoft's survey](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/05/MS-Code-Review-Tech-Report-MSR-TR-2016-27.pdf) found out that code improvement, finding defects, and knowledge transfers are top 3 reasons for doing a code review.

| Reason for Code Reviewing | Score | Overall Rank |
| --- | --- | --- |
| Code improvement | 2835 | 1 |
| Find defects | 2749 | 2 |
| Increase knowledge transfer | 1528 | 3 |
| Find alternative solutions | 1199 | 4 |
| Improve the development process | 979 | 5 |
| Avoid breaking builds | 957 | 6 |
| Build team awareness | 790 | 7 |
| Lead to shared code ownership | 717 | 8 |
| Team assessment | 235 | 9 |

## 2\. Be a human

As a **reviewer**, know that you are reviewing code, not the person.

Explain why you suggest a change or improvement. Developers are more likely to take your advice if they understand the *why*.

Don't just criticize; aim to build credibility with constructive comments.

---

As a **reviewee**, sending your code out there for review puts you in a vulnerable state.

Remember, they are reviewing the code, not you.

Also, don't forget that the people reviewing your code are also human.

Be humble, courteous, and patient when you receive a review.

Take in both positive feedback as well as negative criticism in stride. Stay open-minded, and remember that everyone is trying to make the project better.

---

What happens when two developers disagree on a code change?

The development team should have a process in place for resolving conflicts between the reviewer and developer.

**Technical disagreement should not turn personal.**

## 3\. Make the code review short

- **Don't review too much code at once** (<200-400 LOC). Defect density decreased dramatically when the number of lines of code under inspection went above 200.

![](https://josipmisko.com/img/code-review/code-review-effectivness.webp)

- **Take your time (<500 LOC/hour)**. Reviewers who went through the code at rates above 1000 LOC/hour probably weren't looking at the code.
- **Spend less than 60 minutes reviewing**. Performance starts dropping off after 60-90 minutes.

![A chart showing defects per minute discovered while doing a code review](https://josipmisko.com/img/code-review/code-review-defects-per-minute.webp)

Keep your code review sessions shorter than an hour.

## 4\. Conform to principles, not opinions

Software development is a craft, so every developer should be opinionated.

But separate opinions from principles.

Opinions are subjective and not always right. The best way to avoid being opinionated is to stay with agreed-upon principles.

These can be language-specific or project-wide quality standards that the team has set up and agreed upon.

Give your opinion, but don't make it a pull request blocker.

![Code Review Typo Meme](https://josipmisko.com/img/code-review/code-review-typo-meme.webp)

Code Review Typo Meme

## 5\. Review your code before sending it out for a review

Most IDEs show a code difference view and allow you to review the changes.

Take a step back and look at your code with a critical eye.

Fix any issues before sending the code out for peer review.

It saves time for everyone, but it also helps you develop your code-reviewing skills.

![VS Cod Diff Compare](https://josipmisko.com/img/code-review/vs-code-diff-compar.webp)

VS Cod Diff Compare

## 6\. Foster psychological safety

In 2012, a group of Google employees set out to figure out what makes teams successful.

They [found](https://www.nytimes.com/2016/02/28/magazine/what-google-learned-from-its-quest-to-build-the-perfect-team.html) that the difference between high-performing teams and dysfunctional ones was how team members treated each other.

The number one factor for a successful team was psychological safety.

Psychological safety is the belief that one will not be punished or humiliated for making a mistake.

**Don't measure developer performance based on the defects identified during code reviews. It can only create a sense of threat and hostility.**

Instead, use code reviews to learn from each other.

## 7\. Move fast and don't break things

In 1976, Michael Fagan from IBM [introduced](https://ieeexplore.ieee.org/document/5388086) the formal code review process.

The code review ceremony would go on for weeks.

Compare that to today:

[Research at Meta](https://users.encs.concordia.ca/~pcr/paper/NudgeBot2022FSE-preprint.pdf), showed that they complete reviews in a median of 2.5 hours. And around 75% of them they complete in under 24 hours.

When you are in a time crunch, prioritize quick reviews for non-critical changes. This approach avoids blocking other developers' work.

But, for critical or consistently buggy parts of the system, a rigorous review is still necessary.

## 8\. Choose people to notify

Choose code reviewers based on their:

- expertise in a given programming language
- domain-specific knowledge of the codebase
- availability

Pick wisely. Having too many reviewers leads to responsibility diffusion.

Responsibility diffusion is a phenomenon that occurs when multiple people are involved in a task and no one person feels accountable for its completion.

## 9\. Choose a good code review platform

[Microsoft surveyed](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/05/MS-Code-Review-Tech-Report-MSR-TR-2016-27.pdf) developers on the most important features of their internal code review tool, CodeFlow.

These features are most desired from a code review tool:

- Ease of use and performance
- Integration with static analysis, testing, and continuous integration tools
- Integration of coding style plugins and search
- Features for editing code during review and executing reviewed code
- Ability to create code change narrative and attach auxiliary information for context
- Support for discussion during review and integration with note-taking and documentation tools
- Templates for common code review comments
- Seamless integration with external communication tools
- Better notifications and tracking of feedback lifecycle

![GitHub code review features](https://josipmisko.com/img/code-review/github-code-review-tool-features.webp)

GitHub code review features

## 10\. Nudge code reviewers

We all know that feeling of waiting for a code review for days.

*Should I follow up or no? Am I being annoying?*

Meta [reduced the code review time](https://engineering.fb.com/2022/11/16/culture/meta-code-review-time-improving/) by 6.8% by introducing Nudgebot.

Nudgebot sends a chat ping to likely reviewers with context and quick actions to jump into the code review.

![Meta code review nudging notification](https://josipmisko.com/img/code-review/meta-code-review-notification.webp)

Meta code review nudging notification

There's a valuable lesson here.

You don't need a fancy machine-learning tool to send nudges.

Instead, make sure to follow up with reviewers every couple of hours.

And don't worry about being annoying:

At Microsoft, 73% of nudges get a positive rating.

## 11\. Automate tests, linting, formatting, and analysis

Automating a portion of the code review process will save you 30% of the time.

Most code review tools (GitHub, GitLab, Azure DevOps) let you run test analysis as part of pull requests.

You can configure a policy that prevents merging if unit tests, functionality tests, or test coverage fails.

You can also use tools to enforce code styles:

- **Formatters** enforce consistent code style and formatting rules and improve readability without affecting functionality. (example: Prettier and Black)
- **Linters** perform static analysis on source code to identify code patterns that might lead to errors. (example: ESLint and Pylint)
- **Code analysis tools** like SonarQube analyze code and provide metrics for your code base, detecting bugs, code smells, and potential vulnerabilities.

Formatters and linters are mostly free, code analysis tools are not.

Formatters and linters help you focus on what matters, not the [nitpicks](https://josipmisko.com/posts/code-review-nit).

## 12\. Mentor or be Mentored

Are you a junior dev?

Code reviews are your #1 opportunity to grow.

Take the time to ask questions and learn from more experienced developers.

Try out other forms of peer code reviews such as:

- over-the-shoulder,
- pair programming,
- or formal inspections.

Over-the-shoulder and pair programming are the most effective way to do knowledge transfers.

---

Are you a senior dev?

Ask open-ended questions to guide the junior developers to find the best solution.

Don’t be afraid of providing constructive criticism.

Focus on explaining “why” something is wrong, not just what's wrong.

---

### Bonus: Code Review Security Checklist

| Vulnerability Type | Example |
| --- | --- |
| Race Condition | Improper synchronization of multiple threads accessing shared data. |
| Buffer Overflow | Reading or writing to a buffer without proper bounds checking. |
| Integer Overflow | Performing arithmetic operations on integers without checking for overflow or underflow. |
| Improper Access | Granting access to sensitive data or functionality without proper authentication or permission checking. |
| Command Injection | Constructing a command string using unvalidated user input. |
| Cross Site Scripting (XSS) | Outputting user-controlled data to a web page without proper encoding. |
| Denial of Service (DoS) | Performing computationally expensive or memory-consuming operations. |
| Deadlock | Two or more threads blocked, waiting for each other to release a resource. |
| SQL Injection | Constructing SQL queries using unvalidated user input. |
| Format String | Using unvalidated user input as a format string. |
| Cross Site Request Forgery | Not properly validating the origin of a request. |
| Common Keywords | General keywords that may indicate the presence of a vulnerability. |

![Josip Miskovic](https://josipmisko.com/yH5BAEAAAAALAAAAAABAAEAAAIBRAA7)

Josip Miskovic

About Josip

Josip Miskovic is a software developer at Americaneagle.com. Josip has 10+ years in experience in developing web applications, mobile apps, and games.

[Read more posts →](https://josipmisko.com/blog)

[Follow @JosipMisko](https://twitter.com/intent/user?screen_name=josipmisko)

**Published on:**

![](https://josipmisko.com/img/software-developer-career.jpg)

Download Free Software Developer
```
Career Guide
```

I've used these principles to increase my earnings by 63% in two years. So can you.

Dive into my **7 actionable steps** to elevate your career.