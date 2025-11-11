---
title: Logical Operators — Deep Dive
description: Truth tables, short-circuit returns, composing predicates, and practical idioms for and/or/not.
tags: [python, logical, boolean, short-circuit, idioms]
---

# Logical Operators — Deep Dive

## 1. Truth Tables

| A | B | `A and B` | `A or B` | `not A` |
|---|---|---|---|---|
| F | F | F | F | T |
| F | T | F | T | T |
| T | F | F | T | F |
| T | T | T | T | F |

## 2. Operand-Returning Semantics

- `A or B` returns **A** if truthy else **B**
- `A and B` returns **A** if falsey else **B**

```python
name = raw or "Guest"
first_item = items and items[0]  # None/[] gives falsey
```

## 3. Composing Predicates

```python
def ok(user):
    return user.active and (user.role in ('admin', 'editor'))
```

## 4. Guarded Evaluation

```python
config = loaded and parse(text)   # parse only if loaded is truthy
```

## 5. Common Pitfalls

- `not a == b` parses as `not (a == b)` (okay, but be explicit).
- Avoid `== True` or `== False`; rely on truthiness.

## 6. Exercises

1) Rewrite without calling `expensive()` unless needed:
```python
if cond == True and expensive():
    ...
```
2) Extract first element only if non-empty using one expression.

```{admonition} Answers
:class: dropdown
1) `if cond and expensive(): ...`  
2) `first = items and items[0]`
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
