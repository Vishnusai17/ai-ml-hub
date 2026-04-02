# 🤖 What Are AI Agents? — Foundations & Core Concepts

**Date:** 2026-04-02  
**Topic:** AI Agents — From Simple Reflex to Autonomous Reasoning  
**Level:** 🟢 Beginner → 🔴 Advanced (progressive)

---

## Starting from the Basics: What Is an Agent?

An **agent** is simply anything that **perceives** its environment and **acts** upon it.

```
Environment → [Sensors] → Agent → [Actuators] → Environment
```

That's it. A thermostat is an agent. A chess program is an agent. ChatGPT is an agent.

The difference lies in **how sophisticated** the agent's decision-making is.

---

## The Agent Model

Every agent follows this fundamental loop:

```
┌─────────────────────────────────────────┐
│              ENVIRONMENT                │
│                                         │
│   State → [Percept] → ┌──────────┐     │
│                        │  AGENT   │     │
│                        │          │     │
│   ← [Action] ←────── │  Decide  │     │
│                        └──────────┘     │
└─────────────────────────────────────────┘
```

| Component | What It Does | Example |
|---|---|---|
| **Percept** | What the agent observes | User message, API response, sensor data |
| **State** | Agent's internal understanding | Conversation history, memory, variables |
| **Decision** | Choosing what to do next | Select a tool, generate a response, plan |
| **Action** | What the agent does | Call an API, write code, send a message |

---

## Types of Agents (Classical AI)

These categories come from Russell & Norvig's *AI: A Modern Approach* and build from simple to complex:

### 1. Simple Reflex Agent

Acts only on the **current percept**, ignoring history.

```
IF email contains "urgent" → flag as high priority
IF temperature > 80°F → turn on AC
```

- ✅ Fast, simple
- ❌ No memory, no planning, brittle

### 2. Model-Based Reflex Agent

Maintains an **internal model** of the world to handle partially observable environments.

```
Internal State: "Door was locked 5 minutes ago"
Percept: "No sound from door"
Decision: "Door is still locked" → don't check again
```

- ✅ Can handle incomplete information
- ❌ Still rule-based, no goal reasoning

### 3. Goal-Based Agent

Has explicit **goals** and chooses actions that move toward them.

```
Goal: "Get from home to office"
Current State: "At home"
Options: Drive, bus, walk, bike
Decision: Evaluate each option → choose drive (fastest)
```

- ✅ Can reason about the future
- ❌ No preference between equally goal-achieving actions

### 4. Utility-Based Agent

Assigns **utility scores** to outcomes and maximizes expected utility.

```
Goal: "Get to office"
Drive: utility = 0.8 (fast but stressful)
Bike: utility = 0.9 (exercise + fresh air)
Decision: Bike (higher utility)
```

- ✅ Handles trade-offs, optimizes for "best" not just "good enough"
- ❌ Requires defining a utility function

### 5. Learning Agent

Improves its behavior **over time** through experience.

```
Components:
├── Performance Element — chooses actions
├── Critic — evaluates how well the agent did
├── Learning Element — modifies the agent based on feedback
└── Problem Generator — suggests exploratory actions
```

- ✅ Adapts and improves
- ✅ This is the foundation of modern AI agents

---

## From Classical Agents to LLM-Powered Agents

Classical agents were limited by hand-coded rules. **LLMs changed everything** by providing:

| Capability | What LLMs Bring |
|---|---|
| **Natural language understanding** | Parse any user request |
| **Reasoning** | Break down complex problems step-by-step |
| **Code generation** | Write and execute code on the fly |
| **Knowledge** | Broad world knowledge from pre-training |
| **Few-shot learning** | Adapt to new tasks from just a few examples |

> **The key insight**: An LLM can serve as the "brain" of an agent — replacing hand-coded rules with general-purpose reasoning.

---

## What Is Agentic AI?

**Agentic AI** refers to AI systems that can **autonomously plan, reason, and take actions** to accomplish goals — going beyond simple question-answering.

### The Spectrum: Chatbot → Agent

```
Level 0: Static Responses
  "Here's the answer to your question"

Level 1: Tool Use
  "Let me search the web for that" → [uses search tool] → "Here's what I found"

Level 2: Multi-Step Reasoning
  "To solve this, I need to: (1) search, (2) analyze, (3) synthesize" → executes plan

Level 3: Autonomous Agent
  "I'll figure out the approach, use the right tools, handle errors, 
   and iterate until the task is done"
```

| Feature | Chatbot (Level 0) | Agentic AI (Level 3) |
|---|---|---|
| **Interaction** | Single turn Q&A | Multi-step, autonomous |
| **Tools** | None | Web search, code execution, APIs |
| **Planning** | None | Breaks tasks into subtasks |
| **Memory** | Conversation only | Long-term memory + retrieval |
| **Error handling** | Fails silently | Retries, adapts, self-corrects |
| **Goal tracking** | Per-message | Per-task (across many steps) |

---

## Core Components of an AI Agent

Modern AI agents are built from these key components:

### 1. The "Brain" — LLM as Reasoning Engine

The LLM acts as the central decision-maker:

```
User Task → LLM reasons about what to do → decides on actions → executes → evaluates
```

Popular backbone models: GPT-4, Claude, Gemini, LLaMA, Mistral

### 2. Planning & Decomposition

Agents break complex tasks into manageable steps:

```
Task: "Write a research report on climate change in 2025"

Plan:
├── Step 1: Search for recent climate data and reports
├── Step 2: Identify key findings and statistics
├── Step 3: Outline the report structure
├── Step 4: Write each section with citations
├── Step 5: Review and refine the final report
└── Step 6: Format and deliver
```

#### Planning Strategies

| Strategy | How It Works |
|---|---|
| **Chain-of-Thought (CoT)** | "Let me think step by step..." |
| **ReAct** | Reason → Act → Observe → Repeat |
| **Plan-and-Execute** | Create full plan first, then execute steps |
| **Tree of Thoughts** | Explore multiple reasoning paths, pick the best |
| **Reflexion** | Reflect on failures and retry with improved approach |

### 3. Tool Use

Agents extend their capabilities by using external tools:

| Tool Category | Examples |
|---|---|
| **Search** | Web search, knowledge base lookup |
| **Code execution** | Python interpreter, shell commands |
| **APIs** | Weather, stocks, databases, SaaS platforms |
| **File operations** | Read, write, edit files |
| **Communication** | Send emails, Slack messages |
| **Browser** | Navigate websites, fill forms, scrape data |

#### How Tool Use Works

```
User: "What's the weather in NYC?"

Agent Reasoning:
  Thought: I need current weather data. I can't know this from training.
  Action: call weather_api(location="New York City")
  Observation: {"temp": 72, "condition": "Partly Cloudy"}
  Answer: "It's 72°F and partly cloudy in NYC right now."
```

### 4. Memory

Agents need memory to maintain context across interactions:

| Memory Type | What It Stores | How It Works |
|---|---|---|
| **Short-term (working)** | Current conversation | Context window of the LLM |
| **Long-term (episodic)** | Past interactions | Vector database retrieval (RAG) |
| **Semantic** | Facts and knowledge | Knowledge graph or embedding store |
| **Procedural** | How to do things | Saved tools, workflows, skills |

### 5. Self-Reflection & Error Recovery

Good agents evaluate their own outputs and recover from mistakes:

```
Agent generates code → runs it → ERROR
  ↓
Agent reads the error message
  ↓
Agent reasons about what went wrong
  ↓
Agent fixes the code and retries
  ↓
SUCCESS ✓
```

---

## The ReAct Framework

**ReAct (Reasoning + Acting)** is one of the most influential frameworks for agentic AI. It interleaves thinking and doing:

```
Question: "What is the age difference between the founders of Google?"

Thought 1: I need to find the founders of Google and their birth dates.
Action 1: Search("founders of Google")
Observation 1: Larry Page and Sergey Brin founded Google in 1998.

Thought 2: Now I need their birth dates.
Action 2: Search("Larry Page birth date")
Observation 2: Larry Page was born on March 26, 1973.

Action 3: Search("Sergey Brin birth date")  
Observation 3: Sergey Brin was born on August 21, 1973.

Thought 3: Larry Page (March 1973) and Sergey Brin (August 1973). 
            The difference is about 5 months.
Answer: The founders of Google, Larry Page and Sergey Brin, 
        are about 5 months apart in age.
```

### Why ReAct Works

| Advantage | Explanation |
|---|---|
| **Grounded reasoning** | Actions provide real data to reason about |
| **Traceable** | You can follow the agent's thought process |
| **Flexible** | Works with any set of tools |
| **Self-correcting** | Can observe failures and adjust |

---

## Popular Agent Frameworks

| Framework | Built By | Key Features |
|---|---|---|
| **LangChain / LangGraph** | LangChain Inc. | Chain-based agents, tool integration, graph workflows |
| **AutoGPT** | Community | Fully autonomous goal-driven agent |
| **CrewAI** | CrewAI | Multi-agent collaboration with roles |
| **OpenAI Assistants** | OpenAI | Built-in tools (code interpreter, retrieval) |
| **Semantic Kernel** | Microsoft | Enterprise agent framework for .NET/Python |
| **Haystack** | deepset | Pipeline-based agents for NLP tasks |
| **Smolagents** | HuggingFace | Lightweight, code-first agents |

---

## Multi-Agent Systems

Instead of one agent doing everything, **multiple specialized agents** can collaborate:

```
┌──────────────────────────────────────────────────┐
│                 ORCHESTRATOR AGENT                │
│          (Coordinates and delegates tasks)        │
└──────────┬──────────┬──────────┬─────────────────┘
           │          │          │
     ┌─────▼───┐ ┌────▼────┐ ┌──▼──────────┐
     │Research │ │ Coder   │ │  Reviewer   │
     │ Agent   │ │ Agent   │ │  Agent      │
     └─────────┘ └─────────┘ └─────────────┘
```

### Benefits of Multi-Agent Systems

| Benefit | Explanation |
|---|---|
| **Specialization** | Each agent focuses on what it does best |
| **Parallelism** | Agents can work simultaneously |
| **Modularity** | Easy to add, remove, or swap agents |
| **Debate & verification** | Agents can review each other's work |

### Example: Software Development Team

| Agent | Role |
|---|---|
| **Product Manager** | Interprets requirements, creates specs |
| **Architect** | Designs the system structure |
| **Developer** | Writes the code |
| **Tester** | Writes and runs tests |
| **Reviewer** | Reviews code for quality and bugs |

---

## Challenges in Agentic AI

| Challenge | Description |
|---|---|
| **Hallucination** | Agent confidently takes wrong actions based on fabricated info |
| **Compounding errors** | Small mistakes early in a plan cascade into larger failures |
| **Safety & control** | Autonomous agents need guardrails to prevent harmful actions |
| **Cost** | Each LLM call costs money; agents make many calls |
| **Latency** | Multi-step reasoning is slower than single-shot responses |
| **Evaluation** | Hard to benchmark open-ended agentic tasks |
| **Context limits** | Long plans can exceed the LLM's context window |
| **Reliability** | Non-deterministic outputs make agents unpredictable |

---

## The Future of Agentic AI

| Trend | What's Coming |
|---|---|
| **Computer use agents** | Agents that can use any software via screen + mouse/keyboard |
| **Coding agents** | Autonomous software engineers (Devin, Copilot Workspace) |
| **Personal agents** | Persistent assistants that know your preferences and history |
| **Enterprise agents** | Agents integrated into business workflows |
| **Agent-to-agent protocols** | Standardized communication between agents (MCP, A2A) |
| **Smaller, faster models** | Efficient models purpose-built for agentic reasoning |
| **Self-improving agents** | Agents that learn from their successes and failures |

---

## Key Terminology Glossary

| Term | Definition |
|---|---|
| **Agent** | A system that perceives its environment and takes actions to achieve goals |
| **Agentic AI** | AI systems capable of autonomous planning, reasoning, and action |
| **Tool use** | An agent's ability to call external tools (APIs, search, code execution) |
| **ReAct** | A framework interleaving reasoning and acting |
| **Chain-of-Thought** | Prompting technique where the LLM reasons step-by-step |
| **Multi-agent system** | Multiple agents collaborating to solve a task |
| **Orchestrator** | An agent that coordinates and delegates to other agents |
| **Guardrails** | Safety constraints that limit what an agent can do |
| **Function calling** | LLM capability to output structured tool invocations |
| **MCP** | Model Context Protocol — standard for connecting LLMs to tools |

---

## 🔗 Resources
- [Lilian Weng: LLM-Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/)
- [ReAct Paper (Yao et al., 2022)](https://arxiv.org/abs/2210.03629)
- [A Survey on LLM-based Agents (2024)](https://arxiv.org/abs/2308.11432)
- [Andrew Ng: What's Next for AI Agentic Workflows](https://www.youtube.com/watch?v=sal78ACtGTc)
- [LangChain Documentation](https://python.langchain.com/docs/)
- [CrewAI Documentation](https://docs.crewai.com/)
- [AI: A Modern Approach (Russell & Norvig) — Chapter 2](http://aima.cs.berkeley.edu/)

---

*AI Agents represent the next frontier — moving from AI that answers questions to AI that takes action. The journey from simple reflex to autonomous reasoning mirrors the evolution of intelligence itself. 🚀*
