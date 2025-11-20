---
title: "LLM from scratch :: Giles' blog"
source: "https://www.gilesthomas.com/llm-from-scratch"
author:
published:
created: 2025-11-19
description: "("
tags:
  - "clippings"
---
[About](https://www.gilesthomas.com/about)

[Contact](https://www.gilesthomas.com/contact)

## LLM from scratch

I'm working through [Sebastian Raschka](https://sebastianraschka.com/) 's book " [Build a Large Language Model (from Scratch)](https://www.manning.com/books/build-a-large-language-model-from-scratch) ", writing up the things I find interesting and/or surprising, and filling in some of the gaps. The book is a brilliant explanation of *how* to build an LLM, but sometimes glosses over *why* we do particular things -- for example, why certain sequences of matrix multiplications result in a working, trainable attention mechanism.

I've finished the main body of the book, but the series is ongoing -- there are a few things I want to do before I can finally draw a line under this epic:-)

Here are the posts in this series:

- [Writing an LLM from scratch, part 1](https://www.gilesthomas.com/2024/12/llm-from-scratch-1) (22 December 2024). Kicking off -- covering the introductory first chapter in the book. Adorably, I thought I might be able to finish the book over my Christmas break:-)
- [Writing an LLM from scratch, part 2](https://www.gilesthomas.com/2024/12/llm-from-scratch-2) (23 December 2024). The basics of embeddings and tokenisation.
- [Writing an LLM from scratch, part 3](https://www.gilesthomas.com/2024/12/llm-from-scratch-3) (26 December 2024). Wrangling data so that it can be handled by an LLM, plus token and position embeddings.
- [Writing an LLM from scratch, part 4](https://www.gilesthomas.com/2024/12/llm-from-scratch-4) (28 December 2024). Starting to try to understand attention by looking at the history.
- [Writing an LLM from scratch, part 5 -- more on self-attention](https://www.gilesthomas.com/2025/01/llm-from-scratch-5-self-attention) (11 January 2025). More on attention -- the history, and a little more detail on what it actually is.
- [Writing an LLM from scratch, part 6 -- starting to code self-attention](https://www.gilesthomas.com/2025/01/llm-from-scratch-6-coding-self-attention-part-1) (21 January 2025). Our first cut at an attention mechanism -- a non-trainable one.
- [Writing an LLM from scratch, part 6b -- a correction](https://www.gilesthomas.com/2025/01/llm-from-scratch-6b-correction) (28 January 2025). You can skip this one, it was a post to alert people who were reading along that the previous one had a (since-corrected) error.
- [Writing an LLM from scratch, part 7 -- wrapping up non-trainable self-attention](https://www.gilesthomas.com/2025/02/llm-from-scratch-7-coding-self-attention-part-2) (7 February 2025). Still digging into the example of non-trainable attention.
- [Writing an LLM from scratch, part 8 -- trainable self-attention](https://www.gilesthomas.com/2025/03/llm-from-scratch-8-trainable-self-attention) (4 March 2025). Finally, an explanation of self-attention that makes sense! (At least to me...)
- [Writing an LLM from scratch, part 9 -- causal attention](https://www.gilesthomas.com/2025/03/llm-from-scratch-9-causal-attention) (9 March 2025). Causal, or masked self-attention: when we're considering a token, we don't pay attention to later ones.
- [Writing an LLM from scratch, part 10 -- dropout](https://www.gilesthomas.com/2025/03/llm-from-scratch-10-dropout) (19 March 2025). Adding dropout to the LLM's training is pretty simple, though it does raise one interesting question...
- [Writing an LLM from scratch, part 11 -- batches](https://www.gilesthomas.com/2025/04/llm-from-scratch-11-batches) (19 April 2025). Batching speeds up training and inference, but for LLMs we can't just use matrices for it -- we need higher-order tensors.
- [Writing an LLM from scratch, part 12 -- multi-head attention](https://www.gilesthomas.com/2025/04/llm-from-scratch-12-multi-head-attention) (21 April 2025). Finally getting to the end of chapter 3! This time it’s multi-head attention: what it is, how it works, and why the code does what it does.
- [Writing an LLM from scratch, part 13 -- the 'why' of attention, or: attention heads are dumb](https://www.gilesthomas.com/2025/05/llm-from-scratch-13-taking-stock-part-1-attention-heads-are-dumb) (8 May 2025). Realising that attention heads are simpler than I thought explained why we do the calculations we do.
- [Writing an LLM from scratch, part 14 -- the complexity of self-attention at scale](https://www.gilesthomas.com/2025/05/llm-from-scratch-14-taking-stock-part-2-the-complexity-of-self-attention-at-scale) (14 May 2025). Starting to build intuition on how self-attention scales (and why the simple version doesn't).
- [Writing an LLM from scratch, part 15 -- from context vectors to logits; or, can it really be that simple?!](https://www.gilesthomas.com/2025/05/llm-from-scratch-15-from-context-vectors-to-logits) (31 May 2025). The way we get from context vectors to next-word prediction turns out to be simpler than I imagined -- but understanding why it works took a bit of thought.
- [Writing an LLM from scratch, part 16 -- layer normalisation](https://www.gilesthomas.com/2025/07/llm-from-scratch-16-layer-normalisation) (8 July 2025). Working through layer normalisation -- why do we do it, how does it work, and why doesn't it break everything?
- [Writing an LLM from scratch, part 17 -- the feed-forward network](https://www.gilesthomas.com/2025/08/llm-from-scratch-17-the-feed-forward-network) (12 August 2025). The feed-forward network is one of the easiest parts of an LLM in terms of implementation -- but when I thought about it I realised it was one of the most important.
- [Writing an LLM from scratch, part 18 -- residuals, shortcut connections, and the Talmud](https://www.gilesthomas.com/2025/08/llm-from-scratch-18-residuals-shortcut-connections-and-the-talmud) (18 August 2025). The book's description of shortcut connections is overly-simplified, I think -- residuals are more than just shortcuts to help with gradients.
- [Writing an LLM from scratch, part 19 -- wrapping up Chapter 4](https://www.gilesthomas.com/2025/08/llm-from-scratch-19-wrapping-up-chapter-4) (29 August 2025). A state-of-play update after finishing Chapter 4, with a roadmap of what’s coming next.
- [Writing an LLM from scratch, part 20 -- starting training, and cross entropy loss](https://www.gilesthomas.com/2025/10/llm-from-scratch-20-starting-training-cross-entropy-loss) (2 October 2025). Starting training our LLM requires a loss function, which is called cross entropy loss. What is this and why does it work?
- [Writing an LLM from scratch, part 21 -- perplexed by perplexity](https://www.gilesthomas.com/2025/10/llm-from-scratch-21-perplexed-by-perplexity) (7 October 2025). Raschka calls out perplexity in a sidebar, but I wanted to understand it in a little more depth.
- [Writing an LLM from scratch, part 22 -- finally training our LLM!](https://www.gilesthomas.com/2025/10/llm-from-scratch-22-finally-training-our-llm) (15 October 2025). Finally, we train an LLM! The final part of Chapter 5 runs the model on real text, then loads OpenAI’s GPT-2 weights for comparison.
- [Writing an LLM from scratch, part 23 -- fine-tuning for classification](https://www.gilesthomas.com/2025/10/llm-from-scratch-23-fine-tuning-classification) (22 October 2025). After all the hard work, chapter 6 is a nice easy one -- how do we take a next-token predictor and turn it into a classifier?
- [Writing an LLM from scratch, part 24 -- the transcript hack](https://www.gilesthomas.com/2025/10/llm-from-scratch-24-the-transcript-hack) (28 October 2025). Back when I started playing with LLMs, I found that you could build a (very basic) chatbot with a base model -- no instruction fine-tuning at all! Does that work with GPT-2?
- [Writing an LLM from scratch, part 25 -- instruction fine-tuning](https://www.gilesthomas.com/2025/10/llm-from-scratch-25-instruction-fine-tuning) (29 October 2025). Some notes on the first part of chapter 7: instruction fine-tuning.
- [Writing an LLM from scratch, part 26 -- evaluating the fine-tuned model](https://www.gilesthomas.com/2025/11/llm-from-scratch-26-evaluating-the-fine-tuned-model) (3 November 2025). Coming to the end of the book! We evaluate the quality of the responses our model produces, manually and automatically.
- [Writing an LLM from scratch, part 27 -- what's left, and what's next?](https://www.gilesthomas.com/2025/11/llm-from-scratch-27-whats-left-and-whats-next) (4 November 2025). Having finished the main body of the book, it's time to think about what I need to do to treat this project as fully done.