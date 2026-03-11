# From Vibe Coding to Agentic Engineering

> Note: Unlike previous articles, this one was written by the developer — not AI.

---

## Introduction

In March 2025, "Vibe Coding" first appeared on my radar. Back then, coding agents could put together a decent-looking demo, but that was about it. After a few attempts at getting one to help me with modifications, I never opened that page again.

In January 2026, I started using Claude Code. It was genuinely faster and better — capable of spinning up a working website in minutes. But the debugging process was still painful: the bugs it wrote were mine to find, describe, and correct over and over. I thought I was directing an engineer. In reality, I was gradually becoming a full-time QA.

Then came OpenClaw, which led me to explore the concept of Agentic Engineering. The quality of AI-written code went up another notch. More importantly, this paradigm may still have a lot of room to grow.

**ChurnPilot** is my first side project, and the first project where I genuinely didn't write a single line of code. It's not complex, but it's a functional product. Using it to tell the story from Vibe Coding to Agentic Engineering happens to cover everything I've been tinkering with from January to March in 2026.

---

## Motivation: A Practice Project I'd Actually Use

The motivation for building ChurnPilot was simple.

As a credit card optimizer, I have a lot of cards, each with a pile of benefits — a $10 rideshare credit this quarter, a $15 streaming reimbursement that month, a $200 annual travel credit. I'd been managing all these perks in Excel: resetting every quarter, marking which ones I'd already claimed. I enjoyed it, but always felt the process could be improved.

I was looking for a project to try Claude Code with, and the idea came naturally: **build a website that manages multiple credit cards and their benefit statuses in one place**. The goal was just to make something I'd actually use — so I wouldn't abandon it, and I'd have motivation to keep iterating. As for monetization? Honestly never crossed my mind.

---

## Vibe Coding: Joy and Pain in Equal Measure

So I jumped right in. Signed up for a $20/month Claude Pro subscription, opened Claude Code.

The first experience was genuinely impressive. I roughly described what I wanted, and it just started chugging away. The first goal was simple: a page to add credit cards, running locally. If I remember correctly, it was done in under ten minutes.

Then I kept adding features: user registration, a card template library, benefit status tracking, and so on.

As the system grew more complex, I gradually noticed it struggling more and more. Context kept getting compressed and contaminated, and errors became increasingly frequent — either it couldn't fully implement what I asked for, or it lacked big-picture awareness, fixing one thing while breaking another. That's when I had my first observation:

> **Getting AI to create a demo from scratch is far easier than getting it to modify existing code.**

It was a bittersweet process. The joy came from watching it generate hundreds of lines of code in seconds, terminal all green, feeling impressed. The pain was that much of this code was: 1. ineffective, 2. barely reusable, 3. wrong.

Throughout the entire process, I stuck to one principle: **don't change a single line of code — don't even look at the code**.

This wasn't laziness. I wanted to put an ultimate principle into practice: when you're using AI agents to build things, you should **define rules** to construct the system, letting it self-correct within that framework, rather than manually patching every error. The logic is simple, assuming the LLM is capable enough:

1. If the rules are comprehensive, errors get systematically corrected
2. If errors aren't getting corrected, the rules aren't good enough yet — keep iterating that feedback loop

I also had Claude add end-to-end browser tests with browser automation so it could test itself. But the efficiency wasn't there. It turned into an endless loop of me finding bugs, realizing it misunderstood my intent, and discovering more bugs.

Gradually, I grew disappointed. I could clearly feel this wasn't what I wanted.

What I wanted was: **to build an AI development system that could continuously improve itself**. I didn't want to be the person in this system who's forever doing manual testing.

So ChurnPilot sat in my GitHub repo as a half-finished product.

---

## Agentic Engineering: From Tool to System

That's when OpenClaw entered my field of vision (it was still called Clawdbot back then). Like Claude Code, the initial impression was striking. For me, OpenClaw brought three key incremental capabilities:

1. **Long-term memory** — Claude Code can do this too, but you have to build your own memory retrieval system. OpenClaw provides it out of the box.
2. **Stronger agentic capabilities** — it can run browser tests, send and receive emails, register accounts on its own. It's not just writing code — it can interact with the outside world.
3. **Multi-agent collaboration** — this was the most important point for me. The experience of dividing labor and coordinating between multiple agents was noticeably better than Claude Code.

In theory, Claude Code could do all of this, but OpenClaw is like a toolkit someone has already organized for you. If it's already built, why reinvent the wheel?

Keeping to my earlier principle of "not looking at a single line of code," I gradually used OpenClaw to build a **pipeline-based division of labor system**. The core logic uses GitHub Issues to record each task, combined with a scheduled check script that runs every 5 minutes. If there are pending tasks, they get automatically dispatched to the corresponding sub-agent:

```
Precheck (5min) → CTO Triage → Engineer → Code Review → QA Test → CTO Approval
```

This isn't a novel architecture — plenty of people in the community are doing similar things. Looking back, if I'd found some mature frameworks earlier, I probably would have just used those. But building it myself from scratch had its benefits: **understanding every detail makes future maintenance easier**. The downside is that this is a prompt-defined system, not something with lower-level hooks like LangGraph — it's highly dependent on the model's own capabilities.

Once the system was set up, my workload decreased considerably. Most days I'd create some tickets based on my own observations, let the pipeline handle them, then fine-tune individual steps. Of course, this process was far less effortless than it sounds here. You can never imagine how many bizarre hypotheses an LLM can come up with on its own, or how it can fail to grasp something that seems obvious to me. But fortunately, I discovered along the way that I'm genuinely interested in "building an architecture" — so while it was sometimes tiring, it never felt painful.

The end result? Code quality was mixed. I checked, and the ChurnPilot repo alone already has over 130 tickets. Honestly, this isn't a particularly complex piece of software — it shouldn't need that many tickets. Sometimes a task needs to be sent back multiple times; sometimes I need to step in manually with guidance. This might be because I didn't plan well enough upfront — the next project should go more smoothly.

That said, if I'd been writing it by hand, I probably would have given up long ago out of frustration with all the frontend work.

ChurnPilot still has plenty of bugs, but at least it's basically functional. My goal was never to build a perfect product — just to practice and see where AI's capability boundaries are right now. **The main focus was always on building the system, not the project itself.** From that perspective, mission accomplished.

One more thing: I'm not writing this to say Vibe Coding is obsolete. In fact, if the goal were to ship a complete product faster and better — say, ChurnPilot — I think using Claude Code for Vibe Coding directly could have gotten it online two weeks earlier, with higher quality too. It's just that my personal interest wasn't there, so I quickly pivoted to OpenClaw's system.

---

## A New Pattern: Separating Planning from Execution

The next project is an **LLM-based Character Life Simulation** — inspired by the life simulation games I used to play. I chose this direction for two reasons:

1. I wanted to see if AI could do better on a project that's less frontend-dependent
2. It's fun

The OpenClaw pipeline is great, but the token consumption is enormous — to the point where $200/month of Claude Max isn't enough. Not to mention that Claude now doesn't let OpenClaw use subscriptions. So right now I'm using **Claude** for writing product docs and roadmaps, then using **OpenClaw for execution** — breaking down tasks and delivering based on the planning documents.

Planning quality determines execution efficiency. This separation pattern feels right so far.

---

## A Few Observations

1. **Agent capabilities are limited, but continuously improving.** As long as scaling laws hold, the Agentic Engineering paradigm will keep evolving. What's impossible today might work tomorrow. Just look at how Vibe Coding has developed from last March to now — the pace is staggering.

2. **This model works end-to-end, but maintainability is questionable.** ChurnPilot proved that AI can handle the full lifecycle from start to delivery. But the bottleneck is no longer "how much code can AI generate" — **code quality and QA are the real focus going forward**. Generation is easy; verification is hard. I've felt this very clearly working on ChurnPilot, a project with heavy user interaction.

3. **Developers are still a key part of the equation for now, but the critical skills are shifting.** People without technical backgrounds can absolutely use AI to build interesting demos or small tools — perfectly fine for personal use. But for medium-to-large projects, from a long-term maintainability perspective, understanding software development is still necessary at this point. **In the long run, though, the core competitive advantage may no longer be technical implementation, but taste, market instinct, and sensitivity to user needs.**

---

## One Final Question

If AI capabilities keep expanding, from software into the physical world, to the point where humans become worthless from a productivity standpoint —

**Where do you think your value lies?**

March 2026

Redmond
