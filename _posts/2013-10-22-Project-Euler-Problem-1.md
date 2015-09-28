---
layout: post
title: Project Euler Problem 1
date: 2013-10-22
---

**[Project Euler Problem 1: Multiples of 3 and 5](https://projecteuler.net/problem=1)**
---------------------------------------------------------------------------------------

> **Problem Description**
> 
> If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
>
> Find the sum of all the multiples of 3 or 5 below 1000.

**Approach**
------------

This is a fairly straight-forward problem. In python, you can obtain the answer by a single line of code using list comprehension:

```python
print(sum([n for n in range(1, 1000) \
           if any(n % factor == 0 for factor in (3, 5))]))
```

This is basically a direct translation of the problem: pick numbers from 1 to 1000 (non-inclusive) which are divisible by either 3 or 5, and sum them up. One possible pitfall here is that 1000 is not to be included in the range. Incidentally, `range(1, 1000)` in Python stops just before 1000, so no need to change the code.

**Code**
--------

For a bit of generalization, the code can be expanded to accept a set of factors rather than 3 and 5:

```python
def sum_multiples(limit, factors):
    return sum([n for n in range(1, limit) \
                if any(n % factor == 0 for factor in factors)])

if __name__ == "__main__":
    limit = 1000
    factors = (3, 5)
    print("Sum of multiples of {0} below {1}: {2:,}".format(
          factors, limit, sum_multiples(limit, factors)
         ))
```
