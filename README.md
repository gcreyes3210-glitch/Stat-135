# Stat 135 — Study Notes

Rebuilding Stat 134 foundations while learning Stat 135 (Rice, *Mathematical
Statistics and Data Analysis*, 3rd ed., ch. 7, 8, 9, 11, 12, 13, 14).

One lesson at a time. Do the practice problems before reading the solutions.

## Roadmap

### Phase 0 — Stat 134 rebuild (the parts 135 actually uses)
- [x] **L1** Random variables, expectation, variance
- [x] **L2** Named distributions, the normal curve, LLN and the CLT
- [ ] **L3** Joint distributions, covariance, conditional expectation

### Phase 1 — Stat 135 proper
- [ ] **L4** Ch. 7 — Survey sampling: SRS, estimating a mean/total, standard
      error, finite population correction, stratified sampling
- [ ] **L5** Ch. 8 — Parameters, estimators, the method of moments
- [ ] **L6** Ch. 8 — Maximum likelihood estimation
- [ ] **L7** Ch. 8 — Sampling distributions of MLEs, Fisher information,
      Cramer-Rao, efficiency
- [ ] **L8** Ch. 8 — Sufficiency, the bootstrap, Bayesian estimation
- [ ] **L9** Ch. 9 — Hypothesis testing: Neyman-Pearson, likelihood ratio
      tests, p-values, power, duality with confidence intervals
- [ ] **L10** Ch. 11 — Comparing two samples: t-tests, paired data,
      Mann-Whitney
- [ ] **L11** Ch. 12 — Analysis of variance
- [ ] **L12** Ch. 13 — Categorical data and chi-square tests
- [ ] **L13** Ch. 14 — Linear least squares and regression

## Files
- `lessons/L01-random-variables.md` — lesson text
- `lessons/L01-solutions.md` — worked solutions (try the problems first)
- `lessons/L01-debrief.md` — my error log from attempt 1, and the "where does n come from" rule

## Key formulas so far

    E[aX + b]   = a E[X] + b
    Var(aX + b) = a^2 Var(X)          SD(aX + b) = |a| SD(X)
    Var(X) = E[X^2] - (E[X])^2
    Var(X +/- Y) = Var(X) + Var(Y)    (independent -- variances ADD either way)

    Bernoulli(p):   E = p,    Var = p(1-p)      [only for 0/1 variables]
    Binomial(n,p):  E = np,   Var = np(1-p)
    Sample mean:    E[Xbar] = mu,  SD(Xbar) = sigma/sqrt(n)
    Proportion:     E[phat] = p,   SD(phat) = sqrt(p(1-p)/n)

    z = (X - mu)/sigma                z for 95% = 1.96
    CLT:  Xbar ~approx~ N(mu, sigma^2/n)
    95% CI:  estimate +/- 1.96 * SE

## The protocol (run it on every E/Var problem)

1. Write the row of possible **values** of X.
2. Write the row of **probabilities**. Confirm they sum to 1.
3. Compute E[X], E[X^2], Var = E[X^2] - (E[X])^2.
4. Sanity check: E[X] between min and max value? Var >= 0?
