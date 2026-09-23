# Lesson 3 — Covariance, Correlation, and Dependent Draws

## Why this is next

Lesson 1 gave you a rule with a condition attached:

    Var(X + Y) = Var(X) + Var(Y)      ONLY IF X and Y are independent

Every standard error you have computed so far leaned on that condition. But
real survey sampling **violates it**. When you poll 1600 people you sample
*without replacement* -- once a person is chosen they cannot be chosen again --
and that makes the draws slightly dependent on each other.

So before chapter 7 you need the version of the rule with no condition
attached. That is what covariance provides.

---

## 3.1 Covariance

    Cov(X, Y) = E[ (X - mu_X)(Y - mu_Y) ]

Read it literally: when `X` is above its mean, is `Y` also tending to be above
its mean? If yes, both factors are usually positive, the product is positive,
and the average is positive. If `Y` tends to go the *other* way, one factor is
positive while the other is negative, the product is negative, and so is the
average.

    Cov > 0   they tend to move together
    Cov < 0   they tend to move in opposite directions
    Cov = 0   no LINEAR tendency either way

**Shortcut formula** (same spirit as `Var(X) = E[X^2] - (E[X])^2`):

    Cov(X, Y) = E[XY] - E[X]E[Y]

**Variance is a special case of covariance:**

    Cov(X, X) = E[X^2] - (E[X])^2 = Var(X)

That is not a coincidence -- variance is "how much X moves with itself." Keep
it in mind; it makes several formulas below obvious instead of memorized.

---

## 3.2 The general variance rule

    Var(X + Y) = Var(X) + Var(Y) + 2 Cov(X, Y)
    Var(X - Y) = Var(X) + Var(Y) - 2 Cov(X, Y)

If `X` and `Y` are independent then `Cov(X, Y) = 0` and both collapse to the
Lesson 1 rule. **The old rule was the special case; this is the real one.**

For a sum of many variables:

    Var(X1 + ... + Xn) = sum_i Var(Xi)  +  2 * sum_{i<j} Cov(Xi, Xj)

The first sum has `n` terms; the second has `n(n-1)/2` pairs. When the
variables are independent the entire second piece vanishes, which is exactly
why independence made life so easy.

**Useful property** (constants slide out, shifts do nothing):

    Cov(aX + b, cY + d) = ac * Cov(X, Y)

---

## 3.3 Correlation

Covariance has ugly units -- if `X` is in dollars and `Y` in inches, `Cov` is
in dollar-inches, which means nothing. Divide the units away:

    rho = Corr(X, Y) = Cov(X, Y) / ( SD(X) * SD(Y) )

This is always between **-1 and +1**, regardless of the variables. `rho = +1`
means a perfect increasing straight-line relationship, `rho = -1` a perfect
decreasing one, `rho = 0` no linear relationship.

### The trap: zero correlation does NOT mean independent

    independent  =>  Cov = 0        TRUE
    Cov = 0      =>  independent    FALSE

Counterexample: let `X` be equally likely `-1, 0, 1`, and let `Y = X^2`.

    E[X]  = 0
    E[XY] = E[X^3] = (-1 + 0 + 1)/3 = 0
    Cov   = E[XY] - E[X]E[Y] = 0 - 0 = 0

Zero covariance. Yet `Y` is completely determined by `X` -- they could not
possibly be more dependent. Correlation only detects **linear** association; a
perfect symmetric parabola is invisible to it.

There is one important exception: if `X` and `Y` are **jointly normal**, then
zero correlation DOES imply independence. That special case shows up in
chapter 14 regression.

---

## 3.4 The payoff: sampling without replacement

Now the chapter 7 setup. A population of `N` units has fixed values
`x1, ..., xN`, with

    mu    = (1/N) * sum xi              (population mean)
    sigma^2 = (1/N) * sum (xi - mu)^2   (population variance)

Take a **simple random sample without replacement** of size `n`, giving draws
`X1, ..., Xn`. Any single draw is a uniform pick from the population, so

    E[Xi] = mu        Var(Xi) = sigma^2

But the draws are **not independent**: a unit that comes out on draw 1 cannot
come out again on draw 2.

### Finding the covariance with one slick argument

Imagine drawing the *entire* population, all `N` units. Then

    X1 + X2 + ... + XN = x1 + ... + xN = N*mu

which is a **constant** -- the same every time, no randomness at all. A
constant has variance zero. So apply the general variance rule to it, writing
`c` for the common pairwise covariance (all pairs are equivalent by symmetry):

    0 = Var(X1 + ... + XN) = N*sigma^2 + N(N-1)*c

    =>  c = Cov(Xi, Xj) = -sigma^2 / (N - 1)

**Negative**, as intuition demanded: drawing a large value removes it from the
pool, making the remaining draws lean smaller.

### The variance of the sample mean

    Var(X1 + ... + Xn) = n*sigma^2 + n(n-1)*c
                       = n*sigma^2 - n(n-1)*sigma^2/(N-1)
                       = n*sigma^2 * [ 1 - (n-1)/(N-1) ]
                       = n*sigma^2 * (N - n)/(N - 1)

Divide by `n^2`:

    Var(Xbar) = (sigma^2 / n) * (N - n)/(N - 1)

The extra factor is the **finite population correction (fpc)**:

    fpc = (N - n)/(N - 1)

Your familiar `sigma^2/n`, multiplied by something slightly less than 1.

### Three sanity checks

- **n = 1:** fpc = `(N-1)/(N-1)` = 1, so `Var = sigma^2`. Correct -- one draw
  is just one draw.
- **n = N (a census):** fpc = 0, so `Var(Xbar) = 0`. You measured every single
  member of the population, so there is nothing left to be uncertain about.
  The formula knows this.
- **N enormous compared to n:** fpc is essentially 1, and we are back to plain
  `sigma^2/n`.

### The famous consequence

That third case is why a poll of 1600 people has essentially the same accuracy
for a city of 100,000 as for a country of 300 million:

    N = 100,000:      fpc = 98,400/99,999    = 0.984
    N = 300,000,000:  fpc = 0.99999...       = 1.000

**The precision of a survey depends on the sample size, not on the population
size.** Almost everyone finds this false when they first hear it. The reason
is now visible in the algebra: population size only enters through the fpc,
and the fpc is pinned near 1 unless you are sampling a serious fraction of the
whole population.

---

## 3.5 Conditional expectation (short version)

`E[X | Y = y]` is just the mean of `X` computed within the slice of the world
where `Y` happens to equal `y`. It is an ordinary expectation, taken against
the conditional distribution instead of the full one.

The one fact to carry forward is the **law of total expectation** (the "tower
property"):

    E[X] = E[ E[X | Y] ]

In words: to get an overall average, average within each group, then average
those group averages (weighted by how likely each group is). That is exactly
how stratified sampling works in chapter 7, and it reappears in chapter 8 for
sufficiency. We will go deeper when the course needs it.

---

## Practice

1. `Var(X) = 4`, `Var(Y) = 9`, `Cov(X, Y) = 2`. Find `Var(X + Y)` and
   `Var(X - Y)`. Why are they different now when they were equal in Lesson 1?

2. `X` is a fair die roll and `Y = X + 1`. Find `Cov(X, Y)` and `Corr(X, Y)`.
   (Use the `Cov(aX+b, cY+d)` property -- no summation needed. Recall
   `Var(die) = 35/12`.)

3. `Cov(X, Y) = 2`. Find `Cov(2X + 3, 4Y - 1)`.

4. Let `X` be equally likely `-2, 0, 2` and let `Y = X^2`. Show `Cov(X,Y) = 0`,
   then explain in one sentence why `X` and `Y` are obviously not independent.

5. A population has `N = 1000` and `sigma = 20`. You take an SRS **without
   replacement** of size `n = 100`. Compute `SD(Xbar)` both with and without
   the fpc. By what percentage does the fpc reduce it?

6. In one or two sentences of your own words: why does polling 1600 people
   give roughly the same margin of error for a city of 100,000 as for a
   country of 300 million? Point at the specific piece of the formula.
