---
title: Arithmetic Operators — Deep Dive
description: Learn the exact behavior of +, -, *, /, //, %, ** including edge cases, integer vs float math, and practical patterns.
tags: [python, arithmetic, division, modulo, exponentiation, floor-division, patterns]
---

# Arithmetic Operators — Deep Dive

## 1. Operator Table

| Operator | Name | Example | Notes |
|---|---|---|---|
| `+` | Addition | `a + b` | number or string concat (str + str) |
| `-` | Subtraction | `a - b` | numeric only |
| `*` | Multiplication | `a * b` | `str * int` repeats string |
| `/` | True division | `7 / 2` | always float |
| `//` | Floor division | `7 // 2` | toward -∞: `-3 // 2 == -2` |
| `%` | Modulo | `7 % 2` | remainder, sign follows divisor |
| `**` | Exponent | `2 ** 3` | right-associative |

## 2. Integer vs Float Behavior

```python
7 / 2     # 3.5
7 // 2    # 3
-7 // 2   # -4  (floors toward negative infinity)
-7 % 2    # 1   because (-7) = (-4)*2 + 1
```

## 3. String Multiplication and Addition

```python
"ha" * 3   # 'hahaha'
"py" + "thon"  # 'python'
# Note: '+' only works str+str; not str+int
```

## 4. Patterns You’ll Actually Use

- **Parity**: `n % 2 == 0`
- **Wrap-around index**: `(i + 1) % N`
- **Area/Circle**: `math.pi * r ** 2`
- **Average**: `total / max(count, 1)`

## 5. Edge Cases to Know

- Overflow? Python integers are arbitrary precision; they grow as needed.
- `0 ** 0` is `1` (by Python definition).
- Division by zero raises `ZeroDivisionError`.

## 6. Exercises

1) Implement power-of-two check using modulo or bit logic (hint: `n & (n-1) == 0`).  
2) Compute the last digit of `a ** b` efficiently for small `b`.  
3) Fill in code to safely average numbers even when list might be empty.

```python
nums = []
avg = ____________________________
```

```{admonition} Answers
:class: dropdown
1) `n > 0 and (n & (n-1)) == 0`  
2) `pow(a, b, 10)` returns last digit directly  
3) `sum(nums) / len(nums) if nums else 0`
```


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


[← Back to Expressions Overview](../expressions.md)
