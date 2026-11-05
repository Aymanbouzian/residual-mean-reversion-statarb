# Residual Mean Reversion / Statistical Arbitrage

Group 2 of the Multi-Strategy Trading on QuantConnect project (Python + QuantConnect LEAN, reproducible in Docker).

**Members:** Ayman, Yassine, Ouisse, Oussama Bouffi

## Research question

Do deviations from a common market/sector relationship mean-revert after costs, and when does that relationship break?

## Research ladder

1. **Control:** simple preselected related ETF pair, training-only hedge estimate, lagged spread z-score. Correlation alone is not evidence of a stationary spread.
2. **Ayman's experiment:** regress returns on market/sector factors over rolling historical windows, build a clearly defined residual state, test whether it predicts subsequent reversal.
3. **Later extension:** PCA residuals, with transformations fitted on training data only (an adaptation of the paper, not an exact replication).
4. **Evaluate:** stationarity/stability, turnover, exposure neutrality, borrow costs, short availability. If shorting is unavailable, document it and use a separately specified feasible variant.
5. **One extension at a time.** Reject the idea if costs remove the effect.

## Ownership

| Person | Focus | First evidence |
| --- | --- | --- |
| Ayman | Residual-model hypothesis and maths; rolling regression/residual feature vs pair baseline | Hypothesis note, residual notebook |
| Yassine | Mean reversion and stationarity; spread/z-score control and stability diagnostics | Pair baseline, diagnostics, limitations |
| Ouisse | Data alignment, adjusted prices, shorting assumptions; dataset checks and report | Aligned data, quality report, benchmark/exposure plots |
| Oussama Bouffi | Walk-forward validation, costs; LEAN execution and integration | Runnable algorithm, cost model, OOS plan |

## Key readings

- Avellaneda and Lee, *Statistical Arbitrage in the U.S. Equities Market*
- statsmodels `coint` and `OLS`

## Repository layout

```
docs/          hypothesis notes, paper notes, strategy spec
research/      notebooks (residual feature, pair baseline, diagnostics)
src/           shared signal / data code
algorithms/    LEAN algorithm(s)
tests/         pytest (signal lag, exposure limits, toy examples)
```

## Rules

- No lookahead: fit scalers, regressions, PCA and HMMs on training windows only.
- Report CAGR, Sharpe (state the convention), max drawdown, turnover, gross/net exposure, costs, borrow/financing assumptions.
- Never commit credentials, LEAN auth files or brokerage keys.
- Every strategy is reviewed by another member. No real-money deployment.
- Record commit, parameters, data source/date range, Docker image tag, costs and output location for every backtest.
