# yuzujam

Honeypot observation, data integrity and time-series analysis.
ハニーポットの長期観測と、「欠損を隠さない」データ完全性の研究・開発。

**まず見てほしいもの:** 2拠点・90日のハニーポット観測基盤を自分で設計・運用し、「観測できなかった期間」を隠さず定量的に開示する仕組みを作りました。結果だけでなく、反証された仮説や、結果が頑健でない点（保守ジョブとの重なり、認証のない受付）も同じ重さで書いています。詳細は下の Featured project から。

## Featured project

**[self-proving-observation](https://github.com/yuzujam/self-proving-observation)**: a two-site, 90-day honeypot observation platform in which every site sends a one-minute heartbeat, and observation gaps are recorded and disclosed instead of hidden.

[![CI](https://github.com/yuzujam/self-proving-observation/actions/workflows/ci.yml/badge.svg)](https://github.com/yuzujam/self-proving-observation/actions/workflows/ci.yml)

![Observation platform architecture](https://raw.githubusercontent.com/yuzujam/self-proving-observation/main/docs/architecture.svg)

| | |
|---|---|
| Observation | 2 sites, 90 days (2026-07-02 to 2026-09-30) |
| Heartbeat coverage | 99.9853% (central), 99.9830% (edge). Gaps that were found are reported, not excluded or corrected. Read as an upper bound: the ingest endpoints were unauthenticated, so forged heartbeats cannot be ruled out |
| Loss outside the heartbeat | 11,495 rows (0.0318% of 36,147,106) lost in the backup path after ingestion, 98.6% of them on eight days in late July; found after the observation, cause unidentified, disclosed |
| Comparison with T-Pot/ELK | 1 of 20 conditions significant after correction (ramp, 5,000 RPS); never worse in any batch; negligible-to-small effect. Not robust: baseline losses cluster within 30 minutes after a four-hourly maintenance job, and no condition stays significant once trials with 50% or more baseline loss are removed |
| Drift detection | The hypothesis "SHAP changes lead accuracy drops" was refuted. The detector works as a confirming indicator (91.2-96.2% confirmed detection, n=80, synthetic series only) |
| Preprint | [10.5281/zenodo.23177927](https://doi.org/10.5281/zenodo.23177927) |
| Code | [10.5281/zenodo.23178244](https://doi.org/10.5281/zenodo.23178244) |

The write-up states its limits as plainly as its results: only two sites; drift detection validated on synthetic series (one exploratory real-data case, where the control also fired); no periodicity found (absence of evidence at this scale, not evidence of absence); no continuous 90-day resource record; the controlled experiment covers the ingest layer onward; and the raw logs could not be kept. A journal version is under review.

## Where to look

- 設計と結果を読む: [README（日本語・English summary）](https://github.com/yuzujam/self-proving-observation#readme)
- 限界を読む: [限界（隠さずに書く）](https://github.com/yuzujam/self-proving-observation#限界隠さずに書く)
- コードを見る: [`src/`](https://github.com/yuzujam/self-proving-observation/tree/main/src) と [`tests/`](https://github.com/yuzujam/self-proving-observation/tree/main/tests)
- 論文で確認する: [プレプリント](https://doi.org/10.5281/zenodo.23177927)

## What I work with

Python, FastAPI, Redis, ClickHouse, Docker, Suricata, Vector; pytest, Ruff, mypy, Bandit, Semgrep; PyTorch and SHAP for the drift-detection part of the preprint.

## What I care about

- Not hiding what the system could not observe.
- Designs that keep working when one component stops.
- Reporting what did not work, with the same care as what did.
