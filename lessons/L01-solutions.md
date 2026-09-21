# Lesson 1 — Solutions

## 1. Three fair coin flips

`X ~ Binomial(3, 1/2)`.

**(a) From the full distribution.**

    P(X=0) = 1/8,  P(X=1) = 3/8,  P(X=2) = 3/8,  P(X=3) = 1/8

    E[X]   = 0(1/8) + 1(3/8) + 2(3/8) + 3(1/8) = 12/8 = 1.5
    E[X^2] = 0(1/8) + 1(3/8) + 4(3/8) + 9(1/8) = 24/8 = 3
    Var(X) = 3 - (1.5)^2 = 3 - 2.25 = 0.75

**(b) Indicator shortcut.** Let `Xi = 1` if flip `i` is heads. Each `Xi` is
Bernoulli(1/2), so `E[Xi] = 0.5` and `Var(Xi) = (0.5)(0.5) = 0.25`.

    E[X]   = 0.5 + 0.5 + 0.5 = 1.5
    Var(X) = 0.25 + 0.25 + 0.25 = 0.75     (adding variances is legal:
                                            the flips are independent)

They agree. Method (b) is the one that still works when `n = 400`.

## 2. Biased coin, p = 0.3

    E[X]  = 0.3
    Var(X)= (0.3)(0.7) = 0.21
    SD(X) = sqrt(0.21) = 0.458

## 3. Y = 5X + 2

    E[Y]   = 5(4) + 2 = 22
    Var(Y) = 5^2 * 9 = 225        (the "+2" contributes nothing)
    SD(Y)  = 15                   (= 5 * SD(X) = 5 * 3)

## 4. Poll of 400, p = 0.6

`X ~ Binomial(400, 0.6)`, so `E[X] = 240` and `Var(X) = 400(0.6)(0.4) = 96`.
Since `phat = X/400`, use `E[aX] = aE[X]` and `Var(aX) = a^2 Var(X)` with
`a = 1/400`:

    E[phat]   = 240/400 = 0.6                    <-- unbiased
    Var(phat) = 96 / 400^2 = 0.0006
    SD(phat)  = sqrt(0.0006) = 0.0245

Worth storing as a formula: `SD(phat) = sqrt(p(1-p)/n)`.

Interpretation: a poll of 400 gives a sample proportion typically about
2.5 percentage points off the truth. Multiply by 2 and you have the "+/- 5%
margin of error" you see reported in the news. You just derived it.

## 5. Var(X - Y)

    Var(X - Y) = Var(X) + Var(Y) = 4 + 9 = 13

Why "-5" is wrong before any algebra: variance is defined as the average of
*squared* deviations, so it can never be negative. Any time your variance comes
out negative, you've made an algebra error — this is a free sanity check on
exams, so use it.

The deeper point: the minus sign gets squared away by
`Var(-Y) = (-1)^2 Var(Y) = Var(Y)`. Noise never cancels noise.

## 6. E[1/X] vs 1/E[X]

Let `X = 1` or `X = 2`, each with probability 1/2.

    E[X]     = 1.5          so   1/E[X] = 2/3 = 0.667
    E[1/X]   = (1/2)(1/1) + (1/2)(1/2) = 0.5 + 0.25 = 0.75

`0.75 != 0.667`, so the claim is false.

This is the same trap as `E[X^2] != (E[X])^2`. The general rule: expectation
passes through **linear** functions only (`aX + b`). It does not pass through
squares, reciprocals, logs, or square roots. Keep this loaded — in chapter 8
you'll take logs of likelihoods and the distinction matters immediately.
