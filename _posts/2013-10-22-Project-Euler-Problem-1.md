---
layout: post
title: Project Euler Problem 1: Multiples of 3 and 5
date: 2013-10-22
---

[Project Euler Problem 1: Multiples of 3 and 5](https://projecteuler.net/problem=1)
> **Problem Description**
> 
> If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
> Find the sum of all the multiples of 3 or 5 below 1000.

**Approach**

This is a fairly straight-forward problem. In python, you can obtain the answer by a single line of code using list comprehension:

```python
print(sum([n for n in range(1, 1000) \
           if any(n % factor == 0 for factor in (3, 5))]))
```
