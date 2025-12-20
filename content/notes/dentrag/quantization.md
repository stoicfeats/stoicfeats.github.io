---
title: "quantization"
date: 2025-12-20T10:00:00+05:30
draft: false
---

quantization is the "magic trick" that allows us to run a model that should require 6.4 gb of ram in just 2.0 gb.

to understand how it works in depth, we need to look at what's actually inside an llm file.

## 1. the core problem: precision vs. space

an llm is essentially a giant file of numbers called weights. these weights act like "volume knobs" for neurons.

- **default precision (fp16)**: most models are "born" using 16-bit floating point numbers.
- **the math**: a 16-bit number is essentially a very precise decimal (e.g., 0.82459132). it takes up 2 bytes of space.
- **the scale**: llama 3.2 3b has 3.2 billion of these numbers.
  $$3,200,000,000 \times 2 \text{ bytes} \approx \mathbf{6.4 \text{ gb}}$$

## 2. the solution: the "color palette" analogy

imagine you have a high-resolution photo with 16 million possible colors. to store that photo perfectly, you need a lot of data for every pixel.

quantization is like saying: "i only have enough space to store 16 colors. i'll pick the 16 most important colors and force every pixel in the photo to use the 'closest match' from my small palette."

- the photo still looks like a photo.
- the file size drops by 90%.
- you lose a little detail, but for most people, it's "good enough."

## 3. how the "magic" happens (step-by-step)

in technical terms, we are moving from 16-bit weights to 4-bit weights.

- **step a: grouping (blocking)**
  we don't just round every number individually. we take a "block" of weights (e.g., 32 numbers in a row).

- **step b: finding the range**
  we look at that block and find the highest number (e.g., 0.95) and the lowest (e.g., 0.10).

- **step c: creating the "buckets"**
  since we are using 4 bits, we have $2^4 = 16$ possible "buckets" (levels). we divide the space between 0.10 and 0.95 into 16 equal steps.

- **step d: mapping (the rounding)**
  we take a super-precise 16-bit number like 0.82459132 and ask: "which of my 16 buckets is this closest to?" maybe it's closest to bucket #13. we throw away the precise 0.82459132 and just store the number 13.

**storage savings:**
- storing 0.82459132 required 16 bits.
- storing the number 13 only requires 4 bits.
- **result**: the model is now 4x smaller.

## 4. what does q4_k_m mean?

in your project, the model uses q4_k_m. this is a specific "flavor" of quantization:

- **q4**: 4-bit quantization.
- **k**: uses "k-means" clustering (a smarter way to pick where the "buckets" should be so we lose less intelligence).
- **m**: "medium" size. it quantizes some "important" parts of the brain (the attention layers) with more care than the "less important" parts.

## 5. why doesn't it break the llm?

you might think rounding numbers so aggressively would make the llm output gibberish.

however, neural networks are surprisingly resilient. they don't need the exact "volume" of a knob to be 0.82459132; as long as the knob is "somewhere around 0.8," the signal still flows correctly.

**the "degradation" (perplexity):**
- a 16-bit model might be 100% "smart."
- a 4-bit model is about 98% as smart.

**the trade-off**: you lose 2% intelligence but gain the ability to run it on your laptop instead of a $20,000 server.
