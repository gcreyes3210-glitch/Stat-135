# Lesson 2 — The Normal Curve, the LLN, and the Central Limit Theorem

## Why this is next

Lesson 1 ended with a near-miss. For `Xbar` we found:

    E[Xbar]  = mu             (where it sits)
    SD(Xbar) = sigma/sqrt(n)  (how far off it typically is)

Center and spread. But you cannot yet say "I am 95% confident the truth is in
this range," because a center and a spread do not pin down **shape**. Is the
distribution of `Xbar` a bell? A lump? Two humps?

Lesson 2 supplies the shape -- and the astonishing part is that the answer is
the same no matter what the underlying population looks like.

---

## 2.1 The normal distribution

The normal (Gaussian) distribution is the bell curve. Its density is

    f(x) = 1/(sigma*sqrt(2*pi)) * exp( -(x - mu)^2 / (2*sigma^2) )

Do not memorize it, and do not try to integrate it -- it has no elementary
antiderivative. That is precisely why the back of your textbook has a table:
mathematicians could not find a formula either, so the areas were computed
numerically once and tabulated forever.

What you DO need: the shape is completely determined by two numbers.

- `mu` says **where** the peak sits.
- `sigma` says **how wide** the bell is.

We write `X ~ N(mu, sigma^2)`. Note the second slot is the **variance**, not
the SD. Rice uses this convention and mixing it up is a classic exam disaster.

### The 68-95-99.7 rule

For any normal distribution:

    about 68% of the mass lies within  1 SD of the mean
    about 95% lies within              2 SD
    about 99.7% lies within            3 SD

This is worth more to you than the density formula. It lets you do most normal
problems in your head, and it lets you sanity-check anything a table tells you.

---

## 2.2 Standardization: the z-score

Every normal is a stretched, shifted copy of one master curve. To get back to
the master, subtract the mean and divide by the SD:

    Z = (X - mu) / sigma

**Why this works is pure Lesson 1.** `Z` is just a linear transformation
`aX + b` with `a = 1/sigma` and `b = -mu/sigma`, so:

    E[Z]   = (1/sigma)(mu) - mu/sigma = 0
    Var(Z) = (1/sigma)^2 * sigma^2    = 1

So `Z ~ N(0, 1)`, the **standard normal**. Those two lines are exactly the
rules you drilled in Lesson 1, doing real work.

**What a z-score means:** how many standard deviations above (or below) the
mean you are. `z = 2` means "two SDs above average." That is a unit-free
statement, which is why it transfers across problems.

### Numbers to memorize

    P(|Z| < 1.645) = 90%
    P(|Z| < 1.96 ) = 95%     <-- THE number of Stat 135
    P(|Z| < 2.576) = 99%

The 1.96 is where "about 2 SDs" from the 68-95-99.7 rule becomes exact. You
will write it hundreds of times this semester.

---

## 2.3 The Law of Large Numbers

**Statement:** as `n` grows, `Xbar` converges to `mu`.

**Why, in one line:** `Var(Xbar) = sigma^2/n`, which goes to 0 as `n` grows.
A distribution whose spread collapses to zero has nowhere to be except on top
of its center. That is the whole proof idea, and you already derived the
ingredient in Lesson 1.

**What the LLN does NOT say.** It does not say that a coin which has come up
heads 10 times in a row is now "due" for tails. Future flips are independent;
they have no memory. The proportion drifts toward 0.5 by **dilution**, not
compensation -- as `n` grows, that early surplus of 10 heads becomes a
vanishing share of the total. Nothing pushes back. This is the gambler's
fallacy and it is a standard exam question.

---

## 2.4 The Central Limit Theorem

Here is the main event.

**Statement.** Let `X1, ..., Xn` be i.i.d. with mean `mu` and variance
`sigma^2`. Then for large `n`:

    Xbar is approximately N( mu, sigma^2/n )

equivalently, standardizing:

    (Xbar - mu) / (sigma/sqrt(n))   is approximately  N(0, 1)

**Why it is a miracle.** The population can be any shape at all -- skewed,
bimodal, discrete, lumpy, hideous. Average enough draws from it and the
average is bell-shaped anyway. The original shape is erased.

**Why it is the foundation of this entire course.** In real life you never
know the population's distribution. If you needed it, statistics would be
impossible. The CLT says you do not need it: as long as you are working with
an average (and nearly every estimator in chapters 7-14 is secretly an
average), you know its approximate distribution for free.

**LLN and CLT are a pair.** LLN says where `Xbar` is heading. CLT describes
the shape of the wobble around that destination on the way there.

**Rules of thumb for "large n":**

- `n >= 30` for a roughly symmetric population; more if badly skewed.
- For a proportion, you want `n*p >= 10` AND `n*(1-p) >= 10`.

---

## 2.5 Your first confidence interval

Now the pieces snap together. Start from the CLT statement:

    P( -1.96 < (Xbar - mu)/(sigma/sqrt(n)) < 1.96 ) = 0.95

Algebraically rearrange to put `mu` in the middle:

    P( Xbar - 1.96*sigma/sqrt(n)  <  mu  <  Xbar + 1.96*sigma/sqrt(n) ) = 0.95

That is a **95% confidence interval**. The universal shape:

    estimate  +/-  1.96 * (standard error)

### Worked, using your own numbers

From Lesson 1: a poll of `n = 100` with `phat = 0.2` gave `SE = 0.04`.

    0.2  +/-  1.96 * 0.04  =  0.2 +/- 0.078   ->   (0.122, 0.278)

(Technically the SE uses the unknown true `p`; we plug in `phat`. For large
`n` that is fine, and chapter 8 formalizes why.)

### The interpretation trap

WRONG: "There is a 95% probability that the true `p` lies in (0.122, 0.278)."

The true `p` is a fixed, non-random number. It is either in that interval or
it is not -- there is no probability about it. What is random is the
**interval**: different samples give different endpoints.

RIGHT: "The procedure that produced this interval captures the true `p` for
95% of all possible samples."

The 95% is a property of the **method**, not of this one interval. Berkeley
loves asking this, and the Bayesian alternative in chapter 8 exists precisely
because this interpretation annoys people.

---

## 2.6 Where this goes

- **Chapter 7** applies exactly this to survey sampling, adding a correction
  for sampling from a finite population without replacement.
- **Chapter 9** rearranges the same inequality into hypothesis tests: instead
  of asking "what values of `mu` are plausible," ask "is this specific `mu`
  plausible?" Same algebra, different question.

Essentially every formula in the rest of the course is
`estimate +/- (critical value) * (standard error)`, or a test statistic of the
form `(estimate - hypothesized value)/(standard error)`. Learn that skeleton
now and the rest of the semester is filling in blanks.

---

## Practice

1. IQ scores are `N(100, 15^2)` (so `mu = 100`, `sigma = 15`).
   (a) Use the 68-95-99.7 rule to find `P(X > 115)`.
   (b) What z-score corresponds to `X = 130`?

2. Adult heights have `mu = 64` inches, `sigma = 3`. You sample `n = 36`
   people. Find `E[Xbar]` and `SD(Xbar)`. Then find `P(Xbar > 65)` using a
   z-score and the 68-95-99.7 rule.

3. Income in a city is heavily right-skewed (a few very rich people).
   (a) If you sample `n = 400` and average, is `Xbar` approximately normal?
   (b) What if `n = 4`? Explain the difference in one sentence each.

4. A poll of `n = 1600` finds 45% say yes. Compute `SE(phat)` and give a 95%
   confidence interval. Does your interval contain 0.5? What might that
   suggest?

5. Someone reports your interval from #4 as: "There is a 95% probability the
   true proportion is between those two numbers." Say what is wrong with it
   and restate it correctly.

6. "I have flipped 10 heads in a row. The Law of Large Numbers says tails is
   due." Explain in two sentences why this is wrong, and what the LLN actually
   claims.
