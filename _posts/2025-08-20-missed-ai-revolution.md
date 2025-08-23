---
layout: post
title: "What I Learned From Building LLM Infrastructure After Missing the AI Revolution"
date: 2025-08-20
categories: [ai, llm, infrastructure]
tags: [ai, llm, infrastructure]
---

I left tech to pursue advertising in summer 2022, before AI really took off. During my time as a copywriter, AI tools became widespread seemingly overnight. Taking on an LLM API project this summer was as much about refreshing my coding skills as it was about demystifying this technology that's reshaping our world.

## From Magic to Reality Check

The first time I used Cursor to write code, my jaw hit the floor. I was genuinely mesmerized watching it generate entire files in seconds. But nothing could've snapped me out of it faster than Claude trying to hardcode database auth into a docker compose file. It was a moment that perfectly captured AI's unique way of oscillating between the self-assured troubleshooting of a senior engineer to some kind of summer intern from hell.

(I just learned what vibe coding is this week by the way – a new approach where developers use AI tools to generate code based on natural language prompts. In other words, based on "vibes." It sounds misleadingly calm and laidback, but at least in my experience, coding with agents has more of a "you're a helicopter parent to a robot" type vibe than the "feet on the desk chillin'" vibe I expected.)

## CPU-Only LLMs: When Sluggishness is Part of the Charm

For my LLM project, I wanted to understand the fundamentals without breaking the bank. I chose Hetzner for hosting and looked into CPU-only models. Part of the appeal of self-hosting your own LLM is that you can have chats without your data going to Google or OpenAI. But despite legitimate concerns about privacy, the vast majority of people have no option but use the major AI tools like ChatGPT, CoPilot, Gemini, etc. Their dominance in the market, and therefore convenience factor – not to mention the technical and economic hurdles of setting up your own private model – mean that privacy, as usual, is forced to take a back seat to practicality.

That said, the prevalence of mainstream tools doesn’t mean innovation or alternatives are out of reach. At the end of the day, experimenting and imagining new ways of doing things is what engineering is all about. While my app is charmingly unusable in its slowness, I built the infrastructure so one could easily switch out the models, inference engine, and hosting environment. It was an exercise in understanding how these applications actually work.

## Demystifying the Components

**A LLM** (Large Language Model) is like a master chef who has trained by tasting thousands of dishes and internalized patterns of what makes food delicious.

In reality, a model is just a giant file of numbers – millions or billions of numerical parameters encoding everything learned during training. 

**Inference** is using the model to answer questions, generate images, etc. Inference is the actual cooking process. When you ask the model to generate text, it uses those learned patterns to make decisions.

The **inference engine** is the kitchen itself: the computational environment that makes it possible for our chef to get to work.

It wasn't until I saw the price tags on the GCP Compute Engine page for GPU-resourced VMs that I began to understand just how much power LLMs need – even on a small scale!

I had been researching ratings and reviews of different models, was hearing good things about the model Mistral 7b, and was planning on using it for my app.

Then I learned that a "budget" or smaller version of Mistral 7b would still require ~8-12 GB of VRAM (dedicated GPU memory) to function properly. And I learned that an AWS instance that could support that could run you upwards of $300/month.

That's for a smaller version of Mistral 7b, mind you, where its inference is scaled down. The "Mid-tier GPU inference" – the FP16 version – would require ~24GB of VRAM for smooth inference. Which could run you upwards of $3k/month for the appropriate AWS instance.

So yes, that's why even though I definitely, totally have $3k to dish out monthly for my LLM pet project, I opted for the slowest, tiniest (but highly recommended) model I could find: GPT4All.

All of this put into perspective the computational power needed for AI on an enterprise scale. And when you think about companies training models on the entire internet's worth of data, the scale is truly mind-boggling.

## What This Project Taught Me

### 1. The Infrastructure Reality
Running even a small LLM gave me deep appreciation for the engineering challenges at scale. Meaning that optimization is no joke.

### 2. The Experimentation Framework
In an ideal world, I would have loved to deploy dozens of different models and built dashboards comparing cost, speed, accuracy, and specialization. (I know those dashboards exist somewhere and still would love to see them. 👀)

### 3. It's Time to Demystify AI
There's a lot of misunderstanding around what AI is as a technology. In order for more people to have a say in how AI shapes our world, there needs to be more readily available, accurate information about what it is and how it works. There's a need to demystify AI because it's here whether we like it or not. It's actually crucial for more people to understand how AI works because of the sheer magnitude with which it's affecting our world. It's changing our daily interactions, our work, and ultimately it's reshaping the entire economy in ways we haven't fully felt yet.

The comparison to the assembly line or steam engine isn't hyperbole. While the full consequences aren't visible yet, the transformation is already underway. Understanding how these systems work, their limitations, and how they can be changed, isn't just a question of technical curiosity, it's a collective necessity.

### 4. Creative Engineering Exists
I've always been drawn to the creative aspects of engineering: the problem-solving, the elegant solutions, the way good infrastructure feels like art. In my opinion, AI expands that human creative potential – because its power comes from human creativity and work in the first place. The question becomes – like with any epoch-shaping technology – who has oversight and calls the shots on how AI is used at the end of the day?

## The Rip Van Winkle Effect
#### (Is that a dated reference? Besides in the obvious way.)
This has been a fascinating time-skip back into tech. Missing the initial AI explosion and returning to discover a self-coding VSCode has been eye-opening to say the least.

I think AI is an incredible breakthrough with massive both creative and destructive potential. The direction it goes will be determined by who controls it in the future on a massive scale. I think the more people who learn about AI, demystify AI, and imagine ways to use it as a tool for collective good, the better off we all will be.

Understanding AI doesn't just mean understanding the math behind it or its technical functionality, but also means understanding the wide-reaching social impacts it has and will have in many aspects of life. Imagining the future of AI isn't a responsibility reserved for just MLOps engineers and researchers, this is something everyone has a stake in.

The future feels wide open, and I'm eager to keep learning – about LLMs, about infrastructure, and about the meeting point of creativity and automation. There's something energizing about being back in tech during such a transformative moment.

So even if my LLM API is so slow that it hurts, it's reminded me that understanding these systems isn't optional anymore. It's part of playing an active role in the world we're all building.
