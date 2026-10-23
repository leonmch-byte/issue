# A Conceptual Framework for Testing Order-Flow Behavioral Patterns

A thought experiment on whether public market data can reveal persistent order-flow behavior beyond ordinary market-state variables.

## Status

This repository is a conceptual research note and framework proposal. It is not a trading strategy, not an empirical claim, and not a backtest result. The goal is to define the conditions under which such patterns could be meaningfully tested and falsified.

---

## Motivation

Traditional quantitative research often studies the relationship between observable market states and subsequent price movements. Variables such as volatility, trend, volume, and factor exposures are used to estimate conditional distributions of future outcomes.

This project asks a different question:

Can persistent order-flow patterns be inferred from public market data in a way that remains informative beyond standard market-state variables?

The key distinction is that:

- identifying a persistent statistical pattern is not the same as identifying a participant
- observing a public order-book signature is not the same as inferring intent
- a behavioral signal is not valid merely because it appears stable in-sample

This repository is designed to address the research question rigorously: what would count as evidence for or against such patterns?

---

## Core idea

The project tests four hypotheses:

1. Order-flow behavior exhibits persistence
2. Some persistent patterns are observable in public data
3. Observable patterns contain reproducible conditional information
4. A probabilistic observation framework may be justified if the preceding conditions hold

These hypotheses are treated as testable claims, not assumptions.

---

## Hypothesis 1: Persistence

Trading processes, execution algorithms, and risk constraints may generate persistent patterns in order flow. However, persistence at the market level does not imply that the same participant or decision process is always responsible.

A practical test is to represent order-book states as a Markov-style transition system and evaluate whether transitions exhibit non-random persistence beyond simple autoregressive or market-state baselines.

Important constraint:

- states must be defined ex ante
- post hoc state selection is not valid evidence
- persistence must remain stable across rolling sub-samples or be treated as an artifact of market structure

---

## Hypothesis 2: Observability in public data

Potential observable features include:

- order-flow imbalance
- visible depth changes
- queue imbalance
- changes in book shape across multiple time scales

However, observability does not imply discriminability.

Different underlying processes can map to similar public signatures. For example, a reduction in displayed depth may reflect executions, cancellations, modifications, or combinations of these events. If several distinct behaviors project onto the same observable feature vector, then the conditional signal may collapse into noise.

This is a critical weak point in the logic and must be treated as a testable hypothesis rather than an assumption.

---

## Hypothesis 3: Reproducible conditional information

Even if a pattern persists, it may still be explained by ordinary market dynamics rather than a distinct behavioral mechanism.

The next question is therefore:

Do particular feature states contain out-of-sample information about later market states beyond standard baselines?

The goal is not deterministic prediction. The goal is to estimate conditional distributions and evaluate whether they remain informative on unseen data.

---

## Hypothesis 4: Probabilistic observation framework

If the preceding hypotheses receive empirical support, a framework may classify recurring statistical patterns and estimate their conditional distributions.

Such a framework would:

- describe observable market states
- estimate their conditional properties
- specify the conditions under which the relationship breaks down

It would not establish participant identity, intent, or strategy.

---

## Proposed validation framework

| Component | Proposed approach |
|---|---|
| Data | Level 2 order-book snapshots, such as MBP-10; document depth, sampling frequency, venue coverage, and data-quality limits |
| Feature construction | Define imbalance, depth changes, queue structure, and related variables carefully; treat proxies as proxies |
| Temporal separation | Use early data for calibration, middle data for tuning/model selection, and final data for truly out-of-sample evaluation |
| Baselines | Compare against persistence baselines, autoregressive baselines, market-state baselines, and seasonal nulls |
| Conditional distributions | Estimate future-state probabilities and evaluate calibration along with proper scores such as Brier score or log loss |
| Multiple horizons | Evaluate each horizon separately with its own valid sample and uncertainty estimates |
| Costs | Include spread, fees, slippage, and execution costs if economic value is discussed |
| Uncertainty | Use time-series-aware inference; report confidence intervals and sensitivity checks |
| Reproducibility | Predefine hypotheses, features, horizons, models, and failure criteria before final evaluation |

The final out-of-sample evaluation should only occur after analysis choices are fixed. If the results lead to further model changes, a new unseen evaluation period is required.

---

## Known limitations and failure modes

This project explicitly acknowledges several failure modes:

- imperfect observability
- insufficient independent observations
- regime dependence
- survivorship and observation bias
- confounding explanations
- multiple testing and researcher degrees of freedom
- calibration without useful discrimination
- statistical information without economic value
- adversarial non-stationarity
- gap between contemporaneous explanatory power and predictive value

These are not side issues; they are central to the research question.

---

## What would count as evidence against the hypothesis?

A candidate pattern should not be considered validated if:

- its apparent persistence disappears after controlling for market-state and seasonal effects
- it fails to outperform appropriate baseline forecasts on unseen data
- it is highly sensitive to reasonable feature or sampling choices
- its significance vanishes under proper temporal-dependence and multiple-testing corrections
- the uncertainty remains too large to support a meaningful conclusion

Strong negative evidence would include:

- persistence disappearing across several assets and regimes after realistic controls
- conditional distributions failing to beat sensible baselines out-of-sample
- large sensitivity to feature construction or sampling design
- apparent significance collapsing under valid inference
- economic value being below realistic execution costs across tested horizons

---

## Research questions

- Which link in the reasoning is weakest: persistence, observability, conditional information, or the framework itself?
- Can persistence in order-flow features be distinguished from persistence caused by ordinary market dynamics without observing identities?
- Under what conditions can Level 2 snapshot data support meaningful research despite incomplete reconstruction of event-level activity?
- What tests best distinguish genuine structure from artifacts caused by feature selection, regime dependence, or temporal dependence?
- Which studies have found that order-book microstructure signals fail to generalize out of sample, and why?

---

## References and related work

This repository is informed by research in:

- order-flow imbalance
- market microstructure
- order-book dynamics
- evaluation of predictive signals under non-stationarity
- calibration and proper scoring
- adversarial decay of signal quality

The project does not claim to settle these questions. It proposes a disciplined way to test them.

---

## Repository structure

```text
.
├── README.md
├── docs/
│   ├── research-proposal.md
│   ├── hypotheses.md
│   ├── validation-framework.md
│   └── limitations.md
├── references/
│   └── literature-notes.md
├── notebooks/
│   └── exploratory-analysis.ipynb
├── src/
│   └── (optional analysis code)
└── data/
    └── (optional local data notes)
