# Lesson 2 — Debrief (round 1)

## THE question to ask before every normal problem

> **Is this about ONE individual draw, or about an AVERAGE of n draws?**

    ONE individual      ->  use  sigma
    AVERAGE of n draws  ->  use  sigma/sqrt(n)

Same symbol `sigma` in the problem statement, two different numbers to divide
by. Getting this wrong is the #1 point-loser in chapters 7-9, because every
confidence interval and test statistic divides by a standard error, and the
standard error is almost always the `sigma/sqrt(n)` version.

I wrote `SD(Xbar) = 3` for a sample of 36. That is the SD of **one person**.
The question asked about the **average of 36 people**:

    SD(Xbar) = sigma/sqrt(n) = 3/sqrt(36) = 3/6 = 0.5

Averaging 36 people shrank the spread by a factor of 6. That shrinkage IS the
value of collecting data -- if averaging did not reduce spread, there would be
no reason to sample more than one person.

## The 6-step recipe for any normal probability

1. **Which variable?** One draw or an average? Fixes whether you use `sigma`
   or `sigma/sqrt(n)`.
2. **Write its mean and SD.**
3. **Draw the bell.** Mark the mean in the center, mark the cutoff value.
4. **Shade** the region the question asks for.
5. **Convert the cutoff to a z-score:** `z = (value - mean)/SD`, using the SD
   from step 2.
6. **Read the area** off 68-95-99.7 (or a table), then **check direction**:
   does the shaded piece look bigger or smaller than half the bell?

Step 6 catches almost everything. Also: **z-scores are essentially always
between -3 and +3.** I answered `z = 15` on one problem, which would mean 15
standard deviations above average -- rarer than one in a billion billion. If a
z-score comes out huge, the arithmetic is wrong.

## The area breakdown worth memorizing

Rather than just "68-95-99.7", memorize the six slices:

    2.5%   13.5%    34%  |  34%    13.5%   2.5%
    ---+------+-------+--+--+-------+------+---
     mu-3s  mu-2s  mu-1s mu mu+1s  mu+2s  mu+3s

With these you can answer almost any 68-95-99.7 question by adding slices:

    P(X > mu + 1 SD) = 13.5 + 2.5 = 16%
    P(X > mu + 2 SD) = 2.5%
    P(mu - 1s < X < mu + 2s) = 34 + 34 + 13.5 = 81.5%

## Mistake: reporting a number from the problem instead of computing

For `X = 130` with `mu = 100, sigma = 15` I answered `z = 15`. But 15 is
`sigma` -- a number handed to me in the problem, not a computed result.

    z = (130 - 100)/15 = 30/15 = 2

In words: 130 sits 30 points above average, and one SD is worth 15 points, so
130 is 2 SDs up. A z-score always answers "how many SDs from the mean," so the
answer should feel like a small count.

## Mistake: "greater than" does not mean 50%

I answered `P(Xbar > 65) = 50%`. That would only be true if 65 were the mean.
The mean is 64, so 65 is above it, so the answer MUST be under 50% -- no
computation needed to know that.

    P(X > mean)          = 50%   exactly
    P(X > something above the mean) < 50%
    P(X > something below the mean) > 50%

Use this as a direction check on every single normal problem.

## The two worked problems

**IQ, N(100, 15^2), P(X > 115).** 115 = mu + 1 sigma, so read off the slices
to the right of `mu + 1s`: `13.5 + 2.5 = 16%`.

**Heights, mu=64, sigma=3, n=36, P(Xbar > 65).**

    Step 1: about an AVERAGE   -> SD = sigma/sqrt(n)
    Step 2: mean 64, SD = 3/6 = 0.5
    Step 5: z = (65 - 64)/0.5 = 2
    Step 6: P(Z > 2) = 2.5%    (under half -- direction check passes)

**The contrast that matters.** For ONE person, `z = (65-64)/3 = 0.33`, giving
about 37%. So one person over 65 inches is completely unremarkable, but an
*average of 36 people* over 65 inches happens only 2.5% of the time.

That gap is the entire basis of statistical evidence. Individuals are noisy;
averages are not. When a study reports a surprising average, it is surprising
precisely because `sigma/sqrt(n)` made the bell narrow.
