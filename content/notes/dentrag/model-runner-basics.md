---
title: "model runner and daemon basics"
date: 2025-12-20T09:00:00+05:30
draft: false
---

## 1. what is a model runner?

a model runner is the "infrastructure" that makes an llm actually work. an llm on its own is just a giant file of math (weights). you can't "run" a file of math any more than you can "run" a pdf.

you need a program that can:

- read those weights.
- load them into your ram/gpu.
- perform the trillions of calculations per second needed to predict the next word.

**common model runners:**

- **ollama**: (what you're using) best for simplicity and running in the background.
- **lm studio**: great for people who want a gui (buttons and sliders) instead of code.
- **llama.cpp**: the industry-standard "engine" that almost everyone else is built on.
- **vllm**: a high-speed runner used for big servers.

**do they run locally?** yes, by definition! if it were running on someone else's server, we would call it an api provider (like openai or anthropic).

## 2. the daemon vs. the client

to understand this, let's use the "restaurant analogy."

### the daemon (the chef)
- **who it is**: the chef who stays in the kitchen.
- **what it does**: it does the "heavy lifting." it turns on the stove (allocates ram), prepares the ingredients (loads the model), and cooks the meal (performs the inference math).
- **why a "daemon"?** in tech, a "daemon" is just a program that runs in the background without a window. it sits there quietly, waiting for an order to arrive. when you see ollama in your menu bar, that's the daemon.

### the client (the waiter)
- **who it is**: the person who takes your request to the kitchen.
- **what it does**: it doesn't cook. it just says, "table 5 wants a summary of this dental paper." it sends a message (json) to the chef and waits for the answer.
- **your code**: your `client.py` is the waiter. it doesn't need 8gb of ram; it just needs to know how to "talk" to the chef.

## 3. why separate them? (the "why it matters" part)

you might ask: "why not just put the chef and the waiter in the same program?"

- **efficiency**: loading a 2gb model into ram takes time (5–10 seconds). if you had to load the model every single time you ran `python client.py`, it would be painfully slow. the daemon stays alive so the model stays "warm" and ready in ram.
- **multitasking**: one daemon can serve many clients. you could have your python script, a web browser, and a terminal all asking the same ollama daemon questions at once.
- **port 11434**: this is the "service window" where the waiter (client) talks to the chef (daemon). they use http (the same language as the internet) to communicate.

**in your project:**

- **the daemon**: the software you installed from ollama.com.
- **the client**: the `import ollama` library in your `client.py` file.
