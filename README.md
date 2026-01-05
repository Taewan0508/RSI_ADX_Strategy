# RSI–ADX Momentum Strategy: When Filtering Hurts Performance
## Overview

This project investigates whether conditioning an RSI-based momentum strategy with trend strength (ADX) improves risk-adjusted returns.

Contrary to intuition, adding an ADX filter reduced the Sharpe ratio across all tested assets relative to a simpler RSI-only momentum strategy.

This repository focuses on why that happened, what assumptions failed, and what this taught me about signal conditioning in quantitative trading.

### Strategy Summary
Two strategies were evaluated:

**1. RSI-Only Momentum (Baseline)**

- RSI(14) used as a momentum signal
- Direction determined by the slope of a 50-day moving average
- One-unit long/short positioning
- Daily execution with 5 bps transaction cost

**2. RSI + ADX Conditioned Momentum**

- Same RSI momentum logic
- Trades allowed only when ADX(14) exceeded a threshold (strong trend regime)
- Intended to reduce false signals in choppy markets

## Key Result

Across all tested equities (TSLA, NVDA, IREN):
**RSI-only momentum consistently achieved higher Sharpe ratios than RSI conditioned on ADX.**

The ADX filter reduced total exposure and trade count but eliminated profitable trades along with unprofitable ones, leading to lower risk-adjusted returns.

**Why the ADX Filter Reduced Sharpe**
**1. ADX is a Lagging Measure of Trend Strength**

ADX rises after trends are already established.

As a result:

- Early and mid-trend RSI signals were filtered out
- The strategy entered trends later, with reduced remaining momentum
This lowered average trade expectancy.

**2. Feature Redundancy with RSI + MA Slope**
The RSI-only strategy already incorporated:

- Momentum (RSI)
- Directional bias (MA slope)
ADX added highly correlated information rather than orthogonal insight.

Instead of improving signal quality, it duplicated existing trend information and reduced opportunity.

**3. Opportunity Cost Dominated Noise Reduction**
While ADX successfully filtered out some losing trades, it also:

- Removed a larger number of winning trades
- Reduced time-in-market
- Increased turnover due to regime switching

The net effect was lower Sharpe despite lower gross volatility.

**4. Asset-Specific Market Structure**

The tested assets exhibited:

- Persistent directional drift
- Momentum continuation even in moderate ADX regimes

For such assets, requiring “strong trend” confirmation was unnecessarily restrictive.

## Future Directions

Based on these findings, more promising extensions include:

- Using ADX as a position scaler rather than a hard filter
- Applying the strategy to macro-driven assets (FX, commodities)
- Regime classification using volatility or clustering methods
- Portfolio-level evaluation rather than single-asset testing

## Conclusion

The RSI–ADX strategy did not outperform its simpler baseline on a Sharpe-adjusted basis.

However, this outcome provided a valuable lesson:

- More rules do not imply more edge. Signal quality depends on information content, not indicator count.

This repository documents that learning process transparently.

