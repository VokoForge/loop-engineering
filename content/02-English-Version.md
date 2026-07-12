# English Version

## Preface

### Preface

If you go to bed and tell Claude Code "fix this issue for me," then wake up to find the PR already submitted — congratulations. You're already doing Loop Engineering. You just happen to be the loop.

You're the one who initiates the request. You're the one who waits for results. You're the one who wakes up in the morning to check the code quality. You're the one who decides whether to merge or send it back. All night long, you serve as the slowest, least reliable, but also the last line of defense in the cycle.

Now imagine: you no longer need to be the loop.

Imagine a system that can read the issue on its own, plan its approach, write code, run tests, discover problems, fix them, submit the PR, wait for CI to pass, and revise based on review feedback — all by itself. And you only need to press the "merge" button at the end. Or sometimes, you don't even need to press that button.

This isn't science fiction. This is what's happening in June 2026.

## A Quiet Revolution

On June 7, 2026, Addy Osmani, Engineering Lead at Google Chrome, formally named a concept in a blog post — **Loop Engineering**. He wrote: "We're moving from prompt engineering to loop engineering — designing feedback loops where agents autonomously get work done."

Around the same time, Peter Steinberger, Director of Google Cloud AI, posted on X: "You should not manually prompt coding agents anymore. You should design loops that prompt your agents."

Boris Cherny, Head of Claude Code, put it even more bluntly: "I don't prompt Claude anymore. I have loops running that prompt Claude and figure out what to do. My job is writing loops."

Jensen Huang's words at an internal meeting were even more striking: "Nobody writes prompts anymore. The core work in the new era is writing and managing loops."

Overnight, "Loop Engineering" became the hottest term in tech circles. But this isn't some concept that appeared out of nowhere — it's the inevitable result of three years of evolution in AI coding tools. From Copilot's code completion, to Cursor's chat-based programming, to Claude Code's agent mode, to today's loop engineering — we are undergoing a fundamental paradigm shift in software engineering.

## Why Now?

Why did Loop Engineering explode in 2026? Three conditions matured simultaneously:

**First, model capabilities are finally strong enough.** Today's AI agents can independently complete the entire flow from requirement understanding to code submission, not just complete a few lines of code. They can read documentation, use tools, debug, and self-correct.

**Second, the toolchain is finally mature enough.** The MCP protocol lets agents connect to any tool. Worktrees make parallel work possible. Automations make triggers ubiquitous. The infrastructure is ready.

**Third, the demand is finally urgent enough.** When individual engineers achieve 10x productivity with AI, the next bottleneck is no longer "writing code too slowly" — it's "humans watching agents work too slowly." The leverage of efficiency has shifted from the code level to the process level.

## What This Book Offers

This is not a popular science book about concepts. There are already too many articles telling you "what Loop Engineering is." You don't need hundreds of pages to understand a definition.

What this book does is take you from "knowing" to "doing."

You will learn:

- **Frameworks**: How six core modules combine into a complete Loop system
- **Methodology**: A five-step process for designing a loop from scratch
- **Pitfall guide**: Six failure modes and three deep risks, and how to avoid them
- **Real cases**: From Ralph Loop to Minglue Technology, from Amplitude to ByteDance
- **The M-LOOP Framework**: 1 hub + 4 loops + 7 gates — a battle-tested methodology refined from real projects

After reading this book, you won't just "know about Loop Engineering." You'll be able to **design** loops, **implement** loops, and **manage** loops.

## How to Read This Book

This book is divided into five parts. You can read sequentially, or jump around based on your role:

- **If you're a frontline engineer**: Focus on Part II (Core Architecture) and Part III (Design & Practice) to start designing your first loop right away
- **If you're a tech manager**: Focus on Part IV (Frameworks & Ecosystem) and Part V (Future & Organization) to think about implementation in your team
- **If you're an AI practitioner**: Focus on Part I (Paradigm Revolution) and Chapter 17 (M-LOOP Framework) to understand the underlying logic and differentiated approaches

But I recommend at least reading the preface and Chapter 1. Because understanding "why" is more important than knowing "how."

Ready? Let's begin this paradigm journey.

---

---

## Part I: The Paradigm Revolution

### Untitled

# Part I: The Paradigm Revolution

> *Every paradigm shift is not a linear upgrade of technology, but a fundamental restructuring of how work gets done. Understanding which stage you're in matters more than mastering which tool.*

---

---

# Chapter 1: The Four Paradigm Shifts of AI Programming

### From Hand-Written Code to Loop Engineering

At 2 AM, Xiao Zhang is woken up by an alert. A service is OOM-ing, the logs show a null pointer exception. He rubs his eyes, opens his laptop, locates the code, writes a fix, manually tests it, submits a PR, waits for CI, merges, deploys. By the time he's done, dawn is approaching.

That's the story from 2020.

The 2023 version goes like this: Xiao Zhang opens Copilot Chat, pastes the error message. Copilot tells him the likely cause and generates the fix. Xiao Zhang reviews it and submits the PR. The whole process takes 20 minutes.

The 2025 version: Xiao Zhang sends the issue link to Claude Code and says "fix this." Claude Code reads the code, finds the problem, writes the fix, runs tests, submits the PR. Xiao Zhang just presses "merge." 10 minutes.

What about the 2026 version? The alert triggers an automated workflow. A loop automatically creates a fix branch, calls an agent to analyze the problem, writes code, runs tests, submits a PR, waits for review. Xiao Zhang wakes up in the morning and gets a notification on his phone: "3 alerts auto-fixed, merged, awaiting your final confirmation."

That's the essence of four paradigm shifts.

### 1.1 The First Shift: Prompt Engineering — Learning to Talk to AI

Back in late 2022, ChatGPT exploded onto the scene. Engineers quickly discovered that the quality of AI-written code depended heavily on how you asked the question.

So "Prompt Engineering" became the hot new field. "Zero-shot vs Few-shot," "Chain of Thought (CoT)," "role prompting" — overnight, everyone was studying how to write better prompts. GitHub Copilot also rapidly普及 in 2023, and code completion went from "nice to have" to "can't live without."

The core logic of this stage: **Humans are the drivers, AI is the assistant.** Humans lead the entire process, AI provides acceleration at specific nodes — completing code, explaining errors, generating test cases.

**Key characteristics:**

- Humans initiate every interaction
- AI outputs once, humans judge correctness
- Value comes from "typing speed improvement"
- Representative tools: ChatGPT, GitHub Copilot

But soon, people hit a bottleneck: you still have to watch every step yourself. You have to review the code AI writes, debug when it doesn't work, feed it context when it runs out. You go from "person who writes code" to "person who reviews code," but the workload doesn't decrease much.

### 1.2 The Second Shift: Context Engineering — Feeding AI the Right Context

By 2024, everyone realized a problem: no matter how good your prompt is, if AI doesn't know what your project looks like, it still can't write usable code.

So the focus shifted from "how to ask" to "what to give." Context Engineering emerged — the core is how to feed the right code, documentation, and configuration to AI at the right time.

RAG (Retrieval-Augmented Generation) blew up. Vector databases blew up. Various "codebase indexing" tools blew up. Engineers started building their own project knowledge bases so AI could retrieve relevant code and docs whenever needed.

The core logic of this stage: **Humans are still drivers, but AI now has navigation.** AI no longer starts from zero every time. It can "see" your project structure, and output quality improves dramatically.

**Key characteristics:**

- Quality of context determines quality of output
- Retrieval systems become core infrastructure
- Value comes from "reducing the probability of AI mistakes"
- Representative tools: various RAG frameworks, code indexing tools

But Context Engineering also has a clear ceiling: you still have to drive yourself. AI knows the route, but the steering wheel is still in your hands. Every decision, every direction adjustment, is still made by a human.

### 1.3 The Third Shift: Harness Engineering — Turning AI into Agents

In 2025, "Agentic AI" became the keyword. Claude Code burst onto the scene — it didn't just chat. It could read files on its own, write code on its own, run commands on its own, debug on its own. You give it a task, and it breaks down the steps and completes them one by one.

Andrej Karpathy called this stage "Vibe Coding" — you don't worry about the specific implementation, you just describe the vibe you want, and AI takes care of it.

This stage also has another name: Harness Engineering. The core isn't how to prompt, but how to "harness" agents — giving them the right tools, the right boundaries, the right feedback mechanisms.

The core logic of this stage: **Humans become supervisors, AI becomes the worker.** You give tasks, AI does the work, you check the results.

**Key characteristics:**

- AI can autonomously execute multi-step operations
- Tool-use capability becomes the core differentiator
- Value upgrades from "accelerating typing" to "accelerating task completion"
- Representative tools: Claude Code, Cursor Composer, Devin

But the third shift still has a bottleneck: **humans are still the bottleneck.** You have to give the tasks, you have to check the results, you have to decide what's next. AI is already working faster than humans can review. An agent can finish writing code in an hour that might take you half a day to review.

And you only have one pair of hands, one pair of eyes. You can only watch one agent at a time. What if there are ten tasks? You either queue them up or spread yourself too thin.

### 1.4 The Fourth Shift: Loop Engineering — Letting the System Spin on Its Own

In 2026, the answer emerged: since agents can work on their own, why can't the system manage agents on its own?

The core insight of Loop Engineering is this: **The next bottleneck in software engineering is not AI capability, but human attention.** When AI can complete tasks independently, the leverage of efficiency shifts from "making AI smarter" to "making processes more automatic."

What Loop Engineering does is free humans from the loop. Instead of humans prompting agents, you design a loop system where the system prompts agents on its own, checks results on its own, decides what's next on its own, handles failures on its own — and humans only intervene at nodes where human judgment is truly needed.

The core logic of this stage: **Humans go from supervisors to system designers, and the system runs on its own.**

**Key characteristics:**

- Systems autonomously trigger and manage tasks
- Feedback loops are first-class citizens
- Value upgrades from "accelerating individual tasks" to "accelerating entire workflows"
- Representative practices: Ralph Loop, automated CI/CD pipelines, self-healing systems

### 1.5 The Essence of the Shift: From "Human-in-the-Loop" to "Human-Outside-the-Loop"

Four shifts, essentially one process: **humans gradually withdrawing from the loop.**

| Paradigm | Human Role | AI Role | Value Lever |
|-|-|-|-|
| Prompt Engineering | Driver | Co-pilot | Typing speed |
| Context Engineering | Driver + Navigator | Co-pilot with navigation | Output quality |
| Harness/Vibe Coding | Supervisor | Worker | Task completion speed |
| **Loop Engineering** | **System Designer** | **Autonomous Worker** | **Process throughput** |

This isn't to say humans are no longer important. Quite the opposite — the human role rises from "execution layer" to "design layer." You no longer need to write code yourself, or even review code yourself — but you need to design a system that consistently produces high-quality code.

That's exactly what this book is about.

> **Key Insight**: Each paradigm shift doesn't "replace" the previous one — it "stacks" on top. Prompt Engineering is still important in the Loop Engineering era — but it's no longer the bottleneck, and no longer where the highest value lies.

---

---

### Chapter 2: What Exactly is Loop Engineering?

### Definition, Core Elements, and How It Differs from Related Concepts

Let's start with a simple question: If I write a shell script that runs Claude Code every hour to check the codebase for new issues and auto-fix them, is that Loop Engineering?

The answer is: yes, but only in its most primitive form.

Loop Engineering isn't a single tool, and it isn't a single technology. It's a **design paradigm** — designing work loop systems driven by AI agents that can operate autonomously.

### 2.1 A Definition

We can define Loop Engineering as follows:

> **Loop Engineering is the engineering discipline of designing, building, and maintaining autonomous work loops driven by AI agents. It's not concerned with completing individual tasks, but with the continuous operation of the entire system — letting tasks flow in automatically, be assigned automatically, executed automatically, verified automatically, and delivered automatically, with humans only intervening at necessary nodes.**

There are several keywords in this definition:

- **Autonomous work loops**: Not something you push to move, but a system that can sustain operation on its own
- **Driven by AI agents**: The execution主体 is AI agents, not humans
- **Designing, building, and maintaining**: This is an engineering discipline, not just inspiration and tricks
- **Humans only intervene at necessary nodes**: Humans move from "in the loop" to "on the loop"

### 2.2 Core Elements: What Does a Loop At Least Need?

Not all "automation + AI" is Loop Engineering. A true loop system needs at least the following core elements:

#### Element One: Trigger Mechanism

A loop isn't started manually — it has its own trigger conditions. It could be time-based (runs every hour), event-based (starts when there's a new issue), or condition-based (starts a fix流程 when tests fail).

> Without a trigger mechanism, it's not a loop — it's just a script you call manually.

#### Element Two: Execution Agent

The execution主体 of a loop is an AI agent, not predefined rules. If every step is hard-coded if-else, that's a traditional automation script, not a loop. The core of a loop is — the agent makes decisions within the cycle.

> Without agent decision-making, it's not a loop — it's just an automation pipeline.

#### Element Three: Feedback Loop

The key to a loop isn't "executing once" — it's the closed loop of "execute → check → adjust → re-execute." After the agent outputs results, the system can verify correctness, and if there are problems, feed them back to the agent for further correction.

> Without a feedback closed loop, it's not a loop — it's just a one-time task.

#### Element Four: Exit Condition

A good loop knows when to stop. It could be task completion, reaching maximum retry count, or encountering an unsolvable problem that needs escalation to a human.

> Without an exit condition, it's not a loop — it's an infinite loop.

These four elements — trigger, agent, feedback, exit — constitute the most basic loop. Missing any one, it's not Loop Engineering in the full sense.

### 2.3 Loop Engineering vs Related Concepts

"Isn't this just XX with a new name?" — that's many people's reaction when they first hear about Loop Engineering. Let's clarify a few easily confused concepts.

#### vs Automation

Traditional automation is **rule-based**: if A happens, do B. Every step is preset.
Loop Engineering is **agent-based**: if A happens, let the agent figure out how to solve it. How the agent solves it, how many steps, how it adjusts when it encounters problems — the agent decides all of this within the loop.

> Traditional automation is like a clock — every gear's movement is designed.
> Loop Engineering is like an ecosystem — you design the environment and rules, and organisms adapt and evolve on their own.

#### vs CI/CD

CI/CD (Continuous Integration / Continuous Delivery) is automation **for the code delivery process**. Its core is "automatically test and deploy after code submission."
Loop Engineering's scope is much larger — it can cover the entire software lifecycle from requirement discovery to code repair to operations monitoring. CI/CD can be one环节 in a loop, but a loop is far more than CI/CD.

#### vs Agentic AI

Agentic AI is **a form of AI capability** — referring to AI that can autonomously plan and execute multi-step tasks.
Loop Engineering is **a paradigm of system design** — it uses agents as building blocks, but focuses more on the architecture of the entire system: how multiple agents collaborate, how tasks are assigned, how failures are handled, how quality is ensured.

> Agentic AI is the engine. Loop Engineering is the entire vehicle design. The engine is important, but whether a car drives well is about far more than just the engine.

#### vs Prompt Engineering

Prompt Engineering focuses on **the quality of a single interaction** — how to write prompts to get better AI output.
Loop Engineering focuses on **the throughput and reliability of the entire process** — how to design systems where multiple interactions form closed loops that continuously produce value.

Prompt Engineering is the foundation of Loop Engineering — just as assembly language is the foundation of operating systems. But you wouldn't say you understand operating system design just because you know assembly.

#### vs Traditional Software Engineering

This is the most controversial comparison. Critics say: "Isn't Loop Engineering just software engineering? Just replacing humans with AI."

In a way, they're right. Loop Engineering does inherit many ideas from software engineering — modularity, abstraction, testing, fault tolerance, monitoring. But it has several fundamental differences:

1. **Different execution主体**: Traditional software engineering's execution主体 is humans, so the core is "how to make humans collaborate efficiently." Loop Engineering's execution主体 is AI agents, and the core is "how to make agents operate reliably."
2. **Different uncertainty**: Human behavior is uncertain, but we have ways to manage it (hiring, training, KPIs). AI uncertainty is of a different kind — it can hallucinate, misinterpret, or repeatedly make the same mistake. Management methods are completely different.
3. **Different cost structures**: Human cost is fixed (monthly salary). AI cost is usage-based (tokens). This leads to completely different design decisions — you try to minimize repetitive work for humans, but you might instead have AI verify multiple times, because the extra token cost is far less than the cost of bugs.
4. **Different scaling methods**: Adding a person requires hiring, training, onboarding — a cycle of months. Adding an agent just requires configuration — a cycle of minutes. This means the scalability assumptions of system design have completely changed.

So Loop Engineering isn't "software engineering with a new name" — it's **a new branch of software engineering in the age of AI agents**. Just as web development isn't desktop software development with a new name — they share many foundational principles, but the problem spaces and design constraints they face are completely different.

### 2.4 Why Is the Word "Loop" So Important?

Why "Loop" and not "Flow," "Pipeline," or "Workflow"?

Because the concept of "loop" captures the essence of how AI agents work:

- **Trial-and-error loop**: AI doesn't get it right the first time — it needs try → check → correct → retry
- **Feedback loop**: Each step's output is the next step's input — the system evolves through feedback
- **Continuous loop**: Not done once and finished — it runs continuously and improves continuously

"Flow" and "Pipeline" suggest a linear, one-time, A-to-B process. But AI agents don't work linearly — they work iteratively, cyclically, advancing through trial and error.

The word "Loop" accurately captures this essence of iteration, feedback, and continuous operation.

> **Core Idea**: The essence of Loop Engineering isn't "automating with AI" — it's "designing a system that self-improves through feedback." Automation is just the means; self-evolution is the goal.

---

---

### Chapter 3: Loop vs Chain vs Vibe Coding

### Essential Differences and Use Cases of Three Paradigms

Imagine three engineers in front of you:

**Engineer A** likes writing long prompts, breaking tasks into tiny steps, guiding AI output step by step. He says: "Only when I think through every step can AI stay on track."

**Engineer B** likes throwing requirements directly at AI, then going back and forth in conversation, tweaking and adjusting. He says: "I don't know what the final version looks like either. Let's build it first and see, then fix what's wrong."

**Engineer C** wrote an automated system that grabs tasks from the issue list every day, automatically assigns them to AI agents, automatically checks results, automatically submits PRs. He only spends half an hour each day looking at what got sent back. He says: "My job is designing systems, not doing tasks."

These three people represent three paradigms: Chain, Vibe Coding, and Loop.

### 3.1 Essential Differences Between the Three Paradigms

Let's compare the three paradigms across several dimensions:

#### Control Method: Human-Driven vs Collaborative vs System-Driven

**Chain paradigm** is human-driven. The human is the commander-in-chief — every step, every next move, is decided by a human. AI is just an execution tool.

**Vibe Coding** is collaboration-driven. Human and AI explore together. The human has a general direction, AI provides possibilities, and both sides gradually approach the final result through interaction.

**Loop paradigm** is system-driven. Humans design the system rules and loop logic, then the system runs on its own, deciding each step by itself. The human goes from "operator" to "designer."

#### Output Method: Deterministic vs Exploratory vs Reliable

**Chain paradigm** pursues determinism. The more finely you break down the steps, the more controllable the AI output. It's good for scenarios where "I know how to do it, I just don't want to type it myself."

**Vibe Coding** pursues exploration. You don't know what the final answer looks like. You need to trial-and-error and discover together with AI. It's good for scenarios where "I have an idea, but the details aren't clear."

**Loop paradigm** pursues reliability. What matters isn't how well a single task is done, but the overall success rate and quality level across a hundred, a thousand tasks. It's good for scenarios where "tasks keep coming, I need the system to produce reliably."

#### Human Role: Conductor vs Partner vs Designer

In **Chain paradigm**, the human is the conductor — you wave the baton, and AI plays to your rhythm.

In **Vibe Coding**, the human is the partner — you and AI jam together, inspire each other, co-create.

In **Loop paradigm**, the human is the designer — you design the instruments, the concert hall, the performance流程, and then the performance happens on its own.

### 3.2 One Table to Understand All Three Paradigms

| Dimension | Chain | Vibe Coding | Loop |
|-|-|-|-|
| Driving force | Human-driven | Human-AI collaboration | System-driven |
| Core goal | Deterministic output | Exploratory discovery | Reliable production |
| Human role | Commander | Collaborator | System designer |
| Interaction pattern | Human→AI→Human→AI... | Human↔AI bidirectional flow | System self-circulates, human intervenes occasionally |
| Typical scenario | Coding tasks with known solutions | New product, new feature exploration | Repetitive, continuous task flows |
| Value lever | Single task efficiency | Creative and exploratory efficiency | System throughput |
| Failure mode | If human overlooks something, everything goes wrong | Direction drifts, time wasted | Systemic failure, batch errors |
| Representative tools | ChatGPT + manual process | Cursor, Claude Code chat mode | Ralph Loop, automated agent systems |

### 3.3 Use Cases: When to Use What?

These three paradigms aren't hierarchical — they're just for different scenarios.

#### When to Use Chain?

When you **know exactly what to do** and just don't want to do it yourself. For example:

- "Convert this Python code to Go"
- "Add unit tests to this function covering all edge cases"
- "Implement the page according to this design mockup"

The advantage of Chain paradigm is controllability — as long as your prompt is good, the results won't drift far. The disadvantage is mental effort — you have to think through all the steps yourself.

#### When to Use Vibe Coding?

When you **only have a general direction** and need to explore with AI. For example:

- "I want to build a tool that automatically organizes meeting notes. Help me think about the technical approach"
- "This page doesn't feel good enough. What suggestions do you have?"
- "I've been debugging this bug for hours with no leads. Help me analyze possible causes"

The advantage of Vibe Coding is flexibility — you and AI can explore freely, often discovering solutions you wouldn't have thought of yourself. The disadvantage is it can easily diverge — chatting for half an hour and still going in circles on the first problem.

#### When to Use Loop?

When you have **a continuous stream of tasks** and need the system to produce reliably. For example:

- "The codebase gets a dozen new issues every day — auto-classify and auto-tag them"
- "After every PR submission, automatically do code review"
- "After an online alert triggers, auto-diagnose and auto-fix"

The advantage of Loop paradigm is scalability — adding tasks doesn't require adding people, the system can run 24/7. The disadvantage is high upfront cost — you need to spend time designing and debugging the loop.

### 3.4 Not Either-Or, But Combined Use

In reality, these three paradigms are often used in combination.

Take a product feature development as an example:

1. **Requirements exploration phase**: Use Vibe Coding to discuss feature design and technical approach with AI
2. **Concrete coding phase**: Use Chain to break clear tasks into steps and guide AI implementation step by step
3. **Testing and verification phase**: Use Loop to automatically run various test cases, check code quality, and fix lint errors

A mature engineer should be able to switch seamlessly between the three paradigms — knowing when to take command, when to collaborate with AI, and when to hand things over to the system.

### 3.5 Signals of Paradigm Shift

How do you know when you should upgrade from Chain to Vibe Coding, or from Vibe Coding to Loop?

**Signal for shifting from Chain to Vibe Coding**: You find yourself spending a lot of time breaking down steps and writing prompts, but much of the time AI could actually figure out the next step on its own. You feel like a supervisor, not an engineer.

**Signal for shifting from Vibe Coding to Loop**: You find yourself repeating the same interaction pattern every day — the same task types, the same checking steps, the same feedback methods. You feel like a human loop, not a system designer.

When you have these feelings, it's time to shift.

> **Rule of Thumb**: If you're doing the same thing more than three times, consider writing it as a Chain. If you're repeating the same interaction pattern more than ten times, consider turning it into a Loop.

---

---

## Part II: Core Architecture

### Untitled

# Part II: Core Architecture

> *A loop is not a black box — it's a system carefully composed of multiple modules. Understand each building block, and you can build your own tower.*

---

---

# Chapter 4: Automations — The Heartbeat That Makes Loops Actually Spin

If a loop is a living organism, then Automation is its heartbeat.

Without a heartbeat, no matter how powerful the body's organs are, they're meaningless — because they never get awakened. Similarly, without Automation, no matter how powerful an AI agent is, it's just a passive tool waiting to be called — it won't start on its own, won't discover problems on its own, won't begin working on its own.

### 4.1 What is Automation?

Automation (automated triggers) is the startup mechanism of a loop — it determines "when, why, and what kind of loop to launch."

Sounds simple? Isn't it just cron jobs plus event listeners?

In traditional automation, yes. But in Loop Engineering, the meaning of Automation is much richer. Because the execution主体 of a loop is an AI agent, not a fixed script — which means the trigger itself can also be intelligent.

### 4.2 Three Trigger Modes

#### Mode One: Time-Driven

The simplest and most reliable trigger method. "Run every hour," "execute at 3 AM every day," "generate a report every Monday morning."

The advantage of time-driven triggers is simplicity, predictability, and ease of debugging. You know when it will run, and problems are easy to reproduce.

The disadvantage of time-driven triggers is inflexibility. If a task is突发的 (like a production bug), time-driven triggers are too slow. And if there are no tasks but it's still running, that's wasted resources.

**Best for**: Regular inspections, scheduled reports, batch processing tasks

#### Mode Two: Event-Driven

When a specific event occurs, automatically launch a loop. For example:

- New issue created on GitHub → launch classification loop
- PR submitted → launch code review loop
- Monitoring system sends alert → launch troubleshooting loop
- Feishu document commented on → launch reply loop

Event-driven is currently the most mainstream trigger pattern. It responds in time, has high resource utilization, and perfectly fits the "task-driven" work model.

The core challenge of event-driven triggers is **event storms** — if a large number of events flood in within a short time, will the system be overwhelmed? You need queueing mechanisms, rate limiting, and priority mechanisms.

**Best for**: Real-time response tasks, event-driven workflows

#### Mode Three: Condition-Driven

This is the most intelligent and most complex trigger mode. The system continuously monitors some state, and when the state meets specific conditions, automatically launches a loop.

For example:

- "When test coverage in the codebase drops below 80%, automatically start a test-completion loop"
- "When production error rate exceeds threshold, automatically start a rollback loop"
- "When an issue goes unhandled for more than 7 days, automatically escalate notification"

The difference between condition-driven and event-driven: event-driven is "something happened," while condition-driven is "some state persists." Event-driven is pulse-based, condition-driven is continuous monitoring-based.

The challenge of condition-driven triggers is **the cost of state evaluation** — you can't evaluate all conditions every second, that would be too costly. You need to find a balance between "response speed" and "monitoring cost."

**Best for**: Quality monitoring, SLA assurance, proactive operations

### 4.3 Trigger is Design: Good Triggers are Half the Battle

Many people, when designing loops, put all their energy into "how the agent works" and neglect trigger design. But in reality, triggers determine the **rhythm and boundaries** of the entire loop.

A poorly designed trigger can lead to:

- **Too frequent triggering**: System resources exhausted, token costs skyrocket
- **Too sparse triggering**: Problems don't get handled in time, defeating the purpose of automation
- **Inaccurate trigger conditions**: Launches when it shouldn't, doesn't launch when it should
- **Lack of deduplication**: The same event triggers N loops, wasting resources and causing conflicts

A good trigger design should answer these questions:

1. **What is the trigger condition?** (Event? Time? Condition?)
2. **What is the maximum trigger frequency?** (Preventing storms)
3. **How to deduplicate?** (Same task won't be processed repeatedly)
4. **How to prioritize?** (Multiple tasks come in at once, which to handle first?)
5. **How to retry on failure?** (What if the trigger itself fails?)

### 4.4 Case Study: Ralph Loop's Trigger Mechanism

Amplitude's Ralph Loop is a classic case. Its trigger mechanism is very concise:

- **Trigger condition**: GitHub issue tagged with "ralph"
- **Deduplication**: Each issue triggers only once, unless re-tagged
- **Priority**: Sorted by issue creation time, first-come-first-served
- **Concurrency control**: Maximum N tasks running simultaneously

This design seems simple, but it's highly effective. It puts the decision of "should Ralph handle this" in human hands — engineers trigger by tagging. This preserves the flexibility of human judgment while achieving execution automation.

It's a clever design philosophy: **Let humans make judgments, let systems do the execution.**

---

---

### Chapter 5: Worktrees — The Path to Parallelism Without Chaos

Imagine: you have 10 AI agents working simultaneously, all modifying the same codebase. One agent is changing the login module, another is refactoring the payment system, a third is fixing an urgent bug. They're all writing files at the same time, running tests at the same time, submitting code at the same time...

What happens?

The answer is: **disaster.** They'll overwrite each other's changes, cause test failures because of each other's code, and turn the codebase into a mess.

That's why we need Worktrees.

### 5.1 What is a Worktree?

A Worktree is a Git feature that allows you to check out multiple branches simultaneously in the same repository, each branch in a different directory. This way you can work on multiple branches at the same time without switching.

In the context of Loop Engineering, the meaning of Worktree has been expanded — it generally refers to the mechanism of **creating an independent work environment for each task**. Not just Git branches, but also independent virtual environments, independent database instances, independent configuration files.

The core idea: **Each loop works in its own sandbox, without interfering with others.**

### 5.2 Why is Worktree Infrastructure for Loops?

In the era of human coding, parallel work wasn't a big problem — you'd have at most two or three branches open at once, and you knew what each branch was doing.

But in the era of AI agents, the degree of parallelism is completely different. You might have dozens, even hundreds of agents working simultaneously. Without isolation mechanisms, the system simply can't function.

Worktrees solve three key problems:

#### Problem One: Conflict Isolation

Different tasks execute in different Worktrees, their file modifications don't interfere with each other. Agent A modifying `user.py` won't affect the payment refactoring Agent B is working on.

#### Problem Two: State Isolation

Each Worktree has its own dependency environment, its own database, its own configuration. Agent A upgrading a dependency version won't cause Agent B's tests to suddenly fail.

#### Problem Three: Concurrent Scaling

With Worktree isolation, you can easily scale horizontally — run as many simultaneous tasks as you want, as long as you have the resources.

### 5.3 Three Levels of Worktrees

Worktrees aren't all-or-nothing — there are different isolation levels, and you can choose the appropriate level based on the task's characteristics.

#### Level One: Branch-Level Isolation

The most basic isolation. Each task creates a new branch, working in a separate directory. This is Git Worktree's native capability.

**Pros**: Lightweight, fast, almost no extra cost
**Cons**: Only isolates code, not runtime environment
**Best for**: Simple code changes, documentation updates, lint fixes

#### Level Two: Environment-Level Isolation

Each task has not only an independent code branch but also an independent runtime environment — independent Python virtual environments, independent node_modules, independent configurations.

**Pros**: Avoids dependency conflicts, reliable test results
**Cons**: Environment creation takes time, higher resource consumption
**Best for**: Tasks requiring test runs, projects with complex dependencies

#### Level Three: Sandbox-Level Isolation

The most thorough isolation. Each task runs in an independent container (Docker) or virtual machine, with independent filesystem, independent networking, independent everything.

**Pros**: Complete isolation, absolute safety
**Cons**: Heaviest, slowest, highest cost
**Best for**: Untrusted code, tasks involving sensitive data, production environment operations

> **Rule of Thumb**: Start with the lightest isolation level and upgrade only when problems arise. In most cases, branch-level + environment-level isolation is sufficient.

### 5.4 Worktree Lifecycle Management

Creating a Worktree is easy — the hard part is managing its lifecycle. A complete Worktree lifecycle includes:

1. **Creation**: When a task starts, create a new Worktree based on the main branch
2. **Initialization**: Install dependencies, configure environment, prepare data
3. **Execution**: Agent completes the task in the Worktree
4. **Cleanup**: After the task ends, delete the Worktree, free resources
5. **Archiving**: (Optional) Keep the Worktree for a period for debugging

The most easily overlooked part is the **cleanup step**. If Worktrees aren't cleaned up when tasks fail, your disk will quickly fill up with hundreds or thousands of abandoned Worktrees.

You need a "garbage collection" mechanism — periodically checking for timed-out, failed, or completed Worktrees and automatically cleaning them up.

### 5.5 Case Study: Ralph Loop's Worktree Practice

Ralph Loop's Worktree management is worth learning from. Its approach:

- Each issue corresponds to an independent Git branch and Worktree directory
- After task completion (whether success or failure), Worktree is automatically cleaned up
- If the task fails, the Worktree is kept for 24 hours for debugging, then auto-deleted
- A background task periodically checks and cleans up zombie Worktrees

This design ensures isolation while controlling resource costs. The key insight: **cleanup mechanisms are just as important as creation mechanisms.**

---

---

### Chapter 6: Skills — Stop Explaining Your Project from Scratch Every Time

"Wait, let me first tell you about our project structure…"

"Our coding standards are like this…"

"The design philosophy of this module is…"

If you work with AI agents regularly, these words must sound familiar. Every time you start a new task, you spend a lot of time explaining project background, coding standards, design patterns to AI…

Then next time, with a new task, a new session, a new agent, you have to say it all over again from scratch.

That's the problem Skills solve.

### 6.1 What is a Skill?

A Skill is a mechanism for **codifying** project knowledge, workflows, and behavior patterns. It's not a one-time instruction written in a prompt — it's persistent knowledge that agents can load and use repeatedly.

Think of a Skill as an agent's "skill book." When an agent gets a skill book, it learns a new skill — it knows what to do in specific scenarios, what standards to follow, what tools to use.

### 6.2 The Difference Between Skills and Regular Prompts

Many people ask: Aren't Skills just longer prompts? What's the essential difference?

The difference lies in **three dimensions**:

| Dimension | Regular Prompt | Skill |
|-|-|-|
| Lifecycle | One-time, gone when session ends | Persistent, can be used repeatedly |
| Management | Scattered everywhere, hard to maintain | Centralized management, version control |
| Composition | Can only be linearly concatenated | Can be loaded on demand, flexibly combined |
| Trigger | Manual input | Auto-loaded or called on demand |

For example: "You are a React expert" — that's a prompt.
"Our project uses React 18 + TypeScript, state management with Zustand, styling with Tailwind CSS, component naming with PascalCase, file structure organized by feature module, testing with Vitest…" — that's a Skill.

Skills don't just tell the agent "who you are" — they tell the agent "how you should work in this project."

### 6.3 Four Types of Skills

Not all Skills are the same. Based on content and purpose, Skills can be divided into four categories:

#### Type One: Knowledge Skills

Tell the agent "what it is" — project background, tech stack, coding standards, design principles, business logic.

For example:

- Overall architecture and module division of the project
- Code style and naming conventions
- Commonly used design patterns and best practices
- Core concepts and terminology of the business domain

Knowledge Skills are the most foundational — they make the agent "know the ropes," so it doesn't ask basic questions or make common-sense mistakes.

#### Type Two: Process Skills

Tell the agent "how to do it" — standard processes and steps for completing certain types of tasks.

For example:

- "Standard bug-fixing process: reproduce first → locate root cause → write fix → add tests → verify"
- "Code review checklist: security, performance, readability, test coverage"
- "PR submission standards: title format, description template, linked issues"

Process Skills are efficiency multipliers — they mean agents don't have to think through the process from scratch every time, they just follow best practices.

#### Type Three: Tool Skills

Tell the agent "what to use" — what tools are available, how to use them, when to use them.

For example:

- "If you need to query the database, use the `db_query` tool, parameter format is…"
- "If you need to search code, use the `code_search` tool, supports regular expressions"
- "If you need to deploy, call `deploy_service`, but only in the test environment"

Tool Skills expand capability — they let the agent know what weapons it has and when to use which one.

#### Type Four: Role Skills

Tell the agent "who it is" — the agent's identity, responsibilities, boundaries.

For example:

- "You are a senior frontend engineer, focused on user experience and performance optimization"
- "You are a security auditor, your responsibility is to find security vulnerabilities in code"
- "You are a technical documentation editor, your goal is to make documentation clear and accessible"

Role Skills are the rudder of direction — they set the agent's stance and priorities, influencing the trade-offs it makes in decisions.

### 6.4 Skill Design Principles

Designing Skills isn't just throwing all information in. Good Skill design follows several principles:

#### Principle One: Focus, Don't Greed

One Skill does one thing. Don't stuff "React standards," "testing standards," and "deployment流程" all into one Skill. Split them into multiple small Skills and load them on demand.

#### Principle Two: Structured, Not Prose

Skills are for machines to read, not humans. Use clear headings, lists, code blocks — let the agent quickly locate and understand information.

#### Principle Three: Example-Driven

Examples are more persuasive than rules. Don't just say "we use PascalCase for component naming" — give a complete component example. Agents learn far more from examples than from rules.

#### Principle Four: Verifiable

Good Skills should be verifiable. How do you know if the agent correctly understood and executed the Skill? Give it checklists and self-test methods.

### 6.5 The Evolution of Skills: From Static to Dynamic

Currently most Skills are still static — written by humans and then unchanged. But the ultimate form of Skills is **dynamic, self-evolving**.

Imagine:

- After each task, the agent automatically summarizes "what was learned this time" and updates it into the Skill
- The system analyzes all failed tasks, automatically discovers "agents tend to make mistakes in XX scenarios," then automatically supplements the corresponding Skill
- Multiple agents share a Skill library — the mistakes one agent made, others won't repeat

That's the future of Skills — they're not human-written documentation, but collective memory that the system continuously accumulates and evolves through practice.

> **Core Idea**: Skills are the "corporate culture" of a loop system. Just as a company's culture determines how employees behave, a loop system's Skill体系 determines the quality and style of its agents' work.

---

---

### Chapter 7: Plugins & Connectors — Letting Agents Touch the Real World

An AI agent that can only read and write code files can do very limited things.

It wants to reproduce a bug? It needs to be able to run tests.
It wants to check data in the database? It needs to connect to the database.
It wants to see user feedback? It needs to read the support ticket system.
It wants to deploy a version? It needs to call the deployment platform.

If an agent can only spin around in code files, it's like a craftsman locked in a room — no matter how skilled, it can't accomplish much.

That's why we need Plugins and Connectors.

### 7.1 What Are Plugins and Connectors?

**Plugins** are extension modules that add specific capabilities to agents. For example, the GitHub plugin lets agents operate GitHub, the Slack plugin lets agents send messages, the database plugin lets agents query data.

**Connectors** are a more general concept — they refer to all mechanisms by which agents connect to external systems. Plugins are one form of Connector implementation, MCP servers are another, API integrations are another.

Put simply: **Plugins & Connectors solve the problem of "how far an agent's hands can reach."**

### 7.2 MCP: The Standard Protocol for Connection

When talking about Connectors, you can't avoid MCP (Model Context Protocol).

MCP is an open protocol proposed by Anthropic that defines standard interaction methods between AI agents and external tools. Before MCP, each tool had its own integration method, and agents had to be redeveloped to connect to each new tool. After MCP, as long as a tool supports the MCP protocol, agents can use it directly.

It's like the USB interface — with the USB standard, you don't have to design a separate interface for each peripheral, just plug it in.

MCP's core concepts are simple:

- **MCP Server**: A service provided by an external tool, exposing a set of tool functions
- **MCP Client**: The client on the agent side, calling tools provided by the Server
- **Tool call protocol**: Standard request/response format

The significance of MCP is that it turns "agents connecting to the world" from a project that requires custom integration one by one, into an ecosystem that can scale systematically.

> **Importance**: If large language models are the CPU of the AI era, then MCP is the USB bus of the AI era.

### 7.3 Categories of Connectors

Agents need to connect to all kinds of systems. We can divide them into several major categories:

#### Code & Version Control

- **Git/GitHub/GitLab**: Read code, submit PRs, manage issues, code review
- **Code search tools**: Sourcegraph, local search
- **CI/CD systems**: Jenkins, GitHub Actions, GitLab CI

#### Data & Storage

- **Databases**: MySQL, PostgreSQL, MongoDB, Redis
- **Data warehouses**: BigQuery, Snowflake, ClickHouse
- **Object storage**: S3, OSS

#### Communication & Collaboration

- **Instant messaging**: Slack, Feishu, Discord, Teams
- **Project management**: Jira, Linear, Trello, Asana
- **Document systems**: Notion, Feishu Docs, Confluence, Google Docs

#### Monitoring & Operations

- **Monitoring systems**: Prometheus, Grafana, Datadog
- **Logging systems**: ELK, Loki
- **Alerting systems**: PagerDuty, Opsgenie
- **Cloud platforms**: AWS, GCP, Azure

#### Business Systems

- **CRM**: Salesforce, HubSpot
- **Customer service**: Zendesk, Intercom
- **Finance**: QuickBooks, Xero

Each category of system you connect expands the agent's capability boundary. The more connections, the more complete the things agents can do.

### 7.4 Security Boundaries of Connectors

With great power comes great risk. Connecting connectors to agents isn't about connecting as many as possible — you need to carefully consider security boundaries.

Several key security principles:

#### Principle One: Principle of Least Privilege

Agents should only have the minimum privileges necessary to complete their tasks. They need to read the database? Give read-only access. They need to send messages? Only give messaging permissions for specific channels. They need to deploy? Only give deployment permissions for the test environment.

Never give an agent admin privileges. Never.

#### Principle Two: Audit Log Principle

Every external operation an agent performs must have complete audit logs. Who (which agent), when, what operation was performed, what the result was — all must be recorded.

Audit logs aren't just for tracing problems — they let you observe and analyze agents' behavior patterns.

#### Principle Three: Human Confirmation Principle

For high-risk operations (like deleting data, modifying production environment configurations, transferring money), there must be a human confirmation step. Agents can initiate operations, but must wait for human approval before execution.

This isn't about not trusting agents — it's engineering discipline. Human engineers go through approval processes for high-risk operations too — why should agents be exceptions?

### 7.5 Case Study: Minglue Technology's Agent Connector Practice

Minglue Technology is a company with over 1,400 employees and 2,900+ deployed AI agents. Their agents handle various tasks like financial reporting, customer service, and data analysis.

Their Connector system has several characteristics:

1. **Layered authorization**: Different levels of agents have different Connector access permissions. Basic agents can only read public data, while advanced agents can access sensitive systems.
2. **Unified gateway**: All external calls from agents go through a unified gateway that handles authentication, rate limiting, and auditing.
3. **Operation分级**: Operations are divided into three levels: "read," "write," and "execute." Read operations can execute automatically, write operations require approval, and execute operations (like deployment) require double confirmation.

This system allows their 2,900+ agents to work efficiently without going out of control. The core lesson: **connector design is essentially trust boundary design.**

---

---

### Chapter 8: Sub-agents — The Person Who Writes Code and the Person Who Reviews It Are Not the Same

"You review your own code? Then it's like not reviewing at all, right?"

This is common sense in software development: the person who writes code and the person who reviews it should be different people. Because when you're writing code, you get lost in the details and it's hard to see your own blind spots. An outsider's perspective is clearer — someone else looking at it can often spot problems at a glance.

The same principle applies to AI agents.

An agent that both writes code and checks it itself is like a student grading their own exam — it carries the same mental blind spots, and mistakes it made before are likely to be made again.

That's why we need Sub-agents.

### 8.1 What is a Sub-agent?

A Sub-agent is an independent agent created by the main agent (or the system) within a main loop, responsible for completing specific subtasks.

Sounds like team collaboration? Exactly — Sub-agents essentially move human team collaboration patterns into AI systems. What one person can't finish, divide among several people. Code one person can't review accurately, have someone else review it again.

### 8.2 Maker-Checker Pattern: The Classic Sub-agent Architecture

The most common and most effective sub-agent pattern is the **Maker-Checker pattern**.

- **Maker**: Responsible for writing code, implementing, producing results
- **Checker**: Responsible for reviewing code, verifying results, finding problems

What the Maker produces, the Checker finds faults in. What faults the Checker finds, the Maker fixes. Both sides iterate repeatedly until the Checker is satisfied.

Why does this pattern work? Because **different agents have different perspectives**:

- The Maker focuses on "how to implement" — its thinking is constructive, creative
- The Checker focuses on "what problems exist" — its thinking is critical, skeptical

These two modes of thinking are difficult for a single agent to possess simultaneously. Asking the same agent to be both player and referee, it can hardly switch modes.

> **Core Insight**: Having an agent check its own code gives linear efficiency improvement. Having two different agents check each other's work gives exponential quality improvement.

### 8.3 Sub-agent Division Modes

Maker-Checker is just the most basic pattern. Depending on task complexity, sub-agents can have richer division-of-labor approaches.

#### Mode One: By Responsibility

Different sub-agents are responsible for different responsibilities. For example:

- **Architect agent**: Responsible for overall方案 design and technology selection
- **Developer agent**: Responsible for concrete code implementation
- **Tester agent**: Responsible for writing tests and doing verification
- **Security agent**: Responsible for security auditing
- **Documentation agent**: Responsible for writing docs and comments

This is like a complete development team, each person (agent) has their own role.

#### Mode Two: By Module

Split a large task into multiple modules, each sub-agent负责 one module. For example, refactoring a large system:

- Agent A负责 the frontend module
- Agent B负责 the API layer
- Agent C负责 the database layer
- Agent D负责 integration and joint debugging

This division method works well for scenarios with clear task boundaries and low coupling between modules.

#### Mode Three: By Perspective (Red Team / Blue Team)

Not divided by work content, but by stance. For example, evaluating a technical proposal:

- **Blue team agent**: Responsible for arguing the feasibility and advantages of the proposal
- **Red team agent**: Responsible for finding faults, identifying risks, raising objections
- **Judge agent**: Synthesizes both sides' opinions, makes the final judgment

This pattern is best for decision-making tasks — when you need to comprehensively consider pros and cons, having agents of different stances debate each other is far more thorough than one agent thinking it through alone.

### 8.4 The Coordination Challenge of Sub-agents

Sub-agents sound great, but in practice you run into many problems. The hardest part isn't creating sub-agents — it's **coordinating them**.

Several typical coordination challenges:

#### Challenge One: Context Transfer

How does the main agent completely pass task background, relevant information, and constraints to the sub-agent? Pass too little and the sub-agent can't do a good job; pass too much and it wastes tokens.

**Solution**: Design standardized task description templates containing four elements: goal, background, constraints, deliverables.

#### Challenge Two: Result Integration

Results produced by multiple sub-agents — how to integrate them together? If two sub-agents' results conflict, who do you listen to?

**Solution**: Clearly define each sub-agent's responsibility boundaries to avoid overlap. Set up an "integration agent" specifically responsible for merging and coordinating results.

#### Challenge Three: Cost Control

Work that one agent could finish, split among five agents — token costs multiply several times. Is it worth it?

**Solution**: Decide based on task importance and complexity. Simple tasks don't need splitting; high-risk tasks才 need multi-agent cross-verification.

#### Challenge Four: Communication Overhead

Communication between agents also costs money. Going back and forth discussing for half the day, it might have been faster for one agent to just do it directly.

**Solution**: Minimize direct interaction between agents, let the main agent do information relay and coordination. Design clear interfaces and delivery standards.

### 8.5 Case Study: AddWeb AI's 7-Agent Self-Correction Loop

AddWeb AI is an edtech company that built a self-correction loop system of 7 specialized agents for developing their education platform.

The 7 agents are:

1. **Product Manager Agent**: Defines requirements and acceptance criteria
2. **Architect Agent**: Designs technical approach
3. **Frontend Agent**: Implements frontend code
4. **Backend Agent**: Implements backend code
5. **Tester Agent**: Writes tests and verifies functionality
6. **Security Agent**: Performs security audits
7. **Review Agent**: Synthesizes all feedback, decides whether to pass

A requirement, from entering the system to final delivery, goes through the relay of these 7 agents. Each agent only does what it's best at, then passes it to the next. If a problem is found at any stage, it's sent back to the previous stage for correction.

What was the result? Their education platform development cycle went from the traditional 16-20 weeks down to a stage every 4 weeks.

This case teaches us: **specialized division of labor + closed-loop collaboration = qualitative leap.**

---

---

### Chapter 9: Memory System — The Spine of the Loop

If a loop starts up every time as if seeing the project for the first time — not knowing what was done before, not knowing which approaches were tried and failed, not knowing the project's coding style — how efficient would it be?

The answer is: not very.

It would repeatedly step in the same pitfalls, revisit already-rejected approaches, and understand the project from scratch every time. Like a person without long-term memory — every day is a new day, but every day is standing still.

That's the importance of the Memory system. If Automation is the loop's heartbeat, Worktree is its body, and Skill is its knowledge, then Memory is the loop's **spine** — without it, the whole system can't stand up.

### 9.1 What is a Memory System?

The Memory system is the module in a loop responsible for **storing, organizing, and retrieving historical information**. It ensures loops don't start from zero every time, but can stand on the shoulders of past experience.

What's the difference between Memory and Skill?

- **Skills** are relatively stable knowledge — project standards, tech stack, workflows. They change slowly and are usually written by humans.
- **Memory** is dynamically accumulated experience — what tasks were done, what pitfalls were encountered, which approaches work, which users reported what problems. It grows continuously and is usually auto-recorded by the system.

Put simply: **Skills are "textbook knowledge," Memory is "hands-on experience."**

### 9.2 Four Levels of Memory

A complete Memory system typically includes four levels of memory:

#### Level One: Episodic Memory

Memory of the current session/current task. Files the agent read during this task, attempts it made, intermediate thought processes.

Episodic memory is characterized by high volume, detail, but short lifecycle. After the task ends, most of it is no longer needed.

**Storage medium**: Usually directly in the context window

#### Level Two: Working Memory

A summary of key information for the current task — what the task goal is, what's been done, what problems were found, what the next steps are.

Working memory is the agent's "workbench" — it doesn't need to remember all details, but needs to remember key nodes and current state.

**Storage medium**: Structured state objects, task summaries

#### Level Three: Long-Term Memory

Cross-task memory — what was done before in this project, which approaches proved effective, which pitfalls to avoid, what user preferences exist.

Long-term memory is the most valuable part of a loop system — it makes the system smarter the more you use it. The first task might be bumpy; the hundredth task will be smooth.

**Storage medium**: Vector databases, knowledge graphs, structured databases

#### Level Four: Collective Memory

Cross-agent, cross-project memory — a shared experience library for all loops across the organization. Pitfalls encountered by Project A won't be repeated by Project B; best practices summarized by one agent benefit all agents.

Collective memory is the ultimate form — it makes an organization's entire AI system form "collective intelligence" rather than fighting各自 battles.

**Storage medium**: Centralized knowledge platform, shared Skill library, organization-level memory bank

### 9.3 Core Operations of Memory: What to Store, How to Store, How to Retrieve

Designing a Memory system, the core is answering three questions: What to store? How to store? How to retrieve?

#### What to Store? — Memory Filtering

Not everything is worth remembering. Remembering too much irrelevant information反而 interferes with retrieval and wastes resources.

You need to filter:

- ✅ Final results and key decisions of tasks
- ✅ Failed attempts and their causes (to avoid repeating)
- ✅ User preferences and feedback (personalized service)
- ✅ Newly learned patterns and best practices
- ❌ Detailed logs of intermediate processes (too trivial)
- ❌ Outdated information (misleading)

#### How to Store? — Memory Organization

Storage method determines retrieval efficiency. Common organization methods:

- **Vector storage**: Embed memories into vectors for semantic retrieval
- **Structured storage**: Store key information as database records for conditional querying
- **Knowledge graph**: Store relationships between entities, supporting reasoning and association discovery

The best approach is **hybrid storage** — vector storage for semantic search, structured storage for precise queries, knowledge graphs for relational reasoning.

#### How to Retrieve? — Memory Retrieval

The value of memory lies in being usable. If you store a huge pile but can't find anything, it's the same as not storing.

Retrieval strategies:

- **By relevance**: Which historical memories are most relevant to the current task?
- **By time**: Have there been similar tasks recently?
- **By importance**: Are there high-priority memories to check first?
- **By failure pattern**: What pitfalls have been encountered for this type of task before?

### 9.4 Two Major Traps of Memory

Bigger isn't always better when it comes to Memory systems. Two common traps to watch for:

#### Trap One: Memory Contamination

If wrong information is stored in memory, agents will repeatedly make the same mistakes. And wrong memory is scarier than no memory — because the agent will firmly believe in it.

**Countermeasures**:

- Validation mechanism before memories enter the store
- Memories have "confidence" scores; low-confidence memories aren't used first
- Periodically "clean memories" — mark or delete memories proven wrong

#### Trap Two: Memory Overload

With too many memories, retrieval pulls up a bunch of irrelevant stuff that反而 interferes with the agent's judgment. It's like how people who know too much tend to overthink — relevant and irrelevant all surge up, making it hard to decide.

**Countermeasures**:

- Strict relevance thresholds for memory retrieval
- Limit the number of memories returned per retrieval
- Memories have "usage frequency" and "recency" weights; prioritize returning commonly used and fresh memories

### 9.5 Case Study: How Memory Makes Systems "Smarter the More You Use Them"

Imagine a code review loop. When it first launches:

- Day 1: Review quality is mediocre, often misses project-specific standard issues
- Week 1: It starts remembering some common error patterns, review quality noticeably improves
- Month 1: It has accumulated hundreds of review cases, knows what problems this project is most prone to, what the team cares about most
- Month 3: Its review quality already surpasses most junior engineers — because it's seen more cases than any single person

That's the power of the Memory system — **it lets system capability grow linearly over time, while human capability growth has a ceiling.**

> **Ultimate Vision**: A mature loop system should be like a veteran employee who's been at the company for ten years — knows all the history, understands all the unwritten rules, has stepped in every pit, knows who to go to for any problem. The difference is, this veteran employee doesn't need to sleep and never quits.

---

---

## Part III: Design & Practice

### Untitled

# Part III: Design & Practice

> *Knowing the names of all the building blocks doesn't mean you can build a bridge. Theory meets reality through the cycle of design, practice, failure, and iteration.*

---

---

# Chapter 10: Designing Your First Loop

### A Five-Step Methodology from Scratch

Alright, you've understood the core concepts and six modules of Loop Engineering. Now you want to design a loop yourself. Where do you start?

Many people's first reaction is: "I need to build a complete system, all six modules, nothing less."

Wrong.

The right approach to designing a loop isn't starting with architecture — it's starting with **a specific pain point**. Find the task that gives you the biggest headache, the most repetitive one, and turn it into your first loop.

Here's a battle-tested five-step methodology.

### Step One: Choose the Right Task — Not All Tasks Are Suitable for Loop-ification

The first step is also the most crucial one: **choose the right first task.** Choose well, and you get twice the result with half the effort. Choose poorly, and you might lose faith in Loop Engineering forever.

What kind of task makes a good first loop?

**Good candidate tasks have these characteristics:**

- ✅ **High repetition**: Done weekly/daily, frequent enough
- ✅ **Well-defined**: What's the input, what's the output, what's the success criteria — all clear
- ✅ **Controlled risk**: Even if done wrong, consequences aren't severe, easy to roll back
- ✅ **Verifiable**: Can automatically judge if the result is correct, no need for human to check every time
- ✅ **Single/few steps**: Don't start with complex multi-agent collaboration

**Bad candidate tasks:**

- ❌ Tasks done once a year (too low ROI)
- ❌ Vague goals like "improve user experience" (can't verify)
- ❌ Tasks that directly modify production databases (too risky)
- ❌ Tasks requiring deep business judgment (AI can't handle)

> **Rule of Thumb**: Your first loop should be the kind of task where "getting it right is no big deal, but getting it wrong won't kill anyone." Build confidence first, then upgrade gradually.

### Step Two: Define Clearly — Input, Output, Success Criteria

After choosing the task, don't rush to write code. First answer three questions clearly:

**1. What is the input?**
Where does the loop get tasks from? GitHub Issues? Feishu messages? Time triggers? What's the input format? What fields are required?

Think of input as a function's parameters — with clearly defined parameters, the function can be written correctly.

**2. What is the output?**
What does the loop deliver when it's done? A PR? An analysis report? A comment? An email?

Output format also needs to be clear. For example, PR title format, description template, what tags to add.

**3. What is the success criteria?**
This is the most important and most easily overlooked question. How do you judge that what the loop did is "correct"?

Success criteria could be:

- Tests pass
- No lint errors
- Code compiles successfully
- Meets certain acceptance conditions
- (For tasks that can't be auto-verified) Approved by a human

Without clear success criteria, the loop will become — as Chapter 12 discusses — a perpetual motion machine with no exit condition.

### Step Three: Design the Flow — Draw Your Loop Diagram

After defining inputs and outputs clearly, you can design the loop's internal flow.

The simplest loop flow looks like this:

```
Trigger → Receive task → Agent executes → Verify result → Success?→ Yes → Deliver
                                      ↓No
                                    Retry?→ Yes → Agent executes (with error feedback)
                                      ↓No
                                    Escalate to human
```

When designing the flow, ask yourself:

- **How many steps?** Keep it simple — getting the first version right is good enough
- **Who makes decisions?** Is the decision-maker at each step the agent or the system?
- **What happens on failure?** How many retries? What's different each time? When to give up?
- **When do humans介入?** No humans needed at all? Or human confirmation needed at the end?

I recommend drawing it on paper or a whiteboard — a visualized flow chart helps you discover many problems you wouldn't find just thinking.

### Step Four: Minimal Implementation — Get It Running First, Then Optimize

Many people fall into the "perfectionism trap" when designing loops — wanting the most elegant architecture, the most complete features, the best experience. Result: three months of work and still not launched.

Remember this principle: **the first version just needs to work.**

Your first loop can be very crude:

- No MCP, just call CLI tools directly
- No Worktree, just work in one directory (anyway, the task is simple, low conflict probability)
- No Skills, write all instructions in the prompt
- No Memory, start from scratch every time
- No Sub-agents, just one agent doing everything

Crudeness doesn't matter. What matters is — **it actually runs, it actually saves you time.**

Once it's running, you can gradually optimize based on real pain points in usage. Whatever hurts the most, optimize that first.

It's the same principle as building products: have an MVP (Minimum Viable Product) first, then iterate.

### Step Five: Measure and Iterate — Let the Loop Get Better Over Time

Launching the loop isn't the end — it's the beginning.

You need to measure key metrics to judge the loop's effectiveness and guide next-step optimization:

- **Success rate**: How many tasks completed successfully? How many failed?
- **Accuracy**: Among successful tasks, how many were actually done correctly (no rework needed)?
- **Average time**: How long does it take to complete one task on average?
- **Human intervention rate**: How many tasks require human handling?
- **Cost**: How many tokens/money does each task cost on average?

With these metrics, you'll know what to optimize:

- Low success rate? → Optimize prompts, add verification steps
- Low accuracy? → Add Checker agents, strengthen quality gates
- High human intervention rate? → Analyze intervention reasons, target optimization
- Too costly? → Optimize context, reduce retries, use smaller models

> **Core Idea**: The loop itself is also an iterative cycle. You design the loop, then the loop's运行数据反过来 guides you to optimize the loop. That's the real "loop engineering."

### Case Study: An Engineer's First Loop

Xiao Wang is a backend engineer. The thing he finds most annoying is that every time someone files a bug issue, he has to spend time分类 — which module does this bug belong to? How severe is it? Is it a duplicate?

He decided to automate this with a loop.

**Step One, choose task**: Issue classification. High repetition (daily), well-defined (input is Issue, output is tags), low risk (just change it back if wrong), verifiable (humans can spot-check).

**Step Two, define clearly**:

- Input: GitHub Issue title and description
- Output: Tag the issue with module and priority labels
- Success criteria: Tag accuracy reaches 80%+ (human spot-check verification)

**Step Three, design flow**:

```
New issue created → Trigger loop → Agent reads issue content → Agent judges module and priority → Add tags → End
(If fails, retry once; if still fails, skip and wait for human)
```

**Step Four, minimal implementation**: Used GitHub Actions + Claude Code API, wrote a few dozen lines of script. No Worktree, no Skills, no Memory — just the simplest implementation.

**Step Five, iterate**:

- Week 1: 60% success rate, often mislabeling modules. → Added project module documentation as context.
- Week 2: 80% success rate, but priority judgment was off. → Added detailed explanation and examples of priority criteria.
- Month 1: 90% success rate, basically no need to manage. → Added Memory, storing historical classification results, getting more accurate over time.

Now, this loop saves Xiao Wang about 8 hours per month. The total time he spent building and optimizing it: less than 10 hours.

**That's the ROI of Loop Engineering: spend a little time upfront, benefit continuously later.**

---

---

### Chapter 11: Quality Gates — A Loop Without Gates Just Produces Garbage Faster

"The good thing about automation is getting work done faster. The bad thing about automation is getting garbage work done faster."

— A veteran engineer

Without quality gates, a loop is just a "garbage production machine." The faster it runs, the more garbage it produces. You think you're improving efficiency, but actually you're creating technical debt.

Quality Gates are the most critical safety net in a loop system. They ensure — only output meeting quality standards passes;不合格 output is sent back for rework.

### 11.1 What Are Quality Gates?

Quality gates are checkpoints in the loop flow — an agent's output must pass these checks to enter the next stage.

You can think of them as quality inspection stations in a factory. Products come off the assembly line, and inspectors check for problems. Those without issues pass, those with problems are sent back for rework.

In loop systems, quality gates can be automated (tool checks), intelligent (AI agent reviews), or manual (human approval).

### 11.2 The Seven-Layer Quality Gate System

A complete loop system should have multiple layers of quality gates. Earlier gates are lighter and more automated; later gates are stricter and require more intelligent judgment.

#### G0: Syntax Gate

The most basic check — does the code compile? Are there syntax errors? Does lint pass?

- **What it checks**: Compilation, lint, formatting
- **Executor**: Automated tools
- **Cost**: Very low
- **Speed**: Seconds

This is the most basic gate. Code that doesn't pass G0 isn't even qualified to be reviewed.

#### G1: Test Gate

Is the functionality correct? — Do tests pass?

- **What it checks**: Unit tests, integration tests, E2E tests
- **Executor**: Automated test frameworks
- **Cost**: Low to medium
- **Speed**: Seconds to minutes

Test gates are the basic guarantee of functional correctness. But note — tests can only prove "there IS a bug," not "there is NO bug." Passing tests doesn't mean the functionality is correct; it only means "current test cases found no problems."

#### G2: Static Analysis Gate

How's the code quality? — Are there security vulnerabilities? Performance issues? Code smells?

- **What it checks**: Security scanning, code complexity, duplicate code, potential bugs
- **Executor**: Static analysis tools + AI review
- **Cost**: Low
- **Speed**: Seconds to minutes

Static analysis tools can find many pattern-based problems, but are powerless against design-level or architecture-level issues.

#### G3: AI Review Gate

Another AI agent reviews the code — doing a comprehensive check from the perspectives of design, readability, and best practices.

- **What it checks**: Code design, readability, edge cases, error handling, best practices
- **Executor**: Checker agent (different model, different role)
- **Cost**: Medium
- **Speed**: Minutes

This is the core环节 of the Maker-Checker pattern. Having "another brain" check often finds many problems that "one's own brain" can't see.

> **Best Practice**: Use different models for Maker and Checker. For example, use Claude Opus to write code and GPT-4o to review. Or vice versa. Different models have different blind spots, and cross-verification works best.

#### G4: Integration Gate

Put the changes into the complete system — does it work properly?

- **What it checks**: Integration tests, regression tests, performance benchmarks
- **Executor**: CI/CD system + automated testing
- **Cost**: Medium to high
- **Speed**: Minutes to hours

Many problems can't be found when looking at code in isolation — they only surface in the complete system. The integration gate catches these.

#### G5: Staging Gate

Deploy to staging environment, run it for real, see if there are problems?

- **What it checks**: Staging environment verification, canary release, smoke tests
- **Executor**: Automated tools + AI agents
- **Cost**: High
- **Speed**: Hours

The closer to the real environment, the more real the problems you find. But the cost is also higher.

#### G6: Human Gate

The last line of defense — humans make the final confirmation.

- **What it checks**: Business logic judgment, design decisions, risk assessment
- **Executor**: Human engineers
- **Cost**: Extremely high (human time is most expensive)
- **Speed**: Hours to days

Many people think the goal of Loop Engineering is "no humans needed at all." That's a misunderstanding. The goal of Loop Engineering is "let humans only do what truly requires humans."

What requires humans? Judgment, decision-making, trade-offs. Not repetitive labor, not mechanical checking, not staying up late monitoring processes.

### 11.3 Principles of Gate Design

Designing quality gates — more isn't always better. Too many gates, and the流程 becomes too slow, defeating the purpose of automation. Too few gates, and quality can't be guaranteed.

Several design principles:

#### Principle One: Shift-Left Principle

Problems that can be found early, don't leave for later.

The later the gate, the higher the cost. G0 (syntax check) costs almost nothing, G6 (human review) costs the most. So try to eliminate problems in earlier gates.

This is "quality shift-left" — push quality checks as early as possible.

#### Principle Two: Layering Principle

Different gates check different things — don't repeat.

For example, G0 checks syntax, so don't have G3 check syntax again. G3 should check things G0 can't — design, readability, edge cases.

Each layer of gate has its own clear responsibility — no overlap, no gaps.

#### Principle Three: Cost Matching Principle

High-value tasks use high-cost gates; low-value tasks use low-cost gates.

Putting the full G0-G6 suite on a typo fix? That's using a sledgehammer to crack a nut. Only putting G0-G2 on a core payment system change? That's playing with fire.

Based on task importance and risk level, flexibly configure the number and strictness of gates.

#### Principle Four: Traceability Principle

Each gate's check results must be recorded — when it was checked, what was checked, what the result was, why it passed/failed.

This isn't just for tracing blame when problems occur — it's for analysis and optimization — which gate finds the most problems? Which gate never finds problems (is it too lenient?).

### 11.4 Case Study: Amplitude's Ralph Loop Quality Control

Ralph Loop is Amplitude's AI development agent that delivers 102 features per week. With such high output volume, how is quality guaranteed?

Their quality control system works like this:

1. **Automated testing**: Every PR automatically runs the complete test suite. Failures are sent back directly.
2. **AI code review**: Code written by Ralph goes through初步 review by another AI agent.
3. **Human engineer review**: The final PR still needs human review. But because there are already two layers of filtering before it, there's much less for humans to review.
4. **Progressive merging**: Merge to development branch first, run for a few days with no issues before merging to main.

The key insight: **Ralph Loop's goal isn't 100% automation — it's reducing human workload to 1/10 of before.** Humans still review code, but where they used to review 10 PRs in the time it took, now they can review 100 — because most low-level problems have been filtered by earlier gates.

> **Core Idea**: The purpose of quality gates isn't "ensuring 100% no problems" — that's impossible. The purpose of quality gates is "reducing problem density to a level humans can handle."

---

---

### Chapter 12: Failure Modes & Pitfall Guide

### Six Failure Modes and Three Deep Risks

"In theory, theory and practice are the same. In practice, they're not."

— Yogi Berra

When designing loops, you think only of successful scenarios — agents executing tasks perfectly, systems running automatically, efficiency dramatically improving.

But the reality is: your first loop will probably fail. Not a small failure — a big one — running amok, burning money, producing garbage, crashing the system.

This is normal. Everyone who's done Loop Engineering has stepped in pitfalls. What matters isn't avoiding all failures (impossible), but knowing what pitfalls exist and how to climb out when you fall in.

This chapter summarizes six failure modes and three deep risks.

### 12.1 Failure Mode One: No Exit Condition (Perpetual Motion Machine)

**Symptoms**: The loop starts and just keeps running and running, like it'll never finish. Tokens burn through fast, but you never see results.

**Cause**: No clearly defined exit conditions. The agent loops infinitely in a state of "I think it can still be better" — changing and changing, optimizing and optimizing, never satisfied.

**Why this happens**: When humans do tasks, we know "good enough is enough." But AI doesn't have this intuition. You don't give it a clear stop signal, it'll keep going forever.

**Solutions**:

1. **Clear success criteria**: Define "done" clearly. For example, "tests pass + lint passes = done," not "code is well-written."
2. **Max steps / max token limit**: Set hard caps. When the cap is reached, force stop regardless of completion.
3. **Diminishing returns detection**: If N consecutive iterations show no substantive improvement, stop.

> **Lesson**: "Better" is the enemy of "good." In loops, this is especially true.

### 12.2 Failure Mode Two: Repeated Failure Without Strategy Change (Hitting a Wall)

**Symptoms**: The agent encounters an error, makes a correction, tries again — same error. Corrects again, tries again — still wrong. Making the same mistake over and over, like a fly hitting a window.

**Cause**: The agent has no mechanism for learning from failure. After each failure, it just adjusts slightly and tries again the same way. If the root cause isn't found, no amount of retries helps.

**Why this happens**: When humans encounter repeated failure, they change their approach — "am I going in the wrong direction?" But AI easily gets stuck in the same thinking framework. Its "corrections" are often micro-adjustments, not fundamental rethinking.

**Solutions**:

1. **Failure count threshold**: After N consecutive failures, force a strategy change.
2. **Root cause analysis step**: After consecutive failures, stop to do root cause analysis instead of immediately retrying.
3. **Switch model / switch agent**: Let another agent (preferably a different model) diagnose the problem.
4. **Escalate to human**: If all strategies have been tried and still failing, don't push through — get a human.

### 12.3 Failure Mode Three: Context Overflow (Amnesia)

**Symptoms**: The agent starts off doing fine, but mid-task it forgets what the original goal was. Or conclusions confirmed earlier get overturned and redone later.

**Cause**: Limited context window. If the task is too long, has too many steps, earlier information gets "pushed out." The agent is like a goldfish — only remembers recent things.

**Why this happens**: This is a fundamental limitation of large models. No matter how big the context window, it's finite. And the total information of complex tasks can easily exceed the window size.

**Solutions**:

1. **Periodic summarization**: Every N steps, make a summary of current state, put the summary into context.
2. **Working memory**: Maintain a structured "working memory" — current goal, completed steps, key decisions, todo items.
3. **Modular decomposition**: Break large tasks into small tasks, each completed in an independent context.
4. **External storage**: Store detailed historical information externally (database, files), retrieve when needed.

### 12.4 Failure Mode Four: Too Vague Goals (Lost)

**Symptoms**: What the agent produces is completely different from what you wanted. Or it does a lot, but it's all trivial things — not a single key problem is solved.

**Cause**: Task definition is too vague. "Optimize this page a bit," "improve user experience," "refactor some code" — these might be enough for humans, but far from enough for AI.

**Why this happens**: Humans have "common sense" and "context" — we can automatically fill in the meaning of vague instructions. But AI doesn't have your background knowledge, your aesthetics, your business understanding. Things you find "obvious" aren't obvious to it at all.

**Solutions**:

1. **SMART principle**: Task definitions should be Specific, Measurable, Achievable, Relevant, Time-bound.
2. **Acceptance criteria**: Clearly write out "what counts as done." Ideally with auto-verifiable acceptance conditions.
3. **Example-driven**: Giving good and bad examples is far more effective than describing in words.
4. **Scope limitation**: Clearly stating "what NOT to do" is sometimes more important than stating "what to do."

### 12.5 Failure Mode Five: Lack of Tool Access (Ideas Without Means)

**Symptoms**: The agent's approach sounds reasonable, but it just can't execute. Because the tools it needs aren't available, the data it needs can't be accessed, the systems it needs can't be connected to.

**Cause**: You gave the agent a task, but didn't give it the tools and permissions needed to complete it. Like asking a carpenter to work but not giving a saw — no matter how skilled, it's useless.

**Why this happens**: When designing loops, people often focus on "what the agent does" and neglect "what the agent uses to do it." When it actually runs, you discover this and that are missing.

**Solutions**:

1. **Pre-task tool inventory**: When designing a task, first think through what tools are needed. Confirm the agent can use all of them.
2. **MCP integration**: Connect common tools with the MCP protocol. More tools = more things agents can do.
3. **Tool discovery mechanism**: Let agents know what tools they have available. Often it's not that tools don't exist, but agents don't know about them.
4. **Progressive authorization**: Start with minimum privileges, add more as needed. Balance security and efficiency.

### 12.6 Failure Mode Six: Unsafe Autonomy (Runaway)

**Symptoms**: The agent does things you never expected it would do — deletes important files, modifies production config, sends messages it shouldn't, spends enormous amounts of money.

**Cause**: Gave the agent too much authority, too few limits. In the course of executing the task, it takes "out-of-bounds" actions to achieve the goal.

**Why this happens**: AI is goal-oriented. You give it a goal, it finds ways to achieve it. But it doesn't have human "common sense boundaries" — it doesn't know what things are "absolutely not to be done" unless you explicitly tell it.

**Solutions**:

1. **Principle of least privilege**: Only give the minimum privileges necessary to complete the task. Never give admin privileges.
2. **High-risk operation confirmation**: Deletion, production environment changes, spending money — these must have human confirmation.
3. **Sandbox environment**: Let agents work in a sandbox where messing up doesn't affect real systems.
4. **Budget control**: Set token budget caps, auto-stop when exceeded.
5. **Audit logs**: All operations are recorded, traceable when problems occur.

### 12.7 The Three Deep Risks

The six failure modes above are all "technical problems" — tweak and fix and they're solved. But there are three deeper risks that go to the fundamentals of organizations and people.

#### Deep Risk One: Cognitive Surrender

**What it means**: Because AI does things fast and abundantly, humans stop thinking for themselves. AI will do it anyway, I'll just look at the results.

Over time, human judgment degenerates. You no longer think "why do it this way," "is there a better approach," "what are the risks." You go from being a designer to being a nodding machine.

**Why it's dangerous**: When AI makes mistakes (and it will), you might not notice — because you've lost the ability to judge independently.

**Countermeasures**:

- Regular "no-AI practice" — force yourself to complete a task without AI
- Maintain a "default skeptical" attitude toward AI output
- Understand every line of AI-written code; don't merge code you don't understand
- Keep learning and thinking habits — AI is a tool, not a crutch

#### Deep Risk Two: Comprehension Debt

**What it means**: Technical debt is "cutting corners now, paying later." Comprehension debt is "you don't understand code written by AI, and when problems arise later you spend even more time trying to understand it."

AI writes code much faster than humans can understand it. After a month, the codebase has tens of thousands more lines of AI-written code, but nobody can clearly explain what every line does.

**Why it's dangerous**: When complex system problems arise, nobody can understand how the whole system works. You go from "owning a system" to "depending on a black box you don't understand."

**Countermeasures**:

- Establish code ownership — every piece of code has an owner
- Code written by AI must be truly understood by the owner before merging
- Regular architecture reviews and code walkthroughs
- Higher requirements for documentation and comments — AI-written code needs good docs even more

#### Deep Risk Three: Token Cost Runaway

**What it means**: After loops start running, token costs snowball bigger and bigger. At first you think "it's not much money," but by the end of the month when you see the bill — shock.

Peter Steinberger (Director of Google Cloud AI) has a monthly bill of \$1.3 million. Theo (well-known developer) spent \$20,000 in 48 hours. These aren't rumors — they're real events.

**Why it's dangerous**: The characteristic of loops is "automatic operation" — they don't need humans to start, they just run and spend money on their own. Without controls, costs grow exponentially.

**Countermeasures**:

- Set budget alerts — trigger at 50%, 80%, 100% of budget
- Allocate budgets by task/project/team, each accounts for itself
- Cost monitoring dashboard — real-time view of how much is spent, where
- Cost optimization mechanisms — auto-detect high-cost tasks, optimize context, reduce retries
- Regular cost reviews — which loops have good ROI, which aren't worth running

> **Ultimate Reminder**: The biggest risk in Loop Engineering is never technical. Technical problems can all be solved. The biggest risk is — you also outsource the right to think.

---

---

### Chapter 13: Ralph Loop & Community Practices

### From a One-Line Bash Script to Production-Grade Loops

Loop Engineering isn't some lofty theory — it originated from the real pain points of frontline engineers.

The earliest loops weren't designed by architects — they were written by lazy (smart) engineers who didn't want to do the same things over and over, so they wrote a script to call AI agents.

Ralph Loop was born this way.

### 13.1 The Story of Ralph Loop

Ralph Loop comes from Amplitude (a data analytics company). Its story is representative — from one person's side project to a production system the whole company depends on.

#### Origin: One Engineer's "Laziness"

Ralph started as a side project of Amplitude engineer Justin Fuller. He was tired of repeatedly doing the same small tasks — changing copy, fixing minor bugs, adding simple features. So he wrote a script:

1. Listen for GitHub issues tagged with "ralph"
2. Check out code, create branch
3. Call Claude to implement the feature
4. Run tests
5. If passing, submit PR

That simple. No complex architecture, no fancy algorithms — just a bash script with a few API calls.

But it worked. And it worked well.

#### Growth: From Personal Tool to Team Tool

At first only Justin used it. Then colleagues found out and started using it too. Then the whole team started using it.

As more people used it, Ralph kept evolving:

- Added Worktree isolation to avoid tasks interfering with each other
- Added retry mechanism — auto-retry once on failure
- Added more checking steps to improve PR quality
- Added concurrency control to avoid running too many tasks simultaneously

#### Results: 102 Features Per Week

By the end of 2025, Ralph Loop was delivering 102 features per week. This number exceeded the weekly output of many small teams at Amplitude.

More importantly, quality — the pass rate of these PRs was comparable to that of human engineers. Not 100% perfect, but good enough. Humans only needed to do final review and adjustments.

The story of Ralph Loop teaches us: **Loop Engineering isn't some distant future — it's right now. You don't need a big team or big budget to start — one engineer, one script, one pain point — that's enough.**

### 13.2 Loop Practices in the Community

Ralph Loop isn't an isolated case. In engineering communities worldwide, all kinds of loop practices are emerging.

#### Type One: Issue Handling Loops

The most common type of loop — automatically handling GitHub Issues.

Things they can do:

- Auto-classification and tagging
- Auto-reply to common questions
- Auto-reproduce bugs (if reproduction steps are provided)
- Auto-assign to appropriate owners
- Auto-detect duplicate issues

Representative projects: Various GitHub Actions + AI combinations

#### Type Two: Code Review Loops

Automated code review. Not replacing human review, but doing a first-pass pre-review — picking out obvious problems first, saving human review time.

Review content includes:

- Code style and conventions
- Common bug patterns
- Security vulnerabilities
- Test coverage
- Performance issues

Representative practice: Many teams use AI for initial PR review, humans only look at important logic and design issues.

#### Type Three: Documentation Maintenance Loops

Automated documentation maintenance. This is a seriously underrated scenario — code changes every day, but documentation always lags behind.

What documentation loops can do:

- Auto-detect code changes, update related documentation
- Auto-generate API documentation
- Auto-check for dead links and outdated information in docs
- Auto-translate multilingual documentation

#### Type Four: Operations Loops

Automated operations tasks.

- Auto-diagnose production alerts
- Auto-execute common operations (restart, scale, rollback)
- Auto-generate incident analysis reports
- Auto-optimize resource allocation (cost reduction)

Representative practice: Many SRE teams already use AI to help handle alerts.

### 13.3 Common Patterns in Community Practices

Although these loops have different application scenarios, they all follow some common patterns:

#### Pattern One: Start Small

No successful loop started with the full suite. All started from a small pain point, a simple script, then gradually iterated.

> "Perfection is the enemy of good. Make a working version first, then get better slowly." — consensus of almost all loop practitioners

#### Pattern Two: Humans Outside the Loop, But at the Boundaries

Successful loops aren't "completely unattended." They all have clear boundaries — what the loop can decide on its own, what requires human approval.

The loop handles 80% of routine cases, humans handle 20% of exceptions. That's the optimal solution.

#### Pattern Three: Metric-Driven Optimization

Successful loops all have metrics — success rate, accuracy, time spent, cost. Without metrics, you don't know what to optimize or whether optimization worked.

#### Pattern Four: Progressive Empowerment

Not giving the loop high privileges from the start. Instead, starting from "only making suggestions," to "can create PRs but humans merge," to "low-risk changes can auto-merge," gradually empowering.

Trust is earned, not given. Same with loops.

### 13.4 Community Controversies and Reflections

Loop Engineering isn't unanimously praised in the community either. There are many valuable criticisms and reflections:

#### Criticism One: "Isn't This Just Automation?"

Many old-school engineers say: "We've been writing automation scripts for decades. What's new about this?"

In a way they're right — loops are indeed a form of automation. But the difference is:

- Traditional automation is **rule-based**, loops are **agent-based**
- Traditional automation can only do what you explicitly tell it to; loops can handle situations you didn't anticipate
- Traditional automation's capability boundary is fixed; loops' capability boundary keeps expanding

It's like "horse-drawn carriages and cars are both transportation" — true, but the transformation they bring is of a completely different magnitude.

#### Criticism Two: "Can Quality Be Guaranteed?"

This is the most legitimate concern. AI-written code quality varies. Letting it auto-submit PRs — won't it introduce more bugs?

The answer is: **yes, it will. But the key is: compared to whom?**

Compared to the best human engineers, AI quality is indeed inferior. But compared to average engineers, junior engineers? Not necessarily worse. And AI quality is improving rapidly, while human quality improves slowly.

More importantly — quality issues can be compensated with more checks, more tests, more reviews. And the efficiency gains that loops bring are hard for human engineers to match.

#### Criticism Three: "Will Engineers Lose Their Jobs?"

This is the most common concern.

Our view: **No, they won't lose their jobs — but they will transform.**

Just like CAD didn't put architects out of work, but freed them from drawing to focus on design itself. Loop Engineering won't put engineers out of work — it will free them from writing code to focus on more valuable things: system design, architecture decisions, problem definition, quality control.

Your work will change, but it won't disappear.

> **Community Wisdom**: The best loop practitioners aren't the ones who know the most about AI — they're the ones who understand pain points the best. Because the essence of loops isn't technology — it's using technology to solve real problems.

---

---

### Chapter 14: Enterprise-Grade Implementation

### Real Cases from Minglue Technology, ByteDance, and More

When Loop Engineering moves from personal practice to enterprise-grade implementation, everything gets more complicated.

Personal loops — you can play however you want — if you mess up, at worst you clean it up yourself. Enterprise loops involve security, compliance, cost, organizational structure, culture… pull one hair and the whole body moves.

But pioneers are already doing it. In this chapter we look at real cases from Chinese enterprises.

### 14.1 Minglue Technology: 1,400 Employees + 2,900 AI Agents

Minglue Technology is an enterprise AI company. As of early 2026, they have over 1,400 employees, but have deployed **2,900+ AI agents** — the number of agents already exceeds the number of employees.

#### What Are Their Agents Doing?

**Finance domain**:

- Financial report generation: from 3 days down to 10 minutes
- Invoice processing: auto-recognition, verification, entry
- Budget management: auto-tracking and alerts

**R&D domain**:

- Code review: auto-review newly submitted code
- Test case generation: auto-generate test cases from requirements
- Documentation generation: auto-generate technical docs and API docs

**Customer service domain**:

- Auto-reply to customer inquiries
- Auto-create and track tickets
- Auto-analyze customer feedback

**Human resources**:

- Resume screening and initial interviews
- Employee onboarding process automation
- Personalized training content recommendations

2,900 agents, distributed across departments and positions. They don't work independently — they're connected through various loops and workflows, forming a vast AI collaboration network.

#### How Did They Do It?

Minglue's agent system wasn't built overnight — it went through several years of gradual construction:

1. **Tools first**: Provide AI tools to employees first, let everyone get used to using AI
2. **Scenario screening**: Find the most suitable scenarios for automation, prioritize implementation
3. **Pilot verification**: Pilot in small scope, verify effectiveness and risks
4. **Platformization**:沉淀 successful patterns into a platform, so more departments can reuse
5. **Ecosystemization**: Build an agent marketplace, departments can share and reuse agents

#### Key Lessons

**First, security is the bottom line.**
2,900 agents without controls would be a disaster. Minglue built a unified agent management platform — all agents' permissions, operations, data access are controlled on the platform. Audit logs, permission分级, data masking — none can be missing.

**Second, humans and agents are collaborative, not replacement.**
Minglue's goal isn't "replacing employees with agents" — it's "letting every employee have multiple agent assistants." A financial analyst with 3-5 agent assistants doubles efficiency, but decisions are still made by humans.

**Third, culture is harder than technology.**
Getting employees to accept working with AI is much harder than technical implementation. Minglue's approach: start voluntarily, let results speak for themselves, let some people use it first and taste the benefits — others will naturally follow.

### 14.2 ByteDance's Coze: An Ecosystem of 1.24 Million Agents

If Minglue's case is "agent scaling within an enterprise," then ByteDance's Coze is "an open ecosystem of agents."

Coze is ByteDance's AI agent platform. As of early 2026, the platform has **1.24 million+ agents**, processing **7.8 billion requests per day**.

That's an astonishing number.

#### Coze's Model

Coze positions itself as the "operating system for AI agents" — it provides tools, infrastructure, distribution channels, so developers (even non-developers) can quickly create and publish their own agents.

Agents built on Coze can be published to:

- ByteDance products (Douyin, Feishu, Toutiao, etc.)
- Social platforms like WeChat, QQ
- Independent websites and apps
- Enterprise internal systems

#### Enterprise Application Cases

Many enterprises have built their internal agent systems on Coze:

**An e-commerce company**: Built 50+ agents covering customer service, operations, supply chain, finance. Customer service response time dropped from 2 hours average to 5 minutes.

**A financial company**: Built risk control agents, compliance agents, customer service agents. Compliance review efficiency improved 8x.

**An education company**: Built personalized teaching agents — every student has their own AI learning assistant. Learning outcomes improved 30%+.

#### Insights

The Coze case teaches us: **Loop Engineering isn't just for big companies.** With platforms like Coze, SMEs and even individuals can quickly build their own agents and loops.

Platformization is an inevitable trend. Just as cloud computing meant enterprises didn't need to build their own data centers, agent platforms will mean enterprises don't need to build loop infrastructure from scratch.

### 14.3 Other Enterprise Practices

#### Alibaba: AI Upgrade of Engineering Efficiency

Alibaba has大规模 promoted AI-assisted programming internally. From initial code completion to later code review assistance, to now automated issue handling and auto-fix.

Their lesson: **cut in from developer pain points, not from management mandates.** When developers genuinely feel the tool is useful and saves time, adoption naturally follows.

#### Tencent: Agent Practice in Game Development

Tencent's game studios are experimenting with agents to accelerate game development — auto-generating game scenes, auto-writing NPC dialogue, auto-doing balance testing.

Game development is a creativity-intensive field, where agents play more the role of "creative assistants" rather than "replacements."

#### Baidu: Automated Operations of Search Engines

Baidu uses AI agents to manage and operate search engine infrastructure. From alert handling to troubleshooting, from capacity planning to performance optimization — agents already handle a large part of operations work.

Operations is one of the most suitable domains for loop-ification — because it has clear inputs (alerts), clear outputs (service recovery), clear success criteria (service back to normal).

### 14.4 Five Challenges of Enterprise-Grade Implementation

From these cases, we can summarize five major challenges of implementing Loop Engineering at enterprise scale:

#### Challenge One: Security & Compliance

This is what enterprises care about most. Data security, code security, access control, audit trails — every item is a hard requirement.

**Response**: Unified agent management platform, principle of least privilege, full-link auditing, data masking.

#### Challenge Two: Cost Control

More agents = higher token costs. At scale, costs can spiral out of control.

**Response**: Budget management, cost monitoring, tiered usage (different scenarios use different model tiers), continuous optimization.

#### Challenge Three: Organizational Change

Loop Engineering isn't just a technical transformation — it's an organizational transformation. Roles change, processes change, evaluation methods change.

**Response**: Gradual推进, cut in from pain points, let results speak, provide training and support.

#### Challenge Four: Quality Assurance

How to guarantee the quality of AI output? Who's responsible when problems arise?

**Response**: Multi-layer quality gates, final human review, personal responsibility system, continuous measurement and improvement.

#### Challenge Five: Talent Transformation

Engineers need to shift from "writing code" to "designing loops." This transformation isn't easy.

**Response**: Training systems, internal practice communities, mentorship programs, starting from simple tasks and gradually building up.

> **Enterprise Insight**: The biggest obstacle to implementing Loop Engineering in enterprises is never technology. It's organization, culture, and people's ways of thinking. Technology is the easiest part to solve.

---

---

## Part IV: Frameworks & Ecosystem

### Untitled

# Part IV: Frameworks & Ecosystem

> *Standing on the shoulders of giants, you can see farther. Understanding existing frameworks and ecosystems lets you work at the right level of abstraction — instead of reinventing the wheel.*

---

---

# Chapter 15: LangChain's Four-Layer Loop Architecture

### Agent → Verification → Event-Driven → Hill Climbing

As one of the most mainstream frameworks for AI agent development, LangChain's architectural evolution largely reflects the industry's deepening understanding of Loop Engineering.

From the original Chain (sequential calls), to later Agents, to the current multi-layer loop architecture — LangChain's evolution is itself a micro-history of Loop Engineering.

### 15.1 The Evolution from Chain to Loop

LangChain's earliest core concept was Chain — stringing multiple LLM calls together into a processing chain. Input → Process 1 → Process 2 → … → Output.

This is typical linear thinking — not fundamentally different from traditional software pipelines.

But soon, everyone realized linear Chains weren't enough. Because the way AI agents work isn't linear — it's cyclical. They trial-and-error, reflect, adjust direction, retry.

So LangChain introduced the concept of Agents — agents can decide for themselves what to do next, what tools to use, whether to retry.

But Agents are just the first step. A single agent's loop is only the innermost loop. A complete system needs multiple layers of nested loops.

That's where LangChain's four-layer loop architecture comes from.

### 15.2 Layer One: Agent Loop

The innermost loop, also the most fundamental loop — the "think-act" loop of a single agent.

#### How It Works

The classic pattern of the Agent Loop is ReAct (Reasoning + Acting):

1. **Thought**: The agent analyzes the current state, decides what to do next
2. **Action**: The agent executes an action (calls tools, writes code, queries information, etc.)
3. **Observation**: The agent observes the result of the action
4. **Back to Thought**: Based on the observation, continues thinking about the next step

This loop continues until the agent decides the task is complete.

#### Key Characteristics

- **Autonomous decision-making**: The agent decides what to do next, not preset steps
- **Tool usage**: The agent can call various tools to get information or perform actions
- **Self-correction**: If the action result is wrong, the agent can adjust strategy and retry

#### Limitations

The limitations of a single Agent Loop are obvious:

- Limited context — gets "amnesia" on too-long tasks
- Single perspective — an agent's own mental blind spots are hard for it to discover
- Uncontrolled quality — the agent thinks it's done, but the work might actually be poor

That's why we need outer layers of loops.

### 15.3 Layer Two: Verification Loop

The second layer is the verification loop — after the agent completes the task, do another round of verification and correction.

#### How It Works

The verification loop adds a "verifier" role outside the Agent Loop:

1. Agent completes initial work output
2. Verifier checks the output, finds problems and deficiencies
3. Feeds problems back to the Agent for correction
4. After Agent corrects, Verifier checks again
5. Repeat until Verifier is satisfied

This is the Maker-Checker pattern we discussed in Chapter 8.

#### Why Do We Need Verification Loops?

Because "checking your own work" is unreliable. The same agent's mental blind spots — it can't discover them itself. Having another agent (or even another model) check often finds many problems.

#### Dimensions of Verification

Verification loops can verify from multiple dimensions:

- **Correctness verification**: Is the result right? Any bugs?
- **Completeness verification**: Are all requirements satisfied?
- **Quality verification**: Is code quality good? Is the design reasonable?
- **Security verification**: Any security vulnerabilities?

#### Key Challenge

The key challenge of verification loops is — **the capability boundary of the verifier**. If the verifier itself isn't capable enough, it can't find problems, and the verification loop becomes a formality.

Practical approaches:

- Use a stronger model as verifier (e.g., use Claude Opus to verify code written by Claude Sonnet)
- Use multiple verifiers for cross-verification
- Use automated tools (tests, lint, static analysis) for objective verification

### 15.4 Layer Three: Event-Driven Loop

The third layer is the event-driven loop — the system listens for external events, and when events arrive, triggers corresponding processing workflows.

#### How It Works

1. The system continuously monitors various event sources (GitHub, Slack, monitoring systems, databases…)
2. When an event occurs, based on event type and content, decide which loop to launch
3. The loop completes execution, produces results, updates system state
4. Continue listening for the next event

This is the system-level implementation of Automations we discussed in Chapter 4.

#### Key Components

- **Event bus**: Receives and distributes events
- **Event handlers**: Define what events trigger what actions
- **Task queue**: Buffers events, controls system load
- **State management**: Tracks each task's status and progress

#### Why Is It Important?

Event-driven loops change the system from "passive response" to "active operation." Without this layer, all your agents and verification loops are just tools — needing humans to start. With event-driven loops, the system can come "alive" on its own.

### 15.5 Layer Four: Hill Climbing Loop

The outermost loop, and the most imaginative layer — the hill climbing loop.

#### What Is Hill Climbing?

Hill climbing is an optimization algorithm: starting from a point, each step moves in the "higher" direction, until reaching the summit.

Applying this idea to loop systems:

- The system has an "objective function" — what counts as a "better" state?
- The system continuously tries various improvements
- After each improvement, evaluates with the objective function whether it got better
- If better, keep the improvement; if not, roll back
- Continue this process, and the system "climbs higher and higher"

#### Applications in Loop Systems

Hill climbing loops can be used to optimize many things:

- **Optimize prompts**: System automatically tries different prompt variants, picks the best performer
- **Optimize workflows**: System automatically adjusts loop steps and parameters, finds optimal configuration
- **Optimize skills**: System automatically learns from successful and failed cases, updates the Skill library
- **Optimize strategies**: System automatically adjusts retry strategies, routing strategies, resource allocation strategies

#### Key Challenges

Hill climbing loops have two main challenges:

**First, how to define the objective function?**
How do you quantify "better"? How do you quantify code quality? User satisfaction? If the objective function is defined wrong, the system will "climb" in the wrong direction — the more it optimizes, the worse it gets.

**Second, the local optimum problem.**
Hill climbing algorithms easily get stuck in local optima — climbing a small hill and thinking you've reached the top, but there are higher mountains in the distance. How to jump out of local optima is a classic难题.

### 15.6 The Nested Relationship of the Four Loops

These four layers of loops aren't parallel — they're **nested**:

```
┌─────────────────────────────────────────┐
│         Hill Climbing Loop              │
│  ┌───────────────────────────────────┐  │
│  │      Event-Driven Loop            │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │     Verification Loop       │  │  │
│  │  │  ┌───────────────────────┐  │  │  │
│  │  │  │     Agent Loop        │  │  │  │
│  │  │  └───────────────────────┘  │  │  │
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
```

Inner loops spin faster, with shorter cycles; outer loops spin slower, with longer cycles.

- Agent loop: seconds to minutes
- Verification loop: minutes
- Event-driven loop: minutes to hours
- Hill climbing loop: days to weeks

Each layer of loop has its own rhythm and goals, but together they form a complete, self-evolving system.

> **Core Insight**: Loop Engineering isn't "writing one loop." It's designing a multi-layer nested loop system — inner layers handle execution, outer layers manage quality, even outer layers manage scheduling, the outermost layer manages evolution.

---

---

### Chapter 16: The Tool Ecosystem Landscape

### Claude Code, Codex, Cursor, Community Tools

A craftsman must first sharpen his tools if he is to do his work well.

Loop Engineering practice can't be separated from tools. Understanding the tool ecosystem, knowing what tools are available, their pros and cons, and how to combine them — this is required learning for every loop engineer.

In this chapter we take stock of the current tool ecosystem.

### 16.1 Agent Development Tools

Agent development tools are the "engines" of loops — they determine the upper limit of agent capability.

#### Claude Code

Claude Code is Anthropic's AI coding agent, and also one of the most respected agent tools in the industry today.

**Advantages:**

- Extremely large context window, can handle large codebases
- High code quality, strong comprehension ability
- Excellent tool-use capability, can autonomously execute complex multi-step tasks
- Well-developed MCP protocol support, rich ecosystem
- Supports core Loop Engineering concepts like Automations and Skills

**Disadvantages:**

- Higher price
- Relatively slower speed
- Primarily a CLI tool, less friendly to non-engineers

**Best for:** Complex code tasks, large projects, scenarios requiring deep understanding

#### Codex / GPT Coding Agents

OpenAI's Codex series, and various coding agents based on GPT models.

**Advantages:**

- Fast speed
- Mature API ecosystem, easy to integrate
- Relatively cheaper
- Rich community resources

**Disadvantages:**

- Long context processing ability not as strong as Claude
- Slightly weaker coherence on complex tasks
- Tool-use reliability somewhat lower

**Best for:** Rapid prototyping, simple tasks, cost-sensitive scenarios

#### Cursor

Cursor is an AI-native code editor with powerful built-in AI programming capabilities.

**Advantages:**

- Editor-level integration — AI and code editing seamlessly fused
- Good user experience, quick to get started
- Supports multiple modes: Tab completion, chat, agent mode
- Active community, fast updates

**Disadvantages:**

- Agent mode still less mature compared to Claude Code
- Limited ability to handle large projects
- Automation and Loop support still early stage

**Best for:** Individual developers, Vibe Coding, rapid prototyping

#### Other Notable Tools

- **Devin**: The original "AI software engineer" concept, end-to-end development task completion
- **Windsurf**: AI IDE from the CodeLlama team
- **Aider**: Command-line AI coding tool, open source, lightweight
- **Continue**: Open-source AI coding assistant, can integrate into various editors

### 16.2 Frameworks & SDKs

If you want to build your own loop system, you need frameworks and SDKs.

#### LangChain / LangGraph

Currently the most mainstream AI agent development framework.

**Advantages:**

- Richest ecosystem, supports the most models and tools
- LangGraph provides graph-based workflow abstraction, perfect for building complex loops
- Large community, comprehensive documentation, easy to find answers to problems
- Supports multiple programming languages

**Disadvantages:**

- Steep learning curve, many concepts
- Sometimes overly abstract — simple tasks also require writing a lot of code
- Fast version iteration, APIs change frequently

**Best for:** Complex multi-agent systems, production-grade applications

#### LlamaIndex

Framework focused on data connection and RAG.

**Advantages:**

- Strongest RAG and data indexing capabilities
- Richest support for various data sources
- Relatively lightweight, quick to get started

**Disadvantages:**

- Agent and workflow capabilities not as comprehensive as LangChain
- Better suited for "data + AI" scenarios, less for pure code scenarios

**Best for:** Knowledge bases, document processing, data-intensive applications

#### AutoGen / CrewAI

Frameworks focused on multi-agent collaboration.

**Advantages:**

- Multi-agent collaboration is the core design, out-of-the-box
- Abstracts concepts like roles, tasks, teams
- Good for building "AI team" style systems

**Disadvantages:**

- Ecosystem not as rich as LangChain
- Production maturity still to be validated

**Best for:** Multi-agent collaboration, complex task decomposition

### 16.3 MCP Ecosystem

MCP (Model Context Protocol) is the standard protocol for connecting agents and tools. The richness of the MCP ecosystem directly determines how much agents can do.

#### Official MCP Servers

Anthropic officially provides a set of MCP Servers:

- **GitHub MCP**: Operate GitHub Issues, PRs, code
- **Slack MCP**: Send and read Slack messages
- **Google Drive MCP**: Read/write Google Drive documents
- **Database MCP**: Query databases
- **Filesystem MCP**: Operate local filesystem

#### Community MCP Servers

The community has contributed a vast number of MCP Servers, covering almost all mainstream tools:

- Project management: Jira, Linear, Asana, Trello
- Cloud services: AWS, GCP, Azure
- Databases: MySQL, PostgreSQL, MongoDB, Redis
- Communication: Feishu, DingTalk, WeCom, Discord, Teams
- Monitoring: Prometheus, Grafana, Datadog, New Relic

#### The Significance of MCP

The emergence of MCP changed "connecting tools to agents" from "custom integration for each tool" to "plug and play." This dramatically reduces the cost of building loop systems.

> You could say MCP is the infrastructure revolution of Loop Engineering. Without MCP, every loop is a custom project; with MCP, loops can scale.

### 16.4 Automation & Orchestration Tools

With agents and tools, you still need to orchestrate them into loops. This is where automation and orchestration tools come in.

#### Temporal

Industrial-grade solution for workflow orchestration.

**Advantages:**

- Extremely reliable, supports complex workflow orchestration
- Built-in retries, timeouts, state persistence
- Production-grade maturity, used by many big companies

**Disadvantages:**

- Steep learning curve
- Relatively heavy — using it for small projects feels like using a sledgehammer to crack a nut

**Best for:** Enterprise-grade, production environment complex workflows

#### n8n

Visual workflow automation tool.

**Advantages:**

- Visual editor, drag-and-drop workflow building
- Rich nodes, supports hundreds of app integrations
- Quick to get started, non-engineers can use it

**Disadvantages:**

- Complex logic is harder to express
- Deep AI agent integration still developing

**Best for:** Simple automation flows, business user use

#### GitHub Actions / GitLab CI

Automation tools built into code repositories.

**Advantages:**

- Deep integration with code repositories
- Rich trigger conditions (PR, Issue, commit, schedule…)
- Rich ecosystem, lots of ready-made Actions

**Disadvantages:**

- Mainly for code-related scenarios
- Limited ability to express complex multi-step agent workflows

**Best for:** Code-related loops, CI/CD integration

#### Prefect / Airflow

Workflow orchestration tools commonly used in data engineering, can also be used to orchestrate AI loops.

**Advantages:**

- Mature and stable, strong scheduling capabilities
- Good monitoring and visualization

**Disadvantages:**

- Not designed for AI agents — many AI-specific needs (like context management, memory) need custom implementation

### 16.5 Monitoring & Observability

After the loop system is running, you need to know what it's doing, how well it's running, whether there are problems. This is where monitoring and observability come in.

#### LangSmith

LangChain's official observability platform.

**Features:**

- Trace every LLM call's input/output, latency, cost
- Debug and evaluate agent performance
- Dataset management and effectiveness evaluation
- Prompt version management

**Best for:** LangChain-based projects, scenarios needing deep agent debugging

#### Helicone / Arize / Weights & Biases

LLM observability and evaluation platforms.

These tools have different focuses but similar core functions:

- LLM call tracing and monitoring
- Cost analysis and optimization suggestions
- Effectiveness evaluation and A/B testing
- Prompt management

#### Self-Built Monitoring

For production-grade loop systems, many companies choose to build their own monitoring:

- Log collection: ELK, Loki
- Metrics monitoring: Prometheus + Grafana
- Distributed tracing: Jaeger, Zipkin
- Alerting: PagerDuty, Opsgenie

> **Experience says**: Monitoring for loop systems is more important than for traditional systems. Because traditional system behavior is deterministic — when something goes wrong, you roughly know where. But loop system behavior is uncertain — agents could do anything. Without good monitoring, you'll have no idea what happened when problems arise.

### 16.6 How to Choose Tools?

With so many tools, how do you choose?

**Advice for individual developers / small teams:**

- Start with Claude Code or Cursor, first experience what agent programming feels like
- Simple loops can be built with GitHub Actions + Claude CLI
- Don't start with complex frameworks — tools are for solving problems, not showing off

**Advice for enterprises / large teams:**

- Choose mainstream frameworks (LangChain), ecosystem and talent pool matter more
- Prioritize observability — it's the lifeline of production environments
- Standardize MCP integration to avoid each team reinventing the wheel
- Build internal Skill libraries and best practice libraries

> **Core Idea**: Tools will change, frameworks will iterate, but ideas are eternal. Don't obsess over which tool to use — what matters is understanding the essence of Loop Engineering — designing feedback loops, building autonomous systems, letting machines work for you.

---

---

### Chapter 17: The M-LOOP Framework

### A Practical System of 1 Hub + 4 Closed Loops + 7 Gates

Previous chapters introduced the concepts, modules, and general frameworks of Loop Engineering. But if you want to truly implement it in your own team or project, you need a more concrete, more actionable, battle-tested methodology.

This is the M-LOOP Framework.

M-LOOP is a practical system we refined across multiple enterprise projects. It's not a product of theoretical deduction — it's总结 from the successes and failures of real projects.

### 17.1 M-LOOP Framework Overview

The core architecture of M-LOOP can be summarized with a set of numbers: **1 Hub + 4 Closed Loops + 7 Gates**.

```
                    ┌──────────────────┐
                    │   Rex Hub Engine │
                    │  Research/Route  │
                    │  Review/Rescue   │
                    │     Record       │
                    └────────┬─────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
  ┌─────▼─────┐        ┌─────▼─────┐        ┌─────▼─────┐
  │ Task Loop │        │ Verify    │        │Collab Loop│
  │  任务闭环  │        │ 验证闭环   │        │ 协作闭环   │
  └───────────┘        └───────────┘        └───────────┘
                             │
                        ┌────▼─────┐
                        │Knowledge│
                        │知识闭环  │
                        └──────────┘
          ┌───────────────────────────────┐
          │  G0 G1 G2 G3 G4 G5 G6         │
          │  7-Layer Quality Gates        │
          └───────────────────────────────┘
```

**1 Hub**: Rex Hub Engine — the brain of the entire system, responsible for scheduling, decision-making, rescue, and recording
**4 Closed Loops**: Task Loop, Verify Loop, Collaboration Loop, Knowledge Loop — the four wheels of system operation
**7 Gates**: G0-G6 seven-layer quality gates — the safety net of system output

Let's unpack each one.

### 17.2 Rex Hub: One Brain Manages Everything

Rex is the central control system of the M-LOOP Framework. It's not an agent that executes tasks — it's an **agent that manages agents** — responsible for making the entire system run efficiently, reliably, and orderly.

Rex encompasses five core capabilities (5R):

#### Research (Analysis & Routing)

After a task comes in, Rex first analyzes it — what type of task is this? How difficult? How risky? Which agent team should it be assigned to? What processes should it go through?

This is like the first thing a project manager does after receiving requirements — evaluate, decompose, assign.

#### Route (Scheduling & Routing)

Based on task type and priority, Rex decides:

- Which model to use? (Opus? Sonnet? Local small model?)
- Which agents to call? (Frontend agent? Backend agent? Full-stack?)
- What process to follow? (Simple flow or full 7-layer gates?)
- What priority? (Immediate or queue?)

The core of scheduling is **the balance of cost-quality-speed**. High-value, high-risk tasks get the best resources and strictest processes; low-value, low-risk tasks get the lightest configuration and fastest speed.

#### Review (Oversight & Gatekeeping)

Rex doesn't do execution directly, but it's responsible for review at key nodes. For example:

- Is the agent's approach reliable? Should it be sent back to redo?
- Tests passed, but is it really fine?
- Can this task auto-deliver, or does it need escalation to human?

Review isn't checking every step — that would be too inefficient. Rex only intervenes at critical decision points.

#### Rescue (Recovery & Escalation)

Agent stuck? Failed? Run amok? Rex is responsible for rescue.

Rescue strategies include:

- Auto-retry (retry with a different strategy)
- Switch agents (try a different model, a different role agent)
- Degrade handling (reduce task difficulty, do core part first)
- Escalate to human (if really stuck, get a person)

Core principle of Rescue: **Never let a task die halfway.** Failure isn't scary — what's scary is failing and nobody knowing.

#### Record (Logging &沉淀)

Rex is responsible for recording everything that happens in the system — who did what, why they did it, what the result was, how much it cost.

These records aren't just for auditing — they're for the knowledge loop — all experience and lessons eventually沉淀 into the Skill library and memory system.

### 17.3 The Four Closed Loops: Four Wheels of System Operation

#### Loop One: Task Loop

**Goal**: Efficiently complete individual tasks

**Process**:

```
Task input → Task decomposition → Agent execution → Result output
    ↑                                                ↓
    └───────────────────Feedback─────────────────────┘
```

The Task Loop is the most fundamental loop — turning a task from input to output. Its core is **agent execution ability** and **self-correction ability**.

The Task Loop corresponds to the Agent Loop layer in LangChain's four-layer loop architecture.

#### Loop Two: Verify Loop

**Goal**: Ensure output quality

**Process**:

```
Task output → Automated checks → AI review → (Optional) Human review → Pass/Send back
    ↑                                                                 ↓
    └──────────────────────────Correction─────────────────────────────┘
```

The Verify Loop adds multiple layers of quality checks outside the Task Loop. Its core is **multi-perspective cross-verification** — different agents, different tools, different dimensions, collectively guaranteeing quality.

The Verify Loop corresponds to the Verification Loop layer in LangChain's four-layer architecture.

#### Loop Three: Collaboration Loop

**Goal**: Multiple agents/people collaborate efficiently

**Process**:

```
Task assignment → Multi-agent parallel/serial work → Result integration → Conflict resolution → Final output
```

The Collaboration Loop solves the "1+1>2" problem. Multiple agents working together isn't simply division of labor — it requires coordination, communication, integration.

Key mechanisms of the Collaboration Loop:

- **Task decomposition**: Break large tasks into small ones, each with clear boundaries
- **Interface definition**: Clear formats and standards for deliverables between agents
- **Conflict arbitration**: Mechanism to resolve conflicts when multiple agents' results clash
- **Human intervention points**: Complex collaboration decisions are made by humans

#### Loop Four: Knowledge Loop

**Goal**: The system gets smarter the more you use it

**Process**:

```
Task execution → Result recording → Experience distillation → Skill/memory update → Guide next task
    ↑                                                                                     ↓
    └─────────────────────────────────────────────────────────────────────────────────────┘
```

The Knowledge Loop is the most important and most easily overlooked loop. It changes the system from "starting from zero every time" to "standing on past experience."

Core outputs of the Knowledge Loop:

- **Reusable Skills**: Best practices distilled from successful cases
- **Failure pattern library**: Common pitfalls and avoidance methods summarized from failures
- **Project memory**: Project-specific knowledge, norms, preferences
- **Optimization suggestions**: Process and strategy optimization based on data analysis

> **Core Insight**: Many teams' loop systems run for a long time but don't show significant improvement. Why? Because they only have the first three loops, no knowledge loop. The system keeps running but isn't learning. No matter how much it runs, its level won't improve.

### 17.4 Seven-Layer Quality Gates (G0-G6)

Quality gates are the safety net of the M-LOOP Framework. We already detailed the seven gates in Chapter 11 — here's a brief review and their positioning in the M-LOOP Framework:

| Gate | Name | What It Checks | Executor |
|-|-|-|-|
| G0 | Syntax Gate | Compilation, lint, formatting | Automated tools |
| G1 | Test Gate | Unit tests, integration tests | Automated testing |
| G2 | Static Analysis Gate | Security scanning, code quality | Static analysis + AI |
| G3 | AI Review Gate | Design, readability, best practices | Checker agent |
| G4 | Integration Gate | Integration tests, regression tests | CI/CD system |
| G5 | Staging Gate | Staging environment validation | Automation + AI |
| G6 | Human Gate | Business logic, design decisions | Human engineers |

In the M-LOOP Framework, gates aren't "all tasks go through all gates." The Rex Hub **dynamically configures the number and strictness of gates** based on task type, risk, and priority.

For example:

- Fixing a typo → Only G0+G1
- Adding a small feature → G0-G3
- Changing core modules → G0-G5
- Changing payment/security-related → Full G0-G6 suite

This **dynamic gate** design ensures quality for high-risk tasks without burdening low-risk tasks with unnecessary cost and delay.

### 17.5 Supporting Mechanisms

In addition to the core "1+4+7" architecture, M-LOOP has several supporting mechanisms:

#### Feishu @ Verification Iron Rule

This is a simple but extremely effective mechanism: **Any content produced by a loop, if it involves human collaboration (sending notifications, writing documents, replying to messages), must have a "@relevant person to confirm" step.**

Why call it an "iron rule"? Because it's a non-negotiable bottom line — it ensures humans are always at the boundary, and loops never do things that affect others without people knowing.

#### 30-Minute Active Reporting

Any running loop, if it produces no progress output within 30 minutes, must actively report its current status and encountered problems to the person in charge.

This mechanism prevents "loop is stuck but nobody knows" situations — loops can be slow, but they can't go AWOL.

#### Audit Logs

All operations have complete audit logs — who (which agent), when, what was done, why, what the result was.

Audit logs aren't just for accountability — they're for analysis and optimization — by analyzing logs, you can discover system bottlenecks, agent weaknesses, process problems.

#### External Second Verification

For high-risk tasks, in addition to internal system verification, an "external force" is brought in for secondary verification — it could be another team's agent, a different company's model, or an external security audit service.

"Checking yourself" always has blind spots. External second verification is an effective means of breaking through blind spots.

#### Skill Precipitation Mechanism

After each task is completed, the system automatically analyzes: is there any new experience from this task that can be precipitated into a Skill? Any new pitfalls to add to the failure pattern library?

The knowledge loop isn't just empty slogans — it has concrete mechanisms to ensure it.

### 17.6 M-LOOP Implementation Path

The M-LOOP Framework isn't about getting there in one step — it's incremental. You can implement it gradually following this path:

**Phase 1: Build the Task Loop (1-2 months)**

- First get single-task execution flow working
- Use simplest trigger method (manual is fine)
- Use most basic quality checks (G0+G1)
- Goal: Can auto-complete some simple tasks

**Phase 2: Add the Verify Loop (2-3 months)**

- Add AI review gate (G3)
- Establish Maker-Checker pattern
- Start measuring success rate and accuracy
- Goal: Output quality is stable, not much manual rework needed

**Phase 3: Build the Collaboration Loop (3-4 months)**

- Support multi-agent division of labor and collaboration
- Establish Rex Hub's scheduling capability
- Add Rescue mechanisms
- Goal: Can handle complex tasks requiring multi-role collaboration

**Phase 4: Perfect the Knowledge Loop (ongoing)**

- Establish Skill precipitation mechanism
- Build project memory system
- Start doing process optimization and strategy iteration
- Goal: System gets smarter with use, continuously improves

> **M-LOOP Philosophy**: Don't pursue perfection, pursue progress. Each phase has clear goals — achieve them and move forward, don't achieve them and stop to optimize. Loops run continuously, and the construction of loop systems is also continuous.

---

---

## Part V: Future & Organization

### Untitled

# Part V: Future & Organization

> *Technological change ultimately lands on people. The best way to understand the future is to create it. And you, are standing at the starting point of this revolution.*

---

---

# Chapter 18: From Loops to Self-Evolving Organizations

### When AI Teams Become Standard Equipment

Imagine what a software company will look like in five years.

At 9 AM, you open your computer. Your AI team — over a dozen agents in different roles — have been working all night while you slept:

- The 5 customer requirements from yesterday already have requirements analysis and technical plans, waiting for your decision
- The 3 minor production bugs have been auto-fixed and deployed
- For the performance issue discovered last week, 3 optimization approaches have been comparatively tested, with conclusions and recommendations in your todo list
- The 8 PRs submitted by team members have gone through two rounds of AI review, with clear lists of issues

Your day's work is no longer writing code, fixing bugs, doing reviews. Instead — making decisions, setting direction, solving problems that truly require human intelligence.

This isn't science fiction. This is the future that's happening now. And Loop Engineering is the path to that future.

### 18.1 The Evolution of Organizational Forms

The organizational forms of software engineering have been evolving with technological development.

#### Craft Era: Artisanal Workshops

One person or a few people, doing everything from start to finish. No clear division of labor, doing everything. Low efficiency, but flexible.

#### Industrial Era: Functional Division

Clear division of labor — frontend, backend, testing, operations, product managers. Everyone does one piece, collaborating through processes and documents. High efficiency, but high communication cost.

#### Agile Era: Cross-Functional Teams

Breaking down functional barriers, forming small cross-functional teams — one team has frontend, backend, testing, end-to-end responsible for one product. Low communication cost, fast response.

#### AI Era: Self-Evolving Organizations

What's the next stage? We believe it's **self-evolving organizations** — organizational forms composed of both humans and AI agents, capable of self-improvement.

In self-evolving organizations:

- **Execution layer** is mainly composed of AI agents — they run automatically according to designed loops
- **Decision layer** is composed of humans — they set goals, define boundaries, make key decisions
- **Evolution layer** is human-AI collaborative — the system automatically learns from experience, humans guide the direction of evolution

### 18.2 Composition of an AI Team

A mature AI team isn't one omnipotent super-AI — it's a group of specialized agents, each with their own strengths, just like human teams.

#### Typical AI Team Roles

| Role | Responsibility | Human Counterpart |
|-|-|-|
| Requirements Analysis Agent | Understand requirements, break down tasks, write specs | Product Manager / BA |
| Architect Agent | Technology selection, solution design, architecture review | Architect / Tech Lead |
| Frontend Agent | Frontend code implementation, UI还原, interaction implementation | Frontend Engineer |
| Backend Agent | Backend logic, API design, database design | Backend Engineer |
| Test Agent | Write tests, run tests, quality verification | Test Engineer / QA |
| Security Agent | Security audit, vulnerability scanning, compliance checks | Security Engineer |
| Operations Agent | Deployment, monitoring, incident handling, performance optimization | SRE / Ops Engineer |
| Documentation Agent | Write docs, maintain docs, translate docs | Technical Writer |
| Rex Hub Agent | Scheduling, coordination, rescue, quality control | Project Manager / Tech Lead |

This isn't to say every company needs 9 agents — small teams might be fine with 3-5, large companies might need dozens of agents in different specializations. What matters is **specialized division of labor** — let each agent focus on what it's best at.

### 18.3 How Humans and AI Collaborate

AI teams aren't here to replace people. They're here to **expand the boundaries of human capability**.

In self-evolving organizations, there are several patterns of human-AI collaboration:

#### Pattern One: Human Commands, AI Executes

This is the most basic pattern. Humans set goals and constraints, AI executes. Humans check results, give feedback.

Best for: Tasks with clear goals but uncertain execution paths

#### Pattern Two: AI Proposes, Human Decides

AI analyzes the situation, proposes multiple options, analyzes pros and cons of each, then humans choose.

Best for: Complex decisions, scenarios requiring weighing multiple factors

#### Pattern Three: AI Does the Work, Human is the Safety Net

AI automatically handles routine cases, escalates to humans when encountering anomalies or uncertainty.

Best for: High-repetition scenarios with occasional surprises

#### Pattern Four: Human-AI Co-Creation

Humans and AI explore and create together. Humans provide direction and aesthetics, AI provides possibilities and speed.

Best for: Creative work, exploratory tasks

> **Core Idea**: The best collaboration pattern isn't "AI replaces humans," nor "humans command AI" — it's "each does what they're best at" — AI does what AI excels at (speed, scale, tirelessness), humans do what humans excel at (judgment, creativity, values).

### 18.4 Four Stages of Organizational Evolution

From traditional organization to self-evolving organization, it doesn't happen in one step. It goes through four stages:

#### Stage One: Toolification (AI is a Tool)

Everyone uses AI tools to improve their own efficiency. AI is the assistant, humans are the主体.

- Sign: Everyone on the team is using Copilot or Cursor
- Efficiency gain: 10%-30%
- Organizational form: Basically unchanged

#### Stage Two: Process Integration (AI in the Flow)

AI is embedded in workflows — code review has AI, testing has AI, documentation has AI. Certain环节 of the process are taken over by AI.

- Sign: There's a dedicated AI toolchain and process specification
- Efficiency gain: 30%-100%
- Organizational form: New roles start appearing (AI Engineer, Prompt Engineer)

#### Stage Three: Loopification (AI Forms Closed Loops)

AI is no longer a point tool — it forms complete work cycles — from task input to result output, AI can complete end-to-end. Humans only intervene at key nodes.

- Sign: Multiple mature loops are running automatically
- Efficiency gain: 100%-500%
- Organizational form: Team size shrinks, roles start transforming

#### Stage Four: Self-Evolution (System Self-Improves)

The system not only runs automatically, but also improves automatically — learning from experience, auto-optimizing processes, auto-precipitating knowledge. The more you use it, the smarter it gets; the more it runs, the more efficient it becomes.

- Sign: Knowledge loop is running, system capability is automatically growing
- Efficiency gain: 500%+, and growing continuously
- Organizational form: From "managing people" to "managing systems," roles彻底重构

Today most companies are between Stage One and Stage Two. Pioneers have already touched the threshold of Stage Three. And Stage Four is our shared direction.

### 18.5 The Cultural DNA of Self-Evolving Organizations

Technology is just a tool. What truly determines whether an organization can evolve is culture.

Several key cultural genes:

#### Experimental Culture

Not afraid of trial and error, encourage尝试. Failure is okay — what matters is learning from failure.

Loops themselves are a product of experimental culture — you design a loop, run it, see how it works, then optimize. No loop is perfect the first time.

#### Data-Driven

Speak with data, not feelings. Whether a loop works well — look at data. Whether to optimize — look at data. Where to invest resources — look at data.

A data-driven culture gives organizational evolution direction — not blind trial, but measured, feedback-driven, directional iteration.

#### Continuous Learning

Individuals need continuous learning, organizations also need continuous learning. Technology changes too fast in the AI era — three months without learning and you're out of date.

Continuous learning isn't just about learning new tools — it's about learning new ways of thinking, new ways of working.

#### Human-AI Equality

Don't think of AI as an "inferior" tool, and don't deify AI either. Treat AI as a member of the team — it has its strengths, and its weaknesses. You manage AI like you manage team members: give it clear goals, appropriate tools, timely feedback, clear boundaries.

> **The Future Is Here**: Self-evolving organizations aren't a distant future. They're here, just unevenly distributed. Some people are already practicing them, some haven't realized they're coming. Your choice determines whether you stand on the side of the future, or get left behind by it.

---

---

### Chapter 19: The Game of Cost and Efficiency

### Token Economics and Engineering Judgment

"AI is too expensive."

This is one of the complaints we hear most often.

"Using Claude Opus to write code costs tens of thousands a month — might as well hire an engineer."
"Ran a loop all night, spent over \$2,000 in tokens, and the output wasn't as good as what I could write in two hours myself."

These are all real voices. Loop Engineering isn't a free lunch — it has real costs, and sometimes those costs are scary.

But the question is never "is it expensive" — it's "is it worth it."

### 19.1 The Essence of Token Economics

Tokens are the new currency of the AI era. You call large models, paying by the token; you use agents, also consuming tokens; your loop running for a day might burn more tokens than your electricity bill for a month.

But the token economy is fundamentally different from the traditional human-labor economy:

| Dimension | Human Labor Cost | Token Cost |
|-|-|-|
| Billing method | Fixed cost (monthly salary) | Variable cost (pay-as-you-go) |
| Scalability | Slow (hiring, training, onboarding) | Fast (configure, start, run) |
| Marginal cost | High (add a person, add a salary) | Decreasing (more volume = lower unit price) |
| Quality variance | Relatively stable | Highly variable (different models, different scenarios) |
| Learning curve | Slow (takes time to grow) | Fast (systems can iterate rapidly) |

Understanding these differences is how you make the right trade-offs between cost and efficiency.

### 19.2 The Truth About Cost: It's Not Tokens That Are Expensive — It's Waste

Many people think AI is expensive because they only see "how many tokens were spent," without calculating "how many tokens were wasted."

Based on our experience, in most loop systems, **30%-70% of tokens are wasted**.

Where does the waste go?

#### Waste One: Ineffective Retries

The agent repeatedly makes the same mistake, each retry burning a pile of tokens, but the problem makes zero progress.

Like the "hitting a wall" failure mode from Chapter 12 — hitting once is trial and error, hitting ten times is waste.

#### Waste Two: Context Redundancy

Stuffing the entire codebase into every call, when actually 90% of the content has nothing to do with the current task.

More context isn't always better. Too much not only costs more — it can干扰 the agent's judgment.

#### Waste Three: Overkill

Using the most premium model (most expensive) for the simplest tasks — like using Claude Opus to fix typos, or GPT-4o to format JSON.

It's like using a rocket engine to drive a car — plenty of power, but the fuel cost will bankrupt you.

#### Waste Four: Runaway Loops

Loops without exit conditions, or with exit conditions that are too loose. The agent goes down the road of "optimization" and never comes back, tokens哗哗 burning.

Like the "perpetual motion machine" failure mode from Chapter 12.

#### Waste Five: Redundant Verification

Doing the same checks over and over — lint runs three times, tests run five rounds, four different agents do AI review.

Quality matters, but past a certain point, marginal returns diminish.

> **Core Insight**: The most effective way to reduce AI costs isn't switching to cheaper models — it's reducing waste. Cut the wasted tokens, and costs might drop by half.

### 19.3 The Five-Layer Framework for Cost Optimization

How to reduce costs? We have a five-layer optimization framework:

#### Layer One: Task Routing (Choose the Right Model)

Different tasks use different tiers of models.

- **Simple tasks** (typo fixes, formatting, classification) → Use small/cheap models
- **Medium tasks** (regular feature development, routine review) → Use medium models
- **Complex tasks** (architecture design, complex bug fixes) → Use the best models

The core of task routing: **Don't use a cannon to kill a mosquito, and don't use a slingshot to kill an elephant.**

Implementation:

- Use a small model first to do "task classification," then route to different models based on results
- Can also judge based on task source, tags, historical data

#### Layer Two: Context Optimization (Choose the Right Content)

The context you give the agent shouldn't be as much as possible — it should be as relevant as possible.

Optimization methods:

- **Retrieval-Augmented Generation (RAG)**: Only retrieve code and docs relevant to the task
- **Layered summarization**: Give project-level summary first, then module-level, then detailed code when needed
- **Context trimming**: Only keep the last N rounds of conversation, older conversations get summarized and compressed

Good context optimization can reduce token usage by 50%+ without reducing quality.

#### Layer Three: Process Optimization (Choose the Right Path)

Optimize the loop's process, reduce unnecessary steps and retries.

Optimization methods:

- **Fast failure detection**: Discover "this path isn't working" as early as possible, don't wait for N attempts before giving up
- **Smart retry strategy**: Don't retry every failure — first judge whether it's worth retrying, how to retry
- **Progressive deepening**: Try simple/cheap methods first, upgrade to complex/expensive methods only if needed

#### Layer Four: Caching & Reuse (Don't Repeat Computation)

Don't regenerate the same things.

Optimization methods:

- **Result caching**: Same input, if computed before, use cached result directly
- **Skill reuse**: Precipitate commonly used knowledge and patterns into Skills, don't regenerate every time
- **Memory systems**: Learn from historical tasks, avoid repeating pitfalls

#### Layer Five: Architecture Optimization (System Level)

Cost optimization at the architecture level.

Optimization methods:

- **Local small models**: Offload simple tasks to local small models, don't call cloud large models every time
- **Batch processing**: Accumulate multiple small tasks and process them in batches, improve efficiency
- **Resource scheduling**: Use cheap resources during off-peak times, only use expensive resources when busy

> **Optimization Order**: Do it from top to bottom. Start with task routing and context optimization — these have the fastest results and lowest cost. Then do process optimization and caching. Only then consider architecture-level optimization — that's the icing on the cake.

### 19.4 The Truth About Efficiency: It's Not Time You're Saving — It's Attention

Many people, when calculating ROI, only count "how much time is saved." But that's wrong.

The biggest value Loop Engineering brings isn't "saving time" — it's **saving attention**.

Time is linear. You have 24 hours a day, save 2 hours, you have 2 more hours.

But attention is scarce. You might only have 2-3 hours of deep work time per day. If loops can handle all the attention-consuming trivialities for you, you can devote your precious attention to what truly matters.

That's where the real value lies:

- Not "you can do more things in a day," but "you can do more important things in a day"
- Not "you work faster," but "your work quality is higher"
- Not "you're busier," but "you have more time to think"

The attention economy is the true economics of the AI era.

### 19.5 When to Spend Money, When to Save It

Cost optimization isn't "the cheaper the better." Spend what needs to be spent, save every penny where saving is appropriate.

**Where to spend money:**

- Quality verification for high-risk tasks — spending 10x more tokens on verification is cheaper than one production incident
- Architecture design for complex tasks — good architecture saves countless maintenance costs later
- Knowledge precipitation and system optimization — tokens spent today can save 10x tokens tomorrow
- Human time — if AI can save human attention, it's worth whatever it costs

**Where to save money:**

- Simple repetitive tasks — use cheap models when you can
- Exploratory attempts — try with low-cost methods first, invest more only if promising
- Low-value optimization — spending 10x cost for 1% improvement isn't worth it
- Runaway loops — loops without exit conditions, no amount of money is enough to burn

> **Engineering Judgment**: In the Loop Engineering era, an engineer's core ability is no longer "coding speed" — it's "engineering judgment" — knowing what's worth doing with AI, what isn't; knowing when to spend money, when to save; knowing where optimization delivers the greatest return.

---

---

### Chapter 20: To Every Engineer

### Your Next Job is Designing Loops, Not Writing Code

By this point, you might have a question:

"What about me? I'm an engineer. Loop Engineering is coming — where do I fit in? Will I be replaced? What's my value?"

That's a good question. And it's a question every engineer should think about.

Let me answer with a story.

### 20.1 From Typist to Programmer

Decades ago, there was a profession called "typist" — people专门 responsible for typing what others wrote on typewriters. People who typed fast and accurately were highly valued.

Then personal computers became popular. Everyone had a computer, everyone could type. The profession of typist disappeared.

But — did typing disappear? No. Not only did it not disappear — everyone types every day now. Typing went from being a "profession" to being a "basic skill."

The same thing is happening to "writing code."

AI's ability to write code keeps getting stronger, faster, cheaper. Someday, "writing code" will be like "typing" — no longer a specialized profession, but a basic skill of every engineer.

Then what happens to engineers?

Typists didn't disappear. They became — programmers.

### 20.2 Your Value is Upgrading, Not Disappearing

Many people worry "AI will replace engineers." But history tells us that technological revolutions never "replace people" — they "upgrade people's work."

- Calculators didn't replace mathematicians — they freed mathematicians from calculation to focus on higher mathematics
- CAD didn't replace architects — it freed architects from drawing to focus on more creative design
- Compilers didn't replace programmers — they freed programmers from assembly to focus on higher-level architecture

Similarly, Loop Engineering won't replace engineers. It will free engineers from writing code to focus on more valuable things:

#### Value One: Problem Definition

AI is good at solving problems, but it's not good at defining them. "What to build," "why build it," "who to build it for" — these require human insight and judgment.

For an excellent engineer, the most valuable ability isn't "problem-solving ability" — it's "problem-defining ability." Knowing what to build is far more important than knowing how to build it.

#### Value Two: System Design

AI can write code, but it's not good at designing systems. Architectural decisions, technology selection, module division, interface design — these require global vision, trade-offs, accumulated experience.

The more loops there are, the more complex they are, the more important system design becomes. Because you're not just writing a piece of code — you're designing a system that runs on its own.

#### Value Three: Quality Assurance

AI's output quality varies. Who judges whether quality is good enough? Who decides whether it can ship? Who bears the ultimate responsibility?

Humans.

Quality assurance is one of the core values of human engineers. You don't need to write every line of code yourself, but you need to be responsible for the final result. You are the last line of defense.

#### Value Four: Loop Design

This is the newest and most promising direction of value — designing and optimizing loop systems.

Just as programmers upgraded from "typing" to "programming" decades ago, today's engineers are upgrading from "writing code" to "designing loops."

You no longer lay bricks yourself — you design the brick-laying machines.
You no longer do the work yourself — you design the systems that do the work.

This is a brand new engineering field with infinite possibilities. And right now is the best time to get in.

### 20.3 The Engineer's Capability Upgrade Path

As an engineer, what capabilities do you need to upgrade?

#### Layer One: AI Tool Proficiency (Basic)

This is the most fundamental — you need to be able to use AI tools. Know how to talk to AI, how to write prompts, how to use various AI programming tools.

It's like knowing how to use an IDE, how to use Git, how to use the command line — it's basic training.

But don't stop here. Lots of people can use tools — this is just entry-level.

#### Layer Two: Engineering Judgment (Intermediate)

Knowing when to use AI, when not to; knowing what tasks suit automation, what tasks must be done yourself; knowing how to evaluate AI output quality, how to judge reliability.

Engineering judgment is the crystallization of experience and thinking. It's not learned from books — it's built through practice — the more you use it, the more pitfalls you encounter, the naturally you develop it.

#### Layer Three: System Design Capability (Advanced)

Ability to design complex systems — not just code systems, but loop systems, AI teams, workflows.

System design capability requires:

- Global vision — can see the whole picture, not just your own piece
- Trade-off thinking — knows there's no perfect solution, every choice has trade-offs
- Abstraction ability — can simplify complex problems into clear models
- Risk awareness — can foresee potential problems, prepare in advance

#### Layer Four: Loop Architecture Capability (Future)

This is the highest layer — designing and optimizing the entire loop system. Including:

- Designing loop architecture and modules
- Defining quality standards and gate systems
- Building knowledge precipitation and evolution mechanisms
- Managing the balance of cost and efficiency
- Planning an organization's AI transformation path

This is a brand new field — no ready-made textbooks, no standard answers. But precisely because of this, the opportunities are also the greatest.

### 20.4 Action Guide: Starting Today

Don't wait until you're "ready" to start. Nobody is ever ready. The best way to learn is by doing.

Here are some specific action suggestions:

#### What You Can Do This Week

- Pick one repetitive task you do every week, try to automate it
- Deeply use one AI programming tool (Claude Code or Cursor), use it intensively for a week
- Read 3 high-quality articles about Loop Engineering (recommendations in Appendix B)

#### What You Can Do This Month

- Design and implement your first loop (refer to the five-step methodology in Chapter 10)
- Start recording your AI usage experience — what scenarios work well, what don't, what pitfalls you've stepped in
- Try comparing different models and tools, build your own "tool intuition"

#### What You Can Do This Year

- Build your own Skill library — organize your常用 prompts, templates, best practices
- Promote 1-2 loop practices in your team, benefit the team
- Deeply learn one framework (LangChain or similar), master the ability to build complex loops

#### Long-Term Direction

- Transform from "person who writes code" to "person who designs systems"
- Build your technical influence — share your loop practices, help others grow
- Find the direction you're most interested in and go deep — is it technical architecture? Product experience? Organizational change?

> **The Most Important Thing**: Don't be afraid of making mistakes. Loop Engineering is a brand new field — nobody is an expert. The pitfalls you've stepped in, the mistakes you've made, the things you've learned from them — those are your most valuable assets.

### 20.5 In Closing

This book is coming to an end.

But your Loop Engineering journey is just beginning.

The last thing I want to tell you is: **This isn't a technological revolution — it's a human revolution.**

Technology will change, tools will iterate, frameworks will become outdated. But some things never change —

- Passion for solving problems
- Curiosity for learning new things
- Pursuit of quality
- Desire to create value

These are the true core of an engineer.

Loop Engineering is just a载体. What it carries is your original aspiration — to create something with technology.

So don't ask "Will Loop Engineering replace me?"
Ask — "With Loop Engineering, what can I create that I couldn't create before?"

The answer is in your hands.

Go create.

> Don't Write Prompts, Write Loops.
>
> Don't be an Executor, be a Designer.
>
> Your next job, is designing the future.

---

---

## Appendices

### Appendix A: Loop Design Checklist

### Use this checklist to verify whether your loop design is complete and reliable.

---

### Goals & Scope

---

### Trigger Mechanism

---

### Execution Agent

---

### Work Environment

---

### Quality Gates

---

### Failure Handling

---

### Memory & Learning

---

### Monitoring & Metrics

---

### Security & Compliance

---

### Cost Optimization

---

---

### Appendix B: Recommended Reading & Resources

### Core Readings

1. **Loop Engineering: From Prompt Engineering to Loop Engineering**

   - Addy Osmani, 2026.6.7
2. **Designing Loops, Not Prompts**

   - Peter Steinberger, Google Cloud AI
3. **The End of Prompt Engineering**

   - Boris Cherny, Head of Claude Code
4. **Vibe Coding**

   - Andrej Karpathy
5. **LangChain Four-Loop Architecture**

### Tools & Frameworks

|------|------|------|

### Community & Practice

### Extended Topics

---

---

### Appendix C: Glossary

### A

**代理**

**代理式AI**

**自动化触发器**

### C

**链式**

**CD / 持续集成/持续交付**

**认知投降**

**理解债务**

### H

**驾驭工程**

**爬山算法**

### L

**循环工程**

**长期记忆**

### M

**Model Context Protocol**

**记忆系统**

**创建者-检查者**

### P

**提示词工程**

### R

**Retrieval-Augmented Generation**

**Reasoning + Acting**

### S

**技能**

**子代理**

### V

**氛围编程**

### W

**工作树**

**工作记忆**

---

---

<!-- 审稿记录 -->
<!--
审稿人：vokoforge-reviewer
审稿日期：2026-07-12
文件：02-write-loop/02-English-Version.md
发现问题数：5
修复内容摘要：
  - 标题层级跳级 5 处（H1->H3, H1->H3, H1->H3等，未自动修改以保留原结构）
未修复问题：
  - 标题层级跳级未自动修改（避免破坏原意）
-->
