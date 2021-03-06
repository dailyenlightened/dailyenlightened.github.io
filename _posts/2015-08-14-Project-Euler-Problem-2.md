---
layout: post
title: Project Euler Problem 2 
date: 2015-08-14
---

**[Project Euler Problem 2: Even Fibonacci numbers ](https://projecteuler.net/problem=2)**
---------------------------------------------------------------------------------------

> **Problem Description**
> 
> Each new term in the Fibonacci sequence is generated by adding the previous two terms. By starting with 1 and 2, the first 10 terms will be:
>
> 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, …
>
> By considering the terms in the Fibonacci sequence whose values do not exceed four million, find the sum of the even-valued terms.

**Approach**
------------

Is there a way to find out only even Fibonacci numbers?

First, let’s check the parity of Fibonacci numbers.

`\(F_1 = 1\)` (odd)

$$\Sigma_n=1^10 n^2 = n^4$$

$F2 = 1$ (odd)

`$F3 = 1 + 1 = 2$` (odd + odd = even)

F4 = 1 + 2 = 3 (odd + even= odd)

F5 = 2 + 3 = 5 (even + odd = odd)

F6 = 3 + 5 = 8 ( odd + odd = even)

…

Note that at F5, two consecutive numbers are odd, which is the same pattern in the beginning. So the odd-odd-even pattern will continue on and on.

Therefore, we only need to sum up every third numbers in the Fibonacci sequence to solve the problem. Or, we can devise a formula to find out the next even number.

Suppose a Fibonacci number Fn is an even number. Then, Fn+3 is the next even number.

Fn+1 = Fn-1 + Fn
Fn+2 = Fn + Fn+1 = Fn + (Fn-1 + Fn) = Fn-1 + 2 * Fn
Fn+3 = Fn+1 + Fn+2 = (Fn-1 + Fn) + (Fn-1 + 2 * Fn) = 2 * Fn-1 + 3 * Fn
Fn+4 = Fn+2 + Fn+3 = (Fn-1 + 2Fn) + (2Fn-1 + 3Fn) = 3 * Fn-1 + 5 * Fn
Fn+5 = Fn+3 + Fn+4 = (2Fn-1 + 3Fn) + (3Fn-1 + 5Fn) = 5 * Fn-1 + 8 * Fn
Fn+6 = Fn+4 + Fn+5 = (3Fn-1 + 5Fn) + (5Fn-1 + 8Fn) = 8 * Fn-1 + 13 * Fn

Now, we want to have a way to express Fn+6 with Fn and Fn+3, so that we can have a recurrence relation of even Fibonacci numbers. Note:

Fn+3 = 2 * Fn-1 + 3 * Fn
-> Fn-1 = (Fn+3 -3 * Fn) / 2

We plug this in to the formula for Fn+6:

Fn+6 = 8 * Fn-1 + 13 * Fn = 8 * (Fn+3 - 3 * Fn) / 2 + 13 * Fn = 4Fn+3 + Fn

So the recurrent relation for even Fibonacci numbers G is:
G0 = 0
G1 = 2
Gn+1 = 4 * Gn + Gn-1

**Code**
--------

The code is more or less direct implementation of the formula.

```python
def even_fib(max_n=float("inf")):
    even_fib_prev = 0
    even_fib_current = 2

    while True:
        yield even_fib_current

        even_fib_next = 4 * even_fib_current + even_fib_prev
        if even_fib_next > max_n:
            return None

        even_fib_prev = even_fib_current
        even_fib_current = even_fib_next

if __name__ == "__main__":
    max_n = 4000000
    print("Sum of even Fibonacci numbers upto {0:,}: {1:,}".format(
          max_n, sum(even_fib(max_n)
    )))
```
