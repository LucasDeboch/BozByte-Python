---
title: Precedence and Evaluation Order — Deep Dive
description: Master Python's operator precedence, associativity, short-circuit rules, and evaluation guarantees with rigorous examples and exercises.
tags: [python, precedence, evaluation-order, associativity, parsing, boolean, chaining]
---

# Precedence and Evaluation Order — Deep Dive

This page explains **what is evaluated first**, **how results flow**, and **when to add parentheses**.

## 1. Precedence Ladder (high → low)

| Level | Operators | Notes |
|---|---|---|
| 1 | `()` | Parentheses — always evaluated first |
| 2 | `x[i]`, `x.y`, function calls | Subscripts, attribute access, calls |
| 3 | `**` | Right-associative |
| 4 | `+x`, `-x`, `~x` | Unary operators |
| 5 | `* / // %` | Multiplicative |
| 6 | `+ -` | Additive |
| 7 | `<< >>` | Shifts (not common for beginners) |
| 8 | `&` | Bitwise AND |
| 9 | `^` | Bitwise XOR |
| 10 | `|` | Bitwise OR |
| 11 | Comparisons | `< <= > >= != == is is not in not in` (see chaining) |
| 12 | `not` | Boolean not |
| 13 | `and` | Boolean and (short-circuit) |
| 14 | `or` | Boolean or (short-circuit) |
| 15 | `if ... else ...` | Conditional expression |
| 16 | `:=` | Walrus operator (assignment expression) |

```{note}
`**` is **right-associative**; most others are left-associative. Parentheses are a communication tool — use them.
```

## 2. Associativity with Examples

```python
2 ** 3 ** 2   # 2 ** (3 ** 2) == 512  (right)
10 - 3 - 1    # (10 - 3) - 1 == 6     (left)
```

## 3. Chained Comparisons

Python evaluates `a < b < c` as `(a < b) and (b < c)` **without re-evaluating `b`**.

```python
x = 5
0 < x < 10    # True
(0 < x) and (x < 10)  # equivalent
```

## 4. Short-Circuit Semantics (and/or)

- `A or B` → return `A` if truthy else `B`
- `A and B` → return `A` if falsey else `B`

```python
name = input() or "Guest"     # defaulting
config = loaded and parse(cfg) # guard evaluate
```

## 5. Conditional Expressions and Walrus

```python
status = "ok" if code == 200 else "error"
while (chunk := stream.read(1024)):    # assignment expression
    process(chunk)
```

## 6. When Precedence Surprises You

```python
not 1 == 1   # parsed as not (1 == 1) -> False
# Prefer: (not 1) == 1  # if that's what you meant (rare)
```

```python
a = 1
b = 2
c = 3
a < b == c   # True only if a < b and b == c
```

## 7. Best Practices

- Use parentheses to show intent in complex expressions.
- Avoid mixing arithmetic, comparisons, and logic on one line.
- Prefer clear intermediate variables for readability.

## 8. Worked Examples

```python
# 1) What is printed?
print(2 ** 3 ** 2 / 10 // 2)
# Explanation: 3 ** 2 = 9; 2 ** 9 = 512; 512 / 10 = 51.2; 51.2 // 2 = 25.0

# 2) Why does this not call has_perm() sometimes?
if ready and has_perm():
    do_work()
# because of short-circuiting: if ready is False, has_perm is not evaluated
```

## 9. Exercises

1) Predict results without running:
```python
3 * 2 ** 3
not 0 == 0
(5 and 0) or ("" or 7)
1 < 2 < 2 < 3
```

2) Add parentheses so the intent is unambiguous:
```python
total - discount / qty or 1
```

3) Rewrite with chained comparisons:
```python
if a > 0 and a < 10: ...
```

```{admonition} Answers
:class: dropdown
1) 24, False, 7, False  
2) `( (total - discount) / (qty or 1) )`  
3) `if 0 < a < 10: ...`
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
