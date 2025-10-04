---
title: "Code Review Checklist: Follow My 4-Step Process"
source: "https://josipmisko.com/code-review-checklist"
author:
  - "[[Josip Miskovic]]"
published: 2023-03-05
created: 2025-10-01
description: "In this article, I'll give you my code review checklist, explain how I created it, and why it's important."
tags:
  - "clippings"
---
In this article, I'll give you my [code review checklist](https://josipmisko.com/#code-review-checklist), explain [how](https://josipmisko.com/#what-does-the-code-review-checklist-cover) I created it, and [why](https://josipmisko.com/#why-use-code-review-checklists) it's important.

Lately, I've been obsessed with finding ways to improve software quality. My research found that [code reviews](https://josipmisko.com/code-reviews) are the best way to find software defects.

Code reviews find 50-60% of software defects, while the next best method, integration tests, find 45%.

But there's a big difference there. Integration tests are based on code, while code reviews depend on human interaction. The code review quality can vary a lot based on the reviewer.

How can we maximize the code review quality across the team?

→ **Code Review Checklist**

![](https://josipmisko.com/img/code-review/code-review-checklist-effectivness.webp)

Using a code review checklist [showed](https://link.springer.com/article/10.1007/s10664-022-10123-8#Sec27) significantly better efficiency than not using one.

A code review checklist is a step-by-step guideline that defines what truly matters in a code review.

**Complete Code Review Checklist:**

## 1\. Clarity and Shared Understanding

| Question | Pass |
| --- | --- |
| How easy is it to understand the code? From 1 to 10. |  |
| Does the code read from top to bottom? |  |
| Do all variables and functions have clear names? |  |
| Any redundant comments or commented-out code? |  |
| Are if/then, else, and switch statements easy to follow? |  |
| Are all the changes relevant? |  |

## 2\. Implementation

| Question | Pass |
| --- | --- |
| Is the code following best practices of the programming language or framework? |  |
| Does the code anticipate overflow or underflow? Divide-by-zero errors? |  |
| Are null checks in place for all nullable types? |  |
| Are collections checked for out-of-range indexing? |  |
| Do loops end under all possible conditions? |  |
| Is the code designed to fail gracefully? |  |
| Does a function or procedure alter a parameter that is only meant as an input parameter? |  |
| Does the code avoid magic numbers? |  |
| If adding 3rd party packages, are they properly vetted for performance, security, and licensing? |  |

## 3\. Security

| Question | Pass |
| --- | --- |
| Are credentials stored in an encrypted format? |  |
| Is code logging sensitive information (personal information, passwords, API keys)? |  |
| Are SQL queries parameterized to prevent **SQL injection**? |  |
| Is all input data and rendered data validated to prevent **Cross-Site Scripting (XSS)**? |  |
| Do forms use Cross-Site **Request Forgery (CSRF)** tokens? |  |
| Does code or APIs reveal secret information? |  |
| **Authentication**: Should new functionality be available to unauthenticated vs. authenticated users? |  |
| **Authorization**: Does the new functionality separate user boundaries? Should a user be allowed to do that? |  |

## 4\. Performance

| Question | Pass |
| --- | --- |
| Are ther any expensive operation inside a loop? |  |
| Is there heavy use of memory? Memory leaks, reading data into memory, in-memory caching? |  |
| Is the choice of the algorithm optimal? |  |
| Are database calls optimized to pull only the necessary data? |  |
| Are resource-heavy operations cached? |  |

## Why use code review checklists?

**Use review checklists because history has proven that they work.**

In 1935, the US Army Air Corps was purchasing long-range bomber aircraft. The Boeing Model 299 was the most advanced among the contenders, with greater capacity for bombs, speed, and range.

![](https://josipmisko.com/img/code-review/Boeing-Model-299-crash.webp)

Despite the initial evaluations favoring the Model 299, the test flight ended in a fatal crash.

It was the most advanced aircraft. What happened?

**Human error**. The pilot had forgotten to release the locking mechanism on the airplane's elevator controls.

Luckily, the US Army didn't give up. They bought 12 Model 299s for testing.

To ensure the same errors don't happen, they developed four checklists covering:

- takeoff,
- flight,
- before landing, and
- after landing.

Most importantly, they taught all pilots how to use them.

**Outcome**:

- The planes went on to fly almost 2 million miles without any major issues.
- The Army ordered +13,000 of the aircraft, known as the B-17, which proved vital during World War II.

![Graph of Fatal Accidents per Year in Aviation, 1946–2021, and 5-Year Moving Average](https://josipmisko.com/img/code-review/aviation-fatal-accidents-peryear-1946%E2%80%932021.webp)

Aviation: Fatal Accidents per Year, 1946–2021, and 5-Year Moving Average

Checklists were also key to the success of the Apollo moon landings, with astronaut Michael Collins calling them "The fourth crew member."

![Apollo 16 Checklist](https://josipmisko.com/img/code-review/apollo-16-checklist.webp)

The checklist from Apollo 16 mission

Checklists turned out to be crucial for all major industries, including medicine.

Peter Pronovost developed medicine's first checklist for safely inserting a central line into a patient's chest. After 15 months of using it, hospitals cut their infection rate from 4% to zero, saving 1,500 lives and nearly $200 million.

![Peter Pronovost's checklist](https://josipmisko.com/img/code-review/pronovost-checklist.webp)

Peter Pronovost's checklist

## What does the code review checklist cover?

I've created this code review checklist based on many Computer Science studies.

Here are the 4 main areas that the checklist covers:

### 1\. Clarity and Shared Understanding

Researchers from IBM and Carnegie Mellon University did a [quantitative analysis of code review comments](https://arxiv.org/pdf/2204.00107.pdf).

They found that asking for clarification was the most common code review comment.

From my experience, I also believe that code clarity and a shared understanding of code are crucial outcomes of the code review process.

Change is inevitable in software development.

Make it easy for yourself: Write code that's clear to understand now, so you save yourself a headache later.

### 2\. Implementation

Now that we underhand the code, we need to make sure that it does what it's supposed to do.

The paper *[Expectations, Outcomes, and Challenges of Modern Code Review](https://sback.it/publications/icse2013.pdf)* reveals that finding defects and code improvements are the most important motivators of the code review process:

![Bar Chart showing Ranked Motivations from Developers when performing Code Reviews](https://josipmisko.com/img/code-review/code-review-motivations-for-developers.webp)

Bar Chart showing Ranked Motivations from Developers when performing Code Reviews

Based on these goals, the "Implementation" checklist is focused on:

- Coding best practices for the given programming language
- Finding defects (bugs)
- Alternative solutions that are faster, more secure, or simpler

### 3\. Security

Changes are high that one of the PRs will include a security vulnerability:

- 84% of codebases contained at least one vulnerability
- 48% of codebases contained high-risk vulnerabilities

Security is so important that it's even a separate branch of code reviews, *secure code reviews*.

The goal of a secure code review is to ensure that a penetration test does not discover any additional vulnerabilities.

![Codebase vulnerability graph](https://josipmisko.com/img/code-review/codebases-vulnerability-graph.webp)

Codebase Vulnerability percentages since 2018.

### 4\. Performance

Performance has a direct impact on both user experience and spending.

Performant code saves money because it uses less CPU, memory, disk, and network bandwidth.

Performance defects are hard to spot during a code review process. It's more about being suspicious and identifying code that could be low-performing. If we see such a code, it's a candidate for further testing.

We should not try to optimize software without proper measurements.

![Josip Miskovic](https://josipmisko.com/_next/image?url=%2Fjosip-miskovic.jpg&w=128&q=90)

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