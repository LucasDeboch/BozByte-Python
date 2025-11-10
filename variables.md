---
title: Variables and Data Types — Representing Information in Code
description: Learn how computers store and manipulate information using variables and data types — the first step to translating thought into code.
tags: [python, variables, data-types, foundation, cognitive-programming]
---

# Variables and Data Types — Representing Information in Code

Every program starts with data — numbers, text, or information we want the computer to process.  
To work with that data, we need a **way to store, name, and reuse it**. That’s where variables and data types come in.

---
## 0) Quick Python Syntax (at a glance)

- **Indentation** defines blocks; use 4 spaces.
- **Statements** end with a newline (no semicolons needed).
- **Comments** start with `#`.
- **Strings**: `'single'`, `"double"`, `'''triple'''`.
- **Print/Input**: `print(...)`, `input(...)`.
- **Naming**: `snake_case` for variables/functions.

```python
# example
name = "Ada"
if len(name) > 2:
    print(f"Hello, {name}")
```

## 1. The Conceptual Foundation — Why Variables Exist

In human thought, we constantly label ideas:  
> “My age is 25.” “The temperature is 20°C.” “My name is Sam.”

Each label represents information that can change over time.  
In programming, we mimic this mental habit by creating **variables** — names that point to data stored in memory.

**Analogy:**  
A variable is a box with a label. The label stays fixed, but what’s inside can change.

```{note}
Computers don’t “know” what an age or a name means — they just store data.  
Meaning comes from *how we name and use* the data.
```

---

## 2. Creating Variables in Python

Python makes it simple to assign data to variables using the `=` operator.

```python
age = 25
name = "Sam"
temperature = 20.5
is_student = True
```

**How it works:**
- The variable name (`age`, `name`) is a label.
- The value (`25`, `"Sam"`, `20.5`, `True`) is stored in memory.
- The `=` symbol means “assign the value on the right to the name on the left.”

---

## 3. Data Types — Understanding What Kind of Data You’re Storing

Every value in Python belongs to a **data type**, which defines what operations you can perform on it.

| Data Type | Example | Description |
|------------|----------|-------------|
| **int** | `10`, `-5` | Whole numbers |
| **float** | `3.14`, `-2.7` | Decimal numbers |
| **str** | `"Hello"`, `'Python'` | Text data (string) |
| **bool** | `True`, `False` | Logical values (yes/no) |

```python
# Examples
x = 10          # int
y = 3.14        # float
name = "Alice"  # str
is_active = True  # bool
```

Python automatically detects the type when you assign a value.  
You can check it with the built-in `type()` function:

```python
print(type(name))      # <class 'str'>
print(type(x))         # <class 'int'>
```

---

## 4. Mental Model: How the Computer Stores Variables

```{mermaid}
graph TD
    A["Variable Name"] --> B["Memory Address"]
    B --> C["Stored Value"]

    A1["name"] --> B1["@0x12A"]
    B1 --> C1["Sam"]

    A2["age"] --> B2["@0x12B"]
    B2 --> C2["25"]
```

This visualization helps you understand that:
- A variable name is just a *reference* to where data lives.
- Changing a variable doesn’t “edit” the data — it points the name to a new value.

```python
x = 5
x = 10  # 'x' now refers to a new value
```

---

## 5. Naming Variables — Clarity and Intent

Good naming is the difference between readable code and confusion.

**Rules:**
- Must start with a letter or underscore.
- Can contain letters, numbers, and underscores.
- Case-sensitive (`name` ≠ `Name`).
- No spaces or symbols.

**Best practices:**
- Use descriptive names (`total_price`, `user_name`).
- Avoid single letters unless for short loops (`i`, `n`).
- Use lowercase with underscores (Python’s “snake_case” convention).

---

## 6. Type Conversion — When Data Needs to Change Form

Sometimes, you need to convert one type into another.  
Python provides built-in functions for **type casting**.

```python
# String to integer
age = int("25")

# Integer to string
score = str(100)

# Float to integer
price = int(9.99)

# Integer to float
speed = float(10)
```

Be careful: converting incorrectly can cause errors.

```python
# This fails:
number = int("abc")  # ValueError
```

```{tip}
Think of type conversion as translation:  
you can’t do math on a word, but you can turn it into a number if it makes sense.
```

---

## 7. Real-World Example — Personalized Message Generator

Let’s use variables and types in a simple program.

```python
name = input("What is your name? ")
age = int(input("How old are you? "))
year_of_birth = 2025 - age

print(f"Hello, {name}! You were born in {year_of_birth}.")
```

**Concepts used:**
- Input (string)
- Type conversion (string → int)
- Arithmetic and formatting
- Output through interpolation

---

## Practice: Embedded Sandbox

<div style="margin: 1rem 0;">
<iframe
  src="https://codapi.org/embed/?sandbox=python&code=data%3A%3Bbase64%2CBcHJCQAgDADBVhYsyrfEgMEjEvRh984kcthRnl%2FEq9K0BGVVZJh04i6OIz63Df0%3D"
  width="100%"
  height="480"
  frameborder="0"
  loading="lazy"
  allow="clipboard-read; clipboard-write">
</iframe>
</div>

---

## 8. Reflection and Conceptual Connection

```{admonition} Reflection Exercise
:class: tip
1. What kind of information do you interact with daily — names, prices, choices, dates?  
2. How would you represent them in Python using variables and data types?  
3. Which type would you use for each?
```

**Example:**
| Real Data | Python Variable | Data Type |
|------------|----------------|-----------|
| “Alice” | `name` | `str` |
| 24 | `age` | `int` |
| 72.5 | `weight` | `float` |
| True | `is_logged_in` | `bool` |

---

## 9. Common Mistakes and How to Think About Them

| Mistake | Why It Happens | Cognitive Fix |
|----------|----------------|----------------|
| Mixing data types (`"5" + 5`) | Confusing representation vs value | Ask: *Is this number or text?* |
| Using unclear names (`x1`, `y2`) | Lack of meaning mapping | Reconnect name → concept |
| Forgetting to convert input | Input is always text | Always cast: `int(input())` if numeric |

---

## 10. Mini Checkpoint

Try answering these without running the code first:

1. What is the output?
   ```python
   x = 5
   y = "5"
   print(x + int(y))
   ```
2. What type is returned by `input()`?
3. How do you convert `3.14` into an integer?
4. Why might `"10" + "5"` give a different result than `10 + 5`?

---

## 11. Summary Diagram

```{mermaid}
graph TD
  A[Variables and Data Types] --> B[Variables]
  A --> C[Data Types]
  A --> D[Naming Rules]
  A --> E[Type Conversion]
  A --> F[Input and Output]
  B -->|Labeling Information| C
  C -->|Defines Behavior| E
  F -->|Interacts with User| A
```

---

## 12. Next Step

👉 Continue to **Expressions and Operators — Describing Relationships in Code** 
