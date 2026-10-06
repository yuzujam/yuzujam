# yuzujam

Honeypot observation, data integrity and time-series analysis.
ハニーポットの長期観測と、「欠損を隠さない」データ完全性の研究・開発。

## Featured project

**[self-proving-observation](https://github.com/yuzujam/self-proving-observation)**: a two-site, 90-day honeypot observation platform in which every site sends a one-minute heartbeat, and observation gaps are recorded and disclosed instead of hidden.

| | |
|---|---|
| Observation | 2 sites, 90 days (2026-07-02 to 2026-09-30) |
| Heartbeat coverage | 99.9853% (central), 99.9830% (edge) |
| Comparison with T-Pot/ELK | 1 of 20 conditions significant after correction; never worse in any batch |
| Preprint | [10.5281/zenodo.23092261](https://doi.org/10.5281/zenodo.23092261) |

The write-up states its limits as plainly as its results: the drift-detector results come from synthetic time series, there are only two sites, and the periodicity analysis found no cycle.

## What I work with

Python, FastAPI, Redis, ClickHouse, Docker, Suricata, Vector, PyTorch, SHAP

## What I care about

- Not hiding what the system could not observe.
- Designs that keep working when one component stops.
- Reporting what did not work, with the same care as what did.
