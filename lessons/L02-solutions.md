# Lesson 2 — Solutions

## 1. IQ, N(100, 15^2)

**(a)** 115 is exactly 1 SD above the mean. The 68-95-99.7 rule says 68% lies
within 1 SD, so 32% lies outside. By symmetry half of that is above:

    P(X > 115) = 32%/2 = 16%

**(b)** `z = (130 - 100)/15 = 2`. Two SDs above the mean. (And by the same
reasoning, only about 2.5% of people are above it.)

## 2. Heights, mu = 64, sigma = 3, n = 36

    E[Xbar]  = mu = 64
    SD(Xbar) = sigma/sqrt(n) = 3/sqrt(36) = 3/6 = 0.5

Note how much tighter that is than a single person's SD of 3 -- averaging
shrank the spread by a factor of 6.

    z = (65 - 64)/0.5 = 2

So `P(Xbar > 65) = P(Z > 2)` = about **2.5%** (95% within 2 SD, 5% outside,
half of that above).

The point: one randomly chosen person being over 65 inches is unremarkable,
but an *average of 36* people exceeding 65 would be genuinely surprising.
Averages are far less variable than individuals. That gap is where statistical
evidence comes from.

## 3. Skewed income

**(a)** `n = 400`: yes, approximately normal. The CLT does not care that the
population is skewed -- with enough draws the skew washes out of the average.

**(b)** `n = 4`: no. Four draws is nowhere near enough to erase heavy skew;
the average of 4 incomes is still dragged around by the occasional huge value,
so its distribution stays right-skewed.

The CLT is a large-`n` promise, and "large" has to be judged against how ugly
the population is.

## 4. Poll of 1600, phat = 0.45

    SE(phat) = sqrt( p(1-p)/n ) = sqrt( (0.45)(0.55)/1600 )
             = sqrt( 0.2475/1600 ) = sqrt(0.00015469) = 0.0124

    95% CI:  0.45 +/- 1.96(0.0124) = 0.45 +/- 0.0244
                                   = (0.4256, 0.4744)

The interval does **not** contain 0.5. Every plausible value of the true
proportion is below half, which is evidence that the true support really is a
minority rather than a coin flip that happened to land at 45%.

That reasoning -- "is this value inside or outside my interval?" -- is
literally a hypothesis test. You just did chapter 9 without the vocabulary.

## 5. The interpretation trap

Wrong because the true proportion is a **fixed number**, not a random one. It
is either inside (0.4256, 0.4744) or it is not; there is no probability
involved. The randomness lives in the **interval**, whose endpoints change
from sample to sample.

Correct statement: "This interval was produced by a procedure that captures
the true proportion in 95% of all possible samples." The 95% describes the
method's long-run track record, not this one interval.

## 6. Gambler's fallacy

Coin flips are independent, so the next flip is 50/50 no matter what the last
ten were -- the coin has no memory and nothing "pushes back" to balance the
books.

What the LLN actually says is that the **proportion** of heads approaches 0.5
as `n` grows, and it gets there by **dilution**: after a million more flips
those 10 extra heads are a negligible share of the total. The surplus is never
cancelled, just drowned out.
