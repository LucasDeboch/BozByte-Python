---
title: Computational thinking
description: The first step in learning to code — understanding how computers think, and how to translate problems into logic before writing code.
tags: [orientation, computational-thinking, mental-models, programming-basics]
---

# Building Mental Models

Programming starts long before code is written.  
Before learning **syntax**, we learn **how to think** — how to deconstruct problems, identify patterns, and model ideas so that a computer can understand them.

This stage builds the mental scaffolding that every later skill depends on.

---

## 1. The Goal of Orientation

Most beginners start by memorizing code.  
Here, the goal is to **understand what code *represents*** — a series of logical instructions that describe how to solve a problem.

By the end of this section, you will:
- Understand what a computer *actually does* when it runs a program.  
- Learn to think algorithmically — in steps, decisions, and repetitions.  
- Build mental habits of decomposition, pattern recognition, and abstraction.  
- Be ready to write your first simple algorithms in pseudocode.

---

## 2. What It Means to “Think Computationally”

Computational thinking is a structured way to solve problems. It involves four core skills:

| Concept | Meaning | Everyday Example |
|----------|----------|------------------|
| **Decomposition** | Breaking a big problem into smaller steps | Making tea → Boil water → Add tea → Pour → Serve |
| **Pattern Recognition** | Spotting recurring elements | Recognizing that all drinks require heating liquid |
| **Abstraction** | Focusing on relevant details only | Ignoring the cup color when making tea |
| **Algorithm Design** | Creating a precise, repeatable plan | The exact steps needed to brew tea perfectly |

```{note}
Computers don’t “understand” — they follow patterns we define.  
Good programmers design clear, repeatable patterns for machines to execute.
```

---

## 3. How Computers “Think”

At its core, a computer performs **three fundamental operations**:

1. **Input** — receiving data (keyboard, file, sensor).  
2. **Process** — performing operations based on logic.  
3. **Output** — presenting results (screen, sound, file).

That’s all programming is — telling a computer how to process inputs to produce meaningful outputs.

**Example mental model:**

```{mermaid}
graph LR
A[Input: User enters number] --> B[Process: Multiply by 2]
B --> C[Output: Display result]
```

---

## 4. From Real World to Code Thinking

Let’s translate a real-world task into algorithmic logic.

> **Task:** Make a cup of coffee.

**Human way:**  
“I’ll grab a mug, boil some water, add coffee, pour water, and stir.”

**Computational way:**
```
start
  fill kettle with water
  boil water
  add coffee powder to cup
  pour water into cup
  stir
end
```

Notice — no emotions, no assumptions. Just ordered, repeatable instructions.  
That’s *algorithmic thinking.*

---

## 5. Exercise — Write a Simple Algorithm (No Code Yet)

Choose any daily task (e.g., tying your shoes, cooking eggs, sending a message).  
Write it as a **sequence of precise steps** — as if you were explaining it to a robot.

Example:
```
start
  open chat app
  select friend
  type message
  press send
end
```

Then, ask yourself:
- Is every step unambiguous?
- Could someone follow this exactly and get the same result?

That’s the mindset of a programmer.

---

## 6. Mental Model: The Flow of Logic

Programming follows logical flow — from **conditions** to **actions**.

```{mermaid}
graph TD
  A[Start] --> B{Condition met?}
  B -->|Yes| C[Perform Action]
  B -->|No| D[Do Something Else]
  C --> E[End]
  D --> E
```

This structure appears in nearly every programming language — Python included.

---

## 7. Reflection — Think Like a Computer

```{admonition} Reflection Exercise
:class: tip
Pick one everyday decision (like deciding what to eat).
Write down the steps and decisions involved.
Then ask yourself — how would a computer make this same decision if it could only use data and conditions?
```

---

## 8. Transition — From Thinking to Doing

Once we can model thought as logic and rules, writing Python becomes simple:  
each line of code is just one small part of the mental model you’ve already built.

Next, we’ll learn how to **translate logic into syntax** — the 20% of Python fundamentals that power 80% of programming tasks.

```{note}
You’re now ready to move from *thinking about code* to *writing your first lines*.
```

---

## 9. Concept Map — The Journey from Thought to Code

```{mermaid}
graph TD
  subgraph CT[Computational Thinking]
    D1[Decomposition]
    D2[Pattern Recognition]
    D3[Abstraction]
    D4[Algorithm Design]
  end

  subgraph CP[Computer Process]
    I1[Input]
    I2[Process]
    I3[Output]
  end

  subgraph FL[Flow of Logic]
    L1[Conditions]
    L2[Actions]
    L3[Loops]
  end

  subgraph PC[Problem to Code]
    P1[Define Steps]
    P2[Write Pseudocode]
    P3[Implement in Python]
  end

  CT --> CP --> FL --> PC
```
