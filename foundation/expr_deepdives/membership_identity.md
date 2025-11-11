---
title: Membership and Identity — Deep Dive
description: Containment with in/not in across types; object identity rules and best practices.
tags: [python, membership, identity, containment, strings, dicts, sets]
---

# Membership and Identity — Deep Dive

## 1. Membership Across Types

- **Strings**: substring search → `"py" in "python"`
- **Lists/Tuples**: element present? → `3 in [1,2,3]`
- **Dicts**: checks **keys** → `k in mapping`
- **Sets**: O(1) avg lookup → `x in my_set`

```python
mapping = {'a': 1, 'b': 2}
'a' in mapping         # True (key)
1 in mapping.values()  # check values
```

## 2. Identity Rules

- `is`: **same object** (identity). Use for singletons: `None`, `True`, `False`.
- CPython interns some small ints/short strings → `a is b` may be True **accidentally**.

```python
a = 256; b = 256; a is b   # often True (implementation detail)
```

**Best practice**: use `==` for value, `is` only for singletons.

## 3. Exercises

1) Check if a value exists in a dict **by value** efficiently.  
2) Why does `value is None` preferred over `value == None`?

```{admonition} Answers
:class: dropdown
1) `target in mapping.values()` or invert mapping if frequent lookups.  
2) Identity is unambiguous and robust; equality may be overloaded.
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
