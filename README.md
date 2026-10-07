# yuzujam

Honeypot observation, data integrity and time-series analysis.
ハニーポットの長期観測と、「欠損を隠さない」データ完全性の研究・開発。

## Featured project

**[self-proving-observation](https://github.com/yuzujam/self-proving-observation)**: a two-site, 90-day honeypot observation platform in which every site sends a one-minute heartbeat, and observation gaps are recorded and disclosed instead of hidden.

[![CI](https://github.com/yuzujam/self-proving-observation/actions/workflows/ci.yml/badge.svg)](https://github.com/yuzujam/self-proving-observation/actions/workflows/ci.yml)

![Observation platform architecture](https://raw.githubusercontent.com/yuzujam/self-proving-observation/main/docs/architecture.svg)

| | |
|---|---|
| Observation | 2 sites, 90 days (2026-07-02 to 2026-09-30) |
| Heartbeat coverage | 99.9853% (central), 99.9830% (edge); every gap is listed |
| Loss outside the heartbeat | 11,495 rows (0.0318%) lost in the backup path, found by hand and disclosed |
| Comparison with T-Pot/ELK | 1 of 20 conditions significant after correction; never worse in any batch; small effect |
| Preprint | [10.5281/zenodo.23177927](https://doi.org/10.5281/zenodo.23177927) |
| Code | [10.5281/zenodo.23178244](https://doi.org/10.5281/zenodo.23178244) |

The write-up states its limits as plainly as its results: there are only two sites, the controlled experiment covers the ingest layer onward, the raw logs could not be kept, and the periodicity analysis found no cycle. A journal version is under review.

## What I work with

Python, FastAPI, Redis, ClickHouse, Docker, Suricata, Vector; pytest, Ruff, mypy, Bandit, Semgrep; PyTorch and SHAP for the drift-detection part of the preprint.

## What I care about

- Not hiding what the system could not observe.
- Designs that keep working when one component stops.
- Reporting what did not work, with the same care as what did.
