---
title: "ART·E: How We Built an Email Research Agent That Beats o3 | OpenPipe"
source: https://openpipe.ai/blog/art-e-mail-agent
author:
published:
created: 2025-09-30
description:
tags:
  - clippings
  - agent
---
[Launch App](https://app.openpipe.ai/)

[Back to all articles](https://openpipe.ai/blog)

Technical

## ART·E: How We Built an Email Research Agent That Beats o3

Kyle Corbitt

Apr 29, 2025

12 min read

OpenAI's version of [Deep Research](https://openai.com/index/introducing-deep-research/) showed how effective reinforcement learning (RL) can be for teaching an agent a specific task. Compared to previous research agents, it was a major step forward in effectiveness. With our new project, "ART·E", we've applied this training recipe to a new, realistic task: **answering natural-language questions by searching an email inbox**. We've produced a model that is *faster*, *cheaper*, and *more accurate* than o3 on this task.

![Accuracy comparison](https://openpipe.ai/blog-images/art-e/art-e-accuracy-comparison.svg)

ART·E outperforms o3 on a realistic agentic research task, answering 60% of the questions that o3 missed.

![Cost and latency comparison](https://openpipe.ai/blog-images/art-e/art-e-cost-latency-comparison.svg)

ART·E is 5x faster and 64x cheaper to run than o3.

We've open-sourced both the [final model](https://huggingface.co/OpenPipe/art-e-008) and [all training code](https://github.com/OpenPipe/ART/tree/main/examples/art-e). In this post we'll cover the details of how we built it, and lessons learned you can apply to build your own!

## Let's Define Our Task

For this project we wanted a task that was realistic and useful, while still being narrow enough to see quick improvement through RL.

Searching my email inbox felt like the perfect match. I've wanted an agent that can do this for me forever. Today, when I have a question like "how do I RSVP for my daughter's classroom party" or "what time is my brother's flight on Friday" I have to open my inbox, think up keywords, and read through search results. *So* 2022. Why isn't AI doing this for me? ART·E is designed to do exactly this, with style!

## "Synthetic" Data

To train a model and evaluate its performance, we needed a realistic dataset of answerable email queries. Luckily for us, when notorious energy trader [Enron](https://en.wikipedia.org/wiki/Enron) was sued for [massive accounting fraud](https://en.wikipedia.org/wiki/Enron_scandal) in 2001, 500K of their emails were made public in the litigation (**pro tip:** if you're engaging in massive accounting fraud, maybe don't save all your emails).

We [randomly selected](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/data/test_and_train_inboxes.py) 8 employee inboxes as a "test set" and an additional 20 as a "train set". Each selected inbox had at least 5K emails, and many had 10K+.

Of course, having a realistic email inbox isn't enough—we also need realistic questions a user might ask that can be answered by searching the inbox! Since a good dataset of that shape doesn't exist, we had to generate one **synthetically**. This is a fancy way of saying "make it up".

![I made it up](https://openpipe.ai/blog-images/art-e/i-made-it-up.webp)

For each inbox, we iterated through 1000 emails in batches of 20. For each batch, we prompted gpt-4.1 <sup><a href="https://openpipe.ai/blog/#user-content-fn-1">1</a></sup> to generate several **synthetic question-answer pairs** for each email ([full prompt](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/data/generate_synthetic_question_data.py#L119)). The model output a list of questions along with the correct answer and source message ID. We also asked the model to generate a `how_realistic` score between 0 and 1, which was actually pretty effective at filtering out questions that no person would actually ask.

We've included some of the generated questions below, and you can find the whole dataset of ~4k questions [here](https://huggingface.co/datasets/corbt/enron_emails_sample_questions).

| Question | Answer | Source |
| --- | --- | --- |
| What issues will be discussed at the Tuesday afternoon meeting with EES? | What to do about forcing the utilities to pay delinquent PX credits, whether the new 1 cent surcharge should be passed on to our customers, and whether to try to return our customers to utility bundled service. | Thanks, Harry. I want to re-enforce the switching issue, since EES is likely to be very focused on moving customers back to the utility on Tuesday. Switching would certainly reduce EES' going-forward exposure to 1) growing |
| When is the Astros group game against the Cubs? | Thursday, April 27, at 3:05 PM. | You have a ticket - we will see you there, with you pager on! Patti will get your ticket to you before Thursday. |
| What countries are on the boycott list for e-commerce trading? | Bahrain, Iraq, Kuwait, Lebanon, Libya, Oman, Qatar, Saudi Arabia, Syria, United Arab Emirates, Republic of Yemen. | Louise and Mark, As we discussed in our meeting last Thursday, set forth below is the most |
| What is my confirmation number for my Continental Airlines flight to Colorado Springs? | N1BTZH | Thank you for making your OnePass travel arrangements with Continental Airlines. Your flight information is listed below. Replies to this e-mail will not be returned. For changes or questions about your E-Ticket |
| Where can I find the revised anexb.doc form? | It is located in atty.fms/swaps/current forms/anexb.doc. | We have completed the revisions to anexb.doc (the document used to prepare credit for omnibus confirmations). It has been moved into the attorney forms bank and is located in atty.fms/swaps/current forms/anexb.doc. The prior |

## Define the Environment

An agent always operates in an **environment**, which just means "the tools you give it and the information it has access to". In our case, we have relatively simple environment. The agent is given an initial prompt defining the task, which is to answer the user's question based on the contents of their inbox. It is also given 3 tools:

1. `search_emails(keywords, sent_after, sent_before)`: finds up to 10 emails matching the given keywords with date filters applied, and returns the message IDs as well as matching snippets ([implementation](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/email_search_tools.py#L32))
2. `read_email(message_id)`: returns the full email body for the given message ID ([implementation](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/email_search_tools.py#L155))
3. `return_final_answer(answer: str, sources: list[str])`: returns the final answer to the user's question, and the list of message IDs that supported the answer ([implementation](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/rollout.py#L116))

To facilitate tools (1) and (2), we pre-process the dataset into a local sqlite database which allows for efficient querying. `search_emails` is implemented using sqlite's [FTS5](https://sqlite.org/fts5.html) full-text search engine.

With these tools available, we simply implement the world's simplest agentic loop:

1. Call the LLM with the initial prompt ([source](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/rollout.py#L245))
2. Parse the tool call it made ([source](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/rollout.py#L273))
3. Call the appropriate tool with the given arguments ([source](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/rollout.py#L315))
4. Append the LLM's response and the tool call's output to the conversation history ([source](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/rollout.py#L268))
5. Goto 1 until the model returns a final answer or we exceed 10 steps ([source](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/rollout.py#L351))

This is extremely simple—no recursive calls, backtracking, etc. But we've found in practice this works more often than not.

## Benchmarking the Competition

Before actually training a model with RL (we're getting there, I promise!) we always recommend benchmarking off-the-shelf prompted models, and trying *really hard* to get them to perform well. There are multiple reasons to do this:

1. You may find that an existing model is already great at your task, and you don't need to train with RL after all!
2. Oftentimes, the reason a model *doesn't* do well on your task is because you're withholding critical context, the tools you're giving it don't actually work, or the goal is too vague. These aren't problems that RL can solve for you, so it's important to identify and fix them before training.
3. If you know your prompted baselines, you are permitted to loudly whoop around the office and share victory memes on X when your RL model eventually surpasses them during training. This is the most important reason.

We ended up benchmarking a bunch of different models and fixing numerous issues with our agentic loop before even starting RL training.

One thing we'll cover in a moment is **how to measure performance**. For now, we can stick with a simple evaluation: if the model returned a final answer, use an LLM to check if it matches the golden one, and count the number of correct answers across our test set.

![Accuracy comparison](https://openpipe.ai/blog-images/art-e/art-e-accuracy-comparison-prompted-models.svg)

Accuracy comparison

## Defining the Reward Function

> Show me the incentive and I'll show you the outcome. — Charlie Munger

(Charlie would have made a great RL researcher!)

The next step is to define our **reward function**. This is how you tell the model what it "should" do. **Reward function design is critical to RL success**, and can be a surprisingly tricky to get right.

"But wait," you say, "don't we already have a reward function? We already defined an LLM-as-judge to evaluate our prompted models!"

Great point! Our judge prompt is a great starting point for our reward function, and covers answer correctness, which is what we care about most. But one of the very cool things about RL is that you can get the model to optimize for multiple objectives at once. You can even tell it which are most important by setting their relative weights in the final reward!

Here are some of the additional objectives we added:

### Minimize Turns

![](https://openpipe.ai/blog-images/art-e/art-e-num-turns-training-progress.svg)

OpenAI's version of Deep Research showed how effective reinforcement learning (RL) can be for teaching an agent a specific task. Compared to previous research agents, it was a major step forward in effectiveness. With our new project, "ART·E", we've applied this training recipe to a new, realistic task: answering natural-language questions by searching an email inbox. We've produced a model that is faster, cheaper, and more accurate than o3 on this task.

We gave a very small "extra credit" reward to the model for taking fewer turns to answer the question correctly. This is a proxy for **latency** —fewer round trips to the email inbox means faster answers for the user. By the end of training, the model was taking almost a full turn less than o3, while still getting higher accuracy!

### Penalize Hallucinations

![](https://openpipe.ai/blog-images/art-e/art-e-wrong-answer-training-progress.svg)

OpenAI's version of Deep Research showed how effective reinforcement learning (RL) can be for teaching an agent a specific task. Compared to previous research agents, it was a major step forward in effectiveness. With our new project, "ART·E", we've applied this training recipe to a new, realistic task: answering natural-language questions by searching an email inbox. We've produced a model that is faster, cheaper, and more accurate than o3 on this task.

Getting the answer right is ideal, but if it can't find the right answer, it is *much better* for the model to say "I don't know" than to hallucinate a wrong one. We added a significant penalty to incorrect answers to discourage hallucination. This worked great; as you can see in the plot above, by the time our model finished training, it not only got the right answer more often than o3, it also hallucinated fewer wrong ones!

### (Unsuccessful) Partial Credit

We also attempted to give the model small amounts of "partial credit" for each of the following:

- Ever finding the right email in search results
- Ever reading the right email using `read_email`
- Getting the source email right, even if the answer was wrong

The theory here is that these partial credits would make our reward function more **dense** —that is, give the model a cleaner gradient to follow between "totally wrong" and "totally right". This kind of intermediate reward is super common in RL, especially for difficult, long-horizon tasks that the model realistically can't solve when training begins.

In this case, these partial credits basically didn't speed up training at all, probably because the model was already able to find the right answer often enough to learn from that signal directly.

**Be careful with these instrumental goals.** The model will take them very literally! In an early run we gave partial credit for taking more turns. The model actually learned to just start repeating its last tool call over and over again until it ran out of turns! Sometimes it's best to skip intermediate rewards and let the model optimize for the final objective directly. This is a reflection of [the bitter lesson](http://www.incompleteideas.net/IncIdeas/BitterLesson.html).

## Let's Train!

![Blog image](https://openpipe.ai/blog-images/art-e/lets-train.webp)

Ok, now that we have our dataset, environment and reward function, we can train our model!

We used our open source [ART library](https://github.com/OpenPipe/ART) for all the training and evaluations. ART (Agent Reinforcement Trainer) is purpose-built to make it easy to train real-world multi-turn agents using [Group Relative Policy Optimization](https://rlhfbook.com/c/11-policy-gradients.html#group-relative-policy-optimization) (GRPO).

The GRPO training loop is quite simple. For this task, we just do the following:

1. Load a batch of 12 questions (and their correct answers) from our dataset.
2. For each question, run the agent 4 times using our [rollout](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/rollout.py) function. We refer to the final list of messages produced by each run through our rollout function as a **trajectory**.
3. Score all 4 trajectories with our reward function.
4. Use all 12 groups of 4 trajectories (so 48 trajectories total) along with their rewards to calculate the loss using the GRPO formula and update the model.
5. (Every 30 steps) Run 100 validation questions and calculate the accuracy of the model on our metrics.
6. Goto 1 until the model stops improving on our validation set.

You can see our full training script [here](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/art_e/train.py#L122-L151), which is just a few lines of code!

## Monitoring Training

The GRPO training loop is simple to understand, but that doesn't mean getting good results is automatic! We ended up running 15 training jobs (most for only a few hours) while tweaking hyperparameters. **Good observability** is key to understanding what's happening and making changes if necessary.

![Training curve](https://openpipe.ai/blog-images/art-e/art-e-accuracy-training-progress.svg)

Our final run has a pretty good-looking training curve, but the first run we tried didn't look this way!

Here are some tips to monitoring your training:

1. **Watch your reward standard deviation.** GRPO works by running the same input N times, scoring all of them, and then training the model to behave more like the best-performing ones. But if the model gets stuck in a local optimum, all the trajectories will have a similar score and there will be nothing to train on. If this happens, you can try increasing trajectories per rollout, making your reward function more dense, decreasing the learning rate, or training your model in more diverse scenarios.
2. **Track lots of metrics.** For this task we tracked 15 different metrics, including answer accuracy, number of turns, and number of hallucinations. This is easy to do with ART, which lets you associate metrics with each trajectory. that are reported in aggregate to Weights & Biases as well as saved in your run logs.See the full list of metrics we tracked.
	```python
	class FinalRubric:
	    answer_correct: bool = False
	    sources_correct: bool = False
	    num_turns: int = 0
	    attempted_answer: bool = False
	    ever_found_right_email: bool = False
	    ever_read_right_email: bool = False
	    cant_parse_tool_call: bool = False
	    bad_tool_call_name: bool = False
	    bad_tool_call_args: bool = False
	    ran_out_of_turns: bool = False
	    returned_i_dont_know: bool = False
	    num_sources: int = 0
	    ever_tried_to_read_invalid_email: bool = False
	    prompt_tokens: int = 0
	    completion_tokens: int = 0
	```
3. **Look at actual model outputs**. Your RL model is [sneaky and always trying to reward hack](https://twitter.com/corbtt/status/1913283594191245652?ref_src=twsrc%5Etfw). Even if your reward is increasing, you need to look at actual outputs regularly to make sure it's really doing what you want.<sup><a href="https://openpipe.ai/blog/#user-content-fn-2">2</a></sup> On one early run, we decided to give a small "partial credit" bonus for taking more turns to encourage exploration. The model learned to just repeat the last tool call over and over until it hit the maximum number of turns!

![Model repeating tool calls](https://openpipe.ai/blog-images/art-e/run-002-many-turns.webp)

For one early run, the model settled on 'padding-out' every trajectory to the max number of turns (10) by repeating the last tool call

![Model repeating same message](https://openpipe.ai/blog-images/art-e/art-e-model-repeats-6-times.webp)

Repeating the same message over and over

## Costs

For the final training run we used a learning rate of 1.2e-5 and 2 epochs. We ran the training job using [Skypilot](https://docs.skypilot.co/en/latest/) ([code](https://github.com/OpenPipe/ART/blob/art-e/examples/art-e/run_training_job.py)) on a [Runpod](https://www.runpod.io/) GPU.

ART uses lots of tricks to speed up training, like running rollouts with [vLLM](https://docs.vllm.ai/en/latest/), using aggressive sample packing at training time, and building on [Unsloth](https://github.com/unslothai/unsloth) 's training optimizations. This leads to faster feedback cycles and cheaper training. With these optimizations, the job took just under a day to run and fit on a single H100 GPU. This meant the total training cost was about **$80**.

You can see representative trajectories comparing o3, o4-mini, and the base Qwen-14B model in the results section below.

## Example Trajectories

system

You are an email search agent. You are given a user query and a list of tools you can use to search the user's email. Use the tools to search the user's emails and find the answer to the user's query. You may take up to 10 turns to find the answer, so if your first seach doesn't find the answer, you can try with different keywords. User's email address is tim.belden@enron.com Today's date is 2000-12-30

user

When is Shari's move to Portland targeted for?

assistant

search\_emails({"keywords": \["Shari", "Portland"\], "sent\_before": "2000-12-30", "max\_results": 10})

tool

\[{"message\_id": "<18249430.1075853404722.JavaMail.evans@thyme>", "snippet": "... are working on \\nfinalizing <b>Shari</b>'s move to <b>Portland</b>. <b>Shari</b> is looking for a \\"relocation... "}, {"message\_id": "<28511885.1075859526780.JavaMail.evans@thyme>", "snippet": "I have discussed relocating <b>Shari</b> to <b>Portland</b> with both of you. Elizabeth \\nwanted to make... "}\]

assistant

read\_email({"message\_id": "<18249430.1075853404722.JavaMail.evans@thyme>"})

tool

{"message\_id": "<18249430.1075853404722.JavaMail.evans@thyme>", "date": "2000-12-14 13:45:00", "subject": "Shari's relocation", "from\_address": "elizabeth.sager@enron.com", "to\_addresses": \[\], "cc\_addresses": \[\], "bcc\_addresses": \[\], "body": "FYI - I wanted you to know that, despite all appearances, we are working on \\nfinalizing Shari's move to Portland. Shari is looking for a \\"relocation\\" \\npackage. HR has been tied up in PRC and is now searching for a package that \\nworks. HR has promised me a response today and then I can discuss w Mark H \\nand then present to Shari. End of Feb is still the target date. \\n\\nHope all well (despite the press).\\n\\nElizabeth\\n713 853 6349", "file\_name": "sager-e/all\_documents/286."}

assistant

return\_final\_answer({"answer": "Shari's move to Portland is targeted for the end of February.", "sources": \["<18249430.1075853404722.JavaMail.evans@thyme>", "<28511885.1075859526780.JavaMail.evans@thyme>"\]})

## Learn more

Everything we did is open source, and we'd love to see others build on top of our work! The [ART library](https://github.com/OpenPipe/ART) is a great place to start, and you can find all the code for this specific project [here](https://github.com/OpenPipe/ART/tree/art-e/examples/art-e).

If you'd like to build your own project using ART, join us on [Discord](https://discord.gg/zbBHRUpwf4). And if you're an enterprise interested in working with our team to train your own proprietary agents, [let's chat](https://openpipe.ai/blog/) and see how we can help!

**UPDATE:** Due to popular demand, we're going to host a community "lunch & learn" webinar to discuss the project and answer questions on Tuesday, May 6. You can [sign up here](https://lu.ma/mj027vka). Hope to see you there!

---

[^1]: I also tried Gemini 2.5 Pro, but found that GPT-4.1 did a better job here.

[^2]: We've been using OpenPipe's [request logs](https://docs.openpipe.ai/features/request-logs/logging-requests) to monitor trajectories, although admittedly we didn't really design it for this purpose. We'll have something better built into the ART library soon!