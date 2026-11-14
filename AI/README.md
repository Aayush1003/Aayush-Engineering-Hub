# AI & Agent Learning Path

Welcome! This folder is a guided path for understanding **AI, generative AI, and AI agents** in plain language. It is written for someone who wants to understand what code is doing, not just copy a framework tutorial.

## Start here

1. **[Foundations and learning path](fundamentals/README.md)** — Python, math, machine learning, neural networks, and generative AI.
2. **[AI history](history/AI-HISTORY.md)** — how the field developed and why progress comes in waves.
3. **[Transformers explained](transformers/README.md)** — tokens, attention, and the model architecture behind many language models.
4. **[AI agents and workflows](agents/README.md)** — the practical guide to models, tools, memory, RAG, agent loops, safety, and examples from your own projects.
5. **[AI engineering](engineering/README.md)** — how to structure, test, evaluate, document, and operate an AI project.
6. **[Learning resources](resources/README.md)** — courses, papers, official documentation, and responsible-AI references.

## Recommended order

- Learn basic Python and the machine-learning ideas in **Foundations**.
- Read the **Transformer** guide to understand what a language model is doing when it generates text.
- Read **AI agents and workflows**. Trace the simple workflow diagram, then open the linked projects and follow their entry points.
- Read **AI engineering** before treating a demo as a dependable product: test outputs, protect data, measure cost, and document limitations.
- Build a tiny, testable project. Prefer one useful tool and a clear stopping rule over a complex multi-agent design.

## Key idea

A language model generates likely next tokens from its input; it does not automatically know facts, use tools, remember past sessions, or complete real-world work. An **AI application** adds the surrounding software. An **agent** is an application that uses a model to choose or sequence actions—often tools—while operating within state, permissions, and stop conditions. Use a fixed workflow when the steps are known; add agent decision-making only when it brings measurable value.

## Other parts of this repository

- [Interview Ready](../Interview-Ready/README.md) contains DSA and system-design practice, not AI-agent implementations.
- [The DSA and System Design Sheet](../Aayush-DSA-System-Design-Sheet.csv) is a study tracker.

## Learning checkpoint

After following the path, try to explain in your own words:

- What is the difference between a model, an AI application, an agent, and a workflow?
- What is one tool call, and how does its result get back to the model?
- How is RAG different from fine-tuning and from model memory?
- What could go wrong, and how would you test the system before trusting it?
