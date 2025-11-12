---
title: Control Flow — Decisions and Loops
description: A professional, book‑quality chapter that teaches control flow step by step. Each topic follows Concept → Syntax → Diagram → Example with detailed explanation → Exercise. Focused on the 20% you’ll reuse in 80% of programs.
tags: [python, control flow, beginner, if, elif, else, boolean, for, while, break, continue]
---

# Control Flow — Decisions and Loops

Control flow turns a list of instructions into a program that **reasons**. It lets code make **choices** (branching) and **repeat** work (iteration) until a goal is reached. In this chapter we master the essentials you’ll reuse constantly: **conditions**, **`if/elif/else`**, **boolean logic**, **`for`**, **`while`**, and **`break/continue`**.

---

## 1) Conditions — Writing Precise Yes/No Questions

### Concept
A **condition** is any expression that evaluates to `True` or `False`. Every branch in your program rests on a condition, so clarity here determines the reliability of the entire control flow.

Two principles make conditions robust:

1. **Boundaries reflect intent.** If you mean “between 0 and 100 inclusive,” write `0 <= score <= 100`. State the boundary explicitly.
2. **Grouping removes ambiguity.** When combining ideas, wrap them with parentheses to make your logic obvious to both the interpreter and the human reader.

Python also has the notion of **truthiness**: values like `False`, `None`, `0`, `""` (empty string), `[]`, `{}` count as false. Everything else is truthy. Use this carefully—prefer explicit comparisons when it improves clarity.

### Syntax
```python
# Comparisons
x == 10
y != 0
0 <= score <= 100

# Combined logic
(name != "") and (score >= 60)
not email.endswith(".")

# Truthiness 
if len(name) > 0:
    ...
```

### Diagram
```{mermaid}
flowchart TD
  A[Evaluate condition] --> B{True or False?}
  B -- True --> C[Run intended action]
  B -- False --> D[Skip / choose alternative]
  C --> E[Next statement]
  D --> E
```

### Example
```python
percentage = 87
name = "Sam"

if (0 <= percentage <= 100) and (name != ""):
    print("Valid record")
else:
    print("Invalid record")
```

### Detailed explanation
- `0 <= percentage <= 100` is a **chained comparison**; Python interprets this as `(0 <= percentage) and (percentage <= 100)`. Writing it as one expression reduces duplication and off-by-one mistakes.
- `(name != "")` states explicitly that an empty string is not acceptable. Although `if name:` would also work by truthiness, explicit comparison is clearer to beginners.
- The whole `if` condition is a conjunction: both the range check and the name check must be `True`. Parentheses make the grouping and precedence unambiguous.

### Exercise
Write a condition that is `True` only if:
- `age` is between 13 and 17 inclusive, **and**
- `country` is not `"NA"`, **and**
- `name` is not empty.

Explain why each set of parentheses helps readability.

---

## 2) `if / elif / else` — Choosing Exactly One Path

### Concept
An `if` statement selects **one** of several alternatives. Python evaluates the branches **top to bottom** and runs the **first** branch whose condition is `True`. If none match, the optional `else` branch runs. The readability of your branching depends on **non-overlapping ranges** and **shallow nesting**. When a case can be ruled out early (e.g., “not logged in”), handle it first; what remains is the “happy path.”

### Syntax
```python
if condition_a:
    # block A
elif condition_b:
    # block B
else:
    # block C  # optional
```

### Diagram
```{mermaid}
flowchart TD
  A[Start] --> B{condition_a true?}
  B -- Yes --> C[Run block A] --> G[Next]
  B -- No  --> D{condition_b true?}
  D -- Yes --> E[Run block B] --> G
  D -- No  --> F[Run else] --> G
```

### Example
```python
temp = 18

if temp < 0:
    label = "Freezing"
elif temp < 10:
    label = "Cold"
elif temp < 20:
    label = "Cool"
else:
    label = "Warm"

print(label)
```

### Detailed explanation
- The first matching branch wins; later branches are ignored. With `temp = 18`, the `temp < 20` check is the first `True`, so `"Cool"` is chosen.
- Each threshold uses a strict `<` comparison. Because the checks are ordered from smallest to largest, every possible value fits exactly one branch. This design eliminates fence-post bugs and makes later maintenance straightforward.
- If you’re tempted to nest `if` inside `if`, consider flipping the outer condition to handle a fast failure first; it will usually read better.

### Exercise
Write an `if/elif/else` ladder that classifies a test score into:
- `"A"` for 90–100,
- `"B"` for 80–89,
- `"C"` for 70–79,
- `"D"` for 60–69,
- `"F"` for below 60.

Ensure your ranges don’t overlap and no score is left unclassified.

```{admonition} Try it yourself (click to open)
:class: dropdown
<div style="margin: 0.5rem 0 1rem;">
<iframe
  src="https://codapi.org/embed/?sandbox=python&code=data%3A%3Bbase64%2CBcHJCQAgDADBVhYsyrfEgMEjEvRh984kcthRnl%2FEq9K0BGVVZJh04i6OIz63Df0%3D"
  width="100%"
  height="420"
  frameborder="0"
  loading="lazy"
  allow="clipboard-read; clipboard-write"
  title="Python Practice Sandbox">
</iframe>
</div>
```
---

## 3) Boolean Logic — Combining Ideas Precisely

### Concept
Real decisions often combine smaller truths. Use:
- `and` when **every** required condition must hold,
- `or` when **any one** is sufficient,
- `not` to express a prohibition or negation.

Python uses **short-circuit evaluation**:
- For `A and B`, if `A` is `False`, Python won’t evaluate `B` (the whole expression can’t be `True`).
- For `A or B`, if `A` is `True`, Python won’t evaluate `B` (the whole expression is already `True`).

This saves time and prevents unnecessary or unsafe operations.

### Syntax
```python
(age >= 18) and has_id
(has_coupon) or (total >= 50)
not username.endswith(".")
```

### Diagram (short-circuit behavior)
```{mermaid}
flowchart TD
  A[Evaluate A] -->|A is True| B{Evaluate B}
  A -->|A is False| F[Result: False]
  B -->|B is True| E[Result: True]
  B -->|B is False| F
```
```{mermaid}
flowchart TD
  A[Evaluate A] -->|A is True| E[Result: True]
  A -->|A is False| B{Evaluate B}
  B -->|B is True| E
  B -->|B is False| F[Result: False]
```

### Example
```python
text = "42"
if (text != "") and text.isdigit():
    n = int(text)
    print("Parsed:", n)
else:
    print("Invalid input")
```

### Detailed explanation
- The left condition `(text != "")` prevents pointless or risky checks on an empty string. Thanks to short-circuiting, `text.isdigit()` runs only if the first check succeeded.
- After both conditions pass, we convert to `int` safely.
- Parentheses communicate structure and intent immediately; when you revisit this code, the logic is obvious.

### Exercise
Given `email` (a string), write a condition that returns `True` only if:
- there is an `"@"` somewhere in the string, **and**
- the string does **not** end with `"."`.

Explain how short-circuiting could avoid unnecessary work.

---

## 4) `for` Loops — Iterating Cleanly

### Concept
Use a `for` loop to iterate over a **known collection** (list, string, file lines) or a **controlled count** from `range`. Prefer iterating **items directly**; resort to indices only when the index is genuinely part of the logic (e.g., numbering rows).

### Syntax
```python
# Items directly
for item in collection:
    # body

# Count with range (stop is exclusive)
for i in range(start, stop, step):
    # body
```

### Diagram
```{mermaid}
flowchart TD
  A[Start for-loop] --> B[Take next element]
  B --> C{Any element left?}
  C -- Yes --> D[Run body with element] --> B
  C -- No  --> E[Exit loop]
```

### Example
```python
names = ["Ada", "Grace", "Linus"]

for name in names:
    print(name)

for i in range(1, 4):   # 1, 2, 3
    print("Round", i)
```
### Detailed explanation
- `for name in names` reads like the intent: “for each name, do…”. The absence of manual indexing reduces clutter and prevents index mistakes.
- `range(1, 4)` yields `1`, `2`, `3`. Remember that the `stop` boundary is **not included**. This convention aligns with slice semantics and makes ranges predictable.

### Exercise
Print the odd numbers from 1 to 19 (inclusive) using a single `for` loop and `range`. Explain how the `step` argument avoids extra `if` checks inside the loop.

```{admonition} Try it yourself (click to open)
:class: dropdown
<div style="margin: 0.5rem 0 1rem;">
<iframe
  src="https://codapi.org/embed/?sandbox=python&code=data%3A%3Bbase64%2CBcHJCQAgDADBVhYsyrfEgMEjEvRh984kcthRnl%2FEq9K0BGVVZJh04i6OIz63Df0%3D"
  width="100%"
  height="420"
  frameborder="0"
  loading="lazy"
  allow="clipboard-read; clipboard-write"
  title="Python Practice Sandbox">
</iframe>
</div>
```

---

## 5) `while` Loops — Repeat Until the Goal Is Reached

### Concept
A `while` loop repeats **as long as** its condition is `True`. Choose `while` when you do not know the number of iterations in advance. The loop must make **progress** toward ending; otherwise, it risks running forever.

A dependable `while` loop has:
- a **condition** tied to the goal,
- a **state update** inside the body that moves the condition toward `False`.

### Syntax
```python
while condition:
    # body
    # update something that affects condition
```

### Diagram
```{mermaid}
flowchart TD
  A[Enter while] --> B{condition True?}
  B -- Yes --> C[Run body]
  C --> D[Update state]
  D --> B
  B -- No --> E[Exit loop]
```

### Example
```python
text = ""
while text == "":
    text = input("Type something: ").strip()

print("You typed:", text)
```

### Detailed explanation
- The loop expresses the goal directly: “while empty, keep asking.” This makes the intent self-documenting.
- The state update is the line that reads input and assigns to `text`. Without that, `text` would never change and the loop would never end.
- Structuring your `while` loops this way helps prevent infinite loops and captures the real-world process cleanly.

### Exercise
Write a `while` loop that asks for a password until it is at least 8 characters **and** contains at least one digit. Explain which line causes progress toward the loop’s termination.

```{admonition} Try it yourself (click to open)
:class: dropdown
<div style="margin: 0.5rem 0 1rem;">
<iframe
  src="https://codapi.org/embed/?sandbox=python&code=data%3A%3Bbase64%2CBcHJCQAgDADBVhYsyrfEgMEjEvRh984kcthRnl%2FEq9K0BGVVZJh04i6OIz63Df0%3D"
  width="100%"
  height="420"
  frameborder="0"
  loading="lazy"
  allow="clipboard-read; clipboard-write"
  title="Python Practice Sandbox">
</iframe>
</div>
```

---

## 6) Fine-Tuning Loops with `break` and `continue`

### Concept
Two small tools make loops practical:

- **`break`**: exit the **nearest** loop immediately. Use when the goal is achieved (e.g., found the item).
- **`continue`**: skip the rest of the current iteration. Use to ignore unhelpful items without nesting deeper.

### Syntax
```python
for x in data:
    if should_stop(x):
        break        # done
    if should_skip(x):
        continue     # try next item
    # normal processing
```

### Diagram
```{mermaid}
flowchart TD
    S((Iteration start)) --> Q1{Stop condition?}
    Q1 -->|Yes| END[Exit loop]
    Q1 -->|No| Q2{Skip condition?}
    Q2 -->|Yes| NEXT[Next iteration]
    Q2 -->|No| BODY[Run body]
    BODY --> NEXT
    NEXT --> S
```

### Example
```python
# Stop when the odd target appears; ignore even numbers
target = 7
for n in range(1, 10):
    if n % 2 == 0:
        continue
    if n == target:
        print("Found odd target:", n)
        break
```

### Detailed explanation
- `continue` performs a fast filter: even numbers are discarded before any other work, keeping the main logic at the same indentation level.
- When the target appears, `break` ends the loop immediately, avoiding unnecessary iterations and clarifying intent: “found → done.”

### Exercise
Given `items = ["", "pen", "", "notebook", "phone"]`, write a loop that prints the first **non-empty** item and then stops. Explain why `continue` is unnecessary in your solution.

```{admonition} Try it yourself (click to open)
:class: dropdown
<div style="margin: 0.5rem 0 1rem;">
<iframe
  src="https://codapi.org/embed/?sandbox=python&code=data%3A%3Bbase64%2CBcHJCQAgDADBVhYsyrfEgMEjEvRh984kcthRnl%2FEq9K0BGVVZJh04i6OIz63Df0%3D"
  width="100%"
  height="420"
  frameborder="0"
  loading="lazy"
  allow="clipboard-read; clipboard-write"
  title="Python Practice Sandbox">
</iframe>
</div>
```

---

## 7) Small Integrated Example — Putting It All Together

### Concept
This compact program combines the core elements—precise conditions, an `if/elif/else` ladder, a `while` loop to keep trying, and `continue`/`break` to control the flow—into a finished, readable tool.

### Example
```python
import random

target = random.randint(1, 100)
attempts = 0

while True:
    s = input("Guess 1..100: ").strip()
    if not s.isdigit():           # precise validation
        print("Digits only.")
        continue                  # try again without counting

    guess = int(s)
    attempts += 1

    if guess < target:
        print("Too low.")
    elif guess > target:
        print("Too high.")
    else:
        print(f"Correct in {attempts} attempt(s).")
        break                     # success → exit loop
```

### Detailed explanation
- **Validation before conversion.** The guard `if not s.isdigit()` prevents a crash and communicates the input contract clearly. Using `continue` keeps the happy path unindented and easy to read.
- **Single source of truth for attempts.** We increment `attempts` only after a valid numeric input—this avoids counting malformed entries.
- **Clear branching.** The `if/elif/else` blocks are mutually exclusive and ordered logically from “too small” to “too large,” with success as the final case.
- **Termination conditions are explicit.** The loop ends only when the user succeeds; all other flows lead back to the start of the loop, making the program’s behavior predictable and easy to test.

### Exercise
Modify the program to:
1) Limit the user to 7 valid guesses; if exceeded, reveal the number and end.  
2) After a game ends (win or out of guesses), ask the user if they want to play again (`y/n`).  
Explain where and why you would use `break` versus `continue`.

```{admonition} Try it yourself (click to open)
:class: dropdown
<div style="margin: 0.5rem 0 1rem;">
<iframe
  src="https://codapi.org/embed/?sandbox=python&code=data%3A%3Bbase64%2CBcHJCQAgDADBVhYsyrfEgMEjEvRh984kcthRnl%2FEq9K0BGVVZJh04i6OIz63Df0%3D"
  width="100%"
  height="420"
  frameborder="0"
  loading="lazy"
  allow="clipboard-read; clipboard-write"
  title="Python Practice Sandbox">
</iframe>
</div>
```

---

## Mastery Checklist (20% that powers 80%)
- I phrase conditions with correct boundaries and explicit grouping where needed.  
- My `if/elif/else` ladders are ordered, non-overlapping, and shallow.  
- I iterate items with `for` and count with `range` safely.  
- I use `while` when the number of repetitions is unknown and I make progress each iteration.  
- I adjust loops with `break` (early exit) and `continue` (skip this turn) appropriately.  
- I can combine these to write small, robust programs.
