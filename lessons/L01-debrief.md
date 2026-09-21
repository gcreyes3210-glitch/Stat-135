# Lesson 1 — Debrief (my actual mistakes, first attempt)

## The root cause: "where does n come from?"

I made opposite errors on two problems:

- Problem 1 (3 coin flips): forgot to multiply by n. Wrote `E[X] = p = 1/2`
  when the answer is `3 * 1/2 = 1.5`.
- Problem 2 (one biased coin): invented an n. Wrote `Var(X) = 0.3n * 0.7`
  when there is no n -- it is a single trial, so `Var(X) = 0.21`.

**The rule:** `n` appears exactly when you are ADDING UP n separate random
things. Never for a single draw. And if you then DIVIDE the sum by n to make an
average, n comes back, this time shrinking the variance.

| quantity                        | mean | variance    |
|---------------------------------|------|-------------|
| one Bernoulli(p) trial          | p    | p(1-p)      |
| sum of n trials, X = X1+...+Xn  | np   | n p(1-p)    |
| average, phat = X/n             | p    | p(1-p)/n    |

Read down the variance column: summing makes variance grow, averaging makes it
shrink. That is the whole story of why bigger samples are better.

## Mistake 2: confusing "which trial" with "how many heads"

I wrote `E[X] = (1/3)(1+2+3) = 2` for 3 coin flips. Two bugs fused together:

1. The possible values of X are **0, 1, 2, 3** -- I dropped 0. X counts heads,
   it does not label the flips.
2. Those values are **not equally likely**, so weighting each by 1/3 is wrong.

The values of X and their probabilities are two SEPARATE lists. Always write
both out:

    X:     0     1     2     3
    P(X):  1/8   3/8   3/8   1/8      (from the 8 equally likely HHH/HHT/... )

    E[X]   = (0 + 3 + 6 + 3)/8  = 12/8 = 1.5
    E[X^2] = (0 + 3 + 12 + 9)/8 = 24/8 = 3
    Var(X) = 3 - 1.5^2 = 0.75

## Mistake 3: squaring the wrong thing

I wrote `Var(X) = 1/9 + 4/9 + 1 = 14/9`, which came from squaring each term
`x * p(x)` of the expectation sum.

Variance is NOT "the expectation computation with squares on the terms."
It is `E[(X - mu)^2]`: measure each deviation from the mean, square THAT,
then take the weighted average. Or use the shortcut `E[X^2] - (E[X])^2`,
where the probabilities stay unsquared:

    E[X^2] = sum of  x^2 * p(x)        <-- square x, NOT p(x)

## Mistake 4: stopping at symbols

On problem 3 I wrote `E[Y] = 5E[X] + 2` and `Var(Y) = 25 Var(X)`. Both rules
correct -- but I never plugged in `E[X] = 4`, `Var(X) = 9`. Finish the
arithmetic: `E[Y] = 22`, `Var(Y) = 225`, `SD(Y) = 15`.

Sanity check that costs 2 seconds: `SD(Y)` should be `5 * SD(X) = 5*3 = 15`,
and `sqrt(225) = 15`. Agreement means the two rules are consistent.

## Habit to build: disagreeing answers are a fire alarm

Two methods on problem 1 gave me 2 and 1/2. I wrote both down and moved on.
When two correct methods disagree, at least one is wrong -- that is free
error detection and I should always stop and hunt.

## Problem 4, worked (the one I skipped)

400 people, each supports independently with p = 0.6.

    one person:   E = 0.6,          Var = (0.6)(0.4) = 0.24
    X = the sum:  E[X] = 400(0.6) = 240,   Var(X) = 400(0.24) = 96
    phat = X/400: multiply by a = 1/400, so use E[aX]=aE[X], Var(aX)=a^2Var(X)

    E[phat]   = 240/400 = 0.6                 <-- unbiased
    Var(phat) = 96 / 400^2 = 0.0006
    SD(phat)  = sqrt(0.0006) = 0.0245

General formula worth memorizing: **SD(phat) = sqrt( p(1-p) / n )**

Meaning: a poll of 400 is typically off by about 2.5 percentage points.
Double it and you get the "+/- 5% margin of error" from the news.

## Problem 5, worked

    Var(X - Y) = Var(X) + Var(-Y) = Var(X) + (-1)^2 Var(Y) = 4 + 9 = 13

Why "-5" is wrong before any algebra: variance is an average of squared
things, so it can NEVER be negative. Free sanity check on every exam.

## Problem 6, worked

Let X be 1 or 2, each with probability 1/2.

    1/E[X] = 1/1.5              = 0.667
    E[1/X] = (1/2)(1) + (1/2)(1/2) = 0.75

Not equal. Expectation passes through linear functions (`aX + b`) ONLY --
never through squares, reciprocals, logs, or square roots.
