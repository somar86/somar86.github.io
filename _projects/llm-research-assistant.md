---
title: "LLM Research Assistant for 80,000+ Technical Reports"
excerpt: "An internal research assistant built on open-weight LLMs and custom-trained on more than 80,000 oilfield-services research reports. Answers cite their sources, and multi-agent cross-checking catches and corrects hallucinations."
order: 4
toc: true
tags: [LLM, RAG, multi-agent systems, AI]
---

**Role:** Designer and developer · **Organization:** SLB

## Overview

Decades of engineering knowledge live in technical reports. I built an **internal research assistant** on **open-weight large language models**, served with **Ollama** and custom-trained on a repository of **more than 80,000 oilfield-services research reports**. Anyone in the organization can ask a technical question in plain language and get an answer that **cites the reports it came from**. Before an answer reaches the user, **multiple agents are pitted against each other** to find and correct hallucinations.

## The problem

- **Knowledge is hard to reach.** With tens of thousands of reports, finding an answer usually means knowing which report to open or whom to ask.
- **General-purpose chatbots are not enough.** They don't know a company's internal work, and they can state wrong answers with confidence.
- **Engineers need sources.** An answer an engineer cannot trace back to a report is an answer they cannot act on.
- **The reports are proprietary**, so the system has to run on models the organization controls.

## Approach

- **Open-weight models, self-hosted with Ollama**, so proprietary reports stay in-house
- **Custom training** on the report repository, so the models handle the domain's vocabulary and content
- **Advanced retrieval-augmented generation (RAG):** relevant passages are retrieved from the repository, and every answer cites the reports it draws on
- **Multi-agent hallucination correction:** several agents are launched and pitted against each other to challenge the draft answer, and claims they find unsupported are corrected before the answer is returned
- **One chat interface for the whole organization**, with no need to know which report or expert holds the answer

## Impact

- Anyone in the organization can query a technical record of more than 80,000 reports in plain language
- Answers are **traceable**: each one points to its source reports, so users can check them before acting
- Multi-agent cross-checking reduces confident but wrong answers, a key barrier to trusting LLMs in engineering work
- Demonstrates a practical pattern for LLM assistants built on self-hosted open models when the data must stay private
