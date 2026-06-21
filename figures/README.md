# Figures

Paper-quality figures for the research-paper deliverable, rendered **entirely from committed data**
(`tests/fixtures/scoreboard_golden.json`, the C1 real-data fixtures, and
`results/reports/ground_truth_labels.jsonl`) — no video, GPU, or detection caches — so they
reproduce on a fresh checkout and cannot drift from the published numbers. Every figure's point
values are gated against the golden scoreboard / published headline before it is drawn.

Regenerate:

```bash
uv run --no-sync python scripts/generate_figures.py          # fig_counts / fig_f1_ci / fig_simultaneity
uv run --no-sync python scripts/operating_curve.py           # fig_operating_curve
```

| File | Shows | Backing report |
|---|---|---|
| `fig_counts.png` | Predicted IN (motion, absorption) vs manual GT per camera, with the ±10% count band as grey caps on the GT bar. All four absorption counts land in-band. | [`scoreboard.md`](../scoreboard.md) |
| `fig_f1_ci.png` | Temporal F1 (±15f) per camera/method with bootstrap 95% CIs. CIs overlap on the sparse cameras (C1/C2 — method choice rests on count, not F1) and separate on the dense ones (C3/C4 — absorption significantly beats motion). | [`metric_uncertainty.md`](../metric_uncertainty.md) |
| `fig_simultaneity.png` | Fraction of GT entries sharing a frame, rising monotonically C1→C4 (8/11/17/29%); white labels are the entry rate. This is the structural recall ceiling — near-coincident entries both counters dedup by construction. | [`gt_characterization.md`](../gt_characterization.md) |
| `fig_operating_curve.png` | C1 precision/recall operating curve for both counters, each swept along its recall lever, with the shipped operating point starred. The shipped point is the in-band F1 peak; absorption dominates motion across the curve. | [`operating_curve.md`](../operating_curve.md) |
