# Lesson 3 — Solutions

## 1. Var(X+Y) and Var(X-Y) with Cov = 2

    Var(X + Y) = 4 + 9 + 2(2) = 17
    Var(X - Y) = 4 + 9 - 2(2) = 9

In Lesson 1 they were equal because independence forced `Cov = 0`, killing the
cross term. With positive covariance the two variables tend to rise and fall
together, so adding them amplifies the swings (17) while subtracting them
cancels some of the shared movement (9).

## 2. X a fair die, Y = X + 1

Use `Cov(aX + b, cY + d) = ac Cov(X, Y)` with `Y = X + 1`:

    Cov(X, X + 1) = 1 * 1 * Cov(X, X) = Var(X) = 35/12

For the correlation, adding a constant does not change spread, so
`SD(Y) = SD(X)`:

    Corr = Cov/(SD(X) SD(Y)) = Var(X)/Var(X) = 1

Exactly 1, which is right: `Y` is a perfect increasing linear function of `X`.
Correlation measures linear relationship, and this one is as linear as it gets.

## 3. Cov(2X + 3, 4Y - 1)

    = (2)(4) Cov(X, Y) = 8 * 2 = 16

The `+3` and `-1` contribute nothing. Shifting a variable never changes how it
co-varies with anything, for the same reason shifting never changes variance.

## 4. X on {-2, 0, 2}, Y = X^2

    E[X]  = (-2 + 0 + 2)/3 = 0
    E[XY] = E[X^3] = (-8 + 0 + 8)/3 = 0
    Cov   = E[XY] - E[X]E[Y] = 0 - (0)(E[Y]) = 0

`X` and `Y` are not independent because knowing `X` tells you `Y` exactly
(`Y = X^2`, so `X = -2` forces `Y = 4`). Covariance is blind here because the
relationship is symmetric: the negative side contributes exactly as much as
the positive side, and they cancel. Correlation only sees straight lines.

## 5. FPC with N = 1000, sigma = 20, n = 100

Without the correction:

    SD(Xbar) = sigma/sqrt(n) = 20/10 = 2

With it:

    fpc = (N - n)/(N - 1) = 900/999 = 0.9009
    Var(Xbar) = (400/100)(0.9009) = 4(0.9009) = 3.6036
    SD(Xbar)  = sqrt(3.6036) = 1.898

Reduction: `(2 - 1.898)/2 = 5.1%`.

Note the fpc multiplies the **variance**, so the SD picks up only its square
root -- `sqrt(0.9009) = 0.949`. Sampling 10% of the population bought about a
5% reduction in standard error. Real, but modest.

## 6. Why population size barely matters

Population size `N` enters the answer through exactly one place: the factor
`(N - n)/(N - 1)`. Once `N` is much larger than `n`, that ratio sits
essentially at 1 and drops out, leaving `sigma/sqrt(n)` -- which contains no
`N` at all.

    city, N = 100,000:      fpc = 98,400/99,999 = 0.984   (SE cut ~0.8%)
    country, N = 300 mil:   fpc = 0.9999947             (SE cut ~0.0003%)

Both are effectively 1, so both polls have essentially the same margin of
error. Precision is bought with **sample size**, not with a large slice of the
population.

Intuition: a spoonful is enough to tell whether soup is salty, and it does not
matter whether the pot or the bathtub it came from is larger -- as long as you
stirred (that is, as long as the sample is genuinely random).
