---
title: Assignment and Augmented Assignment — Deep Dive
description: Binding, unpacking, walrus operator, augmented ops with mutability semantics, and idioms.
tags: [python, assignment, unpacking, augmented, walrus, mutability]
---

# Assignment and Augmented Assignment — Deep Dive

## 1. Binding and Rebinding
```python
x = 1
x = x + 1
```

## 2. Unpacking and Starred Targets
```python
a, b = 1, 2
a, b = b, a
first, *rest = [10, 20, 30, 40]
head, *_, tail = [1, 2, 3, 4, 5]
```

## 3. Augmented Assignment (`+=`, `*=`, ...)

- Immutable types create new objects:
```python
s = "a"; s += "b"   # new string
```
- Mutable types may mutate **in place**:
```python
lst = [1, 2]; lst += [3]  # same list, extended
```

## 4. Walrus Operator `:=` (Assignment Expression)
Bind and use in one expression:
```python
while (line := f.readline()):
    handle(line)
if (m := pattern.search(text)):
    print(m.group(0))
```

## 5. Exercises

1) Swap three variables `a, b, c` so that `a←b, b←c, c←a` in one line.  
2) Extend `lst` with `[4,5]` without creating a new list object.  
3) Read chunks from a stream until empty with a single `while` line.

```{admonition} Answers
:class: dropdown
1) `a, b, c = b, c, a`  
2) `lst += [4, 5]` (or `extend`)  
3) `while (chunk := stream.read(4096)): ...`
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
