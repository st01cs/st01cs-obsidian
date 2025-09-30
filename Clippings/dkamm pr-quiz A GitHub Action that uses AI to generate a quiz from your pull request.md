---
title: "dkamm/pr-quiz: A GitHub Action that uses AI to generate a quiz from your pull request"
source: "https://github.com/dkamm/pr-quiz"
author:
  - "[[dkamm]]"
published:
created: 2025-09-30
description:
tags:
  - "clippings"
---
**[pr-quiz](https://github.com/dkamm/pr-quiz)** Public

A GitHub Action that uses AI to generate a quiz from your pull request

[MIT license](https://github.com/dkamm/pr-quiz/blob/main/LICENSE)

[Open in github.dev](https://github.dev/) [Open in a new github.dev tab](https://github.dev/) [Open in codespace](https://github.com/codespaces/new/dkamm/pr-quiz?resume=1)

## PR Quiz

## Intro

AI Agents are starting to write more code. How do we make sure we understand what they're writing?

PR Quiz is a GitHub Action that uses AI to generate a quiz based on a pull request. It can help you, the human reviewer, test your understanding of your AI Agent's code. (And block you from deploying code you don't understand!)

[![Demo](https://github.com/dkamm/pr-quiz/raw/main/assets/demo.gif)](https://github.com/dkamm/pr-quiz/blob/main/assets/demo.gif)

## Getting started

1. Make sure you have an OpenAI API Key and an ngrok auth token (free tier works).\*
2. Add the OpenAI API Key and ngrok auth token as action secrets to your repository (`settings -> secrets -> actions` in the UI)
3. Add the following `quiz.yml` to your `.github/workflows` directory
```
# quiz.yml

name: PR Quiz

on:
  pull_request_review:
    types: [submitted]

permissions:
  contents: read
  pull-requests: read

jobs:
  quiz:
    name: PR Quiz
    runs-on: ubuntu-latest
    environment: your-environment # TODO: change this to your actual environment
    # Only trigger on approvals to save tokens
    if: github.event.review.state == 'approved'

    steps:
      - name: Checkout
        id: checkout
        uses: actions/checkout@v4

      - name: Serve Quiz
        id: serve-quiz
        uses: dkamm/pr-quiz@v0.1.0
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          openai-api-key: ${{ secrets.OPENAI_API_KEY }}
          ngrok-authtoken: ${{ secrets.NGROK_AUTHTOKEN }}
```

\*The PR Quiz action creates a temporary webserver inside the GitHub Actions runner and uses ngrok to create a public tunnel to it

## Inputs

| Name | Description | Default Value | Required |
| --- | --- | --- | --- |
| github-token | GitHub token for API access | \- | Yes |
| ngrok-authtoken | The ngrok authtoken to use for the server hosting the quiz. | \- | Yes |
| openai-api-key | OpenAI API key for API access | \- | Yes |
| model | The model to use for generating the quiz. It must be a model that supports structured outputs. | `o4-mini` | No |
| lines-changed-threshold | The minimum number of lines changed required to create a quiz. This is to prevent quizzes from being created for small pull requests. | `100` | No |
| time-limit-minutes | The time limit to complete the quiz in minutes. This prevents the action from running indefinitely. | `10` | No |
| max-attempts | The maximum number of attempts to pass the quiz. A value of 0 means unlimited attempts. | `3` | No |
| exclude-file-patterns | A list of file patterns to exclude from the quiz as a JSON-ified string. | `'["**/*-lock.json", "**/*-lock.yaml", "**/*.lock", "**/*.map", "**/*.pb.*", "**/*_pb2.py", "**/*.generated.*", "**/*.auto.*"]'` | No |
| system-prompt | Optional override for the system prompt. Be sure the specify that multiple choice questions must be returned. | See [here](https://github.com/dkamm/pr-quiz/blob/main/src/quiz/DefaultSystemPrompt.js) for the default system prompt | No |

## Privacy

Because this action runs a temporary webserver inside the GitHub Actions runner, your code isn't sent to any third party other than the model provider (OpenAI). This action can be easily modified to work with self-hosted models as well.

## Releases 1

## Packages

No packages published  

## Languages

- [JavaScript 79.0%](https://github.com/dkamm/pr-quiz/search?l=javascript)
- [CSS 10.5%](https://github.com/dkamm/pr-quiz/search?l=css)
- [EJS 10.5%](https://github.com/dkamm/pr-quiz/search?l=ejs)