---
title: Numeric Precision — Deep Dive
description: Floating-point representation, rounding pitfalls, exact decimals, tolerant comparisons, and money-safe patterns.
tags: [python, floating-point, decimal, rounding, money, isclose]
---

# Numeric Precision — Deep Dive

## 1. Why Floats Drift

Binary floats cannot represent many decimal fractions exactly:
```python
0.1 + 0.2 == 0.3  # False
```

## 2. Strategies by Use Case

### Display-Only
```python
value = 12.34567
print(f"{value:.2f}")   # 12.35 (rounded for presentation)
```

### Tolerant Comparisons
```python
import math
math.isclose(0.1 + 0.2, 0.3, rel_tol=1e-9, abs_tol=0.0)
```

### Exact Decimals (Money)
Use `decimal.Decimal` end-to-end; avoid mixing with floats.
```python
from decimal import Decimal, getcontext
getcontext().prec = 28
price = Decimal("1.10")
tax   = Decimal("0.20")
total = price + tax
```

### Modulo and Division with Negatives
```python
-7 // 2  # -4
-7 % 2   # 1
```

## 3. Patterns and Anti-Patterns

- ✅ Use `Decimal` for currency, VAT, invoices.
- ✅ Use `isclose` for scientific/engineering comparisons.
- ❌ Do not compare floats with `==` directly.
- ❌ Do not mix `Decimal` and `float` in the same calculation.

## 4. Exercises

1) Implement a function that compares two floats with a default tolerance.  
2) Sum a list of string prices **exactly** and print with two decimals.  
3) Explain why `round(2.675, 2)` prints `2.67`.

```{admonition} Answers
:class: dropdown
1) 
```python
import math
def feq(a, b, rel=1e-9, abs_=0.0):
    return math.isclose(a, b, rel_tol=rel, abs_tol=abs_)
```
2)
```python
from decimal import Decimal
total = sum(Decimal(x) for x in ["1.10", "2.20", "3.30"])
print(f"{total:.2f}")
```
3) 2.675 is not exactly representable in binary; rounding happens on the closest representable float.
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
