# Lesson 1 — Random Variables, Expectation, Variance

## Why this is first

Nearly every procedure in Stat 135 has the same shape:

1. Collect data.
2. Squeeze the data into one number (an *estimate*).
3. Ask: how far off is that number likely to be?

Step 3 is a variance question, and step 2 is an expectation question. So
expectation and variance are not review material you get past — they *are* the
course. Everything else this semester is decoration on top of them.

---

## 1.1 What a random variable is

A **random variable** is just a number whose value depends on chance.

- `X` = the result of one die roll
- `X` = 1 if a randomly chosen voter says "yes", 0 otherwise
- `X` = the height of a randomly chosen student

Notation convention, which trips up everyone: **capital `X`** is the random
thing *before* you look; **lowercase `x`** is one particular value it landed on.
When a textbook writes `P(X = x)` it means "the chance that the random thing
turns out to equal this specific number."

The **distribution** of `X` is the complete bookkeeping of what values `X` can
take and how likely each is.

**Discrete** (countable list of values): described by a probability mass
function `p(x) = P(X = x)`. All values are >= 0 and they sum to 1.

**Continuous** (a whole interval of values): described by a density `f(x)`,
where `P(a <= X <= b)` is the *area* under `f` from `a` to `b`. For a
continuous variable `P(X = x) = 0` for every single point — probability is
area, not height.

Two distributions you must know cold, because 135 uses them constantly:

- **Bernoulli(p):** `X = 1` with probability `p`, `X = 0` with probability
  `1 - p`. One yes/no trial.
- **Binomial(n, p):** `X` = number of 1s in `n` independent Bernoulli(p)
  trials.

---

## 1.2 Expectation

**`E[X]` is the weighted average of the values, weighted by their
probabilities.** That's the whole idea.

    Discrete:    E[X] = sum over x of  x * P(X = x)
    Continuous:  E[X] = integral of    x * f(x) dx

**Example (die).**

    E[X] = 1(1/6) + 2(1/6) + 3(1/6) + 4(1/6) + 5(1/6) + 6(1/6) = 21/6 = 3.5

Notice 3.5 is impossible to roll. Expectation is a *center of mass*, not a
prediction. If you picture the probability histogram as physical weights on a
plank, `E[X]` is where the plank balances.

**Example (Bernoulli).**

    E[X] = 1*p + 0*(1-p) = p

Memorize this one: **the mean of a 0/1 indicator is the probability of the
event.** An enormous amount of Stat 135 is this fact plus bookkeeping.

**Functions of X.** To get `E[g(X)]` you do *not* need to work out the
distribution of `g(X)`. Just reuse the same weights:

    E[g(X)] = sum over x of  g(x) * P(X = x)

In particular `E[X^2] = sum of x^2 * p(x)`, which you'll need in a moment.

**Warning:** in general `E[g(X)]` is NOT `g(E[X])`. Averaging and squaring
don't commute. This is the single most common error on 135 exams.

---

## 1.3 Linearity — the workhorse

    E[aX + b] = a E[X] + b
    E[X + Y]  = E[X] + E[Y]        <-- ALWAYS true, no independence needed

The second one holds even when `X` and `Y` are tangled up with each other.
That is unusual and extremely useful. Extending it:

    E[X1 + X2 + ... + Xn] = E[X1] + E[X2] + ... + E[Xn]

**Payoff (binomial mean).** Let `X ~ Binomial(n, p)`. Writing out
`sum k * C(n,k) p^k (1-p)^(n-k)` is miserable. Instead write
`X = X1 + ... + Xn` where each `Xi` is a Bernoulli(p) indicator for trial `i`.
Then

    E[X] = E[X1] + ... + E[Xn] = p + p + ... + p = np

Breaking a count into a sum of indicators is a technique you will use all
semester. Learn the move, not just the answer.

---

## 1.4 Variance

Expectation says where the distribution sits. **Variance says how spread out
it is.**

    Var(X) = E[(X - mu)^2],   where mu = E[X]

In words: the average squared distance from the center.

Why squared? Because the plain average deviation `E[X - mu]` is exactly 0 for
every random variable — the positives and negatives cancel. Squaring kills the
cancellation.

The square root puts you back in the original units:

    SD(X) = sqrt(Var(X))

Rule of thumb for the semester: **compute with variance, report standard
deviation.** Variance has the clean algebra; SD is the one that's interpretable
(it's in dollars, or inches, or percentage points).

**The shortcut formula** — you will use this hundreds of times:

    Var(X) = E[X^2] - (E[X])^2

**Example (die).**

    E[X^2] = (1 + 4 + 9 + 16 + 25 + 36)/6 = 91/6 = 15.1667
    E[X]   = 3.5,  so (E[X])^2 = 12.25
    Var(X) = 15.1667 - 12.25 = 2.9167  (= 35/12)
    SD(X)  = 1.71

**Example (Bernoulli).** Since `0^2 = 0` and `1^2 = 1`, the variable `X^2` is
identical to `X`, so `E[X^2] = p`. Therefore

    Var(X) = p - p^2 = p(1 - p)

This is largest at `p = 0.5` and shrinks to 0 as `p` approaches 0 or 1 — which
makes sense: a coin that almost always lands heads is barely random at all.

---

## 1.5 Variance rules

    Var(aX + b) = a^2 * Var(X)

Two things to read off that. Adding a constant `b` does nothing — sliding a
distribution sideways doesn't change its spread. Multiplying by `a` multiplies
the *variance* by `a^2`, and therefore the *SD* by `|a|`.

    Var(X + Y) = Var(X) + Var(Y)      ONLY IF X and Y are independent

(In general there's an extra `+ 2 Cov(X, Y)` term; that's Lesson 3.) And the
one that looks wrong but isn't:

    Var(X - Y) = Var(X) + Var(Y)      for independent X, Y

Variances **add** even when you subtract the variables. Uncertainty can't
cancel out uncertainty — subtracting two noisy things gives you something
noisier than either. This shows up the moment you compare two groups in
chapter 11.

**Payoff (binomial variance).** Same indicator trick, now legal to add
variances because the trials are independent:

    Var(X) = p(1-p) + ... + p(1-p) = n p (1-p)

---

## 1.6 The payoff: the sample mean

This is where Lesson 1 turns into Stat 135. Let `X1, ..., Xn` be independent
draws from the same distribution ("i.i.d."), each with mean `mu` and variance
`sigma^2`. The **sample mean** is

    Xbar = (X1 + X2 + ... + Xn) / n

Here is the key mental shift: **`Xbar` is itself a random variable.** Run the
study again tomorrow, get different data, get a different `Xbar`. So it has its
own mean and its own variance, and we can compute both with the rules above.

Mean, using linearity:

    E[Xbar] = (1/n) * (mu + mu + ... + mu) = (1/n)(n mu) = mu

So on average the sample mean lands exactly on the true `mu`. We call that
**unbiased**. It's the first good property of an estimator you'll meet, and in
chapter 8 it becomes a formal definition.

Variance, using `Var(aX) = a^2 Var(X)` and independence:

    Var(Xbar) = (1/n^2) * (sigma^2 + ... + sigma^2) = (1/n^2)(n sigma^2)
              = sigma^2 / n

    SD(Xbar) = sigma / sqrt(n)

That last quantity is the **standard error** — the typical distance between
your estimate and the truth.

Read what it says. The spread of your estimate shrinks like `1/sqrt(n)`, not
like `1/n`. To cut your error in half you need **four times** the data. To cut
it to a tenth you need a hundred times the data. That `sqrt(n)` is in the
denominator of essentially every confidence interval and test statistic you
will write this semester. When you see `sigma/sqrt(n)` in chapter 7 next week,
it is not a new formula — it's this line.

---

## Practice

Try all six before looking at `L01-solutions.md`. Getting them wrong after a
real attempt teaches you more than reading a correct solution does.

1. `X` = number of heads in 3 flips of a fair coin. Find `E[X]` and `Var(X)`
   **two ways**: (a) write out the full distribution of `X` and use the
   definitions; (b) use the indicator/linearity shortcut. Confirm they agree.

2. A biased coin has `P(heads) = 0.3`. Let `X = 1` if heads, `0` if tails.
   Find `E[X]`, `Var(X)`, and `SD(X)`.

3. `E[X] = 4` and `Var(X) = 9`. Let `Y = 5X + 2`. Find `E[Y]`, `Var(Y)`,
   `SD(Y)`.

4. You poll 400 randomly chosen people; each independently supports a measure
   with probability `p = 0.6`. Let `X` = number of supporters and let
   `phat = X/400` be the sample proportion. Find `E[phat]` and `SD(phat)`.
   (This is a genuine Stat 135 answer, not a toy one.)

5. `X` and `Y` are independent with `Var(X) = 4`, `Var(Y) = 9`. Find
   `Var(X - Y)`. Then explain in one sentence why the answer "-5" is wrong on
   its face, before doing any algebra.

6. Someone claims `E[1/X] = 1/E[X]`. Build a counterexample using a variable
   that takes just two values with probability 1/2 each.
