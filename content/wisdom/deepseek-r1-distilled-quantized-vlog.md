---
title: "DeepSeek R1: Distilled & Quantized Models — Vlog"
date: 2025-12-24T10:00:00+05:30
draft: false
tags: ["ai","models","distillation","quantization","vlog"]
---

A concise vlog-style summary of "DeepSeek R1: Distilled & Quantized Models Explained" — cleaned up and without timestamps.

- Purpose of distilled models: smaller models are trained on outputs from DeepSeek R1 so they mimic its reasoning style while running on much smaller hardware.
- What distillation means: it produces entirely new, smaller “student” models (often based on Qwen or Llama) trained to reproduce the teacher’s behavior rather than compressing the original model.
- Tradeoffs of distillation: students gain efficiency and accessibility but lose some accuracy, nuance, and depth compared to the original R1.
- What quantization means: it reduces numeric precision of a model’s weights (e.g., 8-bit, 4-bit), shrinking file size while keeping the original model’s structure.
- Quantization vs distillation: quantized models compress R1 itself and often retain more of its behavior, but even heavy quantization leaves models large and hardware-demanding; distillation produces much smaller models that are easier to run but less faithful.
- Precision and inference: R1 is trained at high precision (FP32) and typically runs at BF16 or lower for inference; lower-bit quantization further reduces size but can degrade response quality.
- Example size reductions: numeric precision changes can dramatically reduce file sizes (e.g., large FP16 models → much smaller 4-bit files), yet those quantized files can still be too large for typical consumer hardware.
- Availability and variants: several distilled R1 variants (Qwen- and Llama-based, across parameter sizes like ~1.5B to 70B) have been open-sourced to broaden access.
- Practical choice: choose distillation when you need a small, efficient model for limited hardware; choose quantization if you prefer a more faithful, compressed version of the original model and have stronger hardware.

Further reading and context: Glasp notes and highlights for the video are available — https://glasp.co/reader?url=https://www.youtube.com/watch?v=AxAj16ZmanY

If you want, I can: extract differences between specific distilled variants, add a short summary card for the wisdom index, or update `content/wisdom/_index.md` to feature this vlog.
