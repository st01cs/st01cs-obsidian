---
title: "A visual introduction to vector embeddings"
source: "https://blog.pamelafox.org/2025/05/a-visual-exploration-of-vector.html"
author:
published:
created: 2025-10-01
description: "For Pycon 2025, I created a poster exploring vector embedding models, which you can download at full-size .    In this post, I'll translate ..."
tags:
  - "clippings"
---
*For Pycon 2025, I created a poster exploring vector embedding models, which you can [download at full-size](https://drive.google.com/file/d/1pnI2XGxwhQQDKF2Ktl2XvaUUf294_-Qe/view). In this post, I'll translate that poster into words.*

## Vector embeddings

A **vector embedding** is a mapping from an input (like a word, list of words, or image) into a list of floating point numbers. That list of numbers represents that input in the multidimensional embedding space of the model. We refer to the length of the list as its **dimensions**, so a list with 1024 numbers would have 1024 dimensions.

![The word dog is sent to an embedding model and a list of floating point numbers is returned](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiRJ9rX6o3j7_X8_zNMOjq0DeUEiKn-spn_qMjetcJZd2mjzAn8WTmPeRqOSGjHa-GfcUUSxOhpIYDzexwzCeG8fh4EtRq58clDKvto2vgjxVwL_2JcfdDhICtWcRtmjAvndoNWqClx3FkkucetCOWdxmadu28xfIHiLaH9Itpeupx8-y2jXfwkn_U7zQ/s1600/Screenshot%202025-05-28%20at%2011.52.58%E2%80%AFAM.png)

  

## Embedding models

Each embedding model has its own dimension length, allowed input types, similarity space, and other characteristics.

### word2vec

For a long time, word2vec was the most well-known embedding model. It could only accept single words, but it was easily trainable on any machine, it is very good at representing the semantic meaning of words. A typical word2vec model outputs vectors of 300 dimensions, though you can customize that during training. This chart shows the 300 dimensions for the word "queen" from a word2vec model that was trained on a Google News dataset:  
![Chart showing 300 dimensions on x axis with values from -0.6 to 0.4](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhCHbjJcFGvFpQS-_Kl6a6Db5ZcLb7YOO-k1u0b9Nenb0t3SDsSTQ6IAyDllbVMOVX3DWY8UVrQn-S_cKKuXtIeFTTDjWz5SEWUO1FH92YKe-zoBdhCcnGwyJBLgD086j0IkoiSsCl7KsT9TC53KPLCs0WvnaQHeRDxFp7rw-Fj9LwzvWrgQU6Coah9HQ/s1600/model_word2vec.png)

### text-embedding-ada-002

When OpenAI came out with its chat models, it also offered embedding models, like text-embedding-ada-002 which was [released in 2022](https://openai.com/index/new-and-improved-embedding-model/). That model was significant for being powerful, fast, and significantly cheaper than previous models, and is still used by many developers. The text-embedding-ada-002 model accepts up to 8192 "tokens", where a "token" is the unit of measurement for the model (typically corresponding to a word or syllable), and outputs 1536 dimensions. Here are the 1536 dimensions for the word "queen":  
![Chart showing 1536 dimensions on x axis with y values from -0.7 to 0.2](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjk0PlMFLXByHXdffF6eoCUZHYnhhz5pgXnd0ful59lGGVBvb0Oa-F23eGYtGfEEk0p2Lv_wmj7Vk73ftcBWlsnHji0eg14HYlK8ZbOk2GZGnK_g0WgfxEFbjIl4BCubCCUekEXGiVGPEjptiOU_hvdgualw7R8Hg4fv1D_AszXbqw3C3TmboN436vpMg/s1600/model_ada002.png)  
Notice the strange spike downward at dimension 196? I found that spike in every single vector embedding generated from the model - short ones, long ones, English ones, Spanish ones, etc. For whatever reason, this model always produces a vector with that spike. Very peculiar!

### text-embedding-3-small

In 2024, OpenAI [announced two new embedding models](https://openai.com/index/new-embedding-models-and-api-updates/), text-embedding-3-small and text-embedding-3-large, which are once again faster and cheaper than the previous model. For this post, we'll use the text-embedding-3-small model as an example. Like the previous model, it accepts 8192 tokens, and outputs 1536 dimensions by default. As we'll see later, it optionally allows you to output less dimensions. Here are the 1536 dimensions for the word "queen":  
![Chart showing 1536 dimensions on x axis with y values from -0.1 to 0.1](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjDqIp7FlcMc6fAJVdHbsLzjrHQl5etibHz-LGnoT7Bc9ACfyHkCFWmNogiAIpwnlnH7AXcpM5nGQ1QHFs__CFx00o7hyphenhyphenJrxy4AE9KYtoLgbjkkRJx77oV79nWyhDoGuoFNo8mIErNeB4WS_qW1QXvpizZjEYGBNZ0O8omTHRHTp8mdogyOVHE5L3ErFw/s1600/model_emb3.png)  
This time, there is no downward spike, and all of the values look well distributed across the positive and negative.

  

## Similarity spaces

Why go through all this effort to turn inputs into embeddings? Once we have embeddings of different inputs from the same embedding model, then we can compare the vectors using a distance metric, and determine the relative similarity of inputs. Each model has its own "similarity space", so the similarity rankings will vary across models (sometimes only slightly, sometimes significantly). When you're choosing a model, you want to make sure that its similarity rankings are well aligned with human rankings.

For example, let's compare the embedding for "dog" to the embeddings for 1000 common English words, across each of the models, using the cosine similarity metric.

### word2vec similarity

For the word2vec model, here are the closest words to "dog", and the similarity distribution across all 1000 words:

![Similar words (cat, animal, horse) plus a chart with a histogram of similarity values](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj35tcxBW9_-o1ztJ4BYxk8BX5-jizx_UeLNkba5AeM2Zb3MQmCZpzTYaa8D2VvuCRv_2O1HfQ37VSGP_823XSjP0n23zfqHWRF9bD1B6Zwme9eTrAZKFvG2ebHa-PxPmRcoGXT_jlUAnxAkHlXSZxpS3qwIpH8KoBgqQBygCE6Z5T99Czah4GjBXCQmQ/s1600/word2vec_similar.png)

As you can see, the cosine similarity values range from 0 to 0.76, with most values clustered between 0 and 0.2.

### text-embedding-ada-002 similarity

For the text-embedding-ada-002 model, the closest words and similarity distribution is quite different:

![Similar words (animal, god, cat) plus a chart with a histogram of similarity values](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhyo6b_sCsvx6zULszvVQ-9ZDl8tCX9VzN8RcDpqm7RYLcWK0ARQIXZIjLEH6cTt6sJ7gcyJYNekFNZ9MZiE-1xzS5Mvfbh3UbUn1tOPOlvFy2EYHUEifUeIlAVJTFlehpwNhUzk4cby2y9tDcaA5QQ2WICRbxeXDZa-WKHmvXZcPVBkgfM0f4vsCMbtA/s1600/ada002_similarity.png)

Curiously, the model thinks that "god" is very similar to "dog". My theory is that OpenAI trained this model in a way that made it pay attention to spelling similarities, since that's the main way that "dog" and "god" are similar. Another curiousity is that the similarity values are in a very tight range, between 0.75 and 0.88. Many developers find that unintuitive, as we might see a value of 0.75 initially and think it indicates a very similar value, when it actually is the opposite for this model. That's why it's so important to look at *relative* similarity values, not absolute. Or, if you're going to look at absolute values, you must calibrate your expectations first based on the standard similarity range of each model.

### text-embedding-3-small similarity

The text-embedding-3-small model looks more similar to word2vec in terms of its closest words and similarity distribution:

![Similar words (animal, horse, cat) plus a chart with a histogram of similarity values](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiMXsVOksByaHKvOmVb8ZHFId01afwi7cU0zWUts6yL80pSO5mIZzsZ5HUIBBGr5JcEt4QRndEpHB3cc7K4J-qqG2Za1YecoV7X9QQVTbQ5-qRI1AIg2XWsegVMBlWWawQeGW8KVYr2_GkNa-ZEO_rS95O1pL-1ipdAdGLWkbPAOWut15MttuuJCTa1Eg/s1600/emb3_similarity.png)

The most similar words are all similarity in semantics only, no spelling, and the similarity values peak at 0.68, with most values between 0.2 and 0.4. My theory is that OpenAI saw the weirdness in the text-embedding-ada-002 model and cleaned it up in the text-embedding-3 models.

  

## Vector similarity metrics

There are multiple metrics we could possibly use to decide how "similar" two vectors are. We need to get a bit more math-y to understand the metrics, but I've found it helpful to know enough about metrics so that I can pick the right metric for each scenario.

### Cosine similarity

The **cosine similarity** metric is the most well known way to measure the similarity of two vectors, by taking the cosine of the angle between the two vectors.

![Graph showing two vectors with the angle shaded between them](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg9sQrIs7y_agKFhjHyIncbPv25wCAlh3haE9KFocgxB18L-x9b1nXGgW5tVrhgTS56FBZGTPhvM1QIGtS8kXNmRIT5l3TgFWHAsfpM4vEzFf65si8CBhcNJWMH49DNLMAM1ot0qpL3mvL4Axr6N3Dw7PcbLBI8lshL2MRxC9IWLh7YQ7G8D3Sah-coIg/s1600/cosine_distance.png)

For cosine similarity, the highest value of 1.0 signifies the two vectors are the most similar possible (overlapping completely, no angle between them). The lowest theoretical value is -1.0, but as we saw earlier, modern embedding models models tend to have a more narrow angular distribution, so all the cosine similarity values end up higher than 0.

Here's the formal definition for cosine similarity:  
![Cosine similarity = dot product of x and y, divided by product of magnitude of x and y](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhpRjmC6HnWc1o4CSH9aiX5OhLrRha9drRCuQGePL7x30VjRAekGAYgzIG0SbMrfTLMm-KDJ9B-DzREffP1JVTWu5A6Kmh9wmeHRTUOh0kDANWsWg1D_ljhAZW-6B4-2T3c6zOh2dykf4VjrqzwIbRw_tHlNNTBRQ9cuzwW_ej78DUT1UlEV5EwD_VsDQ/s1600/Screenshot%202025-05-28%20at%2012.22.32%E2%80%AFPM.png)  
That formula divides the dot product of the vectors by the product of their magnitudes.

### Dot product

The **dot product** is a metric that can be used on its own to measure similarity. The dot product sums up the products of corresponding vector elements:  
![Dot product = the sum of components of vectors](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjWYY4Q-TTusnpLvwdlv4zMct4E04LP0MFdzV6xEiX-_VPC6u-M_IgciYwt2ykDEl7Jr7c7D34uYb07cEQiRlcW4Ysg8sIkr4eTzt0hY6Bp750MeivB1zCd4CET1z-hS24PeTwRc5ZnkWP911GVcvQQbSFU-TZyV_tECS8PWcjLydHs20hvVH6i8xy4fA/s1600/Screenshot%202025-05-28%20at%2012.24.19%E2%80%AFPM.png)

Here's what's interesting: cosine similarity and dot product produce the *same exact values* for unit vectors. How come? A unit vector has a magnitude of 1, so the product of the magnitude of two unit vectors is also 1, which means that the cosine similarity formula simplifies to the dot product formula in that special case.

Many of the popular embedding models do indeed output unit vectors, like text-embedding-ada-002 and text-embedding-3-small. For models like those, we can sometimes get performance speedups from a vector database by using the simpler dot product metric instead of cosine similarity, since the database can skip the extra step to calculate the denominator.

## Vector distance metrics

Most vector databases also support **distance metrics**, where a *smaller* value indicates higher similarity. Two of them are related to the similarity metrics we just discussed: **cosine distance** is the complement of cosine similarity, and **negative inner product** is the negation of the dot product.

The **Euclidean distance** between two vectors is the straight-line distance between the vectors in multi-dimensional space - the path a bird would take to get straight from vector A to vector B.

![A graph showing Euclidean distance (a straight line) between two vectors](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgUpkDEBXr0a2JIrxcwyJ6Q26ufm5tBgXnuO9jNX86I6bZjMxR8_lZuRhKX1cNHmD90e8oPd3KdUInwPxrDgkbOPijcJCSD2MfbE9YJse_OG0uE5IKpboOM2K9u4-HEX8-5msslfD6oOFuE1czFXjzygXIptvpOMKdGD7MoaHUfQpOAwoFwjw0JMRvn5w/s1600/euclidean_distance.png)

The formula for calculating Euclidean distance:

![Euclidean distance = the square root of squares of component differences](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEixPkY4LhOSPRh_3CgoO0kA0D0yL-fQM8am0k3wilo92_C0UTwlgNruQ0PAMxt6RRbyjTl5v1owooOi9ixlzvR7vEKpKTMF9C-hkKWtRBED7nDIQ_RsdxHqF9AydqCprjJwaUtvZbr16zQJa4a1Ii5QQeZ0OJFZPopjdSUlQlzM_kbXMKDnicLAZfhMzA/s1600/Screenshot%202025-05-28%20at%2012.28.26%E2%80%AFPM.png)

The **Manhattan distance** is the "taxi-cab distance" between the vectors - the path a car would need to take along each dimension of the space. This distance will be longer than Euclidean distance, since it can't take any shortcuts.

![A graph showing Manhattan distance (a segmented line) between two vectors](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhZeUD02UXw0oeiWnGfs59WGMlaTfwMAVfPP78x13x9IjnbGvhUkHfWTthv3FAh-uw4n4sG8824MWq-_F1nbfdtdrZ2-xJyiT7zpDSX7WPiM80obRnmFHVrVy6FfzV8ySGS8mWIqTqlMcwzAhyphenhyphenIyIXx3HwJ96_EP5vJEttoQ_OFUQvWtpRPTMdo4MEAwQ/s1600/manhattan_distance.png)

The formula for Manhattan distance:

![Manhattan distance = The sum of the magnitude of component differences](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjRUMmxBArFpeD5KMuEa8THx6pP_3192KrCLo_9d_1i4N76I5lq2a9W9LUgodHitjm271kKP1OdTo4ts92VfewodHOVq7Eu9ef6X6trQxnGDdjmIR3hSH8VJ2o49XnGH6I-fQRHw5ObBbsMNsfL2mNvINwXTA3JZeFOwiVduCxfLXwQUGc-L_9Ne0mFsQ/s1600/Screenshot%202025-05-28%20at%2012.30.47%E2%80%AFPM.png)

When would you use Euclidean or Manhattan? We don't typically use these metrics with text embedding models, like all the ones we've been exploring in those post. However, if you are working with a vector where each dimension has a very specific meaning and has been constructed with per-dimension meaning intentionally, then these distance metrics may be the best ones for the job.

## Vector search

Once we can compute the similarity between two vectors, we can also compute the similarity between an arbitrary input vector and the existing vectors in a database. That's known as vector search, and it's the primary use case for vector embeddings these days. When we use vector search, we can find anything that is similar semantically, not just similar lexicographically. We can also use vector search across languages, since embedding models are frequently trained on more than just English data, and we can use vector search with images as well, if we use a multimodal embedding model that was trained on both text and images.

![An input vector is turned into an embedding, and that embedding is used to search other vectors](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_iVWvOJKEnaIF4PYEKJJJDsQv2kseLRfJkM8AxdW3Wt7LhvBqtP4aajKDbGmqc16EiLqShnGVjmqYSUxzPzP_-BxlIV8pB33i6zJvOuYyFnKbQnv0mSm6p9AW_Ijr8-R4oJT890C-uGxrj2-VSXq7KgmKaFVXvcuTHJZahyH4WVqCTACgNMaD90YHCA/s1600/Screenshot%202025-05-28%20at%2012.33.59%E2%80%AFPM.png)

When we have a small number of vectors, we can do an **exhaustive search**, measuring the similarity between the input vector and every single stored vector, and returning the full ranked list.

However, once we start growing our vector database size, we typically need to use an **Approximate Nearest Neighbors (ANN) algorithm** to search the embedding space heuristically. A popular algorithm is HNSW, but other algorithms can also be used, depending on what your vector database supports and your application requirements.

| Algorithm | Python package | Example database support |
| --- | --- | --- |
| HNSW | hnswlib | PostgreSQL pgvector extension   Azure AI Search   Chromadb   Weaviate |
| DiskANN | diskannpy | Cosmos DB |
| IVFFlat | faiss | PostgreSQL pgvector extension |
| Faiss | faiss | None, [in-memory index only\*](https://github.com/facebookresearch/faiss/wiki/Indexes-that-do-not-fit-in-RAM) |

  
  

## Vector compression

When our database grows to include millions or even billions of vectors, we start to feel the effects of vector size. It takes a lot of space to store thousands of floating point numbers, and it takes up computation time to calculate their similarity. There are two techniques that we can use to reduce vector size: quantization and dimension reduction.

### Scalar quantization

A floating point number requires significant storage space, either 32 bits or 64 bits. The process of **scalar quantization** turns each floating point number into an 8-bit signed integer. First, the minimum and maximum values are determined, based off either the current known values, or a hardcoded min/max for the given embedding model. Then, each floating point number is re-mapped to a number between -127 to 128.

![Diagram showing range from min value to max value being mapped to -127 to 128](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg7UWcr8kAJT3KR_8d6Pd4CfLhBFBL2lnwmvW058baBIqGyPscbrOZChjD9_9c8Tg1EZ3twV5AiqGjOJ7oO3gN3NT_q4pkbkrNbbJdPIdUfM4dchpXpLUkBEHWR47GrW2b9pDhIQ8QQEzrZhSB4bkCJXgJWA9vQrPmdfRcjFeCxsh8xLQdFU5V-Ax5jRg/s1600/Screenshot%202025-05-28%20at%2012.37.09%E2%80%AFPM.png)

The resulting list of integers requires ~13% of the original storage, but can still be used for similarity and search, with similar outputs. For example, compare the most similar movie titles to "Moana" between the original floating point vectors and the scalar quantized vectors:

![Table showing most similar movie titles to Moana, before and after scalar quantization - only two movies change position](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEggcrlgY-GZL2YlKBrxwyD6lj6PSGIyCSRQU0QDoHPtmVOXduCcnCjjBRcFg-nHS5LaJHX6HhVa-C17qiQwtzB9wUFKf8WkSAKbmfVecqRPxnHo2kmMXilcxd1jV3dEf6BcE5E9UHc3uchc7-dEzX2e9-HKsclagIFvReeffzJoTQt05Z3yLOm1aLBkPA/s1600/moana_similar_scalar.png)

### Binary quantization

A more extreme form of compression is **binary quantization**: turning each floating point number into a single bit, 0 or 1. For this process, the centroid between the minimum and maximum is determined, and any lower value becomes 0 while any higher value becomes 1.

![Diagram showing range from min value to max value being mapped to 0 or 1](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh3AiDmS7Yh8Jv2vxfibCM-xOrn3a6wcpkygRCda2pGtlak_SVnpAjLyXjBgO9Or8o-D0-pCaFymE756a3svPXiGlcYKJp-Lf18ngo0woXnoqXurDFnorkUIdEOL_NFcVgU1uQYJtHPSzC9bRRbr3ppHhpbdqZcDF8AKCs4kPJqLRMNoVn-HWcdMh0DJg/s1600/Screenshot%202025-05-28%20at%2012.41.00%E2%80%AFPM.png)

In theory, the resulting list of bits requires only 13% of the storage needed for scalar quantization, but that's only the case if the vector database supports **bit-packing** - if it has the ability to store multiple bits into a single byte of memory. Incredibly, the list of bits still retains a lot of the original semantic information. Here's a comparison once again for "Moana", this time between the scalar and binary quantized vectors:

![Table showing most similar movie titles to Moana, before and after binary quantization - only two movies change position](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgF4nuYdxEGGHNNm2QPukIv6WC_3jhTHlqViaWBF7sdgv6dpYjMTGHACZEVNpp0zMGbEJKFmJGdRNn54GTnfB9zFOWzRR6dEjfYpo4wUidadwvFwTl1zpgsagJdz-JFFXnvM29Ett0iHdSvGPJRhgmypGJKOS7KPij8XHekEW0H1sTiPX5R_YK8gsuNvA/s1600/Screenshot%202025-05-28%20at%2012.42.17%E2%80%AFPM.png)

  

### Dimension reduction

Another way to compress vectors is to reduce their dimensions - to shorten the length of the list. This is only possible in models that were trained to support [Matryoska Representation Learning (MRL)](https://huggingface.co/blog/matryoshka#theoretically-1). Fortunately, many newer models like text-embedding-3 were trained with MRL and thus support dimension reduction. In the case of text-embedding-3-small, the default/maximum dimension count is 1536, but the model can be reduced all the way down to 256.

![Diagram showing vector dimension reudction](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXkDkC9US_rPcgnl35RjSUUA36KbK3KgoqgQn6kX5C-YcNyCkoBcJBRfTULPN2xWnMnjlMXPELjJ8tmAuPTsYUOCquj0OXYfgJw8TeB6MvvRe69U8W1vCYWX7GVxthSzNOzMMUPYUr3KCsOB_RXTvMy9xvOnztnufDz2iudKsClcflGeifpaX2MPFPxQ/s1600/Screenshot%202025-05-28%20at%2012.45.49%E2%80%AFPM.png)

You can reduce the dimensions for a vector either via the API call, or you can do it yourself, by slicing the vector and normalizing the result. Here's a comparison of the values between a full 1536 dimension vector and its reduced 256 version, for text-embedding-3-small:

![Graphs for vectors with 1536 dimension, then with 256 dimensions](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhcsiuRtTa3VDK_f80DRXOkS3fMW9Go04PXJ9m4llnEi7umjZzgkH99h2TV7rkragarsd5d2q5loyDyfgOhCEBnMh6UYdYKSr9SG0vaX3YxIsSXBsbmxUYmgsHBHVMugo5OuqLjWIjGWy4lSCO2ZrozultgH3OnScCZijhRFQHbOrYcg_eJ81-ijEZyGw/s1600/Screenshot%202025-05-28%20at%2012.46.35%E2%80%AFPM.png)

  

### Compression with rescoring

For optimal compression, you can combine both quantization and dimension reduction:

![Diagram showing vector dimension reduction followed by quantization](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjXvkwolV2eTCoNTEUPRc6v5_Y5tz6wQPhbtTxXEoZ135_ORDpb9OS1tCuP4rfKuTJdB4YnWDUevTZ9-9SI7gc8WZHBkbIxH5LEfVa6lf5aDeS40ihyWxUmNcXJoT0tsvbNodHvJC6n513MjDnwyBSsaRpo_o6sYVo6YqUZSulwGyOEmZeTMnlGQEzBjQ/s1600/Screenshot%202025-05-28%20at%2012.49.22%E2%80%AFPM.png)

However, you will definitely see a quality degradation for vector search results. There's a way you can both save on storage and get high quality results, however:

1. For the vector index, use the compressed vectors
2. Store the original vectors as well, but don't index them
3. When performing a vector search, oversample: request 10x the N that you actually need
4. For each result that comes back, swap their compressed vector with original vector
5. Rescore every result using the original vectors
6. Only use the top N of the rescored results

That sounds like a fair bit of work to implement yourself, but databases like Azure AI Search offer [rescoring](https://github.com/microsoft/rag-time/tree/main/Journey%203%20-%20Optimize%20your%20Vector%20Index%20for%20Scale) as a built-in feature, so you may find that your vector database makes it easy for you.

### Additional resources

If you want to keep digging into vector embeddings:

1. Explore the [Jupyter notebooks](https://github.com/pamelafox/vector-embeddings-demos) that generated all the visualizations above
2. Check out the links at the bottom of each of those notebooks for further learning
3. Watch my talk about [vector embeddings](https://www.youtube.com/watch?v=lyIJcHKA6b0) from the [Python + AI series](https://techcommunity.microsoft.com/blog/EducatorDeveloperBlog/learn-python--ai-from-our-video-series/4400393)