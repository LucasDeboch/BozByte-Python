---
title: Comparison Operators — Deep Dive
description: Equality vs identity, ordering, chained comparisons, tuple comparison, and robust patterns.
tags: [python, comparison, equality, ordering, chained, tuple-comparison]
---

# Comparison Operators — Deep Dive

## 1. Equality vs Identity (review)

- `==` compares **values**
- `is` compares **object identity** (same object in memory)
- Use `is None` / `is not None` for `None` checks.

## 2. Ordering Operators

`< <= > >=` compare numbers and strings (lexicographic). Mixed incompatible types raise `TypeError`.

```python
"apple" < "banana"  # True
```

## 3. Chaining

```python
0 <= x < 10 < y
a == b == c         # all equal
```

## 4. Tuple and Sequence Comparison

Python compares element-by-element:
```python
(1, 2, 3) < (1, 3, 0)   # True (compares at first differing element)
```

## 5. Robust Patterns

- Prefer tolerant comparison for floats: `math.isclose(a, b)`
- For multiple conditions, chain when readable, else split lines.

## 6. Exercises

1) Predict:
```python
(1, 2) < (1, 2, 0)
"Ada" < "Adam"
```

2) Implement a safe float comparison for currency amounts.

```{admonition} Answers
:class: dropdown
1) True, True  
2) `math.isclose(a, b, rel_tol=1e-9, abs_tol=Decimal("0.00"))` (or use Decimal arithmetic end-to-end)
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
