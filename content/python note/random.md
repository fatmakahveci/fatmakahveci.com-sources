---
title: random
description: random
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
---
- It implements pseudo-random number generators for various distributions, given below:

```python
import random

random.uniform(a, b) # Random float:  a <= N <= b

random.triangular(low, high, mode) # N such that low <= N <= high # mode defaults to the midpoint between the bounds, giving a symmetric distribution.

random.betavariate(alpha, beta) # beta distribution [0.0, 1.0), alpha > 0, beta > 0

random.expovariate(1 / N) # Exponential distribution. lambd is 1.0 divided by the desired mean.Interval between arrivals averaging N seconds.

random.gammavariate(alpha, beta) # Gamma distribution. (Not the gamma function!) Conditions on the parameters are alpha > 0 and beta > 0.

random.gauss(mu, sigma) # Normal (Gaussian) distribution # random.normalvariate(mu, sigma)

random.lognormvariate(mu, sigma) # Log normal distribution. If you take the natural logarithm of this distribution, you’ll get a normal distribution with mean mu and standard deviation sigma. mu can have any value, and the sigma must be greater than zero.

random.vonmisesvariate(mu, kappa) # mu is the mean angle, expressed in radians between 0 and 2*pi, and kappa is the concentration parameter, which must be greater than or equal to zero. If kappa is equal to zero, this distribution reduces to a uniform random angle over the range 0 to 2*pi.

random.paretovariate(alpha) # Pareto distribution. alpha is the shape parameter.

random.weibullvariate(alpha, beta) # Weibull distribution. alpha is the scale parameter and beta is the shape parameter.
```

## Random

- `class Random` can also be subclassed if you want to use a different basic generator of your devising: in that case, override the following methods:

### i. random()

- Return the next random floating point number in the range [0.0, 1.0)

### ii. random.seed(a=None)

- If `a` is omitted or `None`, the current system time is used, `os.urandom()`.

### iii. random.getstate()

### iv. random.setstate(state)

---

### 1. Integers

- There is a uniform selection from a range.

```python
import random

random.randrange(stop) # Integer from 0 to stop inclusive

random.randrange(start, stop[,step])
# equivalent to
random.choice(range(start, stop, step))

random.randint(a, b) # N := a <= N <= b
# equivalent to
random.randrange(a, b+1)
```

### 2. Sequences

#### i. A function to generate a random permutation of a list in-place

```python
import random

deck = 'ace two three four'.split()
random.shuffle(deck) # ['four', 'two', 'ace', 'three']
```

#### ii. A function for random sampling without replacement

```python
import random

random.choice(['win', 'lose', 'draw']) # 'draw'
random.sample([10, 20, 30, 40, 50], k=4) # [40, 10, 50, 30]
```

### 3. Floating point numbers

- Floating point numbers are numbers that contain floating decimal points.

```python
import random

random.random() # Random float:  0.0 <= x < 1.0
```

### 4. Bytes

```python
import random

random.randbytes(n) # generate n random bytes
```
