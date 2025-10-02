---
title: "My Experiments with NotebookLM for Teaching"
source: "https://towardsdatascience.com/my-experiments-with-notebooklm-for-teaching/"
author:
  - "[[Parul Pandey]]"
published: 2025-09-17
created: 2025-10-01
description: "Exploring NotebookLM as a teaching companion"
tags:
  - "clippings"
---
[Skip to content](https://towardsdatascience.com/my-experiments-with-notebooklm-for-teaching/#wp--skip-link--target)

  
If you were to scroll through my recent [X timeline](https://x.com/pandeyparul), you’d notice I’ve been experimenting with a lot of different AI tools for the purpose of teaching. I have been working on this project for nearly a year, primarily to explore how we can utilize AI to enhance the interactivity and effectiveness of learning. My focus is on educators, parents, and teachers so that they spend less time searching for resources online and more time with the students. I’m aware that there are already a ton of educational sites out there, but in my experience, they suffer from two main issues:

• A lot of these tools require unnecessary signups and are filled with a lot of irrelevant ads.  
• Sometimes the content is just not tailored to our requirements. Either it’s too basic or too complex.

That’s why I started coding my own tools or creating custom resources by mixing and matching what’s available. Based on the positive responses I’m getting from the community, I’ve now compiled them in this article, starting with NotebookLM. Over time, I plan to continue this series with other tools as well.

Through this article, I share my experiences of using NotebookLM to teach more effectively, focusing on the K—10 age group kids.

## Why NotebookLM for Education

The tagline for [NotebookLM](https://notebooklm.google/) is ***understand anything,*** and it really lives up to that. NotebookLM has been a great companion for me. I have been using it in a variety of ways, from understanding research papers to organizing ideas, summarizing technical talks, and a lot more. But it can be an effective tool for teaching as well, due to its features like mind maps, flashcards, quiz generator, customizable reports, video overviews, etc.

What really stands out for me is that the answers are strongly grounded in the actual information provided. That’s one of the most important requirements when using any tool for education. You don’t want a hallucinating assistant, especially when it’s being used to study.

## 1\. Making History Dates Easy to Remember

NotebookLM has a **timeline feature** that can automatically generate timelines from the sources you provide. This is especially useful for remembering important dates or events in history, making it easier for students to see how things connect over time.

Let’s see it in action. Below, I’ve pasted some text from Wikipedia on human history as a source in NotebookLM. Then, by going to **Reports** and selecting the **Timeline** option, I can get a clear timeline of the main events.

To make these dates stick, kids need something visual. You can take the generated timeline and copy it into another tool called [**NapkinAI**](https://www.napkin.ai/), which is designed to turn text into visuals. NapkinAI will automatically convert into a nice timeline chart that students can use for studying or even include in their projects.

![](https://www.youtube.com/watch?v=8N4R0sgK7Zo)

*Turning Wikipedia text into visual history timelines with NotebookLM + NapkinAI.* Video by Author

---

But we don’t need to stop at history lessons; it works for academic papers, too. Just swap the source with a research paper and follow the same steps. It’s a neat way to pull out all the key milestones that led up to that particular research.

![](https://contributor.insightmediagroup.io/wp-content/uploads/2025/09/11tgzye1CQtE8iaJxDXwwaA.gif)

Extracting milestones from research papers and turning them into timeline charts with NotebookLM + NapkinAI. Video by Author

## 2\. Turn Lessons into interactive Crosswords

Students love crosswords, and if we can turn their lessons into crosswords, they’ll not only enjoy solving them, but it’s an excellent way to help them remember their lessons in a fun way. It’s also a great method to test understanding.

For this, we’ll use [**CrosswordLabs**](https://crosswordlabs.com/), a free website that makes it easy to create crosswords. But instead of making random ones, we’ll pull the clues directly from lesson plans.

Add your lesson materials to **NotebookLM**. Now, CrosswordLabs expects clues in a specific format:

```markup
dog Man's best friend
cat Likes to chase mice
bat Flying mammal
elephant Has a trunk
kangaroo Large marsupial
```

To generate clues from your lessons in this format, prompt NotebookLM with a few-shot example like the one above. For instance, the prompt can be:

```markup
Given the lesson text, create word–clue pairs in this style:
dog Man's best friend
cat Likes to chase mice
bat Flying mammal.
```

Take the generated output and paste it into CrosswordLabs, and it will auto-build your crossword. Once it’s ready, you can print it, download it as a PDF, or share the link so students can solve it online.

![](https://contributor.insightmediagroup.io/wp-content/uploads/2025/09/1NkwvaeOaYVLTKIzZZfSLzg.gif)

From lesson text → word–clue pairs → instant crosswords with NotebookLM + CrosswordLabs. Video by Author

## 3\. From Study Guides to Storybooks

[Storybook](https://gemini.google/overview/storybook/) is a great feature in the [Gemini App](https://gemini.google.com/app?hl=en-IN) and one of my favorites. It allows you to create a 10-page, personalized, and illustrated storybook for any topic, idea, or situation you have in mind. Apart from being fun, these storybooks are incredibly useful for teaching new concepts to students. This is because you can tailor them based on their interests. For instance, if your students like Legos, you can generate one around that theme. Maybe they enjoy picnics, create one around that instead.

What is even more useful is that this technique can help students understand complex topics. So, if you’re an educator planning to introduce a new concept, here’s how you can use the Gemini Storybook feature together with NotebookLM to make it easier:

- First, create a simple study guide in NotebookLM from the material that you are planning to use.
- Paste the generated guide in the Gemini App along with the prompt:
```markup
Create a unique storybook about the study guide I've uploaded.
Tailor it for a 2nd grade kid.
```

Here is how I created a storybook to introduce the concept of Magnetism to fifth graders.

![](https://contributor.insightmediagroup.io/wp-content/uploads/2025/09/1JRIBT78HdxHDQOhZqRqGYw.gif)

I turned a NotebookLM study guide on Magnetism into a fun illustrated storybook with Gemini. Video by Author

  
It’s a quick way to turn your syllabus into something students actually enjoy learning from.

## 4\. NotebookLM + Google AI Studio

I love the mindmaps from NotebookLM because they capture the whole topic so well. But for kids, plain text isn’t enough, so I turned to Google AI Studio to build an image flashcard generator from scratch. While NotebookLM recently added a Flashcard Generator, it’s text-based.

[Google AI Studio](https://aistudio.google.com/apps) hosts a variety of applets that can be remixed, making it easy to build on top of them. It works like an experimental playground to test Google Gemini models and create prototypes, which can then be deployed on the cloud. One of the applets was designed for generating flashcards, so I modified the flashcard app to pair text with images, making the flashcards more engaging and kid-friendly.

![](https://contributor.insightmediagroup.io/wp-content/uploads/2025/09/1btrfZ6zjvZ63_pQxwQ_1VA.gif)

Upgrading text-only mindmaps into image flashcards with NotebookLM + Google AI Studio. Video by Author

I have published the [app](https://aistudio.google.com/apps/drive/17wgHsdaCI89z3RK0GsWJsgpKzv_0VL_o?showPreview=true&showAssistant=true), and now you can use it as it is or make your own version of it.

## 5\. NotebookLM for learning a new language

I’ve been experimenting with **NotebookLM** for language learning, and the new Flashcards + Custom Reports feature fits really well. Since NotebookLM now supports many languages, I tried customizing prompts so that the outputs feel more like a language teacher explaining concepts, rather than just raw translations.

In case you missed it, NotebookLM now comes with a custom reports feature. This means instead of just getting the regular reports, you can create your own report based on your preference and output language.

![](https://contributor.insightmediagroup.io/wp-content/uploads/2025/09/1mpBh7ys1BR3GtF-4VWHpQ.png)

Custom reports option in NotebookLM | Image by Author

So let’s say I’m an English speaker and I want to learn Hindi. I can take any Hindi passage that I want to understand, generate a custom report by specifying the output language as Hindi, and then save that report as a source in NotebookLM. From there, I can create flashcards directly from the source.

For example, the report prompt could be:

```markup
You are a Hindi–English language tutor for kids who know English but are learning Hindi through stories. I will give you a Hindi story. Create a structured bilingual learning report in this format:

Title of the story in Hindi and English

Introduction in English: Explain what the story is about in a friendly way

For each sentence in the story:
• Write the original sentence in Hindi
• Give a simple English translation"*
 Read the passage below and rewrite it in simple Hindi with grammar notes and word meanings in brackets.
```
![](https://contributor.insightmediagroup.io/wp-content/uploads/2025/09/1j0Vrf9kaFwOiyQG3L3KuBg.gif)

Using Custom Reports + Flashcards in NotebookLM to make Hindi learning more like a real tutor. Video by Author

While there are plenty of good apps for learning a new language, not everyone learns best by answering a repetitive set of questions. For many people, myself included, it’s easier and more effective when an expert explains the grammatical nuances. In this case, that expert can be NotebookLM.

## Conclusion

In this article, I’ve shared some of my experiments in the AI for education space using NotebookLM. Every child learns at their own pace and through different mechanisms. With AI, I believe we can offer a more personalized approach to teaching by creating content tailored to each learner. As I mentioned earlier, my focus is on empowering educators, since they are the ones who need the right tools to guide students effectively. This could help them save time, reduce effort, and focus more on the actual learning journey with their students.

---

Written By

Parul Pandey

, , , ,

Towards Data Science is a community publication. Submit your insights to reach our global audience and earn through the TDS Author Payment Program.

[Write for TDS](https://towardsdatascience.com/questions-96667b06af5/)

## Related Articles

- ![](https://towardsdatascience.com/wp-content/uploads/2025/07/doppleware_two_modern_robots_using_a_tin-can_phone_and_wire_t_bff835d3-b41a-4957-aeb4-13226f1760b2_0.png)
	## Talk to my Agent
	The exciting new world of designing conversation driven APIs for LLMs.
	9 min read
- ![Illustration of robots evaluating a model](https://towardsdatascience.com/wp-content/uploads/2025/07/image-345.png)
	Illustration of robots evaluating a model
	## How to Evaluate Graph Retrieval in MCP Agentic Systems
	A framework for measuring retrieval quality in Model Context Protocol agents.
	9 min read
- ![](https://towardsdatascience.com/wp-content/uploads/2025/08/ChatGPT-Image-Aug-3-2025-11_57_46-AM.png)
	## Finding Golden Examples: A Smarter Approach to In-Context Learning
	From random example selection to systematic AuPair generation  — how to make your LLM prompts actually…
	7 min read
- ![](https://towardsdatascience.com/wp-content/uploads/2025/08/ChatGPT-Image-20-ago-2025-09_29_42.jpg)
	## “Where’s Marta?”: How We Removed Uncertainty From AI Reasoning
	A primer on overcoming LLM limitations with formal verification.
	12 min read
- ![](https://towardsdatascience.com/wp-content/uploads/2025/08/unlocking-multimodal-video-transcription.gif)
	## Unlocking Multimodal Video Transcription with Gemini
	Explore how to transcribe videos with speaker identification in a single prompt
	66 min read
- ![](https://towardsdatascience.com/wp-content/uploads/2025/08/0Ul9PApxHSz02D3_D.webp)
	## How to Develop a Bilingual Voice Assistant
	Exploring ways to make voice assistants more personal
	8 min read
- ![Image by Author.](https://towardsdatascience.com/wp-content/uploads/2025/09/tds.png)
	Image by Author.
	## AI Operations Under the Hood: Challenges and Best Practices
	Building robust, reproducible, and reliable GenAI applications requires a framework of continuous improvement, rigorous evaluation,…
	18 min read

Some areas of this page may shift around if you resize the browser window. Be sure to check heading and document order.