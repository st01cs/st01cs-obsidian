---
title: "AI Engineering in the real world"
source: "https://newsletter.pragmaticengineer.com/p/ai-engineering-in-the-real-world"
author:
  - "[[Gergely Orosz]]"
published: 2025-03-26
created: 2025-10-06
description: "What does AI engineering look like in practice? Hands-on examples and learnings from software engineers turned “AI engineers” at seven companies"
tags:
  - "clippings"
---
### What does AI engineering look like in practice? Hands-on examples and learnings from software engineers turned “AI engineers” at seven companies

AI Engineering is the hottest new engineering field, and it’s also an increasingly loaded phrase which can mean a host of different things to different people. It can refer to ML engineers building AI models, or data scientists and analysts working with large language models (LLMs), or software engineers building on top of LLMs, etc. To make things more confusing, some AI tooling vendors use the term for their products, like Cognition AI naming theirs an “AI engineer.”

In her new book “AI Engineering,” author Chip Huyen [defines](https://newsletter.pragmaticengineer.com/p/ai-engineering-with-chip-huyen) AI engineering as building applications that use LLMs, placing it between software engineering (building software products using languages, frameworks, and APIs), and ML engineering (building models for applications to use). Overall, AI engineering feels closer to software engineering because it usually starts with software engineers building AI applications using LLM APIs. The more complex the AI engineering use case, the more it can morph into looking like ML engineering.

**Today, we focus on software engineers who have switched to being AI engineers.** These are devs who work with LLMs, and build features and products on top of them. We cover:

1. **What are companies building?** An overview of seven companies at different stages and in various segments of tech.
2. **Onboarding to AI Engineering as a software engineer**. Approaches that help devs get up to speed faster.
3. **Tech stack**. Seven different tech stacks, showcasing variety and some common choices.
4. **Engineering challenges.** Problems caused by LLMs being non-deterministic, evals, latency, privacy, and more.
5. **Novel tooling.** Several companies build in-house tooling, which pays off with this fast-moving technology. Incident management startup, incident.io, shares their unique, bespoke stack.
6. **Cost considerations.** LLMs can quickly get expensive, although costs are dropping quickly. But as this happens, usage tends to grow which causes its own issues. Businesses share how big a deal costs really are.
7. **Learnings from software devs turned AI engineers**. Building a prototype is the easy bit, vibes-based development inevitably turns bad, smart teams fail because they get overwhelmed; educating AI users, and more.

*Note: I am an investor in incident.io and Wordsmith, which both share details in this deepdive. I always focus on being unbiased in these articles – but at the same time, being an investor means these companies share otherwise hard-to-obtain details. I was not paid by any business to mention them in this article. See [my ethics statement](https://blog.pragmaticengineer.com/ethics-statement/) for more.*

*Thanks to the engineers contributing to this deepdive: [Lawrence Jones](https://blog.lawrencejones.dev/) (senior staff engineer at incident.io), [Tillman Elser](https://www.linkedin.com/in/tillman-elser/) (AI lead at Sentry), [Ross McNairn](https://www.linkedin.com/in/rossmcnairn/) (cofounder at Wordsmith AI), [Igor Ostrovsky](https://www.linkedin.com/in/igoro/) (cofounder at Augment Code),* [Matt Morgis](https://www.linkedin.com/in/matthew-morgis-44015027/) *(Staff Engineer, AI, formerly at Elsevier), [Ashley Peacock](https://www.linkedin.com/in/ashley-peacock-133749120/) (Staff Engineer at Simply Business), and [Ryan Cogswell](https://x.com/ryanecogswell) (Application Architect at DSI).*

### 1\. What are companies building?

#### Incident.io: incident note taker and bot

[Incident.io](http://incident.io/) is a tool to help resolve outages as they happen. A few months ago, the engineering team went back to the drawing board to build features that capitalize on how much LLMs have improved to date. Two of these features:

- **AI note taker during incidents.** This includes live transcription, real-time summaries for people joining a call to get up to speed with, and key decisions/actions to clarify who does what.
- **Incident investigator:** an agent looks into an ongoing incident by checking code, logs, monitoring, and old incidents to identify root causes and share findings, with a responder being paged. More details on [how this tool is built](https://incident.io/building-with-ai).

Both these features make heavy use of LLMs, and also integrate with several other systems like backend services, Slack, etc.

![](https://substackcdn.com/image/fetch/$s_!QAEF!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ffcec9ab8-fa1e-4d85-9570-c4d9f08fa2bc_1600x879.png)

AI feature: when joining an incident, get a summary of what’s currently being discussed

#### Sentry: Autofix and issue grouping

[Sentry](https://sentry.io/) is a popular application monitoring software. Two interesting projects they built:

- **Autofix**: make it really fast to go from a problem with code (a Sentry issue) to a fix with a GitHub PR. Autofix is an open source RAG framework that combines all of Sentry’s context/telemetry data with code in order to root cause, fix, and create unit tests for bugs.
- **Issue Grouping:** cut down alerting volume while reducing noise. For this, the team used recent advancements in approximate neighbor search (ANN), plus dramatic recent improvements in embedding quality from the new BERT architecture transformer models.

Both these features are [fair source](https://github.com/getsentry/seer), meaning you can see exactly how they work.

![](https://substackcdn.com/image/fetch/$s_!wgHY!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff0569b70-50cb-4f63-84ff-2f4f18eefdf4_1498x1295.png)

Autofix identifies the root cause of an issue with a useless Stack Trace

#### Wordsmith: legal AI

[Wordsmith](https://www.wordsmith.ai/) is building AI tools that legal teams use, including:

- **Documents workspace:** plug into all of a company’s communication streams, including analyzing documents and augmenting their contents, and drafting communications. [Check out a video of it in action.](https://www.youtube.com/watch?v=UXrQ5WZzTG8)
- **AI contract review:** A product that can analyse any contract or website, then review it and generate a marked-up word doc, [here](https://app.wordsmith.ai/shared/reviews/f110ec32-759d-4f63-beee-d058a49a7175). Basically, it’s a lawyer anyone can use.

![](https://substackcdn.com/image/fetch/$s_!d0Nd!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F1942506b-a161-45bf-a823-e09490234691_1600x929.png)

AI contract review: AI tool detects, highlights and summarizes potential contractual issues

#### Augment Code

[Augment Code](https://www.augmentcode.com/) is an AI coding assistant for engineering teams and large codebases. This kind of product probably needs little introduction for devs:

- **AI coding assistant**: including IDE extensions for VS Code, JetBrains, Cursor, and Vim, and a Slack extension
- **Fine-tuning models**: for AI coding tools, models make a big difference. The team don’t pre-train models or build their own LLMs, but run extensive post-training and do fine tuning to suit the 4-5 models used for specific coding-related cases.

#### Elsevier: RAG platform

[Elsevier](https://www.elsevier.com/) is one of the world’s leading publishers of scientific and medical content. Matt Morgis was an engineering manager at the company when the engineering leadership noticed that several product teams were independently implementing [RAG capabilities](https://newsletter.pragmaticengineer.com/p/rag); each sourcing content, parsing it, chunking it, and creating embeddings.

**An enterprise-wide RAG platform** was the solution Matt and his team built, to enable multiple teams to build AI-powered products for medical and scientific professionals. Their platform consists of:

1. **Database**. A content database that centralized and normalized content from various sources.
2. **Embeddings+search:** A content embedding & indexing pipeline and vector search API.
3. **LLM API:** interfacing to multiple LLM models. This API allows teams to experiment with different models by changing a parameter on the API. It also allowed Elsevier to track the usage of various LLM models based on applications using it.

Products built on top of this platform:

- **Intelligent tutoring system** for medical students
- **Clinical decisions support tool** for doctors

#### Insurance company: chatbot

Ashley Peacock is a staff software engineer at the insurer, [Simply Business](https://www.simplybusiness.com/), who built a pretty common use case: a chatbot for customers to get answers to questions. This seems like the simplest of use cases – you might assume it just involves connecting documentation for the chatbot to use – but it was surprisingly challenging because:

- **Industry regulation.** The chatbot cannot be inaccurate or make things up, as customers use the information to make decisions about which insurance purchases.
- **Non-deterministic responses**. The business needed to turn a nondeterministic chatbot into one that only produces approved responses.

The team had the idea to create an “approved answers” knowledge base for the chatbot, and faced the challenge of creating the questions for this. The team made the chatbot state when it cannot answer a question, and to then connect with human support, which then updated the knowledge base with their solution. This approach works pretty well after taking a few iterations to get right.

#### HR SaaS: summarization features

[Data Solutions International](https://datasolutionsinc.com/) (DSI) is a 30-person HR tech company with 5 engineers, selling products that help with performance review processes, assessments, and employee engagement surveys. The company is family-owned, has been operating for 27 years, and is profitable.

**Summarizing comments for employee engagement processes** was the first feature they wanted to build, as something customers would appreciate, and which the team could learn about working with LLMs from.

During an employee engagement process, there are questions like "what do you like most about working here", and "if you could change one thing about working at Company X, what would it be?", etc. For larger companies with thousands of employees, there may be thousands of comments per question. Individual departmental leads might read all comments relevant to them, but there’s no way an HR team at a very large business could check every single comment.

Before LLMs, such comments were categorized into predefined categories, which were hardcoded, per company and per survey. This was *okay*, but not great. Data Solutions International’s goal was to use LLMs to summarize a large number of comments, and report to survey admins the broad categories which comments belong in, how many comments per category there are, and to allow drilling down into the data.

![](https://substackcdn.com/image/fetch/$s_!3RGV!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F9871893a-4a76-48ee-919d-71f457c55e2e_1600x734.png)

Summary of teamwork-related comments: The feature builds a word cloud of common topics from thousands of comments, and provides an overview of any term

### 2\. Onboarding to AI Engineering as a software engineer

So, how do you get started building applications with LLMs as a software engineer transitioning to this new field? Some advice from folks at the above companies who have:

#### You can teach AI yourself – and probably should

Let’s start with an encouraging story from veteran software engineer [Ryan Cogswell](https://x.com/ryanecogswell), at HR tech company, DSI. He joined the company 25 years ago, and was the first engineering hire. When AI tools came along, DSI decided to build a relatively simple first AI feature in their HR system that summarized comments for employee engagement purposes. Neither Ryan nor any of the other 4 devs had expertise in AI and LLMs, so the company contracted an external agency which offered a fixed, timeboxed offer to scope the project. Here’s how it went:

- Month #1: the agency goes and builds stuff, and shares LLM outputs with DSI
- Month #2: while continuing to iterate on desired outputs, devs at DSI ask the agency for access to how things work. They get access to scripts and notebooks
- Month #3: the agency lays out the proposed architecture for the project.

The proposal was for a really complex architecture:

- **SageMaker**: a heavyweight solution from AWS to build, train, and deploy ML models
- **Langfuse:** an open source LLM engineering platform to debug and improve LLM applications
- **Lambdas:** serverless functions to run computations
- **Database #1:** store interim states of data between prompts
- **Database #2**: storing user feedback
- **Other parts:** to support RAG aspects
- **Pipings**: to hold it all together

The agency quoted 6-9 months to build the relatively small feature (!!), and an estimated operational cost higher than DSI’s entire investment in all their infrastructure! This was when Ryan asked how hard it could be to build it themselves, and got to work reading and prototyping, making himself the company’s resident GenAI expert.

In 2 months, Ryan and a couple of colleagues built the feature for a fraction of the cost to operate than the agency’s quote. His tech stack choice:

- **AWS Bedrock:** chosen for cost (vs hosting own models), security, and that the platform doesn’t use their input or output tokens for training
- **[Cohere Embed v3](https://cohere.com/blog/introducing-embed-v3)**: the model used to generate embeddings
- **PostgreSQL**: to store embeddings and do vector-based database queries, using AWS Aurora PostgreSQL
- **Java:** the backend code runs on this, deployed in AWS
- **React**: the frontend that fetches and displays the data, integrated into the existing web app

#### Get used to non-deterministic outputs

Ross McNairn is cofounder and CEO of the startup, Wordsmith, which several software engineers have joined. You need to rethink how to think about things, he says:

> “Working with AI requires a totally different way of approaching problems.
> 
> For new joiner engineers, there is a major readjustment in the first few weeks while they explore the codebase and participate in discussions. There are so many problems that can be eloquently sidestepped using AI. Understanding the suite of tools available takes some time.  
>   
> **Getting comfortable with evaluations and iterating on non-deterministic outputs is the biggest challenge most devs have.** A lot of solutions are more subjective: engineers need to *really* understand the domain in order to assess if output is high-quality. It takes time to ramp up to the point where you can confidently assess output quality.”

#### Switching to in-house can be easier, even for EMs

[Matt Morgis](https://www.linkedin.com/in/matthew-morgis-44015027/) was an engineering manager at Elsevier who decided to transition back to staff engineer, specifically to work on AI:

> “The move to go from manager to IC was deliberate: working with AI has rekindled my joy in coding.
> 
> For experienced engineers who know how to break problems down, AI tools are an incredible force multiplier. At the same time, when I was a manager, I saw AI coding tools handicap junior engineers’ development. The tools are powerful, but I think they’re best wielded by those who understand good software engineering principles.”

The transition was successful, and today Matt is a staff engineer focusing on GenAI at CVS Health.

### 3\. Tech stack

Here’s the tech stack which various companies used. *There’s no right or wrong tech stack – what follows is for context and inspiration, not a blueprint.*

#### Incident.io

The stack:

- **Postgres and [pgvector](https://github.com/pgvector/pgvector)** for storing embeddings and searching them
- **ChatGPT 4o** as the default model, and **Sonnet 3.7** for code analysis and technical tasks, as they find this Anthropic model performs better. Built in a way to easily switch between them as needed
- **Gemini**: some models used GCP’s Vertex offering, but less often than other models
- **GCP** using **Kubernetes**: the infrastructure layer
- **Go** on the backend, running as a monolith
- **React + Typescript** on the frontend, including for the dashboard of their own developers’ custom AI tools (covered below)

#### Sentry

**In-house LLM agent tooling**: the team evaluated and rejected using a tool like the [LangChain](https://en.wikipedia.org/wiki/LangChain) framework to integrate LLMs with other data sources and into workflows. It was a lot more work to build their own, but the upsides are that the architecture and code are more in-line with abstractions and design patterns in Sentry’s existing codebase.

The company used the following languages and frameworks to build this tooling:

- **Postgres** for database and vector store, **[pgvector](https://github.com/pgvector/pgvector)** for similarity search (for Approximate Nearest Neighbor – [ANN](https://www.cs.umd.edu/~mount/ANN/) – search)
- **Clickhouse** for online analytical processing (OLAP)
- **Sentry** for observability – *it would be odd to not use their own product for this*
- **Kubernetes** for orchestrating compute resources
- **Python and [PyTorch](https://pytorch.org/)** (machine learning library) for inference

#### Legal AI startup Wordsmith

The stack:

- **Pinecone** as their vector database
- **LangChain** as their framework to integrate LLMs into the stack. **[LangSmith](https://www.langchain.com/langsmith)** as their developer platform
- **[LlamaIndex](https://www.llamaindex.ai/)** as orchestration frameworks to integrate data with LLMs

Multi-cloud providers:

- **AWS** for running **Anthropic** models via Bedrock. *AWS offers generous credits for startups, which was a factor in the choice*
- **Azure** to access **OpenAI** services because it allows specifying regions to use, which is important when serving EU customers, for example. Using OpenAI’s services directly would *not* allow switching of regions.
- **GCP**: for **Gemini** and **Vertex** (Google’s search AI).

Azure and GCP each have business models for locking in customers; Microsoft is the only major cloud provider offering OpenAI models, and only GCP offers Gemini.

The company routes to different model by use case:

- **OpenAI**: for reasoning-heavy use cases, where the o1 and o3 models are very strong
- **Groq**: when performance is critical, or the goal is to augment UI. Wordsmith calls their API directly – as the performance of Groq is incredibly fast; a step-change in AI development, according to the WordSmith team. *Note: [Groq](https://groq.com/) is a standalone company and product, not to be confused with Grok, the AI assistant on social media site, X.*

#### AI coding assistant, Augment Code

The stack to build and run LLMs:

- **Google Cloud**: the cloud vendor of choice
- **A3 Mega 600GPU/75 node cluster:** used for LLM training and inference
- **NVIDIA:** the hardware choice for GPUs, and for software (CUDA)
- **Python** and **PyTorch**: the team wrote training and inference libraries making heavy use of PyTorch

#### RAG platform at scientific publisher Elsevier

The scientific publisher used this stack to build their in-house RAG platform:

- **AWS Bedrock** and **Azure OpenAI** for hosting and running LLMs
- **LangChain** for LLM integration
- **Snowflake** as their content data warehouse
- Embedding pipelines and vector database:
	- [Apache Airflow](https://airflow.apache.org/) for running embedding pipelines
	- [AWS Fargate for ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html) to run containers
	- [AWS OpenSearch](https://aws.amazon.com/opensearch-service/) as the vector search database
- **[FastAPI](https://fastapi.tiangolo.com/)** (a Python-based web framework to build HTTP APIs) for HTTP APIs

#### Chatbot for insurance company Simply Business

A pretty simple stack:

- **AWS Bedrock** to host the model, making use of [Knowledge Bases and Guardrails features](https://aws.amazon.com/blogs/machine-learning/introducing-guardrails-in-knowledge-bases-for-amazon-bedrock/)
- **Anthropic** Sonnet 3.5 model
- **Ruby on Rails** as the language and framework, running it on top of [AWS ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)

#### Summarization at HR tech DSI

As covered above, Ryan took the initiative at DSI by building a simpler solution than the one an AI vendor proposed. DSI ended up with:

- **AWS Bedrock** for running the models
- **PostgreSQL**: to store embeddings and do vector-based database queries. Using AWS Aurora PostgreSQL, and [Cohere Embed v3](https://cohere.com/blog/introducing-embed-v3) for generating embeddings

#### Tech stack trends across companies

The seven businesses in this article are all different, but there are some common trends:

- **AWS Bedrock:** the preferred way to host and run Anthropic models
- **Postgres with pgvector**: the database of choice to work with embeddings and vectors at most companies. The exception is Wordsmith, which uses vector database [Pinecone](https://www.pinecone.io/)
- **LangChain:** a few places use this as the framework to integrate LLMs into their stacks
- **The bigger the scale, the closer you get to the “metal:”** most startups are happy to use cloud providers to run LLMs. However, when starting to get into fine-tuning LLMs and heavy usage, it becomes time to rent larger resources and get close to the hardware. Augment Code using NVIDIA GPUs and CUDA software is an example.

### 4\. Engineering challenges

What unusual or new challenges does AI Engineering pose for more “traditional” software engineers? The most common ones mentioned:

#### Non-deterministic LLMs

Every engineer feels this top-ranked frustration sooner or later, as Lawrence Jones AI engineer at Incident.io describes:

> “You can build something that works well 5 times in a row, but fails terribly on the sixth run with the same inputs!
> 
> This is made harder by there being no objective method for using AI ‘correctly.’ All you can do is develop an intuition for the models based on understanding them technically and putting the hours into using them.
> 
> **Working on AI features has been an extremely frustrating experience for much of our team.** Counterintuitively, the people who find this most annoying are often the most experienced/productive engineers.”

Ross McNairn, cofounder at Wordsmith:

> “When you start to chain prompts together in workflows, variation compounds and things get even less predictable. There's even more variation when introducing agents.
> 
> Getting structured and formatted output from the AI where it will follow specific schemes, requires validators and “classical” software bulkheads to force the output to validate between steps.”

Ryan Cogswell, application architect at DSI:

> “We can do automated tests for the various pieces around the AI parts, but there isn't any way to guarantee *good* output from GenAI. All you can do is reduce the risk of getting *bad* output. Strategies I've used to mitigate quality and hallucination risks:
> 
> - **Validate** the output format. We do this on the fly (validating the JSON output) and also store the full input and output for all Bedrock GenAI calls, so we can recheck later, if needed.
> - **Repeat prompts during development.** When working on a prompt for a particular set of inputs, I execute the prompt 10-20 times with the same inputs to make sure that I get good results each time. When tweaking the prompt, I start over. It’s not pretty, but it works!
> - **Use single-purpose, narrow focus prompts.** Aim to have one prompt only deal with only one set of inputs.
> - **Avoid doing filtering or sorting via a prompt.** LLMs are not the best tool to do so: do filtering and sorting outside the prompt.”

#### Evals

“Evals” is short for “evaluations” and refers to testing AI models and applications to confirm they behave as expected, which can be done in three ways:

- **Manually**: this is surprisingly common — and necessary!
- **Automated**: the more scalable solution. Several companies have open sourced eval frameworks: the [OpenAI’s eval framework](https://github.com/openai/evals) is a better-known one.
- **LLM as judge**: an approach for an LLM to evaluate and score an outcome

You need to put in a lot of additional work to build useful evals, as Lawrence Jones from incident.io shares:

> “Evals frameworks don’t help with testing AI product features. They are generalised performance tests for models, often using other legacy models like [ROUGE](https://huggingface.co/spaces/evaluate-metric/rouge) to compare actual and expected outputs, which doesn’t help you check a feature for correctness.
> 
> Most eval frameworks work entirely at a *prompt level*: they take wholesale prompts with user data mixed into them. However, developers building AI features want to keep a set of *input data* and *expected output data,* and then run evals over those datasets while tweaking the structure of the prompt, not the input data itself.
> 
> This means you want the eval framework to be embedded in the code you use to generate your prompt. All eval frameworks I know are written in Python, while many of the AI applications use other languages (we use Go, for example).
> 
> You’re still on the hook for producing datasets for input and expected output, and a grading criteria. Nothing will solve this for you.”

How different teams build evals:

- Incident.io:
	- **Custom eval test suite**. This grades prompts in products. They run evals on them in CI and check for regressions on pull requests.
- Sentry:
	- **Hand-labeled, built with SMEs + LLM as a judge** for grading. There's always a "right" answer to the output from Autofix, but labeling it is very labor intensive. They chose a relatively small dataset (in the hundreds) of high quality labeled answers. They use the LLM as a judge to evaluate whether or not fixes match the correct solutions.
- Wordsmith:
	- **Evals sets built with SMEs.** The company builds curated, targeted sets of evals. They do this with subject-matter experts (SMEs), in this case, lawyers. The company learned that SMEs and devs need to work very tightly together, and that you cannot “throw stuff over the wall and sit back.”
- Elsevier:
	- **Manual with SMEs.** Manual evals done by SMEs (medical professionals) for major releases. This included evaluating the entire chat: from input query, through retrieved documents, to the final LLM response.
	- **LLM as a Judge**: used for smaller changes

Running evals on the CI can result in massive AI bills!Unlike “traditional” tests like unit tests that are practically free to run in terms of computing costs, running AI evals cost money. Here’s how incident.io avoids massive bills by caching and “stealing” evals from production:

- **Caching**: the incident.io team caches all eval results for a few days to avoid massive AI bills on each code push. They use cache keys that incorporate a checksum of the prompt + config + inputs. This means they do not re-run evals for a few days (say, 3 days) when the eval does not change in the code, as this would be burning money on AI evaluations.
- **“Stealing” evals from production:** they built an eval downloader tool which allows going quickly from a production LLM call into an eval that is anonymised in their codebase. Basically, they capture real-world usage while avoiding additional cost, as they do not have to re-run the eval. Some teams refer to this tactic as “stealing” an eval to production. This flow of getting evals from production to use for testing, can improve costly feedback loops and cut costs.

#### Latency

Lawrence Jones, AI Engineer at incident.io, explains the problem with latency and chaining:

> There is a disconnect between how quickly users want answers, and how long LLMs take to give them. Users usually expect an answer in under 3 seconds, and want to see *all* answers in 10 seconds.
> 
> Calling an LLM usually takes 1-3 seconds, but can be as long as 15 seconds. However, as you build more AI applications, you realize that you get more reliable AI experiences by *chaining* LLM responses, which means even more delay!
> 
> Here is how chaining LLMs works on most platforms:
> 
> - You write a prompt and say “you have access to these tools that you can optionally call to help you achieve your task”
> - When you execute the prompt and ask for the response – such as the message to respond to the user – you’ll either get:
> 	- A) The response, great, you can return it immediately
> 	- B) “Please call this tool for me with these parameters”
> 		- In this case: you need to create a new prompt to call the tool. The response from calling the tool could be:
> 			- C) The response, great, you can return it immediately
> 			- D) “Please call this tool for me with these parameters” using another tool….
> 				- Hopefully, after this second tool, the LLM will now terminate!
> 
> For an LLM response that invokes one tool, your latency will be:
> 
> - Cost of calling the original prompt (1-3 seconds)
> - Cost of calling the tool (potentially large: 5-15 seconds)
> - Cost of calling the original prompt again with tool results (1-3s)
> 
> In order to meet latency expectations, you end up doing some pretty crafty engineering!
> 
> Our prompt pipeline now looks more like a software CPU architecture.We do clever tricks like speculative execution to get answers faster:

![](https://substackcdn.com/image/fetch/$s_!z1J4!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F03c9cec3-f73c-465d-b02c-1cb92118e804_1600x968.png)

Experimenting with speculative answers, where the LLM goes ahead to execute a prompt that might be needed later

#### Debugging is tricky

Ross McNairn at Wordsmith:

> “Debugging was hard at the start. Langsmith was a great product for us, and we shared how we debug in a [case study with Langsmith](https://blog.langchain.dev/customers-wordsmith/). We had some early performance issues where we logged our output too much and it caused downstream issues. Once we got the balance right in logging enough to allow for auditing and debugging, but not too much to impact performance, these logs became an unbelievably powerful tool for us.
> 
> Putting logs to help debugging and auditing would be the first thing to lay down in a new project”.

#### Feedback on AI features

Is an AI feature working as expected? Ross advises to ask users and fix complaints they have. But first, you need to know about what it is:

> “Once a feature hits production, it's critical to have two features:
> 
> **1\. Users can iterate on it.** There should be ways to iterate on prompts to get better quality. Good products put eloquent recovery and iteration front-and-center.
> 
> **2\. One-click feedback to the dev team.** AI product engineering teams need to have the muscle to act on users’ feedback almost immediately.
> 
> **The moat in AI products is built on many tiny paper cuts.** Fix a thousand issues that slightly annoy people, and you will end up with a way of iterating on the various surfaces of the AI, and polishing the edges to get it working well.
> 
> Great products in this space are hammered into shape by months of iteration on the final 1% of quality around the edges”.

#### Privacy

If you decide to use the latest models that LLM vendors ship, it often means using APIs they provide, which raises the question of whether a vendor stores your prompts, and the answer to this *could* be “yes.”

OpenAI and Anthropic offer a 'zero-data retention' (ZDA) agreement, under which they hold onto minimal amounts of data sent to their servers. This “minimal data” is used for the sole purpose of preventing fraud and other abuse by tracking jailbreak attempts and other abuse vectors. The ZDA involves a customer trusting their provider to adhere to this ZDA.

**Self-hosting models** might be necessary for more sensitive use cases. Solutions like AWS Bedrock are also becoming popular by offering a tradeoff of easy setup and operation of a model, while not using inputs and outputs for training.

#### No fixed approach

Igor Ostrovsky, cofounder of Augment Code:

> “Because of the speed at which this space evolves, it’s important to be adaptable and develop best practices as you go.
> 
> There is no established way to do AI engineering.We find a lot of comfort in building our own tooling as needed, and building our own testing and evaluation benchmarks to suit our use case.”

### 5\. Novel tooling

Indcident.io have built a full stack of custom tooling. AI Engineer Lawrence Jones shares details about some of their interesting tools:

#### Custom tooling for debugging

‘The problem with debugging is that modern AI interactions are *many* LLM prompts chained together, not *one!* You only realize this once you work with LLMs, and using several LLM prompts is true of AI interactions of basic sophistication.

‘To make debugging easier, we append a small footer to each response for debugging purposes (hidden behind the three dots, below), which contains:

- **Trace**: links to a GCP trace of the interaction so you can see application code level details for debugging.
- **Evals**: this links into custom tooling designed around making this interaction debuggable, and plugging into our existing tooling.

![](https://substackcdn.com/image/fetch/$s_!DN_l!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fd563bdea-1909-4b1e-9b78-b84496a4684e_1408x860.png)

Adding custom debug tooling for each LLM-generated message / action

‘The *evals* link is the “magic sauce,” as it massively accelerates our team when building these features. Here’s what we show to devs who open the “evals” link:

![](https://substackcdn.com/image/fetch/$s_!n4Cp!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F527cf4e3-2e0f-42e6-8e92-ab7e2925103b_1600x756.png)

First part of the “evals” debugging function

‘We list measures that we grade bot interactions with, and these help us track bot performance, and to grade it on tone, efficiency, alignment, and also to calculate an overall score. We use this 'scorecard' UI for a variety of our AI systems.

‘All ratings are tracked, and are also part of monitoring and alerting, so our team gets alerted on regressions. We also trace how long a prompt takes to execute, which parts need to be executed, and how much it cost to run:

![](https://substackcdn.com/image/fetch/$s_!1MZu!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fda712325-98c6-4ec2-9d9d-639835a6daa9_1600x807.png)

Trace view of the prompt: 15 seconds to execute, with 5 sub-prompts, and cost $0.05 in total

#### No customer data for training models

*Gergely again.* Here’s an interesting challenge some vendors have: they *cannot* use customer data to train their models because customer data could contain private information, and also because customers pay to not train a vendor’s models with their usage. *Of course, there are vendors that [opt in customers to train their GenAI models](https://newsletter.pragmaticengineer.com/i/145833117/slack-and-adobe-make-t-and-cs-genai-compatible-after-outcry) by default, but they risk customer churn.*

**Vendors can improve their models by dogfooding.** When a vendor is a major user of its own product, the company can itself contribute to improving it. This is exactly what incident.io does by using their product to manage incidents on the platform. They also built additional tools to make it easy to tweak prompts; when they work better for incident.io, they likely work better for customers!

incident.io created tooling to make it easier to improve prompts while they dogfood the product. For any bot response, devs can inspect the eval, and get a copy-pasteable [YAML](https://en.wikipedia.org/wiki/YAML) snippet about the eval. If they want to tweak the code, they can copy this YAML, drop it into the code and re-deploy it:

![](https://substackcdn.com/image/fetch/$s_!5X1u!,w_424,c_limit,f_webp,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fe519f796-9767-46a5-883d-75513685943f_1600x990.png)

Internal tooling lets devs using the incident bot to easily improve prompts powering the bot

### 6\. Cost considerations

GenAI can quickly get expensive, but how important is this to the businesses in this article? There’s no one answer:

#### Low cost

Ashley Peacock at insurance tech company, Simply Business:

> We have started out small and are live with only a handful of trades because of the manual nature of the review, and we don't want to overwhelm reviewers. So, the cost is honestly pretty small right now, as it's just the AWS Knowledge Bases (backed by OpenSearch Serverless) and AWS Bedrock model invocations; Kafka is already widely used at the company. The actual cost of the model invocation is around $200/month right now.

We *could* reduce that cost by ~90%, but we're at the point where we want to scale it out as quickly as possible, and not spend time going overboard in optimizing cost.

#### Being slow controls costs

Ryan Cogswell at HR tech, DSI:

> “Today, “smarter” LLMs are much slower than less sophisticated ones. Users don’t usually tolerate overly long latency. But ‘smarter’ LLMs have innately slower response times, and this latency from the LLM itself helps keep costs kept at bay.
> 
> If LLM API calls became significantly faster while delivering the same or better quality, cost could become an issue.”

#### Costs keep dropping, so no problem

Tillman Elser at Sentry:

> “I have a simple philosophy on cost right now: we just don’t care very much. The cost landscape is changing dramatically: for example, OpenAI o1 went from ~$200p/m to free, basically overnight – likely thanks to DeepSeek releasing R1 for free.
> 
> **When you have sufficient funding, optimizing around costs is just not a good use of time or energy.** For now, I just follow the trendline until it stabilizes. This is also why I am not particularly interested in fine-tuning LLMs for our specific application or self-hosting/managing the infra. Both are fundamentally cost optimizations. I would rather pay a bit more for something that’s state of the art, than worry about this stuff right now.”

Ross McNairn of Wordsmith:

> “We operate under the standing assumption that costs will compact by an order of magnitude over the next 24 months. Optimization is a problem we leave to the foundation models and the infra layer. We focus on speed and quality of user experience and accept that today and tomorrow's margin profiles will be very different without any additional investment from our team.”

### 7\. Learnings from software engineers-turned-AI engineers

#### Lawrence Jones at incident.io

Lawrence has gone deep into AI engineering in the past 12 months, building custom tools, new architectures, and pushing the limits of the possible with products by using LLMs. He shares some practical learnings – dare I say, pragmatic – ones:

**‘Building a prototype is the easy part.** Getting a first version of a product that looks ‘credible’ is really, really easy. That’s because AI produces nice-looking content most of the time, and the hard part is getting it to produce valuable content. But people, and especially product engineers, are used to associating ‘nice’ with ‘good’.

‘It may take days to build a decent prototype of something that will take a year to get to market. Be prepared for that, both when building yourself, and especially when judging competitors which are upstart companies with compelling product screenshots that are essentially vapourware.

**‘Vibes-driven-development inevitably becomes just bad vibes;** you can make a decent start on building an LLM system by building an intuition for how to use models, just generally applying good engineering sense, and establishing a fast feedback loop for testing. This works, but only up until a point.

‘When you want to solve a more complex task, or demand consistency and reliability from a system, you can try proceeding with intuition-driven changes, but this will inevitably fail.

‘If you don’t have a way of measuring progress (graders, scorecards, backtesting, whatever) then your changes will undoubtedly impact the system negatively in unpredictable ways that you can’t catch. And if you’re changing it frequently, you won’t be able to track down the change that did it, as everything is too unpredictable to pinpoint.

‘This leads to really demoralising system failures (we called them ‘lobotomies’) where bad days amass and suddenly the system barely works, due to the combined effects of several small changes. Don’t do this.

**‘The LLM ecosystem is not built for product development.** As an engineer, you’re trained to believe that open-source tooling is a sensible place to look before trying to build anything yourself. That’s because conventional engineering has had decades to build tools that are really exceptional, and built by engineers for engineers.

‘The LLM ecosystem is large and active, but:

1. Tools are built by researchers, for researchers
2. They are almost always written in Python
3. and rarely address product engineering concerns

‘Asking your team to learn a complex new space (AI) with very little external guidance, while shipping a product, and doing it in a new language from the tools they’re used to, won’t work. It’s already enough to learn LLMs; don’t have your team give up their leverage too.

‘Equally, frameworks like LangChain appear to be great, but aren’t yet proven. Almost no one has proper agentic products out in the wild, yet these frameworks are meant to know how to work well with agentic products, and to have established best practices? Very unlikely.

‘If you can, the way to go is by using homegrown libraries in a language you’re already familiar with, that’s 100% compatible with your existing codebase.

**‘Smart teams are failing because they get overwhelmed.** Extremely smart teams with proven track records are failing at AI endeavours because they can’t get traction on their problems. This is due to a combination of:

- **Tooling**: they’re using new languages, new tools, new everything, and resetting their productivity back to beginner level.
- **Ambition:** LLMs have blown apart conceptions of what is possible, encouraging people to solve problems that are much more complex than before.
- **Noise:** the AI scene is moving so fast, every news cycle brings new ‘this makes everything else obsolete and you must adopt it!’ hype, which is hugely distracting.
- **LLMs:** people still have to learn how to use the models, and how they function technically.

‘How to avoid a spiral where all this leads to burnout and failed projects:

1. Breakdown larger problems into much smaller milestones
2. Learn how to measure success for milestones: how will you grade it, and know when it’s good?
3. Be extremely focused on only the next milestone
4. When necessary, build or invest in tools that help you achieve it
5. Only count a milestone as done when it’s being used at a non-trivial scale by customers, and hitting metrics for success.

‘If you can do this, you prevent engineers becoming overwhelmed by a problem and feeling like they aren’t making progress, or worse, that they are backsliding each day.’

#### Learnings from others

Tillman Elser at application monitoring platform, Sentry:

> **“It's okay to “overfit” to a relatively small set of high quality evals.** Trying to approach AI validation like a ML model, where you need tons of labeled examples, is often neither practical nor useful. I think that time is better spent on making a smaller set of very high quality evals and looking at specific examples, rather than trusting directional metrics
> 
> **Evaluate whether a simple retrieval strategy works better.** For Autofix, we found things like [BM25](https://en.wikipedia.org/wiki/Okapi_BM25) /search heuristics based on the abstract syntax tree ([AST](https://en.wikipedia.org/wiki/Abstract_syntax_tree)) work better than semantic retrieval via embeddings. Our use case might not be as generic for all LLM applications, though: the files and code referenced by the stack trace give us a great starting point.”

Ross Mcnairn at legal tech startup, Wordsmith:

> **“Design your AI product to cater for failure from the start.** Build in transparency and audit options that give people control makes them much more comfortable with it. We work with people not yet used to working with AI every day, like lawyers. Making them trust AI is part of our product succeeding.  
>   
> **Educate users on the most powerful use cases.** You need to “train” users for them to adapt a new way of working with AI, using your tool. There is an ambiguity to an empty text box that poses serious UX challenges for people using an AI product for the first time; investing a ton of time on that composer and the entry point has been absolutely massive for us.
> 
> **With AI, start simple and start broad.** There are hundreds of small, very simple applications that let you get familiar with the technology, which will be easy to get into production. Creating and adapting UIs is one of the many use cases you could start with. If you shoot for something more complex or multi-step, you’ll almost certainly be committing to months and months of interactions.”

Igor Ostrovsky at AI coding scaleup, Augment Code:

> **“Embed AI researchers in product engineering teams**. We don't separate research and engineering into different groups. We build for strong execution across product/UX, systems engineering, and AI research. Those three worlds need to align and coordinate well to build something great, and the feedback loop between the 3 groups is critical.
> 
> Don’t forget how fast this space is evolving; it feels much faster than with earlier technologies, and there’s extra uncertainty about models’ capabilities. LLM functionality can rapidly change in ways that make a feature irrelevant. You don't want to be a thin wrapper on existing models, due to the danger of commoditization.”

Ashley Peacock of insurance business, Simply Business:

> **“The AI is as good as the person prompting it**. If you can prompt it with a lot of detail, point it in the direction of certain files – effectively use your domain knowledge – and the AI will generally do a sound job.
> 
> **Use AI for the “boring stuff”, but drive the thoughtful parts.** When using tab completions in the code, use it for the boring, repetitive stuff. It’s good at this.
> 
> However, do not let it take the lead on more thoughtful, “harder” stuff. You should be the one making architectural decisions and deciding on the big picture, not the other way around. Don’t let the tail wag the dog.”

Ryan Cogswell at HR tech, DSI:

> **“Prompt engineering is no big deal.** Just give data in the prompt and tell it in plain English what you want, that’s all there is to it.”

*It’s hard to believe there was a time when there was [speculation](https://www.reddit.com/r/PromptEngineering/comments/1auwxpz/so_was_prompt_engineering_jobs_just_a_hype/) that prompt engineering might become its own fulltime job!*

### Takeaways

Thanks again to [Lawrence Jones](https://blog.lawrencejones.dev/), [Tillman Elser](https://www.linkedin.com/in/tillman-elser/), [Ross McNairn](https://www.linkedin.com/in/rossmcnairn/), [Igor Ostrovsky](https://www.linkedin.com/in/igoro/), [Matt Morgis](https://www.linkedin.com/in/matthew-morgis-44015027/), [Ashley Peacock](https://www.linkedin.com/in/ashley-peacock-133749120/) and [Ryan Cogswell](https://x.com/ryanecogswell) for sharing what they’ve learned, first-hand, about AI engineering.

Here is what I collected after talking with all of them.

**AI engineering is easy enough for software engineers to pick up – and you should.** I find Ryan’s story inspiring and relatable: at first, everyone was hesitant to get involved building applications on top of LLMs. They knew they did not have the skills, and this new area was not their expertise.

But it turns out that “experts” like AI agencies might know about more tools, but they don’t know more about software engineering than experienced engineers do! The AI agency came up with a horribly overcomplicated architecture, possibly just to use as many cool technologies as they could find.

AI engineering is “just” working with LLMs, and using software engineering concepts. When getting started, LLMs are often behind APIs, and any software engineer can invoke APIs and integrate them into their application. If this API uses LLMs behind the scenes, congratulations, you’re doing “AI engineering.”

**Working with LLMs is non-deterministic and this trips people up.** The single biggest learning echoed by all engineers is that you need to expect non-deterministic output from LLMs. This is very different to what we’re used to with software engineering: where programming is deterministic.

Sure, there are edge cases with race conditions and parallel computing where we can see non-determinism: but until now, this was the exception, not the norm. But with LLMs, non-deterministic behavior is the norm.

**It can make a lot of sense to build your own tools – at least for now.** The concept of “AI engineering” is barely two years old, and this emergent field is in flux. Lawrence Jones and incident.io are good examples of how it can pay off to build custom tools to iterate faster with LLMs. And building tools to make it easier to debug evals, tweak prompts, etc, isn’t even that big of a deal!

Given how new AI tooling is, there’s a fair chance that the existing tooling might not fit your needs. It could be faster to build it yourself, and decide what to do with more mature solutions later.

Taking on tech debt can speed up iteration speed, and for fast-moving startups, this could be the practical approach with AI engineering and tools. For more tips on how to think about tech debt, see the deepdive [Paying down tech debt](https://newsletter.pragmaticengineer.com/p/paying-down-tech-debt).

**AI engineering is an exciting, rapidly evolving field.** My sense is that working with LLMs will become a baseline expectation for most software engineers at startups and scaleups, similar to how being on the oncall rotation is a given for engineers at many companies.

I hope you’ve found these stories about how software engineers added AI engineering to their toolbelt, motivational and useful. Why not try out the ideas that interest or inspire you: the best way to get better at AI Engineering is to do it!