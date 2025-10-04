---
title: "You Could’ve Invented Transformers"
source: "https://gwern.net/blog/2025/you-could-have-invented-transformers"
author:
  - "[[Gwern]]"
published:
created: 2025-10-01
description: "Proposal for a ‘You Could Have Invented Transformers’ tutorial; someone should write a series showing a logical recreation of Transformers from primitive <em>n</em>-gram language models to full-strength Transformers."
tags:
  - "clippings"
---
([Transformer](https://gwern.net/doc/ai/nn/transformer/index), [tutorial](https://gwern.net/doc/tutorial/index); [⁠similar ⁠](https://gwern.net/metadata/annotation/similar/%252Fblog%252F2025%252Fyou-could-have-invented-transformers.html))

There are many [Transformer ⁠](https://arxiv.org/abs/1706.03762#google) tutorials ([⁠eg ⁠](https://gwern.net/gpt-2#transformer-tutorial)), but they generally focus on presenting a relatively contemporary implementation. This leaves the reader a bit mystified: this complex assemblage of MLPs and self-attention layers and normalization appears to have ‘dropped out of the sky’. How could Noam Shazeer and the other authors have invented the Transformer—divine benevolence (as all else)?

*Why* does this complicated Transformer head block work so well for sequence prediction? Which parts are required, and which are there for optimization purposes? The Transformer was discovered by [a huge amount of trial-and-error ⁠](https://www.wired.com/story/eight-google-employees-invented-modern-ai-transformers-paper/) ([much like resnets ⁠](https://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/)), so following the historical sequence is neither possible nor enlightening.

---

However, at this point, I believe we now understand Transformers & variations well enough that we can invent an imaginary history of Transformers for pedagogical purposes, in the vein of the “You Could Have Invented *X* ” [snowclone ⁠](https://en.wikipedia.org/wiki/Snowclone) (eg. [⁠monads ⁠](http://blog.sigfpe.com/2006/08/you-could-have-invented-monads-and.html "‘You Could Have Invented Monads! (And Maybe You Already Have.)’, sigfpe 2006"), [⁠parser combinators](https://theorangeduck.com/page/you-could-have-invented-parser-combinators "You could have invented Parser Combinators"), [⁠zippers](https://blog.ezyang.com/2010/04/you-could-have-invented-zippers/ "‘You could have invented zippers’, ezyang 2010"), [⁠Fenwick trees ⁠](https://www.cambridge.org/core/journals/journal-of-functional-programming/article/you-could-have-invented-fenwick-trees/B4628279D4E54229CED97249E96F721D "You could have invented Fenwick trees"), [⁠fractional cascading](https://blog.ezyang.com/2012/03/you-could-have-invented-fractional-cascading/ "‘You Could Have Invented Fractional Cascading’, ezyang 2012"), [⁠⁠spectral sequences ⁠](https://gwern.net/doc/math/2006-chow.pdf) …)

Specifically, we understand that the self-attention functions mostly as a way to ‘propagate’ [multiplicative interactions ⁠](https://openreview.net/forum?id=rylnK6VtDH#google) around a large input sequence/  history, providing ‘direct access’ for the MLPs to compute on—as opposed to the hidden-state bottleneck of [RNNs ⁠](https://en.wikipedia.org/wiki/Recurrent_neural_network), where it’s hard to learn what is relevant in the history & ensure it gets propagated.

So we can now tell a history of developing more powerful sequence prediction models (as shown by their lower perplexity at each step), which culminate in a contemporary Transformer.

---

Such a tutorial might go like this:

We start with classic [*n* -grams ⁠](https://en.wikipedia.org/wiki/N-gram), on a small intuitive dataset like [Tiny Shakespeare](https://karpathy.github.io/2015/05/21/rnn-effectiveness/). Their most obvious limitation is difficulty estimating rare combinations of words, especially unseen ones (the 0-count problem). The classic approaches of [adaptive smoothing ⁠](https://en.wikipedia.org/wiki/Adaptive_smoothing) like Laplace or [Good-Turing ⁠](https://en.wikipedia.org/wiki/Good%E2%80%93Turing_frequency_estimation) help but are clearly inadequate to solve the [curse of dimensionality ⁠](https://en.wikipedia.org/wiki/Curse_of_dimensionality), when we must estimate each one in isolation, by itself. (Clearly, that is not necessary, nor is it how humans handle novel combinations of words.)

We can try to cluster ‘similar’ words, and introduce the idea of turning words into summarized ‘fingerprints’, or [embeddings ⁠](https://en.wikipedia.org/wiki/Word_embedding), and then predict *n* -gram probabilities from ‘nearby’ words. By learning a dense vector for each word, the model can understand that “king” is similar to “queen” even if a specific *n* -gram like “the king spoke” is rare but “the queen spoke” is common.

This ‘shares statistical strength’ and is the first step towards abstraction.

---

This still has weaknesses in generalizing when there’s not enough data. So this motivates the use of a function approximator to *learn* to estimate each one by learning the embedding. Then we can use it by just sliding the neural network over the sequence.

How do we learn an embedding? We can train embeddings separately, like the famous [word2vec ⁠](https://en.wikipedia.org/wiki/Word2vec), but they may not be optimized [end-to-end ⁠](https://gwern.net/doc/cs/end-to-end-principle/index) for sequence prediction on our current data. So we then want to learn the embeddings as part of our sequence prediction model. This leads to [⁠Bengio’s simple 2003 LM ⁠](https://jmlr.org/papers/volume3/bengio03a/bengio03a.pdf).

The limitations become obvious in that the different tokens do not interact well with each other: it is obvious that words are extremely contextual, and we need some way to treat “river bank” differently from “investment bank”. We can try to make the LM fixed-size window bigger and bigger, but what worked well at a window of 3 words explodes at 10 words. What if, instead of a unique weight for the first word in the window, the second, etc, we had a set of *shared weights* that slide across the window? This way, the same pattern detector (eg. ‘adjective noun’) can be found anywhere. This motivates taking a LM and sliding it over windows.

We can try a simple [bag-of-words ⁠](https://openreview.net/forum?id=SkfMWhAqYQ) LM, where we average all the embeddings in the window; this doesn’t work well; we then learn positional weights; this works better and is *almost* a convolution. Then we introduce convolutions with fixed weights looking at a small local region each time, which slide over it (depth-wise 1-D conv with kernel size = *k*). But we haven’t solved the fixed-window problem.

Dilated convolutions (famously used in [⁠WaveNet ⁠](https://deepmind.google/discover/blog/wavenet-a-generative-model-for-raw-audio/)) help handle long sequences as the ‘effective window’ grows exponentially fast with each layer, but still are weak and struggle to propagate or interact signals from different places in the sequence. Dilated convolutions are better, but information still has to pass through many layers to get from the start of a long sequence to the end: this makes it hard to track something as simple as a pronoun or pluralization, because the right information has to survive multiple layers before it becomes relevant. Our NN keeps ‘forgetting’ internally.

The signal is too indirect. Can we make every token directly ‘aware’ of every other token, somehow?

---

We can ask how we can mix tokens quicker, and have a ‘convolution which sees all tokens’. What sort of ‘sliding’ our NN along the input can do better? More sliding in various directions, perhaps?

This leads to the simple but performant [MLP-Mixer ⁠](https://arxiv.org/abs/2105.01601#google). MLP-Mixer is introduced to allow global context fusion—every word can now influence every other, though fixed by the frozen learned weights. We can frame its “token-mixing MLPs” as a more general way of allowing all tokens to interact (like a very large convolutional filter that sees all tokens), and “channel-mixing MLPs” as operating along the feature dimension. The key is to highlight how information from different parts of the sequence is combined: like a spreadsheet or table, down vs across.

Making the MLPs deeper quickly leads to problems with optimization, however: classic vanishing/  exploding gradients. We fix the optimization by introducing residual layers and regularization [like bottlenecks ⁠](https://arxiv.org/abs/2306.13575) or [dropout ⁠](https://en.wikipedia.org/wiki/Dilution_\(neural_networks\)) or [weight decay ⁠](https://arxiv.org/abs/1711.05101). But it still seems slow and data-hungry.

---

But we can then ask: what if we let those weights vary? That gives us [dynamic convolutions ⁠](https://arxiv.org/abs/1901.10430#facebook). They give us convolutions which now depend on the tokens themselves, within a small local region.

Dynamic convolutions adapt their weights based on the input. What if, instead of a local filter, we wanted each token to compute its own ‘mixing weights’ for *every other token* in the entire sequence? And what if these weights were determined by how relevant or compatible pairs of tokens are?

This is the single trickiest step here: it’s not obvious how you go from dynamic convolutions to QKV self-attention. You will probably want to start with a very crude QKV first, with simple weighted sums or only looking at one token, perhaps. There may need to be a detour here through ‘hard’ attention first, trained with a simple [REINFORCE ⁠](https://en.wikipedia.org/wiki/Reinforcement_learning#REINFORCE) or [CMA-ES ⁠](https://en.wikipedia.org/wiki/CMA-ES) approach, working with just a few tokens in a discrete ‘hard’ way, before we motivate the now-universal ‘soft’ or quadratic attention as a generalization of ‘but why forbid all the other tokens from helping out?’.

Now we can proceed to global mixing with the QKV formulation as our answer for fully dynamic, context-aware mixing. This yields ([single-headed ⁠](https://arxiv.org/abs/1911.11423)?) self-attention and a [Set Transformer ⁠](https://arxiv.org/abs/1810.00825).

Finally, because sets are not a great representation of an ordered sequence (although still feasible—consider that you can guess what is *probably* meant by the set `{”cat”, “chases”, “dog”}`, but when you guess wrong, you are very wrong), one introduces positional embeddings to break the set symmetries…

Adding the index is a good starting point, but has flaws compared to more sophisticated embeddings like sinusoidal or [RoPE ⁠](https://arxiv.org/abs/2104.09864), etc, but you can [⁠get there by logical improvements](https://fleetwood.dev/posts/you-could-have-designed-SOTA-positional-encoding "‘You could have designed state-of-the-art Positional Encoding’, Fleetwood 2024").

---

And now one is *almost* at a normal Transformer! A multi-head Transformer is just a single-headed Transformer but more so. It turns out that it is more useful to have a few small heads than one big head, as they can specialize and look at different parts of the problem, and we can get an idea of what each one is ‘thinking’ by just looking at what tokens they attend to.

The various normalizations are just an empirical matter of which one optimizes better, and can be left to neural architecture search, and all of the optimizations are now easily motivated as ways to more efficiently do something our basic Transformer does slowly.

By this point, the mysterious magic of the Transformer and QKV mumbo-jumbo has been dissolved. Transformers now look like a fancier MLP which happens to implement a complicated but effective way of doing token-mixing inspired by RNNs (whose various problems and solutions are now clearer by analogy to what we observed along the way), and heavily tweaked empirically to eke out a bit more performance with various add-ons and doodads; each of those additions solves a problem that naturally arose after we pushed an earlier version to its limits, and no longer looks like it was dropped off by friendly space aliens.

---

By the end, it is now “obvious” that Transformers, or something like them, *could* work well, and how one could have invented them. (Although there are limits to how much intuition building we can do at this small scale: it’s not obvious that things like [⁠induction heads ⁠](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html#anthropic) would be learned, or that ‘in-context learning’ is even possible or would [do any meta-learning ⁠](https://gwern.net/doc/ai/nn/transformer/attention/meta-descent/index); we will probably still remain surprised by what Transformers can do when we scale them to billions of parameters on Internet-scale datasets—making *that* intuitive probably requires an entirely different tutorial.)

---

A good followup tutorial would be taxonomizing the zoo of state-space models and RNN variants (eg. the historical Transformer anticipation of [fast weight programmers ⁠](https://arxiv.org/abs/2102.11174#schmidhuber)), and trying to understand them as moving back and forth between steps here, or offering an alternate solution to some of the problems that Transformers solved.

> Our interest does not fall back upon these causes of the formation of concepts; we are not doing natural science; nor yet natural history—since we can also invent fictitious natural history for our purpose…Is scientific progress useful for philosophy? Certainly. The realities that are discovered lighten the philosopher’s task, imagining possibilities.
> 
> Wittgenstein

\[[⁠Return to blog index ⁠](https://gwern.net/blog/index)\]