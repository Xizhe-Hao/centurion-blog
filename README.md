# Centurion — Project Blog

A written report, published as a webpage, on **Centurion: Distributed On-Device LLM Training** — a proof-of-concept system that trains a GPT-2-class language model across everyday consumer devices (phones, tablets, and laptops) collaborating over the internet.

**Live site:** https://xizhe-hao.github.io/centurion-blog/

## About the project

Training large language models normally happens in datacenters because of its computational footprint. Centurion asks whether pre-training can instead be spread across the idle compute already sitting in personal devices. With four heterogeneous workers (one iPhone, two iPads, and a Mac), Centurion trained **GPT-2-Medium (355M parameters)** over the internet at roughly **3,250 tokens per second** — a model none of those devices could hold on its own, trained by all of them together.

The system uses **pipeline parallelism**: the model is sliced into consecutive layer ranges, each device owns one range, activations flow forward and gradients flow back, and a coordinating server relays them between stages. Layer assignment is **capability-proportional** — stronger devices get more layers — which keeps the pipeline from being throttled by the slowest worker.

The blog covers the motivation, how the system works, results, findings, and next steps.

## Authors

Kurt Gu · Zach Hao · Tony Wu — University of Washington, CSE 599M

## Repository contents

This repo hosts the blog itself, a single self-contained page with no build step.

| File | Purpose |
|---|---|
| `index.html` | The full blog (HTML + inline CSS) |
| `implementation.png` | System architecture diagram |
| `pipeline.png` | Pipeline-timeline figure (forward / backward / bubbles) |

## Run locally

No build tooling required — just open the file:

```bash
git clone https://github.com/Xizhe-Hao/centurion-blog.git
cd centurion-blog
# open index.html in any browser
```

(The embedded demo video only plays over `http(s)`, not when opening the file directly, so view the live site to watch it.)

## Project code

The Centurion system itself (iOS/macOS app, MLX-Swift transformer, and the Python coordination server) lives in a separate repository:
https://github.com/therapyKG/Centurion
